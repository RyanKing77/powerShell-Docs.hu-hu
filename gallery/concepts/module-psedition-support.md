---
ms.date: 06/12/2017
contributor: manikb
keywords: katalógus, powershell, a parancsmag, psget
title: Kompatibilis PowerShell-kiadások rendelkező modulok
ms.openlocfilehash: 2b11d833e7abc50f26b1581f678b9509a098c2c5
ms.sourcegitcommit: 77f62a55cac8c13d69d51eef5fade18f71d66955
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/17/2018
ms.locfileid: "39093524"
---
# <a name="modules-with-compatible-powershell-editions"></a><span data-ttu-id="3a0e2-103">Kompatibilis PowerShell-kiadások rendelkező modulok</span><span class="sxs-lookup"><span data-stu-id="3a0e2-103">Modules with compatible PowerShell Editions</span></span>

<span data-ttu-id="3a0e2-104">Az 5.1-es verziótól kezdődően a PowerShell különböző kiadásokban érhető el, amelyek különböző szolgáltatáskészleteket és platformkompatibilitást kínálnak.</span><span class="sxs-lookup"><span data-stu-id="3a0e2-104">Starting with version 5.1, PowerShell is available in different editions which denote varying feature sets and platform compatibility.</span></span>

- <span data-ttu-id="3a0e2-105">**Desktop kiadás:** A .NET-keretrendszeren alapul, és a Windows teljes erőforrás-igényű kiadásain, például a Server Core és a Windows asztali kiadásain futtatott PowerShell-verziókat célzó szkriptekhez és modulokhoz biztosít kompatibilitást.</span><span class="sxs-lookup"><span data-stu-id="3a0e2-105">**Desktop Edition:** Built on .NET Framework and provides compatibility with scripts and modules targeting versions of PowerShell running on full footprint editions of Windows such as Server Core and Windows Desktop.</span></span>
- <span data-ttu-id="3a0e2-106">**Core kiadás:** .NET Core-on alapul, és a Windows csökkentett erőforrás-igényű kiadásain, például a Nano Serveren és a Windows IoT kiadásokon futtatott PowerShell-verziókat célzó szkriptekhez és modulokhoz biztosít kompatibilitást.</span><span class="sxs-lookup"><span data-stu-id="3a0e2-106">**Core Edition:** Built on .NET Core and provides compatibility with scripts and modules targeting versions of PowerShell running on reduced footprint editions of Windows such as Nano Server and Windows IoT.</span></span>

## <a name="the-running-edition-of-powershell-is-shown-in-the-psedition-property-of-psversiontable"></a><span data-ttu-id="3a0e2-107">A futtatott PowerShell-verzió a $PSVersionTable PSEdition tulajdonságában jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="3a0e2-107">The running edition of PowerShell is shown in the PSEdition property of $PSVersionTable.</span></span>

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

## <a name="module-authors-can-declare-their-modules-to-be-compatible-with-one-or-more-powershell-editions-using-the-compatiblepseditions-module-manifest-key-this-key-is-only-supported-on-powershell-51-or-later"></a><span data-ttu-id="3a0e2-108">A modulkészítők a CompatiblePSEditions moduljegyzékkulcs segítségével deklarálhatják, hogy a moduljaik mely PowerShell-kiadással vagy -kiadásokkal kompatibilisek.</span><span class="sxs-lookup"><span data-stu-id="3a0e2-108">Module authors can declare their modules to be compatible with one or more PowerShell editions using the CompatiblePSEditions module manifest key.</span></span> <span data-ttu-id="3a0e2-109">Ez a kulcs csak a PowerShell 5.1-es vagy újabb verzióin támogatott.</span><span class="sxs-lookup"><span data-stu-id="3a0e2-109">This key is only supported on PowerShell 5.1 or later.</span></span>

