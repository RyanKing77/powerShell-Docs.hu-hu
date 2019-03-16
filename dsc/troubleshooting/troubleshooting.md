---
ms.date: 10/30/2018
keywords: DSC, powershell, a konfigurációt, a beállítása
title: A DSC hibaelhárítása
ms.openlocfilehash: 5ee1b68f4f769426fea3c8e10738c3bb6ef94480
ms.sourcegitcommit: caac7d098a448232304c9d6728e7340ec7517a71
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/16/2019
ms.locfileid: "58059745"
---
# <a name="troubleshooting-dsc"></a><span data-ttu-id="ed580-103">A DSC hibaelhárítása</span><span class="sxs-lookup"><span data-stu-id="ed580-103">Troubleshooting DSC</span></span>

<span data-ttu-id="ed580-104">_A következőkre vonatkozik: Windows PowerShell 4.0-s, a Windows PowerShell 5.0_</span><span class="sxs-lookup"><span data-stu-id="ed580-104">_Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0_</span></span>

<span data-ttu-id="ed580-105">Ez a témakör ismerteti azokat a módszereket a DSC elhárításához, ha problémák merülnek fel.</span><span class="sxs-lookup"><span data-stu-id="ed580-105">This topic describes ways to troubleshoot DSC when problems arise.</span></span>

## <a name="winrm-dependency"></a><span data-ttu-id="ed580-106">A WinRM-függőség</span><span class="sxs-lookup"><span data-stu-id="ed580-106">WinRM Dependency</span></span>

<span data-ttu-id="ed580-107">Windows PowerShell Desired State Configuration (DSC) attól függ, hogy a Rendszerfelügyeleti webszolgáltatások.</span><span class="sxs-lookup"><span data-stu-id="ed580-107">Windows PowerShell Desired State Configuration (DSC) depends on WinRM.</span></span> <span data-ttu-id="ed580-108">A Rendszerfelügyeleti webszolgáltatások a Windows Server 2008 R2 és Windows 7 alapértelmezés szerint nincs engedélyezve.</span><span class="sxs-lookup"><span data-stu-id="ed580-108">WinRM is not enabled by default on Windows Server 2008 R2 and Windows 7.</span></span> <span data-ttu-id="ed580-109">Futtatás `Set-WSManQuickConfig`, egy Windows PowerShell az emelt szintű ahhoz, hogy a WinRM-munkamenetben.</span><span class="sxs-lookup"><span data-stu-id="ed580-109">Run `Set-WSManQuickConfig`, in a Windows PowerShell elevated session, to enable WinRM.</span></span>

## <a name="using-get-dscconfigurationstatus"></a><span data-ttu-id="ed580-110">Get-DscConfigurationStatus használatával</span><span class="sxs-lookup"><span data-stu-id="ed580-110">Using Get-DscConfigurationStatus</span></span>

<span data-ttu-id="ed580-111">A [Get-DscConfigurationStatus](/powershell/module/PSDesiredStateConfiguration/Get-DscConfigurationStatus) parancsmag konfigurációs állapotára vonatkozó információkat olvas be egy célcsomóponttal.</span><span class="sxs-lookup"><span data-stu-id="ed580-111">The [Get-DscConfigurationStatus](/powershell/module/PSDesiredStateConfiguration/Get-DscConfigurationStatus) cmdlet gets information about configuration status from a target node.</span></span> <span data-ttu-id="ed580-112">Egy gazdag objektumot ad vissza, amely tartalmazza-e a konfigurációs Futtatás sikeres volt-e magas szintű információkat.</span><span class="sxs-lookup"><span data-stu-id="ed580-112">A rich object is returned that includes high-level information about whether or not the configuration run was successful or not.</span></span> <span data-ttu-id="ed580-113">Meg is tárja az objektum felderítését, például futtassa a konfiguráció részleteit:</span><span class="sxs-lookup"><span data-stu-id="ed580-113">You can dig into the object to discover details about the configuration run such as:</span></span>

- <span data-ttu-id="ed580-114">Az összes erőforrást, amely nem sikerült</span><span class="sxs-lookup"><span data-stu-id="ed580-114">All of the resources that failed</span></span>
- <span data-ttu-id="ed580-115">Bármely erőforrás kért újraindítás</span><span class="sxs-lookup"><span data-stu-id="ed580-115">Any resource that requested a reboot</span></span>
- <span data-ttu-id="ed580-116">Meta-konfigurációs beállítások konfigurációs időpontjában futtatása</span><span class="sxs-lookup"><span data-stu-id="ed580-116">Meta-Configuration settings at time of configuration run</span></span>
- <span data-ttu-id="ed580-117">Etc.</span><span class="sxs-lookup"><span data-stu-id="ed580-117">Etc.</span></span>

<span data-ttu-id="ed580-118">A következő paraméterkészletet adja vissza a legutóbbi konfiguráció futtatása állapotinformációit:</span><span class="sxs-lookup"><span data-stu-id="ed580-118">The following parameter set returns the status information for the last configuration run:</span></span>

```
Get-DscConfigurationStatus [-CimSession <CimSession[]>]
                           [-ThrottleLimit <int>]
                           [-AsJob]
                           [<CommonParameters>]
```
<span data-ttu-id="ed580-119">A következő paraméterkészletet az összes korábbi konfigurációs futtatások állapotának adatait adja vissza:</span><span class="sxs-lookup"><span data-stu-id="ed580-119">The following parameter set returns the status information for all previous configuration runs:</span></span>

```
Get-DscConfigurationStatus -All
                           [-CimSession <CimSession[]>]
                           [-ThrottleLimit <int>]
                           [-AsJob]
                           [<CommonParameters>]
```

## <a name="example"></a><span data-ttu-id="ed580-120">Példa</span><span class="sxs-lookup"><span data-stu-id="ed580-120">Example</span></span>

