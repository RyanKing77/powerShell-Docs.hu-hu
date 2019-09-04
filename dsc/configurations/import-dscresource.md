---
ms.date: 12/12/2018
keywords: DSC, PowerShell, konfigurálás, beállítás
title: Az Import-DSCResource használata
ms.openlocfilehash: e1c2c06d756a70c2de516f330e3123235ce740ba
ms.sourcegitcommit: 02eed65c526ef19cf952c2129f280bb5615bf0c8
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/03/2019
ms.locfileid: "70215398"
---
# <a name="using-import-dscresource"></a><span data-ttu-id="c52c3-103">Az Import-DSCResource használata</span><span class="sxs-lookup"><span data-stu-id="c52c3-103">Using Import-DSCResource</span></span>

<span data-ttu-id="c52c3-104">`Import-DScResource`egy dinamikus kulcsszó, amely csak a konfigurációs parancsfájlok blokkjában használható.</span><span class="sxs-lookup"><span data-stu-id="c52c3-104">`Import-DScResource` is a dynamic keyword, which can only be used inside a Configuration script block.</span></span> <span data-ttu-id="c52c3-105">A `Import-DSCResource` konfigurációban szükséges erőforrások importálására szolgáló kulcsszó.</span><span class="sxs-lookup"><span data-stu-id="c52c3-105">The `Import-DSCResource` keyword to import any resources needed in your Configuration.</span></span> <span data-ttu-id="c52c3-106">A rendszer automatikusan importálja az erőforrásokat, de az ajánlott eljárás a konfigurációban használt összes erőforrás explicit módon történő importálása is. [](Configurations.md) `$pshome`</span><span class="sxs-lookup"><span data-stu-id="c52c3-106">Resources under `$pshome` are imported automatically, but it is still considered best practice to explicitly import all resources used in your [Configuration](Configurations.md).</span></span>

<span data-ttu-id="c52c3-107">A szintaxisa `Import-DSCResource` alább látható.</span><span class="sxs-lookup"><span data-stu-id="c52c3-107">The syntax for `Import-DSCResource` is shown below.</span></span>  <span data-ttu-id="c52c3-108">A modulok név szerint történő megadásakor követelmény, hogy mindegyiket egy új sorba sorolja.</span><span class="sxs-lookup"><span data-stu-id="c52c3-108">When specifying modules by name, it is a requirement to list each on a new line.</span></span>

```syntax
Import-DscResource [-Name <ResourceName(s)>] [-ModuleName <ModuleName>]
```

|<span data-ttu-id="c52c3-109">Paraméter</span><span class="sxs-lookup"><span data-stu-id="c52c3-109">Parameter</span></span>  |<span data-ttu-id="c52c3-110">Leírás</span><span class="sxs-lookup"><span data-stu-id="c52c3-110">Description</span></span>  |
|---------|---------|
|`-Name`|<span data-ttu-id="c52c3-111">A DSC-erőforrás neve (i), amelyet importálnia kell.</span><span class="sxs-lookup"><span data-stu-id="c52c3-111">The DSC resource name(s) that you must import.</span></span> <span data-ttu-id="c52c3-112">Ha a modul neve meg van adva, a parancs ezen a modulon belül keresi a DSC-erőforrásokat. Ellenkező esetben a parancs az összes DSC-erőforrás elérési útján keresi a DSC-erőforrásokat.</span><span class="sxs-lookup"><span data-stu-id="c52c3-112">If the module name is specified, the command searches for these DSC resources within this module; otherwise the command searches the DSC resources in all DSC resource paths.</span></span> <span data-ttu-id="c52c3-113">A helyettesítő karakterek használata támogatott.</span><span class="sxs-lookup"><span data-stu-id="c52c3-113">Wildcards are supported.</span></span>|
|`-ModuleName`|<span data-ttu-id="c52c3-114">A modul neve vagy a modul specifikációja.</span><span class="sxs-lookup"><span data-stu-id="c52c3-114">The module name, or module specification.</span></span>  <span data-ttu-id="c52c3-115">Ha egy modulból importálandó erőforrásokat ad meg, a parancs csak ezeket az erőforrásokat fogja importálni.</span><span class="sxs-lookup"><span data-stu-id="c52c3-115">If you specify resources to import from a module, the command will try to import only those resources.</span></span> <span data-ttu-id="c52c3-116">Ha csak a modult adta meg, a parancs a modulban lévő összes DSC-erőforrást importálja.</span><span class="sxs-lookup"><span data-stu-id="c52c3-116">If you specify the module only, the command imports all the DSC resources in the module.</span></span>|