> [!NOTE]
> <span data-ttu-id="3a0e2-110">Miután egy moduljegyzék CompatiblePSEditions a kulccsal van megadva, nem importálható lesz PowerShell alacsonyabb verzióiban.</span><span class="sxs-lookup"><span data-stu-id="3a0e2-110">Once a module manifest is specified with the CompatiblePSEditions key, it can not be imported on lower versions of PowerShell.</span></span>

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

<span data-ttu-id="3a0e2-111">Az elérhető modulok listáját szűrheti a PowerShell-kiadás alapján.</span><span class="sxs-lookup"><span data-stu-id="3a0e2-111">When getting a list of available modules, you can filter the list by PowerShell edition.</span></span>

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

## <a name="module-authors-can-publish-a-single-module-targeting-to-either-or-both-powershell-editions-desktop-and-core"></a><span data-ttu-id="3a0e2-112">A modul szerzők teheti közzé egy egy modul a célcsoport-kezelési egyik vagy mindkét PowerShell-kiadások (asztalon és mag)</span><span class="sxs-lookup"><span data-stu-id="3a0e2-112">Module authors can publish a single module targeting to either or both PowerShell editions (Desktop and Core)</span></span>

<span data-ttu-id="3a0e2-113">Egy modul dolgozhat asztali és a Core kiadás, az adott modul Szerző hozzáadásához szükséges logikát, vagy a RootModule, vagy a moduljegyzékben $PSEdition változóval rendelkezik.</span><span class="sxs-lookup"><span data-stu-id="3a0e2-113">A single module can work on both Desktop and Core editions, in that module author has to add required logic in either RootModule or in the module manifest using $PSEdition variable.</span></span>
<span data-ttu-id="3a0e2-114">Modulok lefordított DLL-ek CoreCLR-és FullCLR két készletnyi is rendelkezhet.</span><span class="sxs-lookup"><span data-stu-id="3a0e2-114">Modules can have two sets of compiled DLLs targeting both CoreCLR and FullCLR.</span></span>
<span data-ttu-id="3a0e2-115">Az alábbiakban a több, a modul megfelelő DLL betöltésére szolgáló logikai csomag lehetőség közül választhat.</span><span class="sxs-lookup"><span data-stu-id="3a0e2-115">Here are the couple of options to package your module with logic for loading proper dlls.</span></span>

### <a name="option-1-packaging-a-module-for-targeting-multiple-versions-and-multiple-editions-of-powershell"></a><span data-ttu-id="3a0e2-116">1. lehetőség: Csomagolására hajthatja végre a több verziói és több a PowerShell modul</span><span class="sxs-lookup"><span data-stu-id="3a0e2-116">Option 1: Packaging a module for targeting multiple versions and multiple editions of PowerShell</span></span>

#### <a name="module-folder-contents"></a><span data-ttu-id="3a0e2-117">A modul mappa tartalma</span><span class="sxs-lookup"><span data-stu-id="3a0e2-117">Module folder contents</span></span>

