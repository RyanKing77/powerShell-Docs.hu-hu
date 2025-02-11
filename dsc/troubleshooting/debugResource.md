---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: DSC-erőforrások hibakeresése
ms.openlocfilehash: c088e13a25ba31ceebaf52b2d24b5d32b96ae2fc
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62076803"
---
# <a name="debugging-dsc-resources"></a>DSC-erőforrások hibakeresése

> A következőkre vonatkozik: Windows PowerShell 5.0

A PowerShell 5.0-egy új szolgáltatás jelent a Desired State Configuration (DSC), amely lehetővé teszi, hogy a DSC-erőforrások hibakeresése, a konfiguráció alkalmazása folyamatban van.

## <a name="enabling-dsc-debugging"></a>DSC-hibakeresés engedélyezése
Előtt erőforrás hibakeresést is, hogy meghívásával hibakeresés engedélyezése a [engedélyezése – DscDebug](/powershell/module/PSDesiredStateConfiguration/Enable-DscDebug) parancsmagot.
Ennél a parancsmagnál egy kötelező paraméter, **BreakAll**.

Ellenőrizheti, hogy hibakeresés engedélyezve van a hívás eredménye megnézzük [Get-DscLocalConfigurationManager](/powershell/module/PSDesiredStateConfiguration/Get-DscLocalConfigurationManager).

A következő PowerShell-kimenetet jeleníti meg a hibakeresés engedélyezése:


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


## <a name="starting-a-configuration-with-debug-enabled"></a>Egy konfigurációs kezdve hibakeresési engedélyezve
A DSC-erőforrások hibakeresése, indítsa el egy konfigurációt, amely meghívja az adott erőforráshoz.
Ebben a példában egy egyszerű konfigurálás, amely meghívja ezt áttekintjük a **WindowsFeature** erőforrást, győződjön meg arról, hogy telepítve van-e a "WindowsPowerShellWebAccess" funkció:

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
Miután a konfiguráció fordítása, indítsa el meghívásával [Start-DscConfiguration](/powershell/module/psdesiredstateconfiguration/start-dscconfiguration).
A konfiguráció le fog állni, ha a helyi Configuration Manager (LCM) Konfigurálása az első erőforrásra a konfiguráció a beérkező hívások.
Ha használja a `-Verbose` és `-Wait` paramétereket, a kimenetet jeleníti meg a sorok, a hibakeresés meg kell adnia.

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
Ezen a ponton a LCM nevű erőforrás, és az első töréspont jár.
Az utolsó három sort, a kimenetben bemutatják, hogyan csatlakoztathat a folyamat, és indítsa el az erőforrás-parancsprogram-hibakeresés.

## <a name="debugging-the-resource-script"></a>Az erőforrás-parancsprogram-hibakeresés

Indítsa el a PowerShell ISE-ben egy új példányát.
A konzol ablaktáblában adja meg az utolsó három sort kimenetét a `Start-DscConfiguration` as-parancsok, és cserélje le a kimeneti `<credentials>` érvényes felhasználói hitelesítő adatokat.
Meg kell jelennie egy parancssort, amely hasonlít:

```powershell
[TEST-SRV]: [DBG]: [Process:9000]: [RemoteHost]: PS C:\DebugTest>>
```

Az erőforrás-parancsfájl nyílik meg a parancsfájl panelen és a hibakeresőt le van állítva, az első sor a **Test-TargetResource** funkció (a **Test()** módszer egy adott osztály-alapú erőforrás).
Most már használhatja a hibakeresési parancsokat az ISE-ben az erőforrás-parancsfájl elvégezhető, tekintse meg változóértékek, megtekintheti a hívási verem, és így tovább. Ne feledje, hogy az erőforrás parancsfájl (vagy osztály) minden sor egy töréspontot van beállítva.

## <a name="disabling-dsc-debugging"></a>DSC-hibakeresés letiltása

Hívása után [engedélyezése – DscDebug](/powershell/module/PSDesiredStateConfiguration/Enable-DscDebug), minden hívásainak [Start-DscConfiguration](/powershell/module/psdesiredstateconfiguration/start-dscconfiguration) a használhatatlanná tévő belépjen a hibakeresőbe konfigurációt eredményez. Ahhoz, hogy a konfigurációk a normál módon futnak, le kell tiltania meghívásával hibakeresés a [Disable-DscDebug](/powershell/module/PSDesiredStateConfiguration/Disable-DscDebug) parancsmagot.

>**Megjegyzés:** Újraindítás a LCM hibakeresési állapota nem változik. Hibakeresés engedélyezve van, ha egy konfigurációs indítása fog továbbra is megszakítással belépjen a hibakeresőbe újraindítás után.

## <a name="see-also"></a>Lásd még:

- [MOF-egyéni DSC-erőforrás írása](../resources/authoringResourceMOF.md)
- [A PowerShell-osztályok egyéni DSC-erőforrás írása](../resources/authoringResourceClass.md)
