---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: Egyéni DSC-erőforrás MOF írása
ms.openlocfilehash: 4e336e837d2153fecab8325cb8714ffed85a6175
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="writing-a-custom-dsc-resource-with-mof"></a><span data-ttu-id="ec17b-103">Egyéni DSC-erőforrás MOF írása</span><span class="sxs-lookup"><span data-stu-id="ec17b-103">Writing a custom DSC resource with MOF</span></span>

> <span data-ttu-id="ec17b-104">Vonatkozik: A Windows PowerShell 4.0-s verzióját, a Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="ec17b-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="ec17b-105">Ebben a témakörben rendszer MOF-fájlt ad meg egy Windows PowerShell kívánt állapot konfigurációs szolgáltatása (DSC) egyéni erőforrás sémáját, és az erőforrás valósítania egy olyan Windows PowerShell-parancsfájlt.</span><span class="sxs-lookup"><span data-stu-id="ec17b-105">In this topic, we will define the schema for a Windows PowerShell Desired State Configuration (DSC) custom resource in a MOF file, and implement the resource in a Windows PowerShell script file.</span></span> <span data-ttu-id="ec17b-106">Az egyéni erőforrás létrehozására és karbantartására egy webhely van.</span><span class="sxs-lookup"><span data-stu-id="ec17b-106">This custom resource is for creating and maintaining a web site.</span></span>

## <a name="creating-the-mof-schema"></a><span data-ttu-id="ec17b-107">A MOF-séma létrehozása</span><span class="sxs-lookup"><span data-stu-id="ec17b-107">Creating the MOF schema</span></span>

<span data-ttu-id="ec17b-108">A séma definiálja az erőforrás, amelyek képesek a DSC-konfigurációs parancsprogram tulajdonságait.</span><span class="sxs-lookup"><span data-stu-id="ec17b-108">The schema defines the properties of your resource that can be configured by a DSC configuration script.</span></span>

### <a name="folder-structure-for-a-mof-resource"></a><span data-ttu-id="ec17b-109">A MOF-erőforrások esetében mappaszerkezet</span><span class="sxs-lookup"><span data-stu-id="ec17b-109">Folder structure for a MOF resource</span></span>

<span data-ttu-id="ec17b-110">Egyéni DSC-erőforrás a MOF-séma szükséges, hozzon létre a következő mappaszerkezetet.</span><span class="sxs-lookup"><span data-stu-id="ec17b-110">To implement a DSC custom resource with a MOF schema, create the following folder structure.</span></span> <span data-ttu-id="ec17b-111">A MOF-séma Demo_IISWebsite.schema.mof fájlban van definiálva, és az erőforrást parancsprogram Demo_IISWebsite.psm1 van definiálva.</span><span class="sxs-lookup"><span data-stu-id="ec17b-111">The MOF schema is defined in the file Demo_IISWebsite.schema.mof, and the resource script is defined in Demo_IISWebsite.psm1.</span></span> <span data-ttu-id="ec17b-112">Másik lehetőségként létrehozhat egy modul jegyzékfájl (psd1 kiterjesztésű) fájlt.</span><span class="sxs-lookup"><span data-stu-id="ec17b-112">Optionally, you can create a module manifest (psd1) file.</span></span>

```
$env:ProgramFiles\WindowsPowerShell\Modules (folder)
    |- MyDscResources (folder)
        |- DSCResources (folder)
            |- Demo_IISWebsite (folder)
                |- Demo_IISWebsite.psd1 (file, optional)
                |- Demo_IISWebsite.psm1 (file, required)
                |- Demo_IISWebsite.schema.mof (file, required)
```

<span data-ttu-id="ec17b-113">Vegye figyelembe, hogy a legfelső szintű mappa alatt DSCResources nevű mappa létrehozásához szükséges, és, hogy a mappa minden erőforrás neve megegyezik az erőforrás kell rendelkeznie.</span><span class="sxs-lookup"><span data-stu-id="ec17b-113">Note that it is necessary to create a folder named DSCResources under the top-level folder, and that the folder for each resource must have the same name as the resource.</span></span>

### <a name="the-contents-of-the-mof-file"></a><span data-ttu-id="ec17b-114">A MOF-fájl tartalma</span><span class="sxs-lookup"><span data-stu-id="ec17b-114">The contents of the MOF file</span></span>