```powershell
Import-DscResource -ModuleName xActiveDirectory;
```

## <a name="example-use-import-dscresource-within-a-configuration"></a><span data-ttu-id="c52c3-117">Példa: Az import-DSCResource használata egy konfiguráción belül</span><span class="sxs-lookup"><span data-stu-id="c52c3-117">Example: Use Import-DSCResource within a configuration</span></span>

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
> <span data-ttu-id="c52c3-118">Ha több értéket ad meg az erőforrás-nevekhez és a modulok nevéhez, a parancs nem támogatott.</span><span class="sxs-lookup"><span data-stu-id="c52c3-118">Specifying multiple values for Resource names and modules names in same command are not supported.</span></span> <span data-ttu-id="c52c3-119">Nem determinisztikus-viselkedéssel rendelkezik arról, hogy melyik erőforrást kell betölteni, ha az adott erőforrás több modulban is megtalálható.</span><span class="sxs-lookup"><span data-stu-id="c52c3-119">It can have non-deterministic behavior about which resource to load from which module in case same resource exists in multiple modules.</span></span> <span data-ttu-id="c52c3-120">Az alábbi parancs hibát okoz a fordítás során.</span><span class="sxs-lookup"><span data-stu-id="c52c3-120">Below command will result in error during compilation.</span></span>
>
> ```powershell
> Import-DscResource -Name UserConfigProvider*,TestLogger1 -ModuleName UserConfigProv,PsModuleForTestLogger
> ```

<span data-ttu-id="c52c3-121">Csak a name paraméter használata esetén megfontolandó szempontok:</span><span class="sxs-lookup"><span data-stu-id="c52c3-121">Things to consider when using only the Name parameter:</span></span>

- <span data-ttu-id="c52c3-122">Ez egy erőforrás-igényes művelet a gépen telepített modulok számától függően.</span><span class="sxs-lookup"><span data-stu-id="c52c3-122">It is a resource-intensive operation depending on the number of modules installed on machine.</span></span>
- <span data-ttu-id="c52c3-123">A rendszer betölti a megadott névvel rendelkező első erőforrást.</span><span class="sxs-lookup"><span data-stu-id="c52c3-123">It will load the first resource found with the given name.</span></span> <span data-ttu-id="c52c3-124">Abban az esetben, ha egynél több azonos nevű erőforrás van telepítve, akkor a hibás erőforrást is betöltheti.</span><span class="sxs-lookup"><span data-stu-id="c52c3-124">In the case where there is more than one resource with same name installed, it could load the wrong resource.</span></span>

<span data-ttu-id="c52c3-125">Az ajánlott használatot a paraméterrel kell `-Name` megadni `–ModuleName` az alább leírtak szerint.</span><span class="sxs-lookup"><span data-stu-id="c52c3-125">The recommended usage is to specify `–ModuleName` with the `-Name` parameter, as described below.</span></span>

<span data-ttu-id="c52c3-126">Ez a használat a következő előnyökkel jár:</span><span class="sxs-lookup"><span data-stu-id="c52c3-126">This usage has the following benefits:</span></span>

- <span data-ttu-id="c52c3-127">A megadott erőforrás keresési hatókörének korlátozásával csökkenti a teljesítményre gyakorolt hatást.</span><span class="sxs-lookup"><span data-stu-id="c52c3-127">It reduces the performance impact by limiting the search scope for the specified resource.</span></span>
- <span data-ttu-id="c52c3-128">Explicit módon definiálja az erőforrást meghatározó modult, amely biztosítja a megfelelő erőforrás betöltését.</span><span class="sxs-lookup"><span data-stu-id="c52c3-128">It explicitly defines the module defining the resource, ensuring the correct resource is loaded.</span></span>

