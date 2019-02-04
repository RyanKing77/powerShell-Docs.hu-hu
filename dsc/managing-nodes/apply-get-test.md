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
# <a name="apply-get-and-test-configurations-on-a-node"></a><span data-ttu-id="3182a-103">Apply, Get és Test konfigurációk csomóponton</span><span class="sxs-lookup"><span data-stu-id="3182a-103">Apply, Get, and Test Configurations on a Node</span></span>

<span data-ttu-id="3182a-104">Ez az útmutató bemutatja, hogyan használható a konfigurációkat egy cél csomópont.</span><span class="sxs-lookup"><span data-stu-id="3182a-104">This guide will show you how to work with Configurations on a target Node.</span></span> <span data-ttu-id="3182a-105">Ez az útmutató az alábbi lépéseket van osztva:</span><span class="sxs-lookup"><span data-stu-id="3182a-105">This guide is broken up into the following steps:</span></span>

## <a name="apply-a-configuration"></a><span data-ttu-id="3182a-106">A konfiguráció alkalmazása</span><span class="sxs-lookup"><span data-stu-id="3182a-106">Apply a Configuration</span></span>

<span data-ttu-id="3182a-107">Annak érdekében, hogy a alkalmazni, és egy konfigurációjának kezelése, igazolnia kell a ".mof" fájl.</span><span class="sxs-lookup"><span data-stu-id="3182a-107">In order to apply and manage a Configuration, we need to generate a ".mof" file.</span></span> <span data-ttu-id="3182a-108">Az alábbi kód egy egyszerű konfigurálás, ebben az útmutatóban használt képviseli.</span><span class="sxs-lookup"><span data-stu-id="3182a-108">The following code will represent a simple Configuration that will be used throughout this guide.</span></span>

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

<span data-ttu-id="3182a-109">Ez a konfiguráció fordítása előállításához két ".mof" fájlt.</span><span class="sxs-lookup"><span data-stu-id="3182a-109">Compiling this configuration will yield two ".mof" files.</span></span>

```output
Mode                LastWriteTime     Length Name
----                -------------     ------ ----
-a----       11/27/2018   7:29 AM     2.13KB localhost.mof
-a----       11/27/2018   7:29 AM     2.13KB server02.mof
```

<span data-ttu-id="3182a-110">A alkalmazni a konfigurációt, használja a [Start-DSCConfiguration](/powershell/module/psdesiredstateconfiguration/start-dscconfiguration) parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="3182a-110">To apply a Configuration, use the [Start-DSCConfiguration](/powershell/module/psdesiredstateconfiguration/start-dscconfiguration) cmdlet.</span></span> <span data-ttu-id="3182a-111">A `-Path` paraméter adja meg a ".mof" fájlokat tároló könyvtár.</span><span class="sxs-lookup"><span data-stu-id="3182a-111">The `-Path` parameter specifies a directory where ".mof" files reside.</span></span> <span data-ttu-id="3182a-112">Ha nincs `-Computername` meg van adva, `Start-DSCConfiguration` megkísérli minden egyes konfiguráció alkalmazása a számítógép nevére, a ".mof" fájl neve által megadott (\<computername\>.mof).</span><span class="sxs-lookup"><span data-stu-id="3182a-112">If no `-Computername` is specified, `Start-DSCConfiguration` will attempt to apply each Configuration to the computer name specified by the name of the '.mof' file (\<computername\>.mof).</span></span> <span data-ttu-id="3182a-113">Adja meg `-Verbose` való `Start-DSCConfiguration` a részletesebb kimenet megtekintéséhez.</span><span class="sxs-lookup"><span data-stu-id="3182a-113">Specify `-Verbose` to `Start-DSCConfiguration` to see more verbose output.</span></span>

```powershell
Start-DSCConfiguration -Path C:\Temp\ -Verbose
```

<span data-ttu-id="3182a-114">Ha `-Wait` nincs megadva, láthatja, hogy létrehozott egy feladat.</span><span class="sxs-lookup"><span data-stu-id="3182a-114">If `-Wait` is not specified, you see one job created.</span></span> <span data-ttu-id="3182a-115">A feladathoz létrehozott egy lesz **ChildJob** által feldolgozott ".mof" fájl esetében `Start-DSCConfiguration`.</span><span class="sxs-lookup"><span data-stu-id="3182a-115">The job created will have one **ChildJob** for each ".mof" file processed by `Start-DSCConfiguration`.</span></span>

