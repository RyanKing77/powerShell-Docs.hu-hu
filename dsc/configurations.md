---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: DSC-konfigurációk
ms.openlocfilehash: 171068acb51f44e31c81e63f6640222ef71bee38
ms.sourcegitcommit: 77f62a55cac8c13d69d51eef5fade18f71d66955
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/17/2018
ms.locfileid: "39093694"
---
# <a name="dsc-configurations"></a><span data-ttu-id="6ea26-103">DSC-konfigurációk</span><span class="sxs-lookup"><span data-stu-id="6ea26-103">DSC Configurations</span></span>

> <span data-ttu-id="6ea26-104">A következőkre vonatkozik: Windows PowerShell 4.0-s, a Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="6ea26-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="6ea26-105">DSC-konfigurációk a következők PowerShell-parancsfájlok, amelyek meghatározzák egy speciális típusú függvény.</span><span class="sxs-lookup"><span data-stu-id="6ea26-105">DSC configurations are PowerShell scripts that define a special type of function.</span></span>
<span data-ttu-id="6ea26-106">Konfiguráció megadásához használja a PowerShell kulcsszó **konfigurációs**.</span><span class="sxs-lookup"><span data-stu-id="6ea26-106">To define a configuration, you use the PowerShell keyword **Configuration**.</span></span>

```powershell
Configuration MyDscConfiguration {
    Node "TEST-PC1" {
        WindowsFeature MyFeatureInstance {
            Ensure = 'Present'
            Name = 'RSAT'
        }
        WindowsFeature My2ndFeatureInstance {
            Ensure = 'Present'
            Name = 'Bitlocker'
        }
    }
}
MyDscConfiguration
```

<span data-ttu-id="6ea26-107">Mentse a parancsfájlt egy .ps1 fájlba.</span><span class="sxs-lookup"><span data-stu-id="6ea26-107">Save the script as a .ps1 file.</span></span>

## <a name="configuration-syntax"></a><span data-ttu-id="6ea26-108">Konfigurációs szintaxis</span><span class="sxs-lookup"><span data-stu-id="6ea26-108">Configuration syntax</span></span>

<span data-ttu-id="6ea26-109">A konfigurációs parancsfájlt a következő részekből áll:</span><span class="sxs-lookup"><span data-stu-id="6ea26-109">A configuration script consists of the following parts:</span></span>

- <span data-ttu-id="6ea26-110">A **konfigurációs** letiltása.</span><span class="sxs-lookup"><span data-stu-id="6ea26-110">The **Configuration** block.</span></span> <span data-ttu-id="6ea26-111">Ez az a legkülső parancsfájlblokkban.</span><span class="sxs-lookup"><span data-stu-id="6ea26-111">This is the outermost script block.</span></span> <span data-ttu-id="6ea26-112">Segítségével meghatározhatja a **konfigurációs** kulcsszó és a egy nevet.</span><span class="sxs-lookup"><span data-stu-id="6ea26-112">You define it by using the **Configuration** keyword and providing a name.</span></span> <span data-ttu-id="6ea26-113">Ebben az esetben a konfiguráció név "MyDscConfiguration".</span><span class="sxs-lookup"><span data-stu-id="6ea26-113">In this case, the name of the configuration is "MyDscConfiguration".</span></span>
- <span data-ttu-id="6ea26-114">Egy vagy több **csomópont** blokkokat.</span><span class="sxs-lookup"><span data-stu-id="6ea26-114">One or more **Node** blocks.</span></span> <span data-ttu-id="6ea26-115">Ezek adják meg a konfigurálni kívánt csomópont (számítógép vagy virtuális gépeken).</span><span class="sxs-lookup"><span data-stu-id="6ea26-115">These define the nodes (computers or VMs) that you are configuring.</span></span> <span data-ttu-id="6ea26-116">A fenti konfigurációban van egy **csomópont** egy számítógépet célzó letiltása a "TEST-PC1" nevű.</span><span class="sxs-lookup"><span data-stu-id="6ea26-116">In the above configuration, there is one **Node** block that targets a computer named "TEST-PC1".</span></span>
- <span data-ttu-id="6ea26-117">Egy vagy több erőforrás blokkokat.</span><span class="sxs-lookup"><span data-stu-id="6ea26-117">One or more resource blocks.</span></span> <span data-ttu-id="6ea26-118">Ez az, ahol a konfiguráció az erőforrásokat, konfiguráló tulajdonságainak beállítása.</span><span class="sxs-lookup"><span data-stu-id="6ea26-118">This is where the configuration sets the properties for the resources that it is configuring.</span></span> <span data-ttu-id="6ea26-119">Ebben az esetben két erőforrás blokkok, amelyek a "WindowsFeature" erőforrás hívása vannak.</span><span class="sxs-lookup"><span data-stu-id="6ea26-119">In this case, there are two resource blocks, each of which call the "WindowsFeature" resource.</span></span>

