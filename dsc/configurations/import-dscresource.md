---
ms.date: 12/12/2018
keywords: DSC, powershell, a konfigurációt, a beállítása
title: Az Import-DSCResource használatával
ms.openlocfilehash: 6bc3c1aa1d34a05e3188666da825322235c0672e
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/14/2018
ms.locfileid: "53404289"
---
# <a name="using-import-dscresource"></a><span data-ttu-id="55128-103">Az Import-DSCResource használatával</span><span class="sxs-lookup"><span data-stu-id="55128-103">Using Import-DSCResource</span></span>

<span data-ttu-id="55128-104">`Import-DScResource` van egy dinamikus kulcsszóval, amely csak egy konfigurációs parancsfájl-blokkon belül használható.</span><span class="sxs-lookup"><span data-stu-id="55128-104">`Import-DScResource` is a dynamic keyword, which can only be used inside a Configuration script block.</span></span> <span data-ttu-id="55128-105">A `Import-DSCResource` kulcsszó használatával importálja a konfigurációt a szükséges erőforrásokat.</span><span class="sxs-lookup"><span data-stu-id="55128-105">The `Import-DSCResource` keyword to import any resources needed in your Configuration.</span></span> <span data-ttu-id="55128-106">Alatt lévő erőforrások `$phsome` importálása automatikusan történik, de továbbra is ajánlott explicit módon importálja az összes erőforrás használatban a [konfigurációs](Configurations.md).</span><span class="sxs-lookup"><span data-stu-id="55128-106">Resources under `$phsome` are imported automatically, but it is still considered best practice to explicitly import all resources used in your [Configuration](Configurations.md).</span></span>

<span data-ttu-id="55128-107">A szintaxist a `Import-DSCResource` alább találja.</span><span class="sxs-lookup"><span data-stu-id="55128-107">The syntax for `Import-DSCResource` is shown below.</span></span>

```syntax
Import-DscResource [-Name <ResourceName(s)>] [-ModuleName <ModuleName(s)>]
```

|<span data-ttu-id="55128-108">Paraméter</span><span class="sxs-lookup"><span data-stu-id="55128-108">Parameter</span></span>  |<span data-ttu-id="55128-109">Leírás</span><span class="sxs-lookup"><span data-stu-id="55128-109">Description</span></span>  |
|---------|---------|
|`-Name`|<span data-ttu-id="55128-110">A DSC erőforrás neve, amely importálnia kell.</span><span class="sxs-lookup"><span data-stu-id="55128-110">The DSC resource name(s) that you must import.</span></span> <span data-ttu-id="55128-111">Ha a modul neve van megadva, a parancs megkeresi ezen DSC-erőforrások belül ez a modul; Ellenkező esetben a parancs a DSC-erőforrások keresés minden DSC-erőforrás elérési utat.</span><span class="sxs-lookup"><span data-stu-id="55128-111">If the module name is specified, the command searches for these DSC resources within this module; otherwise the command searches the DSC resources in all DSC resource paths.</span></span> <span data-ttu-id="55128-112">A helyettesítő karakterek használata támogatott.</span><span class="sxs-lookup"><span data-stu-id="55128-112">Wildcards are supported.</span></span>|
|`-ModuleName`|<span data-ttu-id="55128-113">Container modul neve, vagy a modul előírásokat.</span><span class="sxs-lookup"><span data-stu-id="55128-113">The container module name(s), or module specification(s).</span></span>  <span data-ttu-id="55128-114">Erőforrások importálása a modul adja meg, ha a parancs megpróbál importálása csak azokat az erőforrásokat.</span><span class="sxs-lookup"><span data-stu-id="55128-114">If you specify resources to import from a module, the command will try to import only those resources.</span></span> <span data-ttu-id="55128-115">Ha csak a modul adja meg, a parancs importálja a modult a DSC-erőforrások.</span><span class="sxs-lookup"><span data-stu-id="55128-115">If you specify the module only, the command imports all the DSC resources in the module.</span></span>|

