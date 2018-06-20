---
ms.date: 06/12/2017
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: A DSC-konfigurációk
ms.openlocfilehash: d98bf0e85c12103d9b1eeded155bab1af364bd4c
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/16/2018
ms.locfileid: "34188445"
---
# <a name="dsc-configurations"></a><span data-ttu-id="6c9c4-103">A DSC-konfigurációk</span><span class="sxs-lookup"><span data-stu-id="6c9c4-103">DSC Configurations</span></span>

><span data-ttu-id="6c9c4-104">Vonatkozik: A Windows PowerShell 4.0-s verzióját, a Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="6c9c4-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="6c9c4-105">A DSC-konfigurációk olyan PowerShell-parancsfájlok, amelyek meghatározzák a függvény futásakor.</span><span class="sxs-lookup"><span data-stu-id="6c9c4-105">DSC configurations are PowerShell scripts that define a special type of function.</span></span>
<span data-ttu-id="6c9c4-106">A konfiguráció megadásához használja a PowerShell kulcsszó **konfigurációs**.</span><span class="sxs-lookup"><span data-stu-id="6c9c4-106">To define a configuration, you use the PowerShell keyword **Configuration**.</span></span>

```powershell
Configuration MyDscConfiguration {

    Node "TEST-PC1" {
        WindowsFeature MyFeatureInstance {
            Ensure = "Present"
            Name =  "RSAT"
        }
        WindowsFeature My2ndFeatureInstance {
            Ensure = "Present"
            Name = "Bitlocker"
        }
    }
}
MyDscConfiguration

```

<span data-ttu-id="6c9c4-107">Mentse a parancsfájlt egy .ps1 fájlba.</span><span class="sxs-lookup"><span data-stu-id="6c9c4-107">Save the script as a .ps1 file.</span></span>

## <a name="configuration-syntax"></a><span data-ttu-id="6c9c4-108">Konfigurációs szintaxis</span><span class="sxs-lookup"><span data-stu-id="6c9c4-108">Configuration syntax</span></span>

<span data-ttu-id="6c9c4-109">Egy konfigurációs parancsfájl a következő részből áll:</span><span class="sxs-lookup"><span data-stu-id="6c9c4-109">A configuration script consists of the following parts:</span></span>

- <span data-ttu-id="6c9c4-110">A **konfigurációs** blokkot.</span><span class="sxs-lookup"><span data-stu-id="6c9c4-110">The **Configuration** block.</span></span> <span data-ttu-id="6c9c4-111">Ez egy, a legkülső parancsprogram-blokkot tartalmazzon.</span><span class="sxs-lookup"><span data-stu-id="6c9c4-111">This is the outermost script block.</span></span> <span data-ttu-id="6c9c4-112">Segítségével meghatározhatja a **konfigurációs** kulcsszó és megadása.</span><span class="sxs-lookup"><span data-stu-id="6c9c4-112">You define it by using the **Configuration** keyword and providing a name.</span></span> <span data-ttu-id="6c9c4-113">Ebben az esetben a konfiguráció neve nem "MyDscConfiguration".</span><span class="sxs-lookup"><span data-stu-id="6c9c4-113">In this case, the name of the configuration is "MyDscConfiguration".</span></span>
- <span data-ttu-id="6c9c4-114">Egy vagy több **csomópont** blokkolja.</span><span class="sxs-lookup"><span data-stu-id="6c9c4-114">One or more **Node** blocks.</span></span> <span data-ttu-id="6c9c4-115">Ezek határozzák meg a konfigurálni kívánt csomópontok (számítógépek és virtuális gépeken).</span><span class="sxs-lookup"><span data-stu-id="6c9c4-115">These define the nodes (computers or VMs) that you are configuring.</span></span> <span data-ttu-id="6c9c4-116">A fenti konfigurációban van egy **csomópont** blokkot, amelynek célpontja a számítógép neve a "TEST-PC1".</span><span class="sxs-lookup"><span data-stu-id="6c9c4-116">In the above configuration, there is one **Node** block that targets a computer named "TEST-PC1".</span></span>
- <span data-ttu-id="6c9c4-117">Egy vagy több erőforrás-címblokkokat.</span><span class="sxs-lookup"><span data-stu-id="6c9c4-117">One or more resource blocks.</span></span> <span data-ttu-id="6c9c4-118">Ez azért, ahol a konfigurációt az erőforrásokat, amelyek azt konfigurálja tulajdonságainak beállítása.</span><span class="sxs-lookup"><span data-stu-id="6c9c4-118">This is where the configuration sets the properties for the resources that it is configuring.</span></span> <span data-ttu-id="6c9c4-119">Ebben az esetben két erőforrás-blokk, a "WindowsFeature" erőforrás hívható, amelyek nincsenek.</span><span class="sxs-lookup"><span data-stu-id="6c9c4-119">In this case, there are two resource blocks, each of which call the "WindowsFeature" resource.</span></span>

