---
ms.date: 2017-06-12
contributor: manikb
ms.topic: reference
keywords: "gyűjtemény, a powershell, a parancsmag, a psget"
title: "A modul keresése"
ms.openlocfilehash: 65c466909c007ed08c3fa978f78483983b00ba73
ms.sourcegitcommit: 58371abe9db4b9a0e4e1eb82d39a9f9e187355f9
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/05/2017
---
# <a name="find-module"></a>A modul keresése
Megkeresi a megadott feltételeknek megfelelő modulok egy online katalógusból.

## <a name="description"></a>Leírás
Keresés-modult a modulok regisztrált tárházak találhatók, amely a megadott feltételeknek megfelelő deríti fel.
Minden modul található, keresés-modul egy objektumot ad vissza PSRepositoryItemInfo opcionálisan átirányítható, amely az Install-modul a modulok telepítése.

- Keresés-modul is szűrő alapján a modul a - parancs, - DscResource, - RoleCapability a tartalom és - paramétereket tartalmaz.
- Keresés-modul verzió paraméterekkel szűrheti: MinimumVersion, MaximumVersion, RequiredVersion, AllVersions.
  - Ezek a paraméterek kölcsönösen kizárják egymást, kivéve a MinmimumVersion és MaximumVersion.
  - Ezen verzió paraméterek csak nevű egy modul nélkül a helyettesítő karakterek megengedettek.
  - A RequiredVersion paraméter nincs megadva, ha a keresés-modul a modult, amely egyenlő vagy nagyobb, mint a minimális verzió van megadva, vagy a legújabb verzióját a modul esetén nincs minimális verzió van megadva a legújabb verzióját adja vissza. 
  - A RequiredVersion paraméter van megadva, az keresés-modul csak adja vissza a modult, amely pontosan megegyezik a megadott version verzióját.
- Keresés-modul a modul metaadatai szűrheti az a – Tag paraméter
- Keresés-modul a tárház vonatkozó keresést nyelvi szűrheti az - szűrő paraméterrel.
- A modul keresése modulok vagy kevés a regisztrált adattárak végezhet.

## <a name="cmdlet-syntax"></a>A parancsmag szintaxisa
```powershell
Get-Command -Name Find-Module -Module PowerShellGet -Syntax
```

## <a name="cmdlet-online-help-reference"></a>A parancsmag online Súgó-hivatkozás

[A modul keresése](http://go.microsoft.com/fwlink/?LinkID=398574)

## <a name="example-commands"></a>Példa parancsok
```powershell
# Find a specific module
Find-Module Azure

Version    Name                                Repository           Description
-------    ----                                ----------           -----------
1.3.2      Azure                               PSGallery            Microsoft Azure PowerShell - Service Management

# Find multiple modules
Find-Module Azure,AzureRM

# Find modules with wildcards in -Name
Find-Module -Name AzureRM*

# Find all versions of a module
Find-Module -Name PSReadline -AllVersions

# Find a module with -MinimumVersion. 
# With MinimumVersion we can find a module whose version is greate than or equal to the specified MinimumVersion value.
Find-Module -Name PSReadline -MinimumVersion 1.0.0.12

# Find a module with MaximumVersion
Find-Module -Name PSReadline -MaximumVersion 1.0.0.13

# Find a module with both MinimumVersion and MaximumVersion range.
Find-Module -Name PSReadline -MinimumVersion 1.0.0.12 -MaximumVersion 1.0.0.13

# Find a module with exact version
Find-Module -Name AzureRM -RequiredVersion 1.3.2

# Find a module with a specific prerelease version
Find-Module -Name AzureRM -RequiredVersion 1.3.2-alpha -AllowPrerelease

# Find a module from the specified repository
Find-Module -Name Contoso -Repository MyLocalRepo

# Find available modules from all registered repositories
Find-Module

# Find available modules from few registered repositories
Find-Module -Repository PSGallery,PrivatePSGallery

# Find a module along with its dependencies
Find-Module -Name AzureRM -IncludeDependencies

# Find all modules with Dsc resources
Find-Module -Includes DscResource

# Find modules with a specific DscResource
Find-Module -DscResource xFirewall

# Find all modules with cmdlets
Find-Module -Includes Cmdlet

# Find all modules with functions
Find-Module -Includes Function

# Find all modules with Role Capabilities
Find-Module -Includes RoleCapability

# Find all modules with the specified Role Capability name
Find-Module -RoleCapability RoleCap1
Find-Module -RoleCapability RoleCap2 -Includes RoleCapability

# Find modules with specific commands
Find-Module -Command Get-ScriptAnalyzerRule, Invoke-ScriptAnalyzer
Find-Module -Command Get-ScriptAnalyzerRule, Invoke-ScriptAnalyzer -Includes Cmdlet
Find-Module -Command Get-ScriptAnalyzerRule, Invoke-ScriptAnalyzer -Includes Function

# Find modules with -Filter based search. -Filter searches in description and names
Find-Module -Filter Cookbook
Find-Module -Filter RBAC
Find-Module -Filter 'App Domain' -Includes 'DscResource'

# Find all modules with tags Azure or DSC
Find-Module -Tag Azure, DSC

# Properties of Find-Module returned object
Find-Module AzureRM.Profile | Format-List * -Force

Name                       : AzureRM.profile
Version                    : 1.0.8
Type                       : Module
Description                : Microsoft Azure PowerShell - Profile credential management cmdlets for Azure Resource
                             Manager
Author                     : Microsoft Corporation
CompanyName                : {elogeel, azure-sdk}
Copyright                  : Microsoft Corporation. All rights reserved.
PublishedDate              : 5/4/2016 9:40:33 PM
InstalledDate              :
UpdatedDate                :
LicenseUri                 : https://raw.githubusercontent.com/Azure/azure-powershell/dev/LICENSE.txt
ProjectUri                 : https://github.com/Azure/azure-powershell
IconUri                    :
Tags                       : {PSModule}
Includes                   : {Function, RoleCapability, Command, DscResource...}
PowerShellGetFormatVersion :
ReleaseNotes               : https://github.com/Azure/azure-powershell/blob/dev/ChangeLog.md
Dependencies               : {}
RepositorySourceLocation   : https://www.powershellgallery.com/api/v2/
Repository                 : PSGallery
PackageManagementProvider  : NuGet
AdditionalMetadata         : {downloadCount, description, copyright, FileList...}

```

