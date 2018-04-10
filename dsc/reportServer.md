---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: A DSC jelentéskészítő kiszolgálójának használata
ms.openlocfilehash: e239414dc30c7458c509392792d4775d04f2311a
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="using-a-dsc-report-server"></a>A DSC jelentéskészítő kiszolgálójának használata

> Vonatkozik: A Windows PowerShell 5.0

>**Megjegyzés:** a jelentéskészítő kiszolgáló, a jelen témakörben ismertetett PowerShell 4.0 nem érhető el.

A helyi Configuration Manager (LCM) egy csomópont beállítható úgy, hogy a konfigurációs állapotára vonatkozó jelentések küldése lekéréses kiszolgálóhoz, lekérdezhető, hogy az adatok beolvasása. Minden alkalommal, amikor a csomópont ellenőrzi, és a beállítások alkalmazása elküldi a jelentést a jelentéskészítő kiszolgáló. Ezek a jelentések egy adatbázis a kiszolgálón tárolja, és a jelentéskészítő webszolgáltatás hívásával kérhető. Az egyes jelentések tartalmaz információkat, például milyen konfigurációk alkalmazott, és hogy sikeresen, az erőforrások használt, esetlegesen előforduló hibák fordultak elő, és indítsa el és befejezési idő.

## <a name="configuring-a-node-to-send-reports"></a>Jelentések küldése a csomópont konfigurálása

Egy csomópont-jelentést küldeni a kiszolgáló használatával biztosítják a **ReportServerWeb** a csomópont LCM konfigurációs letiltása (a LCM konfigurálásával kapcsolatos további információkért lásd: [konfigurálása a helyi Configuration Manager](metaConfig.md) ). A kiszolgáló, amelyhez a csomópont jelentések küldése webkiszolgálóként lekéréses (nem küld jelentéseket SMB-megosztáson) kell beállítani. A lekéréses kiszolgáló beállításával kapcsolatos információkért lásd: [DSC lekérési webkiszolgáló beállítása](pullServer.md). A jelentéskészítő kiszolgáló lehet ugyanazt a szolgáltatást, amelyből a csomópont lekéri a konfigurációt, és lekérdezi az erőforrások, vagy egy másik szolgáltatást.

Az a **ReportServerWeb** blokk, megadhatja az URL-címet, a lekéréses és ismert, hogy a kiszolgáló regisztrációs kulcsot.

A következő konfigurációs csomópont konfigurálja a lekéréses beállításokat egy szolgáltatás, és jelentést küldeni a szolgáltatás egy másik kiszolgálón.

```powershell
[DSCLocalConfigurationManager()]
configuration ReportClientConfig
{
    Node localhost
    {
        Settings
        {
            RefreshMode          = 'Pull'
            RefreshFrequencyMins = 30
            RebootNodeIfNeeded   = $true
        }

        ConfigurationRepositoryWeb CONTOSO-PullSrv
        {
            ServerURL          = 'https://CONTOSO-PULL:8080/PSDSCPullServer.svc'
            RegistrationKey    = 'bbb9778f-43f2-47de-b61e-a0daff474c6d'
            ConfigurationNames = @('ClientConfig')
        }

        ReportServerWeb CONTOSO-ReportSrv
        {
            ServerURL               = 'http://CONTOSO-REPORT:8080/PSDSCReportServer.svc'
            RegistrationKey         = 'ba39daaa-96c5-4f2f-9149-f95c46460faa'
            AllowUnsecureConnection = $true
        }
    }
}
ReportClientConfig
```

A következő konfigurációs egy csomópont egyetlen kiszolgáló használandó konfigurációk, erőforrások és a jelentéskészítés konfigurálása.

```powershell
[DSCLocalConfigurationManager()]
configuration PullClientConfig
{
    Node localhost
    {
        Settings
        {
            RefreshMode = 'Pull'
            RefreshFrequencyMins = 30
            RebootNodeIfNeeded = $true
        }

        ConfigurationRepositoryWeb CONTOSO-PullSrv
        {
            ServerURL = 'https://CONTOSO-PullSrv:8080/PSDSCPullServer.svc'
            RegistrationKey = 'fbc6ef09-ad98-4aad-a062-92b0e0327562'
        }



        ReportServerWeb CONTOSO-ReportSrv
        {
            ServerURL = 'https://CONTOSO-PullSrv:8080/PSDSCPullServer.svc'
        }
    }
}
PullClientConfig
```

