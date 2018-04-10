---
ms.date: 06/12/2017
contributor: manikb
ms.topic: reference
keywords: gyűjtemény, a powershell, a parancsmag, a psget
title: Keresés – parancsprogram
ms.openlocfilehash: 1f5076d94015c0b1041591144f1f0fe36819204b
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="find-script"></a><span data-ttu-id="4e9fc-103">Keresés – parancsprogram</span><span class="sxs-lookup"><span data-stu-id="4e9fc-103">Find-Script</span></span>

<span data-ttu-id="4e9fc-104">A PowerShell parancsfájlok egy online katalógusból megadott feltételeknek megfelelő talál.</span><span class="sxs-lookup"><span data-stu-id="4e9fc-104">Finds the PowerShell script files from an online gallery that match specified criteria.</span></span>

## <a name="description"></a><span data-ttu-id="4e9fc-105">Leírás</span><span class="sxs-lookup"><span data-stu-id="4e9fc-105">Description</span></span>

<span data-ttu-id="4e9fc-106">Keresés-parancsfájl a parancsfájlok a regisztrált tárházak találhatók, amely a megadott feltételeknek megfelelő deríti fel.</span><span class="sxs-lookup"><span data-stu-id="4e9fc-106">Find-Script discovers the script files from registered repositories that matches the specified criteria.</span></span>
<span data-ttu-id="4e9fc-107">Minden parancsprogram található, keresés-parancsfájl egy objektumot ad vissza PSRepositoryItemInfo opcionálisan átirányítható, amely az Install-parancsfájl a parancsfájlok telepítéséhez.</span><span class="sxs-lookup"><span data-stu-id="4e9fc-107">For each script found, Find-Script returns a PSRepositoryItemInfo object which can optionally be piped to Install-Script for installing the scripts.</span></span>
<span data-ttu-id="4e9fc-108">Keresés-parancsfájl parancsmag lehetővé teszi a parancsfájlok, például a neve, címke, szűrő, utasítás neve, verziója tartományon, pontos verziót, összes verzió és annak függőségeit és az adott vagy regisztrált összes adattárak különböző keresési feltételekkel felderítéséhez.</span><span class="sxs-lookup"><span data-stu-id="4e9fc-108">Find-Script cmdlet lets you to discover the script files with different search criteria like name, tag, filter, command name, version range, exact version, all versions, including its dependencies and from specific or all registered repositories.</span></span>

- <span data-ttu-id="4e9fc-109">Keresés-parancsfájlt is szűrő alapján a parancsfájl - paranccsal tartalom és - paramétereket tartalmaz.</span><span class="sxs-lookup"><span data-stu-id="4e9fc-109">Find-Script can filter based on script contents with the -Command and -Includes parameters.</span></span>
- <span data-ttu-id="4e9fc-110">Keresés-parancsfájl verziója paraméterekkel szűrheti: MinimumVersion, MaximumVersion, RequiredVersion, AllVersions.</span><span class="sxs-lookup"><span data-stu-id="4e9fc-110">Find-Script can filter with version parameters: MinimumVersion, MaximumVersion, RequiredVersion, AllVersions.</span></span>
  - <span data-ttu-id="4e9fc-111">Ezek a paraméterek kölcsönösen kizárják egymást, kivéve a MinmimumVersion és MaximumVersion.</span><span class="sxs-lookup"><span data-stu-id="4e9fc-111">These parameters are mutually exclusive, except MinmimumVersion and MaximumVersion.</span></span>
  - <span data-ttu-id="4e9fc-112">Ezen verzió paraméterek csak nevű egyetlen parancsfájllal bármely helyettesítő karakterek nem engedélyezettek.</span><span class="sxs-lookup"><span data-stu-id="4e9fc-112">These version parameters are allowed only with the single script name without any wildcards.</span></span>
  - <span data-ttu-id="4e9fc-113">A RequiredVersion paraméter nincs megadva, ha a keresés-parancsfájl a legújabb verzióját a parancsfájlt, amely egyenlő vagy nagyobb, mint a minimális verzió van megadva, vagy a legújabb verzióját a parancsfájl nincs minimális verzió megadása adja vissza.</span><span class="sxs-lookup"><span data-stu-id="4e9fc-113">If the RequiredVersion parameter is not specified, Find-Script returns the latest version of the script that is equal to or greater than the minimum version specified or the latest version of the script if no minimum version is specified.</span></span>
  - <span data-ttu-id="4e9fc-114">A RequiredVersion paraméter van megadva, az keresés-parancsfájl csak adja vissza a parancsfájlt, amely pontosan megegyezik a megadott version verzióját.</span><span class="sxs-lookup"><span data-stu-id="4e9fc-114">If the RequiredVersion parameter is specified, Find-Script only returns the version of script that exactly matches the specified version.</span></span>
