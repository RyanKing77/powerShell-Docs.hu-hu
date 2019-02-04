---
ms.date: 12/12/2018
keywords: DSC, powershell, a konfigurációt, a beállítása
title: DSC-konfigurációk
ms.openlocfilehash: 6af27f442de3080facd65892c713c989d0e388c5
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55684289"
---
# <a name="dsc-configurations"></a><span data-ttu-id="6142a-103">DSC-konfigurációk</span><span class="sxs-lookup"><span data-stu-id="6142a-103">DSC Configurations</span></span>

> <span data-ttu-id="6142a-104">Érvényes: Windows PowerShell 4.0-s, a Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="6142a-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="6142a-105">DSC-konfigurációk a következők PowerShell-parancsfájlok, amelyek meghatározzák egy speciális típusú függvény.</span><span class="sxs-lookup"><span data-stu-id="6142a-105">DSC configurations are PowerShell scripts that define a special type of function.</span></span>
<span data-ttu-id="6142a-106">Konfiguráció megadásához használja a PowerShell kulcsszó **konfigurációs**.</span><span class="sxs-lookup"><span data-stu-id="6142a-106">To define a configuration, you use the PowerShell keyword **Configuration**.</span></span>

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

<span data-ttu-id="6142a-107">Mentse a parancsfájlt, mint egy `.ps1` fájlt.</span><span class="sxs-lookup"><span data-stu-id="6142a-107">Save the script as a `.ps1` file.</span></span>

## <a name="configuration-syntax"></a><span data-ttu-id="6142a-108">Konfigurációs szintaxis</span><span class="sxs-lookup"><span data-stu-id="6142a-108">Configuration syntax</span></span>

<span data-ttu-id="6142a-109">A konfigurációs parancsfájlt a következő részekből áll:</span><span class="sxs-lookup"><span data-stu-id="6142a-109">A configuration script consists of the following parts:</span></span>

- <span data-ttu-id="6142a-110">A **konfigurációs** letiltása.</span><span class="sxs-lookup"><span data-stu-id="6142a-110">The **Configuration** block.</span></span> <span data-ttu-id="6142a-111">Ez az a legkülső parancsfájlblokkban.</span><span class="sxs-lookup"><span data-stu-id="6142a-111">This is the outermost script block.</span></span> <span data-ttu-id="6142a-112">Segítségével meghatározhatja a **konfigurációs** kulcsszó és a egy nevet.</span><span class="sxs-lookup"><span data-stu-id="6142a-112">You define it by using the **Configuration** keyword and providing a name.</span></span> <span data-ttu-id="6142a-113">Ebben az esetben a konfiguráció név "MyDscConfiguration".</span><span class="sxs-lookup"><span data-stu-id="6142a-113">In this case, the name of the configuration is "MyDscConfiguration".</span></span>
- <span data-ttu-id="6142a-114">Egy vagy több **csomópont** blokkokat.</span><span class="sxs-lookup"><span data-stu-id="6142a-114">One or more **Node** blocks.</span></span> <span data-ttu-id="6142a-115">Ezek adják meg a konfigurálni kívánt csomópont (számítógép vagy virtuális gépeken).</span><span class="sxs-lookup"><span data-stu-id="6142a-115">These define the nodes (computers or VMs) that you are configuring.</span></span> <span data-ttu-id="6142a-116">A fenti konfigurációban van egy **csomópont** egy számítógépet célzó letiltása a "TEST-PC1" nevű.</span><span class="sxs-lookup"><span data-stu-id="6142a-116">In the above configuration, there is one **Node** block that targets a computer named "TEST-PC1".</span></span> <span data-ttu-id="6142a-117">A csomópont blokk fogadhat több számítógépnevet.</span><span class="sxs-lookup"><span data-stu-id="6142a-117">The Node block can accept multiple computer names.</span></span>
- <span data-ttu-id="6142a-118">Egy vagy több erőforrás blokkokat.</span><span class="sxs-lookup"><span data-stu-id="6142a-118">One or more resource blocks.</span></span> <span data-ttu-id="6142a-119">Ez az, ahol a konfiguráció az erőforrásokat, konfiguráló tulajdonságainak beállítása.</span><span class="sxs-lookup"><span data-stu-id="6142a-119">This is where the configuration sets the properties for the resources that it is configuring.</span></span> <span data-ttu-id="6142a-120">Ebben az esetben két erőforrás blokkok, amelyek a "WindowsFeature" erőforrás hívása vannak.</span><span class="sxs-lookup"><span data-stu-id="6142a-120">In this case, there are two resource blocks, each of which call the "WindowsFeature" resource.</span></span>