- <span data-ttu-id="3a0e2-118">Microsoft.Windows.PowerShell.ScriptAnalyzer.BuiltinRules.dll</span><span class="sxs-lookup"><span data-stu-id="3a0e2-118">Microsoft.Windows.PowerShell.ScriptAnalyzer.BuiltinRules.dll</span></span>
- <span data-ttu-id="3a0e2-119">Microsoft.Windows.PowerShell.ScriptAnalyzer.dll</span><span class="sxs-lookup"><span data-stu-id="3a0e2-119">Microsoft.Windows.PowerShell.ScriptAnalyzer.dll</span></span>
- <span data-ttu-id="3a0e2-120">PSScriptAnalyzer.psd1</span><span class="sxs-lookup"><span data-stu-id="3a0e2-120">PSScriptAnalyzer.psd1</span></span>
- <span data-ttu-id="3a0e2-121">PSScriptAnalyzer.psm1</span><span class="sxs-lookup"><span data-stu-id="3a0e2-121">PSScriptAnalyzer.psm1</span></span>
- <span data-ttu-id="3a0e2-122">ScriptAnalyzer.format.ps1xml</span><span class="sxs-lookup"><span data-stu-id="3a0e2-122">ScriptAnalyzer.format.ps1xml</span></span>
- <span data-ttu-id="3a0e2-123">ScriptAnalyzer.types.ps1xml</span><span class="sxs-lookup"><span data-stu-id="3a0e2-123">ScriptAnalyzer.types.ps1xml</span></span>
- <span data-ttu-id="3a0e2-124">coreclr\Microsoft.Windows.PowerShell.ScriptAnalyzer.BuiltinRules.dll</span><span class="sxs-lookup"><span data-stu-id="3a0e2-124">coreclr\Microsoft.Windows.PowerShell.ScriptAnalyzer.BuiltinRules.dll</span></span>
- <span data-ttu-id="3a0e2-125">coreclr\Microsoft.Windows.PowerShell.ScriptAnalyzer.dll</span><span class="sxs-lookup"><span data-stu-id="3a0e2-125">coreclr\Microsoft.Windows.PowerShell.ScriptAnalyzer.dll</span></span>
- <span data-ttu-id="3a0e2-126">en-US\about_PSScriptAnalyzer.help.txt</span><span class="sxs-lookup"><span data-stu-id="3a0e2-126">en-US\about_PSScriptAnalyzer.help.txt</span></span>
- <span data-ttu-id="3a0e2-127">en-US\Microsoft.Windows.PowerShell.ScriptAnalyzer.dll-Help.xml</span><span class="sxs-lookup"><span data-stu-id="3a0e2-127">en-US\Microsoft.Windows.PowerShell.ScriptAnalyzer.dll-Help.xml</span></span>
- <span data-ttu-id="3a0e2-128">PSv3\Microsoft.Windows.PowerShell.ScriptAnalyzer.BuiltinRules.dll</span><span class="sxs-lookup"><span data-stu-id="3a0e2-128">PSv3\Microsoft.Windows.PowerShell.ScriptAnalyzer.BuiltinRules.dll</span></span>
- <span data-ttu-id="3a0e2-129">PSv3\Microsoft.Windows.PowerShell.ScriptAnalyzer.dll</span><span class="sxs-lookup"><span data-stu-id="3a0e2-129">PSv3\Microsoft.Windows.PowerShell.ScriptAnalyzer.dll</span></span>
- <span data-ttu-id="3a0e2-130">Settings\CmdletDesign.psd1</span><span class="sxs-lookup"><span data-stu-id="3a0e2-130">Settings\CmdletDesign.psd1</span></span>
- <span data-ttu-id="3a0e2-131">Settings\DSC.psd1</span><span class="sxs-lookup"><span data-stu-id="3a0e2-131">Settings\DSC.psd1</span></span>
- <span data-ttu-id="3a0e2-132">Settings\ScriptFunctions.psd1</span><span class="sxs-lookup"><span data-stu-id="3a0e2-132">Settings\ScriptFunctions.psd1</span></span>
- <span data-ttu-id="3a0e2-133">Settings\ScriptingStyle.psd1</span><span class="sxs-lookup"><span data-stu-id="3a0e2-133">Settings\ScriptingStyle.psd1</span></span>
- <span data-ttu-id="3a0e2-134">Settings\ScriptSecurity.psd1</span><span class="sxs-lookup"><span data-stu-id="3a0e2-134">Settings\ScriptSecurity.psd1</span></span>

#### <a name="contents-of-psscriptanalyzerpsd1-file"></a><span data-ttu-id="3a0e2-135">Contents of PSScriptAnalyzer.psd1 file</span><span class="sxs-lookup"><span data-stu-id="3a0e2-135">Contents of PSScriptAnalyzer.psd1 file</span></span>

```powershell
@{

# Author of this module
Author = 'Microsoft Corporation'

# Script module or binary module file associated with this manifest.
RootModule = 'PSScriptAnalyzer.psm1'

# Version number of this module.
ModuleVersion = '1.6.1'

# ---
}
```

