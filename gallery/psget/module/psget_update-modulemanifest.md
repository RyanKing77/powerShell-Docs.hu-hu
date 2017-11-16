---
ms.date: 2017-06-12
contributor: manikb
ms.topic: reference
keywords: "gyűjtemény, a powershell, a parancsmag, a psget"
title: "Frissítés-ModuleManifest"
ms.openlocfilehash: ce3f6f173535d98648eb51adb1dbf84764e4f434
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2017
---
# <a name="update-modulemanifest"></a><span data-ttu-id="07f38-103">Frissítés-ModuleManifest</span><span class="sxs-lookup"><span data-stu-id="07f38-103">Update-ModuleManifest</span></span>
<span data-ttu-id="07f38-104">Egy modul jegyzékfájl frissíti.</span><span class="sxs-lookup"><span data-stu-id="07f38-104">Updates a module manifest file.</span></span>

## <a name="description"></a><span data-ttu-id="07f38-105">Leírás</span><span class="sxs-lookup"><span data-stu-id="07f38-105">Description</span></span>

<span data-ttu-id="07f38-106">A frissítés-ModuleManifest parancsmag frissíti egy modul jegyzékfájlt (.psd1) fájlt.</span><span class="sxs-lookup"><span data-stu-id="07f38-106">The Update-ModuleManifest cmdlet updates a module manifest (.psd1) file.</span></span>

### <a name="notes"></a><span data-ttu-id="07f38-107">Megjegyzések</span><span class="sxs-lookup"><span data-stu-id="07f38-107">Notes</span></span>
    - <span data-ttu-id="07f38-108">DscResourcesToExport csak a legújabb PowerShell 5.0-s verziója támogatott.</span><span class="sxs-lookup"><span data-stu-id="07f38-108">DscResourcesToExport is only supported on the latest PowerShell version 5.0.</span></span> <span data-ttu-id="07f38-109">Azt nem lehet frissíteni a mező, ha a PowerShell alacsonyabb verzióját futtatja.</span><span class="sxs-lookup"><span data-stu-id="07f38-109">We won’t be able to update the field if you are running on lower versions of PowerShell.</span></span>

## <a name="cmdlet-syntax"></a><span data-ttu-id="07f38-110">A parancsmag szintaxisa</span><span class="sxs-lookup"><span data-stu-id="07f38-110">Cmdlet syntax</span></span>
```powershell
Get-Command -Name Update-ModuleManifest -Module PowerShellGet -Syntax
```

## <a name="cmdlet-online-help-reference"></a><span data-ttu-id="07f38-111">A parancsmag online Súgó-hivatkozás</span><span class="sxs-lookup"><span data-stu-id="07f38-111">Cmdlet online help reference</span></span>