> [!NOTE]
> <span data-ttu-id="c52c3-129">A PowerShell 5,0-ben a DSC-erőforrások több verzióval is rendelkezhetnek, és a verziók a számítógépen egymás mellett telepíthetők.</span><span class="sxs-lookup"><span data-stu-id="c52c3-129">In PowerShell 5.0, DSC resources can have multiple versions, and versions can be installed on a computer side-by-side.</span></span> <span data-ttu-id="c52c3-130">Ez egy olyan erőforrás-modul több verziójával valósul meg, amely ugyanabban a modul mappában található.</span><span class="sxs-lookup"><span data-stu-id="c52c3-130">This is implemented by having multiple versions of a resource module that are contained in the same module folder.</span></span>
> <span data-ttu-id="c52c3-131">További információ: [erőforrások használata több verzióval](sxsresource.md).</span><span class="sxs-lookup"><span data-stu-id="c52c3-131">For more information, see [Using resources with multiple versions](sxsresource.md).</span></span>

## <a name="intellisense-with-import-dscresource"></a><span data-ttu-id="c52c3-132">IntelliSense importálással – DSCResource</span><span class="sxs-lookup"><span data-stu-id="c52c3-132">Intellisense with Import-DSCResource</span></span>

<span data-ttu-id="c52c3-133">A DSC-konfiguráció ISE-ben történő létrehozásakor a PowerShell IntelliSence biztosít az erőforrásokhoz és az erőforrás-tulajdonságokhoz.</span><span class="sxs-lookup"><span data-stu-id="c52c3-133">When authoring the DSC configuration in ISE, PowerShell provides IntelliSence for resources and resource properties.</span></span> <span data-ttu-id="c52c3-134">A `$pshome` modul elérési útjának erőforrás-definíciói automatikusan betöltődik.</span><span class="sxs-lookup"><span data-stu-id="c52c3-134">Resource definitions under the `$pshome` module path are loaded automatically.</span></span> <span data-ttu-id="c52c3-135">Ha a `Import-DSCResource` kulcsszó használatával importál erőforrásokat, a rendszer hozzáadja a megadott erőforrás-definíciókat, az IntelliSense kibontása pedig az importált erőforrás sémájának belefoglalásához.</span><span class="sxs-lookup"><span data-stu-id="c52c3-135">When you import resources using the `Import-DSCResource` keyword, the specified resource definitions are added and Intellisense is expanded to include the imported resource's schema.</span></span>

![Erőforrás IntelliSense](../media/resource-intellisense.png)

> [!NOTE]
> <span data-ttu-id="c52c3-137">A PowerShell 5,0-től kezdve a TAB befejezését a DSC-erőforrásokhoz és azok tulajdonságaihoz adta hozzá a rendszer.</span><span class="sxs-lookup"><span data-stu-id="c52c3-137">Beginning in PowerShell 5.0, tab completion was added to the ISE for DSC resources and their properties.</span></span> <span data-ttu-id="c52c3-138">További információ: [erőforrások](../resources/resources.md).</span><span class="sxs-lookup"><span data-stu-id="c52c3-138">For more information, see [Resources](../resources/resources.md).</span></span>

<span data-ttu-id="c52c3-139">A konfiguráció fordításakor a PowerShell az importált erőforrás-definíciók használatával ellenőrzi a konfigurációban lévő összes erőforrás-blokkot.</span><span class="sxs-lookup"><span data-stu-id="c52c3-139">When compiling the Configuration, PowerShell uses the imported resource definitions to validate all resource blocks in the configuration.</span></span>
<span data-ttu-id="c52c3-140">Az egyes erőforrás-blokkokat az erőforrás sémájának definíciója alapján érvényesíti a következő szabályokhoz.</span><span class="sxs-lookup"><span data-stu-id="c52c3-140">Each resource block is validated, using the resource's schema definition, for the following rules.</span></span>