#### <a name="contents-of-psscriptanalyzerpsm1-file"></a><span data-ttu-id="3a0e2-136">PSScriptAnalyzer.psm1 fájl tartalma</span><span class="sxs-lookup"><span data-stu-id="3a0e2-136">Contents of PSScriptAnalyzer.psm1 file</span></span>

<span data-ttu-id="3a0e2-137">Alább logikai betölti a szükséges szerelvényeket, attól függően, a jelenlegi kiadása vagy verziója.</span><span class="sxs-lookup"><span data-stu-id="3a0e2-137">Below logic loads the required assemblies depending on the current edition or version.</span></span>

```powershell
#
# Script module for module 'PSScriptAnalyzer'
#
Set-StrictMode -Version Latest

# Set up some helper variables to make it easier to work with the module
$PSModule = $ExecutionContext.SessionState.Module
$PSModuleRoot = $PSModule.ModuleBase

# Import the appropriate nested binary module based on the current PowerShell version
$binaryModuleRoot = $PSModuleRoot


if (($PSVersionTable.Keys -contains "PSEdition") -and ($PSVersionTable.PSEdition -ne 'Desktop')) {
    $binaryModuleRoot = Join-Path -Path $PSModuleRoot -ChildPath 'coreclr'
}
else
{
    if ($PSVersionTable.PSVersion -lt [Version]'5.0') {
        $binaryModuleRoot = Join-Path -Path $PSModuleRoot -ChildPath 'PSv3'
    }
}

$binaryModulePath = Join-Path -Path $binaryModuleRoot -ChildPath 'Microsoft.Windows.PowerShell.ScriptAnalyzer.dll'
$binaryModule = Import-Module -Name $binaryModulePath -PassThru

# When the module is unloaded, remove the nested binary module that was loaded with it
$PSModule.OnRemove = {
    Remove-Module -ModuleInfo $binaryModule
}
```

### <a name="option-2-use-psedition-variable-in-the-psd1-file-to-load-the-proper-dlls-and-nestedrequired-modules"></a><span data-ttu-id="3a0e2-138">2. lehetőség: A psd1 kiterjesztésű fájl $PSEdition változót használja a megfelelő DLL-EK és a beágyazott/szükséges modulok betöltése</span><span class="sxs-lookup"><span data-stu-id="3a0e2-138">Option 2: Use $PSEdition variable in the PSD1 file to load the proper DLLs and Nested/Required modules</span></span>

<span data-ttu-id="3a0e2-139">A PS 5.1-es vagy újabb a modul jegyzékfájl $PSEdition globális változó használata engedélyezett.</span><span class="sxs-lookup"><span data-stu-id="3a0e2-139">In PS 5.1 or newer, $PSEdition global variable is allowed in the module manifest file.</span></span>
<span data-ttu-id="3a0e2-140">Használja ezt a változót, a modul Szerző értékeket adhat meg a feltételes modul jegyzékfájl.</span><span class="sxs-lookup"><span data-stu-id="3a0e2-140">Using this variable, module author can specify the conditional values in the module manifest file.</span></span> <span data-ttu-id="3a0e2-141">A korlátozott nyelvmód vagy adatok szakasz $PSEdition változó lehet hivatkozni.</span><span class="sxs-lookup"><span data-stu-id="3a0e2-141">$PSEdition variable can be referenced in restricted language mode or a Data section.</span></span>

> [!NOTE]
> <span data-ttu-id="3a0e2-142">Miután egy moduljegyzék a CompatiblePSEditions kulcs meg van adva, vagy $PSEdition változót használ, nem importálható lesz PowerShell alacsonyabb verzióiban.</span><span class="sxs-lookup"><span data-stu-id="3a0e2-142">Once a module manifest is specified with the CompatiblePSEditions key or uses $PSEdition variable, it can not be imported on lower versions of PowerShell.</span></span>