- <span data-ttu-id="4e9fc-115">Keresés-parancsfájl szűrést végezhet a parancsprogram-metaadatait az a – Tag paraméter.</span><span class="sxs-lookup"><span data-stu-id="4e9fc-115">Find-Script can filter on script metadata with the -Tag parameter.</span></span>
- <span data-ttu-id="4e9fc-116">Keresés parancsfájl-tárház vonatkozó keresést nyelvével szűrheti az - szűrő paraméterrel.</span><span class="sxs-lookup"><span data-stu-id="4e9fc-116">Find-Script can filter on repository-specific search language with the -Filter parameter.</span></span>
- <span data-ttu-id="4e9fc-117">Keresés-parancsfájl parancsfájlok vagy kevés a regisztrált adattárak végezhet.</span><span class="sxs-lookup"><span data-stu-id="4e9fc-117">Find-Script can filter on scripts from all or few of the registered repositories.</span></span>

<span data-ttu-id="4e9fc-118">**Megjegyzés:** regisztrált PSRepository rendelkeznie kell egy érvényes ScriptSourceLocation.</span><span class="sxs-lookup"><span data-stu-id="4e9fc-118">**NOTE:** Registered PSRepository should have a valid ScriptSourceLocation.</span></span> <span data-ttu-id="4e9fc-119">A Set-PSRepository ScriptSourceLocation érték használható.</span><span class="sxs-lookup"><span data-stu-id="4e9fc-119">You can use the Set-PSRepository to set ScriptSourceLocation value.</span></span>

## <a name="cmdlet-syntax"></a><span data-ttu-id="4e9fc-120">A parancsmag szintaxisa</span><span class="sxs-lookup"><span data-stu-id="4e9fc-120">Cmdlet syntax</span></span>

```powershell
Get-Command -Name Find-Script -Module PowerShellGet -Syntax
```

## <a name="cmdlet-online-help-reference"></a><span data-ttu-id="4e9fc-121">A parancsmag online Súgó-hivatkozás</span><span class="sxs-lookup"><span data-stu-id="4e9fc-121">Cmdlet online help reference</span></span>