- <span data-ttu-id="c52c3-141">Csak a sémában definiált tulajdonságok használatosak.</span><span class="sxs-lookup"><span data-stu-id="c52c3-141">Only properties defined in schema are used.</span></span>
- <span data-ttu-id="c52c3-142">Az egyes tulajdonságok adattípusai helyesek.</span><span class="sxs-lookup"><span data-stu-id="c52c3-142">The data types for each property are correct.</span></span>
- <span data-ttu-id="c52c3-143">A kulcsok tulajdonságai meg vannak adva.</span><span class="sxs-lookup"><span data-stu-id="c52c3-143">Keys properties are specified.</span></span>
- <span data-ttu-id="c52c3-144">A rendszer nem használ írásvédett tulajdonságot.</span><span class="sxs-lookup"><span data-stu-id="c52c3-144">No read-only property is used.</span></span>
- <span data-ttu-id="c52c3-145">Érvényesítés az érték térképek típusain.</span><span class="sxs-lookup"><span data-stu-id="c52c3-145">Validation on value maps types.</span></span>

<span data-ttu-id="c52c3-146">Vegye figyelembe a következő konfigurációt:</span><span class="sxs-lookup"><span data-stu-id="c52c3-146">Consider the following configuration:</span></span>

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

<span data-ttu-id="c52c3-147">A konfiguráció fordítása hibát eredményez.</span><span class="sxs-lookup"><span data-stu-id="c52c3-147">Compiling this Configuration results in an error.</span></span>

```output
PSDesiredStateConfiguration\WindowsFeature: At least one of the values ‘Invalid’ is not supported or valid for property ‘Ensure’ on class ‘WindowsFeature’. Please specify only supported values: Present, Absent.
```

<span data-ttu-id="c52c3-148">Az IntelliSense és a séma érvényesítése lehetővé teszi, hogy több hibát kapjon az elemzési és a fordítási idő során, és elkerülve a szövődmények futási idejét.</span><span class="sxs-lookup"><span data-stu-id="c52c3-148">Intellisense and schema validation allow you to catch more errors during parse and compilation time, avoiding complications at run time.</span></span>

> [!NOTE]
> <span data-ttu-id="c52c3-149">Minden DSC-erőforrás rendelkezhet egy névvel, és az erőforrás sémája által definiált **FriendlyName** is.</span><span class="sxs-lookup"><span data-stu-id="c52c3-149">Each DSC resource can have a name, and a **FriendlyName** defined by the resource's schema.</span></span> <span data-ttu-id="c52c3-150">Az alábbiakban a "MSFT_ServiceResource. shema. MOF" első két sora látható.</span><span class="sxs-lookup"><span data-stu-id="c52c3-150">Below are the first two lines of "MSFT_ServiceResource.shema.mof".</span></span>
> ```syntax
> [ClassVersion("1.0.0"),FriendlyName("Service")]
> class MSFT_ServiceResource : OMI_BaseResource
> ```
> <span data-ttu-id="c52c3-151">Ha ezt az erőforrást egy konfigurációban használja, megadhatja a **MSFT_ServiceResource** vagy a **szolgáltatást**.</span><span class="sxs-lookup"><span data-stu-id="c52c3-151">When using this resource in a Configuration, you can specify **MSFT_ServiceResource** or **Service**.</span></span>

## <a name="powershell-v4-and-v5-differences"></a><span data-ttu-id="c52c3-152">PowerShell v4 és V5 különbségek</span><span class="sxs-lookup"><span data-stu-id="c52c3-152">PowerShell v4 and v5 differences</span></span>

