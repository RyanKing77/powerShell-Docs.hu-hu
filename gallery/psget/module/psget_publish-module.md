---
ms.date: 06/12/2017
contributor: manikb
ms.topic: reference
keywords: gyűjtemény, a powershell, a parancsmag, a psget
title: Publish-Module
ms.openlocfilehash: 8b73be2814678ce143cc5b53e2b8103b3297eb6a
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="publish-module"></a><span data-ttu-id="209fa-103">Publish-Module</span><span class="sxs-lookup"><span data-stu-id="209fa-103">Publish-Module</span></span>

<span data-ttu-id="209fa-104">Közzéteszi a megadott modul a helyi számítógépről egy online gyűjteményébe.</span><span class="sxs-lookup"><span data-stu-id="209fa-104">Publishes a specified module from the local computer to an online gallery.</span></span>

## <a name="description"></a><span data-ttu-id="209fa-105">Leírás</span><span class="sxs-lookup"><span data-stu-id="209fa-105">Description</span></span>

<span data-ttu-id="209fa-106">A **Publish-modul** parancsmag modul közzéteszi az online NuGet-alapú tárak, API-kulcs használatával a katalógusban felhasználói profil részeként tárolja.</span><span class="sxs-lookup"><span data-stu-id="209fa-106">The **Publish-Module** cmdlet publishes a module to an online NuGet-based gallery by using an API key, stored as part of a user's profile in the gallery.</span></span> <span data-ttu-id="209fa-107">A modul közzététele a modul neve, vagy a modult tartalmazó mappa elérési útját adhatja meg.</span><span class="sxs-lookup"><span data-stu-id="209fa-107">You can specify the module to publish either by the module's name, or by the path to the folder containing the module.</span></span>

<span data-ttu-id="209fa-108">Amikor megad egy modul neve, **Publish-modul** tesz közzé az első modul, amely futtatásával volna található `Get-Module -ListAvailable <Name>`.</span><span class="sxs-lookup"><span data-stu-id="209fa-108">When you specify a module by name, **Publish-Module** publishes the first module that would be found by running `Get-Module -ListAvailable <Name>`.</span></span> <span data-ttu-id="209fa-109">Ha megad egy modul közzétételéhez legalább **Publish-modul** tesz közzé az első modul olyan verzióra, amely nagyobb vagy egyenlő a megadott minimális verziójának.</span><span class="sxs-lookup"><span data-stu-id="209fa-109">If you specify a minimum version of a module to publish, **Publish-Module** publishes the first module with a version that is greater than or equal to the minimum version that you have specified.</span></span>

<span data-ttu-id="209fa-110">Közzétételi modul szükséges metaadatokat, amelyek a modul gyűjtemény lapján megjelenik.</span><span class="sxs-lookup"><span data-stu-id="209fa-110">Publishing a module requires metadata that is displayed on the gallery page for the module.</span></span> <span data-ttu-id="209fa-111">Kötelező metaadatok közé tartozik, a modul neve, a verziót, a leírás és a szerző.</span><span class="sxs-lookup"><span data-stu-id="209fa-111">Required metadata includes the module name, version, description, and author.</span></span> <span data-ttu-id="209fa-112">Bár a legtöbb metaadatok a moduljegyzékben származik, bizonyos metaadatait meg kell adni a **Publish-modul** paraméterek, például a *címke, ReleaseNote, IconUri, ProjectUri,* és  *LicenseUri*, mert ezek a paraméterek megegyeznek a NuGet-alapú tárban mezők.</span><span class="sxs-lookup"><span data-stu-id="209fa-112">Although most metadata is taken from the module manifest, some metadata must be specified in **Publish-Module** parameters, such as *Tag, ReleaseNote, IconUri, ProjectUri,* and *LicenseUri*, because these parameters match fields in a NuGet-based gallery.</span></span>

