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
# <a name="find-module"></a><span data-ttu-id="85fdc-103">A modul keresése</span><span class="sxs-lookup"><span data-stu-id="85fdc-103">Find-Module</span></span>
<span data-ttu-id="85fdc-104">Megkeresi a megadott feltételeknek megfelelő modulok egy online katalógusból.</span><span class="sxs-lookup"><span data-stu-id="85fdc-104">Finds modules from an online gallery that match specified criteria.</span></span>

## <a name="description"></a><span data-ttu-id="85fdc-105">Leírás</span><span class="sxs-lookup"><span data-stu-id="85fdc-105">Description</span></span>
<span data-ttu-id="85fdc-106">Keresés-modult a modulok regisztrált tárházak találhatók, amely a megadott feltételeknek megfelelő deríti fel.</span><span class="sxs-lookup"><span data-stu-id="85fdc-106">Find-Module discovers the modules from registered repositories that matches the specified criteria.</span></span>
<span data-ttu-id="85fdc-107">Minden modul található, keresés-modul egy objektumot ad vissza PSRepositoryItemInfo opcionálisan átirányítható, amely az Install-modul a modulok telepítése.</span><span class="sxs-lookup"><span data-stu-id="85fdc-107">For each module found, Find-Module returns a PSRepositoryItemInfo object which can optionally be piped to Install-Module for installing the modules.</span></span>

- <span data-ttu-id="85fdc-108">Keresés-modul is szűrő alapján a modul a - parancs, - DscResource, - RoleCapability a tartalom és - paramétereket tartalmaz.</span><span class="sxs-lookup"><span data-stu-id="85fdc-108">Find-Module can filter based on module contents with the -Command, -DscResource, -RoleCapability and -Includes parameters.</span></span>
- <span data-ttu-id="85fdc-109">Keresés-modul verzió paraméterekkel szűrheti: MinimumVersion, MaximumVersion, RequiredVersion, AllVersions.</span><span class="sxs-lookup"><span data-stu-id="85fdc-109">Find-Module can filter with version parameters: MinimumVersion, MaximumVersion, RequiredVersion, AllVersions.</span></span>
  - <span data-ttu-id="85fdc-110">Ezek a paraméterek kölcsönösen kizárják egymást, kivéve a MinmimumVersion és MaximumVersion.</span><span class="sxs-lookup"><span data-stu-id="85fdc-110">These parameters are mutually exclusive, except MinmimumVersion and MaximumVersion.</span></span>
  - <span data-ttu-id="85fdc-111">Ezen verzió paraméterek csak nevű egy modul nélkül a helyettesítő karakterek megengedettek.</span><span class="sxs-lookup"><span data-stu-id="85fdc-111">These version parameters are allowed only with the single module name without any wildcards.</span></span>
  - <span data-ttu-id="85fdc-112">A RequiredVersion paraméter nincs megadva, ha a keresés-modul a modult, amely egyenlő vagy nagyobb, mint a minimális verzió van megadva, vagy a legújabb verzióját a modul esetén nincs minimális verzió van megadva a legújabb verzióját adja vissza.</span><span class="sxs-lookup"><span data-stu-id="85fdc-112">If the RequiredVersion parameter is not specified, Find-Module returns the latest version of the module that is equal to or greater than the minimum version specified or the latest version of the module if no minimum version is specified.</span></span> 
  - <span data-ttu-id="85fdc-113">A RequiredVersion paraméter van megadva, az keresés-modul csak adja vissza a modult, amely pontosan megegyezik a megadott version verzióját.</span><span class="sxs-lookup"><span data-stu-id="85fdc-113">If the RequiredVersion parameter is specified, Find-Module only returns the version of module that exactly matches the specified version.</span></span>
- <span data-ttu-id="85fdc-114">Keresés-modul a modul metaadatai szűrheti az a – Tag paraméter</span><span class="sxs-lookup"><span data-stu-id="85fdc-114">Find-Module can filter on module metadata with the -Tag parameter</span></span>
- <span data-ttu-id="85fdc-115">Keresés-modul a tárház vonatkozó keresést nyelvi szűrheti az - szűrő paraméterrel.</span><span class="sxs-lookup"><span data-stu-id="85fdc-115">Find-Module can filter on repository-specific search language with the -Filter parameter.</span></span>
- <span data-ttu-id="85fdc-116">A modul keresése modulok vagy kevés a regisztrált adattárak végezhet.</span><span class="sxs-lookup"><span data-stu-id="85fdc-116">Find-Module can filter on modules from all or few of the registered repositories.</span></span>

## <a name="cmdlet-syntax"></a><span data-ttu-id="85fdc-117">A parancsmag szintaxisa</span><span class="sxs-lookup"><span data-stu-id="85fdc-117">Cmdlet syntax</span></span>
```powershell
Get-Command -Name Find-Module -Module PowerShellGet -Syntax
```

## <a name="cmdlet-online-help-reference"></a><span data-ttu-id="85fdc-118">A parancsmag online Súgó-hivatkozás</span><span class="sxs-lookup"><span data-stu-id="85fdc-118">Cmdlet online help reference</span></span>

[<span data-ttu-id="85fdc-119">A modul keresése</span><span class="sxs-lookup"><span data-stu-id="85fdc-119">Find-Module</span></span>](http://go.microsoft.com/fwlink/?LinkID=398574)

## <a name="example-commands"></a><span data-ttu-id="85fdc-120">Példa parancsok</span><span class="sxs-lookup"><span data-stu-id="85fdc-120">Example commands</span></span>
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

