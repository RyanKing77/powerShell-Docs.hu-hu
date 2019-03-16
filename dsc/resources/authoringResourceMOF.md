---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: MOF-egyéni DSC-erőforrás írása
ms.openlocfilehash: f243c3e3297711e6f6346a0f813a9c017fe227c3
ms.sourcegitcommit: caac7d098a448232304c9d6728e7340ec7517a71
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/16/2019
ms.locfileid: "58059728"
---
# <a name="writing-a-custom-dsc-resource-with-mof"></a><span data-ttu-id="7ef04-103">MOF-egyéni DSC-erőforrás írása</span><span class="sxs-lookup"><span data-stu-id="7ef04-103">Writing a custom DSC resource with MOF</span></span>

> <span data-ttu-id="7ef04-104">Érvényes: Windows PowerShell 4.0-s, a Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="7ef04-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="7ef04-105">Ebben a témakörben azt fogja adjon meg egy Windows PowerShell Desired State Configuration (DSC) egyéni erőforrást a sémát a MOF-fájlt, és az erőforrás megvalósítása az egy olyan Windows PowerShell-parancsfájlt.</span><span class="sxs-lookup"><span data-stu-id="7ef04-105">In this topic, we will define the schema for a Windows PowerShell Desired State Configuration (DSC) custom resource in a MOF file, and implement the resource in a Windows PowerShell script file.</span></span> <span data-ttu-id="7ef04-106">Az egyéni erőforrás létrehozása és üzemeltetése egy webhely van.</span><span class="sxs-lookup"><span data-stu-id="7ef04-106">This custom resource is for creating and maintaining a web site.</span></span>

## <a name="creating-the-mof-schema"></a><span data-ttu-id="7ef04-107">A MOF-séma létrehozása</span><span class="sxs-lookup"><span data-stu-id="7ef04-107">Creating the MOF schema</span></span>

<span data-ttu-id="7ef04-108">A séma meghatározza az erőforrást, amely a DSC konfigurációs parancsfájlt is konfigurálhatja a tulajdonságait.</span><span class="sxs-lookup"><span data-stu-id="7ef04-108">The schema defines the properties of your resource that can be configured by a DSC configuration script.</span></span>

### <a name="folder-structure-for-a-mof-resource"></a><span data-ttu-id="7ef04-109">A mappastruktúra a MOF-erőforrás</span><span class="sxs-lookup"><span data-stu-id="7ef04-109">Folder structure for a MOF resource</span></span>

<span data-ttu-id="7ef04-110">DSC MOF sémával egyéni erőforrás megvalósításához, hozzon létre a következő mappaszerkezetet.</span><span class="sxs-lookup"><span data-stu-id="7ef04-110">To implement a DSC custom resource with a MOF schema, create the following folder structure.</span></span> <span data-ttu-id="7ef04-111">A MOF-séma Demo_IISWebsite.schema.mof fájlban van definiálva, és az erőforrás-parancsfájl Demo_IISWebsite.psm1 van definiálva.</span><span class="sxs-lookup"><span data-stu-id="7ef04-111">The MOF schema is defined in the file Demo_IISWebsite.schema.mof, and the resource script is defined in Demo_IISWebsite.psm1.</span></span> <span data-ttu-id="7ef04-112">Igény szerint hozhat létre egy modul jegyzékfájlt (psd1 kiterjesztésű) fájlt.</span><span class="sxs-lookup"><span data-stu-id="7ef04-112">Optionally, you can create a module manifest (psd1) file.</span></span>

```
$env:ProgramFiles\WindowsPowerShell\Modules (folder)
    |- MyDscResources (folder)
        |- DSCResources (folder)
            |- Demo_IISWebsite (folder)
                |- Demo_IISWebsite.psd1 (file, optional)
                |- Demo_IISWebsite.psm1 (file, required)
                |- Demo_IISWebsite.schema.mof (file, required)
```

<span data-ttu-id="7ef04-113">Vegye figyelembe, hogy a legfelső szintű mappa alatt DSCResources nevű mappa létrehozásához szükséges, és, hogy a mappát az egyes erőforrások rendelkeznie kell az erőforrás azonos néven.</span><span class="sxs-lookup"><span data-stu-id="7ef04-113">Note that it is necessary to create a folder named DSCResources under the top-level folder, and that the folder for each resource must have the same name as the resource.</span></span>