<span data-ttu-id="209fa-113">A RequiredVersion paraméter lehetővé teszi közzé kell tenni egy modul pontos verziójának megadását.</span><span class="sxs-lookup"><span data-stu-id="209fa-113">The RequiredVersion parameter allows you to specify the exact version of a module to be published.</span></span>
<span data-ttu-id="209fa-114">A Path paramétert is támogatja a modul alap útvonalat a mappát.</span><span class="sxs-lookup"><span data-stu-id="209fa-114">The Path parameter also supports the module base path with the version folder.</span></span>
<span data-ttu-id="209fa-115">A Publish-modul a parancsmag a Force kapcsolót paramétert a NuGet.exe betöltéséhez értesítése nélkül.</span><span class="sxs-lookup"><span data-stu-id="209fa-115">The Force switch parameter on Publish-Module cmdlet bootstraps the NuGet.exe without prompting.</span></span>

## <a name="cmdlet-syntax"></a><span data-ttu-id="209fa-116">A parancsmag szintaxisa</span><span class="sxs-lookup"><span data-stu-id="209fa-116">Cmdlet syntax</span></span>
```powershell
Get-Command -Name Publish-Module -Module PowerShellGet -Syntax
```

## <a name="cmdlet-online-help-reference"></a><span data-ttu-id="209fa-117">A parancsmag online Súgó-hivatkozás</span><span class="sxs-lookup"><span data-stu-id="209fa-117">Cmdlet online help reference</span></span>

