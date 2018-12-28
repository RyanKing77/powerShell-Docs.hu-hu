---
ms.date: 06/12/2017
contributor: manikb
keywords: katalógus, powershell, a parancsmag, psget
title: Kompatibilis PowerShell-kiadások rendelkező modulok
ms.openlocfilehash: bda924393d37ea1596fbf0d813c10cbdea33c218
ms.sourcegitcommit: 548547b2d5fc73e726bb9fec6175d452a351d975
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/20/2018
ms.locfileid: "53655327"
---
# <a name="modules-with-compatible-powershell-editions"></a><span data-ttu-id="4a560-103">Kompatibilis PowerShell-kiadások rendelkező modulok</span><span class="sxs-lookup"><span data-stu-id="4a560-103">Modules with compatible PowerShell Editions</span></span>

<span data-ttu-id="4a560-104">Az 5.1-es verziótól kezdődően a PowerShell különböző kiadásokban érhető el, amelyek különböző szolgáltatáskészleteket és platformkompatibilitást kínálnak.</span><span class="sxs-lookup"><span data-stu-id="4a560-104">Starting with version 5.1, PowerShell is available in different editions which denote varying feature sets and platform compatibility.</span></span>

- <span data-ttu-id="4a560-105">**Desktop kiadás:** .NET-keretrendszer épül, és kompatibilis a Windows például a Server Core és a Windows asztal teljes erőforrás-igényű kiadásain fut PowerShell-verziókat célzó szkriptekhez és modulokhoz biztosít.</span><span class="sxs-lookup"><span data-stu-id="4a560-105">**Desktop Edition:** Built on .NET Framework and provides compatibility with scripts and modules targeting versions of PowerShell running on full footprint editions of Windows such as Server Core and Windows Desktop.</span></span>
- <span data-ttu-id="4a560-106">**Core kiadás:** .NET Core épül, és kompatibilis csökkentett erőforrás-igényű kiadása esetén például a Nano Server Windows és Windows IoT kiadásokon futtatott PowerShell-verziókat célzó szkriptekhez és modulokhoz biztosít.</span><span class="sxs-lookup"><span data-stu-id="4a560-106">**Core Edition:** Built on .NET Core and provides compatibility with scripts and modules targeting versions of PowerShell running on reduced footprint editions of Windows such as Nano Server and Windows IoT.</span></span>

<span data-ttu-id="4a560-107">A futó használni kívánt PowerShell PSEdition tulajdonságában jelenik meg `$PSVersionTable`.</span><span class="sxs-lookup"><span data-stu-id="4a560-107">The running edition of PowerShell is shown in the PSEdition property of `$PSVersionTable`.</span></span>

```powershell
$PSVersionTable
```

```output
Name                           Value
----                           -----
PSVersion                      5.1.14300.1000
PSEdition                      Desktop
PSCompatibleVersions           {1.0, 2.0, 3.0, 4.0...}
CLRVersion                     4.0.30319.42000
BuildVersion                   10.0.14300.1000
WSManStackVersion              3.0
PSRemotingProtocolVersion      2.3
SerializationVersion           1.1.0.1
```

## <a name="declaring-compatible-editions"></a><span data-ttu-id="4a560-108">Deklaráló kompatibilis verziója esetén</span><span class="sxs-lookup"><span data-stu-id="4a560-108">Declaring compatible editions</span></span>

<span data-ttu-id="4a560-109">A modulkészítők a CompatiblePSEditions moduljegyzékkulcs segítségével deklarálhatják, hogy a moduljaik mely PowerShell-kiadással vagy -kiadásokkal kompatibilisek.</span><span class="sxs-lookup"><span data-stu-id="4a560-109">Module authors can declare their modules to be compatible with one or more PowerShell editions using the CompatiblePSEditions module manifest key.</span></span> <span data-ttu-id="4a560-110">Ez a kulcs csak a PowerShell 5.1-es vagy újabb verzióin támogatott.</span><span class="sxs-lookup"><span data-stu-id="4a560-110">This key is only supported on PowerShell 5.1 or later.</span></span>