<span data-ttu-id="6c9c4-120">Belül egy **konfigurációs** blokk, akkor is végrehajthat, amelyek általában egy PowerShell-függvény sikertelen.</span><span class="sxs-lookup"><span data-stu-id="6c9c4-120">Within a **Configuration** block, you can do anything that you normally could in a PowerShell function.</span></span> <span data-ttu-id="6c9c4-121">Például az előző példában, ha nem szeretné a nevét, a konfigurációban, a célszámítógép merevlemez code hozzáadhat egy paraméter, a csomópont neve:</span><span class="sxs-lookup"><span data-stu-id="6c9c4-121">For example, in the previous example, if you didn't want to hard code the name of the target computer in the configuration, you could add a parameter for the node name:</span></span>

```powershell
Configuration MyDscConfiguration {

    param(
        [string[]]$ComputerName="localhost"
    )
    Node $ComputerName {
        WindowsFeature MyFeatureInstance {
            Ensure = "Present"
            Name =  "RSAT"
        }
        WindowsFeature My2ndFeatureInstance {
            Ensure = "Present"
            Name = "Bitlocker"
        }
    }
}
MyDscConfiguration -ComputerName $ComputerName

```

<span data-ttu-id="6c9c4-122">Ebben a példában, akkor adja meg a csomópont neve úgy, hogy azt a **számítógépnév** paramétert, ha a konfiguráció fordítása.</span><span class="sxs-lookup"><span data-stu-id="6c9c4-122">In this example, you specify the name of the node by passing it as the **ComputerName** parameter when you compile the configuration.</span></span> <span data-ttu-id="6c9c4-123">A név az alapértelmezett érték "localhost".</span><span class="sxs-lookup"><span data-stu-id="6c9c4-123">The name defaults to "localhost".</span></span>

## <a name="compiling-the-configuration"></a><span data-ttu-id="6c9c4-124">A konfiguráció fordítása</span><span class="sxs-lookup"><span data-stu-id="6c9c4-124">Compiling the configuration</span></span>

<span data-ttu-id="6c9c4-125">Egy konfigurációs is kihirdeti, mielőtt, hogy a MOF-dokumentumba van.</span><span class="sxs-lookup"><span data-stu-id="6c9c4-125">Before you can enact a configuration, you have to compile it into a MOF document.</span></span>
<span data-ttu-id="6c9c4-126">Ehhez a konfigurációs hívja, például akkor hívja meg a PowerShell függvényt.</span><span class="sxs-lookup"><span data-stu-id="6c9c4-126">You do this by calling the configuration like you would call a PowerShell function.</span></span>
<span data-ttu-id="6c9c4-127">A példában csak a konfiguráció nevét tartalmazó utolsó sora meghívja a konfiguráció.</span><span class="sxs-lookup"><span data-stu-id="6c9c4-127">The last line of the example containing only the name of the configuration, calls the configuration.</span></span>