<span data-ttu-id="6ea26-120">Belül egy **konfigurációs** letiltása, akkor is végrehajthat, amely általában egy PowerShell-függvény sikerült.</span><span class="sxs-lookup"><span data-stu-id="6ea26-120">Within a **Configuration** block, you can do anything that you normally could in a PowerShell function.</span></span> <span data-ttu-id="6ea26-121">Például az előző példában, ha nem szeretné a konfigurációban a célszámítógép nevét keményen code hozzáadhat egy paramétert a csomópont nevét:</span><span class="sxs-lookup"><span data-stu-id="6ea26-121">For example, in the previous example, if you didn't want to hard code the name of the target computer in the configuration, you could add a parameter for the node name:</span></span>

```powershell
Configuration MyDscConfiguration {
    param(
        [string[]]$ComputerName='localhost'
    )
    Node $ComputerName {
        WindowsFeature MyFeatureInstance {
            Ensure = 'Present'
            Name = 'RSAT'
        }
        WindowsFeature My2ndFeatureInstance {
            Ensure = 'Present'
            Name = 'Bitlocker'
        }
    }
}
MyDscConfiguration -ComputerName $ComputerName
```

<span data-ttu-id="6ea26-122">Ebben a példában átadásával, megadhatja a csomópont nevét a **ComputerName** konfiguráció fordítása paramétert.</span><span class="sxs-lookup"><span data-stu-id="6ea26-122">In this example, you specify the name of the node by passing it as the **ComputerName** parameter when you compile the configuration.</span></span> <span data-ttu-id="6ea26-123">A név az alapértelmezett érték "localhost".</span><span class="sxs-lookup"><span data-stu-id="6ea26-123">The name defaults to "localhost".</span></span>

## <a name="compiling-the-configuration"></a><span data-ttu-id="6ea26-124">A konfiguráció fordítása</span><span class="sxs-lookup"><span data-stu-id="6ea26-124">Compiling the configuration</span></span>

<span data-ttu-id="6ea26-125">A konfiguráció is kihirdeti, mielőtt rendelkezik, hogy a MOF-dokumentumba.</span><span class="sxs-lookup"><span data-stu-id="6ea26-125">Before you can enact a configuration, you have to compile it into a MOF document.</span></span>
<span data-ttu-id="6ea26-126">Ehhez a konfigurációs meghívásával, például egy PowerShell függvény akkor hívható meg.</span><span class="sxs-lookup"><span data-stu-id="6ea26-126">You do this by calling the configuration like you would call a PowerShell function.</span></span>
<span data-ttu-id="6ea26-127">A példában csak a konfiguráció nevét tartalmazó utolsó sora meghívja a konfigurációt.</span><span class="sxs-lookup"><span data-stu-id="6ea26-127">The last line of the example containing only the name of the configuration, calls the configuration.</span></span>