<span data-ttu-id="55128-116">A helyettesítő karaktereket is használhat a `-Name` paraméter használatakor `Import-DSCResource`.</span><span class="sxs-lookup"><span data-stu-id="55128-116">You can use wildcards with the `-Name` parameter when using `Import-DSCResource`.</span></span>

```powershell
Import-DscResource -Name * -ModuleName xActiveDirectory;
```

## <a name="example-use-import-dscresource-within-a-configuration"></a><span data-ttu-id="55128-117">Példa: Az Import-DSCResource használja a konfiguráció belül</span><span class="sxs-lookup"><span data-stu-id="55128-117">Example: Use Import-DSCResource within a configuration</span></span>

```powershell
Configuration MSDSCConfiguration
{
    # Search for and imports Service, File, and Registry from the module PSDesiredStateConfiguration.
    Import-DSCResource -ModuleName MS_DSC1 -name Service, File, Registry

    # Search for and import Resource1 from the module that defines it.
    # If only –Name parameter is used then resources can belong to different PowerShell modules as well.
    # TimeZone resource is from the ComputerManagementDSC module which is not installed by default.
    Import-DSCResource -Name File, TimeZone

    # Search for and import all DSC resources inside the module PSDesiredStateConfiguration.
    Import-DSCResource -ModuleName PSDesiredStateConfiguration
...
```

> [!NOTE]
> <span data-ttu-id="55128-118">Több érték erőforrás és modulok nevének megadása a ugyanazt a parancsot nem támogatottak.</span><span class="sxs-lookup"><span data-stu-id="55128-118">Specifying multiple values for Resource names and modules names in same command are not supported.</span></span> <span data-ttu-id="55128-119">Lehet, hogy a nem determinisztikus viselkedés kapcsolatos melyik erőforrást kell betölteni a modul, abban az esetben, ha ugyanazon az erőforráson több modul megtalálható.</span><span class="sxs-lookup"><span data-stu-id="55128-119">It can have non-deterministic behavior about which resource to load from which module in case same resource exists in multiple modules.</span></span> <span data-ttu-id="55128-120">Alább parancs hibát eredményez a fordítás közben.</span><span class="sxs-lookup"><span data-stu-id="55128-120">Below command will result in error during compilation.</span></span>
>
> ```powershell
> Import-DscResource -Name UserConfigProvider*,TestLogger1 -ModuleName UserConfigProv,PsModuleForTestLogger
> ```

<span data-ttu-id="55128-121">Csak a Name paraméter használatakor figyelembe kell dolgot:</span><span class="sxs-lookup"><span data-stu-id="55128-121">Things to consider when using only the Name parameter:</span></span>

- <span data-ttu-id="55128-122">Egy erőforrás-igényes művelet gépen telepített modul számától függően.</span><span class="sxs-lookup"><span data-stu-id="55128-122">It is a resource-intensive operation depending on the number of modules installed on machine.</span></span>
- <span data-ttu-id="55128-123">Az első erőforrás található a megadott nevű betölti azt.</span><span class="sxs-lookup"><span data-stu-id="55128-123">It will load the first resource found with the given name.</span></span> <span data-ttu-id="55128-124">Abban az esetben, ahol egynél több erőforrás azonos nevű telepítve van, akkor sikerült betölteni a helytelen erőforrás.</span><span class="sxs-lookup"><span data-stu-id="55128-124">In the case where there is more than one resource with same name installed, it could load the wrong resource.</span></span>

<span data-ttu-id="55128-125">A javasolt felhasználás az, hogy adja meg `–ModuleName` együtt a `-Name` paramétert, az alábbiakban leírtak szerint.</span><span class="sxs-lookup"><span data-stu-id="55128-125">The recommended usage is to specify `–ModuleName` with the `-Name` parameter, as described below.</span></span>

<span data-ttu-id="55128-126">A szintaxis a következő előnyökkel jár:</span><span class="sxs-lookup"><span data-stu-id="55128-126">This usage has the following benefits:</span></span>