```output
Id     Name            PSJobTypeName   State         HasMoreData     Location             Command
--     ----            -------------   -----         -----------     --------             -------
45     Job45           Configuratio... Running       True            localhost,server02   Start-DSCConfiguration...
```

<span data-ttu-id="3182a-116">Egy konfigurációs van a hosszú ideig tart, és le azt szeretné, használhatja [Stop-DSCConfiguration](/powershell/module/PSDesiredStateConfiguration/Stop-DscConfiguration) , állítsa le az alkalmazást a helyi csomóponton.</span><span class="sxs-lookup"><span data-stu-id="3182a-116">If a Configuration is taking a long time and you want to stop it, you can use [Stop-DSCConfiguration](/powershell/module/PSDesiredStateConfiguration/Stop-DscConfiguration) to stop application on the local Node.</span></span>

```powershell
Stop-DSCConfiguration -Force
```

<span data-ttu-id="3182a-117">Ha elkészült, a feladat által visszaadott objektum keresztül a feladatok állapotát megtekintheti [Get-Job](/powershell/module/microsoft.powershell.core/get-job).</span><span class="sxs-lookup"><span data-stu-id="3182a-117">Once complete, you can view the status of the jobs through the job object returned by [Get-Job](/powershell/module/microsoft.powershell.core/get-job).</span></span>

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

<span data-ttu-id="3182a-118">Megtekintheti a **részletes** kimeneti, a következő parancsok segítségével megtekintheti a **részletes** minden stream **ChildJob**.</span><span class="sxs-lookup"><span data-stu-id="3182a-118">To see the **Verbose** output, use the following commands to view the **Verbose** stream for each **ChildJob**.</span></span> <span data-ttu-id="3182a-119">PowerShell-feladatokkal kapcsolatos további információkért lásd: [about_Jobs](/powershell/module/microsoft.powershell.core/about/about_jobs).</span><span class="sxs-lookup"><span data-stu-id="3182a-119">For more about PowerShell jobs, see [about_Jobs](/powershell/module/microsoft.powershell.core/about/about_jobs).</span></span>

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

<span data-ttu-id="3182a-120">A PowerShell 5.0-, kezdve a `-UseExisting` paraméter hozzá lett adva `Start-DSCConfiguration`.</span><span class="sxs-lookup"><span data-stu-id="3182a-120">Beginning in PowerShell 5.0, the `-UseExisting` parameter was added to `Start-DSCConfiguration`.</span></span> <span data-ttu-id="3182a-121">Megadásával `-UseExisting`, utasíthatja a parancsmagot használja a meglévő alkalmazott konfiguráció által meghatározott helyett a `-Path` paraméter.</span><span class="sxs-lookup"><span data-stu-id="3182a-121">By specifying `-UseExisting`, you instruct the cmdlet to use the existing applied Configuration instead of one specified by the `-Path` parameter.</span></span>

```powershell
Start-DSCConfiguration -UseExisting -Verbose -Wait
```

## <a name="test-a-configuration"></a><span data-ttu-id="3182a-122">A konfiguráció tesztelése</span><span class="sxs-lookup"><span data-stu-id="3182a-122">Test a Configuration</span></span>

<span data-ttu-id="3182a-123">Jelenleg az alkalmazott konfiguráció használatával tesztelhet [a Test-DSCConfiguration](/powershell/module/psdesiredstateconfiguration/Test-DSCConfiguration).</span><span class="sxs-lookup"><span data-stu-id="3182a-123">You can test a currently applied Configuration using [Test-DSCConfiguration](/powershell/module/psdesiredstateconfiguration/Test-DSCConfiguration).</span></span> <span data-ttu-id="3182a-124">`Test-DSCConfiguration` Visszaadja `True` a csomópont nem megfelelő, ha és `False` , ha nincs.</span><span class="sxs-lookup"><span data-stu-id="3182a-124">`Test-DSCConfiguration` will return `True` if the Node is compliant, and `False` if it is not.</span></span>

```powershell
Test-DSCConfiguration
```

<span data-ttu-id="3182a-125">A PowerShell 5.0-, kezdve a `-Detailed` paraméter hozzá lett adva, a gyűjtemények egy objektumot ad vissza, amely **ResourcesInDesiredState** és **ResourcesNotInDesiredState**</span><span class="sxs-lookup"><span data-stu-id="3182a-125">Beginning in PowerShell 5.0, the `-Detailed` parameter was added which returns an object with collections for **ResourcesInDesiredState** and **ResourcesNotInDesiredState**</span></span>

```powershell
Test-DSCConfiguration -Detailed
```