[<span data-ttu-id="4e9fc-122">Find-Script</span><span class="sxs-lookup"><span data-stu-id="4e9fc-122">Find-Script</span></span>](http://go.microsoft.com/fwlink/?LinkId=619785)

## <a name="example-commands"></a><span data-ttu-id="4e9fc-123">Példa parancsok</span><span class="sxs-lookup"><span data-stu-id="4e9fc-123">Example commands</span></span>

```powershell
# Find a script from the registered repository with ScriptSourceLocation
Find-Script Connect-AzureVM

Version    Name                                Repository           Description
-------    ----                                ----------           -----------
1.0        Connect-AzureVM                     PSGallery            This runbook sets up a connection to an Azure vi...

# Find multiple scripts
Find-Script -Name Connect-AzureVM, Show-Tree, Connect-O365

# Find scripts with wildcards in -Name
Find-Script -Name *Azure*

# Find all versions of a script
Find-Script -Name Connect-O365 -AllVersions

# Find a script with -MinimumVersion.
# With MinimumVersion we can find a script whose version is greate than or equal to the specified MinimumVersion value.
Find-Script Connect-O365 -MinimumVersion 1.4

# Find a script with MaximumVersion
Find-Script -Name Connect-O365 -MaximumVersion 1.6.2

# Find a script with both MinimumVersion and MaximumVersion range.
Find-Script -Name Connect-O365 -MinimumVersion 1.1 -MaximumVersion 1.6.2

# Find a script with exact version
Find-Script -Name Connect-O365 -RequiredVersion 1.5.7

# Find a script with a specific pre-release version
Find-Script -Name Connect-O365 -RequiredVersion 1.3.2-alpha -AllowPrerelease

# Find a script from the specified repository
Find-Script -Name Fabrikam-ServerScript -Repository MyLocalRepo

# Find available scripts from all registered repositories
Find-Script

# Find available scripts from few registered repositories
Find-Script -Repository PSGallery, PrivatePSGallery

# Find a script along with its dependent modules and scripts
Find-Script -Name Connect-AzureVM -IncludeDependencies

Version    Name                                Repository           Description
-------    ----                                ----------           -----------
1.0        Connect-AzureVM                     PSGallery            This runbook sets up a connection to an Azure vi...
1.4.0      Azure                               PSGallery            Microsoft Azure PowerShell - Service Management
1.1.2      Azure.Storage                       PSGallery            Microsoft Azure PowerShell - Storage service cmd...
1.0.8      AzureRM.profile                     PSGallery            Microsoft Azure PowerShell - Profile credential ...

# Find all scripts with workflows
Find-Script -Includes Workflow

# Find all scripts with functions
Find-Script -Includes Function

# Find scripts with specific commands
Find-Script -Command Log-Message
Find-Script -Command Log-Message, Show-Tree -Includes Function
Find-Script -Command Connect-AzureVM -Includes Workflow

# Find scripts with -Filter based search. -Filter searches in description and names
Find-Script -Filter Windows
Find-Script -Filter Azure

# Find all scripts with tags O365 or Nano
Find-Script -Tag O365, Nano

# Properties of Find-Script returned object
Find-Script Show-Tree | Format-List * -Force
Name                       : Show-Tree
Version                    : 1.0.0
Type                       : Script
Description                : Script to show the layout of PowerShell namespaces (Trees) using ASCII
Author                     : Jeffrey Snover
CompanyName                : jsnover
Copyright                  : (C) Microsoft Corporation. All rights reserved.
PublishedDate              : 2/15/2016 10:15:35 PM
InstalledDate              :
UpdatedDate                :
LicenseUri                 :
ProjectUri                 :
IconUri                    :
Tags                       : {Nano, PSScript}
Includes                   : {Function, RoleCapability, Command, DscResource...}
PowerShellGetFormatVersion :
ReleaseNotes               :
Dependencies               : {}
RepositorySourceLocation   : https://www.powershellgallery.com/api/v2/
Repository                 : PSGallery
PackageManagementProvider  : NuGet
AdditionalMetadata         : {versionDownloadCount, ItemType, copyright, PackageManagementProvider...}


# Includes property on PSRepositoryItemInfo object
$t = Find-Script -Includes Workflow -Repository INT -Name Fabrikam-ClientScript
$t.Includes

Name                           Value
----                           -----
Function                       {Test-FunctionFromScript_Fabrikam-ClientScript}
RoleCapability                 {}
Command                        {Test-FunctionFromScript_Fabrikam-ClientScript, Test-WorkflowFromScript_Fabrikam-Clie...
DscResource                    {}
Workflow                       {Test-WorkflowFromScript_Fabrikam-ClientScript}
Cmdlet                         {}


```