### <a name="the-contents-of-the-mof-file"></a><span data-ttu-id="7ef04-114">A MOF-fájl tartalmát</span><span class="sxs-lookup"><span data-stu-id="7ef04-114">The contents of the MOF file</span></span>

<span data-ttu-id="7ef04-115">Következő egy példa MOF-fájlt, amely egy egyéni webhely erőforrás használható.</span><span class="sxs-lookup"><span data-stu-id="7ef04-115">Following is an example MOF file that can be used for a custom website resource.</span></span> <span data-ttu-id="7ef04-116">Kövesse az ebben a példában, ebben a sémában mentése fájlba, és hívja meg a fájl *Demo_IISWebsite.schema.mof*.</span><span class="sxs-lookup"><span data-stu-id="7ef04-116">To follow this example, save this schema to a file, and call the file *Demo_IISWebsite.schema.mof*.</span></span>

```
[ClassVersion("1.0.0"), FriendlyName("Website")]
class Demo_IISWebsite : OMI_BaseResource
{
  [Key] string Name;
  [Required] string PhysicalPath;
  [write,ValueMap{"Present", "Absent"},Values{"Present", "Absent"}] string Ensure;
  [write,ValueMap{"Started","Stopped"},Values{"Started", "Stopped"}] string State;
  [write] string Protocol[];
  [write] string BindingInfo[];
  [write] string ApplicationPool;
  [read] string ID;
};
```

<span data-ttu-id="7ef04-117">Az előző kód kapcsolatos megjegyzések:</span><span class="sxs-lookup"><span data-stu-id="7ef04-117">Note the following about the previous code:</span></span>

* <span data-ttu-id="7ef04-118">`FriendlyName` Meghatározza a segítségével tekintse meg a DSC konfigurációs szkripteket az egyéni erőforrás nevét.</span><span class="sxs-lookup"><span data-stu-id="7ef04-118">`FriendlyName` defines the name you can use to refer to this custom resource in DSC configuration scripts.</span></span> <span data-ttu-id="7ef04-119">Ebben a példában `Website` egyenértékű a valódi nevet a `Archive` a beépített archív erőforrás.</span><span class="sxs-lookup"><span data-stu-id="7ef04-119">In this example, `Website` is equivalent to the friendly name `Archive` for the built-in Archive resource.</span></span>
* <span data-ttu-id="7ef04-120">Az osztály esetében az egyéni erőforrás származhat határoz meg `OMI_BaseResource`.</span><span class="sxs-lookup"><span data-stu-id="7ef04-120">The class you define for your custom resource must derive from `OMI_BaseResource`.</span></span>
* <span data-ttu-id="7ef04-121">Kvalifikátor typu se `[Key]`, a tulajdonság azt jelzi, hogy ezt a tulajdonságot egyedileg azonosítja az erőforrás-példány.</span><span class="sxs-lookup"><span data-stu-id="7ef04-121">The type qualifier, `[Key]`, on a property indicates that this property will uniquely identify the resource instance.</span></span> <span data-ttu-id="7ef04-122">Legalább egy `[Key]` tulajdonságot kötelező megadni.</span><span class="sxs-lookup"><span data-stu-id="7ef04-122">At least one `[Key]` property is required.</span></span>
* <span data-ttu-id="7ef04-123">A `[Required]` minősítő azt jelzi, hogy a tulajdonság megadása kötelező (értéket kell megadni minden más konfigurációs parancsfájl, amely ezt az erőforrást használ).</span><span class="sxs-lookup"><span data-stu-id="7ef04-123">The `[Required]` qualifier indicates that the property is required (a value must be specified in any configuration script that uses this resource).</span></span>
* <span data-ttu-id="7ef04-124">A `[write]` minősítő azt jelzi, hogy ez a tulajdonság nem kötelező az egyéni erőforrás az konfigurációs parancsfájl használata során.</span><span class="sxs-lookup"><span data-stu-id="7ef04-124">The `[write]` qualifier indicates that this property is optional when using the custom resource in a configuration script.</span></span> <span data-ttu-id="7ef04-125">A `[read]` minősítő azt jelzi, hogy a tulajdonság nem állítható be a konfiguráció szerint, és csak jelentéskészítési célból van.</span><span class="sxs-lookup"><span data-stu-id="7ef04-125">The `[read]` qualifier indicates that a property cannot be set by a configuration, and is for reporting purposes only.</span></span>
* <span data-ttu-id="7ef04-126">`Values` korlátozza az értékeket, amelyeket a megadott értékek listájára tulajdonsághoz rendelhető `ValueMap`.</span><span class="sxs-lookup"><span data-stu-id="7ef04-126">`Values` restricts the values that can be assigned to the property to the list of values defined in `ValueMap`.</span></span> <span data-ttu-id="7ef04-127">További információkért lásd: [ValueMap és érték minősítők](/windows/desktop/WmiSdk/value-map).</span><span class="sxs-lookup"><span data-stu-id="7ef04-127">For more information, see [ValueMap and Value Qualifiers](/windows/desktop/WmiSdk/value-map).</span></span>
* <span data-ttu-id="7ef04-128">Például egy tulajdonság nevű `Ensure` értékekkel `Present` és `Absent` arra, hogy a beépített DSC-erőforrások egységes stílus karbantartása javasolt az erőforrás.</span><span class="sxs-lookup"><span data-stu-id="7ef04-128">Including a property called `Ensure` with values `Present` and `Absent` in your resource is recommended as a way to maintain a consistent style with built-in DSC resources.</span></span>
* <span data-ttu-id="7ef04-129">A sémafájl az egyéni erőforrás a következő nevet: `classname.schema.mof`, ahol `classname` azonosítója a következő a `class` kulcsszó a sémadefiníciókban.</span><span class="sxs-lookup"><span data-stu-id="7ef04-129">Name the schema file for your custom resource as follows: `classname.schema.mof`, where `classname` is the identifier that follows the `class` keyword in your schema definition.</span></span>

