---
ms.date: 12/12/2018
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: Az Import-DSCResource használata
ms.openlocfilehash: f22c741969b1429074e7307a00a5c014cf563089
ms.sourcegitcommit: 6ae5b50a4b3ffcd649de1525c3ce6f15d3669082
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/14/2019
ms.locfileid: "56265501"
---
# <a name="using-import-dscresource"></a><span data-ttu-id="61aea-103">Az Import-DSCResource használata</span><span class="sxs-lookup"><span data-stu-id="61aea-103">Using Import-DSCResource</span></span>

<span data-ttu-id="61aea-104">`Import-DScResource` a dinamikus kulcsszóval, amely csak akkor használható egy konfigurációs parancsfájl-blokkon belül van.</span><span class="sxs-lookup"><span data-stu-id="61aea-104">`Import-DScResource` is a dynamic keyword, which can only be used inside a Configuration script block.</span></span> <span data-ttu-id="61aea-105">A `Import-DSCResource` kulcsszó importálásához a konfiguráció szükséges erőforrásokat.</span><span class="sxs-lookup"><span data-stu-id="61aea-105">The `Import-DSCResource` keyword to import any resources needed in your Configuration.</span></span> <span data-ttu-id="61aea-106">Alatt lévő erőforrások `$phsome` importálása automatikusan történik, de továbbra is ajánlott eljárás, explicit módon a használt összes erőforrások importálása a [konfigurációs](Configurations.md).</span><span class="sxs-lookup"><span data-stu-id="61aea-106">Resources under `$phsome` are imported automatically, but it is still considered best practice to explicitly import all resources used in your [Configuration](Configurations.md).</span></span>

<span data-ttu-id="61aea-107">A szintaxisának `Import-DSCResource` alább láthatók.</span><span class="sxs-lookup"><span data-stu-id="61aea-107">The syntax for `Import-DSCResource` is shown below.</span></span>  <span data-ttu-id="61aea-108">Amikor modulok megadása név szerint, nem követelmény a listában minden új sorba.</span><span class="sxs-lookup"><span data-stu-id="61aea-108">When specifying modules by name, it is a requirement to list each on a new line.</span></span>

```syntax
Import-DscResource [-Name <ResourceName(s)>] [-ModuleName <ModuleName>]
```

|<span data-ttu-id="61aea-109">Paraméter</span><span class="sxs-lookup"><span data-stu-id="61aea-109">Parameter</span></span>  |<span data-ttu-id="61aea-110">Leírás</span><span class="sxs-lookup"><span data-stu-id="61aea-110">Description</span></span>  |
|---------|---------|
|`-Name`|<span data-ttu-id="61aea-111">A DSC erőforrás neve, amely importálnia kell.</span><span class="sxs-lookup"><span data-stu-id="61aea-111">The DSC resource name(s) that you must import.</span></span> <span data-ttu-id="61aea-112">Ha a modul neve meg van adva, a parancs keresi ezeket DSC erőforrások Ez a modul; Ellenkező esetben a parancs a DSC-erőforrás görbékhez keres a DSC-erőforrások.</span><span class="sxs-lookup"><span data-stu-id="61aea-112">If the module name is specified, the command searches for these DSC resources within this module; otherwise the command searches the DSC resources in all DSC resource paths.</span></span> <span data-ttu-id="61aea-113">Helyettesítő karakterek használata támogatott.</span><span class="sxs-lookup"><span data-stu-id="61aea-113">Wildcards are supported.</span></span>|
|`-ModuleName`|<span data-ttu-id="61aea-114">A modul neve, vagy modul megadását.</span><span class="sxs-lookup"><span data-stu-id="61aea-114">The module name, or module specification.</span></span>  <span data-ttu-id="61aea-115">Modul importálása erőforrásokat ad meg, ha a parancs megpróbálja importálása csak azokat az erőforrásokat.</span><span class="sxs-lookup"><span data-stu-id="61aea-115">If you specify resources to import from a module, the command will try to import only those resources.</span></span> <span data-ttu-id="61aea-116">Csak a modul adja meg, ha a parancs importálására a modul DSC-erőforrások.</span><span class="sxs-lookup"><span data-stu-id="61aea-116">If you specify the module only, the command imports all the DSC resources in the module.</span></span>|

