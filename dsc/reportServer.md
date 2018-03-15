---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "A DSC-jelentés kiszolgálóval"
ms.openlocfilehash: fdf16a2de6aea46844d3812029fae474e80ae6ac
ms.sourcegitcommit: 99227f62dcf827354770eb2c3e95c5cf6a3118b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/15/2018
---
# <a name="using-a-dsc-report-server"></a><span data-ttu-id="f0b5d-103">A DSC-jelentés kiszolgálóval</span><span class="sxs-lookup"><span data-stu-id="f0b5d-103">Using a DSC report server</span></span>

> <span data-ttu-id="f0b5d-104">Vonatkozik: A Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="f0b5d-104">Applies To: Windows PowerShell 5.0</span></span>

><span data-ttu-id="f0b5d-105">**Megjegyzés:** a jelentéskészítő kiszolgáló, a jelen témakörben ismertetett PowerShell 4.0 nem érhető el.</span><span class="sxs-lookup"><span data-stu-id="f0b5d-105">**Note:** The report server described in this topic is not available in PowerShell 4.0.</span></span>

<span data-ttu-id="f0b5d-106">A helyi Configuration Manager (LCM) egy csomópont beállítható úgy, hogy a konfigurációs állapotára vonatkozó jelentések küldése lekéréses kiszolgálóhoz, lekérdezhető, hogy az adatok beolvasása.</span><span class="sxs-lookup"><span data-stu-id="f0b5d-106">The Local Configuration Manager (LCM) of a node can be configured to send reports about its configuration status to a pull server, which can then be queried to retrieve that data.</span></span> <span data-ttu-id="f0b5d-107">Minden alkalommal, amikor a csomópont ellenőrzi, és a beállítások alkalmazása elküldi a jelentést a jelentéskészítő kiszolgáló.</span><span class="sxs-lookup"><span data-stu-id="f0b5d-107">Each time the node checks and applies a configuration, it sends a report to the report server.</span></span> <span data-ttu-id="f0b5d-108">Ezek a jelentések egy adatbázis a kiszolgálón tárolja, és a jelentéskészítő webszolgáltatás hívásával kérhető.</span><span class="sxs-lookup"><span data-stu-id="f0b5d-108">These reports are stored in a database on the server, and can be retrieved by calling the reporting web service.</span></span> <span data-ttu-id="f0b5d-109">Az egyes jelentések tartalmaz információkat, például milyen konfigurációk alkalmazott, és hogy sikeresen, az erőforrások használt, esetlegesen előforduló hibák fordultak elő, és indítsa el és befejezési idő.</span><span class="sxs-lookup"><span data-stu-id="f0b5d-109">Each report contains information such as what configurations were applied and whether they succeeded, the resources used, any errors that were thrown, and start and finish times.</span></span>

## <a name="configuring-a-node-to-send-reports"></a><span data-ttu-id="f0b5d-110">Jelentések küldése a csomópont konfigurálása</span><span class="sxs-lookup"><span data-stu-id="f0b5d-110">Configuring a node to send reports</span></span>

<span data-ttu-id="f0b5d-111">Egy csomópont-jelentést küldeni a kiszolgáló használatával biztosítják a **ReportServerWeb** a csomópont LCM konfigurációs letiltása (a LCM konfigurálásával kapcsolatos további információkért lásd: [konfigurálása a helyi Configuration Manager](metaConfig.md) ).</span><span class="sxs-lookup"><span data-stu-id="f0b5d-111">You tell a node to send reports to a server by using a **ReportServerWeb** block in the node's LCM configuration (for information about configuring the LCM, see [Configuring the Local Configuration Manager](metaConfig.md)).</span></span> <span data-ttu-id="f0b5d-112">A kiszolgáló, amelyhez a csomópont jelentések küldése webkiszolgálóként lekéréses (nem küld jelentéseket SMB-megosztáson) kell beállítani.</span><span class="sxs-lookup"><span data-stu-id="f0b5d-112">The server to which the node sends reports must be set up as a web pull server (you cannot send reports to an SMB share).</span></span> <span data-ttu-id="f0b5d-113">A lekéréses kiszolgáló beállításával kapcsolatos információkért lásd: [DSC lekérési webkiszolgáló beállítása](pullServer.md).</span><span class="sxs-lookup"><span data-stu-id="f0b5d-113">For information about setting up a pull server, see [Setting up a DSC web pull server](pullServer.md).</span></span> <span data-ttu-id="f0b5d-114">A jelentéskészítő kiszolgáló lehet ugyanazt a szolgáltatást, amelyből a csomópont lekéri a konfigurációt, és lekérdezi az erőforrások, vagy egy másik szolgáltatást.</span><span class="sxs-lookup"><span data-stu-id="f0b5d-114">The report server can be the same service from which the node pulls configurations and gets resources, or it can be a different service.</span></span>
 