### <a name="writing-the-resource-script"></a><span data-ttu-id="7ef04-130">Az erőforrás-parancsprogram írása</span><span class="sxs-lookup"><span data-stu-id="7ef04-130">Writing the resource script</span></span>

<span data-ttu-id="7ef04-131">Az erőforrás-parancsfájl valósítja meg az erőforrás a logikát.</span><span class="sxs-lookup"><span data-stu-id="7ef04-131">The resource script implements the logic of the resource.</span></span> <span data-ttu-id="7ef04-132">Ebben a modulban nevű három funkció tartalmaznia **Get-TargetResource**, **Set-TargetResource**, és **Test-TargetResource**.</span><span class="sxs-lookup"><span data-stu-id="7ef04-132">In this module, you must include three functions called **Get-TargetResource**, **Set-TargetResource**, and **Test-TargetResource**.</span></span> <span data-ttu-id="7ef04-133">Mindhárom funkció, amely megegyezik a MOF-séma, az erőforrás létrehozott tulajdonságkészlettel paraméterkészlet kell tennie.</span><span class="sxs-lookup"><span data-stu-id="7ef04-133">All three functions must take a parameter set that is identical to the set of properties defined in the MOF schema that you created for your resource.</span></span> <span data-ttu-id="7ef04-134">Ebben a dokumentumban a tulajdonságai készletét a neve a "erőforrás-tulajdonságokat."</span><span class="sxs-lookup"><span data-stu-id="7ef04-134">In this document, this set of properties is referred to as the “resource properties.”</span></span> <span data-ttu-id="7ef04-135">Ezek három funkciót egy fájlban nevű Store <ResourceName>.psm1.</span><span class="sxs-lookup"><span data-stu-id="7ef04-135">Store these three functions in a file called <ResourceName>.psm1.</span></span> <span data-ttu-id="7ef04-136">A functions a következő példában egy Demo_IISWebsite.psm1 nevű fájlban vannak tárolva.</span><span class="sxs-lookup"><span data-stu-id="7ef04-136">In the following example, the functions are stored in a file called Demo_IISWebsite.psm1.</span></span>

