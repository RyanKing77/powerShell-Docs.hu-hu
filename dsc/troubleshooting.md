---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "Hibaelhárítási DSC"
ms.openlocfilehash: cdb11a80daecec0e0d01071752612663ac69ac6d
ms.sourcegitcommit: 99227f62dcf827354770eb2c3e95c5cf6a3118b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/15/2018
---
# <a name="troubleshooting-dsc"></a><span data-ttu-id="3557f-103">Hibaelhárítási DSC</span><span class="sxs-lookup"><span data-stu-id="3557f-103">Troubleshooting DSC</span></span>

><span data-ttu-id="3557f-104">Vonatkozik: A Windows PowerShell 4.0-s verzióját, a Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="3557f-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="3557f-105">Ez a témakör ismerteti azokat a módszereket DSC elhárításához, amikor probléma merül fel.</span><span class="sxs-lookup"><span data-stu-id="3557f-105">This topic describes ways to troubleshoot DSC when problems arise.</span></span>

## <a name="winrm-dependency"></a><span data-ttu-id="3557f-106">A WinRM-függőség</span><span class="sxs-lookup"><span data-stu-id="3557f-106">WinRM Dependency</span></span>

<span data-ttu-id="3557f-107">Windows PowerShell kívánt állapot konfigurációs szolgáltatása (DSC) attól függ, hogy a Rendszerfelügyeleti webszolgáltatások.</span><span class="sxs-lookup"><span data-stu-id="3557f-107">Windows PowerShell Desired State Configuration (DSC) depends on WinRM.</span></span> <span data-ttu-id="3557f-108">Rendszerfelügyeleti webszolgáltatások a Windows Server 2008 R2 és Windows 7 alapértelmezés szerint nincs engedélyezve.</span><span class="sxs-lookup"><span data-stu-id="3557f-108">WinRM is not enabled by default on Windows Server 2008 R2 and Windows 7.</span></span> <span data-ttu-id="3557f-109">Futtatás ```Set-WSManQuickConfig```, egy Windows PowerShell az emelt szintű ahhoz, hogy a WinRM-munkamenetben.</span><span class="sxs-lookup"><span data-stu-id="3557f-109">Run ```Set-WSManQuickConfig```, in a Windows PowerShell elevated session, to enable WinRM.</span></span>

## <a name="using-get-dscconfigurationstatus"></a><span data-ttu-id="3557f-110">Get-DscConfigurationStatus használatával</span><span class="sxs-lookup"><span data-stu-id="3557f-110">Using Get-DscConfigurationStatus</span></span>

