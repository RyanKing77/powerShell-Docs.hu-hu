---
ms.date: 06/12/2017
contributor: manikb
keywords: gyűjtemény, a powershell, a parancsmag, a psget
title: Verzióval kompatibilis PowerShell modulok
ms.openlocfilehash: fbbfda2f913d54c3e69c0724fea4d977923279c1
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/16/2018
---
# <a name="modules-with-compatible-powershell-editions"></a><span data-ttu-id="f0d7a-103">Verzióval kompatibilis PowerShell modulok</span><span class="sxs-lookup"><span data-stu-id="f0d7a-103">Modules with compatible PowerShell Editions</span></span>

<span data-ttu-id="f0d7a-104">Az 5.1-es verziótól kezdődően a PowerShell különböző kiadásokban érhető el, amelyek különböző szolgáltatáskészleteket és platformkompatibilitást kínálnak.</span><span class="sxs-lookup"><span data-stu-id="f0d7a-104">Starting with version 5.1, PowerShell is available in different editions which denote varying feature sets and platform compatibility.</span></span>

- <span data-ttu-id="f0d7a-105">**Desktop kiadás:** A .NET-keretrendszeren alapul, és a Windows teljes erőforrás-igényű kiadásain, például a Server Core és a Windows asztali kiadásain futtatott PowerShell-verziókat célzó szkriptekhez és modulokhoz biztosít kompatibilitást.</span><span class="sxs-lookup"><span data-stu-id="f0d7a-105">**Desktop Edition:** Built on .NET Framework and provides compatibility with scripts and modules targeting versions of PowerShell running on full footprint editions of Windows such as Server Core and Windows Desktop.</span></span>
- <span data-ttu-id="f0d7a-106">**Core kiadás:** .NET Core-on alapul, és a Windows csökkentett erőforrás-igényű kiadásain, például a Nano Serveren és a Windows IoT kiadásokon futtatott PowerShell-verziókat célzó szkriptekhez és modulokhoz biztosít kompatibilitást.</span><span class="sxs-lookup"><span data-stu-id="f0d7a-106">**Core Edition:** Built on .NET Core and provides compatibility with scripts and modules targeting versions of PowerShell running on reduced footprint editions of Windows such as Nano Server and Windows IoT.</span></span>

## <a name="the-running-edition-of-powershell-is-shown-in-the-psedition-property-of-psversiontable"></a><span data-ttu-id="f0d7a-107">A futtatott PowerShell-verzió a $PSVersionTable PSEdition tulajdonságában jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="f0d7a-107">The running edition of PowerShell is shown in the PSEdition property of $PSVersionTable.</span></span>

```powershell
$PSVersionTable

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

## <a name="module-authors-can-declare-their-modules-to-be-compatible-with-one-or-more-powershell-editions-using-the-compatiblepseditions-module-manifest-key-this-key-is-only-supported-on-powershell-51-or-later"></a><span data-ttu-id="f0d7a-108">A modulkészítők a CompatiblePSEditions moduljegyzékkulcs segítségével deklarálhatják, hogy a moduljaik mely PowerShell-kiadással vagy -kiadásokkal kompatibilisek.</span><span class="sxs-lookup"><span data-stu-id="f0d7a-108">Module authors can declare their modules to be compatible with one or more PowerShell editions using the CompatiblePSEditions module manifest key.</span></span> <span data-ttu-id="f0d7a-109">Ez a kulcs csak a PowerShell 5.1-es vagy újabb verzióin támogatott.</span><span class="sxs-lookup"><span data-stu-id="f0d7a-109">This key is only supported on PowerShell 5.1 or later.</span></span>

<span data-ttu-id="f0d7a-110">*Megjegyzés:* után egy moduljegyzék CompatiblePSEditions a kulccsal van megadva, nem importálható-e a PowerShell korábbi verzióiban.</span><span class="sxs-lookup"><span data-stu-id="f0d7a-110">*NOTE* Once a module manifest is specified with the CompatiblePSEditions key, it can not be imported on lower versions of PowerShell.</span></span>

```powershell
New-ModuleManifest -Path .\TestModuleWithEdition.psd1 -CompatiblePSEditions Desktop,Core -PowerShellVersion 5.1
$ModuleInfo = Test-ModuleManifest -Path .\TestModuleWithEdition.psd1
$ModuleInfo.CompatiblePSEditions
Desktop
Core

$ModuleInfo | Get-Member CompatiblePSEditions

   TypeName: System.Management.Automation.PSModuleInfo