> [!NOTE]
> <span data-ttu-id="4a560-111">Miután egy moduljegyzék CompatiblePSEditions a kulccsal van megadva, nem importálható lesz PowerShell alacsonyabb verzióiban.</span><span class="sxs-lookup"><span data-stu-id="4a560-111">Once a module manifest is specified with the CompatiblePSEditions key, it can not be imported on lower versions of PowerShell.</span></span>

```powershell
New-ModuleManifest -Path .\TestModuleWithEdition.psd1 -CompatiblePSEditions Desktop,Core -PowerShellVersion 5.1
$ModuleInfo = Test-ModuleManifest -Path .\TestModuleWithEdition.psd1
$ModuleInfo.CompatiblePSEditions
```

```output
Desktop
Core
```

```powershell
$ModuleInfo | Get-Member CompatiblePSEditions
```

```output
   TypeName: System.Management.Automation.PSModuleInfo

Name                 MemberType Definition
----                 ---------- ----------
CompatiblePSEditions Property   System.Collections.Generic.IEnumerable[string] CompatiblePSEditions {get;}
```

<span data-ttu-id="4a560-112">Az elérhető modulok listáját szűrheti a PowerShell-kiadás alapján.</span><span class="sxs-lookup"><span data-stu-id="4a560-112">When getting a list of available modules, you can filter the list by PowerShell edition.</span></span>

```powershell
Get-Module -ListAvailable -PSEdition Desktop
```

```output
    Directory: C:\Program Files\WindowsPowerShell\Modules


ModuleType Version    Name                                ExportedCommands
---------- -------    ----                                ----------------
Manifest   1.0        ModuleWithPSEditions
```

```powershell
Get-Module -ListAvailable -PSEdition Core | % CompatiblePSEditions
```

```output
Desktop
Core
```

## <a name="targeting-multiple-editions"></a><span data-ttu-id="4a560-113">Célzás több kiadás</span><span class="sxs-lookup"><span data-stu-id="4a560-113">Targeting multiple editions</span></span>

<span data-ttu-id="4a560-114">A modul szerzők esetleg mindkét PowerShell-kiadások (asztalon és Core) célzó egy modul teheti közzé.</span><span class="sxs-lookup"><span data-stu-id="4a560-114">Module authors can publish a single module targeting to either or both PowerShell editions (Desktop and Core).</span></span>

<span data-ttu-id="4a560-115">Egy modul dolgozhat asztali és a Core kiadás, az adott modul Szerző hozzáadásához szükséges logikát, vagy a RootModule, vagy a moduljegyzékben $PSEdition változóval rendelkezik.</span><span class="sxs-lookup"><span data-stu-id="4a560-115">A single module can work on both Desktop and Core editions, in that module author has to add required logic in either RootModule or in the module manifest using $PSEdition variable.</span></span> <span data-ttu-id="4a560-116">Modulok lefordított DLL-ek CoreCLR-és FullCLR két készletnyi is rendelkezhet.</span><span class="sxs-lookup"><span data-stu-id="4a560-116">Modules can have two sets of compiled DLLs targeting both CoreCLR and FullCLR.</span></span> <span data-ttu-id="4a560-117">Az alábbiakban a több, a modul megfelelő DLL betöltésére szolgáló logikai csomag lehetőség közül választhat.</span><span class="sxs-lookup"><span data-stu-id="4a560-117">Here are the couple of options to package your module with logic for loading proper dlls.</span></span>

### <a name="option-1-packaging-a-module-for-targeting-multiple-versions-and-multiple-editions-of-powershell"></a><span data-ttu-id="4a560-118">1. lehetőség: A célcsoport-kezelési több verziói és több a PowerShell modul csomagolása</span><span class="sxs-lookup"><span data-stu-id="4a560-118">Option 1: Packaging a module for targeting multiple versions and multiple editions of PowerShell</span></span>

<span data-ttu-id="4a560-119">A modul mappa tartalma</span><span class="sxs-lookup"><span data-stu-id="4a560-119">Module folder contents</span></span>