<span data-ttu-id="f0b5d-115">Az a **ReportServerWeb** blokk, megadhatja az URL-címet, a lekéréses és ismert, hogy a kiszolgáló regisztrációs kulcsot.</span><span class="sxs-lookup"><span data-stu-id="f0b5d-115">In the **ReportServerWeb** block, you specify the URL of the pull service and a registration key that is known to the server.</span></span>
 
<span data-ttu-id="f0b5d-116">A következő konfigurációs csomópont konfigurálja a lekéréses beállításokat egy szolgáltatás, és jelentést küldeni a szolgáltatás egy másik kiszolgálón.</span><span class="sxs-lookup"><span data-stu-id="f0b5d-116">The following configuration configures a node to pull configurations from one service, and send reports to a service on a different server.</span></span> 
 
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

<span data-ttu-id="f0b5d-117">A következő konfigurációs egy csomópont egyetlen kiszolgáló használandó konfigurációk, erőforrások és a jelentéskészítés konfigurálása.</span><span class="sxs-lookup"><span data-stu-id="f0b5d-117">The following configuration configures a node to use a single server for configurations, resources, and reporting.</span></span>

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

><span data-ttu-id="f0b5d-118">**Megjegyzés:** nevet adhat a webszolgáltatás függetlenül szüksége van, amikor egy lekéréses kiszolgáló, de a **ServerURL** tulajdonságának meg kell egyeznie a szolgáltatás nevét.</span><span class="sxs-lookup"><span data-stu-id="f0b5d-118">**Note:** You can name the web service whatever you want when you set up a pull server, but the **ServerURL** property must match the service name.</span></span>

## <a name="getting-report-data"></a><span data-ttu-id="f0b5d-119">A jelentés adatainak beolvasása</span><span class="sxs-lookup"><span data-stu-id="f0b5d-119">Getting report data</span></span>