```powershell
Import-DscResource -ModuleName xActiveDirectory;
```

## <a name="example-use-import-dscresource-within-a-configuration"></a><span data-ttu-id="61aea-117">Példa: Import-DSCResource használható konfiguráció</span><span class="sxs-lookup"><span data-stu-id="61aea-117">Example: Use Import-DSCResource within a configuration</span></span>

```powershell
Configuration MSDSCConfiguration
{
    # Search for and imports Service, File, and Registry from the module PSDesiredStateConfiguration.
    Import-DSCResource -ModuleName PSDesiredStateConfiguration -Name Service, File, Registry
    
    # Search for and import Resource1 from the module that defines it.
    # If only –Name parameter is used then resources can belong to different PowerShell modules as well.
    # TimeZone resource is from the ComputerManagementDSC module which is not installed by default.
    # As a best practice, list each requirement on a different line if possible.  This makes reviewing
    # multiple changes in source control a bit easier.
    Import-DSCResource -Name File
    Import-DSCResource -Name TimeZone

    # Search for and import all DSC resources inside the module PSDesiredStateConfiguration.
    # When specifying the modulename parameter, it is a requirement to list each on a new line.
    Import-DSCResource -ModuleName PSDesiredStateConfiguration
    Import-DSCResource -ModuleName ComputerManagementDsc
...
```

> [!NOTE]
> <span data-ttu-id="61aea-118">Több értéket erőforrás és modulok nevének megadása a ugyanezt a parancsot nem támogatottak.</span><span class="sxs-lookup"><span data-stu-id="61aea-118">Specifying multiple values for Resource names and modules names in same command are not supported.</span></span> <span data-ttu-id="61aea-119">Nem determinisztikus jelenség melyik erőforrást kell, hogy melyik modul betöltése, abban az esetben, ha ugyanaz az erőforrás létezik-e több modulban kapcsolatos rendelkezhet.</span><span class="sxs-lookup"><span data-stu-id="61aea-119">It can have non-deterministic behavior about which resource to load from which module in case same resource exists in multiple modules.</span></span> <span data-ttu-id="61aea-120">Alább parancs eredményez hiba történik a fordítás során.</span><span class="sxs-lookup"><span data-stu-id="61aea-120">Below command will result in error during compilation.</span></span>
>
> ```powershell
> Import-DscResource -Name UserConfigProvider*,TestLogger1 -ModuleName UserConfigProv,PsModuleForTestLogger
> ```

<span data-ttu-id="61aea-121">Csak a Name paraméter használata esetén vegye figyelembe a következőkre:</span><span class="sxs-lookup"><span data-stu-id="61aea-121">Things to consider when using only the Name parameter:</span></span>

- <span data-ttu-id="61aea-122">Egy erőforrás-igényes művelet, attól függően, hogy a számítógépen telepített modulok száma is.</span><span class="sxs-lookup"><span data-stu-id="61aea-122">It is a resource-intensive operation depending on the number of modules installed on machine.</span></span>
- <span data-ttu-id="61aea-123">Az első erőforrás található a megadott nevű betölti azt.</span><span class="sxs-lookup"><span data-stu-id="61aea-123">It will load the first resource found with the given name.</span></span> <span data-ttu-id="61aea-124">Abban az esetben, ahol egynél több erőforrás azonos nevű telepítve van, a megfelelő erőforrás tudott betölteni.</span><span class="sxs-lookup"><span data-stu-id="61aea-124">In the case where there is more than one resource with same name installed, it could load the wrong resource.</span></span>

<span data-ttu-id="61aea-125">Az ajánlott használati, ha `–ModuleName` rendelkező a `-Name` paramétert, az alábbiaknak megfelelően.</span><span class="sxs-lookup"><span data-stu-id="61aea-125">The recommended usage is to specify `–ModuleName` with the `-Name` parameter, as described below.</span></span>

