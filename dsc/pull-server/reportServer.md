---
ms.date: 06/12/2017
keywords: DSC, PowerShell, konfigurálás, beállítás
title: A DSC jelentéskészítő kiszolgálójának használata
ms.openlocfilehash: 1ccd4f96b782b41b7d7c953735cb41b3ba3d2bce
ms.sourcegitcommit: 5a004064f33acc0145ccd414535763e95f998c89
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/23/2019
ms.locfileid: "69986549"
---
# <a name="using-a-dsc-report-server"></a>A DSC jelentéskészítő kiszolgálójának használata

Érvényes: Windows PowerShell 5,0

> [!IMPORTANT]
> A lekérési kiszolgáló (Windows *-szolgáltatás DSC-Service*) a Windows Server támogatott összetevője, azonban nincsenek új funkciók vagy képességek kínáló csomagok. Ajánlott megkezdeni a felügyelt ügyfelek átváltását [Azure Automation DSC](/azure/automation/automation-dsc-getting-started) -re (beleértve a Windows Serveren futó lekéréses kiszolgálón túli szolgáltatásokat) vagy az [itt](pullserver.md#community-solutions-for-pull-service)felsorolt közösségi megoldások egyikét.
>
> [!NOTE]
> A jelen témakörben ismertetett jelentéskészítő kiszolgáló nem érhető el a PowerShell 4,0-ben.

A csomópontok helyi Configuration Manager (LCD ChipOnGlas) beállítható úgy, hogy a konfigurációs állapotáról jelentéseket küldjön egy lekéréses kiszolgálónak, amely ezután lekérdezhető az adott adat lekéréséhez. Minden alkalommal, amikor a csomópont ellenőrzi és alkalmazza a konfigurációt, jelentést küld a jelentéskészítő kiszolgálónak. Ezeket a jelentéseket a rendszer egy adatbázisban tárolja a-kiszolgálón, és a jelentéskészítő webszolgáltatás meghívásával kérhető le. Minden jelentés olyan információkat tartalmaz, mint például az alkalmazott konfigurációk, és hogy sikeresek voltak-e, a felhasznált erőforrások, az eldobott hibák, valamint az Indítás és a Befejezés időpontja.

## <a name="configuring-a-node-to-send-reports"></a>Csomópont konfigurálása jelentések küldéséhez

Ha azt szeretné, hogy egy csomópont egy **ReportServerWeb** blokk használatával küldjön jelentéseket egy kiszolgálónak a csomópont LCD-konfigurációjában (az LCD-k konfigurálásával kapcsolatban lásd: [a helyi Configuration Manager konfigurálása](../managing-nodes/metaConfig.md)). A kiszolgálót, amelyhez a csomópont küld jelentéseket, webes lekéréses kiszolgálónak kell beállítani (nem küldhet jelentéseket SMB-megosztásra). A lekéréses kiszolgáló beállításával kapcsolatos információkért lásd: [DSC webes lekéréses kiszolgáló beállítása](pullServer.md). A jelentéskészítő kiszolgáló lehet ugyanaz a szolgáltatás, amelyről a csomópont lekéri a konfigurációkat, és erőforrásokat kap, vagy más szolgáltatás lehet.

A **ReportServerWeb** blokkban meg kell adnia a lekéréses szolgáltatás URL-címét és a kiszolgáló által ismert regisztrációs kulcsot.

A következő konfiguráció úgy konfigurálja a csomópontot, hogy lekérje a konfigurációk egyik szolgáltatásból való lekérését, és jelentéseket küldjön egy másik kiszolgálón lévő szolgáltatásnak.

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
            ServerURL               = 'http://CONTOSO-REPORT:8080/PSDSCPullServer.svc'
            RegistrationKey         = 'ba39daaa-96c5-4f2f-9149-f95c46460faa'
            AllowUnsecureConnection = $true
        }
    }
}

ReportClientConfig
```

A következő konfiguráció úgy konfigurálja a csomópontot, hogy egyetlen kiszolgálót használjon a konfigurációkhoz, az erőforrásokhoz és a jelentéskészítéshez.

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
> A webszolgáltatást a lekéréses kiszolgáló beállításakor is elnevezheti, de a **ServerURL** tulajdonságnak meg kell egyeznie a szolgáltatás nevével.

## <a name="getting-report-data"></a>Jelentésadatok beolvasása

A lekérési kiszolgálónak elküldett jelentéseket a rendszer egy adatbázisba írja be a kiszolgálón. A jelentések a webszolgáltatás hívásával érhetők el. Egy adott csomópont jelentésének lekéréséhez küldjön egy HTTP-kérelmet a jelentés webszolgáltatásának a következő formában:`http://CONTOSO-REPORT:8080/PSDSCReportServer.svc/Nodes(AgentId='MyNodeAgentId')/Reports`
ahol `MyNodeAgentId` az a csomópont ügynökazonosító, amelyhez jelentést szeretne kapni. A csomópont ügynökazonosító lekéréséhez hívja meg a [Get-DscLocalConfigurationManager](/powershell/module/PSDesiredStateConfiguration/Get-DscLocalConfigurationManager) ezen a csomóponton.

A jelentések JSON-objektumok tömbje lesznek visszaadva.

A következő parancsfájl a futtatott csomópont jelentéseit adja vissza:

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

## <a name="viewing-report-data"></a>Jelentési információ megtekintése

Ha változót állít be a **GetReport** függvény eredményére, megtekintheti az egyes mezőket a visszaadott tömb elemeiben:

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

Alapértelmezés szerint a jelentések a **JobID**szerint vannak rendezve. A legfrissebb jelentés beszerzéséhez rendezheti a jelentéseket csökkenő kezdési tulajdonság szerint , majd beolvashatja a tömb első elemét:

```powershell
$reportsByStartTime = $reports | Sort-Object {$_."StartTime" -as [DateTime] } -Descending
$reportMostRecent = $reportsByStartTime[0]
```

Figyelje meg, hogy a **StatusData** tulajdonság számos tulajdonsággal rendelkező objektum. A jelentéskészítési adatmennyiség nagy része. Nézzük meg a legutóbbi jelentés **StatusData** tulajdonságának egyes mezőit:

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

Ez többek között azt mutatja, hogy a legújabb konfiguráció két erőforrásnak nevezett, és hogy ezek egyike a kívánt állapotban volt, és egyikük sem volt. A **ResourcesNotInDesiredState** tulajdonságnak csak olvasható kimenete lehet:

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

Vegye figyelembe, hogy ezek a példák azt mutatják be, hogy mit tehet a jelentésekkel kapcsolatos adattal. A JSON a PowerShellben való használatáról további információt a következő témakörben talál: a [JSON és a PowerShell lejátszása](https://blogs.technet.microsoft.com/heyscriptingguy/2015/10/08/playing-with-json-and-powershell/).

## <a name="see-also"></a>Lásd még:

[A helyi Configuration Manager konfigurálása](../managing-nodes/metaConfig.md)

[DSC web pull-kiszolgáló beállítása](pullServer.md)

[Lekérési ügyfél beállítása konfigurációs nevekkel](pullClientConfigNames.md)