Name                 MemberType Definition
----                 ---------- ----------
CompatiblePSEditions Property   System.Collections.Generic.IEnumerable[string] CompatiblePSEditions {get;}

```

<span data-ttu-id="f0d7a-111">Az elérhető modulok listáját szűrheti a PowerShell-kiadás alapján.</span><span class="sxs-lookup"><span data-stu-id="f0d7a-111">When getting a list of available modules, you can filter the list by PowerShell edition.</span></span>

```powershell
Get-Module -ListAvailable -PSEdition Desktop

    Directory: C:\Program Files\WindowsPowerShell\Modules


ModuleType Version    Name                                ExportedCommands
---------- -------    ----                                ----------------
Manifest   1.0        ModuleWithPSEditions

Get-Module -ListAvailable -PSEdition Core | % CompatiblePSEditions
Desktop
Core

```

## <a name="module-authors-can-publish-a-single-module-targeting-to-either-or-both-powershell-editions-desktop-and-core"></a><span data-ttu-id="f0d7a-112">A modul szerzők tehet közzé egy egy modul a célcsoport-kezelési egyik vagy mindkét PowerShell-kiadások (asztali és mag)</span><span class="sxs-lookup"><span data-stu-id="f0d7a-112">Module authors can publish a single module targeting to either or both PowerShell editions (Desktop and Core)</span></span>

<span data-ttu-id="f0d7a-113">Egy modul asztal és a Core kiadásában használható, az adott modul Szerző szükséges logika hozzáadása vagy RootModule vagy a moduljegyzékben $PSEdition változóval rendelkezik.</span><span class="sxs-lookup"><span data-stu-id="f0d7a-113">A single module can work on both Desktop and Core editions, in that module author has to add required logic in either RootModule or in the module manifest using $PSEdition variable.</span></span>
<span data-ttu-id="f0d7a-114">Modulok rendelkezhet lefordított DLL-ek CoreCLR és a FullCLR célzó két csoportja.</span><span class="sxs-lookup"><span data-stu-id="f0d7a-114">Modules can have two sets of compiled DLLs targeting both CoreCLR and FullCLR.</span></span>
<span data-ttu-id="f0d7a-115">Az alábbiakban a néhány lehetőségek kiválasztásával becsomagolhatja a modul logikával megfelelő DLL-fájlok feltöltését.</span><span class="sxs-lookup"><span data-stu-id="f0d7a-115">Here are the couple of options to package your module with logic for loading proper dlls.</span></span>

### <a name="option-1-packaging-a-module-for-targeting-multiple-versions-and-multiple-editions-of-powershell"></a><span data-ttu-id="f0d7a-116">1. lehetőség: Csomagolására hajthatja végre a több verziói és több a PowerShell modul</span><span class="sxs-lookup"><span data-stu-id="f0d7a-116">Option 1: Packaging a module for targeting multiple versions and multiple editions of PowerShell</span></span>

#### <a name="module-folder-contents"></a><span data-ttu-id="f0d7a-117">A modul mappa tartalma</span><span class="sxs-lookup"><span data-stu-id="f0d7a-117">Module folder contents</span></span>

- <span data-ttu-id="f0d7a-118">Microsoft.Windows.PowerShell.ScriptAnalyzer.BuiltinRules.dll</span><span class="sxs-lookup"><span data-stu-id="f0d7a-118">Microsoft.Windows.PowerShell.ScriptAnalyzer.BuiltinRules.dll</span></span>
- <span data-ttu-id="f0d7a-119">Microsoft.Windows.PowerShell.ScriptAnalyzer.dll</span><span class="sxs-lookup"><span data-stu-id="f0d7a-119">Microsoft.Windows.PowerShell.ScriptAnalyzer.dll</span></span>
- <span data-ttu-id="f0d7a-120">PSScriptAnalyzer.psd1</span><span class="sxs-lookup"><span data-stu-id="f0d7a-120">PSScriptAnalyzer.psd1</span></span>
- <span data-ttu-id="f0d7a-121">PSScriptAnalyzer.psm1</span><span class="sxs-lookup"><span data-stu-id="f0d7a-121">PSScriptAnalyzer.psm1</span></span>
- <span data-ttu-id="f0d7a-122">ScriptAnalyzer.format.ps1xml</span><span class="sxs-lookup"><span data-stu-id="f0d7a-122">ScriptAnalyzer.format.ps1xml</span></span>
- <span data-ttu-id="f0d7a-123">ScriptAnalyzer.types.ps1xml</span><span class="sxs-lookup"><span data-stu-id="f0d7a-123">ScriptAnalyzer.types.ps1xml</span></span>
- <span data-ttu-id="f0d7a-124">coreclr\Microsoft.Windows.PowerShell.ScriptAnalyzer.BuiltinRules.dll</span><span class="sxs-lookup"><span data-stu-id="f0d7a-124">coreclr\Microsoft.Windows.PowerShell.ScriptAnalyzer.BuiltinRules.dll</span></span>
- <span data-ttu-id="f0d7a-125">coreclr\Microsoft.Windows.PowerShell.ScriptAnalyzer.dll</span><span class="sxs-lookup"><span data-stu-id="f0d7a-125">coreclr\Microsoft.Windows.PowerShell.ScriptAnalyzer.dll</span></span>
- <span data-ttu-id="f0d7a-126">en-US\about_PSScriptAnalyzer.help.txt</span><span class="sxs-lookup"><span data-stu-id="f0d7a-126">en-US\about_PSScriptAnalyzer.help.txt</span></span>
- <span data-ttu-id="f0d7a-127">en-US\Microsoft.Windows.PowerShell.ScriptAnalyzer.dll-Help.xml</span><span class="sxs-lookup"><span data-stu-id="f0d7a-127">en-US\Microsoft.Windows.PowerShell.ScriptAnalyzer.dll-Help.xml</span></span>
- <span data-ttu-id="f0d7a-128">PSv3\Microsoft.Windows.PowerShell.ScriptAnalyzer.BuiltinRules.dll</span><span class="sxs-lookup"><span data-stu-id="f0d7a-128">PSv3\Microsoft.Windows.PowerShell.ScriptAnalyzer.BuiltinRules.dll</span></span>
- <span data-ttu-id="f0d7a-129">PSv3\Microsoft.Windows.PowerShell.ScriptAnalyzer.dll</span><span class="sxs-lookup"><span data-stu-id="f0d7a-129">PSv3\Microsoft.Windows.PowerShell.ScriptAnalyzer.dll</span></span>
- <span data-ttu-id="f0d7a-130">Settings\CmdletDesign.psd1</span><span class="sxs-lookup"><span data-stu-id="f0d7a-130">Settings\CmdletDesign.psd1</span></span>
- <span data-ttu-id="f0d7a-131">Settings\DSC.psd1</span><span class="sxs-lookup"><span data-stu-id="f0d7a-131">Settings\DSC.psd1</span></span>
- <span data-ttu-id="f0d7a-132">Settings\ScriptFunctions.psd1</span><span class="sxs-lookup"><span data-stu-id="f0d7a-132">Settings\ScriptFunctions.psd1</span></span>
- <span data-ttu-id="f0d7a-133">Settings\ScriptingStyle.psd1</span><span class="sxs-lookup"><span data-stu-id="f0d7a-133">Settings\ScriptingStyle.psd1</span></span>
- <span data-ttu-id="f0d7a-134">Settings\ScriptSecurity.psd1</span><span class="sxs-lookup"><span data-stu-id="f0d7a-134">Settings\ScriptSecurity.psd1</span></span>

#### <a name="contents-of-psscriptanalyzerpsd1-file"></a><span data-ttu-id="f0d7a-135">Contents of PSScriptAnalyzer.psd1 file</span><span class="sxs-lookup"><span data-stu-id="f0d7a-135">Contents of PSScriptAnalyzer.psd1 file</span></span>

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

#### <a name="contents-of-psscriptanalyzerpsm1-file"></a><span data-ttu-id="f0d7a-136">PSScriptAnalyzer.psm1 fájl tartalma</span><span class="sxs-lookup"><span data-stu-id="f0d7a-136">Contents of PSScriptAnalyzer.psm1 file</span></span>

<span data-ttu-id="f0d7a-137">Alább logika betölti a szükséges szerelvényeket, attól függően, hogy a jelenlegi kiadása vagy verziója.</span><span class="sxs-lookup"><span data-stu-id="f0d7a-137">Below logic loads the required assemblies depending on the current edition or version.</span></span>

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

### <a name="option-2-use-psedition-variable-in-the-psd1-file-to-load-the-proper-dlls-and-nestedrequired-modules"></a><span data-ttu-id="f0d7a-138">2. lehetőség: A psd1 kiterjesztésű fájl $PSEdition változót használja a megfelelő DLL-EK és a beágyazott/szükséges modulok betöltése</span><span class="sxs-lookup"><span data-stu-id="f0d7a-138">Option 2: Use $PSEdition variable in the PSD1 file to load the proper DLLs and Nested/Required modules</span></span>

<span data-ttu-id="f0d7a-139">PS 5.1-es vagy újabb a modul jegyzékfájl $PSEdition globális változó használata engedélyezett.</span><span class="sxs-lookup"><span data-stu-id="f0d7a-139">In PS 5.1 or newer, $PSEdition global variable is allowed in the module manifest file.</span></span>
<span data-ttu-id="f0d7a-140">Használja ezt a változót, modul Szerző értékeket adhat meg a feltételes modul jegyzékfájl.</span><span class="sxs-lookup"><span data-stu-id="f0d7a-140">Using this variable, module author can specify the conditional values in the module manifest file.</span></span> <span data-ttu-id="f0d7a-141">Korlátozott nyelvi módban, vagy egy adatszakasz $PSEdition változó lehet hivatkozni.</span><span class="sxs-lookup"><span data-stu-id="f0d7a-141">$PSEdition variable can be referenced in restricted language mode or a Data section.</span></span>

<span data-ttu-id="f0d7a-142">*Megjegyzés:* után egy moduljegyzék CompatiblePSEditions a kulccsal van megadva, vagy használja $PSEdition változót, akkor nem importálható PowerShell korábbi verzióiban.</span><span class="sxs-lookup"><span data-stu-id="f0d7a-142">*NOTE* Once a module manifest is specified with the CompatiblePSEditions key or uses $PSEdition variable, it can not be imported on lower versions of PowerShell.</span></span>


#### <a name="sample-module-manifest-file-with-compatiblepseditions-key"></a><span data-ttu-id="f0d7a-143">Minta modul jegyzékfájl CompatiblePSEditions kulccsal</span><span class="sxs-lookup"><span data-stu-id="f0d7a-143">Sample module manifest file with CompatiblePSEditions key</span></span>

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

#### <a name="module-contents"></a><span data-ttu-id="f0d7a-144">A modul tartalma</span><span class="sxs-lookup"><span data-stu-id="f0d7a-144">Module contents</span></span>

```powershell

