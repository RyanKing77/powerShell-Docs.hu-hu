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
# <a name="using-a-dsc-report-server"></a><span data-ttu-id="e8dd4-103">A DSC jelentéskészítő kiszolgálójának használata</span><span class="sxs-lookup"><span data-stu-id="e8dd4-103">Using a DSC report server</span></span>

<span data-ttu-id="e8dd4-104">Érvényes: Windows PowerShell 5,0</span><span class="sxs-lookup"><span data-stu-id="e8dd4-104">Applies To: Windows PowerShell 5.0</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e8dd4-105">A lekérési kiszolgáló (Windows *-szolgáltatás DSC-Service*) a Windows Server támogatott összetevője, azonban nincsenek új funkciók vagy képességek kínáló csomagok.</span><span class="sxs-lookup"><span data-stu-id="e8dd4-105">The Pull Server (Windows Feature *DSC-Service*) is a supported component of Windows Server however there are no plans to offer new features or capabilities.</span></span> <span data-ttu-id="e8dd4-106">Ajánlott megkezdeni a felügyelt ügyfelek átváltását [Azure Automation DSC](/azure/automation/automation-dsc-getting-started) -re (beleértve a Windows Serveren futó lekéréses kiszolgálón túli szolgáltatásokat) vagy az [itt](pullserver.md#community-solutions-for-pull-service)felsorolt közösségi megoldások egyikét.</span><span class="sxs-lookup"><span data-stu-id="e8dd4-106">It is recommended to begin transitioning managed clients to [Azure Automation DSC](/azure/automation/automation-dsc-getting-started) (includes features beyond Pull Server on Windows Server) or one of the community solutions listed [here](pullserver.md#community-solutions-for-pull-service).</span></span>
>
> [!NOTE]
> <span data-ttu-id="e8dd4-107">A jelen témakörben ismertetett jelentéskészítő kiszolgáló nem érhető el a PowerShell 4,0-ben.</span><span class="sxs-lookup"><span data-stu-id="e8dd4-107">The report server described in this topic is not available in PowerShell 4.0.</span></span>

<span data-ttu-id="e8dd4-108">A csomópontok helyi Configuration Manager (LCD ChipOnGlas) beállítható úgy, hogy a konfigurációs állapotáról jelentéseket küldjön egy lekéréses kiszolgálónak, amely ezután lekérdezhető az adott adat lekéréséhez.</span><span class="sxs-lookup"><span data-stu-id="e8dd4-108">The Local Configuration Manager (LCM) of a node can be configured to send reports about its configuration status to a pull server, which can then be queried to retrieve that data.</span></span> <span data-ttu-id="e8dd4-109">Minden alkalommal, amikor a csomópont ellenőrzi és alkalmazza a konfigurációt, jelentést küld a jelentéskészítő kiszolgálónak.</span><span class="sxs-lookup"><span data-stu-id="e8dd4-109">Each time the node checks and applies a configuration, it sends a report to the report server.</span></span> <span data-ttu-id="e8dd4-110">Ezeket a jelentéseket a rendszer egy adatbázisban tárolja a-kiszolgálón, és a jelentéskészítő webszolgáltatás meghívásával kérhető le.</span><span class="sxs-lookup"><span data-stu-id="e8dd4-110">These reports are stored in a database on the server, and can be retrieved by calling the reporting web service.</span></span> <span data-ttu-id="e8dd4-111">Minden jelentés olyan információkat tartalmaz, mint például az alkalmazott konfigurációk, és hogy sikeresek voltak-e, a felhasznált erőforrások, az eldobott hibák, valamint az Indítás és a Befejezés időpontja.</span><span class="sxs-lookup"><span data-stu-id="e8dd4-111">Each report contains information such as what configurations were applied and whether they succeeded, the resources used, any errors that were thrown, and start and finish times.</span></span>

## <a name="configuring-a-node-to-send-reports"></a><span data-ttu-id="e8dd4-112">Csomópont konfigurálása jelentések küldéséhez</span><span class="sxs-lookup"><span data-stu-id="e8dd4-112">Configuring a node to send reports</span></span>

<span data-ttu-id="e8dd4-113">Ha azt szeretné, hogy egy csomópont egy **ReportServerWeb** blokk használatával küldjön jelentéseket egy kiszolgálónak a csomópont LCD-konfigurációjában (az LCD-k konfigurálásával kapcsolatban lásd: [a helyi Configuration Manager konfigurálása](../managing-nodes/metaConfig.md)).</span><span class="sxs-lookup"><span data-stu-id="e8dd4-113">You tell a node to send reports to a server by using a **ReportServerWeb** block in the node's LCM configuration (for information about configuring the LCM, see [Configuring the Local Configuration Manager](../managing-nodes/metaConfig.md)).</span></span> <span data-ttu-id="e8dd4-114">A kiszolgálót, amelyhez a csomópont küld jelentéseket, webes lekéréses kiszolgálónak kell beállítani (nem küldhet jelentéseket SMB-megosztásra).</span><span class="sxs-lookup"><span data-stu-id="e8dd4-114">The server to which the node sends reports must be set up as a web pull server (you cannot send reports to an SMB share).</span></span> <span data-ttu-id="e8dd4-115">A lekéréses kiszolgáló beállításával kapcsolatos információkért lásd: [DSC webes lekéréses kiszolgáló beállítása](pullServer.md).</span><span class="sxs-lookup"><span data-stu-id="e8dd4-115">For information about setting up a pull server, see [Setting up a DSC web pull server](pullServer.md).</span></span> <span data-ttu-id="e8dd4-116">A jelentéskészítő kiszolgáló lehet ugyanaz a szolgáltatás, amelyről a csomópont lekéri a konfigurációkat, és erőforrásokat kap, vagy más szolgáltatás lehet.</span><span class="sxs-lookup"><span data-stu-id="e8dd4-116">The report server can be the same service from which the node pulls configurations and gets resources, or it can be a different service.</span></span>