> [!NOTE]
> <span data-ttu-id="6ea26-128">Szeretne hívásokat indítani olyan konfiguráció, a függvény kell globális hatókör (csakúgy, mint bármely más PowerShell függvény).</span><span class="sxs-lookup"><span data-stu-id="6ea26-128">To call a configuration, the function must be in global scope (as with any other PowerShell function).</span></span>
> <span data-ttu-id="6ea26-129">Meghatározhat, ez történik vagy a "rögzítési művelet" a parancsfájl vagy a konfigurációs parancsprogram futtatásával az F5 billentyűvel, vagy kattintson a a **parancsfájl futtatása** gomb az ISE-ben.</span><span class="sxs-lookup"><span data-stu-id="6ea26-129">You can make this happen either by "dot-sourcing" the script, or by running the configuration script by using F5 or clicking on the **Run Script** button in the ISE.</span></span>
> <span data-ttu-id="6ea26-130">Pont – forrás a parancsfájlt, futtassa a parancsot `. .\myConfig.ps1` ahol `myConfig.ps1` a parancsfájl, amely tartalmazza a konfiguráció neve.</span><span class="sxs-lookup"><span data-stu-id="6ea26-130">To dot-source the script, run the command `. .\myConfig.ps1` where `myConfig.ps1` is the name of the script file that contains your configuration.</span></span>

<span data-ttu-id="6ea26-131">A konfiguráció, hívja ezt:</span><span class="sxs-lookup"><span data-stu-id="6ea26-131">When you call the configuration, it:</span></span>

- <span data-ttu-id="6ea26-132">Oldja fel az összes változót</span><span class="sxs-lookup"><span data-stu-id="6ea26-132">Resolves all variables</span></span>
- <span data-ttu-id="6ea26-133">Létrehoz egy mappát a neve megegyezik a konfiguráció az aktuális könyvtárban található.</span><span class="sxs-lookup"><span data-stu-id="6ea26-133">Creates a folder in the current directory with the same name as the configuration.</span></span>
- <span data-ttu-id="6ea26-134">Létrehoz egy fájlt _csomópontnév_.mof az új címtárban, ahol _csomópontnév_ a célcsomópont a konfiguráció neve.</span><span class="sxs-lookup"><span data-stu-id="6ea26-134">Creates a file named _NodeName_.mof in the new directory, where _NodeName_ is the name of the target node of the configuration.</span></span>
  <span data-ttu-id="6ea26-135">Ha egynél több csomópont, a MOF-fájlt az egyes csomópontok létrejön.</span><span class="sxs-lookup"><span data-stu-id="6ea26-135">If there are more than one nodes, a MOF file will be created for each node.</span></span>

> [!NOTE]
> <span data-ttu-id="6ea26-136">A MOF-fájl összes a célcsomópont konfigurációs adatait tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="6ea26-136">The MOF file contains all of the configuration information for the target node.</span></span> <span data-ttu-id="6ea26-137">Emiatt fontos tárolja biztonságos helyen.</span><span class="sxs-lookup"><span data-stu-id="6ea26-137">Because of this, it’s important to keep it secure.</span></span>
> <span data-ttu-id="6ea26-138">További információkért lásd: [a MOF-fájl biztonságossá tétele](secureMOF.md).</span><span class="sxs-lookup"><span data-stu-id="6ea26-138">For more information, see [Securing the MOF file](secureMOF.md).</span></span>

<span data-ttu-id="6ea26-139">A fenti eredmények a következő gyökérmappa-szerkezetében lévő első konfiguráció fordítása:</span><span class="sxs-lookup"><span data-stu-id="6ea26-139">Compiling the first configuration above results in the following folder structure:</span></span>

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

