---
ms.date: 12/12/2018
keywords: DSC, powershell, a konfigurációt, a beállítása
title: Apply, Get és Test konfigurációk csomóponton
ms.openlocfilehash: 41f8d2d75d3dd9621de615e7999c2690cb8ce44a
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55684338"
---
# <a name="apply-get-and-test-configurations-on-a-node"></a>Apply, Get és Test konfigurációk csomóponton

Ez az útmutató bemutatja, hogyan használható a konfigurációkat egy cél csomópont. Ez az útmutató az alábbi lépéseket van osztva:

## <a name="apply-a-configuration"></a>A konfiguráció alkalmazása

Annak érdekében, hogy a alkalmazni, és egy konfigurációjának kezelése, igazolnia kell a ".mof" fájl. Az alábbi kód egy egyszerű konfigurálás, ebben az útmutatóban használt képviseli.

```powershell
Configuration Sample
{
    # This will generate two .mof files, a localhost.mof, and a server02.mof
    Node localhost, server02
    {
        File SampleFile
        {
            DestinationPath = 'C:\Temp\temp.txt'
            Contents = 'This is a simple resource to show Configuration functionality on a Node.'
        }
    }
}

# The -OutputPath parameter is built into every Configuration automatically.
# The value of -OutputPath determines where the .mof file should be stored, once compiled.
Sample -OutputPath "C:\Temp\"
```

Ez a konfiguráció fordítása előállításához két ".mof" fájlt.

```output
Mode                LastWriteTime     Length Name
----                -------------     ------ ----
-a----       11/27/2018   7:29 AM     2.13KB localhost.mof
-a----       11/27/2018   7:29 AM     2.13KB server02.mof
```

A alkalmazni a konfigurációt, használja a [Start-DSCConfiguration](/powershell/module/psdesiredstateconfiguration/start-dscconfiguration) parancsmagot. A `-Path` paraméter adja meg a ".mof" fájlokat tároló könyvtár. Ha nincs `-Computername` meg van adva, `Start-DSCConfiguration` megkísérli minden egyes konfiguráció alkalmazása a számítógép nevére, a ".mof" fájl neve által megadott (\<computername\>.mof). Adja meg `-Verbose` való `Start-DSCConfiguration` a részletesebb kimenet megtekintéséhez.

```powershell
Start-DSCConfiguration -Path C:\Temp\ -Verbose
```

Ha `-Wait` nincs megadva, láthatja, hogy létrehozott egy feladat. A feladathoz létrehozott egy lesz **ChildJob** által feldolgozott ".mof" fájl esetében `Start-DSCConfiguration`.

```output
Id     Name            PSJobTypeName   State         HasMoreData     Location             Command
--     ----            -------------   -----         -----------     --------             -------
45     Job45           Configuratio... Running       True            localhost,server02   Start-DSCConfiguration...
```

Egy konfigurációs van a hosszú ideig tart, és le azt szeretné, használhatja [Stop-DSCConfiguration](/powershell/module/PSDesiredStateConfiguration/Stop-DscConfiguration) , állítsa le az alkalmazást a helyi csomóponton.

```powershell
Stop-DSCConfiguration -Force
```

Ha elkészült, a feladat által visszaadott objektum keresztül a feladatok állapotát megtekintheti [Get-Job](/powershell/module/microsoft.powershell.core/get-job).

```powershell
$job = Get-Job
$job.ChildJobs
```

```output
Id     Name            PSJobTypeName   State         HasMoreData     Location             Command
--     ----            -------------   -----         -----------     --------             -------
49     Job49           Configuratio... Completed     True            localhost            Start-DSCConfiguration...
50     Job50           Configuratio... Completed     True            server02             Start-DSCConfiguration...
```

Megtekintheti a **részletes** kimeneti, a következő parancsok segítségével megtekintheti a **részletes** minden stream **ChildJob**. PowerShell-feladatokkal kapcsolatos további információkért lásd: [about_Jobs](/powershell/module/microsoft.powershell.core/about/about_jobs).