[<span data-ttu-id="07f38-112">Frissítés-ModuleManifest</span><span class="sxs-lookup"><span data-stu-id="07f38-112">Update-ModuleManifest</span></span>](http://go.microsoft.com/fwlink/?LinkId=619311)

## <a name="example-commands"></a><span data-ttu-id="07f38-113">Példa parancsok</span><span class="sxs-lookup"><span data-stu-id="07f38-113">Example commands</span></span>

<span data-ttu-id="07f38-114">Ez a parancsmag bemeneti tulajdonság értékekkel jegyzékfájl frissítése érdekében használatos.</span><span class="sxs-lookup"><span data-stu-id="07f38-114">This new cmdlet is used to help update manifest file with input property values.</span></span> <span data-ttu-id="07f38-115">Összes paramétert, amely új-ModuleManifest vesz igénybe.</span><span class="sxs-lookup"><span data-stu-id="07f38-115">It takes all parameters that New-ModuleManifest does.</span></span>

<span data-ttu-id="07f38-116">Azt figyelje meg, hogy a modul szerzők nagy szeretné adja meg "\*" FunctionsToExport, CmdletsToExport, például az exportált értékek stb. Modul közzététele PowerShell gyűjteményébe, során nem meghatározott funkciók és parancsok lesz nem kitöltve megfelelően alakzatot a gyűjteményben.</span><span class="sxs-lookup"><span data-stu-id="07f38-116">We notice that a lot of module authors would like to specify “\*” in exported values such as FunctionsToExport, CmdletsToExport, etc. During module publishing to PowerShell Gallery, unspecified functions and commands will not be populated properly onto the Gallery.</span></span> <span data-ttu-id="07f38-117">Ezért javasoljuk, hogy modul szerzők frissítése megfelelő értékekkel a jegyzékfájlban.</span><span class="sxs-lookup"><span data-stu-id="07f38-117">Therefore, we suggest module authors update their manifests with proper values.</span></span>

<span data-ttu-id="07f38-118">Ha tulajdonságok exportált modulok, a frissítés-ModuleManifest tölti a megadott jegyzékfájl exportált funkciók, a parancsmagok, a változók stb adataival:</span><span class="sxs-lookup"><span data-stu-id="07f38-118">If you have modules that have exported properties, Update-ModuleManifest will fill the specified manifest file with information from exported functions, cmdlets, variables etc:</span></span>
```powershell
Get-Content -Path "C:\Temp\PSGTEST-TestPackageMetadata\2.5\PSGTEST-TestPackageMetadata.psd1"
@{
# Script module or binary module file associated with this manifest.
# RootModule = ''
# Version number of this module.
ModuleVersion = '2.5'
# ID used to uniquely identify this module
GUID = '610e5c5b-dc42-4eaa-8511-ebfb44066d5e'

#(Other properties removed here for Simplicity…)

# Functions to export from this module
FunctionsToExport = '*'
# Cmdlets to export from this module
CmdletsToExport = '*'
# Variables to export from this module
VariablesToExport = '*'
# Aliases to export from this module
AliasesToExport = '*'
}
```

<span data-ttu-id="07f38-119">Miután a frissítés-ModuleManifest:</span><span class="sxs-lookup"><span data-stu-id="07f38-119">After Update-ModuleManifest:</span></span>
```powershell
Update-ModuleManifest -Path "C:\Temp\PSGTEST-TestPackageMetadata\2.5\PSGTEST-TestPackageMetadata.psd1"
Get-Content -Path "C:\Temp\PSGTEST-TestPackageMetadata\2.5\PSGTEST-TestPackageMetadata.psd1"
#
# Module manifest for module 'NewManifest'
#
# Generated by: author name
#
# Generated on: 11/13/2015
#
@{
# Script module or binary module file associated with this manifest.
# RootModule = ''
# Version number of this module.
ModuleVersion = '2.5'
# ID used to uniquely identify this module
GUID = '610e5c5b-dc42-4eaa-8511-ebfb44066d5e'
# Functions to export from this module
FunctionsToExport = 'Get-FooFn Get-FooWF'
# Cmdlets to export from this module
CmdletsToExport = 'Test-PSGetTestCmdlet'
}
```

<span data-ttu-id="07f38-120">Minden modul vannak társítva metaadatmezőket.</span><span class="sxs-lookup"><span data-stu-id="07f38-120">For each module, there are also metadata fields associated with it.</span></span> <span data-ttu-id="07f38-121">Metaadatok helyes megjelenítéséhez a PowrShell gyűjteménye, a frissítés-ModuleManifest segítségével feltöltése PrivateData a mezőket.</span><span class="sxs-lookup"><span data-stu-id="07f38-121">In order to display metadata properly on PowrShell Gallery, you can use Update-ModuleManifest to populate those fields under PrivateData.</span></span>

```powershell
Update-ModuleManifest -Path "C:\Temp\PSGTEST-TestPackageMetadata\2.5\PSGTEST-TestPackageMetadata.psd1" -Tags "Tag1" -LicenseUri "http://license.com" -ProjectUri "http://project.com" -IconUri "http://icon.com" -ReleaseNotes "Test module"
```

<span data-ttu-id="07f38-122">A jegyzékfájl sablonból PrivateData hashtable tulajdonságai a következők</span><span class="sxs-lookup"><span data-stu-id="07f38-122">PrivateData hashtable from the manifest file template has the following properties</span></span>

```powershell
# Private data to pass to the module specified in RootModule/ModuleToProcess. This may also contain a PSData hashtable with additional module metadata used by PowerShell.
PrivateData = @{
    PSData = @{
        # Tags applied to this module. These help with module discovery in online galleries.
        # Tags = @()

        # A URL to the license for this module.
        # LicenseUri = ''
    
        # A URL to the main website for this project.
        # ProjectUri = ''
        
        # A URL to an icon representing this module.
        # IconUri = ''
        
        # ReleaseNotes of this module
        # ReleaseNotes = ''
        
        # External dependent modules of this module
        # ExternalModuleDependencies = ''
    } # End of PSData hashtable
} # End of PrivateData hashtable
```