- <span data-ttu-id="55128-127">Csökkenti a teljesítményre gyakorolt hatás, a keresés hatókörét, a megadott erőforrás korlátozza.</span><span class="sxs-lookup"><span data-stu-id="55128-127">It reduces the performance impact by limiting the search scope for the specified resource.</span></span>
- <span data-ttu-id="55128-128">Explicit módon a modult, amely meghatározza az erőforrást, biztosítva a megfelelő erőforrás betöltött határozza meg.</span><span class="sxs-lookup"><span data-stu-id="55128-128">It explicitly defines the module defining the resource, ensuring the correct resource is loaded.</span></span>

> [!NOTE]
> <span data-ttu-id="55128-129">A PowerShell 5.0-s DSC-erőforrásokat több verziója is rendelkezik, és verziók egy számítógép egymás mellett telepíthető.</span><span class="sxs-lookup"><span data-stu-id="55128-129">In PowerShell 5.0, DSC resources can have multiple versions, and versions can be installed on a computer side-by-side.</span></span> <span data-ttu-id="55128-130">Ez valósul meg kellene resource modul több verzióját, a modul mappájában található.</span><span class="sxs-lookup"><span data-stu-id="55128-130">This is implemented by having multiple versions of a resource module that are contained in the same module folder.</span></span>
> <span data-ttu-id="55128-131">További információkért lásd: [eltérő verziójú erőforrások használata](sxsresource.md).</span><span class="sxs-lookup"><span data-stu-id="55128-131">For more information, see [Using resources with multiple versions](sxsresource.md).</span></span>

## <a name="intellisense-with-import-dscresource"></a><span data-ttu-id="55128-132">Az Import-DSCResource az IntelliSense</span><span class="sxs-lookup"><span data-stu-id="55128-132">Intellisense with Import-DSCResource</span></span>

<span data-ttu-id="55128-133">Szerzői műveletek a DSC-konfiguráció ISE-ben, ha a PowerShell IntelliSence biztosít az erőforrások és erőforrás-tulajdonságok.</span><span class="sxs-lookup"><span data-stu-id="55128-133">When authoring the DSC configuration in ISE, PowerShell provides IntelliSence for resources and resource properties.</span></span> <span data-ttu-id="55128-134">Erőforrás-definíciók alapján a `$pshome` modul elérési útja automatikusan töltődnek be.</span><span class="sxs-lookup"><span data-stu-id="55128-134">Resource definitions under the `$pshome` module path are loaded automatically.</span></span> <span data-ttu-id="55128-135">Erőforrások importálásakor a `Import-DSCResource` kulcsszó, az adott erőforrás-definíciókban hozzáadja, és az Intellisense tartalmazza az importált erőforrás-séma ki van bontva.</span><span class="sxs-lookup"><span data-stu-id="55128-135">When you import resources using the `Import-DSCResource` keyword, the specified resource definitions are added and Intellisense is expanded to include the imported resource's schema.</span></span>

![Erőforrás Intellisense](/media/resource-intellisense.png)

> [!NOTE]
> <span data-ttu-id="55128-137">A PowerShell 5.0-es verziótól kezdve kiegészítés hozzáadva a DSC-erőforrások és a hozzájuk tartozó tulajdonságok ISE-ben.</span><span class="sxs-lookup"><span data-stu-id="55128-137">Beginning in PowerShell 5.0, tab completion was added to the ISE for DSC resources and their properties.</span></span> <span data-ttu-id="55128-138">További információkért lásd: [erőforrások](../resources/resources.md).</span><span class="sxs-lookup"><span data-stu-id="55128-138">For more information, see [Resources](../resources/resources.md).</span></span>

<span data-ttu-id="55128-139">A konfiguráció összeállításakor PowerShell ellenőrzése a konfiguráció az összes erőforrás blokkokat használja az importált erőforrás-definíciókban.</span><span class="sxs-lookup"><span data-stu-id="55128-139">When compiling the Configuration, PowerShell uses the imported resource definitions to validate all resource blocks in the configuration.</span></span>
<span data-ttu-id="55128-140">Minden erőforrás blokk érvényesítve, az erőforrás sémadefiníciót, használja a következő szabályokat.</span><span class="sxs-lookup"><span data-stu-id="55128-140">Each resource block is validated, using the resource's schema definition, for the following rules.</span></span>