<span data-ttu-id="f0b5d-120">A lekérési kiszolgálón a jelentések egy adatbázis-bekerülnek a kiszolgálón.</span><span class="sxs-lookup"><span data-stu-id="f0b5d-120">Reports sent to the pull server are entered into a database on the server.</span></span> <span data-ttu-id="f0b5d-121">A jelentések és a webszolgáltatás hívás érhetők el.</span><span class="sxs-lookup"><span data-stu-id="f0b5d-121">The reports are available through calls to the web service.</span></span> <span data-ttu-id="f0b5d-122">Egy konkrét csomóponthoz tartozó jelentések beolvasása, küldjön egy HTTP-kérelem a jelentéskészítő webszolgáltatás a következő formában: `http://CONTOSO-REPORT:8080/PSDSCReportServer.svc/Nodes(AgentId= 'MyNodeAgentId')/Reports` ahol `MyNodeAgentId` van a csomópont, amelynek le szeretné kérdezni a jelentések ügynökazonosító.</span><span class="sxs-lookup"><span data-stu-id="f0b5d-122">To retrieve reports for a specific node, send an HTTP request to the report web service in the following form: `http://CONTOSO-REPORT:8080/PSDSCReportServer.svc/Nodes(AgentId= 'MyNodeAgentId')/Reports` where `MyNodeAgentId` is the AgentId of the node for which you want to get reports.</span></span> <span data-ttu-id="f0b5d-123">Kaphat a ügynökazonosító egy csomópontra hívásával [Get-DscLocalConfigurationManager](https://technet.microsoft.com/library/dn407378.aspx) ezen a csomóponton.</span><span class="sxs-lookup"><span data-stu-id="f0b5d-123">You can get the AgentID for a node by calling [Get-DscLocalConfigurationManager](https://technet.microsoft.com/library/dn407378.aspx) on that node.</span></span>

<span data-ttu-id="f0b5d-124">A jelentések, egy JSON-objektumok tömbjét adja vissza.</span><span class="sxs-lookup"><span data-stu-id="f0b5d-124">The reports are returned as an array of JSON objects.</span></span>

<span data-ttu-id="f0b5d-125">Az alábbi parancsfájl a csomópont, amelyen fut a jelentéseket adja vissza:</span><span class="sxs-lookup"><span data-stu-id="f0b5d-125">The following script returns the reports for the node on which it is run:</span></span>

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
    
## <a name="viewing-report-data"></a><span data-ttu-id="f0b5d-126">A jelentés adatainak megtekintése</span><span class="sxs-lookup"><span data-stu-id="f0b5d-126">Viewing report data</span></span>

<span data-ttu-id="f0b5d-127">Ha eredményét a változó a **GetReport** függvény, megtekintheti az egyes mezők a visszaadott tömb az elemben:</span><span class="sxs-lookup"><span data-stu-id="f0b5d-127">If you set a variable to the result of the **GetReport** function, you can view the individual fields in an element of the array that is returned:</span></span>

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

<span data-ttu-id="f0b5d-128">Alapértelmezés szerint a jelentések szerint vannak rendezve **JobID**.</span><span class="sxs-lookup"><span data-stu-id="f0b5d-128">By default, the reports are sorted by **JobID**.</span></span> <span data-ttu-id="f0b5d-129">Ahhoz, hogy a legújabb jelentésre, a jelentések szerint rendezve csökkenő **StartTime** tulajdonság, majd a get az első elem a tömb:</span><span class="sxs-lookup"><span data-stu-id="f0b5d-129">To get the most recent report, you can sort the reports by descending **StartTime** property, and then get the first element of the array:</span></span>

```powershell
$reportsByStartTime = $reports | Sort-Object {$_."StartTime" -as [DateTime] } -Descending
$reportMostRecent = $reportsByStartTime[0]
```

<span data-ttu-id="f0b5d-130">Figyelje meg, hogy a **StatusData** tulajdonság-tulajdonság az objektum.</span><span class="sxs-lookup"><span data-stu-id="f0b5d-130">Notice that the **StatusData** property is an object with a number of properties.</span></span> <span data-ttu-id="f0b5d-131">Ez a ahol nagy részét a jelentési adatokat.</span><span class="sxs-lookup"><span data-stu-id="f0b5d-131">This is where much of the reporting data is.</span></span> <span data-ttu-id="f0b5d-132">Vizsgáljuk meg az egyes mezőit a **StatusData** tulajdonság a legutóbbi jelentés:</span><span class="sxs-lookup"><span data-stu-id="f0b5d-132">Let's look at the individual fields of the **StatusData** property for the most recent report:</span></span>

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

<span data-ttu-id="f0b5d-133">Ez a többek között a, hogy a legfrissebb konfigurálási két erőforrások, neve és, hogy az egyik legyen a megfelelő állapotban, és ezek egyikét nem jeleníti meg.</span><span class="sxs-lookup"><span data-stu-id="f0b5d-133">Among other things, this shows that the most recent configuration called two resources, and that one of them was in the desired state, and one of them was not.</span></span> <span data-ttu-id="f0b5d-134">Csak a, közérthetőbb kimenete kaphat **ResourcesNotInDesiredState** tulajdonság:</span><span class="sxs-lookup"><span data-stu-id="f0b5d-134">You can get a more readable output of just the **ResourcesNotInDesiredState** property:</span></span>

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

<span data-ttu-id="f0b5d-135">Figyelje meg, hogy ezek a példák úgy van kialakítva, hogy adjon meg egy meghatározni, hogy mit tehet a jelentés adataival.</span><span class="sxs-lookup"><span data-stu-id="f0b5d-135">Note that these examples are meant to give you an idea of what you can do with report data.</span></span> <span data-ttu-id="f0b5d-136">Bevezető JSON a PowerShell használatával, lásd: [játszik JSON és a PowerShell és](https://blogs.technet.microsoft.com/heyscriptingguy/2015/10/08/playing-with-json-and-powershell/).</span><span class="sxs-lookup"><span data-stu-id="f0b5d-136">For an introduction on working with JSON in PowerShell, see [Playing with JSON and PowerShell](https://blogs.technet.microsoft.com/heyscriptingguy/2015/10/08/playing-with-json-and-powershell/).</span></span>

## <a name="see-also"></a><span data-ttu-id="f0b5d-137">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="f0b5d-137">See Also</span></span>
- [<span data-ttu-id="f0b5d-138">A helyi Configuration Manager konfigurálása</span><span class="sxs-lookup"><span data-stu-id="f0b5d-138">Configuring the Local Configuration Manager</span></span>](metaConfig.md)
- [<span data-ttu-id="f0b5d-139">A DSC lekérési webkiszolgáló beállítása</span><span class="sxs-lookup"><span data-stu-id="f0b5d-139">Setting up a DSC web pull server</span></span>](pullServer.md)
- [<span data-ttu-id="f0b5d-140">Lekérési ügyfél beállítása konfigurációs nevekkel</span><span class="sxs-lookup"><span data-stu-id="f0b5d-140">Setting up a pull client using configuration names</span></span>](pullClientConfigNames.md)