> [!NOTE]
> <span data-ttu-id="7ef04-137">Az ugyanazon konfigurációs parancsfájl futtatásakor az erőforráson egynél többször, meg kell kapnia nincsenek hibák, és az erőforrás továbbra is ugyanazt az állapotot, a szkript futtatása után.</span><span class="sxs-lookup"><span data-stu-id="7ef04-137">When you run the same configuration script on your resource more than once, you should receive no errors and the resource should remain in the same state as running the script once.</span></span> <span data-ttu-id="7ef04-138">Ehhez ellenőrizze, hogy a **Get-TargetResource** és **Test-TargetResource** funkciók hagyja változatlanul az erőforrás és a meghívása a **Set-TargetResource**egynél többször ugyanezt a paramétert a sorrendben értékek 03T00 mindig egyszer ad meg, a függvény.</span><span class="sxs-lookup"><span data-stu-id="7ef04-138">To accomplish this, ensure that your **Get-TargetResource** and **Test-TargetResource** functions leave the resource unchanged, and that invoking the **Set-TargetResource** function more than once in a sequence with the same parameter values is always equivalent to invoking it once.</span></span>

<span data-ttu-id="7ef04-139">Az a **Get-TargetResource** függvény végrehajtása, a legfontosabb tulajdonságértékek biztosított paraméterek segítségével ellenőrizze a megadott erőforrás-példányának állapotát.</span><span class="sxs-lookup"><span data-stu-id="7ef04-139">In the **Get-TargetResource** function implementation, use the key resource property values that are provided as parameters to check the status of the specified resource instance.</span></span> <span data-ttu-id="7ef04-140">Ez a függvény egy kivonattábla, amely felsorolja a kulcsok és a tényleges értékek ezeket a tulajdonságokat, mint a megfelelő értékeket erőforrás-tulajdonságok kell visszaadnia.</span><span class="sxs-lookup"><span data-stu-id="7ef04-140">This function must return a hash table that lists all the resource properties as keys and the actual values of these properties as the corresponding values.</span></span> <span data-ttu-id="7ef04-141">A következő kód mutatja be.</span><span class="sxs-lookup"><span data-stu-id="7ef04-141">The following code provides an example.</span></span>

```powershell
# DSC uses the Get-TargetResource function to fetch the status of the resource instance specified in the parameters for the target machine
function Get-TargetResource
{
    param
    (
        [ValidateSet("Present", "Absent")]
        [string]$Ensure = "Present",

        [Parameter(Mandatory)]
        [ValidateNotNullOrEmpty()]
        [string]$Name,

        [Parameter(Mandatory)]
        [ValidateNotNullOrEmpty()]
        [string]$PhysicalPath,

        [ValidateSet("Started", "Stopped")]
        [string]$State = "Started",

        [string]$ApplicationPool,

        [string[]]$BindingInfo,

        [string[]]$Protocol
    )

        $getTargetResourceResult = $null;

        <# Insert logic that uses the mandatory parameter values to get the website and assign it to a variable called $Website #>
        <# Set $ensureResult to "Present" if the requested website exists and to "Absent" otherwise #>

        # Add all Website properties to the hash table
        # This simple example assumes that $Website is not null
        $getTargetResourceResult = @{
                                      Name = $Website.Name;
                                        Ensure = $ensureResult;
                                        PhysicalPath = $Website.physicalPath;
                                        State = $Website.state;
                                        ID = $Website.id;
                                        ApplicationPool = $Website.applicationPool;
                                        Protocol = $Website.bindings.Collection.protocol;
                                        Binding = $Website.bindings.Collection.bindingInformation;
                                    }

        $getTargetResourceResult;
}
```

<span data-ttu-id="7ef04-142">Attól függően, az értékeket, amelyeket a konfigurációs parancsfájlt, az erőforrás-tulajdonságok vannak megadva a **Set-TargetResource** tegye a következők egyikét:</span><span class="sxs-lookup"><span data-stu-id="7ef04-142">Depending on the values that are specified for the resource properties in the configuration script, the **Set-TargetResource** must do one of the following:</span></span>

* <span data-ttu-id="7ef04-143">Új webhely létrehozása</span><span class="sxs-lookup"><span data-stu-id="7ef04-143">Create a new website</span></span>
* <span data-ttu-id="7ef04-144">Egy létező webhely frissítése</span><span class="sxs-lookup"><span data-stu-id="7ef04-144">Update an existing website</span></span>
* <span data-ttu-id="7ef04-145">Egy létező webhely törlése</span><span class="sxs-lookup"><span data-stu-id="7ef04-145">Delete an existing website</span></span>