>**Megjegyzés:** nevet adhat a webszolgáltatás függetlenül szüksége van, amikor egy lekéréses kiszolgáló, de a **ServerURL** tulajdonságának meg kell egyeznie a szolgáltatás nevét.

## <a name="getting-report-data"></a>A jelentés adatainak beolvasása

A lekérési kiszolgálón a jelentések egy adatbázis-bekerülnek a kiszolgálón. A jelentések és a webszolgáltatás hívás érhetők el. Egy konkrét csomóponthoz tartozó jelentések beolvasása, küldjön egy HTTP-kérelem a jelentéskészítő webszolgáltatás a következő formában: `http://CONTOSO-REPORT:8080/PSDSCReportServer.svc/Nodes(AgentId= 'MyNodeAgentId')/Reports` ahol `MyNodeAgentId` van a csomópont, amelynek le szeretné kérdezni a jelentések ügynökazonosító. Kaphat a ügynökazonosító egy csomópontra hívásával [Get-DscLocalConfigurationManager](https://technet.microsoft.com/library/dn407378.aspx) ezen a csomóponton.

A jelentések, egy JSON-objektumok tömbjét adja vissza.

Az alábbi parancsfájl a csomópont, amelyen fut a jelentéseket adja vissza:

```powershell
function GetReport
{
    param($AgentId = "$((glcm).AgentId)", $serviceURL = "http://CONTOSO-REPORT:8080/PSDSCPullServer.svc")
    $requestUri = "$serviceURL/Nodes(AgentId= '$AgentId')/Reports"
    $request = Invoke-WebRequest -Uri $requestUri  -ContentType "application/json;odata=minimalmetadata;streaming=true;charset=utf-8" `
               -UseBasicParsing -Headers @{Accept = "application/json";ProtocolVersion = "2.0"} `
               -ErrorAction SilentlyContinue -ErrorVariable ev
    $object = ConvertFrom-Json $request.content
    return $object.value
}
```

## <a name="viewing-report-data"></a>A jelentés adatainak megtekintése

Ha eredményét a változó a **GetReport** függvény, megtekintheti az egyes mezők a visszaadott tömb az elemben:

```powershell
$reports = GetReport
$reports[1]


JobId                : 019dfbe5-f99f-11e5-80c6-001dd8b8065c
OperationType        : Consistency
RefreshMode          : Pull
Status               : Success
ReportFormatVersion  : 2.0
ConfigurationVersion : 2.0.0
StartTime            : 04/03/2016 06:21:43
EndTime              : 04/03/2016 06:22:04
RebootRequested      : False
Errors               : {}
StatusData           : {{"StartDate":"2016-04-03T06:21:43.7220000-07:00","IPV6Addresses":["2001:4898:d8:f2f2:852b:b255:b071:283b","fe80::852b:b255:b071
                       :283b%12","::2000:0:0:0","::1","::2000:0:0:0"],"DurationInSeconds":"21","JobID":"{019DFBE5-F99F-11E5-80C6-001DD8B8065C}","Curren
                       tChecksum":"A7797571CB9C3AF4D74C39A0FDA11DAF33273349E1182385528FFC1E47151F7F","MetaData":"Author: configAuthor; Name:
                       Sample_ArchiveFirewall; Version: 2.0.0; GenerationDate: 04/01/2016 15:23:30; GenerationHost: CONTOSO-PullSrv;","RebootRequested":"False
                       ","Status":"Success","IPV4Addresses":["10.240.179.151","127.0.0.1"],"LCMVersion":"2.0","ResourcesNotInDesiredState":[{"SourceInf
                       o":"C:\\ReportTest\\Sample_xFirewall_AddFirewallRule.ps1::23::9::xFirewall","ModuleName":"xNetworking","DurationInSeconds":"8.785",
                       "InstanceName":"Firewall","StartDate":"2016-04-03T06:21:56.4650000-07:00","ResourceName":"xFirewall","ModuleVersion":"2.7.0.0","
                       RebootRequested":"False","ResourceId":"[xFirewall]Firewall","ConfigurationName":"Sample_ArchiveFirewall","InDesiredState":"False
                       "}],"NumberOfResources":"2","Type":"Consistency","HostName":"CONTOSO-PULLCLI","ResourcesInDesiredState":[{"SourceInfo":"C:\\ReportTest\\Sample_xFirewall_AddFirewallRule.ps1::16::9::Archive","ModuleName":"PSDesiredStateConfiguration","DurationInSeconds":"1.848",
                       "InstanceName":"ArchiveExample","StartDate":"2016-04-03T06:21:56.4650000-07:00","ResourceName":"Archive","ModuleVersion":"1.1","
                       RebootRequested":"False","ResourceId":"[Archive]ArchiveExample","ConfigurationName":"Sample_ArchiveFirewall","InDesiredState":"T
                       rue"}],"MACAddresses":["00-1D-D8-B8-06-5C","00-00-00-00-00-00-00-E0"],"MetaConfiguration":{"AgentId":"52DA826D-00DE-4166-8ACB-73F2B46A7E00",
                       "ConfigurationDownloadManagers":[{"SourceInfo":"C:\\ReportTest\\LCMConfig.ps1::14::9::ConfigurationRepositoryWeb","A
                       llowUnsecureConnection":"True","ServerURL":"http://CONTOSO-PullSrv:8080/PSDSCPullServer.svc","RegistrationKey":"","ResourceId":"[Config
                       urationRepositoryWeb]CONTOSO-PullSrv","ConfigurationNames":["ClientConfig"]}],"ActionAfterReboot":"ContinueConfiguration","LCMCo
                       mpatibleVersions":["1.0","2.0"],"LCMState":"Idle","ResourceModuleManagers":[],"ReportManagers":[{"AllowUnsecureConnection":"True
                       ","RegistrationKey":"","ServerURL":"http://CONTOSO-PullSrv:8080/PSDSCPullServer.svc","ResourceId":"[ReportServerWeb]CONTOSO-PullSrv","S
                       ourceInfo":"C:\\ReportTest\\LCMConfig.ps1::24::9::ReportServerWeb"}],"StatusRetentionTimeInDays":"10","LCMVersion":"2.0","Config
                       urationMode":"ApplyAndMonitor","RefreshFrequencyMins":"30","RebootNodeIfNeeded":"True","RefreshMode":"Pull","DebugMode":["NONE"]
                       ,"LCMStateDetail":"","AllowModuleOverwrite":"False","ConfigurationModeFrequencyMins":"15"},"Locale":"en-US","Mode":"Pull"}}
AdditionalData       : {}
```

Alapértelmezés szerint a jelentések szerint vannak rendezve **JobID**. Ahhoz, hogy a legújabb jelentésre, a jelentések szerint rendezve csökkenő **StartTime** tulajdonság, majd a get az első elem a tömb:

```powershell
$reportsByStartTime = $reports | Sort-Object {$_."StartTime" -as [DateTime] } -Descending
$reportMostRecent = $reportsByStartTime[0]
```

Figyelje meg, hogy a **StatusData** tulajdonság-tulajdonság az objektum. Ez a ahol nagy részét a jelentési adatokat. Vizsgáljuk meg az egyes mezőit a **StatusData** tulajdonság a legutóbbi jelentés:

```powershell
$statusData = $reportMostRecent.StatusData | ConvertFrom-Json
$statusData

StartDate                  : 2016-04-04T11:21:41.2990000-07:00
IPV6Addresses              : {2001:4898:d8:f2f2:852b:b255:b071:283b, fe80::852b:b255:b071:283b%12, ::2000:0:0:0, ::1...}
DurationInSeconds          : 25
JobID                      : {135D230E-FA92-11E5-80C6-001DD8B8065C}
CurrentChecksum            : A7797571CB9C3AF4D74C39A0FDA11DAF33273349E1182385528FFC1E47151F7F
MetaData                   : Author: configAuthor; Name: Sample_ArchiveFirewall; Version: 2.0.0; GenerationDate: 04/01/2016 15:23:30; GenerationHost:
                             CONTOSO-PullSrv;
RebootRequested            : False
Status                     : Success
IPV4Addresses              : {10.240.179.151, 127.0.0.1}
LCMVersion                 : 2.0
ResourcesNotInDesiredState : {@{SourceInfo=C:\ReportTest\Sample_xFirewall_AddFirewallRule.ps1::23::9::xFirewall; ModuleName=xNetworking;
                             DurationInSeconds=10.725; InstanceName=Firewall; StartDate=2016-04-04T11:21:55.7200000-07:00; ResourceName=xFirewall;
                             ModuleVersion=2.7.0.0; RebootRequested=False; ResourceId=[xFirewall]Firewall; ConfigurationName=Sample_ArchiveFirewall;
                             InDesiredState=False}}
NumberOfResources          : 2
Type                       : Consistency
HostName                   : CONTOSO-PULLCLI
ResourcesInDesiredState    : {@{SourceInfo=C:\ReportTest\Sample_xFirewall_AddFirewallRule.ps1::16::9::Archive; ModuleName=PSDesiredStateConfiguration;
                             DurationInSeconds=2.672; InstanceName=ArchiveExample; StartDate=2016-04-04T11:21:55.7200000-07:00; ResourceName=Archive;
                             ModuleVersion=1.1; RebootRequested=False; ResourceId=[Archive]ArchiveExample; ConfigurationName=Sample_ArchiveFirewall;
                             InDesiredState=True}}
MACAddresses               : {00-1D-D8-B8-06-5C, 00-00-00-00-00-00-00-E0}
MetaConfiguration          : @{AgentId=52DA826D-00DE-4166-8ACB-73F2B46A7E00; ConfigurationDownloadManagers=System.Object[];
                             ActionAfterReboot=ContinueConfiguration; LCMCompatibleVersions=System.Object[]; LCMState=Idle;
                             ResourceModuleManagers=System.Object[]; ReportManagers=System.Object[]; StatusRetentionTimeInDays=10; LCMVersion=2.0;
                             ConfigurationMode=ApplyAndMonitor; RefreshFrequencyMins=30; RebootNodeIfNeeded=True; RefreshMode=Pull;
                             DebugMode=System.Object[]; LCMStateDetail=; AllowModuleOverwrite=False; ConfigurationModeFrequencyMins=15}
Locale                     : en-US
Mode                       : Pull
```

Ez a többek között a, hogy a legfrissebb konfigurálási két erőforrások, neve és, hogy az egyik legyen a megfelelő állapotban, és ezek egyikét nem jeleníti meg. Csak a, közérthetőbb kimenete kaphat **ResourcesNotInDesiredState** tulajdonság:

```powershell
$statusData.ResourcesInDesiredState

SourceInfo        : C:\ReportTest\Sample_xFirewall_AddFirewallRule.ps1::16::9::Archive
ModuleName        : PSDesiredStateConfiguration
DurationInSeconds : 2.672
InstanceName      : ArchiveExample
StartDate         : 2016-04-04T11:21:55.7200000-07:00
ResourceName      : Archive
ModuleVersion     : 1.1
RebootRequested   : False
ResourceId        : [Archive]ArchiveExample
ConfigurationName : Sample_ArchiveFirewall
InDesiredState    : True
```

Figyelje meg, hogy ezek a példák úgy van kialakítva, hogy adjon meg egy meghatározni, hogy mit tehet a jelentés adataival. Bevezető JSON a PowerShell használatával, lásd: [játszik JSON és a PowerShell és](https://blogs.technet.microsoft.com/heyscriptingguy/2015/10/08/playing-with-json-and-powershell/).

## <a name="see-also"></a>Lásd még:
- [A helyi Configuration Manager konfigurálása](metaConfig.md)
- [A DSC lekérési webkiszolgáló beállítása](pullServer.md)
- [Lekérési ügyfél beállítása konfigurációs nevekkel](pullClientConfigNames.md)