<span data-ttu-id="61aea-126">A használati rendelkezik a következő előnyöket biztosítja:</span><span class="sxs-lookup"><span data-stu-id="61aea-126">This usage has the following benefits:</span></span>

- <span data-ttu-id="61aea-127">A megadott erőforrás keresési hatókör korlátozásával csökkenti a teljesítményre gyakorolt hatást.</span><span class="sxs-lookup"><span data-stu-id="61aea-127">It reduces the performance impact by limiting the search scope for the specified resource.</span></span>
- <span data-ttu-id="61aea-128">Explicit módon meghatározza a modult, amely meghatározza az erőforrás, biztosítva, hogy a helyes erőforrás be van töltve.</span><span class="sxs-lookup"><span data-stu-id="61aea-128">It explicitly defines the module defining the resource, ensuring the correct resource is loaded.</span></span>

> [!NOTE]
> <span data-ttu-id="61aea-129">PowerShell 5.0-s DSC erőforrások több verziója is van, és verziók is telepíthető egy számítógép-mellé.</span><span class="sxs-lookup"><span data-stu-id="61aea-129">In PowerShell 5.0, DSC resources can have multiple versions, and versions can be installed on a computer side-by-side.</span></span> <span data-ttu-id="61aea-130">Ez történik, azzal, hogy egy erőforrás-modul több verziója modul azonos mappában találhatók.</span><span class="sxs-lookup"><span data-stu-id="61aea-130">This is implemented by having multiple versions of a resource module that are contained in the same module folder.</span></span>
> <span data-ttu-id="61aea-131">További információkért lásd: [erőforrásokat használó többféle verzióját tartalmazó](sxsresource.md).</span><span class="sxs-lookup"><span data-stu-id="61aea-131">For more information, see [Using resources with multiple versions](sxsresource.md).</span></span>

## <a name="intellisense-with-import-dscresource"></a><span data-ttu-id="61aea-132">Az Import-DSCResource IntelliSense</span><span class="sxs-lookup"><span data-stu-id="61aea-132">Intellisense with Import-DSCResource</span></span>

<span data-ttu-id="61aea-133">A DSC-konfiguráció ISE készítésekor PowerShell biztosít erőforrásokat és erőforrás-tulajdonságok IntelliSence.</span><span class="sxs-lookup"><span data-stu-id="61aea-133">When authoring the DSC configuration in ISE, PowerShell provides IntelliSence for resources and resource properties.</span></span> <span data-ttu-id="61aea-134">Az erőforrás-definíciókban a `$pshome` modul elérési útján automatikusan be vannak töltve.</span><span class="sxs-lookup"><span data-stu-id="61aea-134">Resource definitions under the `$pshome` module path are loaded automatically.</span></span> <span data-ttu-id="61aea-135">Ha importál eszközzel a `Import-DSCResource` kulcsszóval, a megadott erőforrás-definíciókban is hozzáadja, és az Intellisense tartalmazza az importált erőforrás-séma ki van bontva.</span><span class="sxs-lookup"><span data-stu-id="61aea-135">When you import resources using the `Import-DSCResource` keyword, the specified resource definitions are added and Intellisense is expanded to include the imported resource's schema.</span></span>

![Erőforrás Intellisense](/media/resource-intellisense.png)

> [!NOTE]
> <span data-ttu-id="61aea-137">PowerShell 5.0 verziótól kezdve kiegészítést lett felvéve a ISE DSC-erőforrások és azok tulajdonságait.</span><span class="sxs-lookup"><span data-stu-id="61aea-137">Beginning in PowerShell 5.0, tab completion was added to the ISE for DSC resources and their properties.</span></span> <span data-ttu-id="61aea-138">További információkért lásd: [erőforrások](../resources/resources.md).</span><span class="sxs-lookup"><span data-stu-id="61aea-138">For more information, see [Resources](../resources/resources.md).</span></span>