<span data-ttu-id="7ef04-146">A következő példa ezt mutatja be.</span><span class="sxs-lookup"><span data-stu-id="7ef04-146">The following example illustrates this.</span></span>

```powershell
# The Set-TargetResource function is used to create, delete or configure a website on the target machine.
function Set-TargetResource
{
    [CmdletBinding(SupportsShouldProcess=$true)]
    param
    (
        [ValidateSet("Present", "Absent")]
        [string]$Ensure = "Present",

        [Parameter(Mandatory)]
        [ValidateNotNullOrEmpty()]
        [string]$Name,

        [Parameter(Mandatory)]
        [ValidateNotNullOrEmpty()]
        [string]$PhysicalPath,

        [ValidateSet("Started", "Stopped")]
        [string]$State = "Started",

        [string]$ApplicationPool,

        [string[]]$BindingInfo,

        [string[]]$Protocol
    )

    <# If Ensure is set to "Present" and the website specified in the mandatory input parameters does not exist, then create it using the specified parameter values #>
    <# Else, if Ensure is set to "Present" and the website does exist, then update its properties to match the values provided in the non-mandatory parameter values #>
    <# Else, if Ensure is set to "Absent" and the website does not exist, then do nothing #>
    <# Else, if Ensure is set to "Absent" and the website does exist, then delete the website #>
}
```

<span data-ttu-id="7ef04-147">Végül a **Test-TargetResource** függvény végre kell hajtania állítja be ugyanezt a paramétert **Get-TargetResource** és **Set-TargetResource**.</span><span class="sxs-lookup"><span data-stu-id="7ef04-147">Finally, the **Test-TargetResource** function must take the same parameter set as **Get-TargetResource** and **Set-TargetResource**.</span></span> <span data-ttu-id="7ef04-148">A megvalósításában **Test-TargetResource**, az erőforrás-példány a fő paraméterekkel megadott állapotának ellenőrzéséhez.</span><span class="sxs-lookup"><span data-stu-id="7ef04-148">In your implementation of **Test-TargetResource**, check the status of the resource instance that is specified in the key parameters.</span></span> <span data-ttu-id="7ef04-149">A tényleges erőforrás-példány állapota nem felel meg a paraméterkészletet megadott értékeket, ha vissza **$false**.</span><span class="sxs-lookup"><span data-stu-id="7ef04-149">If the actual status of the resource instance does not match the values specified in the parameter set, return **$false**.</span></span> <span data-ttu-id="7ef04-150">Ellenkező esetben vissza **$true**.</span><span class="sxs-lookup"><span data-stu-id="7ef04-150">Otherwise, return **$true**.</span></span>

<span data-ttu-id="7ef04-151">A következő kód valósítja meg a **Test-TargetResource** függvény.</span><span class="sxs-lookup"><span data-stu-id="7ef04-151">The following code implements the **Test-TargetResource** function.</span></span>

```powershell
function Test-TargetResource
{
[CmdletBinding()]
[OutputType([System.Boolean])]
param
(
[ValidateSet("Present","Absent")]
[System.String]
$Ensure,

[parameter(Mandatory = $true)]
[System.String]
$Name,

[parameter(Mandatory = $true)]
[System.String]
$PhysicalPath,

[ValidateSet("Started","Stopped")]
[System.String]
$State,

[System.String[]]
$Protocol,

[System.String[]]
$BindingData,

[System.String]
$ApplicationPool
)

#Write-Verbose "Use this cmdlet to deliver information about command processing."

#Write-Debug "Use this cmdlet to write debug information while troubleshooting."


#Include logic to
$result = [System.Boolean]
#Add logic to test whether the website is present and its status mathes the supplied parameter values. If it does, return true. If it does not, return false.
$result
}
```