<span data-ttu-id="6ea26-140">Ha a konfigurációs paramétert egy, a második példában látható módon, amely rendelkezik a fordítás során meg kell adni.</span><span class="sxs-lookup"><span data-stu-id="6ea26-140">If the configuration takes a parameter, as in the second example, that has to be provided at compile time.</span></span> <span data-ttu-id="6ea26-141">Itt látható, hogyan néz:</span><span class="sxs-lookup"><span data-stu-id="6ea26-141">Here's how that would look:</span></span>

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

## <a name="using-dependson"></a><span data-ttu-id="6ea26-142">DependsOn használatával</span><span class="sxs-lookup"><span data-stu-id="6ea26-142">Using DependsOn</span></span>

<span data-ttu-id="6ea26-143">Egy hasznos DSC kulcsszó **DependsOn**.</span><span class="sxs-lookup"><span data-stu-id="6ea26-143">A useful DSC keyword is **DependsOn**.</span></span> <span data-ttu-id="6ea26-144">Általában (bár nem feltétlenül mindig), DSC vonatkozik a sorrendben jelennek meg a konfigurációs belül az erőforrásokat.</span><span class="sxs-lookup"><span data-stu-id="6ea26-144">Typically (though not necessarily always), DSC applies the resources in the order that they appear within the configuration.</span></span>
<span data-ttu-id="6ea26-145">Azonban **DependsOn** Megadja, hogy erőforrások más erőforrások függenek, és az LCM Konfigurálása biztosítja, hogy a megfelelő sorrendben, függetlenül az erőforrás-példányok meghatározott sorrendben adják.</span><span class="sxs-lookup"><span data-stu-id="6ea26-145">However, **DependsOn** specifies which resources depend on other resources, and the LCM ensures that they are applied in the correct order, regardless of the order in which resource instances are defined.</span></span>
<span data-ttu-id="6ea26-146">Például egy konfigurációs előfordulhat, hogy adja meg, amely egy példányát a **felhasználói** erőforrás függ, hogy létezik-e egy **csoport** példány:</span><span class="sxs-lookup"><span data-stu-id="6ea26-146">For example, a configuration might specify that an instance of the **User** resource depends on the existence of a **Group** instance:</span></span>

```powershell
Configuration DependsOnExample {
    Node Test-PC1 {
        Group GroupExample {
            Ensure = 'Present'
            GroupName = 'TestGroup'
        }

        User UserExample {
            Ensure = 'Present'
            UserName = 'TestUser'
            FullName = 'TestUser'
            DependsOn = '[Group]GroupExample'
        }
    }
}
```

## <a name="using-new-resources-in-your-configuration"></a><span data-ttu-id="6ea26-147">A konfiguráció új erőforrások használata</span><span class="sxs-lookup"><span data-stu-id="6ea26-147">Using new resources in Your configuration</span></span>