<span data-ttu-id="61aea-139">A konfigurációs összeállításakor PowerShell erőforrás blokkok a konfiguráció érvényesítéséhez használja az importált erőforrás-definíciókban.</span><span class="sxs-lookup"><span data-stu-id="61aea-139">When compiling the Configuration, PowerShell uses the imported resource definitions to validate all resource blocks in the configuration.</span></span>
<span data-ttu-id="61aea-140">Minden erőforrás blokk van hitelesítve, az erőforrás-schema definíció, a következő szabályok segítségével.</span><span class="sxs-lookup"><span data-stu-id="61aea-140">Each resource block is validated, using the resource's schema definition, for the following rules.</span></span>

- <span data-ttu-id="61aea-141">Csak a sémában definiált tulajdonságok használhatók.</span><span class="sxs-lookup"><span data-stu-id="61aea-141">Only properties defined in schema are used.</span></span>
- <span data-ttu-id="61aea-142">Az adattípusok mindegyik tulajdonság megfelelőek-e.</span><span class="sxs-lookup"><span data-stu-id="61aea-142">The data types for each property are correct.</span></span>
- <span data-ttu-id="61aea-143">Kulcsok tulajdonságok vannak megadva.</span><span class="sxs-lookup"><span data-stu-id="61aea-143">Keys properties are specified.</span></span>
- <span data-ttu-id="61aea-144">Nem csak olvasható tulajdonságot használja.</span><span class="sxs-lookup"><span data-stu-id="61aea-144">No read-only property is used.</span></span>
- <span data-ttu-id="61aea-145">Érték ellenőrzése típusok képezi le.</span><span class="sxs-lookup"><span data-stu-id="61aea-145">Validation on value maps types.</span></span>

<span data-ttu-id="61aea-146">Vegye figyelembe a következő konfigurációt:</span><span class="sxs-lookup"><span data-stu-id="61aea-146">Consider the following configuration:</span></span>

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

<span data-ttu-id="61aea-147">Fordítási hiba történt a konfigurációs eredményez.</span><span class="sxs-lookup"><span data-stu-id="61aea-147">Compiling this Configuration results in an error.</span></span>

```output
PSDesiredStateConfiguration\WindowsFeature: At least one of the values ‘Invalid’ is not supported or valid for property ‘Ensure’ on class ‘WindowsFeature’. Please specify only supported values: Present, Absent.
```

<span data-ttu-id="61aea-148">IntelliSense és a séma érvényesítése elkerülése futási időben elemzési és fordítási idő alatt további hibák catch teszik lehetővé.</span><span class="sxs-lookup"><span data-stu-id="61aea-148">Intellisense and schema validation allow you to catch more errors during parse and compilation time, avoiding complications at run time.</span></span>

> [!NOTE]
> <span data-ttu-id="61aea-149">Az egyes DSC erőforrások rendelkezhet egy névvel, és egy **FriendlyName** az erőforrás-séma határozza meg.</span><span class="sxs-lookup"><span data-stu-id="61aea-149">Each DSC resource can have a name, and a **FriendlyName** defined by the resource's schema.</span></span> <span data-ttu-id="61aea-150">Az alábbiakban az első két sort "MSFT_ServiceResource.shema.mof".</span><span class="sxs-lookup"><span data-stu-id="61aea-150">Below are the first two lines of "MSFT_ServiceResource.shema.mof".</span></span>
> ```syntax
> [ClassVersion("1.0.0"),FriendlyName("Service")]
> class MSFT_ServiceResource : OMI_BaseResource
> ```
> <span data-ttu-id="61aea-151">Ehhez az erőforráshoz konfiguráció használatakor is megadhat **MSFT_ServiceResource** vagy **szolgáltatás**.</span><span class="sxs-lookup"><span data-stu-id="61aea-151">When using this resource in a Configuration, you can specify **MSFT_ServiceResource** or **Service**.</span></span>

## <a name="powershell-v4-and-v5-differences"></a><span data-ttu-id="61aea-152">PowerShell v4 és v5 különbségek</span><span class="sxs-lookup"><span data-stu-id="61aea-152">PowerShell v4 and v5 differences</span></span>