- <span data-ttu-id="4a560-120">Microsoft.Windows.PowerShell.ScriptAnalyzer.BuiltinRules.dll</span><span class="sxs-lookup"><span data-stu-id="4a560-120">Microsoft.Windows.PowerShell.ScriptAnalyzer.BuiltinRules.dll</span></span>
- <span data-ttu-id="4a560-121">Microsoft.Windows.PowerShell.ScriptAnalyzer.dll</span><span class="sxs-lookup"><span data-stu-id="4a560-121">Microsoft.Windows.PowerShell.ScriptAnalyzer.dll</span></span>
- <span data-ttu-id="4a560-122">PSScriptAnalyzer.psd1</span><span class="sxs-lookup"><span data-stu-id="4a560-122">PSScriptAnalyzer.psd1</span></span>
- <span data-ttu-id="4a560-123">PSScriptAnalyzer.psm1</span><span class="sxs-lookup"><span data-stu-id="4a560-123">PSScriptAnalyzer.psm1</span></span>
- <span data-ttu-id="4a560-124">ScriptAnalyzer.format.ps1xml</span><span class="sxs-lookup"><span data-stu-id="4a560-124">ScriptAnalyzer.format.ps1xml</span></span>
- <span data-ttu-id="4a560-125">ScriptAnalyzer.types.ps1xml</span><span class="sxs-lookup"><span data-stu-id="4a560-125">ScriptAnalyzer.types.ps1xml</span></span>
- <span data-ttu-id="4a560-126">coreclr\Microsoft.Windows.PowerShell.ScriptAnalyzer.BuiltinRules.dll</span><span class="sxs-lookup"><span data-stu-id="4a560-126">coreclr\Microsoft.Windows.PowerShell.ScriptAnalyzer.BuiltinRules.dll</span></span>
- <span data-ttu-id="4a560-127">coreclr\Microsoft.Windows.PowerShell.ScriptAnalyzer.dll</span><span class="sxs-lookup"><span data-stu-id="4a560-127">coreclr\Microsoft.Windows.PowerShell.ScriptAnalyzer.dll</span></span>
- <span data-ttu-id="4a560-128">en-US\about_PSScriptAnalyzer.help.txt</span><span class="sxs-lookup"><span data-stu-id="4a560-128">en-US\about_PSScriptAnalyzer.help.txt</span></span>
- <span data-ttu-id="4a560-129">en-US\Microsoft.Windows.PowerShell.ScriptAnalyzer.dll-Help.xml</span><span class="sxs-lookup"><span data-stu-id="4a560-129">en-US\Microsoft.Windows.PowerShell.ScriptAnalyzer.dll-Help.xml</span></span>
- <span data-ttu-id="4a560-130">PSv3\Microsoft.Windows.PowerShell.ScriptAnalyzer.BuiltinRules.dll</span><span class="sxs-lookup"><span data-stu-id="4a560-130">PSv3\Microsoft.Windows.PowerShell.ScriptAnalyzer.BuiltinRules.dll</span></span>
- <span data-ttu-id="4a560-131">PSv3\Microsoft.Windows.PowerShell.ScriptAnalyzer.dll</span><span class="sxs-lookup"><span data-stu-id="4a560-131">PSv3\Microsoft.Windows.PowerShell.ScriptAnalyzer.dll</span></span>
- <span data-ttu-id="4a560-132">Settings\CmdletDesign.psd1</span><span class="sxs-lookup"><span data-stu-id="4a560-132">Settings\CmdletDesign.psd1</span></span>
- <span data-ttu-id="4a560-133">Settings\DSC.psd1</span><span class="sxs-lookup"><span data-stu-id="4a560-133">Settings\DSC.psd1</span></span>
- <span data-ttu-id="4a560-134">Settings\ScriptFunctions.psd1</span><span class="sxs-lookup"><span data-stu-id="4a560-134">Settings\ScriptFunctions.psd1</span></span>
- <span data-ttu-id="4a560-135">Settings\ScriptingStyle.psd1</span><span class="sxs-lookup"><span data-stu-id="4a560-135">Settings\ScriptingStyle.psd1</span></span>
- <span data-ttu-id="4a560-136">Settings\ScriptSecurity.psd1</span><span class="sxs-lookup"><span data-stu-id="4a560-136">Settings\ScriptSecurity.psd1</span></span>

<span data-ttu-id="4a560-137">Contents of PSScriptAnalyzer.psd1 file</span><span class="sxs-lookup"><span data-stu-id="4a560-137">Contents of PSScriptAnalyzer.psd1 file</span></span>