```powershell
# View the verbose output of the localhost job using array indexing.
$job.ChildJobs[0].Verbose
```

```output
Perform operation 'Invoke CimMethod' with following parameters, ''methodName' = SendConfigurationApply,'className' = MSFT_DSCLocalConfigurationManager,'namespaceName' = root/Microsoft/Windows/DesiredStateConfiguration'.
An LCM method call arrived from computer SERVER01 with user sid S-1-5-21-124525095-708259637-1543119021-1282804.
[SERVER01]: LCM:  [ Start  Set      ]
[SERVER01]: LCM:  [ Start  Resource ]  [[File]SampleFile]
[SERVER01]: LCM:  [ Start  Test     ]  [[File]SampleFile]
[SERVER01]:                            [[File]SampleFile] The destination object was found and no action is required.
[SERVER01]: LCM:  [ End    Test     ]  [[File]SampleFile]  in 0.0370 seconds.
[SERVER01]: LCM:  [ Skip   Set      ]  [[File]SampleFile]
[SERVER01]: LCM:  [ End    Resource ]  [[File]SampleFile]
[SERVER01]: LCM:  [ End    Set      ]
[SERVER01]: LCM:  [ End    Set      ]    in  0.2400 seconds.
Operation 'Invoke CimMethod' complete.
```

A PowerShell 5.0-, kezdve a `-UseExisting` paraméter hozzá lett adva `Start-DSCConfiguration`. Megadásával `-UseExisting`, utasíthatja a parancsmagot használja a meglévő alkalmazott konfiguráció által meghatározott helyett a `-Path` paraméter.

```powershell
Start-DSCConfiguration -UseExisting -Verbose -Wait
```

## <a name="test-a-configuration"></a>A konfiguráció tesztelése

Jelenleg az alkalmazott konfiguráció használatával tesztelhet [a Test-DSCConfiguration](/powershell/module/psdesiredstateconfiguration/Test-DSCConfiguration). `Test-DSCConfiguration` Visszaadja `True` a csomópont nem megfelelő, ha és `False` , ha nincs.

```powershell
Test-DSCConfiguration
```

A PowerShell 5.0-, kezdve a `-Detailed` paraméter hozzá lett adva, a gyűjtemények egy objektumot ad vissza, amely **ResourcesInDesiredState** és **ResourcesNotInDesiredState**

```powershell
Test-DSCConfiguration -Detailed
```

PowerShell 5.0 kezdve, tesztelheti a konfiguráció alkalmazása nélkül. A `-ReferenceConfiguration` paraméter elfogadja a fájl elérési útját ".mof" a csomóponton elleni teszteléséhez. Nem **beállítása** műveleteket hajtja végre a csomópont ellen. A PowerShell 4.0-s azokat a kerülő megoldásokat a konfiguráció tesztelése alkalmazása nélkül, de azok vannak nem ismertetünk.

## <a name="get-configuration-values"></a>Konfigurációs értékek beolvasása

A [Get-DSCConfiguration](/powershell/module/PSDesiredStateConfiguration/Get-DscConfiguration) parancsmag jelenleg alkalmazott konfigurációját a konfigurált erőforrások aktuális értékeit adja vissza.

```powershell
Get-DSCConfiguration
```

A minta konfigurációs kimenete lenne ha sikeres.

```output
ConfigurationName    : Sample
DependsOn            :
ModuleName           : PSDesiredStateConfiguration
ModuleVersion        :
PsDscRunAsCredential :
ResourceId           : [File]SampleFile
SourceInfo           :
Attributes           : {archive}
Checksum             :
Contents             :
CreatedDate          : 11/27/2018 7:16:06 AM
Credential           :
DestinationPath      : C:\Temp\temp.txt
Ensure               : present
Force                :
MatchSource          :
ModifiedDate         : 11/27/2018 7:16:06 AM
Recurse              :
Size                 : 75
SourcePath           :
SubItems             :
Type                 : file
PSComputerName       :
CimClassName         : MSFT_FileDirectoryConfiguration
```

