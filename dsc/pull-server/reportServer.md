---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: A DSC jelentéskészítő kiszolgálójának használata
ms.openlocfilehash: 73208477a74ff3c615d7d515fcad555beabe8f32
ms.sourcegitcommit: caac7d098a448232304c9d6728e7340ec7517a71
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/16/2019
ms.locfileid: "58059269"
---
# <a name="using-a-dsc-report-server"></a><span data-ttu-id="1624e-103">A DSC jelentéskészítő kiszolgálójának használata</span><span class="sxs-lookup"><span data-stu-id="1624e-103">Using a DSC report server</span></span>

<span data-ttu-id="1624e-104">Érvényes: Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="1624e-104">Applies To: Windows PowerShell 5.0</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1624e-105">A lekéréses kiszolgálón (Windows-szolgáltatás *DSC-szolgáltatás*), a Windows Server támogatott összetevője létezik azonban tervekben sem funkciókat és képességeket kínálnak.</span><span class="sxs-lookup"><span data-stu-id="1624e-105">The Pull Server (Windows Feature *DSC-Service*) is a supported component of Windows Server however there are no plans to offer new features or capabilities.</span></span> <span data-ttu-id="1624e-106">Javasoljuk, hogy helyeződnek felügyelt ügyfelek [Azure Automation DSC](/azure/automation/automation-dsc-getting-started) (beleértve a lekéréses kiszolgálón a Windows Server csomagban) vagy a közösségi megoldások felsorolt [Itt](pullserver.md#community-solutions-for-pull-service).</span><span class="sxs-lookup"><span data-stu-id="1624e-106">It is recommended to begin transitioning managed clients to [Azure Automation DSC](/azure/automation/automation-dsc-getting-started) (includes features beyond Pull Server on Windows Server) or one of the community solutions listed [here](pullserver.md#community-solutions-for-pull-service).</span></span>
>
> [!NOTE]
> <span data-ttu-id="1624e-107">A jelen témakörben található jelentéskészítő kiszolgáló nem érhető el a PowerShell 4.0-s verzióját.</span><span class="sxs-lookup"><span data-stu-id="1624e-107">The report server described in this topic is not available in PowerShell 4.0.</span></span>

<span data-ttu-id="1624e-108">A helyi Configuration Manager (LCM) Konfigurálása a csomópont beállítható úgy, hogy a konfiguráció állapotára vonatkozó jelentések küldése egy lekéréses kiszolgálóra, amely lekérdezhetők az adatok lekéréséhez.</span><span class="sxs-lookup"><span data-stu-id="1624e-108">The Local Configuration Manager (LCM) of a node can be configured to send reports about its configuration status to a pull server, which can then be queried to retrieve that data.</span></span> <span data-ttu-id="1624e-109">Minden alkalommal, amikor a csomópont ellenőrzi, és alkalmazza a konfigurációt, küld egy jelentést a jelentéskészítő kiszolgálón.</span><span class="sxs-lookup"><span data-stu-id="1624e-109">Each time the node checks and applies a configuration, it sends a report to the report server.</span></span> <span data-ttu-id="1624e-110">Ezek a jelentések egy adatbázist a kiszolgálón vannak tárolva, és a jelentéskészítő webszolgáltatáshoz meghívásával lekérhető.</span><span class="sxs-lookup"><span data-stu-id="1624e-110">These reports are stored in a database on the server, and can be retrieved by calling the reporting web service.</span></span> <span data-ttu-id="1624e-111">Az egyes jelentések tartalmaz információkat, például alkalmazott mely konfigurációkat, és azok sikeres volt-e, használja az erőforrásokat, esetlegesen előforduló hibák fordultak elő, és indítsa el, és a befejezési idő.</span><span class="sxs-lookup"><span data-stu-id="1624e-111">Each report contains information such as what configurations were applied and whether they succeeded, the resources used, any errors that were thrown, and start and finish times.</span></span>

## <a name="configuring-a-node-to-send-reports"></a><span data-ttu-id="1624e-112">Egy csomópont küldeni a jelentéseket konfigurálása</span><span class="sxs-lookup"><span data-stu-id="1624e-112">Configuring a node to send reports</span></span>

