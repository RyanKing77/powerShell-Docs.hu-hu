---
ms.date: 06/12/2017
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: DSC-erőforrások hibakeresése
ms.openlocfilehash: 30d49768fc2301b5306d0001e157d60e2e991883
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/17/2018
---
# <a name="debugging-dsc-resources"></a>DSC-erőforrások hibakeresése

> Vonatkozik: A Windows PowerShell 5.0

A PowerShell 5.0-s egy új szolgáltatás a szükséges állapot szabásra szolgáló elemeit (DSC), amely lehetővé teszi a DSC-erőforrás hibakeresési módon végzi a configuration jelent meg.

## <a name="enabling-dsc-debugging"></a>A DSC-hibakeresés engedélyezése
Mielőtt egy erőforrás megoldhassuk, fel kell meghívásával hibakeresés engedélyezése a [Enable-DscDebug](https://technet.microsoft.com/library/mt517870.aspx) parancsmag.
Ez a parancsmag egy kötelező paramétert fogad, **BreakAll**.

Ellenőrizheti, hogy hibakeresés engedélyezve van a hívás eredménye alapján [Get-DscLocalConfigurationManager](https://technet.microsoft.com/library/dn407378.aspx).

A következő PowerShell-kimenet hibakeresés engedélyezése eredményének megjelenítése:


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
A DSC-erőforrás hibakeresési, olyan konfigurációt, amely meghívja az adott erőforrás indítsa el.
Ehhez a példához megnézzük, egy egyszerű konfiguráció, amely behívja a [WindowsFeature](windowsfeatureResource.md) erőforrást, győződjön meg arról, hogy telepítve van-e a "WindowsPowerShellWebAccess" funkció:

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
A konfiguráció fordítása, után indítsa el azt meghívásával [Start-DscConfiguration](https://technet.microsoft.com/library/dn521623.aspx).
A konfigurációs leáll, amikor az első erőforrásra a konfigurációban az meghívja a helyi Configuration Manager (LCM).
Ha használja a `-Verbose` és `-Wait` paraméterek, a kimeneti sorait jeleníti meg, meg kell adnia a hibakeresés.

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
Ezen a ponton a LCM az erőforrás neve, és az első töréspontot tudomást.
Az utolsó három sort a kimenetben bemutatják a folyamat csatolja, és indítsa el az erőforrást parancsprogram-hibakeresés.

## <a name="debugging-the-resource-script"></a>Az erőforrást parancsprogram-hibakeresés

Indítsa el a PowerShell ISE egy új példányát.
A konzol ablaktáblájában adja meg az utolsó három sort kimenetét a `Start-DscConfiguration` parancsok, cseréje kimeneti `<credentials>` érvényes felhasználói hitelesítő adatokat.
Ekkor megjelenik egy értesítés, a következőhöz hasonló:

```powershell
[TEST-SRV]: [DBG]: [Process:9000]: [RemoteHost]: PS C:\DebugTest>>
```

Az erőforrást parancsprogram nyílik meg a parancssori panelbe, és a hibakereső le van állítva, az első sor a **teszt-TargetResource** függvény (a **Test()** metódus osztály-alapú erőforrás).
Most már használhat a hibakeresési parancsok a ISE teljesítéséhez a erőforrást parancsprogram, változók értékeinek meg, a hívási verem megtekintése, és így tovább.
További információ a PowerShell ISE-hibakeresés: [parancsfájlok hibakeresése a Windows PowerShell ISE hogyan](https://technet.microsoft.com/en-us/library/dd819480.aspx).
Ne feledje, hogy a erőforrást parancsprogram (vagy a osztály) minden sor egy töréspontot értéke.

## <a name="disabling-dsc-debugging"></a>A DSC-hibakeresés letiltása

Hívása után [Enable-DscDebug](https://technet.microsoft.com/library/mt517870.aspx), minden hívások [Start-DscConfiguration](https://technet.microsoft.com/library/dn521623.aspx) belépjen a hibakeresőbe megtörje a konfigurációt eredményez. Ahhoz, hogy konfigurálható, hogy a normál módon futnak, le kell tiltania meghívásával hibakeresés a [Disable-DscDebug](https://technet.microsoft.com/en-us/library/mt517872.aspx) parancsmag.

>**Megjegyzés:** Rebooting nem változik a LCM hibakeresési állapotát. Hibakeresés engedélyezve van, ha egy konfigurációs indítása fog továbbra is megszakítással belépjen a hibakeresőbe a rendszer újraindítása után.


## <a name="see-also"></a>Lásd még:
- [Egyéni DSC-erőforrás MOF írása](authoringResourceMOF.md)
- [A PowerShell osztályok egyéni DSC-erőforrás írása](authoringResourceClass.md)