<span data-ttu-id="3182a-126">PowerShell 5.0 kezdve, tesztelheti a konfiguráció alkalmazása nélkül.</span><span class="sxs-lookup"><span data-stu-id="3182a-126">Beginning in PowerShell 5.0 you can test a Configuration without applying it.</span></span> <span data-ttu-id="3182a-127">A `-ReferenceConfiguration` paraméter elfogadja a fájl elérési útját ".mof" a csomóponton elleni teszteléséhez.</span><span class="sxs-lookup"><span data-stu-id="3182a-127">The `-ReferenceConfiguration` parameter accepts the path of a ".mof" file to test the Node against.</span></span> <span data-ttu-id="3182a-128">Nem **beállítása** műveleteket hajtja végre a csomópont ellen.</span><span class="sxs-lookup"><span data-stu-id="3182a-128">No **Set** actions are taken against the Node.</span></span> <span data-ttu-id="3182a-129">A PowerShell 4.0-s azokat a kerülő megoldásokat a konfiguráció tesztelése alkalmazása nélkül, de azok vannak nem ismertetünk.</span><span class="sxs-lookup"><span data-stu-id="3182a-129">In PowerShell 4.0, there are workarounds to test a Configuration without applying it, but they are not discussed here.</span></span>

## <a name="get-configuration-values"></a><span data-ttu-id="3182a-130">Konfigurációs értékek beolvasása</span><span class="sxs-lookup"><span data-stu-id="3182a-130">Get Configuration Values</span></span>

<span data-ttu-id="3182a-131">A [Get-DSCConfiguration](/powershell/module/PSDesiredStateConfiguration/Get-DscConfiguration) parancsmag jelenleg alkalmazott konfigurációját a konfigurált erőforrások aktuális értékeit adja vissza.</span><span class="sxs-lookup"><span data-stu-id="3182a-131">The [Get-DSCConfiguration](/powershell/module/PSDesiredStateConfiguration/Get-DscConfiguration) cmdlet returns the current values for any configured resources in the currently applied Configuration.</span></span>

```powershell
Get-DSCConfiguration
```

<span data-ttu-id="3182a-132">A minta konfigurációs kimenete lenne ha sikeres.</span><span class="sxs-lookup"><span data-stu-id="3182a-132">Output from our sample Configuration would look like this if applied successfully.</span></span>

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

## <a name="get-configuration-status"></a><span data-ttu-id="3182a-133">Konfigurációs állapot beolvasása</span><span class="sxs-lookup"><span data-stu-id="3182a-133">Get Configuration Status</span></span>

<span data-ttu-id="3182a-134">A PowerShell 5.0 kezdve a [Get-DSCConfigurationStatus](/powershell/module/PSDesiredStateConfiguration/Get-DscConfigurationStatus) parancsmag lehetővé teszi az alkalmazott konfiguráció a csomópontra előzményeit.</span><span class="sxs-lookup"><span data-stu-id="3182a-134">Beginning in PowerShell 5.0 the [Get-DSCConfigurationStatus](/powershell/module/PSDesiredStateConfiguration/Get-DscConfigurationStatus) cmdlet allows you to see the history of applied Configurations to the node.</span></span> <span data-ttu-id="3182a-135">PowerShell DSC nyomon követi, hogy az utolsó {{N}} konfigurációk a alkalmazni **leküldéses** vagy **lekéréses** mód.</span><span class="sxs-lookup"><span data-stu-id="3182a-135">PowerShell DSC keeps track of the last {{N}} Configurations applied in **Push** or **Pull** mode.</span></span> <span data-ttu-id="3182a-136">Ez magában foglalja, bármely *konzisztencia* az LCM által végrehajtott ellenőrzések.</span><span class="sxs-lookup"><span data-stu-id="3182a-136">This includes any *consistency* checks executed by the LCM.</span></span> <span data-ttu-id="3182a-137">Alapértelmezés szerint `Get-DSCConfigurationStatus` csak a legutóbbi előzményeinek tétel látható.</span><span class="sxs-lookup"><span data-stu-id="3182a-137">By default, `Get-DSCConfigurationStatus` shows you the last history entry only.</span></span>

```powershell
Get-DSCConfigurationStatus
```

```output
Status     StartDate                 Type            Mode  RebootRequested      NumberOfResources
------     ---------                 ----            ----  ---------------      -----------------
Success    11/27/2018 7:18:40 AM     Consistency     PUSH  False                1
```

