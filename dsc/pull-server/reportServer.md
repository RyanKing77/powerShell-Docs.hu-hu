---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: A DSC jelentéskészítő kiszolgálójának használata
ms.openlocfilehash: 8647f80c311ee49a5cc4d57360472386e01b044e
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55686578"
---
# <a name="using-a-dsc-report-server"></a>A DSC jelentéskészítő kiszolgálójának használata

Érvényes: Windows PowerShell 5.0

> [!IMPORTANT]
> A lekéréses kiszolgálón (Windows-szolgáltatás *DSC-szolgáltatás*), a Windows Server támogatott összetevője létezik azonban tervekben sem funkciókat és képességeket kínálnak. Javasoljuk, hogy helyeződnek felügyelt ügyfelek [Azure Automation DSC](/azure/automation/automation-dsc-getting-started) (beleértve a lekéréses kiszolgálón a Windows Server csomagban) vagy a közösségi megoldások felsorolt [Itt](pullserver.md#community-solutions-for-pull-service).
>
> **Megjegyzés:** a jelen témakörben található jelentéskészítő kiszolgáló nem érhető el a PowerShell 4.0-s verzióját.

A helyi Configuration Manager (LCM) Konfigurálása a csomópont beállítható úgy, hogy a konfiguráció állapotára vonatkozó jelentések küldése egy lekéréses kiszolgálóra, amely lekérdezhetők az adatok lekéréséhez. Minden alkalommal, amikor a csomópont ellenőrzi, és alkalmazza a konfigurációt, küld egy jelentést a jelentéskészítő kiszolgálón. Ezek a jelentések egy adatbázist a kiszolgálón vannak tárolva, és a jelentéskészítő webszolgáltatáshoz meghívásával lekérhető. Az egyes jelentések tartalmaz információkat, például alkalmazott mely konfigurációkat, és azok sikeres volt-e, használja az erőforrásokat, esetlegesen előforduló hibák fordultak elő, és indítsa el, és a befejezési idő.

## <a name="configuring-a-node-to-send-reports"></a>Egy csomópont küldeni a jelentéseket konfigurálása

Egy csomópont küldeni a jelentéseket egy kiszolgálót a használatával megadhatja egy **ReportServerWeb** blokkolja a csomópont LCM konfigurálása a (További információ az LCM konfigurálása: [a Local Configuration Manager](../managing-nodes/metaConfig.md) ). Lekérési kiszolgáló (nem küld jelentéseket egy SMB-megosztás), a kiszolgáló, amelyhez a csomópont küld jelentéseket kell beállítani. Lekérési kiszolgáló beállításával kapcsolatos további információkért lásd: [DSC lekérési kiszolgáló beállítása](pullServer.md). A jelentéskészítő kiszolgáló ugyanazt a szolgáltatást, amelyből a csomópont lekéri a konfigurációt, és megjeleníti az erőforrást, vagy lehet egy másik szolgáltatás.

Az a **ReportServerWeb** letiltása, akkor adja meg az URL-címét a lekérési szolgáltatást és az ismert, hogy a kiszolgáló regisztrációs kulcsot.

Az alábbi beállításokkal konfigurálja a pull-konfigurációkat csomópont egy szolgáltatásból, és küldeni a jelentéseket a szolgáltatás egy másik kiszolgálóra.

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

A következő konfigurációt konfigurálja egy csomópontot egy egykiszolgálós használandó konfigurációk, az erőforrások és a jelentéskészítés.

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

> [!NOTE]
> Nevet adhat a webszolgáltatás akármilyen területen is szüksége van, amikor egy lekéréses kiszolgálót beállította, de a **ServerURL** tulajdonságának meg kell egyeznie a szolgáltatás nevét.

## <a name="getting-report-data"></a>A jelentés adatainak lekérése

A lekéréses kiszolgálóra küldött jelentések bekerülnek egy adatbázist a kiszolgálón. A jelentések a webszolgáltatás hívásainak keresztül érhetők el. Egy adott csomópont jelentések lekéréséhez a HTTP-kérelem küldése a jelentéskészítő webszolgáltatás a következő formátumban: `http://CONTOSO-REPORT:8080/PSDSCReportServer.svc/Nodes(AgentId='MyNodeAgentId')/Reports`
ahol `MyNodeAgentId` a csomópont, amelynek meg szeretné jelentések lekérése a ügynökazonosító van. Megtekintheti a ügynökazonosító egy csomópont meghívásával [Get-DscLocalConfigurationManager](/powershell/module/PSDesiredStateConfiguration/Get-DscLocalConfigurationManager) ezen a csomóponton.

A jelentéseket a rendszer JSON-objektumok tömbjeként adja vissza.

A következő parancsfájl a csomópont, amelyen fut a jelentések adja vissza:

```powershell
function GetReport
{
    param
    (
        $AgentId = "$((glcm).AgentId)", 
        $serviceURL = "http://CONTOSO-REPORT:8080/PSDSCPullServer.svc"
    )

    $requestUri = "$serviceURL/Nodes(AgentId= '$AgentId')/Reports"
    $request = Invoke-WebRequest -Uri $requestUri  -ContentType "application/json;odata=minimalmetadata;streaming=true;charset=utf-8" `
               -UseBasicParsing -Headers @{Accept = "application/json";ProtocolVersion = "2.0"} `
               -ErrorAction SilentlyContinue -ErrorVariable ev
    $object = ConvertFrom-Json $request.content
    return $object.value
}
```

## <a name="viewing-report-data"></a>A jelentés adatainak megtekintése

Ha a változó eredménye a **GetReport** függvény, megtekintheti az egyes mezők a visszaadott tömb elem:

```powershell
$reports = GetReport
$reports[1]
```

```output
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

Alapértelmezés szerint a jelentések szerint vannak rendezve **JobID**. A legutolsó jelentés lekéréséhez a jelentések szerint rendezve csökkenő **StartTime** tulajdonság, majd a get az első elem a tömb:

```powershell
$reportsByStartTime = $reports | Sort-Object {$_."StartTime" -as [DateTime] } -Descending
$reportMostRecent = $reportsByStartTime[0]
```

Figyelje meg, hogy a **StatusData** tulajdonság számos tulajdonságot tartalmazó objektumot. Ez a ahol szinte a jelentési adatokat. Az egyes mezőkhöz, nézzük meg a **StatusData** tulajdonság a legutóbbi jelentés:

```powershell
$statusData = $reportMostRecent.StatusData | ConvertFrom-Json
$statusData
```

```output
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

Ez a többek között a, hogy a legfrissebb konfigurálási nevű két erőforrás és, hogy az egyiket a kívánt állapotban volt, és nem volt az egyiket jeleníti meg. Beszerezheti a tárolópéldányhoz kimenete csak a **ResourcesNotInDesiredState** tulajdonság:

```powershell
$statusData.ResourcesInDesiredState
```

```output
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

Vegye figyelembe, hogy ezek a példák van kialakítva, hogy kiválasztani, mire képes a jelentés adataival. Megismerni a JSON a PowerShellben való használatáról, tekintse meg [JSON és a PowerShell segítségével játszott](https://blogs.technet.microsoft.com/heyscriptingguy/2015/10/08/playing-with-json-and-powershell/).

## <a name="see-also"></a>Lásd még:

[A helyi Configuration Manager](../managing-nodes/metaConfig.md)

[DSC lekérési kiszolgáló beállítása](pullServer.md)

[Lekérési ügyfél beállítása konfigurációs nevekkel](pullClientConfigNames.md)