<span data-ttu-id="3557f-111">A [Get-DscConfigurationStatus](https://technet.microsoft.com/library/mt517868.aspx) parancsmag konfiguráció állapota információ lekérése a cél-csomópont.</span><span class="sxs-lookup"><span data-stu-id="3557f-111">The [Get-DscConfigurationStatus](https://technet.microsoft.com/library/mt517868.aspx) cmdlet gets information about configuration status from a target node.</span></span> <span data-ttu-id="3557f-112">Gazdag objektumot ad vissza, amely tartalmazza-e a konfiguráció futtatása sikeres volt-e magas szintű információkat.</span><span class="sxs-lookup"><span data-stu-id="3557f-112">A rich object is returned that includes high-level information about whether or not the configuration run was successful or not.</span></span> <span data-ttu-id="3557f-113">Akkor is elmerülne a rendszer a objektumba felderítéséhez futtassa, mint a konfigurációs adatait:</span><span class="sxs-lookup"><span data-stu-id="3557f-113">You can dig into the object to discover details about the configuration run such as:</span></span>

* <span data-ttu-id="3557f-114">Az erőforrásokat, melyeknél nem sikerült</span><span class="sxs-lookup"><span data-stu-id="3557f-114">All of the resources that failed</span></span>
* <span data-ttu-id="3557f-115">Minden erőforrás újraindítást kérő</span><span class="sxs-lookup"><span data-stu-id="3557f-115">Any resource that requested a reboot</span></span>
* <span data-ttu-id="3557f-116">Futtassa a konfigurációs időpontjában meta-konfigurációs beállítások</span><span class="sxs-lookup"><span data-stu-id="3557f-116">Meta-Configuration settings at time of configuration run</span></span>
* <span data-ttu-id="3557f-117">Etc.</span><span class="sxs-lookup"><span data-stu-id="3557f-117">Etc.</span></span>

<span data-ttu-id="3557f-118">A következő paraméterhalmaz adja vissza az utolsó futtatása konfigurációra vonatkozó információk:</span><span class="sxs-lookup"><span data-stu-id="3557f-118">The following parameter set returns the status information for the last configuration run:</span></span>

```powershell
Get-DscConfigurationStatus  [-CimSession <CimSession[]>] 
                            [-ThrottleLimit <int>] 
                            [-AsJob] 
                            [<CommonParameters>]
```
<span data-ttu-id="3557f-119">A következő paraméterhalmaz adja vissza az összes korábbi konfigurációs futás esetén:</span><span class="sxs-lookup"><span data-stu-id="3557f-119">The following parameter set returns the status information for all previous configuration runs:</span></span>

```powershell
Get-DscConfigurationStatus  -All 
                            [-CimSession <CimSession[]>] 
                            [-ThrottleLimit <int>] 
                            [-AsJob] 
                            [<CommonParameters>]
```

## <a name="example"></a><span data-ttu-id="3557f-120">Példa</span><span class="sxs-lookup"><span data-stu-id="3557f-120">Example</span></span>

```powershell
PS C:\> $Status = Get-DscConfigurationStatus 

PS C:\> $Status

Status      StartDate               Type            Mode    RebootRequested     NumberOfResources
------      ---------               ----            ----    ---------------     -----------------
Failure     11/24/2015  3:44:56     Consistency     Push    True                36

PS C:\> $Status.ResourcesNotInDesiredState

ConfigurationName       :   MyService
DependsOn               :   
ModuleName              :   PSDesiredStateConfiguration
ModuleVersion           :   1.1
PsDscRunAsCredential    :   
ResourceID              :   [File]ServiceDll
SourceInfo              :   c:\git\CustomerService\Configs\MyCustomService.ps1::5::34::File
DurationInSeconds       :   0.19
Error                   :   SourcePath must be accessible for current configuration. The related file/directory is:
                            \\Server93\Shared\contosoApp.dll. The related ResourceID is [File]ServiceDll
FinalState              :   
InDesiredState          :   False
InitialState            :   
InstanceName            :   ServiceDll
RebootRequested         :   False
ReosurceName            :   File
StartDate               :   11/24/2015  3:44:56
PSComputerName          :
```

## <a name="my-script-wont-run-using-dsc-logs-to-diagnose-script-errors"></a><span data-ttu-id="3557f-121">A parancsprogram nem futott: parancsfájl hibáinak diagnosztizálásához naplózza a DSC használata</span><span class="sxs-lookup"><span data-stu-id="3557f-121">My script won’t run: Using DSC logs to diagnose script errors</span></span>

<span data-ttu-id="3557f-122">Minden Windows szoftverek, például DSC rögzíti hibák és események [naplók](https://msdn.microsoft.com/library/windows/desktop/aa363632.aspx) , hogy megtekinthetők a [Eseménynapló](http://windows.microsoft.com/windows/what-information-event-logs-event-viewer).</span><span class="sxs-lookup"><span data-stu-id="3557f-122">Like all Windows software, DSC records errors and events in [logs](https://msdn.microsoft.com/library/windows/desktop/aa363632.aspx) that can be viewed from the [Event Viewer](http://windows.microsoft.com/windows/what-information-event-logs-event-viewer).</span></span> <span data-ttu-id="3557f-123">Ezek a naplók vizsgálata azt segítenek megérteni miért egy adott művelethez nem sikerült, és a jövőben megakadályozása hiba.</span><span class="sxs-lookup"><span data-stu-id="3557f-123">Examining these logs can help you understand why a particular operation failed, and how to prevent failure in the future.</span></span> <span data-ttu-id="3557f-124">Konfigurációs parancsfájlok írása megkapni, hogy követési hibák könnyíti meg Szerző, a konfiguráció a DSC elemzési eseménynaplóban az előrehaladását úgy követheti nyomon a DSC-napló erőforrás segítségével.</span><span class="sxs-lookup"><span data-stu-id="3557f-124">Writing configuration scripts can be tricky, so to make tracking errors easier as you author, use the DSC Log resource to track the progress of your configuration in the DSC Analytic event log.</span></span>

## <a name="where-are-dsc-event-logs"></a><span data-ttu-id="3557f-125">Hol találhatók a DSC-eseménynaplók?</span><span class="sxs-lookup"><span data-stu-id="3557f-125">Where are DSC event logs?</span></span>

<span data-ttu-id="3557f-126">Az Eseménynapló DSC események szerepelnek: **alkalmazások és szolgáltatások Logs/Microsoft/Windows/kívánt állapot konfigurációs**</span><span class="sxs-lookup"><span data-stu-id="3557f-126">In Event Viewer, DSC events are in: **Applications and Services Logs/Microsoft/Windows/Desired State Configuration**</span></span>

<span data-ttu-id="3557f-127">A megfelelő PowerShell-parancsmag [Get-WinEvent](https://technet.microsoft.com/library/hh849682.aspx), is futtatható tekintse át az eseménynaplókat:</span><span class="sxs-lookup"><span data-stu-id="3557f-127">The corresponding PowerShell cmdlet, [Get-WinEvent](https://technet.microsoft.com/library/hh849682.aspx), can also be run to view the event logs:</span></span>

```
PS C:\> Get-WinEvent -LogName "Microsoft-Windows-Dsc/Operational"
   ProviderName: Microsoft-Windows-DSC
TimeCreated                     Id LevelDisplayName Message                                                                                                  
-----------                     -- ---------------- -------                                                                                                  
11/17/2014 10:27:23 PM        4102 Information      Job {02C38626-D95A-47F1-9DA2-C1D44A7128E7} : 
```

<span data-ttu-id="3557f-128">A fentiek van-e DSC elsődleges napló neve **Microsoft -> Windows -> DSC** (a Windows egyéb napló nevek nem itt látható kivonatosan mutatja).</span><span class="sxs-lookup"><span data-stu-id="3557f-128">As shown above, DSC’s primary log name is **Microsoft->Windows->DSC** (other log names under Windows are not shown here for brevity).</span></span> <span data-ttu-id="3557f-129">Az elsődleges neve van hozzáfűzve csatornát létrehozni a teljes nevét.</span><span class="sxs-lookup"><span data-stu-id="3557f-129">The primary name is appended to the channel name to create the complete log name.</span></span> <span data-ttu-id="3557f-130">A DSC-motor ír főként a naplók három típusa: [működési, elemzési és hibakeresési naplók](https://technet.microsoft.com/library/cc722404.aspx).</span><span class="sxs-lookup"><span data-stu-id="3557f-130">The DSC engine writes mainly into three types of logs: [Operational, Analytic, and Debug logs](https://technet.microsoft.com/library/cc722404.aspx).</span></span> <span data-ttu-id="3557f-131">Mivel az elemzési és hibakeresési naplók alapértelmezés szerint ki van kapcsolva, engedélyezze a őket az eseménynaplóban.</span><span class="sxs-lookup"><span data-stu-id="3557f-131">Since the analytic and debug logs are turned off by default, you should enable them in Event Viewer.</span></span> <span data-ttu-id="3557f-132">Ehhez nyissa meg az eseménynaplót az eseménynaplóban megjelenítése írja be a Windows PowerShell; vagy kattintson a **Start** gombra, majd **Vezérlőpult**, kattintson a **felügyeleti eszközök**, és kattintson a **Eseménynapló**.</span><span class="sxs-lookup"><span data-stu-id="3557f-132">To do this, open Event Viewer by typing Show-EventLog in Windows PowerShell; or, click the **Start** button, click **Control Panel**, click **Administrative Tools**, and then click **Event Viewer**.</span></span> <span data-ttu-id="3557f-133">Az a **nézet** az eseménynaplóban, menüjében kattintson **elemzési és hibakeresési naplók megjelenítése**.</span><span class="sxs-lookup"><span data-stu-id="3557f-133">On the **View** menu in Event viewer, click **Show Analytic and Debug Logs**.</span></span> <span data-ttu-id="3557f-134">A naplófájl neve a analytic channel bejegyzést **elemzési Microsoft-Windows-Dsc**, és a hibakeresési csatorna **Microsoft-Windows-Dsc/Debug**.</span><span class="sxs-lookup"><span data-stu-id="3557f-134">The log name for the analytic channel is **Microsoft-Windows-Dsc/Analytic**, and the debug channel is **Microsoft-Windows-Dsc/Debug**.</span></span> <span data-ttu-id="3557f-135">Is használhatja a [wevtutil](https://technet.microsoft.com/library/cc732848.aspx) segédprogram a naplók engedélyezéséhez az alábbi példában látható módon.</span><span class="sxs-lookup"><span data-stu-id="3557f-135">You could also use the [wevtutil](https://technet.microsoft.com/library/cc732848.aspx) utility to enable the logs, as shown in the following example.</span></span>

```powershell
wevtutil.exe set-log “Microsoft-Windows-Dsc/Analytic” /q:true /e:true
```

## <a name="what-do-dsc-logs-contain"></a><span data-ttu-id="3557f-136">A DSC-naplók tartalmazzák</span><span class="sxs-lookup"><span data-stu-id="3557f-136">What do DSC logs contain?</span></span>

<span data-ttu-id="3557f-137">A DSC-naplók keresztül a három naplózási csatornák, az üzenet fontosságát alapján vannak osztva.</span><span class="sxs-lookup"><span data-stu-id="3557f-137">DSC logs are split over the three log channels based on the importance of the message.</span></span> <span data-ttu-id="3557f-138">A DSC műveleti napló az összes hibaüzenet tartalmazza, és a probléma azonosításához használható.</span><span class="sxs-lookup"><span data-stu-id="3557f-138">The operational log in DSC contains all error messages, and can be used to identify a problem.</span></span> <span data-ttu-id="3557f-139">Az elemzési naplóját nagyobb mennyiségű esemény rendelkezik, és azonosíthatja, ahol egy vagy több hiba történt.</span><span class="sxs-lookup"><span data-stu-id="3557f-139">The analytic log has a higher volume of events, and can identify where error(s) occurred.</span></span> <span data-ttu-id="3557f-140">Ez a csatorna a részletes üzenetek is tartalmaz, (ha van ilyen).</span><span class="sxs-lookup"><span data-stu-id="3557f-140">This channel also contains verbose messages (if any).</span></span> <span data-ttu-id="3557f-141">A hibakeresési napló tartalmazza a naplófájlokat, amelyek azt segítenek megérteni, hogyan a hibák fordultak elő.</span><span class="sxs-lookup"><span data-stu-id="3557f-141">The debug log contains logs that can help you understand how the errors occurred.</span></span> <span data-ttu-id="3557f-142">A DSC-eseményüzenetek felépítése úgy, hogy minden üzenet egy DSC művelet egyedileg jelölő feladatazonosítóval kezdődik.</span><span class="sxs-lookup"><span data-stu-id="3557f-142">DSC event messages are structured such that every event message begins with a job ID that uniquely represents a DSC operation.</span></span> <span data-ttu-id="3557f-143">Az alábbi példa megkísérli az üzenet kérése az első esemény naplózása működési DSC naplóba.</span><span class="sxs-lookup"><span data-stu-id="3557f-143">The example below attempts to obtain the message from the first event logged into the operational DSC log.</span></span>

```powershell
PS C:\> $AllDscOpEvents = Get-WinEvent -LogName "Microsoft-Windows-Dsc/Operational"
PS C:\> $FirstOperationalEvent = $AllDscOpEvents[0]
PS C:\> $FirstOperationalEvent.Message
Job {02C38626-D95A-47F1-9DA2-C1D44A7128E7} : 
Consistency engine was run successfully. 
```

<span data-ttu-id="3557f-144">Egy adott struktúra, amely lehetővé teszi a felhasználó az összegyűjtött eseményeket egy DSC feladatból DSC események naplózása.</span><span class="sxs-lookup"><span data-stu-id="3557f-144">DSC events are logged in a particular structure that enables the user to aggregate events from one DSC job.</span></span> <span data-ttu-id="3557f-145">A struktúra a következőképpen történik:</span><span class="sxs-lookup"><span data-stu-id="3557f-145">The structure is as follows:</span></span>

<span data-ttu-id="3557f-146">**Feladat azonosítója: <Guid>**
**<Event Message>**</span><span class="sxs-lookup"><span data-stu-id="3557f-146">**Job ID : <Guid>**
**<Event Message>**</span></span>

## <a name="gathering-events-from-a-single-dsc-operation"></a><span data-ttu-id="3557f-147">Egy DSC művelettel eseményeinek gyűjtése</span><span class="sxs-lookup"><span data-stu-id="3557f-147">Gathering events from a single DSC operation</span></span>

<span data-ttu-id="3557f-148">A DSC-eseménynaplók különböző DSC műveletei által előállított eseményeket tartalmaz.</span><span class="sxs-lookup"><span data-stu-id="3557f-148">DSC event logs contain events generated by various DSC operations.</span></span> <span data-ttu-id="3557f-149">Azonban általában lesz a részletességgel aggódik egy adott művelet.</span><span class="sxs-lookup"><span data-stu-id="3557f-149">However, you’ll usually be concerned with the detail about just one particular operation.</span></span> <span data-ttu-id="3557f-150">Összes DSC napló csoportosíthatók az egyedi minden DSC művelethez feladat-azonosító tulajdonsággal.</span><span class="sxs-lookup"><span data-stu-id="3557f-150">All DSC logs can be grouped by the job ID property that is unique for every DSC operation.</span></span> <span data-ttu-id="3557f-151">Minden DSC események első tulajdonság értéke jelenik meg a Feladatazonosítót.</span><span class="sxs-lookup"><span data-stu-id="3557f-151">The job ID is displayed as the first property value in all DSC events.</span></span> <span data-ttu-id="3557f-152">Az alábbi lépések ismertetik időtartamok csoportosított tömb struktúrában összes esemény megjelenítése.</span><span class="sxs-lookup"><span data-stu-id="3557f-152">The following steps explain how to accumulate all events in a grouped array structure.</span></span>

```powershell
<##########################################################################
 Step 1 : Enable analytic and debug DSC channels (Operational channel is enabled by default)
###########################################################################>
 
wevtutil.exe set-log “Microsoft-Windows-Dsc/Analytic” /q:true /e:true
wevtutil.exe set-log “Microsoft-Windows-Dsc/Debug” /q:True /e:true
 
<##########################################################################
 Step 2 : Perform the required DSC operation (Below is an example, you could run any DSC operation instead)
###########################################################################>
 
Get-DscLocalConfigurationManager
 
<##########################################################################
Step 3 : Collect all DSC Logs, from the Analytic, Debug and Operational channels
###########################################################################>
 
$DscEvents=[System.Array](Get-WinEvent "Microsoft-Windows-Dsc/Operational") `
         + [System.Array](Get-WinEvent "Microsoft-Windows-Dsc/Analytic" -Oldest) `
         + [System.Array](Get-WinEvent "Microsoft-Windows-Dsc/Debug" -Oldest)
 
 
<##########################################################################
 Step 4 : Group all logs based on the job ID
###########################################################################>
$SeparateDscOperations = $DscEvents | Group {$_.Properties[0].value}  
```

<span data-ttu-id="3557f-153">Itt, a változó `$SeparateDscOperations` tartalmazza a naplók a feladat-azonosítók szerint csoportosítva.</span><span class="sxs-lookup"><span data-stu-id="3557f-153">Here, the variable `$SeparateDscOperations` contains logs grouped by the job IDs.</span></span> <span data-ttu-id="3557f-154">A változó minden tömbelem másik DSC műveletet, amely hozzáférést biztosít a naplókat további információt által naplózott eseményeket csoportja.</span><span class="sxs-lookup"><span data-stu-id="3557f-154">Each array element of this variable represents a group of events logged by a different DSC operation, allowing access to more information about the logs.</span></span>

```
PS C:\> $SeparateDscOperations
 
Count Name                      Group                                                                     
----- ----                      -----                                                                     
   48 {1A776B6A-5BAC-11E3-BF... {System.Diagnostics.Eventing.Reader.EventLogRecord, System.Diagnostics....
   40 {E557E999-5BA8-11E3-BF... {System.Diagnostics.Eventing.Reader.EventLogRecord, System.Diagnostics....
PS C:\> $SeparateDscOperations[0].Group
   ProviderName: Microsoft-Windows-DSC
TimeCreated                     Id LevelDisplayName Message                                               
-----------                     -- ---------------- -------                                               
12/2/2013 3:47:29 PM          4115 Information      Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : ...      
12/2/2013 3:47:29 PM          4198 Information      Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : ...      
12/2/2013 3:47:29 PM          4114 Information      Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : ...      
12/2/2013 3:47:29 PM          4102 Information      Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : ...      
12/2/2013 3:47:29 PM          4098 Warning          Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : ...      
12/2/2013 3:47:29 PM          4098 Warning          Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : ...      
12/2/2013 3:47:29 PM          4176 Information      Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : ...      
12/2/2013 3:47:29 PM          4182 Information      Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : ...      
12/2/2013 3:47:29 PM          4182 Information      Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : ...      
12/2/2013 3:47:29 PM          4182 Information      Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : ...      
12/2/2013 3:47:29 PM          4182 Information      Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : ...      
12/2/2013 3:47:29 PM          4182 Information      Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : ...      
12/2/2013 3:47:29 PM          4182 Information      Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : ...      
12/2/2013 3:47:29 PM          4182 Information      Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : ...      
12/2/2013 3:47:29 PM          4182 Information      Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : ...       
```

<span data-ttu-id="3557f-155">Az adatok a változóban kibonthatja `$SeparateDscOperations` használatával [Where-Object](https://technet.microsoft.com/library/ee177028.aspx).</span><span class="sxs-lookup"><span data-stu-id="3557f-155">You can extract the data in the variable `$SeparateDscOperations` using [Where-Object](https://technet.microsoft.com/library/ee177028.aspx).</span></span> <span data-ttu-id="3557f-156">Az alábbiakban öt forgatókönyvek, amelyekben érdemes DSC hibaelhárítási adatokat nyerhet ki:</span><span class="sxs-lookup"><span data-stu-id="3557f-156">Following are five scenarios in which you might want to extract data for troubleshooting DSC:</span></span>

### <a name="1-operations-failures"></a><span data-ttu-id="3557f-157">1: műveletek hibák</span><span class="sxs-lookup"><span data-stu-id="3557f-157">1: Operations failures</span></span>

<span data-ttu-id="3557f-158">Minden eseményhez [súlyossági szintek](https://msdn.microsoft.com/library/dd996917(v=vs.85)).</span><span class="sxs-lookup"><span data-stu-id="3557f-158">All events have [severity levels](https://msdn.microsoft.com/library/dd996917(v=vs.85)).</span></span> <span data-ttu-id="3557f-159">Ezek az információk segítségével azonosíthatja a hibaesemények:</span><span class="sxs-lookup"><span data-stu-id="3557f-159">This information can be used to identify the error events:</span></span>

```
PS C:\> $SeparateDscOperations | Where-Object {$_.Group.LevelDisplayName -contains "Error"}
Count Name                      Group                                                                     
----- ----                      -----                                                                     
   38 {5BCA8BE7-5BB6-11E3-BF... {System.Diagnostics.Eventing.Reader.EventLogRecord, System.Diagnostics....
```

### <a name="2-details-of-operations-run-in-the-last-half-hour"></a><span data-ttu-id="3557f-160">2: műveletek részleteit futtassa az utolsó fél óra</span><span class="sxs-lookup"><span data-stu-id="3557f-160">2: Details of operations run in the last half hour</span></span>

<span data-ttu-id="3557f-161">`TimeCreated`, minden Windows-esemény tulajdonsága jelzi, amikor az esemény létrejött.</span><span class="sxs-lookup"><span data-stu-id="3557f-161">`TimeCreated`, a property of every Windows event, states the time the event was created.</span></span> <span data-ttu-id="3557f-162">Ezt a tulajdonságot, egy adott dátum/idő objektummal összehasonlításával összes esemény szűrésére használható:</span><span class="sxs-lookup"><span data-stu-id="3557f-162">Comparing this property with a particular date/time object can be used to filter all events:</span></span>

```powershell
PS C:\> $DateLatest = (Get-Date).AddMinutes(-30)
PS C:\> $SeparateDscOperations | Where-Object {$_.Group.TimeCreated -gt $DateLatest}
Count Name                      Group                                                                     
----- ----                      -----                                                                     
    1 {6CEC5B09-5BB0-11E3-BF... {System.Diagnostics.Eventing.Reader.EventLogRecord}   
```

### <a name="3-messages-from-the-latest-operation"></a><span data-ttu-id="3557f-163">3: a legutóbbi művelet üzenetek</span><span class="sxs-lookup"><span data-stu-id="3557f-163">3: Messages from the latest operation</span></span>

<span data-ttu-id="3557f-164">A legutóbbi művelet tárolja az első index a tömb csoport `$SeparateDscOperations`.</span><span class="sxs-lookup"><span data-stu-id="3557f-164">The latest operation is stored in the first index of the array group `$SeparateDscOperations`.</span></span> <span data-ttu-id="3557f-165">A csoport üzenetek 0. index lekérdezése adja vissza a legutóbbi művelet üzenetek:</span><span class="sxs-lookup"><span data-stu-id="3557f-165">Querying the group’s messages for index 0 returns all messages for the latest operation:</span></span>

```powershelll
PS C:\> $SeparateDscOperations[0].Group.Message
Job {5BCA8BE7-5BB6-11E3-BF41-00155D553612} : 
Running consistency engine.
Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : 
Configuration is sent from computer NULL by user sid S-1-5-18.
Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : 
Displaying messages from built-in DSC resources:
 WMI channel 1 
 ResourceID:  
 Message : [INCH-VM]:                            [] Starting consistency engine.
Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : 
Displaying messages from built-in DSC resources:
 WMI channel 1 
 ResourceID:  
 Message : [INCH-VM]:                            [] Consistency check completed. 
```

### <a name="4-error-messages-logged-for-recent-failed-operations"></a><span data-ttu-id="3557f-166">4: legutóbbi meghiúsult műveletek a naplóba hibaüzenetek</span><span class="sxs-lookup"><span data-stu-id="3557f-166">4: Error messages logged for recent failed operations</span></span>

<span data-ttu-id="3557f-167">`$SeparateDscOperations[0].Group` a legutóbbi művelet eseményeket tartalmaz.</span><span class="sxs-lookup"><span data-stu-id="3557f-167">`$SeparateDscOperations[0].Group` contains a set of events for the latest operation.</span></span> <span data-ttu-id="3557f-168">Futtassa a `Where-Object` parancsmag használatával az események szűréséhez szintű megjelenítendő neve alapján.</span><span class="sxs-lookup"><span data-stu-id="3557f-168">Run the `Where-Object` cmdlet to filter the events based on their level display name.</span></span> <span data-ttu-id="3557f-169">Eredmények tárolódnak a `$myFailedEvent` változó, amely lehet további minél esemény üzenet:</span><span class="sxs-lookup"><span data-stu-id="3557f-169">Results are stored in the `$myFailedEvent` variable, which can be further dissected to get the event message:</span></span>

```powershell
PS C:\> $myFailedEvent = ($SeparateDscOperations[0].Group | Where-Object {$_.LevelDisplayName -eq "Error"})
 
PS C:\> $myFailedEvent.Message
Job {5BCA8BE7-5BB6-11E3-BF41-00155D553612} : 
DSC Engine Error : 
 Error Message Current configuration does not exist. Execute Start-DscConfiguration command with -Path pa
rameter to specify a configuration file and create a current configuration first. 
Error Code : 1 
```

### <a name="5-all-events-generated-for-a-particular-job-id"></a><span data-ttu-id="3557f-170">5: összes eseményt hoz létre egy adott feladat.</span><span class="sxs-lookup"><span data-stu-id="3557f-170">5: All events generated for a particular job ID.</span></span>

<span data-ttu-id="3557f-171">`$SeparateDscOperations` egy tömb csoportok, amelyek mindegyikének a neve megegyezik a feladat egyedi azonosítója.</span><span class="sxs-lookup"><span data-stu-id="3557f-171">`$SeparateDscOperations` is an array of groups, each of which has the name as the unique job ID.</span></span> <span data-ttu-id="3557f-172">Futtassa a `Where-Object` parancsmag is kibonthat egy ezeket a csoportokat az eseményeket, amelyek egy adott feladat azonosítója:</span><span class="sxs-lookup"><span data-stu-id="3557f-172">By running the `Where-Object` cmdlet, you can extract those groups of events that have a particular job ID:</span></span>

```powershell
PS C:\> ($SeparateDscOperations | Where-Object {$_.Name -eq $jobX} ).Group

   ProviderName: Microsoft-Windows-DSC
 
TimeCreated                     Id LevelDisplayName Message                                               
-----------                     -- ---------------- -------                                               
12/2/2013 4:33:24 PM          4102 Information      Job {847A5619-5BB2-11E3-BF41-00155D553612} : ...      
12/2/2013 4:33:24 PM          4168 Information      Job {847A5619-5BB2-11E3-BF41-00155D553612} : ...      
12/2/2013 4:33:24 PM          4146 Information      Job {847A5619-5BB2-11E3-BF41-00155D553612} : ...      
12/2/2013 4:33:24 PM          4120 Information      Job {847A5619-5BB2-11E3-BF41-00155D553612} : ...  
```

## <a name="using-xdscdiagnostics-to-analyze-dsc-logs"></a><span data-ttu-id="3557f-173">Naplók segítségével xDscDiagnostics DSC elemzése</span><span class="sxs-lookup"><span data-stu-id="3557f-173">Using xDscDiagnostics to analyze DSC logs</span></span>

<span data-ttu-id="3557f-174">**xDscDiagnostics** egy PowerShell-modul, amely számos funkcióval segíti a számítógépre a DSC-hibák elemzése áll.</span><span class="sxs-lookup"><span data-stu-id="3557f-174">**xDscDiagnostics** is a PowerShell module that consists of several functions that can help analyze DSC failures on your machine.</span></span> <span data-ttu-id="3557f-175">Ezek a funkciók segítségével azonosítja az összes helyi események az elmúlt DSC műveletek vagy DSC események távoli számítógépeken (az érvényes hitelesítő adatok).</span><span class="sxs-lookup"><span data-stu-id="3557f-175">These functions can help you identify all local events from past DSC operations, or DSC events on remote computers (with valid credentials).</span></span> <span data-ttu-id="3557f-176">Itt a DSC-művelet kifejezés egy egyetlen egyedi DSC végrehajtási a kezdetektől végéhez meghatározásához.</span><span class="sxs-lookup"><span data-stu-id="3557f-176">Here, the term DSC operation is used to define a single unique DSC execution from its start to its end.</span></span> <span data-ttu-id="3557f-177">Például `Test-DscConfiguration` egy külön DSC művelet lenne.</span><span class="sxs-lookup"><span data-stu-id="3557f-177">For example, `Test-DscConfiguration` would be a separate DSC operation.</span></span> <span data-ttu-id="3557f-178">Hasonlóképpen, minden más parancsmag DSC (például `Get-DscConfiguration`, `Start-DscConfiguration`stb) minden azonosítható DSC külön műveletként.</span><span class="sxs-lookup"><span data-stu-id="3557f-178">Similarly, every other cmdlet in DSC (such as `Get-DscConfiguration`, `Start-DscConfiguration`, etc.) could each be identified as separate DSC operations.</span></span> <span data-ttu-id="3557f-179">A függvények van arra a [xDscDiagnostics](https://github.com/PowerShell/xDscDiagnostics).</span><span class="sxs-lookup"><span data-stu-id="3557f-179">The functions are explained at [xDscDiagnostics](https://github.com/PowerShell/xDscDiagnostics).</span></span> <span data-ttu-id="3557f-180">Súgó áll rendelkezésre futtatásával `Get-Help <cmdlet name>`.</span><span class="sxs-lookup"><span data-stu-id="3557f-180">Help is available by running `Get-Help <cmdlet name>`.</span></span>

### <a name="getting-details-of-dsc-operations"></a><span data-ttu-id="3557f-181">A DSC-műveletek-információk lekérdezése</span><span class="sxs-lookup"><span data-stu-id="3557f-181">Getting details of DSC operations</span></span> 

<span data-ttu-id="3557f-182">A `Get-xDscOperation` funkció lehetővé teszi, hogy az eredmények, amelyek egy vagy több számítógépen futnak a DSC-műveletek található, és visszahelyezi a minden egyes DSC művelet által létrehozott olyan objektum, amely az események gyűjteményét tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="3557f-182">The `Get-xDscOperation` function lets you find the results of the DSC operations that run on one or multiple computers, and returns an object that contains the collection of events produced by each DSC operation.</span></span> <span data-ttu-id="3557f-183">Például a következő kimenet három parancsot futtatná.</span><span class="sxs-lookup"><span data-stu-id="3557f-183">For example, in the following output, three commands were run.</span></span> <span data-ttu-id="3557f-184">Az átadott, és két, a másik nem.</span><span class="sxs-lookup"><span data-stu-id="3557f-184">The first one passed, and the other two failed.</span></span> <span data-ttu-id="3557f-185">Ezekkel az eredményekkel foglalja össze a kimenetét `Get-xDscOperation`.</span><span class="sxs-lookup"><span data-stu-id="3557f-185">These results are summarized in the output of `Get-xDscOperation`.</span></span>

```powershell
PS C:\DiagnosticsTest> Get-xDscOperation

ComputerName   SequenceId TimeCreated           Result   JobID                                 AllEvents            
------------   ---------- -----------           ------   -----                                 ---------            
SRV1   1          6/23/2016 9:37:52 AM  Failure  9701aadf-395e-11e6-9165-00155d390509  {@{Message=; TimeC...
SRV1   2          6/23/2016 9:36:54 AM  Failure  7e8e2d6e-395c-11e6-9165-00155d390509  {@{Message=; TimeC...
SRV1   3          6/23/2016 9:36:54 AM  Success  af72c6aa-3960-11e6-9165-00155d390509  {@{Message=Operati...

```

<span data-ttu-id="3557f-186">Megadhatja, amelyet csak a legutóbbi művelet használatával a `Newest` paraméter:</span><span class="sxs-lookup"><span data-stu-id="3557f-186">You can also specify that you want only results for the most recent operations by using the `Newest` parameter:</span></span>

```powershell
PS C:\DiagnosticsTest> Get-xDscOperation -Newest 5
ComputerName   SequenceId TimeCreated           Result   JobID                                 AllEvents            
------------   ---------- -----------           ------   -----                                 ---------            
SRV1   1          6/23/2016 4:36:54 PM  Success                                        {@{Message=; TimeC...
SRV1   2          6/23/2016 4:36:54 PM  Success  5c06402b-399b-11e6-9165-00155d390509  {@{Message=Operati...
SRV1   3          6/23/2016 4:36:54 PM  Success                                        {@{Message=; TimeC...
SRV1   4          6/23/2016 4:36:54 PM  Success  5c06402a-399b-11e6-9165-00155d390509  {@{Message=Operati...
SRV1   5          6/23/2016 4:36:51 PM  Success                                        {@{Message=; TimeC...
```

### <a name="getting-details-of-dsc-events"></a><span data-ttu-id="3557f-187">A DSC-események adatainak lekérdezése</span><span class="sxs-lookup"><span data-stu-id="3557f-187">Getting details of DSC events</span></span>

<span data-ttu-id="3557f-188">A `Trace-xDscOperation` parancsmag visszaad egy objektumot tartalmazó események, az esemény típusok gyűjteményét, és az üzenet kimeneti jön létre egy adott DSC-műveletből.</span><span class="sxs-lookup"><span data-stu-id="3557f-188">The `Trace-xDscOperation` cmdlet returns an object containing a collection of events, their event types, and the message output generated from a particular DSC operation.</span></span> <span data-ttu-id="3557f-189">Általában, amikor talált hiba használó műveletek `Get-xDscOperation`, szeretné nyomon követni Ez a művelet, ha szeretné tudni, amely az események hibáját okozta.</span><span class="sxs-lookup"><span data-stu-id="3557f-189">Typically, when you find a failure in any of the operations using `Get-xDscOperation`, you would trace that operation to find out which of the events caused a failure.</span></span>

<span data-ttu-id="3557f-190">Használja a `SequenceID` paraméter használatával beolvassa az eseményeket egy adott művelet egy adott számítógépen.</span><span class="sxs-lookup"><span data-stu-id="3557f-190">Use the  `SequenceID` parameter to get the events for a specific operation for a specific computer.</span></span> <span data-ttu-id="3557f-191">Például, ha megad egy `SequenceID` a 9-es, `Trace-xDscOperaion` a nyomkövetési lekérése a DSC művelet, amely a legutóbbi művelet 9 volt:</span><span class="sxs-lookup"><span data-stu-id="3557f-191">For example, if you specify a `SequenceID` of 9, `Trace-xDscOperaion` get the trace for the DSC operation that was 9th from the last operation:</span></span>

```powershell
PS C:\DiagnosticsTest> Trace-xDscOperation -SequenceID 9

ComputerName   EventType    TimeCreated           Message                                                                                             
------------   ---------    -----------           -------                                                                                             
SRV1   OPERATIONAL  6/24/2016 10:51:52 AM Operation Consistency Check or Pull started by user sid S-1-5-20 from computer NULL.                
SRV1   OPERATIONAL  6/24/2016 10:51:52 AM Running consistency engine.                                                                         
SRV1   OPERATIONAL  6/24/2016 10:51:52 AM The local configuration manager is updating the PSModulePath to WindowsPowerShell\Modules;C:\Prog...
SRV1   OPERATIONAL  6/24/2016 10:51:53 AM  Resource execution sequence :: [WindowsFeature]DSCServiceFeature, [xDSCWebService]PSDSCPullServer. 
SRV1   OPERATIONAL  6/24/2016 10:51:54 AM Consistency engine was run successfully.                                                            
SRV1   OPERATIONAL  6/24/2016 10:51:54 AM Job runs under the following LCM setting. ...                                                       
SRV1   OPERATIONAL  6/24/2016 10:51:54 AM Operation Consistency Check or Pull completed successfully. 
```

<span data-ttu-id="3557f-192">Adja át a **GUID** adott DSC művelethez hozzárendelt (amelyet a `Get-xDscOperation` cmldet) az esemény részleteinek lekérése DSC művelet:</span><span class="sxs-lookup"><span data-stu-id="3557f-192">Pass the **GUID** assigned to a specific DSC operation (as returned by the `Get-xDscOperation` cmldet) to get the event details for that DSC operation:</span></span>

```powershell
PS C:\DiagnosticsTest> Trace-xDscOperation -JobID 9e0bfb6b-3a3a-11e6-9165-00155d390509

ComputerName   EventType    TimeCreated           Message                                                                                             
------------   ---------    -----------           -------                                                                                             
SRV1   OPERATIONAL  6/24/2016 11:36:56 AM Operation Consistency Check or Pull started by user sid S-1-5-20 from computer NULL.                
SRV1   ANALYTIC     6/24/2016 11:36:56 AM Deleting file from C:\Windows\System32\Configuration\DSCEngineCache.mof                             
SRV1   OPERATIONAL  6/24/2016 11:36:56 AM Running consistency engine.                                                                         
SRV1   VERBOSE      6/24/2016 11:36:56 AM [SRV1]:                            [] Starting consistency engine.                          
SRV1   ANALYTIC     6/24/2016 11:36:56 AM Applying configuration from C:\Windows\System32\Configuration\Current.mof.                          
SRV1   ANALYTIC     6/24/2016 11:36:56 AM Parsing the configuration to apply.                                                                 
SRV1   OPERATIONAL  6/24/2016 11:36:56 AM  Resource execution sequence :: [WindowsFeature]DSCServiceFeature, [xDSCWebService]PSDSCPullServer. 
SRV1   VERBOSE      6/24/2016 11:36:56 AM [SRV1]: LCM:  [ Start  Resource ]  [[WindowsFeature]DSCServiceFeature]                      
SRV1   ANALYTIC     6/24/2016 11:36:56 AM Executing operations for PS DSC resource MSFT_RoleResource with resource name [WindowsFeature]DSC...
SRV1   VERBOSE      6/24/2016 11:36:56 AM [SRV1]: LCM:  [ Start  Test     ]  [[WindowsFeature]DSCServiceFeature]                      
SRV1   VERBOSE      6/24/2016 11:36:56 AM [SRV1]:                            [[WindowsFeature]DSCServiceFeature] The operation 'Get...
SRV1   VERBOSE      6/24/2016 11:36:56 AM [SRV1]:                            [[WindowsFeature]DSCServiceFeature] The operation 'Get...
SRV1   VERBOSE      6/24/2016 11:36:56 AM [SRV1]: LCM:  [ End    Test     ]  [[WindowsFeature]DSCServiceFeature] True in 0.3130 sec...
SRV1   VERBOSE      6/24/2016 11:36:56 AM [SRV1]: LCM:  [ End    Resource ]  [[WindowsFeature]DSCServiceFeature]                      
SRV1   VERBOSE      6/24/2016 11:36:56 AM [SRV1]: LCM:  [ Start  Resource ]  [[xDSCWebService]PSDSCPullServer]                        
SRV1   ANALYTIC     6/24/2016 11:36:56 AM Executing operations for PS DSC resource MSFT_xDSCWebService with resource name [xDSCWebService]P...
SRV1   VERBOSE      6/24/2016 11:36:56 AM [SRV1]: LCM:  [ Start  Test     ]  [[xDSCWebService]PSDSCPullServer]                        
SRV1   VERBOSE      6/24/2016 11:36:56 AM [SRV1]:                            [[xDSCWebService]PSDSCPullServer] Check Ensure           
SRV1   VERBOSE      6/24/2016 11:36:56 AM [SRV1]:                            [[xDSCWebService]PSDSCPullServer] Check Port             
SRV1   VERBOSE      6/24/2016 11:36:56 AM [SRV1]:                            [[xDSCWebService]PSDSCPullServer] Check Physical Path ...
SRV1   VERBOSE      6/24/2016 11:36:56 AM [SRV1]:                            [[xDSCWebService]PSDSCPullServer] Check State            
SRV1   VERBOSE      6/24/2016 11:36:56 AM [SRV1]:                            [[xDSCWebService]PSDSCPullServer] Get Full Path for We...
SRV1   VERBOSE      6/24/2016 11:36:56 AM [SRV1]: LCM:  [ End    Test     ]  [[xDSCWebService]PSDSCPullServer] True in 0.0160 seconds.
SRV1   VERBOSE      6/24/2016 11:36:56 AM [SRV1]: LCM:  [ End    Resource ]  [[xDSCWebService]PSDSCPullServer]                        
SRV1   VERBOSE      6/24/2016 11:36:56 AM [SRV1]:                            [] Consistency check completed.                          
SRV1   ANALYTIC     6/24/2016 11:36:56 AM Deleting file from C:\Windows\System32\Configuration\DSCEngineCache.mof                             
SRV1   OPERATIONAL  6/24/2016 11:36:56 AM Consistency engine was run successfully.                                                            
SRV1   OPERATIONAL  6/24/2016 11:36:56 AM Job runs under the following LCM setting. ...                                                       
SRV1   OPERATIONAL  6/24/2016 11:36:56 AM Operation Consistency Check or Pull completed successfully.                                         
SRV1   ANALYTIC     6/24/2016 11:36:56 AM Deleting file from C:\Windows\System32\Configuration\DSCEngineCache.mof
```

<span data-ttu-id="3557f-193">Vegye figyelembe a következőket, azóta `Trace-xDscOperation` események összesíti az elemző, a Debug és műveleti naplói, akkor arra fogja kérni, hogy ezek a naplók engedélyezése a fent leírt módon.</span><span class="sxs-lookup"><span data-stu-id="3557f-193">Note that, since `Trace-xDscOperation` aggregates events from the Analytic, Debug, and Operational logs, it will prompt you to enable these logs as described above.</span></span>

<span data-ttu-id="3557f-194">Alternatív megoldásként adatokat gyűjthet a események kimenete mentésével `Trace-xDscOperation` egy változóba.</span><span class="sxs-lookup"><span data-stu-id="3557f-194">Alternately, you can gather information on the events by saving the output of `Trace-xDscOperation` into a variable.</span></span> <span data-ttu-id="3557f-195">A következő parancsok segítségével egy DSC művelethez tartozó összes esemény megjelenítése.</span><span class="sxs-lookup"><span data-stu-id="3557f-195">You can use the following commands to display all the events for a particular DSC operation.</span></span>

```powershell
PS C:\DiagnosticsTest> $Trace = Trace-xDscOperation -SequenceID 4

PS C:\DiagnosticsTest> $Trace.Event
```

<span data-ttu-id="3557f-196">Megjelenik az azonos a `Get-WinEvent` parancsmag, például az alábbi kimenetben:</span><span class="sxs-lookup"><span data-stu-id="3557f-196">This will display the same results as the `Get-WinEvent` cmdlet, such as in the output below:</span></span>

```powershell
   ProviderName: Microsoft-Windows-DSC

TimeCreated                     Id LevelDisplayName Message                                                                                           
-----------                     -- ---------------- -------                                                                                           
6/23/2016 1:36:53 AM          4312 Information      The DscTimer is running LCM method PerformRequiredConfigurationChecks with the flag set to 5.     
6/23/2016 1:36:53 AM          4343 Information      The DscTimer has successfully run LCM method PerformRequiredConfigurationChecks with flag 5.      
6/23/2016 2:07:00 AM          4312 Information      The DscTimer is running LCM method PerformRequiredConfigurationChecks with the flag set to 5.     
6/23/2016 2:07:01 AM          4343 Information      The DscTimer has successfully run LCM method PerformRequiredConfigurationChecks with flag 5.      
6/23/2016 2:36:55 AM          4312 Information      The DscTimer is running LCM method PerformRequiredConfigurationChecks with the flag set to 5.     
6/23/2016 2:36:56 AM          4343 Information      The DscTimer has successfully run LCM method PerformRequiredConfigurationChecks with flag 5.      
6/23/2016 3:06:55 AM          4312 Information      The DscTimer is running LCM method PerformRequiredConfigurationChecks with the flag set to 5.     
6/23/2016 3:06:55 AM          4343 Information      The DscTimer has successfully run LCM method PerformRequiredConfigurationChecks with flag 5.      
6/23/2016 3:36:55 AM          4312 Information      The DscTimer is running LCM method PerformRequiredConfigurationChecks with the flag set to 5.     
6/23/2016 3:36:55 AM          4343 Information      The DscTimer has successfully run LCM method PerformRequiredConfigurationChecks with flag 5.      
6/23/2016 4:06:53 AM          4312 Information      The DscTimer is running LCM method PerformRequiredConfigurationChecks with the flag set to 5.     
6/23/2016 4:06:53 AM          4343 Information      The DscTimer has successfully run LCM method PerformRequiredConfigurationChecks with flag 5.      
6/23/2016 4:36:52 AM          4312 Information      The DscTimer is running LCM method PerformRequiredConfigurationChecks with the flag set to 5.     
6/23/2016 4:36:53 AM          4343 Information      The DscTimer has successfully run LCM method PerformRequiredConfigurationChecks with flag 5.      
6/23/2016 5:06:52 AM          4312 Information      The DscTimer is running LCM method PerformRequiredConfigurationChecks with the flag set to 5.     
6/23/2016 5:06:53 AM          4343 Information      The DscTimer has successfully run LCM method PerformRequiredConfigurationChecks with flag 5.      
6/23/2016 5:36:54 AM          4312 Information      The DscTimer is running LCM method PerformRequiredConfigurationChecks with the flag set to 5.     
6/23/2016 5:36:54 AM          4343 Information      The DscTimer has successfully run LCM method PerformRequiredConfigurationChecks with flag 5.      
6/23/2016 6:06:52 AM          4312 Information      The DscTimer is running LCM method PerformRequiredConfigurationChecks with the flag set to 5.     
6/23/2016 6:06:53 AM          4343 Information      The DscTimer has successfully run LCM method PerformRequiredConfigurationChecks with flag 5.      
6/23/2016 6:36:56 AM          4312 Information      The DscTimer is running LCM method PerformRequiredConfigurationChecks with the flag set to 5.     
6/23/2016 6:36:57 AM          4343 Information      The DscTimer has successfully run LCM method PerformRequiredConfigurationChecks with flag 5.      
6/23/2016 7:06:52 AM          4312 Information      The DscTimer is running LCM method PerformRequiredConfigurationChecks with the flag set to 5.     
6/23/2016 7:06:53 AM          4343 Information      The DscTimer has successfully run LCM method PerformRequiredConfigurationChecks with flag 5.      
6/23/2016 7:36:53 AM          4312 Information      The DscTimer is running LCM method PerformRequiredConfigurationChecks with the flag set to 5.     
6/23/2016 7:36:54 AM          4343 Information      The DscTimer has successfully run LCM method PerformRequiredConfigurationChecks with flag 5.      
6/23/2016 8:06:54 AM          4312 Information      The DscTimer is running LCM method PerformRequiredConfigurationChecks with the flag set to 5.
```

<span data-ttu-id="3557f-197">Ideális esetben először használja `Get-xDscOperation` listázásához, az elmúlt néhány DSC konfigurációs a gépeken futtatja.</span><span class="sxs-lookup"><span data-stu-id="3557f-197">Ideally, you would first use `Get-xDscOperation` to list out the last few DSC configuration runs on your machines.</span></span> <span data-ttu-id="3557f-198">Ezt követően ellenőrizheti bármely (a SequenceID vagy JobID használatával) egyetlen művelettel rendelkező `Trace-xDscOperation` felderítésére, mi ugyanúgy a háttérben.</span><span class="sxs-lookup"><span data-stu-id="3557f-198">Following this, you can examine any single operation (using its SequenceID or JobID) with `Trace-xDscOperation` to discover what it did behind the scenes.</span></span>

### <a name="getting-events-for-a-remote-computer"></a><span data-ttu-id="3557f-199">Egy távoli számítógépen eseményeinek beolvasása</span><span class="sxs-lookup"><span data-stu-id="3557f-199">Getting events for a remote computer</span></span>

<span data-ttu-id="3557f-200">Használja a `ComputerName` paramétere a `Trace-xDscOperation` parancsmagot, hogy megkapja az esemény részleteit egy távoli számítógépen.</span><span class="sxs-lookup"><span data-stu-id="3557f-200">Use the `ComputerName` parameter of the `Trace-xDscOperation` cmdlet to get the event details on a remote computer.</span></span> <span data-ttu-id="3557f-201">Ezt megteheti, hogy kell hozzon létre egy tűzfalszabályt a távfelügyelet engedélyezéséhez a távoli számítógépen:</span><span class="sxs-lookup"><span data-stu-id="3557f-201">Before you can do this, you have to create a firewall rule to allow remote administration on the remote computer:</span></span>

```powershell
New-NetFirewallRule -Name "Service RemoteAdmin" -DisplayName "Remote" -Action Allow
```
<span data-ttu-id="3557f-202">A hívás adhat meg, hogy a számítógép most `Trace-xDscOperation`:</span><span class="sxs-lookup"><span data-stu-id="3557f-202">Now you can specify that computer in your call to `Trace-xDscOperation`:</span></span>

```powershell
PS C:\DiagnosticsTest> Trace-xDscOperation -ComputerName SRV2 -Credential Get-Credential -SequenceID 5

ComputerName   EventType    TimeCreated           Message
------------   ---------    -----------           -------
SRV2   OPERATIONAL  6/24/2016 11:36:56 AM Operation Consistency Check or Pull started by user sid S-1-5-20 f...
SRV2   ANALYTIC     6/24/2016 11:36:56 AM Deleting file from C:\Windows\System32\Configuration\DSCEngineCach...
SRV2   OPERATIONAL  6/24/2016 11:36:56 AM Running consistency engine.
SRV2   VERBOSE      6/24/2016 11:36:56 AM [SRV2]:                            [] Starting consistency...
SRV2   ANALYTIC     6/24/2016 11:36:56 AM Applying configuration from C:\Windows\System32\Configuration\Curr...
SRV2   ANALYTIC     6/24/2016 11:36:56 AM Parsing the configuration to apply.
SRV2   OPERATIONAL  6/24/2016 11:36:56 AM  Resource execution sequence :: [WindowsFeature]DSCServiceFeature,...
SRV2   VERBOSE      6/24/2016 11:36:56 AM [SRV2]: LCM:  [ Start  Resource ]  [[WindowsFeature]DSCSer...
SRV2   ANALYTIC     6/24/2016 11:36:56 AM Executing operations for PS DSC resource MSFT_RoleResource with re...
SRV2   VERBOSE      6/24/2016 11:36:56 AM [SRV2]: LCM:  [ Start  Test     ]  [[WindowsFeature]DSCSer...
SRV2   VERBOSE      6/24/2016 11:36:56 AM [SRV2]:                            [[WindowsFeature]DSCSer...
SRV2   VERBOSE      6/24/2016 11:36:56 AM [SRV2]:                            [[WindowsFeature]DSCSer...
SRV2   VERBOSE      6/24/2016 11:36:56 AM [SRV2]: LCM:  [ End    Test     ]  [[WindowsFeature]DSCSer...
SRV2   VERBOSE      6/24/2016 11:36:56 AM [SRV2]: LCM:  [ End    Resource ]  [[WindowsFeature]DSCSer...
SRV2   VERBOSE      6/24/2016 11:36:56 AM [SRV2]: LCM:  [ Start  Resource ]  [[xDSCWebService]PSDSCP...
SRV2   ANALYTIC     6/24/2016 11:36:56 AM Executing operations for PS DSC resource MSFT_xDSCWebService with ...
SRV2   VERBOSE      6/24/2016 11:36:56 AM [SRV2]: LCM:  [ Start  Test     ]  [[xDSCWebService]PSDSCP...
SRV2   VERBOSE      6/24/2016 11:36:56 AM [SRV2]:                            [[xDSCWebService]PSDSCP...
SRV2   VERBOSE      6/24/2016 11:36:56 AM [SRV2]:                            [[xDSCWebService]PSDSCP...
SRV2   VERBOSE      6/24/2016 11:36:56 AM [SRV2]:                            [[xDSCWebService]PSDSCP...
SRV2   VERBOSE      6/24/2016 11:36:56 AM [SRV2]:                            [[xDSCWebService]PSDSCP...
SRV2   VERBOSE      6/24/2016 11:36:56 AM [SRV2]:                            [[xDSCWebService]PSDSCP...
SRV2   VERBOSE      6/24/2016 11:36:56 AM [SRV2]: LCM:  [ End    Test     ]  [[xDSCWebService]PSDSCP...
SRV2   VERBOSE      6/24/2016 11:36:56 AM [SRV2]: LCM:  [ End    Resource ]  [[xDSCWebService]PSDSCP...
SRV2   VERBOSE      6/24/2016 11:36:56 AM [SRV2]:                            [] Consistency check co...
SRV2   ANALYTIC     6/24/2016 11:36:56 AM Deleting file from C:\Windows\System32\Configuration\DSCEngineCach...
SRV2   OPERATIONAL  6/24/2016 11:36:56 AM Consistency engine was run successfully.
SRV2   OPERATIONAL  6/24/2016 11:36:56 AM Job runs under the following LCM setting. ...
SRV2   OPERATIONAL  6/24/2016 11:36:56 AM Operation Consistency Check or Pull completed successfully.
SRV2   ANALYTIC     6/24/2016 11:36:56 AM Deleting file from C:\Windows\System32\Configuration\DSCEngineCach...
```

## <a name="my-resources-wont-update-how-to-reset-the-cache"></a><span data-ttu-id="3557f-203">Az erőforrások nem frissíti: a gyorsítótár visszaállítása</span><span class="sxs-lookup"><span data-stu-id="3557f-203">My resources won’t update: How to reset the cache</span></span>

<span data-ttu-id="3557f-204">A DSC-motor valósul meg egy PowerShell-modul hatékonyságát célokra erőforrások gyorsítótárazza.</span><span class="sxs-lookup"><span data-stu-id="3557f-204">The DSC engine caches resources implemented as a PowerShell module for efficiency purposes.</span></span> <span data-ttu-id="3557f-205">Azonban ez problémát okozhat erőforrás szerzői és egyidejűleg tesztelése, mert DSC betölti a gyorsítótárazott verzió, a folyamat újraindításáig.</span><span class="sxs-lookup"><span data-stu-id="3557f-205">However, this can cause problems when you are authoring a resource and testing it simultaneously because DSC will load the cached version until the process is restarted.</span></span> <span data-ttu-id="3557f-206">Csak az újabb verzió betöltése DSC végrehajtásához, explicit módon leállítani a folyamatot a DSC-motor.</span><span class="sxs-lookup"><span data-stu-id="3557f-206">The only way to make DSC load the newer version is to explicitly kill the process hosting the DSC engine.</span></span>

<span data-ttu-id="3557f-207">Hasonlóképpen, ha futtatja `Start-DscConfiguration`, után, és egyéni erőforrás módosításának a módosítás lehet, hogy nem hajthatók végre, vagy, amíg a számítógép újraindítása után.</span><span class="sxs-lookup"><span data-stu-id="3557f-207">Similarly, when you run `Start-DscConfiguration`, after adding and modifying a custom resource, the modification may not execute unless, or until, the computer is rebooted.</span></span> <span data-ttu-id="3557f-208">Ennek az az oka DSC futtatja a WMI-szolgáltató gazdafolyamat (WmiPrvSE), és általában több példánya van WmiPrvSE fut egyszerre.</span><span class="sxs-lookup"><span data-stu-id="3557f-208">This is because DSC runs in the WMI Provider Host Process (WmiPrvSE), and usually, there are many instances of WmiPrvSE running at once.</span></span> <span data-ttu-id="3557f-209">Újraindításakor, a gazdagép folyamatot, és a gyorsítótár nincs bejelölve.</span><span class="sxs-lookup"><span data-stu-id="3557f-209">When you reboot, the host process is restarted and the cache is cleared.</span></span>

<span data-ttu-id="3557f-210">Sikeres hasznosítsa újra a konfigurációt, és anélkül a gyorsítótárat kiürítheti, állítsa le és indítsa újra a gazdagép-folyamat.</span><span class="sxs-lookup"><span data-stu-id="3557f-210">To successfully recycle the configuration and clear the cache without rebooting, you must stop and then restart the host process.</span></span> <span data-ttu-id="3557f-211">Ezt megteheti / példány alapon, amelynek során a folyamat azonosítására, állítsa le és indítsa újra.</span><span class="sxs-lookup"><span data-stu-id="3557f-211">This can be done on a per instance basis, whereby you identify the process, stop it, and restart it.</span></span> <span data-ttu-id="3557f-212">Másik lehetőségként használhatja `DebugMode`, ahogyan az alábbi töltse be újra a PowerShell DSC-erőforrás.</span><span class="sxs-lookup"><span data-stu-id="3557f-212">Or, you can use `DebugMode`, as demonstrated below, to reload the PowerShell DSC resource.</span></span>

<span data-ttu-id="3557f-213">Azonosíthatja, melyik folyamat üzemelteti a DSC-motor, és állítsa le a / példány alapon, listázhatja a WmiPrvSE, amely üzemelteti a DSC-motor Folyamatazonosítója.</span><span class="sxs-lookup"><span data-stu-id="3557f-213">To identify which process is hosting the DSC engine and stop it on a per instance basis, you can list the process ID of the WmiPrvSE which is hosting the DSC engine.</span></span> <span data-ttu-id="3557f-214">Ezt követően frissítse a szolgáltatót, állítsa le a WmiPrvSE folyamatot az alábbi parancsok használatával, és futtassa **Start-DscConfiguration** újra.</span><span class="sxs-lookup"><span data-stu-id="3557f-214">Then, to update the provider, stop the WmiPrvSE process using the commands below, and then run **Start-DscConfiguration** again.</span></span>

```powershell
###
### find the process that is hosting the DSC engine
###
$dscProcessID = Get-WmiObject msft_providers | 
Where-Object {$_.provider -like 'dsccore'} | 
Select-Object -ExpandProperty HostProcessIdentifier 

###
### Stop the process
###
Get-Process -Id $dscProcessID | Stop-Process
```

## <a name="using-debugmode"></a><span data-ttu-id="3557f-215">DebugMode használatával</span><span class="sxs-lookup"><span data-stu-id="3557f-215">Using DebugMode</span></span>

<span data-ttu-id="3557f-216">A DSC helyi Configuration Manager (LCM) használatára konfigurálhatja `DebugMode` mindig törölje a gyorsítótár, a gazdagép-folyamat újraindításakor.</span><span class="sxs-lookup"><span data-stu-id="3557f-216">You can configure the DSC Local Configuration Manager (LCM) to use `DebugMode` to always clear the cache when the host process is restarted.</span></span> <span data-ttu-id="3557f-217">Ha beállítása **igaz**, azt eredményezi, hogy a motor mindig töltse be újra a PowerShell DSC-erőforrás.</span><span class="sxs-lookup"><span data-stu-id="3557f-217">When set to **TRUE**, it causes the engine to always reload the PowerShell DSC resource.</span></span> <span data-ttu-id="3557f-218">Miután a ír, az erőforrás, állíthatja vissza a **hamis** és a motor visszaállítja a modulok gyorsítótárazásának működése.</span><span class="sxs-lookup"><span data-stu-id="3557f-218">Once you are done writing your resource, you can set it back to **FALSE** and the engine will revert to its behavior of caching the modules.</span></span>

<span data-ttu-id="3557f-219">Az alábbiakban látható egy bemutató megjelenítendő hogyan `DebugMode` automatikusan is frissítheti a gyorsítótárban.</span><span class="sxs-lookup"><span data-stu-id="3557f-219">Following is a demonstration to show how `DebugMode` can automatically refresh the cache.</span></span> <span data-ttu-id="3557f-220">Először az alapértelmezett konfiguráció vizsgáljuk meg:</span><span class="sxs-lookup"><span data-stu-id="3557f-220">First, let’s look at the default configuration:</span></span>

```
PS C:\> Get-DscLocalConfigurationManager
 
 
AllowModuleOverwrite           : False
CertificateID                  : 
ConfigurationID                : 
ConfigurationMode              : ApplyAndMonitor
ConfigurationModeFrequencyMins : 30
Credential                     : 
DebugMode                      : False
DownloadManagerCustomData      : 
DownloadManagerName            : 
LocalConfigurationManagerState : Ready
RebootNodeIfNeeded             : False
RefreshFrequencyMins           : 15
RefreshMode                    : PUSH
PSComputerName                 :  
```

<span data-ttu-id="3557f-221">Láthatja, hogy `DebugMode` értéke **hamis**.</span><span class="sxs-lookup"><span data-stu-id="3557f-221">You can see that `DebugMode` is set to **FALSE**.</span></span>

<span data-ttu-id="3557f-222">Beállítása a `DebugMode` bemutató, használja a következő PowerShell-erőforrás:</span><span class="sxs-lookup"><span data-stu-id="3557f-222">To set up the `DebugMode` demonstration, use the following PowerShell resource:</span></span>

```powershell
function Get-TargetResource
{
    param
    (
        [Parameter(Mandatory)]
        $onlyProperty
    )
    return @{onlyProperty = Get-Content -Path "$env:SystemDrive\OutputFromTestProviderDebugMode.txt"}
}
function Set-TargetResource
{
    param
    (
        [Parameter(Mandatory)]
        $onlyProperty
    )
    "1" | Out-File -PSPath "$env:SystemDrive\OutputFromTestProviderDebugMode.txt"
}
function Test-TargetResource
{
    param
    (
        [Parameter(Mandatory)]
        $onlyProperty
    )
    return $false
} 
```

<span data-ttu-id="3557f-223">Most, szerzői egy konfigurációval, a fenti erőforrás neve `TestProviderDebugMode`:</span><span class="sxs-lookup"><span data-stu-id="3557f-223">Now, author a configuration using the above resource called `TestProviderDebugMode`:</span></span>

```powershell
Configuration ConfigTestDebugMode
{
    Import-DscResource -Name TestProviderDebugMode
    Node localhost
    {
        TestProviderDebugMode test
        {
            onlyProperty = "blah"
        }
    }
}
ConfigTestDebugMode
```

<span data-ttu-id="3557f-224">Látni fogja, hogy a fájl tartalmát: "**$env:SystemDrive\OutputFromTestProviderDebugMode.txt**" van **1**.</span><span class="sxs-lookup"><span data-stu-id="3557f-224">You will see that the contents of file: “**$env:SystemDrive\OutputFromTestProviderDebugMode.txt**” is **1**.</span></span>

<span data-ttu-id="3557f-225">Most frissítse a szolgáltatót kódot használja a következő parancsfájlt:</span><span class="sxs-lookup"><span data-stu-id="3557f-225">Now, update the provider code using the following script:</span></span>

```powershell
$newResourceOutput = Get-Random -Minimum 5 -Maximum 30
$content = @"
function Get-TargetResource
{
    param
    (
        [Parameter(Mandatory)]
        `$onlyProperty
    )
    return @{onlyProperty = Get-Content -Path "$env:SystemDrive\OutputFromTestProviderDebugMode.txt"}
}
function Set-TargetResource
{
    param
    (
        [Parameter(Mandatory)]
        `$onlyProperty
    )
    "$newResourceOutput" | Out-File -PSPath C:\OutputFromTestProviderDebugMode.txt
}
function Test-TargetResource
{
    param
    (
        [Parameter(Mandatory)]
        `$onlyProperty
    )
    return `$false
}
"@ | Out-File -FilePath "C:\Program Files\WindowsPowerShell\Modules\MyPowerShellModules\DSCResources\TestProviderDebugMode\TestProviderDebugMode.psm1
```

<span data-ttu-id="3557f-226">Ezt a parancsfájlt hoz létre egy véletlenszerű számot, és ennek megfelelően frissíti a szolgáltató kódot.</span><span class="sxs-lookup"><span data-stu-id="3557f-226">This script generates a random number and updates the provider code accordingly.</span></span> <span data-ttu-id="3557f-227">A `DebugMode` értéke HAMIS, a fájl tartalmát "**$env:SystemDrive\OutputFromTestProviderDebugMode.txt**" soha nem módosulnak.</span><span class="sxs-lookup"><span data-stu-id="3557f-227">With `DebugMode` set to false, the contents of the file “**$env:SystemDrive\OutputFromTestProviderDebugMode.txt**” are never changed.</span></span>

<span data-ttu-id="3557f-228">Most, `DebugMode` való **igaz** konfigurációs parancsfájlban:</span><span class="sxs-lookup"><span data-stu-id="3557f-228">Now, set `DebugMode` to **TRUE** in your configuration script:</span></span>

```powershell
LocalConfigurationManager
{
    DebugMode = $true
} 
```

<span data-ttu-id="3557f-229">Ha a fenti szkript újra futtatja, látni fogja, hogy a fájl tartalma különböző minden alkalommal.</span><span class="sxs-lookup"><span data-stu-id="3557f-229">When you run the above script again, you will see that the content of the file is different every time.</span></span> <span data-ttu-id="3557f-230">(Futtatása `Get-DscConfiguration` , hogy).</span><span class="sxs-lookup"><span data-stu-id="3557f-230">(You can run `Get-DscConfiguration` to check it).</span></span> <span data-ttu-id="3557f-231">Az alábbiakban oka két további fut (a eredmény lehetnek a parancsfájl futtatásakor):</span><span class="sxs-lookup"><span data-stu-id="3557f-231">Below is the result of two additional runs (your results may be different when you run the script):</span></span>

```powershell
PS C:\> Get-DscConfiguration -CimSession (New-CimSession localhost)
 
onlyProperty                            PSComputerName                         
------------                            --------------                         
20                                      localhost                              
 
PS C:\> Get-DscConfiguration -CimSession (New-CimSession localhost)
 
onlyProperty                            PSComputerName                         
------------                            --------------                         
14                                      localhost
```

## <a name="see-also"></a><span data-ttu-id="3557f-232">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="3557f-232">See Also</span></span>

### <a name="reference"></a><span data-ttu-id="3557f-233">Referencia</span><span class="sxs-lookup"><span data-stu-id="3557f-233">Reference</span></span>
* [<span data-ttu-id="3557f-234">A DSC-napló erőforrás</span><span class="sxs-lookup"><span data-stu-id="3557f-234">DSC Log Resource</span></span>](logResource.md)

### <a name="concepts"></a><span data-ttu-id="3557f-235">Fogalmak</span><span class="sxs-lookup"><span data-stu-id="3557f-235">Concepts</span></span>
* [<span data-ttu-id="3557f-236">Egyéni Windows PowerShell kívánt állapot konfigurációs erőforrások létrehozása</span><span class="sxs-lookup"><span data-stu-id="3557f-236">Build Custom Windows PowerShell Desired State Configuration Resources</span></span>](authoringResource.md)

### <a name="other-resources"></a><span data-ttu-id="3557f-237">Egyéb források</span><span class="sxs-lookup"><span data-stu-id="3557f-237">Other Resources</span></span>
* <span data-ttu-id="3557f-238">[A Windows PowerShell célállapot-konfiguráló parancsmagok](https://technet.microsoft.com/library/dn521624(v=wps.630).aspx)</span><span class="sxs-lookup"><span data-stu-id="3557f-238">[Windows PowerShell Desired State Configuration Cmdlets](https://technet.microsoft.com/library/dn521624(v=wps.630).aspx)</span></span>