#### <a name="sample-module-manifest-file-with-compatiblepseditions-key"></a><span data-ttu-id="3a0e2-143">Minta modul jegyzékfájl CompatiblePSEditions kulccsal</span><span class="sxs-lookup"><span data-stu-id="3a0e2-143">Sample module manifest file with CompatiblePSEditions key</span></span>

```powershell
@{
# - - -

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

# -- - -
}
```

#### <a name="module-contents"></a><span data-ttu-id="3a0e2-144">A modul tartalma</span><span class="sxs-lookup"><span data-stu-id="3a0e2-144">Module contents</span></span>

```powershell
dir -Recurse
```

```output
    Directory: C:\Users\manikb\Documents\WindowsPowerShell\Modules\ModuleWithEditions

Mode                LastWriteTime         Length Name
----                -------------         ------ ----
d-----         7/5/2016   1:37 PM                clr
d-----         7/5/2016   1:36 PM                coreclr
-a----         7/5/2016   1:34 PM           4906 ModuleWithEditions.psd1

    Directory: C:\Users\manikb\Documents\WindowsPowerShell\Modules\ModuleWithEditions\clr

Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----         7/5/2016   1:35 PM              0 MyFullClrNM1.dll
-a----         7/5/2016   1:35 PM              0 MyFullClrNM2.dll
-a----         7/5/2016   1:35 PM              0 MyFullClrRM.dl

    Directory: C:\Users\manikb\Documents\WindowsPowerShell\Modules\ModuleWithEditions\coreclr

Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----         7/5/2016   1:35 PM              0 MyCoreClrNM1.dll
-a----         7/5/2016   1:35 PM              0 MyCoreClrNM2.dll
-a----         7/5/2016   1:35 PM              0 MyCoreClrRM.dl
```

## <a name="powershell-gallery-users-can-find-the-list-of-modules-supported-on-a-specific-powershell-edition-using-tags-pseditiondesktop-and-pseditioncore"></a><span data-ttu-id="3a0e2-145">PowerShell-galériából felhasználók egy adott PowerShell kiadás támogatott modulok listáját megtalálhatja, PSEdition_Desktop és PSEdition_Core címkék használatával.</span><span class="sxs-lookup"><span data-stu-id="3a0e2-145">PowerShell Gallery users can find the list of modules supported on a specific PowerShell Edition using tags PSEdition_Desktop and PSEdition_Core.</span></span>

<span data-ttu-id="3a0e2-146">Modulok PSEdition_Desktop és PSEdition_Core címkék nélküli minősülnek jól működnek az PowerShell asztali verziója esetén.</span><span class="sxs-lookup"><span data-stu-id="3a0e2-146">Modules without PSEdition_Desktop and PSEdition_Core tags are considered to work fine on PowerShell Desktop editions.</span></span>

```powershell
# Find modules supported on PowerShell Desktop edition
Find-Module -Tag PSEdition_Desktop

# Find modules supported on PowerShell Core editions
Find-Module -Tag PSEdition_Core
```

## <a name="more-details"></a><span data-ttu-id="3a0e2-147">További részletek</span><span class="sxs-lookup"><span data-stu-id="3a0e2-147">More details</span></span>

[<span data-ttu-id="3a0e2-148">PSEditions paraméterrel rendelkező parancsfájlok</span><span class="sxs-lookup"><span data-stu-id="3a0e2-148">Scripts with PSEditions</span></span>](script-psedition-support.md)

[<span data-ttu-id="3a0e2-149">Pseditions paraméterrel támogatja a PowerShell-Galériabeli</span><span class="sxs-lookup"><span data-stu-id="3a0e2-149">PSEditions support on PowerShellGallery</span></span>](../how-to/finding-items/searching-by-psedition.md)

[<span data-ttu-id="3a0e2-150">Moduljegyzék frissítése</span><span class="sxs-lookup"><span data-stu-id="3a0e2-150">Update module manifest</span></span>](/powershell/module/powershellget/update-modulemanifest)