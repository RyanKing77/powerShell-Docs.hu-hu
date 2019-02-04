---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: DSC-erőforrások hibakeresése
ms.openlocfilehash: 9b2e7dd9b42332b869c4d7fabb21bd4b5a6b8800
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55683953"
---
# <a name="debugging-dsc-resources"></a><span data-ttu-id="01e4b-103">DSC-erőforrások hibakeresése</span><span class="sxs-lookup"><span data-stu-id="01e4b-103">Debugging DSC resources</span></span>

> <span data-ttu-id="01e4b-104">Érvényes: Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="01e4b-104">Applies To: Windows PowerShell 5.0</span></span>

<span data-ttu-id="01e4b-105">A PowerShell 5.0-egy új szolgáltatás jelent meg a kívánt állapot szabásra (DSC), amely lehetővé teszi, hogy a DSC-erőforrások hibakeresése, a konfiguráció alkalmazása folyamatban van.</span><span class="sxs-lookup"><span data-stu-id="01e4b-105">In PowerShell 5.0, a new feature was introduced in Desired State Configuraiton (DSC) that allows you to debug a DSC resource as a configuration is being applied.</span></span>

## <a name="enabling-dsc-debugging"></a><span data-ttu-id="01e4b-106">DSC-hibakeresés engedélyezése</span><span class="sxs-lookup"><span data-stu-id="01e4b-106">Enabling DSC debugging</span></span>
<span data-ttu-id="01e4b-107">Előtt erőforrás hibakeresést is, hogy meghívásával hibakeresés engedélyezése a [engedélyezése – DscDebug](/powershell/module/PSDesiredStateConfiguration/Enable-DscDebug) parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="01e4b-107">Before you can debug a resource, you have to enable debugging by calling the [Enable-DscDebug](/powershell/module/PSDesiredStateConfiguration/Enable-DscDebug) cmdlet.</span></span>
<span data-ttu-id="01e4b-108">Ennél a parancsmagnál egy kötelező paraméter, **BreakAll**.</span><span class="sxs-lookup"><span data-stu-id="01e4b-108">This cmdlet takes a mandatory parameter, **BreakAll**.</span></span>

<span data-ttu-id="01e4b-109">Ellenőrizheti, hogy hibakeresés engedélyezve van a hívás eredménye megnézzük [Get-DscLocalConfigurationManager](/powershell/module/PSDesiredStateConfiguration/Get-DscLocalConfigurationManager).</span><span class="sxs-lookup"><span data-stu-id="01e4b-109">You can verify that debugging has been enabled by looking at the result of a call to [Get-DscLocalConfigurationManager](/powershell/module/PSDesiredStateConfiguration/Get-DscLocalConfigurationManager).</span></span>

<span data-ttu-id="01e4b-110">A következő PowerShell-kimenetet jeleníti meg a hibakeresés engedélyezése:</span><span class="sxs-lookup"><span data-stu-id="01e4b-110">The following PowerShell output shows the result of enabling debugging:</span></span>


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


## <a name="starting-a-configuration-with-debug-enabled"></a><span data-ttu-id="01e4b-111">Egy konfigurációs kezdve hibakeresési engedélyezve</span><span class="sxs-lookup"><span data-stu-id="01e4b-111">Starting a configuration with debug enabled</span></span>
<span data-ttu-id="01e4b-112">A DSC-erőforrások hibakeresése, indítsa el egy konfigurációt, amely meghívja az adott erőforráshoz.</span><span class="sxs-lookup"><span data-stu-id="01e4b-112">To debug a DSC resource, you start a configuration that calls that resource.</span></span>
<span data-ttu-id="01e4b-113">Ebben a példában egy egyszerű konfigurálás, amely meghívja ezt áttekintjük a **WindowsFeature** erőforrást, győződjön meg arról, hogy telepítve van-e a "WindowsPowerShellWebAccess" funkció:</span><span class="sxs-lookup"><span data-stu-id="01e4b-113">For this example, we'll look at a simple configuration that calls the **WindowsFeature** resource to ensure that the "WindowsPowerShellWebAccess" feature is installed:</span></span>

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
<span data-ttu-id="01e4b-114">Miután a konfiguráció fordítása, indítsa el meghívásával [Start-DscConfiguration](/powershell/module/psdesiredstateconfiguration/start-dscconfiguration).</span><span class="sxs-lookup"><span data-stu-id="01e4b-114">After compiling the configuration, start it by calling [Start-DscConfiguration](/powershell/module/psdesiredstateconfiguration/start-dscconfiguration).</span></span>
<span data-ttu-id="01e4b-115">A konfiguráció le fog állni, ha a helyi Configuration Manager (LCM) Konfigurálása az első erőforrásra a konfiguráció a beérkező hívások.</span><span class="sxs-lookup"><span data-stu-id="01e4b-115">The configuration will stop when the Local Configuration Manager (LCM) calls into the first resource in the configuration.</span></span>
<span data-ttu-id="01e4b-116">Ha használja a `-Verbose` és `-Wait` paramétereket, a kimenetet jeleníti meg a sorok, a hibakeresés meg kell adnia.</span><span class="sxs-lookup"><span data-stu-id="01e4b-116">If you use the `-Verbose` and `-Wait` parameters, the output displays the lines you need to enter to start debugging.</span></span>

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
<span data-ttu-id="01e4b-117">Ezen a ponton a LCM nevű erőforrás, és az első töréspont jár.</span><span class="sxs-lookup"><span data-stu-id="01e4b-117">At this point, the LCM has called the resource, and come to the first break point.</span></span>
<span data-ttu-id="01e4b-118">Az utolsó három sort, a kimenetben bemutatják, hogyan csatlakoztathat a folyamat, és indítsa el az erőforrás-parancsprogram-hibakeresés.</span><span class="sxs-lookup"><span data-stu-id="01e4b-118">The last three lines in the output show you how to attach to the process and start debugging the resource script.</span></span>