<span data-ttu-id="1624e-113">Egy csomópont küldeni a jelentéseket egy kiszolgálót a használatával megadhatja egy **ReportServerWeb** blokkolja a csomópont LCM konfigurálása a (További információ az LCM konfigurálása: [a Local Configuration Manager](../managing-nodes/metaConfig.md) ).</span><span class="sxs-lookup"><span data-stu-id="1624e-113">You tell a node to send reports to a server by using a **ReportServerWeb** block in the node's LCM configuration (for information about configuring the LCM, see [Configuring the Local Configuration Manager](../managing-nodes/metaConfig.md)).</span></span> <span data-ttu-id="1624e-114">Lekérési kiszolgáló (nem küld jelentéseket egy SMB-megosztás), a kiszolgáló, amelyhez a csomópont küld jelentéseket kell beállítani.</span><span class="sxs-lookup"><span data-stu-id="1624e-114">The server to which the node sends reports must be set up as a web pull server (you cannot send reports to an SMB share).</span></span> <span data-ttu-id="1624e-115">Lekérési kiszolgáló beállításával kapcsolatos további információkért lásd: [DSC lekérési kiszolgáló beállítása](pullServer.md).</span><span class="sxs-lookup"><span data-stu-id="1624e-115">For information about setting up a pull server, see [Setting up a DSC web pull server](pullServer.md).</span></span> <span data-ttu-id="1624e-116">A jelentéskészítő kiszolgáló ugyanazt a szolgáltatást, amelyből a csomópont lekéri a konfigurációt, és megjeleníti az erőforrást, vagy lehet egy másik szolgáltatás.</span><span class="sxs-lookup"><span data-stu-id="1624e-116">The report server can be the same service from which the node pulls configurations and gets resources, or it can be a different service.</span></span>

<span data-ttu-id="1624e-117">Az a **ReportServerWeb** letiltása, akkor adja meg az URL-címét a lekérési szolgáltatást és az ismert, hogy a kiszolgáló regisztrációs kulcsot.</span><span class="sxs-lookup"><span data-stu-id="1624e-117">In the **ReportServerWeb** block, you specify the URL of the pull service and a registration key that is known to the server.</span></span>

<span data-ttu-id="1624e-118">Az alábbi beállításokkal konfigurálja a pull-konfigurációkat csomópont egy szolgáltatásból, és küldeni a jelentéseket a szolgáltatás egy másik kiszolgálóra.</span><span class="sxs-lookup"><span data-stu-id="1624e-118">The following configuration configures a node to pull configurations from one service, and send reports to a service on a different server.</span></span>

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

<span data-ttu-id="1624e-119">A következő konfigurációt konfigurálja egy csomópontot egy egykiszolgálós használandó konfigurációk, az erőforrások és a jelentéskészítés.</span><span class="sxs-lookup"><span data-stu-id="1624e-119">The following configuration configures a node to use a single server for configurations, resources, and reporting.</span></span>

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
> <span data-ttu-id="1624e-120">Nevet adhat a webszolgáltatás akármilyen területen is szüksége van, amikor egy lekéréses kiszolgálót beállította, de a **ServerURL** tulajdonságának meg kell egyeznie a szolgáltatás nevét.</span><span class="sxs-lookup"><span data-stu-id="1624e-120">You can name the web service whatever you want when you set up a pull server, but the **ServerURL** property must match the service name.</span></span>

## <a name="getting-report-data"></a><span data-ttu-id="1624e-121">A jelentés adatainak lekérése</span><span class="sxs-lookup"><span data-stu-id="1624e-121">Getting report data</span></span>

<span data-ttu-id="1624e-122">A lekéréses kiszolgálóra küldött jelentések bekerülnek egy adatbázist a kiszolgálón.</span><span class="sxs-lookup"><span data-stu-id="1624e-122">Reports sent to the pull server are entered into a database on the server.</span></span> <span data-ttu-id="1624e-123">A jelentések a webszolgáltatás hívásainak keresztül érhetők el.</span><span class="sxs-lookup"><span data-stu-id="1624e-123">The reports are available through calls to the web service.</span></span> <span data-ttu-id="1624e-124">Egy adott csomópont jelentések lekéréséhez a HTTP-kérelem küldése a jelentéskészítő webszolgáltatás a következő formátumban: `http://CONTOSO-REPORT:8080/PSDSCReportServer.svc/Nodes(AgentId='MyNodeAgentId')/Reports`</span><span class="sxs-lookup"><span data-stu-id="1624e-124">To retrieve reports for a specific node, send an HTTP request to the report web service in the following form: `http://CONTOSO-REPORT:8080/PSDSCReportServer.svc/Nodes(AgentId='MyNodeAgentId')/Reports`</span></span>
<span data-ttu-id="1624e-125">ahol `MyNodeAgentId` a csomópont, amelynek meg szeretné jelentések lekérése a ügynökazonosító van.</span><span class="sxs-lookup"><span data-stu-id="1624e-125">where `MyNodeAgentId` is the AgentId of the node for which you want to get reports.</span></span> <span data-ttu-id="1624e-126">Megtekintheti a ügynökazonosító egy csomópont meghívásával [Get-DscLocalConfigurationManager](/powershell/module/PSDesiredStateConfiguration/Get-DscLocalConfigurationManager) ezen a csomóponton.</span><span class="sxs-lookup"><span data-stu-id="1624e-126">You can get the AgentID for a node by calling [Get-DscLocalConfigurationManager](/powershell/module/PSDesiredStateConfiguration/Get-DscLocalConfigurationManager) on that node.</span></span>