## <a name="get-configuration-status"></a>Konfigurációs állapot beolvasása

A PowerShell 5.0 kezdve a [Get-DSCConfigurationStatus](/powershell/module/PSDesiredStateConfiguration/Get-DscConfigurationStatus) parancsmag lehetővé teszi az alkalmazott konfiguráció a csomópontra előzményeit. PowerShell DSC nyomon követi, hogy az utolsó {{N}} konfigurációk a alkalmazni **leküldéses** vagy **lekéréses** mód. Ez magában foglalja, bármely *konzisztencia* az LCM által végrehajtott ellenőrzések. Alapértelmezés szerint `Get-DSCConfigurationStatus` csak a legutóbbi előzményeinek tétel látható.

```powershell
Get-DSCConfigurationStatus
```

```output
Status     StartDate                 Type            Mode  RebootRequested      NumberOfResources
------     ---------                 ----            ----  ---------------      -----------------
Success    11/27/2018 7:18:40 AM     Consistency     PUSH  False                1
```

Használja a `-All` paraméter az összes konfigurációs ügyfélállapot előzményeinek megtekintéséhez.

> [!NOTE]
> Kimeneti kivonatosan csonkítja.

```powershell
Get-DSCConfigurationStatus -All
```

```output
Status     StartDate                 Type            Mode  RebootRequested      NumberOfResources
------     ---------                 ----            ----  ---------------      -----------------
Success    11/27/2018 7:18:40 AM     Consistency     PUSH  False                1
Success    11/27/2018 7:16:06 AM     Initial         PUSH  False                1
Success    11/27/2018 7:04:53 AM     Initial         PUSH  False                1
Success    11/27/2018 7:03:45 AM     Consistency     PUSH  False                2
Success    11/27/2018 7:03:40 AM     Consistency     PUSH  False                2
Success    11/27/2018 6:48:40 AM     Consistency     PUSH  False                2
Success    11/27/2018 6:33:44 AM     Consistency     PUSH  False                2
Success    11/27/2018 6:33:40 AM     Consistency     PUSH  False                2
Success    11/27/2018 6:18:40 AM     Consistency     PUSH  False                2
Success    11/27/2018 6:03:44 AM     Consistency     PUSH  False                2
```

## <a name="manage-configuration-documents"></a>Konfigurációs dokumentumok kezelése

Az LCM kezeli a konfigurációt a csomópont révén **konfigurációs dokumentumok**. Ezek a fájlok ".mof" a "C:\Windows\System32\Configuration" könyvtárban találhatók.

A PowerShell 5.0 kezdve a [Remove-DSCConfigurationDocument](/powershell/module/PSDesiredStateConfiguration/Remove-DscConfigurationDocument) lehetővé teszi, hogy távolítsa el a ".mof" fájlokat jövőbeli konzisztencia-ellenőrzések leállítani, vagy távolítsa el a konfigurációt, amely rendelkezik a hibákat, amikor a alkalmazni. A `-Stage` paraméter lehetővé teszi, hogy adja meg, melyik ".mof" fájl el kívánja távolítani.

```powershell
Remove-DSCConfigurationDocument -Stage Current
```

> [!NOTE]
> A PowerShell 4.0-s, továbbra is távolítsa el a közvetlenül ezek ".mof" a fájlok [Remove-cikk](/powershell/module/microsoft.powershell.management/remove-item).

## <a name="publish-configurations"></a>Konfigurációk közzététele

A PowerShell 5.0-, kezdve a [Publish-DSCConfiguration](/powershell/module/PSDesiredStateConfiguration/Publish-DscConfiguration) parancsmag lett hozzáadva. Ez a parancsmag lehetővé teszi a távoli számítógépek egy ".mof" fájl közzététele alkalmazása nélkül.

```powershell
Publish-DscConfiguration -Path '$home\WebServer' -ComputerName "ContosoWebServer" -Credential (get-credential Contoso\webadministrator)
```

## <a name="see-also"></a>Lásd még:

- [GET, tesztelési, és állítsa be](../resources/get-test-set.md)