><span data-ttu-id="6c9c4-128">**Megjegyzés:** hívni egy konfigurációt, a függvény hatókörében kell lennie globális (úgy, mint bármely más PowerShell függvény).</span><span class="sxs-lookup"><span data-stu-id="6c9c4-128">**Note:** To call a configuration, the function must be in global scope (as with any other PowerShell function).</span></span>
><span data-ttu-id="6c9c4-129">A hiba akkor fordulhat elő vagy az "rögzítési" a parancsfájlt, hogy vagy a konfigurációs parancsfájl futtatásával F5 használatával, vagy kattintson a a **-parancsfájl futtatása** az ISE gombjára.</span><span class="sxs-lookup"><span data-stu-id="6c9c4-129">You can make this happen either by "dot-sourcing" the script, or by running the configuration script by using F5 or clicking on the **Run Script** button in the ISE.</span></span>
><span data-ttu-id="6c9c4-130">A parancsfájl pont-forrás, futtassa a parancsot `. .\myConfig.ps1` ahol `myConfig.ps1` a parancsfájlt, amely tartalmazza a konfiguráció neve.</span><span class="sxs-lookup"><span data-stu-id="6c9c4-130">To dot-source the script, run the command `. .\myConfig.ps1` where `myConfig.ps1` is the name of the script file that contains your configuration.</span></span>

<span data-ttu-id="6c9c4-131">A konfigurációs hívásakor azt:</span><span class="sxs-lookup"><span data-stu-id="6c9c4-131">When you call the configuration, it:</span></span>

- <span data-ttu-id="6c9c4-132">Oldja fel az összes változó</span><span class="sxs-lookup"><span data-stu-id="6c9c4-132">Resolves all variables</span></span>
- <span data-ttu-id="6c9c4-133">Létrejön egy mappa neve megegyezik a konfiguráció az aktuális könyvtár.</span><span class="sxs-lookup"><span data-stu-id="6c9c4-133">Creates a folder in the current directory with the same name as the configuration.</span></span>
- <span data-ttu-id="6c9c4-134">Létrehoz egy nevű fájlt _csomópontnév_.mof új könyvtárban, ahol _csomópontnév_ a célcsomópont a konfiguráció neve.</span><span class="sxs-lookup"><span data-stu-id="6c9c4-134">Creates a file named _NodeName_.mof in the new directory, where _NodeName_ is the name of the target node of the configuration.</span></span>
    <span data-ttu-id="6c9c4-135">Ha egynél több csomópont, a MOF-fájlt az egyes csomópontok létrejön.</span><span class="sxs-lookup"><span data-stu-id="6c9c4-135">If there are more than one nodes, a MOF file will be created for each node.</span></span>

><span data-ttu-id="6c9c4-136">**Megjegyzés:**: A MOF-fájl tartalmazza az összes célcsomóponton vonatkozó konfigurációs adatokat.</span><span class="sxs-lookup"><span data-stu-id="6c9c4-136">**Note**: The MOF file contains all of the configuration information for the target node.</span></span> <span data-ttu-id="6c9c4-137">Ezért fontos biztonságának megőrzése.</span><span class="sxs-lookup"><span data-stu-id="6c9c4-137">Because of this, it’s important to keep it secure.</span></span>
><span data-ttu-id="6c9c4-138">További információkért lásd: [biztonságossá tétele a MOF-fájlt](secureMOF.md).</span><span class="sxs-lookup"><span data-stu-id="6c9c4-138">For more information, see [Securing the MOF file](secureMOF.md).</span></span>

<span data-ttu-id="6c9c4-139">A következő gyökérmappa-szerkezetében lévő eredmények felett első konfiguráció fordítása:</span><span class="sxs-lookup"><span data-stu-id="6c9c4-139">Compiling the first configuration above results in the following folder structure:</span></span>

```powershell
. .\MyDscConfiguration.ps1
MyDscConfiguration
```

```
    Directory: C:\users\default\Documents\DSC Configurations\MyDscConfiguration
Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----       10/23/2015   4:32 PM           2842 localhost.mof
```

<span data-ttu-id="6c9c4-140">Ha a konfigurációs paramétert egy, a második példában látható módon, amelynek meg kell adni a fordítás során.</span><span class="sxs-lookup"><span data-stu-id="6c9c4-140">If the configuration takes a parameter, as in the second example, that has to be provided at compile time.</span></span> <span data-ttu-id="6c9c4-141">Hogyan lenne, amely itt található:</span><span class="sxs-lookup"><span data-stu-id="6c9c4-141">Here's how that would look:</span></span>