<span data-ttu-id="7ef04-152">**Megjegyzés:**: Könnyebb hibakeresés, használja a **Write-Verbose** parancsmagot az előző három funkció megvalósítását.</span><span class="sxs-lookup"><span data-stu-id="7ef04-152">**Note**: For easier debugging, use the **Write-Verbose** cmdlet in your implementation of the previous three functions.</span></span>
><span data-ttu-id="7ef04-153">Ez a parancsmag szöveget ír a részletes üzenet-adatfolyam.</span><span class="sxs-lookup"><span data-stu-id="7ef04-153">This cmdlet writes text to the verbose message stream.</span></span>
><span data-ttu-id="7ef04-154">Alapértelmezés szerint a részletes üzenet-adatfolyam nem jelenik meg, de értékét módosítsa úgy a megjelenítéséhez a **$VerbosePreference** változó vagy a használatával a **részletes** paraméter a DSC-parancsmagok = új.</span><span class="sxs-lookup"><span data-stu-id="7ef04-154">By default, the verbose message stream is not displayed, but you can display it by changing the value of the **$VerbosePreference** variable or by using the **Verbose** parameter in the DSC cmdlets = new.</span></span>

### <a name="creating-the-module-manifest"></a><span data-ttu-id="7ef04-155">A modul jegyzékfájl létrehozása</span><span class="sxs-lookup"><span data-stu-id="7ef04-155">Creating the module manifest</span></span>

<span data-ttu-id="7ef04-156">Végül a **New-ModuleManifest** meghatározásához a parancsmag egy <ResourceName>.psd1 fájlban az egyéni erőforrás-modulhoz.</span><span class="sxs-lookup"><span data-stu-id="7ef04-156">Finally, use the **New-ModuleManifest** cmdlet to define a <ResourceName>.psd1 file for your custom resource module.</span></span> <span data-ttu-id="7ef04-157">Ezzel a parancsmaggal indít el, ha az előző szakaszban leírt parancsfájl modul (.psm1) hivatkozik.</span><span class="sxs-lookup"><span data-stu-id="7ef04-157">When you invoke this cmdlet, reference the script module (.psm1) file described in the previous section.</span></span> <span data-ttu-id="7ef04-158">Például **Get-TargetResource**, **Set-TargetResource**, és **Test-TargetResource** exportálása funkciók listájában.</span><span class="sxs-lookup"><span data-stu-id="7ef04-158">Include **Get-TargetResource**, **Set-TargetResource**, and **Test-TargetResource** in the list of functions to export.</span></span> <span data-ttu-id="7ef04-159">Következő egy példa jegyzékfájl.</span><span class="sxs-lookup"><span data-stu-id="7ef04-159">Following is an example manifest file.</span></span>

```powershell
# Module manifest for module 'Demo.IIS.Website'
#
# Generated on: 1/10/2013
#

@{

# Script module or binary module file associated with this manifest.
# RootModule = ''

# Version number of this module.
ModuleVersion = '1.0'

# ID used to uniquely identify this module
GUID = '6AB5ED33-E923-41d8-A3A4-5ADDA2B301DE'

# Author of this module
Author = 'Contoso'

# Company or vendor of this module
CompanyName = 'Contoso'

# Copyright statement for this module
Copyright = 'Contoso. All rights reserved.'

# Description of the functionality provided by this module
Description = 'This Module is used to support the creation and configuration of IIS Websites through Get, Set and Test API on the DSC managed nodes.'

# Minimum version of the Windows PowerShell engine required by this module
PowerShellVersion = '4.0'

# Minimum version of the common language runtime (CLR) required by this module
CLRVersion = '4.0'

# Modules that must be imported into the global environment prior to importing this module
RequiredModules = @("WebAdministration")

# Modules to import as nested modules of the module specified in RootModule/ModuleToProcess
NestedModules = @("Demo_IISWebsite.psm1")

# Functions to export from this module
FunctionsToExport = @("Get-TargetResource", "Set-TargetResource", "Test-TargetResource")

# Cmdlets to export from this module
#CmdletsToExport = '*'

# HelpInfo URI of this module
# HelpInfoURI = ''
}
```

## <a name="supporting-psdscrunascredential"></a><span data-ttu-id="7ef04-160">PsDscRunAsCredential támogatása</span><span class="sxs-lookup"><span data-stu-id="7ef04-160">Supporting PsDscRunAsCredential</span></span>

><span data-ttu-id="7ef04-161">**Megjegyzés:** **PsDscRunAsCredential** a PowerShell 5.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="7ef04-161">**Note:** **PsDscRunAsCredential** is supported in PowerShell 5.0 and later.</span></span>