- <span data-ttu-id="55128-141">Csak a sémában definiált tulajdonságok szolgálnak.</span><span class="sxs-lookup"><span data-stu-id="55128-141">Only properties defined in schema are used.</span></span>
- <span data-ttu-id="55128-142">Az adattípusok minden egyes tulajdonság megfelelőek-e.</span><span class="sxs-lookup"><span data-stu-id="55128-142">The data types for each property are correct.</span></span>
- <span data-ttu-id="55128-143">Kulcsok tulajdonságok vannak megadva.</span><span class="sxs-lookup"><span data-stu-id="55128-143">Keys properties are specified.</span></span>
- <span data-ttu-id="55128-144">Nem csak olvasható tulajdonság használható.</span><span class="sxs-lookup"><span data-stu-id="55128-144">No read-only property is used.</span></span>
- <span data-ttu-id="55128-145">A maps-típusok érvényesítése értéknek.</span><span class="sxs-lookup"><span data-stu-id="55128-145">Validation on value maps types.</span></span>

<span data-ttu-id="55128-146">Vegye figyelembe a következő konfigurációt:</span><span class="sxs-lookup"><span data-stu-id="55128-146">Consider the following configuration:</span></span>

```powershell
Configuration SchemaValidationInCorrectEnumValue
{
    # It is best practice to explicitly import all resources used in your Configuration.
    # This includes resources that are imported automatically, like WindowsFeature.
    Import-DSCResource -Name WindowsFeature
    Node localhost
    {
        WindowsFeature ROLE1
        {
            Name = “Telnet-Client”
            Ensure = “Invalid”
        }
    }
}
```

<span data-ttu-id="55128-147">Hiba történt a konfiguráció eredményez fordítása.</span><span class="sxs-lookup"><span data-stu-id="55128-147">Compiling this Configuration results in an error.</span></span>

```output
PSDesiredStateConfiguration\WindowsFeature: At least one of the values ‘Invalid’ is not supported or valid for property ‘Ensure’ on class ‘WindowsFeature’. Please specify only supported values: Present, Absent.
```

<span data-ttu-id="55128-148">Az IntelliSense és a séma érvényesítése elkerülése futási időben elemzési és fordítási idő alatt további hibák észlelését teszi lehetővé.</span><span class="sxs-lookup"><span data-stu-id="55128-148">Intellisense and schema validation allow you to catch more errors during parse and compilation time, avoiding complications at run time.</span></span>

> [!NOTE]
> <span data-ttu-id="55128-149">Az egyes DSC-erőforrások is rendelkezik egy névvel, és a egy **FriendlyName** az erőforrás-séma határozza meg.</span><span class="sxs-lookup"><span data-stu-id="55128-149">Each DSC resource can have a name, and a **FriendlyName** defined by the resource's schema.</span></span> <span data-ttu-id="55128-150">Az alábbiakban "MSFT_ServiceResource.shema.mof" első két sorát.</span><span class="sxs-lookup"><span data-stu-id="55128-150">Below are the first two lines of "MSFT_ServiceResource.shema.mof".</span></span>
> ```syntax
> [ClassVersion("1.0.0"),FriendlyName("Service")]
> class MSFT_ServiceResource : OMI_BaseResource
> ```
> <span data-ttu-id="55128-151">Az erőforrás-konfiguráció használatakor megadhatja **MSFT_ServiceResource** vagy **szolgáltatás**.</span><span class="sxs-lookup"><span data-stu-id="55128-151">When using this resource in a Configuration, you can specify **MSFT_ServiceResource** or **Service**.</span></span>

## <a name="powershell-v4-and-v5-differences"></a><span data-ttu-id="55128-152">PowerShell v4 és 5-ös verziójának különbségek</span><span class="sxs-lookup"><span data-stu-id="55128-152">PowerShell v4 and v5 differences</span></span>