<span data-ttu-id="6142a-121">Belül egy **konfigurációs** letiltása, akkor is végrehajthat, amely általában egy PowerShell-függvény sikerült.</span><span class="sxs-lookup"><span data-stu-id="6142a-121">Within a **Configuration** block, you can do anything that you normally could in a PowerShell function.</span></span> <span data-ttu-id="6142a-122">Például az előző példában, ha nem szeretné a konfigurációban a célszámítógép nevét keményen code hozzáadhat egy paramétert a csomópont nevét:</span><span class="sxs-lookup"><span data-stu-id="6142a-122">For example, in the previous example, if you didn't want to hard code the name of the target computer in the configuration, you could add a parameter for the node name:</span></span>

<span data-ttu-id="6142a-123">Ebben a példában átadásával, megadhatja a csomópont nevét a **ComputerName** konfiguráció fordítása paramétert.</span><span class="sxs-lookup"><span data-stu-id="6142a-123">In this example, you specify the name of the node by passing it as the **ComputerName** parameter when you compile the configuration.</span></span> <span data-ttu-id="6142a-124">A név az alapértelmezett érték "localhost".</span><span class="sxs-lookup"><span data-stu-id="6142a-124">The name defaults to "localhost".</span></span>

```powershell
Configuration MyDscConfiguration
{
    param
    (
        [string[]]$ComputerName='localhost'
    )

    Node $ComputerName
    {
        WindowsFeature MyFeatureInstance
        {
            Ensure = 'Present'
            Name = 'RSAT'
        }

        WindowsFeature My2ndFeatureInstance
        {
            Ensure = 'Present'
            Name = 'Bitlocker'
        }
    }
}

MyDscConfiguration
```

<span data-ttu-id="6142a-125">A **csomópont** blokk is fogadhat több számítógépnevet.</span><span class="sxs-lookup"><span data-stu-id="6142a-125">The **Node** block can also accept multiple computer names.</span></span> <span data-ttu-id="6142a-126">A fenti példában, használhatja a `-ComputerName` paraméter vagy számítógépek közvetlenül pass vesszővel elválasztott listáját a **csomópont** letiltása.</span><span class="sxs-lookup"><span data-stu-id="6142a-126">In the above example, you can either use the `-ComputerName` parameter, or pass a comma-separated list of computers directly to the **Node** block.</span></span>

```powershell
MyDscConfiguration -ComputerName "localhost", "Server01"
```

<span data-ttu-id="6142a-127">A számítógépek listáját megadásakor a **csomópont** letiltása, a konfigurációt, belül kell használnia tömb-jelöléssel.</span><span class="sxs-lookup"><span data-stu-id="6142a-127">When specifying a list of computers to the **Node** block, from within a Configuration, you need to use array-notation.</span></span>

```powershell
Configuration MyDscConfiguration
{
    Node @('localhost', 'Server01')
    {
        WindowsFeature MyFeatureInstance
        {
            Ensure = 'Present'
            Name = 'RSAT'
        }

        WindowsFeature My2ndFeatureInstance
        {
            Ensure = 'Present'
            Name = 'Bitlocker'
        }
    }
}

MyDscConfiguration
```

## <a name="compiling-the-configuration"></a><span data-ttu-id="6142a-128">A konfiguráció fordítása</span><span class="sxs-lookup"><span data-stu-id="6142a-128">Compiling the configuration</span></span>

<span data-ttu-id="6142a-129">A konfiguráció is kihirdeti, mielőtt rendelkezik, hogy a MOF-dokumentumba.</span><span class="sxs-lookup"><span data-stu-id="6142a-129">Before you can enact a configuration, you have to compile it into a MOF document.</span></span>
<span data-ttu-id="6142a-130">Ehhez a konfigurációs meghívásával, például egy PowerShell függvény akkor hívható meg.</span><span class="sxs-lookup"><span data-stu-id="6142a-130">You do this by calling the configuration like you would call a PowerShell function.</span></span>
<span data-ttu-id="6142a-131">A példában csak a konfiguráció nevét tartalmazó utolsó sora meghívja a konfigurációt.</span><span class="sxs-lookup"><span data-stu-id="6142a-131">The last line of the example containing only the name of the configuration, calls the configuration.</span></span>

> [!NOTE]
> <span data-ttu-id="6142a-132">Szeretne hívásokat indítani olyan konfiguráció, a függvény kell globális hatókör (csakúgy, mint bármely más PowerShell függvény).</span><span class="sxs-lookup"><span data-stu-id="6142a-132">To call a configuration, the function must be in global scope (as with any other PowerShell function).</span></span>
> <span data-ttu-id="6142a-133">Meghatározhat, ez történik vagy a "rögzítési művelet" a parancsfájl vagy a konfigurációs parancsprogram futtatásával az F5 billentyűvel, vagy kattintson a a **parancsfájl futtatása** gomb az ISE-ben.</span><span class="sxs-lookup"><span data-stu-id="6142a-133">You can make this happen either by "dot-sourcing" the script, or by running the configuration script by using F5 or clicking on the **Run Script** button in the ISE.</span></span>
> <span data-ttu-id="6142a-134">Pont – forrás a parancsfájlt, futtassa a parancsot `. .\myConfig.ps1` ahol `myConfig.ps1` a parancsfájl, amely tartalmazza a konfiguráció neve.</span><span class="sxs-lookup"><span data-stu-id="6142a-134">To dot-source the script, run the command `. .\myConfig.ps1` where `myConfig.ps1` is the name of the script file that contains your configuration.</span></span>