<span data-ttu-id="1624e-127">A jelentéseket a rendszer JSON-objektumok tömbjeként adja vissza.</span><span class="sxs-lookup"><span data-stu-id="1624e-127">The reports are returned as an array of JSON objects.</span></span>

<span data-ttu-id="1624e-128">A következő parancsfájl a csomópont, amelyen fut a jelentések adja vissza:</span><span class="sxs-lookup"><span data-stu-id="1624e-128">The following script returns the reports for the node on which it is run:</span></span>

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

## <a name="viewing-report-data"></a><span data-ttu-id="1624e-129">A jelentés adatainak megtekintése</span><span class="sxs-lookup"><span data-stu-id="1624e-129">Viewing report data</span></span>

<span data-ttu-id="1624e-130">Ha a változó eredménye a **GetReport** függvény, megtekintheti az egyes mezők a visszaadott tömb elem:</span><span class="sxs-lookup"><span data-stu-id="1624e-130">If you set a variable to the result of the **GetReport** function, you can view the individual fields in an element of the array that is returned:</span></span>

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

<span data-ttu-id="1624e-131">Alapértelmezés szerint a jelentések szerint vannak rendezve **JobID**.</span><span class="sxs-lookup"><span data-stu-id="1624e-131">By default, the reports are sorted by **JobID**.</span></span> <span data-ttu-id="1624e-132">A legutolsó jelentés lekéréséhez a jelentések szerint rendezve csökkenő **StartTime** tulajdonság, majd a get az első elem a tömb:</span><span class="sxs-lookup"><span data-stu-id="1624e-132">To get the most recent report, you can sort the reports by descending **StartTime** property, and then get the first element of the array:</span></span>

```powershell
$reportsByStartTime = $reports | Sort-Object {$_."StartTime" -as [DateTime] } -Descending
$reportMostRecent = $reportsByStartTime[0]
```

<span data-ttu-id="1624e-133">Figyelje meg, hogy a **StatusData** tulajdonság számos tulajdonságot tartalmazó objektumot.</span><span class="sxs-lookup"><span data-stu-id="1624e-133">Notice that the **StatusData** property is an object with a number of properties.</span></span> <span data-ttu-id="1624e-134">Ez a ahol szinte a jelentési adatokat.</span><span class="sxs-lookup"><span data-stu-id="1624e-134">This is where much of the reporting data is.</span></span> <span data-ttu-id="1624e-135">Az egyes mezőkhöz, nézzük meg a **StatusData** tulajdonság a legutóbbi jelentés:</span><span class="sxs-lookup"><span data-stu-id="1624e-135">Let's look at the individual fields of the **StatusData** property for the most recent report:</span></span>

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

<span data-ttu-id="1624e-136">Ez a többek között a, hogy a legfrissebb konfigurálási nevű két erőforrás és, hogy az egyiket a kívánt állapotban volt, és nem volt az egyiket jeleníti meg.</span><span class="sxs-lookup"><span data-stu-id="1624e-136">Among other things, this shows that the most recent configuration called two resources, and that one of them was in the desired state, and one of them was not.</span></span> <span data-ttu-id="1624e-137">Beszerezheti a tárolópéldányhoz kimenete csak a **ResourcesNotInDesiredState** tulajdonság:</span><span class="sxs-lookup"><span data-stu-id="1624e-137">You can get a more readable output of just the **ResourcesNotInDesiredState** property:</span></span>

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

<span data-ttu-id="1624e-138">Vegye figyelembe, hogy ezek a példák van kialakítva, hogy kiválasztani, mire képes a jelentés adataival.</span><span class="sxs-lookup"><span data-stu-id="1624e-138">Note that these examples are meant to give you an idea of what you can do with report data.</span></span> <span data-ttu-id="1624e-139">Megismerni a JSON a PowerShellben való használatáról, tekintse meg [JSON és a PowerShell segítségével játszott](https://blogs.technet.microsoft.com/heyscriptingguy/2015/10/08/playing-with-json-and-powershell/).</span><span class="sxs-lookup"><span data-stu-id="1624e-139">For an introduction on working with JSON in PowerShell, see [Playing with JSON and PowerShell](https://blogs.technet.microsoft.com/heyscriptingguy/2015/10/08/playing-with-json-and-powershell/).</span></span>

## <a name="see-also"></a><span data-ttu-id="1624e-140">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="1624e-140">See Also</span></span>

[<span data-ttu-id="1624e-141">A helyi Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="1624e-141">Configuring the Local Configuration Manager</span></span>](../managing-nodes/metaConfig.md)

[<span data-ttu-id="1624e-142">DSC lekérési kiszolgáló beállítása</span><span class="sxs-lookup"><span data-stu-id="1624e-142">Setting up a DSC web pull server</span></span>](pullServer.md)

[<span data-ttu-id="1624e-143">Lekérési ügyfél beállítása konfigurációs nevekkel</span><span class="sxs-lookup"><span data-stu-id="1624e-143">Setting up a pull client using configuration names</span></span>](pullClientConfigNames.md)