<span data-ttu-id="55128-153">Amikor a jelentéskészítési konfigurációk a PowerShell 4.0 VS-ben több különbségek vannak. A PowerShell 5.0-s és újabb verziók.</span><span class="sxs-lookup"><span data-stu-id="55128-153">There are multiple differences you see when authoring Configurations in PowerShell 4.0 vs. PowerShell 5.0 and later.</span></span> <span data-ttu-id="55128-154">Ez a szakasz kiemeli a különbségeket, hogy megjelenik-e ez a cikk a.</span><span class="sxs-lookup"><span data-stu-id="55128-154">This section will highlight the differences that you see relevant to this article.</span></span>

### <a name="multiple-resource-versions"></a><span data-ttu-id="55128-155">Több erőforrás-verzió</span><span class="sxs-lookup"><span data-stu-id="55128-155">Multiple Resource Versions</span></span>

<span data-ttu-id="55128-156">Különböző verzióinak egymás melletti erőforrások telepítéséről és a PowerShell 4.0-s nem támogatott.</span><span class="sxs-lookup"><span data-stu-id="55128-156">Installing and using multiple versions of resources side by side was not supported in PowerShell 4.0.</span></span> <span data-ttu-id="55128-157">Ha azt tapasztalja, erőforrások importálása a konfigurációs problémákat, győződjön meg arról, hogy csak egy verziója van telepítve az erőforrás.</span><span class="sxs-lookup"><span data-stu-id="55128-157">If you notice issues importing resources into your Configuration, ensure that you only have one version of the resource installed.</span></span>

<span data-ttu-id="55128-158">A két verziója az alábbi képen a **xPSDesiredStateConfiguration** modulnak vannak telepítve.</span><span class="sxs-lookup"><span data-stu-id="55128-158">In the image below, two versions of the **xPSDesiredStateConfiguration** module are installed.</span></span>

![Rögzített több erőforrás-verzió](/media/multiple-resource-versions-broken.md)

<span data-ttu-id="55128-160">Másolja a tartalmát a kívánt modul verzióját a legfelső szintű modulkönyvtárat.</span><span class="sxs-lookup"><span data-stu-id="55128-160">Copy the contents of your desired module version to the top level of the module directory.</span></span>

![Rögzített több erőforrás-verzió](/media/multiple-resource-versions-fixed.md)

### <a name="resource-location"></a><span data-ttu-id="55128-162">Erőforrás helye</span><span class="sxs-lookup"><span data-stu-id="55128-162">Resource location</span></span>

<span data-ttu-id="55128-163">Amikor szerzői és konfigurációk fordítása, az erőforrások bármely által megadott könyvtárban tárolható a [PSModulePath](/powershell/developer/module/modifying-the-psmodulepath-installation-path).</span><span class="sxs-lookup"><span data-stu-id="55128-163">When authoring and compiling Configurations, your resources can be stored in any directory specified by your [PSModulePath](/powershell/developer/module/modifying-the-psmodulepath-installation-path).</span></span> <span data-ttu-id="55128-164">A PowerShell 4.0-s, az LCM Konfigurálása szükséges minden DSC-erőforrás modulok "Program Files\WindowsPowerShell\Modules" alapján kell tárolni, vagy `$pshome\Modules`.</span><span class="sxs-lookup"><span data-stu-id="55128-164">In PowerShell 4.0, the LCM requires all DSC resource modules to be stored under "Program Files\WindowsPowerShell\Modules" or `$pshome\Modules`.</span></span> <span data-ttu-id="55128-165">A PowerShell 5.0-es verziótól kezdve ez a követelmény el lett távolítva, és az erőforrás-modulokat bármilyen által megadott könyvtárban tárolható `PSModulePath`.</span><span class="sxs-lookup"><span data-stu-id="55128-165">Beginning in PowerShell 5.0, this requirement was removed, and resource modules can be stored in any directory specified by `PSModulePath`.</span></span>

## <a name="see-also"></a><span data-ttu-id="55128-166">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="55128-166">See also</span></span>

- [<span data-ttu-id="55128-167">Erőforrások</span><span class="sxs-lookup"><span data-stu-id="55128-167">Resources</span></span>](../resources/resources.md)