<span data-ttu-id="6142a-135">A konfiguráció, hívja ezt:</span><span class="sxs-lookup"><span data-stu-id="6142a-135">When you call the configuration, it:</span></span>

- <span data-ttu-id="6142a-136">Oldja fel az összes változót</span><span class="sxs-lookup"><span data-stu-id="6142a-136">Resolves all variables</span></span>
- <span data-ttu-id="6142a-137">Létrehoz egy mappát a neve megegyezik a konfiguráció az aktuális könyvtárban található.</span><span class="sxs-lookup"><span data-stu-id="6142a-137">Creates a folder in the current directory with the same name as the configuration.</span></span>
- <span data-ttu-id="6142a-138">Létrehoz egy fájlt _csomópontnév_.mof az új címtárban, ahol _csomópontnév_ a célcsomópont a konfiguráció neve.</span><span class="sxs-lookup"><span data-stu-id="6142a-138">Creates a file named _NodeName_.mof in the new directory, where _NodeName_ is the name of the target node of the configuration.</span></span>
  <span data-ttu-id="6142a-139">Ha egynél több csomópont, a MOF-fájlt az egyes csomópontok létrejön.</span><span class="sxs-lookup"><span data-stu-id="6142a-139">If there is more than one node, a MOF file will be created for each node.</span></span>

> [!NOTE]
> <span data-ttu-id="6142a-140">A MOF-fájl összes a célcsomópont konfigurációs adatait tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="6142a-140">The MOF file contains all of the configuration information for the target node.</span></span> <span data-ttu-id="6142a-141">Emiatt fontos tárolja biztonságos helyen.</span><span class="sxs-lookup"><span data-stu-id="6142a-141">Because of this, it’s important to keep it secure.</span></span>
> <span data-ttu-id="6142a-142">További információkért lásd: [a MOF-fájl biztonságossá tétele](../pull-server/secureMOF.md).</span><span class="sxs-lookup"><span data-stu-id="6142a-142">For more information, see [Securing the MOF file](../pull-server/secureMOF.md).</span></span>

<span data-ttu-id="6142a-143">A fenti eredmények a következő gyökérmappa-szerkezetében lévő első konfiguráció fordítása:</span><span class="sxs-lookup"><span data-stu-id="6142a-143">Compiling the first configuration above results in the following folder structure:</span></span>

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

<span data-ttu-id="6142a-144">Ha a konfigurációs paramétert egy, a második példában látható módon, amely rendelkezik a fordítás során meg kell adni.</span><span class="sxs-lookup"><span data-stu-id="6142a-144">If the configuration takes a parameter, as in the second example, that has to be provided at compile time.</span></span> <span data-ttu-id="6142a-145">Itt látható, hogyan néz:</span><span class="sxs-lookup"><span data-stu-id="6142a-145">Here's how that would look:</span></span>

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

## <a name="using-new-resources-in-your-configuration"></a><span data-ttu-id="6142a-146">A konfiguráció új erőforrások használata</span><span class="sxs-lookup"><span data-stu-id="6142a-146">Using new resources in Your configuration</span></span>

<span data-ttu-id="6142a-147">Ha az előző példák futtatta, talán észrevette, hogy akkor is figyelmezteti, hogy explicit módon importálása nélkül erőforrás használja.</span><span class="sxs-lookup"><span data-stu-id="6142a-147">If you ran the previous examples, you might have noticed that you were warned that you were using a resource without explicitly importing it.</span></span>
<span data-ttu-id="6142a-148">Még ma DSC tartalmaz 12 erőforrás jelenik meg a PSDesiredStateConfiguration modul részeként.</span><span class="sxs-lookup"><span data-stu-id="6142a-148">Today, DSC ships with 12 resources as part of the PSDesiredStateConfiguration module.</span></span>