<span data-ttu-id="c52c3-153">A PowerShell 4,0-ben és a-ben a konfigurációk létrehozásakor több különbség jelenik meg. PowerShell 5,0 és újabb verziók.</span><span class="sxs-lookup"><span data-stu-id="c52c3-153">There are multiple differences you see when authoring Configurations in PowerShell 4.0 vs. PowerShell 5.0 and later.</span></span> <span data-ttu-id="c52c3-154">Ebben a szakaszban a jelen cikkhez kapcsolódó különbségek láthatók.</span><span class="sxs-lookup"><span data-stu-id="c52c3-154">This section will highlight the differences that you see relevant to this article.</span></span>

### <a name="multiple-resource-versions"></a><span data-ttu-id="c52c3-155">Több erőforrás-verzió</span><span class="sxs-lookup"><span data-stu-id="c52c3-155">Multiple Resource Versions</span></span>

<span data-ttu-id="c52c3-156">A PowerShell 4,0 nem támogatja az erőforrások különböző verzióinak egyoldalas telepítését és használatát.</span><span class="sxs-lookup"><span data-stu-id="c52c3-156">Installing and using multiple versions of resources side by side was not supported in PowerShell 4.0.</span></span> <span data-ttu-id="c52c3-157">Ha az erőforrások a konfigurációba való importálásával kapcsolatos problémákat tapasztal, győződjön meg arról, hogy az erőforrásnak csak egy verziója van telepítve.</span><span class="sxs-lookup"><span data-stu-id="c52c3-157">If you notice issues importing resources into your Configuration, ensure that you only have one version of the resource installed.</span></span>

<span data-ttu-id="c52c3-158">Az alábbi képen a **xPSDesiredStateConfiguration** modul két verziója van telepítve.</span><span class="sxs-lookup"><span data-stu-id="c52c3-158">In the image below, two versions of the **xPSDesiredStateConfiguration** module are installed.</span></span>

![Több erőforrás-verzió javítva](../media/multiple-resource-versions-broken.png)

<span data-ttu-id="c52c3-160">Másolja a kívánt modul verziójának tartalmát a modul könyvtárának legfelső szintjére.</span><span class="sxs-lookup"><span data-stu-id="c52c3-160">Copy the contents of your desired module version to the top level of the module directory.</span></span>

![Több erőforrás-verzió javítva](../media/multiple-resource-versions-fixed.png)

### <a name="resource-location"></a><span data-ttu-id="c52c3-162">Erőforrás helye</span><span class="sxs-lookup"><span data-stu-id="c52c3-162">Resource location</span></span>

<span data-ttu-id="c52c3-163">Konfigurációk létrehozásakor és fordításakor az erőforrások a [PSModulePath](/powershell/developer/module/modifying-the-psmodulepath-installation-path)által meghatározott bármely könyvtárban tárolhatók.</span><span class="sxs-lookup"><span data-stu-id="c52c3-163">When authoring and compiling Configurations, your resources can be stored in any directory specified by your [PSModulePath](/powershell/developer/module/modifying-the-psmodulepath-installation-path).</span></span> <span data-ttu-id="c52c3-164">A PowerShell 4,0-ben a teljes DSC-erőforrás modulokat a "program Files\WindowsPowerShell\Modules" vagy `$pshome\Modules`a (z) alatt kell tárolni.</span><span class="sxs-lookup"><span data-stu-id="c52c3-164">In PowerShell 4.0, the LCM requires all DSC resource modules to be stored under "Program Files\WindowsPowerShell\Modules" or `$pshome\Modules`.</span></span> <span data-ttu-id="c52c3-165">A PowerShell 5,0-es verziójától kezdve ez a követelmény el lett távolítva, és az erőforrás-modulok `PSModulePath`a által meghatározott bármely könyvtárban tárolhatók.</span><span class="sxs-lookup"><span data-stu-id="c52c3-165">Beginning in PowerShell 5.0, this requirement was removed, and resource modules can be stored in any directory specified by `PSModulePath`.</span></span>

## <a name="see-also"></a><span data-ttu-id="c52c3-166">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="c52c3-166">See also</span></span>

- [<span data-ttu-id="c52c3-167">Erőforrások</span><span class="sxs-lookup"><span data-stu-id="c52c3-167">Resources</span></span>](../resources/resources.md)