```powershell
PS C:\> $Status = Get-DscConfigurationStatus

PS C:\> $Status

Status         StartDate                Type            Mode    RebootRequested        NumberOfResources
------        ---------                ----            ----    ---------------        -----------------
Failure        11/24/2015  3:44:56     Consistency        Push    True                36

PS C:\> $Status.ResourcesNotInDesiredState

ConfigurationName     :    MyService
DependsOn             :
ModuleName            :    PSDesiredStateConfiguration
ModuleVersion         :    1.1
PsDscRunAsCredential  :
ResourceID            :    [File]ServiceDll
SourceInfo            :    c:\git\CustomerService\Configs\MyCustomService.ps1::5::34::File
DurationInSeconds     :    0.19
Error                 :    SourcePath must be accessible for current configuration. The related file/directory is:
                           \\Server93\Shared\contosoApp.dll. The related ResourceID is [File]ServiceDll
FinalState            :
InDesiredState        :    False
InitialState          :
InstanceName          :    ServiceDll
RebootRequested       :    False
ResourceName          :    File
StartDate             :    11/24/2015  3:44:56
PSComputerName        :
```

## <a name="my-script-wont-run-using-dsc-logs-to-diagnose-script-errors"></a><span data-ttu-id="ed580-121">A parancsfájl futtatásának megakadályozása: DSC használatával naplózza a parancsprogram-hibák diagnosztizálása</span><span class="sxs-lookup"><span data-stu-id="ed580-121">My script won't run: Using DSC logs to diagnose script errors</span></span>