<span data-ttu-id="61aea-153">Tekintse meg a PowerShell 4.0 vs konfigurációk készítésekor több különbségek vannak. PowerShell 5.0-s és újabb verziók.</span><span class="sxs-lookup"><span data-stu-id="61aea-153">There are multiple differences you see when authoring Configurations in PowerShell 4.0 vs. PowerShell 5.0 and later.</span></span> <span data-ttu-id="61aea-154">Ez a szakasz a különbségek ki, hogy megjelenik ez a cikk vonatkozik.</span><span class="sxs-lookup"><span data-stu-id="61aea-154">This section will highlight the differences that you see relevant to this article.</span></span>

### <a name="multiple-resource-versions"></a><span data-ttu-id="61aea-155">Több erőforrás-verzió</span><span class="sxs-lookup"><span data-stu-id="61aea-155">Multiple Resource Versions</span></span>

<span data-ttu-id="61aea-156">Telepítéséről és használatáról a különböző verzióinak egymás melletti erőforrások az PowerShell 4.0 nem támogatott.</span><span class="sxs-lookup"><span data-stu-id="61aea-156">Installing and using multiple versions of resources side by side was not supported in PowerShell 4.0.</span></span> <span data-ttu-id="61aea-157">Erőforrások importálja a konfigurációs problémákat észlel, győződjön meg arról, hogy csak egy verziója van telepítve az erőforrás.</span><span class="sxs-lookup"><span data-stu-id="61aea-157">If you notice issues importing resources into your Configuration, ensure that you only have one version of the resource installed.</span></span>

<span data-ttu-id="61aea-158">Az alábbi két ábrán a **xPSDesiredStateConfiguration** modul telepítve vannak.</span><span class="sxs-lookup"><span data-stu-id="61aea-158">In the image below, two versions of the **xPSDesiredStateConfiguration** module are installed.</span></span>

![Rögzített több erőforrás-verzió](/media/multiple-resource-versions-broken.md)

<span data-ttu-id="61aea-160">A legfelső szintű modulkönyvtárat másolja a tartalmát a kívánt modul verziója.</span><span class="sxs-lookup"><span data-stu-id="61aea-160">Copy the contents of your desired module version to the top level of the module directory.</span></span>

![Rögzített több erőforrás-verzió](/media/multiple-resource-versions-fixed.md)

### <a name="resource-location"></a><span data-ttu-id="61aea-162">Erőforrás helye</span><span class="sxs-lookup"><span data-stu-id="61aea-162">Resource location</span></span>

<span data-ttu-id="61aea-163">Jelentéskészítő és -konfigurációk fordítása, ha az erőforrások bármely által megadott könyvtárban tárolható a [PSModulePath](/powershell/developer/module/modifying-the-psmodulepath-installation-path).</span><span class="sxs-lookup"><span data-stu-id="61aea-163">When authoring and compiling Configurations, your resources can be stored in any directory specified by your [PSModulePath](/powershell/developer/module/modifying-the-psmodulepath-installation-path).</span></span> <span data-ttu-id="61aea-164">A PowerShell 4.0 a LCM igényel "Program Files\WindowsPowerShell\Modules" a rendszer ne tárolja az összes DSC erőforrás modul vagy `$pshome\Modules`.</span><span class="sxs-lookup"><span data-stu-id="61aea-164">In PowerShell 4.0, the LCM requires all DSC resource modules to be stored under "Program Files\WindowsPowerShell\Modules" or `$pshome\Modules`.</span></span> <span data-ttu-id="61aea-165">PowerShell 5.0 verziótól kezdve ez a követelmény el lett távolítva, és erőforrás-modulok bármely által megadott könyvtárban tárolható `PSModulePath`.</span><span class="sxs-lookup"><span data-stu-id="61aea-165">Beginning in PowerShell 5.0, this requirement was removed, and resource modules can be stored in any directory specified by `PSModulePath`.</span></span>

## <a name="see-also"></a><span data-ttu-id="61aea-166">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="61aea-166">See also</span></span>

- [<span data-ttu-id="61aea-167">Erőforrások</span><span class="sxs-lookup"><span data-stu-id="61aea-167">Resources</span></span>](../resources/resources.md)