<span data-ttu-id="3182a-138">Használja a `-All` paraméter az összes konfigurációs ügyfélállapot előzményeinek megtekintéséhez.</span><span class="sxs-lookup"><span data-stu-id="3182a-138">Use the `-All` parameter to see all Configuration Status history.</span></span>

> [!NOTE]
> <span data-ttu-id="3182a-139">Kimeneti kivonatosan csonkítja.</span><span class="sxs-lookup"><span data-stu-id="3182a-139">Output is truncated for brevity.</span></span>

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

## <a name="manage-configuration-documents"></a><span data-ttu-id="3182a-140">Konfigurációs dokumentumok kezelése</span><span class="sxs-lookup"><span data-stu-id="3182a-140">Manage Configuration Documents</span></span>

<span data-ttu-id="3182a-141">Az LCM kezeli a konfigurációt a csomópont révén **konfigurációs dokumentumok**.</span><span class="sxs-lookup"><span data-stu-id="3182a-141">The LCM manages the Configuration of the Node by working with **Configuration Documents**.</span></span> <span data-ttu-id="3182a-142">Ezek a fájlok ".mof" a "C:\Windows\System32\Configuration" könyvtárban találhatók.</span><span class="sxs-lookup"><span data-stu-id="3182a-142">These ".mof" files reside in the "C:\Windows\System32\Configuration" directory.</span></span>

<span data-ttu-id="3182a-143">A PowerShell 5.0 kezdve a [Remove-DSCConfigurationDocument](/powershell/module/PSDesiredStateConfiguration/Remove-DscConfigurationDocument) lehetővé teszi, hogy távolítsa el a ".mof" fájlokat jövőbeli konzisztencia-ellenőrzések leállítani, vagy távolítsa el a konfigurációt, amely rendelkezik a hibákat, amikor a alkalmazni.</span><span class="sxs-lookup"><span data-stu-id="3182a-143">Beginning in PowerShell 5.0 the [Remove-DSCConfigurationDocument](/powershell/module/PSDesiredStateConfiguration/Remove-DscConfigurationDocument) allows you to remove the ".mof" files to stop future consistency checks or remove a Configuration that has errors when applied.</span></span> <span data-ttu-id="3182a-144">A `-Stage` paraméter lehetővé teszi, hogy adja meg, melyik ".mof" fájl el kívánja távolítani.</span><span class="sxs-lookup"><span data-stu-id="3182a-144">The `-Stage` parameter allows you to specify which ".mof" file you want to remove.</span></span>

```powershell
Remove-DSCConfigurationDocument -Stage Current
```

> [!NOTE]
> <span data-ttu-id="3182a-145">A PowerShell 4.0-s, továbbra is távolítsa el a közvetlenül ezek ".mof" a fájlok [Remove-cikk](/powershell/module/microsoft.powershell.management/remove-item).</span><span class="sxs-lookup"><span data-stu-id="3182a-145">In PowerShell 4.0, you can still remove these ".mof" files directly using [Remove-Item](/powershell/module/microsoft.powershell.management/remove-item).</span></span>

## <a name="publish-configurations"></a><span data-ttu-id="3182a-146">Konfigurációk közzététele</span><span class="sxs-lookup"><span data-stu-id="3182a-146">Publish Configurations</span></span>

<span data-ttu-id="3182a-147">A PowerShell 5.0-, kezdve a [Publish-DSCConfiguration](/powershell/module/PSDesiredStateConfiguration/Publish-DscConfiguration) parancsmag lett hozzáadva.</span><span class="sxs-lookup"><span data-stu-id="3182a-147">Beginning in PowerShell 5.0, the [Publish-DSCConfiguration](/powershell/module/PSDesiredStateConfiguration/Publish-DscConfiguration) cmdlet was added.</span></span> <span data-ttu-id="3182a-148">Ez a parancsmag lehetővé teszi a távoli számítógépek egy ".mof" fájl közzététele alkalmazása nélkül.</span><span class="sxs-lookup"><span data-stu-id="3182a-148">This cmdlet allows you to publish a ".mof" file to remote computers, without applying it.</span></span>

```powershell
Publish-DscConfiguration -Path '$home\WebServer' -ComputerName "ContosoWebServer" -Credential (get-credential Contoso\webadministrator)
```

## <a name="see-also"></a><span data-ttu-id="3182a-149">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="3182a-149">See also</span></span>

- [<span data-ttu-id="3182a-150">GET, tesztelési, és állítsa be</span><span class="sxs-lookup"><span data-stu-id="3182a-150">Get, Test, and Set</span></span>](../resources/get-test-set.md)
