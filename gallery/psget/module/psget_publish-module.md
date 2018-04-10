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
# <a name="publish-module"></a>Publish-Module

Közzéteszi a megadott modul a helyi számítógépről egy online gyűjteményébe.

## <a name="description"></a>Leírás

A **Publish-modul** parancsmag modul közzéteszi az online NuGet-alapú tárak, API-kulcs használatával a katalógusban felhasználói profil részeként tárolja. A modul közzététele a modul neve, vagy a modult tartalmazó mappa elérési útját adhatja meg.

Amikor megad egy modul neve, **Publish-modul** tesz közzé az első modul, amely futtatásával volna található `Get-Module -ListAvailable <Name>`. Ha megad egy modul közzétételéhez legalább **Publish-modul** tesz közzé az első modul olyan verzióra, amely nagyobb vagy egyenlő a megadott minimális verziójának.

Közzétételi modul szükséges metaadatokat, amelyek a modul gyűjtemény lapján megjelenik. Kötelező metaadatok közé tartozik, a modul neve, a verziót, a leírás és a szerző. Bár a legtöbb metaadatok a moduljegyzékben származik, bizonyos metaadatait meg kell adni a **Publish-modul** paraméterek, például a *címke, ReleaseNote, IconUri, ProjectUri,* és  *LicenseUri*, mert ezek a paraméterek megegyeznek a NuGet-alapú tárban mezők.

A RequiredVersion paraméter lehetővé teszi közzé kell tenni egy modul pontos verziójának megadását.
A Path paramétert is támogatja a modul alap útvonalat a mappát.
A Publish-modul a parancsmag a Force kapcsolót paramétert a NuGet.exe betöltéséhez értesítése nélkül.

## <a name="cmdlet-syntax"></a>A parancsmag szintaxisa
```powershell
Get-Command -Name Publish-Module -Module PowerShellGet -Syntax
```

## <a name="cmdlet-online-help-reference"></a>A parancsmag online Súgó-hivatkozás

[Publish-Module](http://go.microsoft.com/fwlink/?LinkID=398575)

## <a name="example-commands"></a>Példa parancsok

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

## <a name="publishing-a-module-with-dependencies"></a>A modul függőségekkel rendelkező közzététele

### <a name="create-a-module-with-dependencies-and-version-range-specified-in-requiredmodules-property-of-its-module-manifest"></a>Hozzon létre egy modul függőségei és a moduljegyzékben RequiredModules tulajdonságában megadott verziója tartományon.

**Megjegyzés:**
  - \* csak MaximumVersion támogatott is kell verzió-karakterlánc végén.
  - \* a verzió objektumban 999999999 helyére.

```powershell
PS C:\windows\system32> $requiredModules = @( @{ModuleName = 'RequiredModule1'; ModuleVersion = '0.1'; MaximumVersion = '1.9'; }, @{ModuleName = 'RequiredModule2'; MaximumVersion = '1.*'; })

PS C:\windows\system32> cd C:\MyModules\ModuleWithDependencies

PS C:\MyModules\ModuleWithDependencies> New-ModuleManifest -Path .\ModuleWithDependencies.psd1 -ModuleVersion 1.0 -RequiredModules $requiredModules -Description 'ModuleWithDependencies demo module'
```

### <a name="publish-modulewithdependencies-module-with-dependencies-to-the-repository"></a>A tárház ModuleWithDependencies modul függőségekkel rendelkező közzététele.

```powershell
PS C:\MyModules\ModuleWithDependencies> Publish-Module -Path C:\MyModules\ModuleWithDependencies -Repository LocalRepo
```

### <a name="find-modulewithdependencies-module-with-its-dependencies-by-specifying--includedependencies"></a>-IncludeDependencies megadásával ModuleWithDependencies modulját és annak függőségeit keresése

```powershell
PS C:\MyModules\ModuleWithDependencies> Find-Module -Name ModuleWithDependencies -Repository LocalRepo -IncludeDependencies

Version    Name                                Type       Repository           Description
-------    ----                                ----       ----------           -----------
1.0        ModuleWithDependencies              Module     localrepo            ModuleWithDependencies demo module
1.5        RequiredModule1                     Module     localrepo            RequiredModule1 module
1.5        RequiredModule2                     Module     localrepo            RequiredModule2 module
```

### <a name="install-the-modulewithdependencies-module-with-dependencies"></a>A ModuleWithDependencies modul telepítése függőségekkel rendelkező.
Vegye figyelembe, hogy verzió tartományok figyelembe vannak-e véve függőségi telepítése során.

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

### <a name="contents-of-modulewithdependencies2-module-manifest-file"></a>A jegyzékfájl ModuleWithDependencies2 modul tartalmát

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


### <a name="external-dependencies"></a>Külső függőségek
Néhány modul függőségek külsőleg kezelheti, ebben az esetben kell adni őket a moduljegyzékben PSData szakaszában ExternalModuleDependencies-bejegyzést.

Ha "SnippetPx" nem érhető el a tárházban, alatt hibát fog jelezni.
```powershell
Publish-PSArtifactUtility : PowerShellGet cannot resolve the module dependency 'SnippetPx' of the module 'TypePx' on the repository 'LocalRepo'. Verify that the dependent module 'SnippetPx' is available in the repository 'LocalRepo'. If this dependent 'SnippetPx' is managed externally, add it to the ExternalModuleDependencies entry in the PSData section of the module manifest.
```