```powershell
. .\MyDscConfiguration.ps1
MyDscConfiguration -ComputerName 'MyTestNode'
```

```
    Directory: C:\users\default\Documents\DSC Configurations\MyDscConfiguration
Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----       10/23/2015   4:32 PM           2842 MyTestNode.mof
```

## <a name="using-dependson"></a><span data-ttu-id="6c9c4-142">DependsOn tulajdonság használatával</span><span class="sxs-lookup"><span data-stu-id="6c9c4-142">Using DependsOn</span></span>

<span data-ttu-id="6c9c4-143">A hasznos DSC kulcsszót **DependsOn**.</span><span class="sxs-lookup"><span data-stu-id="6c9c4-143">A useful DSC keyword is **DependsOn**.</span></span> <span data-ttu-id="6c9c4-144">Általában (azonban nem feltétlenül mindig), DSC alkalmazza a megjelenési sorrendjükben belül a konfigurációs lévő erőforrásokat.</span><span class="sxs-lookup"><span data-stu-id="6c9c4-144">Typically (though not necessarily always), DSC applies the resources in the order that they appear within the configuration.</span></span>
<span data-ttu-id="6c9c4-145">Azonban **DependsOn** Megadja, hogy erőforrások más erőforrások függenek, és a LCM biztosítja, hogy lesznek alkalmazva a megfelelő sorrendben, függetlenül attól, amelyben az erőforrások példányok meghatározásának sorrendje.</span><span class="sxs-lookup"><span data-stu-id="6c9c4-145">However, **DependsOn** specifies which resources depend on other resources, and the LCM ensures that they are applied in the correct order, regardless of the order in which resource instances are defined.</span></span>
<span data-ttu-id="6c9c4-146">Például egy konfigurációban előfordulhat, hogy adja meg, amely egy példányát a **felhasználói** erőforrás létezik-e függ a **csoport** példány:</span><span class="sxs-lookup"><span data-stu-id="6c9c4-146">For example, a configuration might specify that an instance of the **User** resource depends on the existence of a **Group** instance:</span></span>

```powershell
Configuration DependsOnExample {
    Node Test-PC1 {
        Group GroupExample {
            Ensure = "Present"
            GroupName = "TestGroup"
        }

        User UserExample {
            Ensure = "Present"
            UserName = "TestUser"
            FullName = "TestUser"
            DependsOn = "[Group]GroupExample"
        }
    }
}

```

## <a name="using-new-resources-in-your-configuration"></a><span data-ttu-id="6c9c4-147">A konfiguráció új erőforrások használata</span><span class="sxs-lookup"><span data-stu-id="6c9c4-147">Using new resources in Your configuration</span></span>