<span data-ttu-id="e8dd4-117">A **ReportServerWeb** blokkban meg kell adnia a lekéréses szolgáltatás URL-címét és a kiszolgáló által ismert regisztrációs kulcsot.</span><span class="sxs-lookup"><span data-stu-id="e8dd4-117">In the **ReportServerWeb** block, you specify the URL of the pull service and a registration key that is known to the server.</span></span>

<span data-ttu-id="e8dd4-118">A következő konfiguráció úgy konfigurálja a csomópontot, hogy lekérje a konfigurációk egyik szolgáltatásból való lekérését, és jelentéseket küldjön egy másik kiszolgálón lévő szolgáltatásnak.</span><span class="sxs-lookup"><span data-stu-id="e8dd4-118">The following configuration configures a node to pull configurations from one service, and send reports to a service on a different server.</span></span>

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

<span data-ttu-id="e8dd4-119">A következő konfiguráció úgy konfigurálja a csomópontot, hogy egyetlen kiszolgálót használjon a konfigurációkhoz, az erőforrásokhoz és a jelentéskészítéshez.</span><span class="sxs-lookup"><span data-stu-id="e8dd4-119">The following configuration configures a node to use a single server for configurations, resources, and reporting.</span></span>

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
> <span data-ttu-id="e8dd4-120">A webszolgáltatást a lekéréses kiszolgáló beállításakor is elnevezheti, de a **ServerURL** tulajdonságnak meg kell egyeznie a szolgáltatás nevével.</span><span class="sxs-lookup"><span data-stu-id="e8dd4-120">You can name the web service whatever you want when you set up a pull server, but the **ServerURL** property must match the service name.</span></span>

## <a name="getting-report-data"></a><span data-ttu-id="e8dd4-121">Jelentésadatok beolvasása</span><span class="sxs-lookup"><span data-stu-id="e8dd4-121">Getting report data</span></span>

<span data-ttu-id="e8dd4-122">A lekérési kiszolgálónak elküldett jelentéseket a rendszer egy adatbázisba írja be a kiszolgálón.</span><span class="sxs-lookup"><span data-stu-id="e8dd4-122">Reports sent to the pull server are entered into a database on the server.</span></span> <span data-ttu-id="e8dd4-123">A jelentések a webszolgáltatás hívásával érhetők el.</span><span class="sxs-lookup"><span data-stu-id="e8dd4-123">The reports are available through calls to the web service.</span></span> <span data-ttu-id="e8dd4-124">Egy adott csomópont jelentésének lekéréséhez küldjön egy HTTP-kérelmet a jelentés webszolgáltatásának a következő formában:`http://CONTOSO-REPORT:8080/PSDSCReportServer.svc/Nodes(AgentId='MyNodeAgentId')/Reports`</span><span class="sxs-lookup"><span data-stu-id="e8dd4-124">To retrieve reports for a specific node, send an HTTP request to the report web service in the following form: `http://CONTOSO-REPORT:8080/PSDSCReportServer.svc/Nodes(AgentId='MyNodeAgentId')/Reports`</span></span>
<span data-ttu-id="e8dd4-125">ahol `MyNodeAgentId` az a csomópont ügynökazonosító, amelyhez jelentést szeretne kapni.</span><span class="sxs-lookup"><span data-stu-id="e8dd4-125">where `MyNodeAgentId` is the AgentId of the node for which you want to get reports.</span></span> <span data-ttu-id="e8dd4-126">A csomópont ügynökazonosító lekéréséhez hívja meg a [Get-DscLocalConfigurationManager](/powershell/module/PSDesiredStateConfiguration/Get-DscLocalConfigurationManager) ezen a csomóponton.</span><span class="sxs-lookup"><span data-stu-id="e8dd4-126">You can get the AgentID for a node by calling [Get-DscLocalConfigurationManager](/powershell/module/PSDesiredStateConfiguration/Get-DscLocalConfigurationManager) on that node.</span></span>

<span data-ttu-id="e8dd4-127">A jelentések JSON-objektumok tömbje lesznek visszaadva.</span><span class="sxs-lookup"><span data-stu-id="e8dd4-127">The reports are returned as an array of JSON objects.</span></span>