```powershell
@{

# Author of this module
Author = 'Microsoft Corporation'

# Script module or binary module file associated with this manifest.
RootModule = 'PSScriptAnalyzer.psm1'

# Version number of this module.
ModuleVersion = '1.6.1'

# ---
}
```

<span data-ttu-id="4a560-138">Alább logikai betölti a szükséges szerelvényeket, attól függően, a jelenlegi kiadása vagy verziója.</span><span class="sxs-lookup"><span data-stu-id="4a560-138">Below logic loads the required assemblies depending on the current edition or version.</span></span>

<span data-ttu-id="4a560-139">PSScriptAnalyzer.psm1 fájl tartalma:</span><span class="sxs-lookup"><span data-stu-id="4a560-139">Contents of PSScriptAnalyzer.psm1 file:</span></span>

```powershell
#
# Script module for module 'PSScriptAnalyzer'
#
Set-StrictMode -Version Latest

# Set up some helper variables to make it easier to work with the module
$PSModule = $ExecutionContext.SessionState.Module
$PSModuleRoot = $PSModule.ModuleBase

# Import the appropriate nested binary module based on the current PowerShell version
$binaryModuleRoot = $PSModuleRoot


if (($PSVersionTable.Keys -contains "PSEdition") -and ($PSVersionTable.PSEdition -ne 'Desktop')) {
    $binaryModuleRoot = Join-Path -Path $PSModuleRoot -ChildPath 'coreclr'
}
else
{
    if ($PSVersionTable.PSVersion -lt [Version]'5.0')
    {
        $binaryModuleRoot = Join-Path -Path $PSModuleRoot -ChildPath 'PSv3'
    }
}

$binaryModulePath = Join-Path -Path $binaryModuleRoot -ChildPath 'Microsoft.Windows.PowerShell.ScriptAnalyzer.dll'
$binaryModule = Import-Module -Name $binaryModulePath -PassThru

# When the module is unloaded, remove the nested binary module that was loaded with it
$PSModule.OnRemove = {
    Remove-Module -ModuleInfo $binaryModule
}
```

### <a name="option-2-use-psedition-variable-in-the-psd1-file-to-load-the-proper-dlls-and-nestedrequired-modules"></a><span data-ttu-id="4a560-140">2. lehetőség: A psd1 kiterjesztésű fájl $PSEdition változó segítségével a megfelelő DLL-EK és a beágyazott/szükséges modulok betöltése</span><span class="sxs-lookup"><span data-stu-id="4a560-140">Option 2: Use $PSEdition variable in the PSD1 file to load the proper DLLs and Nested/Required modules</span></span>

<span data-ttu-id="4a560-141">A PS 5.1-es vagy újabb a modul jegyzékfájl $PSEdition globális változó használata engedélyezett.</span><span class="sxs-lookup"><span data-stu-id="4a560-141">In PS 5.1 or newer, $PSEdition global variable is allowed in the module manifest file.</span></span> <span data-ttu-id="4a560-142">Használja ezt a változót, a modul Szerző értékeket adhat meg a feltételes modul jegyzékfájl.</span><span class="sxs-lookup"><span data-stu-id="4a560-142">Using this variable, module author can specify the conditional values in the module manifest file.</span></span> <span data-ttu-id="4a560-143">A korlátozott nyelvmód vagy adatok szakasz $PSEdition változó lehet hivatkozni.</span><span class="sxs-lookup"><span data-stu-id="4a560-143">$PSEdition variable can be referenced in restricted language mode or a Data section.</span></span>

> [!NOTE]
> <span data-ttu-id="4a560-144">Miután egy moduljegyzék a CompatiblePSEditions kulcs meg van adva, vagy használja a `$PSEdition` változó, nem importálható lesz a kisebb PowerShell-verziókat.</span><span class="sxs-lookup"><span data-stu-id="4a560-144">Once a module manifest is specified with the CompatiblePSEditions key or uses `$PSEdition` variable, it can not be imported on lower versions of PowerShell.</span></span>

<span data-ttu-id="4a560-145">Minta modul jegyzékfájl CompatiblePSEditions kulccsal</span><span class="sxs-lookup"><span data-stu-id="4a560-145">Sample module manifest file with CompatiblePSEditions key</span></span>