<span data-ttu-id="ec17b-115">Az alábbiakban látható egy példa MOF-fájlt egy egyéni webhely erőforrás használható.</span><span class="sxs-lookup"><span data-stu-id="ec17b-115">Following is an example MOF file that can be used for a custom website resource.</span></span> <span data-ttu-id="ec17b-116">Kövesse az alábbi példát, ebben a sémában mentése fájlba, és hívja meg a fájl *Demo_IISWebsite.schema.mof*.</span><span class="sxs-lookup"><span data-stu-id="ec17b-116">To follow this example, save this schema to a file, and call the file *Demo_IISWebsite.schema.mof*.</span></span>

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

<span data-ttu-id="ec17b-117">Vegye figyelembe az alábbiakat az előző kóddal:</span><span class="sxs-lookup"><span data-stu-id="ec17b-117">Note the following about the previous code:</span></span>

* <span data-ttu-id="ec17b-118">`FriendlyName` Tekintse meg az egyéni erőforrást DSC konfigurációs parancsfájlok segítségével nevet határoz meg.</span><span class="sxs-lookup"><span data-stu-id="ec17b-118">`FriendlyName` defines the name you can use to refer to this custom resource in DSC configuration scripts.</span></span> <span data-ttu-id="ec17b-119">Ebben a példában `Website` felel meg a rövid név `Archive` a beépített archív erőforrás.</span><span class="sxs-lookup"><span data-stu-id="ec17b-119">In this example, `Website` is equivalent to the friendly name `Archive` for the built-in Archive resource.</span></span>
* <span data-ttu-id="ec17b-120">Megadhatja az egyéni erőforrás kell származnia: az osztály `OMI_BaseResource`.</span><span class="sxs-lookup"><span data-stu-id="ec17b-120">The class you define for your custom resource must derive from `OMI_BaseResource`.</span></span>
* <span data-ttu-id="ec17b-121">A típus minősítő `[Key]`, a tulajdonság azt jelzi, hogy ezt a tulajdonságot egyedileg azonosítja a erőforráspéldány.</span><span class="sxs-lookup"><span data-stu-id="ec17b-121">The type qualifier, `[Key]`, on a property indicates that this property will uniquely identify the resource instance.</span></span> <span data-ttu-id="ec17b-122">Legalább egy `[Key]` tulajdonság megadása kötelező.</span><span class="sxs-lookup"><span data-stu-id="ec17b-122">At least one `[Key]` property is required.</span></span>
* <span data-ttu-id="ec17b-123">A `[Required]` minősítő azt jelzi, hogy a tulajdonság szükséges (értéket kell megadni az összes konfigurációs parancsfájl, amely ezt az erőforrást használ).</span><span class="sxs-lookup"><span data-stu-id="ec17b-123">The `[Required]` qualifier indicates that the property is required (a value must be specified in any configuration script that uses this resource).</span></span>
* <span data-ttu-id="ec17b-124">A `[write]` minősítő azt jelzi, hogy ez a tulajdonság opcionális konfigurációs parancsfájl az egyéni erőforrás használatakor.</span><span class="sxs-lookup"><span data-stu-id="ec17b-124">The `[write]` qualifier indicates that this property is optional when using the custom resource in a configuration script.</span></span> <span data-ttu-id="ec17b-125">A `[read]` minősítő azt jelzi, hogy a tulajdonság nem állítható be olyan konfigurációja, és csak jelentéskészítési célból van.</span><span class="sxs-lookup"><span data-stu-id="ec17b-125">The `[read]` qualifier indicates that a property cannot be set by a configuration, and is for reporting purposes only.</span></span>
* <span data-ttu-id="ec17b-126">`Values` korlátozza az értékeket, amelyek a meghatározott értékek listájának tulajdonság hozzárendelhető `ValueMap`.</span><span class="sxs-lookup"><span data-stu-id="ec17b-126">`Values` restricts the values that can be assigned to the property to the list of values defined in `ValueMap`.</span></span> <span data-ttu-id="ec17b-127">További információkért lásd: [ValueMap és érték minősítők](https://msdn.microsoft.com/library/windows/desktop/aa393965.aspx).</span><span class="sxs-lookup"><span data-stu-id="ec17b-127">For more information, see [ValueMap and Value Qualifiers](https://msdn.microsoft.com/library/windows/desktop/aa393965.aspx).</span></span>
* <span data-ttu-id="ec17b-128">Például egy tulajdonság nevű `Ensure` értékekkel `Present` és `Absent` egyik módja egy beépített DSC-erőforrások egységes stílust karbantartása javasolt az erőforrás.</span><span class="sxs-lookup"><span data-stu-id="ec17b-128">Including a property called `Ensure` with values `Present` and `Absent` in your resource is recommended as a way to maintain a consistent style with built-in DSC resources.</span></span>
* <span data-ttu-id="ec17b-129">A fájl az egyéni erőforrás neve az alábbiak szerint: `classname.schema.mof`, ahol `classname` az azonosító, amelyet a következő a `class` a sémadefiníciót kulcsszót.</span><span class="sxs-lookup"><span data-stu-id="ec17b-129">Name the schema file for your custom resource as follows: `classname.schema.mof`, where `classname` is the identifier that follows the `class` keyword in your schema definition.</span></span>

### <a name="writing-the-resource-script"></a><span data-ttu-id="ec17b-130">Az erőforrást parancsprogram írása</span><span class="sxs-lookup"><span data-stu-id="ec17b-130">Writing the resource script</span></span>

<span data-ttu-id="ec17b-131">Az erőforrást parancsprogram valósítja meg az erőforrás logikáját.</span><span class="sxs-lookup"><span data-stu-id="ec17b-131">The resource script implements the logic of the resource.</span></span> <span data-ttu-id="ec17b-132">Ebben a modulban, fel kell venni nevű három funkció **Get-TargetResource**, **Set-TargetResource**, és **teszt-TargetResource**.</span><span class="sxs-lookup"><span data-stu-id="ec17b-132">In this module, you must include three functions called **Get-TargetResource**, **Set-TargetResource**, and **Test-TargetResource**.</span></span> <span data-ttu-id="ec17b-133">Minden három funkciók kell tennie egy paraméter halmaza, amelyet a tulajdonságkészletbe, amelyet az erőforrás hozott létre a MOF-sémájában definiált azonos.</span><span class="sxs-lookup"><span data-stu-id="ec17b-133">All three functions must take a parameter set that is identical to the set of properties defined in the MOF schema that you created for your resource.</span></span> <span data-ttu-id="ec17b-134">Ebben a dokumentumban a tulajdonságkészletbe műveletek a "erőforrás-tulajdonságokat."</span><span class="sxs-lookup"><span data-stu-id="ec17b-134">In this document, this set of properties is referred to as the “resource properties.”</span></span> <span data-ttu-id="ec17b-135">Tárban, ezek három funkciók egy fájlban <ResourceName>.psm1.</span><span class="sxs-lookup"><span data-stu-id="ec17b-135">Store these three functions in a file called <ResourceName>.psm1.</span></span> <span data-ttu-id="ec17b-136">A következő példában a funkciók Demo_IISWebsite.psm1 nevű fájlban vannak tárolva.</span><span class="sxs-lookup"><span data-stu-id="ec17b-136">In the following example, the functions are stored in a file called Demo_IISWebsite.psm1.</span></span>

> <span data-ttu-id="ec17b-137">**Megjegyzés:**: a azonos konfigurációs parancsfájl futtatása a erőforráson egynél többször, nincs hiba kell kapnia, és egyszer fut a parancsfájl abban az állapotban maradjon. az erőforrás.</span><span class="sxs-lookup"><span data-stu-id="ec17b-137">**Note**: When you run the same configuration script on your resource more than once, you should receive no errors and the resource should remain in the same state as running the script once.</span></span> <span data-ttu-id="ec17b-138">Ennek megvalósítása érdekében ügyeljen arra, hogy a **Get-TargetResource** és **teszt-TargetResource** funkciók hagyja változatlanul az erőforrás, és adott meghívása a **Set-TargetResource**egynél többször a ugyanezt a paramétert sorozatba értékek megegyezik mindig egyszer hívja az működik.</span><span class="sxs-lookup"><span data-stu-id="ec17b-138">To accomplish this, ensure that your **Get-TargetResource** and **Test-TargetResource** functions leave the resource unchanged, and that invoking the **Set-TargetResource** function more than once in a sequence with the same parameter values is always equivalent to invoking it once.</span></span>

<span data-ttu-id="ec17b-139">Az a **Get-TargetResource** függvény végrehajtása, által biztosított kulcs erőforrás tulajdonságértéket paraméter segítségével tekintse meg a megadott erőforráspéldány.</span><span class="sxs-lookup"><span data-stu-id="ec17b-139">In the **Get-TargetResource** function implementation, use the key resource property values that are provided as parameters to check the status of the specified resource instance.</span></span> <span data-ttu-id="ec17b-140">Ez a függvény egy kivonattáblát a kulcsok és a tényleges értékek ezeket a tulajdonságokat, mint a megfelelő értékeket erőforrás-tulajdonságok felsoroló kell visszaadnia.</span><span class="sxs-lookup"><span data-stu-id="ec17b-140">This function must return a hash table that lists all the resource properties as keys and the actual values of these properties as the corresponding values.</span></span> <span data-ttu-id="ec17b-141">A következő kód példaként szolgál.</span><span class="sxs-lookup"><span data-stu-id="ec17b-141">The following code provides an example.</span></span>

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

<span data-ttu-id="ec17b-142">Attól függően, hogy az értékek, amelyek nincsenek megadva az erőforrás-tulajdonságok konfigurációs parancsfájl a **Set-TargetResource** tegye a következők egyikét:</span><span class="sxs-lookup"><span data-stu-id="ec17b-142">Depending on the values that are specified for the resource properties in the configuration script, the **Set-TargetResource** must do one of the following:</span></span>

* <span data-ttu-id="ec17b-143">Új webhely létrehozása</span><span class="sxs-lookup"><span data-stu-id="ec17b-143">Create a new website</span></span>
* <span data-ttu-id="ec17b-144">Frissítés egy meglévő webhelyen</span><span class="sxs-lookup"><span data-stu-id="ec17b-144">Update an existing website</span></span>
* <span data-ttu-id="ec17b-145">Egy meglévő webhelyen törlése</span><span class="sxs-lookup"><span data-stu-id="ec17b-145">Delete an existing website</span></span>

<span data-ttu-id="ec17b-146">A következő példa ezt mutatja be.</span><span class="sxs-lookup"><span data-stu-id="ec17b-146">The following example illustrates this.</span></span>

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

<span data-ttu-id="ec17b-147">Végezetül a **teszt-TargetResource** függvény állítja be ugyanazon paraméter szükséges **Get-TargetResource** és **Set-TargetResource**.</span><span class="sxs-lookup"><span data-stu-id="ec17b-147">Finally, the **Test-TargetResource** function must take the same parameter set as **Get-TargetResource** and **Set-TargetResource**.</span></span> <span data-ttu-id="ec17b-148">A megvalósításával **teszt-TargetResource**, tekintse meg a paramétereket a megadott erőforráspéldány.</span><span class="sxs-lookup"><span data-stu-id="ec17b-148">In your implementation of **Test-TargetResource**, check the status of the resource instance that is specified in the key parameters.</span></span> <span data-ttu-id="ec17b-149">Ha a tényleges állapot, az erőforrás-példány nem egyezik meg a paraméterhalmaz megadott értékeket, térjen vissza **$false**.</span><span class="sxs-lookup"><span data-stu-id="ec17b-149">If the actual status of the resource instance does not match the values specified in the parameter set, return **$false**.</span></span> <span data-ttu-id="ec17b-150">Ellenkező esetben a visszatérési **$true**.</span><span class="sxs-lookup"><span data-stu-id="ec17b-150">Otherwise, return **$true**.</span></span>

<span data-ttu-id="ec17b-151">A következő kódot valósít meg a **teszt-TargetResource** függvény.</span><span class="sxs-lookup"><span data-stu-id="ec17b-151">The following code implements the **Test-TargetResource** function.</span></span>

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

<span data-ttu-id="ec17b-152">**Megjegyzés:**: hibakereséshez egyszerűbb, használja a **Write-Verbose** parancsmag az előző három funkció megvalósítását.</span><span class="sxs-lookup"><span data-stu-id="ec17b-152">**Note**: For easier debugging, use the **Write-Verbose** cmdlet in your implementation of the previous three functions.</span></span>
><span data-ttu-id="ec17b-153">Ez a parancsmag szöveg ír a részletes üzenet-adatfolyam.</span><span class="sxs-lookup"><span data-stu-id="ec17b-153">This cmdlet writes text to the verbose message stream.</span></span>
><span data-ttu-id="ec17b-154">Alapértelmezés szerint a részletes üzenet-adatfolyam nem jelenik meg, de értékének módosításával megjelenítheti a **$VerbosePreference** változó vagy használatával a **részletes** a DSC-parancsmagok paraméter = új.</span><span class="sxs-lookup"><span data-stu-id="ec17b-154">By default, the verbose message stream is not displayed, but you can display it by changing the value of the **$VerbosePreference** variable or by using the **Verbose** parameter in the DSC cmdlets = new.</span></span>

### <a name="creating-the-module-manifest"></a><span data-ttu-id="ec17b-155">A modul jegyzékfájl létrehozása</span><span class="sxs-lookup"><span data-stu-id="ec17b-155">Creating the module manifest</span></span>

<span data-ttu-id="ec17b-156">Végül a **New-ModuleManifest** parancsmag használatával adja meg a <ResourceName>.psd1 fájlt az egyéni erőforrás modul.</span><span class="sxs-lookup"><span data-stu-id="ec17b-156">Finally, use the **New-ModuleManifest** cmdlet to define a <ResourceName>.psd1 file for your custom resource module.</span></span> <span data-ttu-id="ec17b-157">Ez a parancsmag meghívásakor hivatkozzon a parancsfájl (.psm1) modul az előző szakaszban leírt.</span><span class="sxs-lookup"><span data-stu-id="ec17b-157">When you invoke this cmdlet, reference the script module (.psm1) file described in the previous section.</span></span> <span data-ttu-id="ec17b-158">Tartalmaznak **Get-TargetResource**, **Set-TargetResource**, és **teszt-TargetResource** exportálása funkciók közül.</span><span class="sxs-lookup"><span data-stu-id="ec17b-158">Include **Get-TargetResource**, **Set-TargetResource**, and **Test-TargetResource** in the list of functions to export.</span></span> <span data-ttu-id="ec17b-159">Az alábbiakban látható egy példa jegyzékfájlt.</span><span class="sxs-lookup"><span data-stu-id="ec17b-159">Following is an example manifest file.</span></span>

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

## <a name="supporting-psdscrunascredential"></a><span data-ttu-id="ec17b-160">PsDscRunAsCredential támogatása</span><span class="sxs-lookup"><span data-stu-id="ec17b-160">Supporting PsDscRunAsCredential</span></span>

><span data-ttu-id="ec17b-161">**Megjegyzés:** **PsDscRunAsCredential** PowerShell 5.0-s vagy újabb támogatott.</span><span class="sxs-lookup"><span data-stu-id="ec17b-161">**Note:** **PsDscRunAsCredential** is supported in PowerShell 5.0 and later.</span></span>

<span data-ttu-id="ec17b-162">A **PsDscRunAsCredential** tulajdonság használható [a DSC-konfigurációk](configurations.md) erőforrás blokk adhatja meg, hogy az erőforrás verziója alatt kell futtatni a megadott hitelesítő adatok készletét.</span><span class="sxs-lookup"><span data-stu-id="ec17b-162">The **PsDscRunAsCredential** property can be used in [DSC configurations](configurations.md) resource block to specify that the resource should be run under a specified set of credentials.</span></span>
<span data-ttu-id="ec17b-163">További információkért lásd: [felhasználói hitelesítő adatokkal rendelkező futtató DSC](runAsUser.md).</span><span class="sxs-lookup"><span data-stu-id="ec17b-163">For more information, see [Running DSC with user credentials](runAsUser.md).</span></span>

<span data-ttu-id="ec17b-164">A felhasználói környezet belül egyéni erőforrás eléréséhez használhatja az automatikus változó `$PsDscContext`.</span><span class="sxs-lookup"><span data-stu-id="ec17b-164">To access the user context from within a custom resource, you can use the automatic variable `$PsDscContext`.</span></span>

<span data-ttu-id="ec17b-165">Például a következő kódot a felhasználói környezet, amely alatt az erőforrás fut, a részletes kimeneti adatfolyamba lesz írási:</span><span class="sxs-lookup"><span data-stu-id="ec17b-165">For example the following code would write the user context under which the resource is running to the verbose output stream:</span></span>

```powershell
if (PsDscContext.RunAsUser) {
    Write-Verbose "User: $PsDscContext.RunAsUser";
}
```