<span data-ttu-id="e8dd4-128">A következő parancsfájl a futtatott csomópont jelentéseit adja vissza:</span><span class="sxs-lookup"><span data-stu-id="e8dd4-128">The following script returns the reports for the node on which it is run:</span></span>

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

## <a name="viewing-report-data"></a><span data-ttu-id="e8dd4-129">Jelentési információ megtekintése</span><span class="sxs-lookup"><span data-stu-id="e8dd4-129">Viewing report data</span></span>

<span data-ttu-id="e8dd4-130">Ha változót állít be a **GetReport** függvény eredményére, megtekintheti az egyes mezőket a visszaadott tömb elemeiben:</span><span class="sxs-lookup"><span data-stu-id="e8dd4-130">If you set a variable to the result of the **GetReport** function, you can view the individual fields in an element of the array that is returned:</span></span>

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

<span data-ttu-id="e8dd4-131">Alapértelmezés szerint a jelentések a **JobID**szerint vannak rendezve.</span><span class="sxs-lookup"><span data-stu-id="e8dd4-131">By default, the reports are sorted by **JobID**.</span></span> <span data-ttu-id="e8dd4-132">A legfrissebb jelentés beszerzéséhez rendezheti a jelentéseket csökkenő kezdési tulajdonság szerint , majd beolvashatja a tömb első elemét:</span><span class="sxs-lookup"><span data-stu-id="e8dd4-132">To get the most recent report, you can sort the reports by descending **StartTime** property, and then get the first element of the array:</span></span>

```powershell
$reportsByStartTime = $reports | Sort-Object {$_."StartTime" -as [DateTime] } -Descending
$reportMostRecent = $reportsByStartTime[0]
```

<span data-ttu-id="e8dd4-133">Figyelje meg, hogy a **StatusData** tulajdonság számos tulajdonsággal rendelkező objektum.</span><span class="sxs-lookup"><span data-stu-id="e8dd4-133">Notice that the **StatusData** property is an object with a number of properties.</span></span> <span data-ttu-id="e8dd4-134">A jelentéskészítési adatmennyiség nagy része.</span><span class="sxs-lookup"><span data-stu-id="e8dd4-134">This is where much of the reporting data is.</span></span> <span data-ttu-id="e8dd4-135">Nézzük meg a legutóbbi jelentés **StatusData** tulajdonságának egyes mezőit:</span><span class="sxs-lookup"><span data-stu-id="e8dd4-135">Let's look at the individual fields of the **StatusData** property for the most recent report:</span></span>

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

<span data-ttu-id="e8dd4-136">Ez többek között azt mutatja, hogy a legújabb konfiguráció két erőforrásnak nevezett, és hogy ezek egyike a kívánt állapotban volt, és egyikük sem volt.</span><span class="sxs-lookup"><span data-stu-id="e8dd4-136">Among other things, this shows that the most recent configuration called two resources, and that one of them was in the desired state, and one of them was not.</span></span> <span data-ttu-id="e8dd4-137">A **ResourcesNotInDesiredState** tulajdonságnak csak olvasható kimenete lehet:</span><span class="sxs-lookup"><span data-stu-id="e8dd4-137">You can get a more readable output of just the **ResourcesNotInDesiredState** property:</span></span>

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

<span data-ttu-id="e8dd4-138">Vegye figyelembe, hogy ezek a példák azt mutatják be, hogy mit tehet a jelentésekkel kapcsolatos adattal.</span><span class="sxs-lookup"><span data-stu-id="e8dd4-138">Note that these examples are meant to give you an idea of what you can do with report data.</span></span> <span data-ttu-id="e8dd4-139">A JSON a PowerShellben való használatáról további információt a következő témakörben talál: a [JSON és a PowerShell lejátszása](https://blogs.technet.microsoft.com/heyscriptingguy/2015/10/08/playing-with-json-and-powershell/).</span><span class="sxs-lookup"><span data-stu-id="e8dd4-139">For an introduction on working with JSON in PowerShell, see [Playing with JSON and PowerShell](https://blogs.technet.microsoft.com/heyscriptingguy/2015/10/08/playing-with-json-and-powershell/).</span></span>

## <a name="see-also"></a><span data-ttu-id="e8dd4-140">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="e8dd4-140">See Also</span></span>

[<span data-ttu-id="e8dd4-141">A helyi Configuration Manager konfigurálása</span><span class="sxs-lookup"><span data-stu-id="e8dd4-141">Configuring the Local Configuration Manager</span></span>](../managing-nodes/metaConfig.md)

[<span data-ttu-id="e8dd4-142">DSC web pull-kiszolgáló beállítása</span><span class="sxs-lookup"><span data-stu-id="e8dd4-142">Setting up a DSC web pull server</span></span>](pullServer.md)

[<span data-ttu-id="e8dd4-143">Lekérési ügyfél beállítása konfigurációs nevekkel</span><span class="sxs-lookup"><span data-stu-id="e8dd4-143">Setting up a pull client using configuration names</span></span>](pullClientConfigNames.md)