PS C:\Users\manikb\Documents\WindowsPowerShell\Modules\ModuleWithEditions> dir -Recurse

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

## <a name="powershell-gallery-users-can-find-the-list-of-modules-supported-on-a-specific-powershell-edition-using-tags-pseditiondesktop-and-pseditioncore"></a><span data-ttu-id="f0d7a-145">PowerShell-galériában felhasználói is megtalálhassák egy adott kiadásán PowerShell támogatott listájához PSEdition_Desktop és PSEdition_Core címkék használatával.</span><span class="sxs-lookup"><span data-stu-id="f0d7a-145">PowerShell Gallery users can find the list of modules supported on a specific PowerShell Edition using tags PSEdition_Desktop and PSEdition_Core.</span></span>

<span data-ttu-id="f0d7a-146">Modulok PSEdition_Desktop és PSEdition_Core címkék nélkül minősülnek PowerShell asztali változatában működnek.</span><span class="sxs-lookup"><span data-stu-id="f0d7a-146">Modules without PSEdition_Desktop and PSEdition_Core tags are considered to work fine on PowerShell Desktop editions.</span></span>

```powershell

# Find modules supported on PowerShell Desktop edition
Find-Module -Tag PSEdition_Desktop

# Find modules supported on PowerShell Core editions
Find-Module -Tag PSEdition_Core

```


## <a name="more-details"></a><span data-ttu-id="f0d7a-147">További részletekért</span><span class="sxs-lookup"><span data-stu-id="f0d7a-147">More details</span></span>

- [<span data-ttu-id="f0d7a-148">PSEditions paraméterrel rendelkező parancsfájlok</span><span class="sxs-lookup"><span data-stu-id="f0d7a-148">Scripts with PSEditions</span></span>](script-psedition-support.md)
- [<span data-ttu-id="f0d7a-149">Támogatja a PSEditions PowerShellGallery</span><span class="sxs-lookup"><span data-stu-id="f0d7a-149">PSEditions support on PowerShellGallery</span></span>](../how-to/finding-items/searching-by-psedition.md)
- <span data-ttu-id="f0d7a-150">[Frissítési moduljegyzék] (/ powershell/modul/powershellget/frissítés-modulemanifest)</span><span class="sxs-lookup"><span data-stu-id="f0d7a-150">[Update module manifest] (/powershell/module/powershellget/update-modulemanifest)</span></span>