<span data-ttu-id="7ef04-162">A **PsDscRunAsCredential** tulajdonság használható [DSC-konfigurációk](../configurations/configurations.md) erőforrás letiltása, hogy az erőforrás alatt kell futtatni. egy meghatározott hitelesítő adatok megadásához.</span><span class="sxs-lookup"><span data-stu-id="7ef04-162">The **PsDscRunAsCredential** property can be used in [DSC configurations](../configurations/configurations.md) resource block to specify that the resource should be run under a specified set of credentials.</span></span>
<span data-ttu-id="7ef04-163">További információkért lásd: [DSC futtatása felhasználói hitelesítő adatokkal](../configurations/runAsUser.md).</span><span class="sxs-lookup"><span data-stu-id="7ef04-163">For more information, see [Running DSC with user credentials](../configurations/runAsUser.md).</span></span>

<span data-ttu-id="7ef04-164">A felhasználói környezet belül egy egyéni erőforrás elérésére, használhatja az automatikus változót `$PsDscContext`.</span><span class="sxs-lookup"><span data-stu-id="7ef04-164">To access the user context from within a custom resource, you can use the automatic variable `$PsDscContext`.</span></span>

<span data-ttu-id="7ef04-165">Például a következő kódot a felhasználói környezet, amelyben az erőforrás fut. a részletes kimeneti adatfolyamba volna írni:</span><span class="sxs-lookup"><span data-stu-id="7ef04-165">For example the following code would write the user context under which the resource is running to the verbose output stream:</span></span>

```powershell
if (PsDscContext.RunAsUser) {
    Write-Verbose "User: $PsDscContext.RunAsUser";
}
```

## <a name="rebooting-the-node"></a><span data-ttu-id="7ef04-166">A csomópont újraindítása</span><span class="sxs-lookup"><span data-stu-id="7ef04-166">Rebooting the Node</span></span>

<span data-ttu-id="7ef04-167">Ha a végrehajtott műveletek az `Set-TargetResource` függvény újra kell indítani, globális jelző használatával ossza meg az LCM kell újraindítani a csomópontot.</span><span class="sxs-lookup"><span data-stu-id="7ef04-167">If the actions taken in your `Set-TargetResource` function require a reboot, you can use a global flag to tell the LCM to reboot the Node.</span></span> <span data-ttu-id="7ef04-168">Az újraindítás közvetlenül után kerül sor a `Set-TargetResource` függvény lefutott.</span><span class="sxs-lookup"><span data-stu-id="7ef04-168">This reboot occurs directly after the `Set-TargetResource` function completes.</span></span>

<span data-ttu-id="7ef04-169">Belül a `Set-TargetResource` működik, adja hozzá a következő kódsort.</span><span class="sxs-lookup"><span data-stu-id="7ef04-169">Inside your `Set-TargetResource` function, add the following line of code.</span></span>

```powershell
# Include this line if the resource requires a system reboot.
$global:DSCMachineStatus = 1
```

<span data-ttu-id="7ef04-170">Ahhoz, hogy az LCM kell újraindítani a csomópontot a **RebootNodeIfNeeded** jelzőt kell beállítani `$true`.</span><span class="sxs-lookup"><span data-stu-id="7ef04-170">In order for the LCM to reboot the Node, the **RebootNodeIfNeeded** flag needs to be set to `$true`.</span></span> <span data-ttu-id="7ef04-171">A **ActionAfterReboot** beállítás is meg kell **ContinueConfiguration**, amely az alapértelmezett érték.</span><span class="sxs-lookup"><span data-stu-id="7ef04-171">The **ActionAfterReboot** setting should also be set to **ContinueConfiguration**, which is the default.</span></span> <span data-ttu-id="7ef04-172">Az LCM konfigurálása a további információkért lásd: [a Local Configuration Manager](../managing-nodes/metaConfig.md), vagy [a Local Configuration Manager (v4)](../managing-nodes/metaConfig4.md).</span><span class="sxs-lookup"><span data-stu-id="7ef04-172">For more information on configuring the LCM, see [Configuring the Local Configuration Manager](../managing-nodes/metaConfig.md), or [Configuring the Local Configuration Manager (v4)](../managing-nodes/metaConfig4.md).</span></span>