<span data-ttu-id="ed580-122">Minden Windows szoftverek, például DSC rögzíti a hibák és események [naplók](/windows/desktop/EventLog/about-event-logging) tekinthetnek meg az a [Eseménynapló](https://support.microsoft.com/hub/4338813/windows-help).</span><span class="sxs-lookup"><span data-stu-id="ed580-122">Like all Windows software, DSC records errors and events in [logs](/windows/desktop/EventLog/about-event-logging) that can be viewed from the [Event Viewer](https://support.microsoft.com/hub/4338813/windows-help).</span></span>
<span data-ttu-id="ed580-123">Ezek a naplók vizsgálata segítségével megtudhatja, miért nem sikerült egy adott művelet, és hogyan hibája megakadályozza a jövőben.</span><span class="sxs-lookup"><span data-stu-id="ed580-123">Examining these logs can help you understand why a particular operation failed, and how to prevent failure in the future.</span></span> <span data-ttu-id="ed580-124">Konfigurációs parancsfájlok írása lehet megkülönböztetni, ezért a követési hibákat egyszerűbb, Szerző, a konfiguráció a DSC elemzési eseménynaplójában az előrehaladását úgy követheti nyomon a DSC-Log erőforrás használatával.</span><span class="sxs-lookup"><span data-stu-id="ed580-124">Writing configuration scripts can be tricky, so to make tracking errors easier as you author, use the DSC Log resource to track the progress of your configuration in the DSC Analytic event log.</span></span>

## <a name="where-are-dsc-event-logs"></a><span data-ttu-id="ed580-125">Hol találhatók a DSC-eseménynaplók?</span><span class="sxs-lookup"><span data-stu-id="ed580-125">Where are DSC event logs?</span></span>

<span data-ttu-id="ed580-126">Az Eseménynapló DSC események szerepelnek: **Alkalmazások és szolgáltatások Logs/Microsoft/Windows/Desired State Configuration**</span><span class="sxs-lookup"><span data-stu-id="ed580-126">In Event Viewer, DSC events are in: **Applications and Services Logs/Microsoft/Windows/Desired State Configuration**</span></span>

<span data-ttu-id="ed580-127">A megfelelő PowerShell-parancsmag [Get-WinEvent](/powershell/module/Microsoft.PowerShell.Diagnostics/Get-WinEvent), tekintse meg az eseménynaplókat, is futtathatók:</span><span class="sxs-lookup"><span data-stu-id="ed580-127">The corresponding PowerShell cmdlet, [Get-WinEvent](/powershell/module/Microsoft.PowerShell.Diagnostics/Get-WinEvent), can also be run to view the event logs:</span></span>

```
PS C:\> Get-WinEvent -LogName "Microsoft-Windows-Dsc/Operational"

   ProviderName: Microsoft-Windows-DSC

TimeCreated                     Id LevelDisplayName Message
-----------                     -- ---------------- -------
11/17/2014 10:27:23 PM        4102 Information      Job {02C38626-D95A-47F1-9DA2-C1D44A7128E7} :
```

<span data-ttu-id="ed580-128">A fentiek DSC tartozó elsődleges naplófájl neve: **Microsoft -> Windows -> DSC** (a Windows más napló neve nem jelennek itt kivonatosan).</span><span class="sxs-lookup"><span data-stu-id="ed580-128">As shown above, DSC's primary log name is **Microsoft->Windows->DSC** (other log names under Windows are not shown here for brevity).</span></span> <span data-ttu-id="ed580-129">Az elsődleges név a rendszer hozzáfűzi a csatorna neve hozhat létre a naplófájl teljes neve.</span><span class="sxs-lookup"><span data-stu-id="ed580-129">The primary name is appended to the channel name to create the complete log name.</span></span> <span data-ttu-id="ed580-130">A DSC motor elsősorban három típusú naplók írja: [Műveleti, elemzési és hibakeresési naplók](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc722404(v=ws.11)).</span><span class="sxs-lookup"><span data-stu-id="ed580-130">The DSC engine writes mainly into three types of logs: [Operational, Analytic, and Debug logs](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc722404(v=ws.11)).</span></span> <span data-ttu-id="ed580-131">Mivel az elemzési és hibakeresési naplók alapértelmezés szerint ki van kapcsolva, engedélyezze a őket az eseménynaplóban.</span><span class="sxs-lookup"><span data-stu-id="ed580-131">Since the analytic and debug logs are turned off by default, you should enable them in Event Viewer.</span></span> <span data-ttu-id="ed580-132">Ehhez nyissa meg az eseménynaplót a Windows PowerShellben; Show-Eseménynapló beírásával vagy kattintson a **Start** gombra, majd **Vezérlőpult**, kattintson a **felügyeleti eszközök**, és kattintson a **Eseménynapló**.</span><span class="sxs-lookup"><span data-stu-id="ed580-132">To do this, open Event Viewer by typing Show-EventLog in Windows PowerShell; or, click the **Start** button, click **Control Panel**, click **Administrative Tools**, and then click **Event Viewer**.</span></span>
<span data-ttu-id="ed580-133">Az a **nézet** az eseménynaplóban menüjében kattintson **elemzési és hibakeresési naplók megjelenítése**.</span><span class="sxs-lookup"><span data-stu-id="ed580-133">On the **View** menu in Event viewer, click **Show Analytic and Debug Logs**.</span></span> <span data-ttu-id="ed580-134">A naplófájl neve az elemzési csatorna **elemzési Microsoft-Windows-Dsc**, és a hibakeresési csatorna **Microsoft-Windows-Dsc/Debug**.</span><span class="sxs-lookup"><span data-stu-id="ed580-134">The log name for the analytic channel is **Microsoft-Windows-Dsc/Analytic**, and the debug channel is **Microsoft-Windows-Dsc/Debug**.</span></span> <span data-ttu-id="ed580-135">Is használhatja a [wevtutil](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/cc732848(v=ws.11)) segédprogram a naplók engedélyezéséhez az alábbi példában látható módon.</span><span class="sxs-lookup"><span data-stu-id="ed580-135">You could also use the [wevtutil](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/cc732848(v=ws.11)) utility to enable the logs, as shown in the following example.</span></span>

```powershell
wevtutil.exe set-log "Microsoft-Windows-Dsc/Analytic" /q:true /e:true
```

## <a name="what-do-dsc-logs-contain"></a><span data-ttu-id="ed580-136">Mi a DSC-naplók tartalmaznak?</span><span class="sxs-lookup"><span data-stu-id="ed580-136">What do DSC logs contain?</span></span>

<span data-ttu-id="ed580-137">DSC-naplók alatt a három naplózási csatornák, az üzenet fontossága alapján vannak osztva.</span><span class="sxs-lookup"><span data-stu-id="ed580-137">DSC logs are split over the three log channels based on the importance of the message.</span></span> <span data-ttu-id="ed580-138">A DSC a műveleti napló az összes hibaüzenet tartalmazza, és a probléma meghatározásához használható.</span><span class="sxs-lookup"><span data-stu-id="ed580-138">The operational log in DSC contains all error messages, and can be used to identify a problem.</span></span> <span data-ttu-id="ed580-139">Az elemzési naplóját nagyobb mennyiségű esemény rendelkezik, és azonosíthatja, ahol a hiba lépett fel.</span><span class="sxs-lookup"><span data-stu-id="ed580-139">The analytic log has a higher volume of events, and can identify where error(s) occurred.</span></span> <span data-ttu-id="ed580-140">Ez a csatorna is tartalmaz részletes üzenetek a (ha van).</span><span class="sxs-lookup"><span data-stu-id="ed580-140">This channel also contains verbose messages (if any).</span></span> <span data-ttu-id="ed580-141">A hibakeresési napló tartalmazza, amelyek segítségével jobban megértheti, hogy a hiba történt a naplók.</span><span class="sxs-lookup"><span data-stu-id="ed580-141">The debug log contains logs that can help you understand how the errors occurred.</span></span> <span data-ttu-id="ed580-142">DSC-eseményüzenetek struktúrája úgy, hogy minden eseményüzenet kezdődik, amely egyedileg jelöli egy DSC művelet Feladatazonosítót.</span><span class="sxs-lookup"><span data-stu-id="ed580-142">DSC event messages are structured such that every event message begins with a job ID that uniquely represents a DSC operation.</span></span> <span data-ttu-id="ed580-143">Az alábbi példa próbál meg az első esemény a műveleti napló DSC bejelentkezett szerezze be az üzenetet.</span><span class="sxs-lookup"><span data-stu-id="ed580-143">The example below attempts to obtain the message from the first event logged into the operational DSC log.</span></span>

```powershell
PS C:\> $AllDscOpEvents = Get-WinEvent -LogName "Microsoft-Windows-Dsc/Operational"
PS C:\> $FirstOperationalEvent = $AllDscOpEvents[0]
PS C:\> $FirstOperationalEvent.Message
Job {02C38626-D95A-47F1-9DA2-C1D44A7128E7} :
Consistency engine was run successfully.
```

<span data-ttu-id="ed580-144">DSC-események egy adott struktúra, amely lehetővé teszi a felhasználó az egyik DSC-feladat eseményeket naplózza.</span><span class="sxs-lookup"><span data-stu-id="ed580-144">DSC events are logged in a particular structure that enables the user to aggregate events from one DSC job.</span></span> <span data-ttu-id="ed580-145">A struktúra a következőképpen történik:</span><span class="sxs-lookup"><span data-stu-id="ed580-145">The structure is as follows:</span></span>

```
Job ID : <Guid>
<Event Message>
```

## <a name="gathering-events-from-a-single-dsc-operation"></a><span data-ttu-id="ed580-146">DSC egyetlen műveletben eseményeinek gyűjtése</span><span class="sxs-lookup"><span data-stu-id="ed580-146">Gathering events from a single DSC operation</span></span>

<span data-ttu-id="ed580-147">DSC-eseménynaplók DSC különféle műveletek által előállított eseményeket tartalmaz.</span><span class="sxs-lookup"><span data-stu-id="ed580-147">DSC event logs contain events generated by various DSC operations.</span></span> <span data-ttu-id="ed580-148">Azonban általában fogja fontos szempont a részletes csak egy adott műveletet.</span><span class="sxs-lookup"><span data-stu-id="ed580-148">However, you'll usually be concerned with the detail about just one particular operation.</span></span> <span data-ttu-id="ed580-149">Minden DSC-naplók csoportosíthatók a feladat azonosító tulajdonság, amely minden DSC művelet esetében egyedi legyen.</span><span class="sxs-lookup"><span data-stu-id="ed580-149">All DSC logs can be grouped by the job ID property that is unique for every DSC operation.</span></span> <span data-ttu-id="ed580-150">A feladat azonosítója első tulajdonság értékét minden DSC-esemény jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="ed580-150">The job ID is displayed as the first property value in all DSC events.</span></span> <span data-ttu-id="ed580-151">A következő lépések azt ismertetik, hogyan gyűlnek szerkezetben vannak csoportosítva tömb összes eseményt.</span><span class="sxs-lookup"><span data-stu-id="ed580-151">The following steps explain how to accumulate all events in a grouped array structure.</span></span>

```powershell
<##########################################################################
 Step 1 : Enable analytic and debug DSC channels (Operational channel is enabled by default)
###########################################################################>

wevtutil.exe set-log "Microsoft-Windows-Dsc/Analytic" /q:true /e:true
wevtutil.exe set-log "Microsoft-Windows-Dsc/Debug" /q:True /e:true

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

<span data-ttu-id="ed580-152">Itt, a változó `$SeparateDscOperations` tartalmazza a naplók a feladat-azonosítók szerint csoportosítva.</span><span class="sxs-lookup"><span data-stu-id="ed580-152">Here, the variable `$SeparateDscOperations` contains logs grouped by the job IDs.</span></span> <span data-ttu-id="ed580-153">A változó egyes tömbelemeken különböző DSC művelet, engedélyezi a hozzáférést a naplók további információ a naplózott eseményeket egy csoportját jelöli.</span><span class="sxs-lookup"><span data-stu-id="ed580-153">Each array element of this variable represents a group of events logged by a different DSC operation, allowing access to more information about the logs.</span></span>

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

<span data-ttu-id="ed580-154">Az adatok a változóban kibonthatja `$SeparateDscOperations` használatával [Where-Object](/powershell/module/microsoft.powershell.core/where-object).</span><span class="sxs-lookup"><span data-stu-id="ed580-154">You can extract the data in the variable `$SeparateDscOperations` using [Where-Object](/powershell/module/microsoft.powershell.core/where-object).</span></span> <span data-ttu-id="ed580-155">Öt forgatókönyvek, amelyben érdemes DSC hibaelhárítási adatokat nyerhet ki a következők:</span><span class="sxs-lookup"><span data-stu-id="ed580-155">Following are five scenarios in which you might want to extract data for troubleshooting DSC:</span></span>

### <a name="1-operations-failures"></a><span data-ttu-id="ed580-156">1: Sikertelen műveletek</span><span class="sxs-lookup"><span data-stu-id="ed580-156">1: Operations failures</span></span>

<span data-ttu-id="ed580-157">Az összes esemény rendelkezik [súlyossági szintek](/windows/desktop/WES/defining-severity-levels).</span><span class="sxs-lookup"><span data-stu-id="ed580-157">All events have [severity levels](/windows/desktop/WES/defining-severity-levels).</span></span> <span data-ttu-id="ed580-158">Ezek az információk segítségével azonosíthatja a hibaesemények:</span><span class="sxs-lookup"><span data-stu-id="ed580-158">This information can be used to identify the error events:</span></span>

```
PS C:\> $SeparateDscOperations | Where-Object {$_.Group.LevelDisplayName -contains "Error"}

Count Name                      Group
----- ----                      -----
   38 {5BCA8BE7-5BB6-11E3-BF... {System.Diagnostics.Eventing.Reader.EventLogRecord, System.Diagnostics....
```

### <a name="2-details-of-operations-run-in-the-last-half-hour"></a><span data-ttu-id="ed580-159">2: Az elmúlt fél órában futtassa a műveletek részletei</span><span class="sxs-lookup"><span data-stu-id="ed580-159">2: Details of operations run in the last half hour</span></span>

<span data-ttu-id="ed580-160">`TimeCreated`, minden Windows esemény-tulajdonságra állapotok a az esemény létrehozásának ideje.</span><span class="sxs-lookup"><span data-stu-id="ed580-160">`TimeCreated`, a property of every Windows event, states the time the event was created.</span></span> <span data-ttu-id="ed580-161">Ennek a tulajdonságnak egy adott dátum/idő objektum összehasonlítása az összes esemény szűrésére használható:</span><span class="sxs-lookup"><span data-stu-id="ed580-161">Comparing this property with a particular date/time object can be used to filter all events:</span></span>

```powershell
PS C:\> $DateLatest = (Get-Date).AddMinutes(-30)
PS C:\> $SeparateDscOperations | Where-Object {$_.Group.TimeCreated -gt $DateLatest}

Count Name                      Group
----- ----                      -----
    1 {6CEC5B09-5BB0-11E3-BF... {System.Diagnostics.Eventing.Reader.EventLogRecord}
```

### <a name="3-messages-from-the-latest-operation"></a><span data-ttu-id="ed580-162">3: A legutóbbi művelet üzeneteit</span><span class="sxs-lookup"><span data-stu-id="ed580-162">3: Messages from the latest operation</span></span>

<span data-ttu-id="ed580-163">A legutóbbi művelet tárolja az első index a tömb csoport `$SeparateDscOperations`.</span><span class="sxs-lookup"><span data-stu-id="ed580-163">The latest operation is stored in the first index of the array group `$SeparateDscOperations`.</span></span>
<span data-ttu-id="ed580-164">A csoport üzenetek 0. index lekérdezése a legutóbbi műveletet üzenetek adja vissza:</span><span class="sxs-lookup"><span data-stu-id="ed580-164">Querying the group's messages for index 0 returns all messages for the latest operation:</span></span>

```powershell
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

### <a name="4-error-messages-logged-for-recent-failed-operations"></a><span data-ttu-id="ed580-165">4: Legutóbbi sikertelen műveletek a naplóba hibaüzenetek</span><span class="sxs-lookup"><span data-stu-id="ed580-165">4: Error messages logged for recent failed operations</span></span>

<span data-ttu-id="ed580-166">`$SeparateDscOperations[0].Group` a legutóbbi művelet események egy meghatározott készletének tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="ed580-166">`$SeparateDscOperations[0].Group` contains a set of events for the latest operation.</span></span> <span data-ttu-id="ed580-167">Futtassa a `Where-Object` parancsmag, amellyel az események szűréséhez állítsa szintű megjelenített név alapján.</span><span class="sxs-lookup"><span data-stu-id="ed580-167">Run the `Where-Object` cmdlet to filter the events based on their level display name.</span></span> <span data-ttu-id="ed580-168">Az eredmények tárolása az `$myFailedEvent` változó, amely lehet további minél az eseményüzenet beolvasásához:</span><span class="sxs-lookup"><span data-stu-id="ed580-168">Results are stored in the `$myFailedEvent` variable, which can be further dissected to get the event message:</span></span>

```powershell
PS C:\> $myFailedEvent = ($SeparateDscOperations[0].Group | Where-Object {$_.LevelDisplayName -eq "Error"})

PS C:\> $myFailedEvent.Message

Job {5BCA8BE7-5BB6-11E3-BF41-00155D553612} :
DSC Engine Error :
 Error Message Current configuration does not exist. Execute Start-DscConfiguration command with -Path pa
rameter to specify a configuration file and create a current configuration first.
Error Code : 1
```

### <a name="5-all-events-generated-for-a-particular-job-id"></a><span data-ttu-id="ed580-169">5: Összes esemény jön létre egy adott feladat azonosítóját.</span><span class="sxs-lookup"><span data-stu-id="ed580-169">5: All events generated for a particular job ID.</span></span>

<span data-ttu-id="ed580-170">`$SeparateDscOperations` egy tömb, csoportok, amelyek mindegyike rendelkezik-e a neve megegyezik a feladat egyedi azonosítója.</span><span class="sxs-lookup"><span data-stu-id="ed580-170">`$SeparateDscOperations` is an array of groups, each of which has the name as the unique job ID.</span></span> <span data-ttu-id="ed580-171">Futtassa a `Where-Object` parancsmagot, kibonthatja a ezeket a csoportokat az eseményeket, amelyek egy adott feladat azonosítója:</span><span class="sxs-lookup"><span data-stu-id="ed580-171">By running the `Where-Object` cmdlet, you can extract those groups of events that have a particular job ID:</span></span>

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

## <a name="using-xdscdiagnostics-to-analyze-dsc-logs"></a><span data-ttu-id="ed580-172">Naplók elemzéséhez a DSC xDscDiagnostics segítségével</span><span class="sxs-lookup"><span data-stu-id="ed580-172">Using xDscDiagnostics to analyze DSC logs</span></span>

<span data-ttu-id="ed580-173">**xDscDiagnostics** egy PowerShell-modul, amely számos funkciót, amely segíthet a gépen a DSC hibák elemzése áll.</span><span class="sxs-lookup"><span data-stu-id="ed580-173">**xDscDiagnostics** is a PowerShell module that consists of several functions that can help analyze DSC failures on your machine.</span></span> <span data-ttu-id="ed580-174">Ezek a függvények is segít azonosítani az elmúlt DSC műveletek összes helyi esemény vagy a távoli számítógépeken lévő DSC események (érvénytelen hitelesítő adatok).</span><span class="sxs-lookup"><span data-stu-id="ed580-174">These functions can help you identify all local events from past DSC operations, or DSC events on remote computers (with valid credentials).</span></span> <span data-ttu-id="ed580-175">Az előfizetési időszak DSC művelet itt, az egy egyetlen egyedi DSC végrehajtása a kezdetektől a teljes körű meghatározására szolgál.</span><span class="sxs-lookup"><span data-stu-id="ed580-175">Here, the term DSC operation is used to define a single unique DSC execution from its start to its end.</span></span> <span data-ttu-id="ed580-176">Ha például `Test-DscConfiguration` lenne egy külön DSC művelet.</span><span class="sxs-lookup"><span data-stu-id="ed580-176">For example, `Test-DscConfiguration` would be a separate DSC operation.</span></span> <span data-ttu-id="ed580-177">Ehhez hasonlóan más parancsmagjáról DSC (például `Get-DscConfiguration`, `Start-DscConfiguration`használatához és így tovább) minden azonosítható külön DSC műveletként.</span><span class="sxs-lookup"><span data-stu-id="ed580-177">Similarly, every other cmdlet in DSC (such as `Get-DscConfiguration`, `Start-DscConfiguration`, etc.) could each be identified as separate DSC operations.</span></span> <span data-ttu-id="ed580-178">A függvények vannak írva [xDscDiagnostics](https://github.com/PowerShell/xDscDiagnostics).</span><span class="sxs-lookup"><span data-stu-id="ed580-178">The functions are explained at [xDscDiagnostics](https://github.com/PowerShell/xDscDiagnostics).</span></span> <span data-ttu-id="ed580-179">Súgó áll rendelkezésre a futó `Get-Help <cmdlet name>`.</span><span class="sxs-lookup"><span data-stu-id="ed580-179">Help is available by running `Get-Help <cmdlet name>`.</span></span>

### <a name="getting-details-of-dsc-operations"></a><span data-ttu-id="ed580-180">DSC-műveletek részleteinek beolvasása közben</span><span class="sxs-lookup"><span data-stu-id="ed580-180">Getting details of DSC operations</span></span>

<span data-ttu-id="ed580-181">A `Get-xDscOperation` funkció lehetővé teszi a keresse meg az eredményeket a DSC-műveletek, amelyek egy vagy több számítógépen futnak, és adja vissza minden egyes DSC művelet által létrehozott olyan objektum, amely az események gyűjteményét tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="ed580-181">The `Get-xDscOperation` function lets you find the results of the DSC operations that run on one or multiple computers, and returns an object that contains the collection of events produced by each DSC operation.</span></span> <span data-ttu-id="ed580-182">Például az alábbi kimenet három parancs futtatná.</span><span class="sxs-lookup"><span data-stu-id="ed580-182">For example, in the following output, three commands were run.</span></span> <span data-ttu-id="ed580-183">Az elsőt átadva, és a másik két nem sikerült.</span><span class="sxs-lookup"><span data-stu-id="ed580-183">The first one passed, and the other two failed.</span></span> <span data-ttu-id="ed580-184">Ezekkel az eredményekkel foglalja össze a kimenetét `Get-xDscOperation`.</span><span class="sxs-lookup"><span data-stu-id="ed580-184">These results are summarized in the output of `Get-xDscOperation`.</span></span>

```powershell
PS C:\DiagnosticsTest> Get-xDscOperation

ComputerName   SequenceId TimeCreated           Result   JobID                                 AllEvents
------------   ---------- -----------           ------   -----                                 ---------
SRV1   1          6/23/2016 9:37:52 AM  Failure  9701aadf-395e-11e6-9165-00155d390509  {@{Message=; TimeC...
SRV1   2          6/23/2016 9:36:54 AM  Failure  7e8e2d6e-395c-11e6-9165-00155d390509  {@{Message=; TimeC...
SRV1   3          6/23/2016 9:36:54 AM  Success  af72c6aa-3960-11e6-9165-00155d390509  {@{Message=Operati...
```

<span data-ttu-id="ed580-185">Azt is beállíthatja, hogy eredményeket össze szeretné csak a legutóbbi műveletek használatával a `Newest` paramétert:</span><span class="sxs-lookup"><span data-stu-id="ed580-185">You can also specify that you want only results for the most recent operations by using the `Newest` parameter:</span></span>

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

### <a name="getting-details-of-dsc-events"></a><span data-ttu-id="ed580-186">DSC-esemény részleteinek beolvasása közben</span><span class="sxs-lookup"><span data-stu-id="ed580-186">Getting details of DSC events</span></span>

<span data-ttu-id="ed580-187">A `Trace-xDscOperation` parancsmag események, az esemény típusok gyűjteményét tartalmazó objektumot ad vissza, és az üzenet kimeneti egy adott DSC műveletből létrehozott.</span><span class="sxs-lookup"><span data-stu-id="ed580-187">The `Trace-xDscOperation` cmdlet returns an object containing a collection of events, their event types, and the message output generated from a particular DSC operation.</span></span> <span data-ttu-id="ed580-188">Általában amikor talált hiba segítségével műveletek `Get-xDscOperation`, meg kellene nyomon követése a működést, és ismerje meg, amely az események hibáját okozta.</span><span class="sxs-lookup"><span data-stu-id="ed580-188">Typically, when you find a failure in any of the operations using `Get-xDscOperation`, you would trace that operation to find out which of the events caused a failure.</span></span>

<span data-ttu-id="ed580-189">Használja a `SequenceID` paramétert az események beolvasása egy adott számítógép egy adott művelethez.</span><span class="sxs-lookup"><span data-stu-id="ed580-189">Use the `SequenceID` parameter to get the events for a specific operation for a specific computer.</span></span>
<span data-ttu-id="ed580-190">Például, ha megad egy `SequenceID` , 9, `Trace-xDscOperaion` a DSC-műveletet, amely az utolsó művelet 9 volt a nyomkövetési adatok lekérése:</span><span class="sxs-lookup"><span data-stu-id="ed580-190">For example, if you specify a `SequenceID` of 9, `Trace-xDscOperaion` get the trace for the DSC operation that was 9th from the last operation:</span></span>

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

<span data-ttu-id="ed580-191">Adja át a **GUID** egy adott DSC művelethez hozzárendelt (által visszaadott a `Get-xDscOperation` parancsmaggal), az esemény részleteinek beolvasása a DSC-művelethez:</span><span class="sxs-lookup"><span data-stu-id="ed580-191">Pass the **GUID** assigned to a specific DSC operation (as returned by the `Get-xDscOperation` cmdlet) to get the event details for that DSC operation:</span></span>

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

<span data-ttu-id="ed580-192">Vegye figyelembe, hogy, mivel `Trace-xDscOperation` események összesíti az elemzési, a Debug és műveleti naplók, akkor arra fogja kérni, hogy ezek a naplók engedélyezése a fent leírtak szerint.</span><span class="sxs-lookup"><span data-stu-id="ed580-192">Note that, since `Trace-xDscOperation` aggregates events from the Analytic, Debug, and Operational logs, it will prompt you to enable these logs as described above.</span></span>

<span data-ttu-id="ed580-193">Azt is megteheti, adatokat gyűjthet az események kimenete mentésével `Trace-xDscOperation` egy változóba.</span><span class="sxs-lookup"><span data-stu-id="ed580-193">Alternately, you can gather information on the events by saving the output of `Trace-xDscOperation` into a variable.</span></span> <span data-ttu-id="ed580-194">A következő parancsokat használhatja egy DSC művelethez tartozó összes esemény megjelenítéséhez.</span><span class="sxs-lookup"><span data-stu-id="ed580-194">You can use the following commands to display all the events for a particular DSC operation.</span></span>

```powershell
PS C:\DiagnosticsTest> $Trace = Trace-xDscOperation -SequenceID 4

PS C:\DiagnosticsTest> $Trace.Event
```

<span data-ttu-id="ed580-195">Ez ugyanazokat az eredményeket, megjeleníti a `Get-WinEvent` parancsmagot, például az alábbi kimenetben:</span><span class="sxs-lookup"><span data-stu-id="ed580-195">This will display the same results as the `Get-WinEvent` cmdlet, such as in the output below:</span></span>

```output
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

<span data-ttu-id="ed580-196">Ideális esetben először használja `Get-xDscOperation` sorolja az elmúlt néhány DSC konfigurációs futtatja a gépeken.</span><span class="sxs-lookup"><span data-stu-id="ed580-196">Ideally, you would first use `Get-xDscOperation` to list out the last few DSC configuration runs on your machines.</span></span> <span data-ttu-id="ed580-197">Ezt követően tekintse meg minden olyan (a saját SequenceID vagy JobID) egyetlen művelettel rendelkező `Trace-xDscOperation` felderítheti, milyen zavartalanul a háttérben.</span><span class="sxs-lookup"><span data-stu-id="ed580-197">Following this, you can examine any single operation (using its SequenceID or JobID) with `Trace-xDscOperation` to discover what it did behind the scenes.</span></span>

### <a name="getting-events-for-a-remote-computer"></a><span data-ttu-id="ed580-198">Események beolvasása egy távoli számítógépen</span><span class="sxs-lookup"><span data-stu-id="ed580-198">Getting events for a remote computer</span></span>

<span data-ttu-id="ed580-199">Használja a `ComputerName` paraméterében a `Trace-xDscOperation` -parancsmaggal beolvasható az esemény részleteinek a távoli számítógépen.</span><span class="sxs-lookup"><span data-stu-id="ed580-199">Use the `ComputerName` parameter of the `Trace-xDscOperation` cmdlet to get the event details on a remote computer.</span></span> <span data-ttu-id="ed580-200">Előtt ezt megteheti, hogy hozzon létre egy tűzfalszabályt a távfelügyelet engedélyezéséhez a távoli számítógépen:</span><span class="sxs-lookup"><span data-stu-id="ed580-200">Before you can do this, you have to create a firewall rule to allow remote administration on the remote computer:</span></span>

```powershell
New-NetFirewallRule -Name "Service RemoteAdmin" -DisplayName "Remote" -Action Allow
```

<span data-ttu-id="ed580-201">Most már megadhatja, hogy a számítógép a hívása `Trace-xDscOperation`:</span><span class="sxs-lookup"><span data-stu-id="ed580-201">Now you can specify that computer in your call to `Trace-xDscOperation`:</span></span>

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

## <a name="my-resources-wont-update-how-to-reset-the-cache"></a><span data-ttu-id="ed580-202">Az erőforrások nem frissítése: A gyorsítótárának visszaállítása</span><span class="sxs-lookup"><span data-stu-id="ed580-202">My resources won't update: How to reset the cache</span></span>

<span data-ttu-id="ed580-203">A DSC motor megvalósítva, egy PowerShell-modul hatékonyság célokra erőforrások gyorsítótárazza.</span><span class="sxs-lookup"><span data-stu-id="ed580-203">The DSC engine caches resources implemented as a PowerShell module for efficiency purposes.</span></span>
<span data-ttu-id="ed580-204">Azonban ez problémákat okozhat szerzői erőforrás és egyidejű tesztelése, mert DSC betölti a gyorsítótárazott verziót, amíg a folyamat újraindítása során.</span><span class="sxs-lookup"><span data-stu-id="ed580-204">However, this can cause problems when you are authoring a resource and testing it simultaneously because DSC will load the cached version until the process is restarted.</span></span> <span data-ttu-id="ed580-205">Győződjön meg arról, az újabb verzió betöltése DSC csak úgy, hogy explicit módon kill a DSC motor tartalmazó folyamat.</span><span class="sxs-lookup"><span data-stu-id="ed580-205">The only way to make DSC load the newer version is to explicitly kill the process hosting the DSC engine.</span></span>

<span data-ttu-id="ed580-206">Hasonlóképpen, ha futtatja `Start-DscConfiguration`, hozzáadásával és a egy egyéni erőforrás módosítása után a módosítás nem futhat, kivéve, ha vagy, amíg a számítógép újraindul.</span><span class="sxs-lookup"><span data-stu-id="ed580-206">Similarly, when you run `Start-DscConfiguration`, after adding and modifying a custom resource, the modification may not execute unless, or until, the computer is rebooted.</span></span> <span data-ttu-id="ed580-207">Ennek az az oka a DSC fut a WMI szolgáltató Gazdagépének folyamatánál (WmiPrvSE), és általában nincsenek WmiPrvSE fut egyszerre több példányát.</span><span class="sxs-lookup"><span data-stu-id="ed580-207">This is because DSC runs in the WMI Provider Host Process (WmiPrvSE), and usually, there are many instances of WmiPrvSE running at once.</span></span> <span data-ttu-id="ed580-208">Újraindítás, amikor a gazdagép-folyamat újraindítása, és a gyorsítótár nem lett kitörölve.</span><span class="sxs-lookup"><span data-stu-id="ed580-208">When you reboot, the host process is restarted and the cache is cleared.</span></span>

<span data-ttu-id="ed580-209">Sikeres újrahasznosítása a konfigurációt, és a gyorsítótár ürítése újraindítás nélkül, állítsa le és indítsa újra a gazdagép-folyamat.</span><span class="sxs-lookup"><span data-stu-id="ed580-209">To successfully recycle the configuration and clear the cache without rebooting, you must stop and then restart the host process.</span></span> <span data-ttu-id="ed580-210">Ez a példány történik, amelyek segítségével azonosíthatja a folyamat, állítsa le és indítsa újra a elvégezhető.</span><span class="sxs-lookup"><span data-stu-id="ed580-210">This can be done on a per instance basis, whereby you identify the process, stop it, and restart it.</span></span> <span data-ttu-id="ed580-211">Vagy használhat `DebugMode`, ahogyan az alábbi betölti a PowerShell DSC-erőforrás is.</span><span class="sxs-lookup"><span data-stu-id="ed580-211">Or, you can use `DebugMode`, as demonstrated below, to reload the PowerShell DSC resource.</span></span>

<span data-ttu-id="ed580-212">Azonosíthatja a folyamatok a DSC motor üzemelteti, és állítsa le a példány, listázhatja a WmiPrvSE, amely a DSC motor Folyamatazonosítója.</span><span class="sxs-lookup"><span data-stu-id="ed580-212">To identify which process is hosting the DSC engine and stop it on a per instance basis, you can list the process ID of the WmiPrvSE which is hosting the DSC engine.</span></span> <span data-ttu-id="ed580-213">Ezután frissítse a szolgáltatót, állítsa le a WmiPrvSE folyamatot az alábbi parancsok használatával, és futtassa **Start-DscConfiguration** újra.</span><span class="sxs-lookup"><span data-stu-id="ed580-213">Then, to update the provider, stop the WmiPrvSE process using the commands below, and then run **Start-DscConfiguration** again.</span></span>

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

## <a name="using-debugmode"></a><span data-ttu-id="ed580-214">DebugMode használatával</span><span class="sxs-lookup"><span data-stu-id="ed580-214">Using DebugMode</span></span>

<span data-ttu-id="ed580-215">A DSC helyi Configuration Manager (LCM) Konfigurálása használatára konfigurálhatja `DebugMode` mindig törölje a gyorsítótárban, a gazdagép-folyamat újraindításakor.</span><span class="sxs-lookup"><span data-stu-id="ed580-215">You can configure the DSC Local Configuration Manager (LCM) to use `DebugMode` to always clear the cache when the host process is restarted.</span></span> <span data-ttu-id="ed580-216">Ha a beállítása **igaz**, azt eredményezi, hogy a motor, mindig töltse be újra a PowerShell DSC-erőforrás.</span><span class="sxs-lookup"><span data-stu-id="ed580-216">When set to **TRUE**, it causes the engine to always reload the PowerShell DSC resource.</span></span> <span data-ttu-id="ed580-217">Ha elkészült a-erőforrás írása állíthatja be, vissza **false (hamis)** és a motor visszaállítja a modulok gyorsítótárazásának működését.</span><span class="sxs-lookup"><span data-stu-id="ed580-217">Once you are done writing your resource, you can set it back to **FALSE** and the engine will revert to its behavior of caching the modules.</span></span>

<span data-ttu-id="ed580-218">Az alábbiakban a megjeleníthető bemutatója hogyan `DebugMode` automatikusan frissítheti a gyorsítótárban.</span><span class="sxs-lookup"><span data-stu-id="ed580-218">Following is a demonstration to show how `DebugMode` can automatically refresh the cache.</span></span> <span data-ttu-id="ed580-219">Először is lássuk az alapértelmezett konfiguráció:</span><span class="sxs-lookup"><span data-stu-id="ed580-219">First, let's look at the default configuration:</span></span>

```powershell
PS C:\> Get-DscLocalConfigurationManager
```

```output
AllowModuleOverwrite           : False
CertificateID                  :
ConfigurationID                :
ConfigurationMode              : ApplyAndMonitor
ConfigurationModeFrequencyMins : 30
Credential                     :
DebugMode                      : {None}
DownloadManagerCustomData      :
DownloadManagerName            :
LocalConfigurationManagerState : Ready
RebootNodeIfNeeded             : False
RefreshFrequencyMins           : 15
RefreshMode                    : PUSH
PSComputerName                 :
```

<span data-ttu-id="ed580-220">Láthatja, hogy `DebugMode` értékre van állítva **"None"**.</span><span class="sxs-lookup"><span data-stu-id="ed580-220">You can see that `DebugMode` is set to **"None"**.</span></span>

<span data-ttu-id="ed580-221">Beállítása a `DebugMode` bemutató a következő PowerShell-erőforrásból:</span><span class="sxs-lookup"><span data-stu-id="ed580-221">To set up the `DebugMode` demonstration, use the following PowerShell resource:</span></span>

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

<span data-ttu-id="ed580-222">Most hozhat létre egy konfigurációt a fenti erőforrás nevű `TestProviderDebugMode`:</span><span class="sxs-lookup"><span data-stu-id="ed580-222">Now, author a configuration using the above resource called `TestProviderDebugMode`:</span></span>

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

<span data-ttu-id="ed580-223">Látni fogja, hogy a fájl tartalmát: `$env:SystemDrive\OutputFromTestProviderDebugMode.txt` van **1**.</span><span class="sxs-lookup"><span data-stu-id="ed580-223">You will see that the contents of file: `$env:SystemDrive\OutputFromTestProviderDebugMode.txt` is **1**.</span></span>

<span data-ttu-id="ed580-224">Most frissítse a szolgáltatót kódot az alábbi parancsfájl használatával:</span><span class="sxs-lookup"><span data-stu-id="ed580-224">Now, update the provider code using the following script:</span></span>

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

<span data-ttu-id="ed580-225">Ez a szkript létrehoz egy véletlenszerű számot, és ennek megfelelően frissíti a szolgáltató kódot.</span><span class="sxs-lookup"><span data-stu-id="ed580-225">This script generates a random number and updates the provider code accordingly.</span></span> <span data-ttu-id="ed580-226">A `DebugMode` hamis, a fájl tartalmát "**$env:SystemDrive\OutputFromTestProviderDebugMode.txt**" soha nem módosulnak.</span><span class="sxs-lookup"><span data-stu-id="ed580-226">With `DebugMode` set to false, the contents of the file "**$env:SystemDrive\OutputFromTestProviderDebugMode.txt**" are never changed.</span></span>

<span data-ttu-id="ed580-227">Most, `DebugMode` való **"ForceModuleImport"** konfigurációs parancsfájlban:</span><span class="sxs-lookup"><span data-stu-id="ed580-227">Now, set `DebugMode` to **"ForceModuleImport"** in your configuration script:</span></span>

```powershell
LocalConfigurationManager
{
    DebugMode = "ForceModuleImport"
}
```

<span data-ttu-id="ed580-228">Ha újra futtatja a fenti szkript, látni fogja, hogy a fájl tartalma eltér minden alkalommal.</span><span class="sxs-lookup"><span data-stu-id="ed580-228">When you run the above script again, you will see that the content of the file is different every time.</span></span> <span data-ttu-id="ed580-229">(Futtathatja `Get-DscConfiguration` , hogy).</span><span class="sxs-lookup"><span data-stu-id="ed580-229">(You can run `Get-DscConfiguration` to check it).</span></span> <span data-ttu-id="ed580-230">Az alábbi, két további futtatásoknál (a találatok eltérő lehet a parancsfájl futtatásakor) eredménye:</span><span class="sxs-lookup"><span data-stu-id="ed580-230">Below is the result of two additional runs (your results may be different when you run the script):</span></span>

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

## <a name="see-also"></a><span data-ttu-id="ed580-231">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="ed580-231">See Also</span></span>

### <a name="concepts"></a><span data-ttu-id="ed580-232">Fogalmak</span><span class="sxs-lookup"><span data-stu-id="ed580-232">Concepts</span></span>

- [<span data-ttu-id="ed580-233">Egyéni Windows PowerShell Desired State Configuration erőforrások létrehozása</span><span class="sxs-lookup"><span data-stu-id="ed580-233">Build Custom Windows PowerShell Desired State Configuration Resources</span></span>](../resources/authoringResource.md)

### <a name="other-resources"></a><span data-ttu-id="ed580-234">Egyéb források</span><span class="sxs-lookup"><span data-stu-id="ed580-234">Other Resources</span></span>

- [<span data-ttu-id="ed580-235">Windows PowerShell Desired State Configuration parancsmagok</span><span class="sxs-lookup"><span data-stu-id="ed580-235">Windows PowerShell Desired State Configuration Cmdlets</span></span>](/powershell/module/psdesiredstateconfiguration/)