## <a name="debugging-the-resource-script"></a><span data-ttu-id="01e4b-119">Az erőforrás-parancsprogram-hibakeresés</span><span class="sxs-lookup"><span data-stu-id="01e4b-119">Debugging the resource script</span></span>

<span data-ttu-id="01e4b-120">Indítsa el a PowerShell ISE-ben egy új példányát.</span><span class="sxs-lookup"><span data-stu-id="01e4b-120">Start a new instance of the PowerShell ISE.</span></span>
<span data-ttu-id="01e4b-121">A konzol ablaktáblában adja meg az utolsó három sort kimenetét a `Start-DscConfiguration` as-parancsok, és cserélje le a kimeneti `<credentials>` érvényes felhasználói hitelesítő adatokat.</span><span class="sxs-lookup"><span data-stu-id="01e4b-121">In the console pane, enter the last three lines of output from the `Start-DscConfiguration` output as commands, replacing `<credentials>` with valid user credentials.</span></span>
<span data-ttu-id="01e4b-122">Meg kell jelennie egy parancssort, amely hasonlít:</span><span class="sxs-lookup"><span data-stu-id="01e4b-122">You should now see a prompt that looks similar to:</span></span>

```powershell
[TEST-SRV]: [DBG]: [Process:9000]: [RemoteHost]: PS C:\DebugTest>>
```

<span data-ttu-id="01e4b-123">Az erőforrás-parancsfájl nyílik meg a parancsfájl panelen és a hibakeresőt le van állítva, az első sor a **Test-TargetResource** funkció (a **Test()** módszer egy adott osztály-alapú erőforrás).</span><span class="sxs-lookup"><span data-stu-id="01e4b-123">The resource script will open in the script pane, and the debugger is stopped at the first line of the **Test-TargetResource** function (the **Test()** method of a class-based resource).</span></span>
<span data-ttu-id="01e4b-124">Most már használhatja a hibakeresési parancsokat az ISE-ben az erőforrás-parancsfájl elvégezhető, tekintse meg változóértékek, megtekintheti a hívási verem, és így tovább.</span><span class="sxs-lookup"><span data-stu-id="01e4b-124">Now you can use the debug commands in the ISE to step through the resource script, look at variable values, view the call stack, and so on.</span></span> <span data-ttu-id="01e4b-125">Ne feledje, hogy az erőforrás parancsfájl (vagy osztály) minden sor egy töréspontot van beállítva.</span><span class="sxs-lookup"><span data-stu-id="01e4b-125">Remember that every line in the resource script (or class) is set as a break point.</span></span>

## <a name="disabling-dsc-debugging"></a><span data-ttu-id="01e4b-126">DSC-hibakeresés letiltása</span><span class="sxs-lookup"><span data-stu-id="01e4b-126">Disabling DSC debugging</span></span>

<span data-ttu-id="01e4b-127">Hívása után [engedélyezése – DscDebug](/powershell/module/PSDesiredStateConfiguration/Enable-DscDebug), minden hívásainak [Start-DscConfiguration](/powershell/module/psdesiredstateconfiguration/start-dscconfiguration) a használhatatlanná tévő belépjen a hibakeresőbe konfigurációt eredményez.</span><span class="sxs-lookup"><span data-stu-id="01e4b-127">After calling [Enable-DscDebug](/powershell/module/PSDesiredStateConfiguration/Enable-DscDebug), all calls to [Start-DscConfiguration](/powershell/module/psdesiredstateconfiguration/start-dscconfiguration) will result in the configuration breaking into the debugger.</span></span> <span data-ttu-id="01e4b-128">Ahhoz, hogy a konfigurációk a normál módon futnak, le kell tiltania meghívásával hibakeresés a [Disable-DscDebug](/powershell/module/PSDesiredStateConfiguration/Disable-DscDebug) parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="01e4b-128">To allow configurations to run normally, you must disable debugging by calling the [Disable-DscDebug](/powershell/module/PSDesiredStateConfiguration/Disable-DscDebug) cmdlet.</span></span>

><span data-ttu-id="01e4b-129">**Megjegyzés:** Újraindítás a LCM hibakeresési állapota nem változik.</span><span class="sxs-lookup"><span data-stu-id="01e4b-129">**Note:** Rebooting does not change the debug state of the LCM.</span></span> <span data-ttu-id="01e4b-130">Hibakeresés engedélyezve van, ha egy konfigurációs indítása fog továbbra is megszakítással belépjen a hibakeresőbe újraindítás után.</span><span class="sxs-lookup"><span data-stu-id="01e4b-130">If debugging is enabled, starting a configuration will still break into the debugger after a reboot.</span></span>

## <a name="see-also"></a><span data-ttu-id="01e4b-131">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="01e4b-131">See Also</span></span>

- [<span data-ttu-id="01e4b-132">MOF-egyéni DSC-erőforrás írása</span><span class="sxs-lookup"><span data-stu-id="01e4b-132">Writing a custom DSC resource with MOF</span></span>](../resources/authoringResourceMOF.md)
- [<span data-ttu-id="01e4b-133">A PowerShell-osztályok egyéni DSC-erőforrás írása</span><span class="sxs-lookup"><span data-stu-id="01e4b-133">Writing a custom DSC resource with PowerShell classes</span></span>](../resources/authoringResourceClass.md)