<span data-ttu-id="6142a-149">A parancsmag [Get-DscResource](/powershell/module/PSDesiredStateConfiguration/Get-DscResource), annak meghatározására, hogy milyen erőforrásokat telepítve a rendszeren, és használható a LCM által használható.</span><span class="sxs-lookup"><span data-stu-id="6142a-149">The cmdlet, [Get-DscResource](/powershell/module/PSDesiredStateConfiguration/Get-DscResource), can be used to determine what resources are installed on the system and available for use by the LCM.</span></span>
<span data-ttu-id="6142a-150">Ha ezek a modulok lettek helyezve `$env:PSModulePath` és a rendszer megfelelően ismeri fel [Get-DscResource](/powershell/module/PSDesiredStateConfiguration/Get-DscResource), továbbra is szükségük van, nem tölthető be a konfigurációs belül.</span><span class="sxs-lookup"><span data-stu-id="6142a-150">Once these modules have been placed in `$env:PSModulePath` and are properly recognized by [Get-DscResource](/powershell/module/PSDesiredStateConfiguration/Get-DscResource), they still need to be loaded within your configuration.</span></span>

<span data-ttu-id="6142a-151">**Az import-DscResource** , amely csak belül felismeri a dinamikus kulcsszó egy **konfigurációs** letiltása, már nem ez a parancsmag.</span><span class="sxs-lookup"><span data-stu-id="6142a-151">**Import-DscResource** is a dynamic keyword that can only be recognized within a **Configuration** block, it is not a cmdlet.</span></span>
<span data-ttu-id="6142a-152">**Az import-DscResource** két paramétereket támogatja:</span><span class="sxs-lookup"><span data-stu-id="6142a-152">**Import-DscResource** supports two parameters:</span></span>

- <span data-ttu-id="6142a-153">**ModuleName** használatának ajánlott módja **Import-DscResource**.</span><span class="sxs-lookup"><span data-stu-id="6142a-153">**ModuleName** is the recommended way of using **Import-DscResource**.</span></span> <span data-ttu-id="6142a-154">A modul (valamint a karakterlánc tömbje modulneveket) importálni erőforrásokat tartalmazó neve fogad el.</span><span class="sxs-lookup"><span data-stu-id="6142a-154">It accepts the name of the module that contains the resources to be imported (as well as a string array of module names).</span></span>
- <span data-ttu-id="6142a-155">**Név** neve, az erőforrás importálásához.</span><span class="sxs-lookup"><span data-stu-id="6142a-155">**Name** is the name of the resource to import.</span></span> <span data-ttu-id="6142a-156">Ez nem a valódi nevet, mint "Name" által visszaadott [Get-DscResource](/powershell/module/PSDesiredStateConfiguration/Get-DscResource), de az osztály nevét használja, amikor az erőforrás-séma meghatározása (adja vissza a **ResourceType** által [Get-DscResource](/powershell/module/PSDesiredStateConfiguration/Get-DscResource)).</span><span class="sxs-lookup"><span data-stu-id="6142a-156">This is not the friendly name returned as "Name" by [Get-DscResource](/powershell/module/PSDesiredStateConfiguration/Get-DscResource), but the class name used when defining the resource schema (returned as **ResourceType** by [Get-DscResource](/powershell/module/PSDesiredStateConfiguration/Get-DscResource)).</span></span>

<span data-ttu-id="6142a-157">További tájékoztatást `Import-DSCResource`, lásd: [Import-DSCResource használatával](import-dscresource.md)</span><span class="sxs-lookup"><span data-stu-id="6142a-157">For more information on using `Import-DSCResource`, see [Using Import-DSCResource](import-dscresource.md)</span></span>

## <a name="powershell-v4-and-v5-differences"></a><span data-ttu-id="6142a-158">PowerShell v4 és 5-ös verziójának különbségek</span><span class="sxs-lookup"><span data-stu-id="6142a-158">PowerShell v4 and v5 differences</span></span>

<span data-ttu-id="6142a-159">Ha a DSC-erőforrások kell tárolni a PowerShell 4.0-s különbségek vannak.</span><span class="sxs-lookup"><span data-stu-id="6142a-159">There are differences in where DSC resources need to be stored in PowerShell 4.0.</span></span> <span data-ttu-id="6142a-160">További információkért lásd: [erőforrás helye](import-dscresource.md#resource-location).</span><span class="sxs-lookup"><span data-stu-id="6142a-160">For more information, see [Resource location](import-dscresource.md#resource-location).</span></span>

## <a name="see-also"></a><span data-ttu-id="6142a-161">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="6142a-161">See Also</span></span>

- [<span data-ttu-id="6142a-162">Windows PowerShell Desired State Configuration áttekintése</span><span class="sxs-lookup"><span data-stu-id="6142a-162">Windows PowerShell Desired State Configuration Overview</span></span>](../overview/overview.md)
- [<span data-ttu-id="6142a-163">DSC-erőforrások</span><span class="sxs-lookup"><span data-stu-id="6142a-163">DSC Resources</span></span>](../resources/resources.md)
- [<span data-ttu-id="6142a-164">A helyi Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="6142a-164">Configuring The Local Configuration Manager</span></span>](../managing-nodes/metaConfig.md)