<span data-ttu-id="6ea26-148">Ha az előző példák futtatta, talán észrevette, hogy akkor is figyelmezteti, hogy explicit módon importálása nélkül erőforrás használja.</span><span class="sxs-lookup"><span data-stu-id="6ea26-148">If you ran the previous examples, you might have noticed that you were warned that you were using a resource without explicitly importing it.</span></span>
<span data-ttu-id="6ea26-149">Még ma DSC tartalmaz 12 erőforrás jelenik meg a PSDesiredStateConfiguration modul részeként.</span><span class="sxs-lookup"><span data-stu-id="6ea26-149">Today, DSC ships with 12 resources as part of the PSDesiredStateConfiguration module.</span></span>
<span data-ttu-id="6ea26-150">Külső modulok egyéb erőforrásokat kell helyezni `$env:PSModulePath` annak érdekében, hogy ismeri fel az LCM Konfigurálása.</span><span class="sxs-lookup"><span data-stu-id="6ea26-150">Other resources in external modules must be placed in `$env:PSModulePath` in order to be recognized by the LCM.</span></span>
<span data-ttu-id="6ea26-151">Új parancsmag, [Get-DscResource](https://technet.microsoft.com/library/dn521625.aspx), annak meghatározására, hogy milyen erőforrásokat telepítve a rendszeren, és használható a LCM által használható.</span><span class="sxs-lookup"><span data-stu-id="6ea26-151">A new cmdlet, [Get-DscResource](https://technet.microsoft.com/library/dn521625.aspx), can be used to determine what resources are installed on the system and available for use by the LCM.</span></span>
<span data-ttu-id="6ea26-152">Ha ezek a modulok lettek helyezve `$env:PSModulePath` és a rendszer megfelelően ismeri fel [Get-DscResource](https://technet.microsoft.com/library/dn521625.aspx), továbbra is szükségük van, nem tölthető be a konfigurációs belül.</span><span class="sxs-lookup"><span data-stu-id="6ea26-152">Once these modules have been placed in `$env:PSModulePath` and are properly recognized by [Get-DscResource](https://technet.microsoft.com/library/dn521625.aspx), they still need to be loaded within your configuration.</span></span>
<span data-ttu-id="6ea26-153">**Az import-DscResource** , amely csak belül felismeri a dinamikus kulcsszó egy **konfigurációs** letiltása (azaz ez még nem parancsmag).</span><span class="sxs-lookup"><span data-stu-id="6ea26-153">**Import-DscResource** is a dynamic keyword that can only be recognized within a **Configuration** block (i.e. it is not a cmdlet).</span></span>
<span data-ttu-id="6ea26-154">**Az import-DscResource** két paramétereket támogatja:</span><span class="sxs-lookup"><span data-stu-id="6ea26-154">**Import-DscResource** supports two parameters:</span></span>

- <span data-ttu-id="6ea26-155">**ModuleName** használatának ajánlott módja **Import-DscResource**.</span><span class="sxs-lookup"><span data-stu-id="6ea26-155">**ModuleName** is the recommended way of using **Import-DscResource**.</span></span> <span data-ttu-id="6ea26-156">A modul (valamint a karakterlánc tömbje modulneveket) importálni erőforrásokat tartalmazó neve fogad el.</span><span class="sxs-lookup"><span data-stu-id="6ea26-156">It accepts the name of the module that contains the resources to be imported (as well as a string array of module names).</span></span>
- <span data-ttu-id="6ea26-157">**Név** neve, az erőforrás importálásához.</span><span class="sxs-lookup"><span data-stu-id="6ea26-157">**Name** is the name of the resource to import.</span></span> <span data-ttu-id="6ea26-158">Ez nem a valódi nevet, mint "Name" által visszaadott [Get-DscResource](https://technet.microsoft.com/library/dn521625.aspx), de az osztály nevét használja, amikor az erőforrás-séma meghatározása (adja vissza a **ResourceType** által [Get-DscResource](https://technet.microsoft.com/library/dn521625.aspx)).</span><span class="sxs-lookup"><span data-stu-id="6ea26-158">This is not the friendly name returned as "Name" by [Get-DscResource](https://technet.microsoft.com/library/dn521625.aspx), but the class name used when defining the resource schema (returned as **ResourceType** by [Get-DscResource](https://technet.microsoft.com/library/dn521625.aspx)).</span></span>

## <a name="see-also"></a><span data-ttu-id="6ea26-159">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="6ea26-159">See Also</span></span>

- [<span data-ttu-id="6ea26-160">Windows PowerShell Desired State Configuration áttekintése</span><span class="sxs-lookup"><span data-stu-id="6ea26-160">Windows PowerShell Desired State Configuration Overview</span></span>](overview.md)
- [<span data-ttu-id="6ea26-161">DSC-erőforrások</span><span class="sxs-lookup"><span data-stu-id="6ea26-161">DSC Resources</span></span>](resources.md)
- [<span data-ttu-id="6ea26-162">A helyi Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="6ea26-162">Configuring The Local Configuration Manager</span></span>](metaConfig.md)