```powershell
@{
    # Script module or binary module file associated with this manifest.
    RootModule = if($PSEdition -eq 'Core')
    {
        'coreclr\MyCoreClrRM.dll'
    }
    else # Desktop
    {
        'clr\MyFullClrRM.dll'
    }

    # Supported PSEditions
    CompatiblePSEditions = 'Desktop', 'Core'

    # Modules to import as nested modules of the module specified in RootModule/ModuleToProcess
    NestedModules = if($PSEdition -eq 'Core')
    {
        'coreclr\MyCoreClrNM1.dll',
        'coreclr\MyCoreClrNM2.dll'
    }
    else # Desktop
    {
        'clr\MyFullClrNM1.dll',
        'clr\MyFullClrNM2.dll'
    }
}
```

### <a name="module-contents"></a><span data-ttu-id="4a560-146">A modul tartalma</span><span class="sxs-lookup"><span data-stu-id="4a560-146">Module contents</span></span>

```powershell
dir -Recurse
```

```output
    Directory: C:\Users\manikb\Documents\WindowsPowerShell\Modules\ModuleWithEditions

Mode           LastWriteTime   Length Name
----           -------------   ------ ----
d-----    7/5/2016   1:37 PM          clr
d-----    7/5/2016   1:36 PM          coreclr
-a----    7/5/2016   1:34 PM     4906 ModuleWithEditions.psd1

    Directory: C:\Users\manikb\Documents\WindowsPowerShell\Modules\ModuleWithEditions\clr

Mode           LastWriteTime    Length Name
----           -------------    ------ ----
-a----    7/5/2016   1:35 PM         0 MyFullClrNM1.dll
-a----    7/5/2016   1:35 PM         0 MyFullClrNM2.dll
-a----    7/5/2016   1:35 PM         0 MyFullClrRM.dl

    Directory: C:\Users\manikb\Documents\WindowsPowerShell\Modules\ModuleWithEditions\coreclr

Mode           LastWriteTime   Length Name
----           -------------   ------ ----
-a----    7/5/2016   1:35 PM        0 MyCoreClrNM1.dll
-a----    7/5/2016   1:35 PM        0 MyCoreClrNM2.dll
-a----    7/5/2016   1:35 PM        0 MyCoreClrRM.dl
```

<span data-ttu-id="4a560-147">PowerShell-galériából felhasználók egy adott PowerShell kiadás támogatott modulok listáját megtalálhatja, PSEdition_Desktop és PSEdition_Core címkék használatával.</span><span class="sxs-lookup"><span data-stu-id="4a560-147">PowerShell Gallery users can find the list of modules supported on a specific PowerShell Edition using tags PSEdition_Desktop and PSEdition_Core.</span></span>

<span data-ttu-id="4a560-148">Modulok PSEdition_Desktop és PSEdition_Core címkék nélküli minősülnek jól működnek az PowerShell asztali verziója esetén.</span><span class="sxs-lookup"><span data-stu-id="4a560-148">Modules without PSEdition_Desktop and PSEdition_Core tags are considered to work fine on PowerShell Desktop editions.</span></span>

```powershell
# Find modules supported on PowerShell Desktop edition
Find-Module -Tag PSEdition_Desktop

# Find modules supported on PowerShell Core editions
Find-Module -Tag PSEdition_Core
```

## <a name="more-details"></a><span data-ttu-id="4a560-149">További részletek</span><span class="sxs-lookup"><span data-stu-id="4a560-149">More details</span></span>

[<span data-ttu-id="4a560-150">PSEditions paraméterrel rendelkező parancsfájlok</span><span class="sxs-lookup"><span data-stu-id="4a560-150">Scripts with PSEditions</span></span>](script-psedition-support.md)

[<span data-ttu-id="4a560-151">Pseditions paraméterrel támogatja a PowerShell-Galériabeli</span><span class="sxs-lookup"><span data-stu-id="4a560-151">PSEditions support on PowerShellGallery</span></span>](../how-to/finding-packages/searching-by-compatibility.md)

[<span data-ttu-id="4a560-152">Moduljegyzék frissítése</span><span class="sxs-lookup"><span data-stu-id="4a560-152">Update module manifest</span></span>](/powershell/module/powershellget/update-modulemanifest)
