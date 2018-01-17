---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "Hibakeresési DSC-erőforrások"
ms.openlocfilehash: 35eb990705bab8190172df899c64c9f34452aa4b
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 01/17/2018
---
# <a name="debugging-dsc-resources"></a><span data-ttu-id="4c8bd-103">Hibakeresési DSC-erőforrások</span><span class="sxs-lookup"><span data-stu-id="4c8bd-103">Debugging DSC resources</span></span>

> <span data-ttu-id="4c8bd-104">Vonatkozik: A Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="4c8bd-104">Applies To: Windows PowerShell 5.0</span></span>

<span data-ttu-id="4c8bd-105">A PowerShell 5.0-s egy új szolgáltatás a szükséges állapot szabásra szolgáló elemeit (DSC), amely lehetővé teszi a DSC-erőforrás hibakeresési módon végzi a configuration jelent meg.</span><span class="sxs-lookup"><span data-stu-id="4c8bd-105">In PowerShell 5.0, a new feature was introduced in Desired State Configuraiton (DSC) that allows you to debug a DSC resource as a configuration is being applied.</span></span>

## <a name="enabling-dsc-debugging"></a><span data-ttu-id="4c8bd-106">A DSC-hibakeresés engedélyezése</span><span class="sxs-lookup"><span data-stu-id="4c8bd-106">Enabling DSC debugging</span></span>
<span data-ttu-id="4c8bd-107">Mielőtt egy erőforrás megoldhassuk, fel kell meghívásával hibakeresés engedélyezése a [Enable-DscDebug](https://technet.microsoft.com/en-us/library/mt517870.aspx) parancsmag.</span><span class="sxs-lookup"><span data-stu-id="4c8bd-107">Before you can debug a resource, you have to enable debugging by calling the [Enable-DscDebug](https://technet.microsoft.com/en-us/library/mt517870.aspx) cmdlet.</span></span> <span data-ttu-id="4c8bd-108">Ez a parancsmag egy kötelező paramétert fogad, **BreakAll**.</span><span class="sxs-lookup"><span data-stu-id="4c8bd-108">This cmdlet takes a mandatory parameter, **BreakAll**.</span></span> 

<span data-ttu-id="4c8bd-109">Ellenőrizheti, hogy hibakeresés engedélyezve van a hívás eredménye alapján [Get-DscLocalConfigurationManager](https://technet.microsoft.com/en-us/library/dn407378.aspx).</span><span class="sxs-lookup"><span data-stu-id="4c8bd-109">You can verify that debugging has been enabled by looking at the result of a call to [Get-DscLocalConfigurationManager](https://technet.microsoft.com/en-us/library/dn407378.aspx).</span></span>

<span data-ttu-id="4c8bd-110">A következő PowerShell-kimenet hibakeresés engedélyezése eredményének megjelenítése:</span><span class="sxs-lookup"><span data-stu-id="4c8bd-110">The following PowerShell output shows the result of enabling debugging:</span></span>


```powershell
PS C:\DebugTest> $LCM = Get-DscLocalConfigurationManager

PS C:\DebugTest> $LCM.DebugMode
NONE

PS C:\DebugTest> Enable-DscDebug -BreakAll

PS C:\DebugTest> $LCM = Get-DscLocalConfigurationManager

PS C:\DebugTest> $LCM.DebugMode
ForceModuleImport
ResourceScriptBreakAll

PS C:\DebugTest>
```


## <a name="starting-a-configuration-with-debug-enabled"></a><span data-ttu-id="4c8bd-111">Egy konfigurációs kezdve hibakeresési engedélyezve</span><span class="sxs-lookup"><span data-stu-id="4c8bd-111">Starting a configuration with debug enabled</span></span>
<span data-ttu-id="4c8bd-112">A DSC-erőforrás hibakeresési, olyan konfigurációt, amely meghívja az adott erőforrás indítsa el.</span><span class="sxs-lookup"><span data-stu-id="4c8bd-112">To debug a DSC resource, you start a configuration that calls that resource.</span></span> <span data-ttu-id="4c8bd-113">Ehhez a példához megnézzük, egy egyszerű konfiguráció, amely behívja a [WindowsFeature](windowsfeatureResource.md) erőforrást, győződjön meg arról, hogy telepítve van-e a "WindowsPowerShellWebAccess" funkció:</span><span class="sxs-lookup"><span data-stu-id="4c8bd-113">For this example, we'll look at a simple configuration that calls the [WindowsFeature](windowsfeatureResource.md) resource to ensure that the "WindowsPowerShellWebAccess" feature is installed:</span></span>

```powershell
Configuration PSWebAccess
    {
    Import-DscResource -ModuleName 'PsDesiredStateConfiguration'
    Node localhost
        {
        WindowsFeature PSWA
            {
            Name = 'WindowsPowerShellWebAccess'
            Ensure = 'Present'
            }
        }
    }
PSWebAccess
```
<span data-ttu-id="4c8bd-114">A konfiguráció fordítása, után indítsa el azt meghívásával [Start-DscConfiguration](https://technet.microsoft.com/en-us/library/dn521623.aspx).</span><span class="sxs-lookup"><span data-stu-id="4c8bd-114">After compiling the configuration, start it by calling [Start-DscConfiguration](https://technet.microsoft.com/en-us/library/dn521623.aspx).</span></span> <span data-ttu-id="4c8bd-115">A konfigurációs leáll, amikor az első erőforrásra a konfigurációban az meghívja a helyi Configuration Manager (LCM).</span><span class="sxs-lookup"><span data-stu-id="4c8bd-115">The configuration will stop when the Local Configuration Manager (LCM) calls into the first resource in the configuration.</span></span> <span data-ttu-id="4c8bd-116">Ha használja a `-Verbose` és `-Wait` paraméterek, a kimeneti sorait jeleníti meg, meg kell adnia a hibakeresés.</span><span class="sxs-lookup"><span data-stu-id="4c8bd-116">If you use the `-Verbose` and `-Wait` parameters, the output displays the lines you need to enter to start debugging.</span></span>

```powershell
Start-DscConfiguration .\PSWebAccess -Wait -Verbose
VERBOSE: Perform operation 'Invoke CimMethod' with following parameters, ''methodName' = SendConfigurationApply,'className' = MSFT_DSCLocalConfiguration
Manager,'namespaceName' = root/Microsoft/Windows/DesiredStateConfiguration'.
VERBOSE: An LCM method call arrived from computer TEST-SRV with user sid S-1-5-21-2127521184-1604012920-1887927527-108583.
VERBOSE: An LCM method call arrived from computer TEST-SRV with user sid S-1-5-21-2127521184-1604012920-1887927527-108583.
VERBOSE: [TEST-SRV]: LCM:  [ Start  Set      ]
WARNING: [TEST-SRV]:                            [DSCEngine] Warning LCM is in Debug 'ResourceScriptBreakAll' mode.  Resource script processing will 
be stopped to wait for PowerShell script debugger to attach.
VERBOSE: [TEST-SRV]:                            [DSCEngine] Importing the module C:\WINDOWS\system32\WindowsPowerShell\v1.0\Modules\PSDesiredStateCo
nfiguration\DscResources\MSFT_RoleResource\MSFT_RoleResource.psm1 in force mode.
VERBOSE: [TEST-SRV]: LCM:  [ Start  Resource ]  [[WindowsFeature]PSWA]
VERBOSE: [TEST-SRV]: LCM:  [ Start  Test     ]  [[WindowsFeature]PSWA]
VERBOSE: [TEST-SRV]:                            [[WindowsFeature]PSWA] Importing the module MSFT_RoleResource in force mode.
WARNING: [TEST-SRV]:                            [[WindowsFeature]PSWA] Resource is waiting for PowerShell script debugger to attach. 
Use the following commands to begin debugging this resource script:
Enter-PSSession -ComputerName TEST-SRV -Credential <credentials>
Enter-PSHostProcess -Id 9000 -AppDomainName DscPsPluginWkr_AppDomain
Debug-Runspace -Id 9
```
<span data-ttu-id="4c8bd-117">Ezen a ponton a LCM az erőforrás neve, és az első töréspontot tudomást.</span><span class="sxs-lookup"><span data-stu-id="4c8bd-117">At this point, the LCM has called the resource, and come to the first break point.</span></span> <span data-ttu-id="4c8bd-118">Az utolsó három sort a kimenetben bemutatják a folyamat csatolja, és indítsa el az erőforrást parancsprogram-hibakeresés.</span><span class="sxs-lookup"><span data-stu-id="4c8bd-118">The last three lines in the output show you how to attach to the process and start debugging the resource script.</span></span>

## <a name="debugging-the-resource-script"></a><span data-ttu-id="4c8bd-119">Az erőforrást parancsprogram-hibakeresés</span><span class="sxs-lookup"><span data-stu-id="4c8bd-119">Debugging the resource script</span></span>

<span data-ttu-id="4c8bd-120">Indítsa el a PowerShell ISE egy új példányát.</span><span class="sxs-lookup"><span data-stu-id="4c8bd-120">Start a new instance of the PowerShell ISE.</span></span> <span data-ttu-id="4c8bd-121">A konzol ablaktáblájában adja meg az utolsó három sort kimenetét a `Start-DscConfiguration` parancsok, cseréje kimeneti `<credentials>` érvényes felhasználói hitelesítő adatokat.</span><span class="sxs-lookup"><span data-stu-id="4c8bd-121">In the console pane, enter the last three lines of output from the `Start-DscConfiguration` output as commands, replacing `<credentials>` with valid user credentials.</span></span> <span data-ttu-id="4c8bd-122">Ekkor megjelenik egy értesítés, a következőhöz hasonló:</span><span class="sxs-lookup"><span data-stu-id="4c8bd-122">You should now see a prompt that looks similar to:</span></span>

```powershell
[TEST-SRV]: [DBG]: [Process:9000]: [RemoteHost]: PS C:\DebugTest>>
```

<span data-ttu-id="4c8bd-123">Az erőforrást parancsprogram nyílik meg a parancssori panelbe, és a hibakereső le van állítva, az első sor a **teszt-TargetResource** függvény (a **Test()** metódus osztály-alapú erőforrás).</span><span class="sxs-lookup"><span data-stu-id="4c8bd-123">The resource script will open in the script pane, and the debugger is stopped at the first line of the **Test-TargetResource** function (the **Test()** method of a class-based resource).</span></span>
<span data-ttu-id="4c8bd-124">Most már használhat a hibakeresési parancsok a ISE teljesítéséhez a erőforrást parancsprogram, változók értékeinek meg, a hívási verem megtekintése, és így tovább.</span><span class="sxs-lookup"><span data-stu-id="4c8bd-124">Now you can use the debug commands in the ISE to step through the resource script, look at variable values, view the call stack, and so on.</span></span> <span data-ttu-id="4c8bd-125">További információ a PowerShell ISE-hibakeresés: [parancsfájlok hibakeresése a Windows PowerShell ISE hogyan](https://technet.microsoft.com/en-us/library/dd819480.aspx).</span><span class="sxs-lookup"><span data-stu-id="4c8bd-125">For information about debugging in the PowerShell ISE, see [How to Debug Scripts in Windows PowerShell ISE](https://technet.microsoft.com/en-us/library/dd819480.aspx).</span></span> <span data-ttu-id="4c8bd-126">Ne feledje, hogy a erőforrást parancsprogram (vagy a osztály) minden sor egy töréspontot értéke.</span><span class="sxs-lookup"><span data-stu-id="4c8bd-126">Remember that every line in the resource script (or class) is set as a break point.</span></span>

## <a name="disabling-dsc-debugging"></a><span data-ttu-id="4c8bd-127">A DSC-hibakeresés letiltása</span><span class="sxs-lookup"><span data-stu-id="4c8bd-127">Disabling DSC debugging</span></span>

<span data-ttu-id="4c8bd-128">Hívása után [Enable-DscDebug](https://technet.microsoft.com/en-us/library/mt517870.aspx), minden hívások [Start-DscConfiguration](https://technet.microsoft.com/en-us/library/dn521623.aspx) belépjen a hibakeresőbe megtörje a konfigurációt eredményez.</span><span class="sxs-lookup"><span data-stu-id="4c8bd-128">After calling [Enable-DscDebug](https://technet.microsoft.com/en-us/library/mt517870.aspx), all calls to [Start-DscConfiguration](https://technet.microsoft.com/en-us/library/dn521623.aspx) will result in the configuration breaking into the debugger.</span></span> <span data-ttu-id="4c8bd-129">Ahhoz, hogy konfigurálható, hogy a normál módon futnak, le kell tiltania meghívásával hibakeresés a [Disable-DscDebug](https://technet.microsoft.com/en-us/library/mt517872.aspx) parancsmag.</span><span class="sxs-lookup"><span data-stu-id="4c8bd-129">To allow configurations to run normally, you must disable debugging by calling the [Disable-DscDebug](https://technet.microsoft.com/en-us/library/mt517872.aspx) cmdlet.</span></span>

><span data-ttu-id="4c8bd-130">**Megjegyzés:** Rebooting nem változik a LCM hibakeresési állapotát.</span><span class="sxs-lookup"><span data-stu-id="4c8bd-130">**Note:** Rebooting does not change the debug state of the LCM.</span></span> <span data-ttu-id="4c8bd-131">Hibakeresés engedélyezve van, ha egy konfigurációs indítása fog továbbra is megszakítással belépjen a hibakeresőbe a rendszer újraindítása után.</span><span class="sxs-lookup"><span data-stu-id="4c8bd-131">If debugging is enabled, starting a configuration will still break into the debugger after a reboot.</span></span>


## <a name="see-also"></a><span data-ttu-id="4c8bd-132">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="4c8bd-132">See Also</span></span>
- [<span data-ttu-id="4c8bd-133">Egyéni DSC-erőforrás MOF írása</span><span class="sxs-lookup"><span data-stu-id="4c8bd-133">Writing a custom DSC resource with MOF</span></span>](authoringResourceMOF.md) 
- [<span data-ttu-id="4c8bd-134">A PowerShell osztályok egyéni DSC-erőforrás írása</span><span class="sxs-lookup"><span data-stu-id="4c8bd-134">Writing a custom DSC resource with PowerShell classes</span></span>](authoringResourceClass.md)