<span data-ttu-id="6c9c4-148">Ha az előző példákban futtatta, akkor előfordulhat, hogy észrevette, hogy akkor is figyelmezteti, hogy egy erőforrás használta explicit importálása nélkül.</span><span class="sxs-lookup"><span data-stu-id="6c9c4-148">If you ran the previous examples, you might have noticed that you were warned that you were using a resource without explicitly importing it.</span></span>
<span data-ttu-id="6c9c4-149">A DSC ma, 12-erőforrásokkal érhető el, a PSDesiredStateConfiguration modulja részét.</span><span class="sxs-lookup"><span data-stu-id="6c9c4-149">Today, DSC ships with 12 resources as part of the PSDesiredStateConfiguration module.</span></span>
<span data-ttu-id="6c9c4-150">Egyéb erőforrások külső modulban kell helyezni `$env:PSModulePath` ahhoz, hogy ismeri fel a LCM.</span><span class="sxs-lookup"><span data-stu-id="6c9c4-150">Other resources in external modules must be placed in `$env:PSModulePath` in order to be recognized by the LCM.</span></span>
<span data-ttu-id="6c9c4-151">Egy új parancsmagot [Get-DscResource](https://technet.microsoft.com/library/dn521625.aspx), annak meghatározására, hogy milyen erőforrásokat telepítve a rendszeren, és használható a LCM által használható.</span><span class="sxs-lookup"><span data-stu-id="6c9c4-151">A new cmdlet, [Get-DscResource](https://technet.microsoft.com/library/dn521625.aspx), can be used to determine what resources are installed on the system and available for use by the LCM.</span></span>
<span data-ttu-id="6c9c4-152">Ha ezek a modulok lettek helyezve `$env:PSModulePath` megfelelően ismeri fel és [Get-DscResource](https://technet.microsoft.com/library/dn521625.aspx), betöltését belül a konfigurációs továbbra is szükséges.</span><span class="sxs-lookup"><span data-stu-id="6c9c4-152">Once these modules have been placed in `$env:PSModulePath` and are properly recognized by [Get-DscResource](https://technet.microsoft.com/library/dn521625.aspx), they still need to be loaded within your configuration.</span></span>
<span data-ttu-id="6c9c4-153">**Import-DscResource** belül csak érzékelt dinamikus kulcsszó egy **konfigurációs** blokk (azaz nincs parancsmag).</span><span class="sxs-lookup"><span data-stu-id="6c9c4-153">**Import-DscResource** is a dynamic keyword that can only be recognized within a **Configuration** block (i.e. it is not a cmdlet).</span></span>
<span data-ttu-id="6c9c4-154">**Importálás – DscResource** két paramétereket támogatja:</span><span class="sxs-lookup"><span data-stu-id="6c9c4-154">**Import-DscResource** supports two parameters:</span></span>
- <span data-ttu-id="6c9c4-155">**Modulnév** használatának ajánlott módja **Import-DscResource**.</span><span class="sxs-lookup"><span data-stu-id="6c9c4-155">**ModuleName** is the recommended way of using **Import-DscResource**.</span></span> <span data-ttu-id="6c9c4-156">A modul, amely tartalmazza az erőforrásokat, importálandók (valamint a karakterlánc tömbje modulneveket) neve fogad.</span><span class="sxs-lookup"><span data-stu-id="6c9c4-156">It accepts the name of the module that contains the resources to be imported (as well as a string array of module names).</span></span>
- <span data-ttu-id="6c9c4-157">**Név** neve, az erőforrás importálásához.</span><span class="sxs-lookup"><span data-stu-id="6c9c4-157">**Name** is the name of the resource to import.</span></span> <span data-ttu-id="6c9c4-158">Ez nem a rövid név, mint a "Name" által visszaadott [Get-DscResource](https://technet.microsoft.com/library/dn521625.aspx), de az osztály nevét, ha használt meghatározása az erőforrás-séma (adja vissza a **ResourceType** által [Get-DscResource](https://technet.microsoft.com/library/dn521625.aspx)).</span><span class="sxs-lookup"><span data-stu-id="6c9c4-158">This is not the friendly name returned as "Name" by [Get-DscResource](https://technet.microsoft.com/library/dn521625.aspx), but the class name used when defining the resource schema (returned as **ResourceType** by [Get-DscResource](https://technet.microsoft.com/library/dn521625.aspx)).</span></span>

## <a name="see-also"></a><span data-ttu-id="6c9c4-159">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="6c9c4-159">See Also</span></span>
* [<span data-ttu-id="6c9c4-160">A Windows PowerShell célállapot-konfiguráló áttekintése</span><span class="sxs-lookup"><span data-stu-id="6c9c4-160">Windows PowerShell Desired State Configuration Overview</span></span>](overview.md)
* [<span data-ttu-id="6c9c4-161">A DSC-erőforrások</span><span class="sxs-lookup"><span data-stu-id="6c9c4-161">DSC Resources</span></span>](resources.md)
* [<span data-ttu-id="6c9c4-162">A helyi Configuration Manager konfigurálása</span><span class="sxs-lookup"><span data-stu-id="6c9c4-162">Configuring The Local Configuration Manager</span></span>](metaConfig.md)