[<span data-ttu-id="209fa-118">Publish-Module</span><span class="sxs-lookup"><span data-stu-id="209fa-118">Publish-Module</span></span>](http://go.microsoft.com/fwlink/?LinkID=398575)

## <a name="example-commands"></a><span data-ttu-id="209fa-119">Példa parancsok</span><span class="sxs-lookup"><span data-stu-id="209fa-119">Example commands</span></span>

```powershell
ContosoServer module with different versions to be published.
PS C:\\windows\\system32> Get-Module -Name ContosoServer -ListAvailable
Directory: C:\\Program Files\\WindowsPowerShell\\Modules
ModuleType Version Name ExportedCommands
---------- ------- ---- ----------------
Manifest 2.8 ContosoServer Get-ContosoServer
Manifest 2.0 ContosoServer Get-ContosoServer
Manifest 1.5 ContosoServer Get-ContosoServer
Manifest 1.0 ContosoServer Get-ContosoServer
PS C:\\windows\\system32> Publish-Module -Name ContosoServer -RequiredVersion 1.0 -Repository LocalRepo -NuGetApiKey Local-Repo-NuGet-ApiKey
PS C:\\windows\\system32> Find-Module -Name ContosoServer -Repository LocalRepo
Version Name Repository Description
------- ---- ---------- -----------
1.0 ContosoServer LocalRepo ContosoServer module
PS C:\\windows\\system32> Publish-Module -Name ContosoServer -RequiredVersion 1.5 -Repository LocalRepo -NuGetApiKey Local-Repo-NuGet-ApiKey
PS C:\\windows\\system32> Find-Module -Name ContosoServer -Repository LocalRepo
Version Name Repository Description
------- ---- ---------- -----------
1.0 ContosoServer LocalRepo ContosoServer module
1.5 ContosoServer LocalRepo ContosoServer module
PS C:\\windows\\system32> Publish-Module -Path "C:\\Program Files\\WindowsPowerShell\\Modules\\ContosoServer\\2.0" -Repository LocalRepo -NuGetApiKey Local-Repo-NuGet-ApiKey
PS C:\\windows\\system32> Find-Module -Name ContosoServer -Repository LocalRepo
Version Name Repository Description
_------ ---- ---------- -----------
1.0 ContosoServer LocalRepo ContosoServer module
1.5 ContosoServer LocalRepo ContosoServer module
2.0 ContosoServer LocalRepo ContosoServer module
```

## <a name="publishing-a-module-with-dependencies"></a><span data-ttu-id="209fa-120">A modul függőségekkel rendelkező közzététele</span><span class="sxs-lookup"><span data-stu-id="209fa-120">Publishing a module with dependencies</span></span>

### <a name="create-a-module-with-dependencies-and-version-range-specified-in-requiredmodules-property-of-its-module-manifest"></a><span data-ttu-id="209fa-121">Hozzon létre egy modul függőségei és a moduljegyzékben RequiredModules tulajdonságában megadott verziója tartományon.</span><span class="sxs-lookup"><span data-stu-id="209fa-121">Create a module with dependencies and version range specified in RequiredModules property of its module manifest.</span></span>

<span data-ttu-id="209fa-122">**Megjegyzés:**</span><span class="sxs-lookup"><span data-stu-id="209fa-122">**Note:**</span></span>
  - <span data-ttu-id="209fa-123">\* csak MaximumVersion támogatott is kell verzió-karakterlánc végén.</span><span class="sxs-lookup"><span data-stu-id="209fa-123">\* is supported only in MaximumVersion and also it should be at the end of version string.</span></span>
  - <span data-ttu-id="209fa-124">\* a verzió objektumban 999999999 helyére.</span><span class="sxs-lookup"><span data-stu-id="209fa-124">\* is replaced with 999999999 in the version object.</span></span>

```powershell
PS C:\windows\system32> $requiredModules = @( @{ModuleName = 'RequiredModule1'; ModuleVersion = '0.1'; MaximumVersion = '1.9'; }, @{ModuleName = 'RequiredModule2'; MaximumVersion = '1.*'; })

PS C:\windows\system32> cd C:\MyModules\ModuleWithDependencies

PS C:\MyModules\ModuleWithDependencies> New-ModuleManifest -Path .\ModuleWithDependencies.psd1 -ModuleVersion 1.0 -RequiredModules $requiredModules -Description 'ModuleWithDependencies demo module'
```

### <a name="publish-modulewithdependencies-module-with-dependencies-to-the-repository"></a><span data-ttu-id="209fa-125">A tárház ModuleWithDependencies modul függőségekkel rendelkező közzététele.</span><span class="sxs-lookup"><span data-stu-id="209fa-125">Publish ModuleWithDependencies module with dependencies to the repository.</span></span>

```powershell
PS C:\MyModules\ModuleWithDependencies> Publish-Module -Path C:\MyModules\ModuleWithDependencies -Repository LocalRepo
```

### <a name="find-modulewithdependencies-module-with-its-dependencies-by-specifying--includedependencies"></a><span data-ttu-id="209fa-126">-IncludeDependencies megadásával ModuleWithDependencies modulját és annak függőségeit keresése</span><span class="sxs-lookup"><span data-stu-id="209fa-126">Find ModuleWithDependencies module with its dependencies by specifying -IncludeDependencies</span></span>

```powershell
PS C:\MyModules\ModuleWithDependencies> Find-Module -Name ModuleWithDependencies -Repository LocalRepo -IncludeDependencies

Version    Name                                Type       Repository           Description
-------    ----                                ----       ----------           -----------
1.0        ModuleWithDependencies              Module     localrepo            ModuleWithDependencies demo module
1.5        RequiredModule1                     Module     localrepo            RequiredModule1 module
1.5        RequiredModule2                     Module     localrepo            RequiredModule2 module
```

### <a name="install-the-modulewithdependencies-module-with-dependencies"></a><span data-ttu-id="209fa-127">A ModuleWithDependencies modul telepítése függőségekkel rendelkező.</span><span class="sxs-lookup"><span data-stu-id="209fa-127">Install the ModuleWithDependencies module with dependencies.</span></span>
<span data-ttu-id="209fa-128">Vegye figyelembe, hogy verzió tartományok figyelembe vannak-e véve függőségi telepítése során.</span><span class="sxs-lookup"><span data-stu-id="209fa-128">Note that version ranges are honored during the dependency installation.</span></span>

```powershell
PS C:\windows\system32> Get-InstalledModule
PS C:\windows\system32>
PS C:\windows\system32> Install-Module -Name ModuleWithDependencies -Repository LocalRepo
PS C:\windows\system32>
PS C:\windows\system32> Get-InstalledModule

Version    Name                                Type       Repository           Description
-------    ----                                ----       ----------           -----------
1.0        ModuleWithDependencies              Module     localrepo            ModuleWithDependencies demo module
1.5        RequiredModule1                     Module     localrepo            RequiredModule1 module
1.5        RequiredModule2                     Module     localrepo            RequiredModule2 module
```

### <a name="contents-of-modulewithdependencies2-module-manifest-file"></a><span data-ttu-id="209fa-129">A jegyzékfájl ModuleWithDependencies2 modul tartalmát</span><span class="sxs-lookup"><span data-stu-id="209fa-129">Contents of ModuleWithDependencies2 module manifest file</span></span>

```powershell
@{
# Version number of this module.
ModuleVersion = '2.0'
# ID used to uniquely identify this module
GUID = '0eae34da-99dd-4608-8d28-c614fe7b0841'
# Author of this module
Author = 'manikb'
# Company or vendor of this module
CompanyName = 'Unknown'
# Copyright statement for this module
Copyright = '(c) 2015 manikb. All rights reserved.'
# Description of the functionality provided by this module
Description = 'ModuleWithDependencies2 module'
# Modules that must be imported into the global environment prior to importing this module
RequiredModules = @('RequiredModule1',
@{ModuleName = 'RequiredModule2'; ModuleVersion = '2.0'; },
@{ModuleName = 'RequiredModule3'; RequiredVersion = '2.5'; },
@{ModuleName = 'RequiredModule4'; ModuleVersion = '1.1'; MaximumVersion = '2.0'; },
@{ModuleName = 'RequiredModule5'; MaximumVersion = '1.5'; })
# Modules to import as nested modules of the module specified in RootModule/ModuleToProcess
NestedModules = @('NestedRequiredModule1',
@{ModuleName = 'NestedRequiredModule2'; ModuleVersion = '2.0'; },
@{ModuleName = 'NestedRequiredModule3'; RequiredVersion = '2.5'; },
@{ModuleName = 'NestedRequiredModule4'; ModuleVersion = '0.7'; MaximumVersion = '2.4'; },
@{ModuleName = 'NestedRequiredModule5'; MaximumVersion = '1.6'; },'ModuleWithDependencies2.psm1')
# Functions to export from this module
FunctionsToExport = '\*'
# Cmdlets to export from this module
CmdletsToExport = '\*'
# Variables to export from this module
VariablesToExport = '\*'
# Aliases to export from this module
AliasesToExport = '\*'
# Private data to pass to the module specified in RootModule/ModuleToProcess. This may also contain a PSData hashtable with additional module metadata used by PowerShell.
PrivateData = @{
    PSData = @{
      # Tags applied to this module. These help with module discovery in online galleries.
      Tags = 'Tag1', 'Tag2', 'Tag-ModuleWithDependencies2-2.0'
      # A URL to the license for this module.
      LicenseUri = 'http://modulewithdependencies2.com/license'
      # A URL to the main website for this project.
      ProjectUri = 'http://modulewithdependencies2.com/'
      # A URL to an icon representing this module.
      IconUri = 'http://modulewithdependencies2.com/icon'
      # ReleaseNotes of this module
      ReleaseNotes = 'ModuleWithDependencies2 release notes'
    } # End of PSData hashtable
} # End of PrivateData hashtable
}
```


### <a name="external-dependencies"></a><span data-ttu-id="209fa-130">Külső függőségek</span><span class="sxs-lookup"><span data-stu-id="209fa-130">External dependencies</span></span>
<span data-ttu-id="209fa-131">Néhány modul függőségek külsőleg kezelheti, ebben az esetben kell adni őket a moduljegyzékben PSData szakaszában ExternalModuleDependencies-bejegyzést.</span><span class="sxs-lookup"><span data-stu-id="209fa-131">Some module dependencies can be managed externally, in that case they should be added to the ExternalModuleDependencies entry in the PSData section of the module manifest.</span></span>

<span data-ttu-id="209fa-132">Ha "SnippetPx" nem érhető el a tárházban, alatt hibát fog jelezni.</span><span class="sxs-lookup"><span data-stu-id="209fa-132">If 'SnippetPx' is not available on the repository, below error will be thrown.</span></span>
```powershell
Publish-PSArtifactUtility : PowerShellGet cannot resolve the module dependency 'SnippetPx' of the module 'TypePx' on the repository 'LocalRepo'. Verify that the dependent module 'SnippetPx' is available in the repository 'LocalRepo'. If this dependent 'SnippetPx' is managed externally, add it to the ExternalModuleDependencies entry in the PSData section of the module manifest.
```