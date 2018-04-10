---
ms.date: 06/12/2017
contributor: manikb
ms.topic: reference
keywords: gyűjtemény, a powershell, a parancsmag, a psget
title: Get-InstalledScript
ms.openlocfilehash: 668327905b0dab40119940a3134b674c452f538d
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="get-installedscript"></a><span data-ttu-id="a5ae8-103">Get-InstalledScript</span><span class="sxs-lookup"><span data-stu-id="a5ae8-103">Get-InstalledScript</span></span>

<span data-ttu-id="a5ae8-104">Lekérdezi a számítógépen telepített parancsfájlok.</span><span class="sxs-lookup"><span data-stu-id="a5ae8-104">Gets installed scripts on a computer.</span></span>

## <a name="description"></a><span data-ttu-id="a5ae8-105">Leírás</span><span class="sxs-lookup"><span data-stu-id="a5ae8-105">Description</span></span>

<span data-ttu-id="a5ae8-106">A Get-InstalledScript parancsmag lekéri a telepített PowerShell-parancsfájlok a számítógépen.</span><span class="sxs-lookup"><span data-stu-id="a5ae8-106">The Get-InstalledScript cmdlet gets installed PowerShell scripts on a computer.</span></span>

<span data-ttu-id="a5ae8-107">Minden telepített parancsprogram Get-InstalledScript ad vissza egy PSRepositoryItemInfo objektumon, amelynek opcionálisan átirányítható eltávolítás-parancsfájl a telepített parancsfájlok eltávolításához.</span><span class="sxs-lookup"><span data-stu-id="a5ae8-107">For each installed script, Get-InstalledScript returns a PSRepositoryItemInfo object which can optionally be piped to Uninstall-Script for uninstalling the installed scripts.</span></span>

- <span data-ttu-id="a5ae8-108">Get-InstalledScript telepített parancsfájlok neve, verziója paraméterek alapján szűrhetők.</span><span class="sxs-lookup"><span data-stu-id="a5ae8-108">Get-InstalledScript can filter installed scripts based on name, version parameters.</span></span>
- <span data-ttu-id="a5ae8-109">Get-InstalledScript verzió paraméterekkel szűrheti: MinimumVersion, MaximumVersion, RequiredVersion, AllVersions.</span><span class="sxs-lookup"><span data-stu-id="a5ae8-109">Get-InstalledScript can filter with version parameters: MinimumVersion, MaximumVersion, RequiredVersion, AllVersions.</span></span>
  - <span data-ttu-id="a5ae8-110">Ezek a paraméterek kölcsönösen kizárják egymást, kivéve a MinmimumVersion és MaximumVersion.</span><span class="sxs-lookup"><span data-stu-id="a5ae8-110">These parameters are mutually exclusive, except MinmimumVersion and MaximumVersion.</span></span>
  - <span data-ttu-id="a5ae8-111">Ezen verzió paraméterek csak nevű egyetlen parancsfájllal bármely helyettesítő karakterek nem engedélyezettek.</span><span class="sxs-lookup"><span data-stu-id="a5ae8-111">These version parameters are allowed only with the single script name without any wildcards.</span></span>
  - <span data-ttu-id="a5ae8-112">Ha a RequiredVersion paraméter nincs megadva, a Get-InstalledScript a legújabb verzióját a telepített parancsfájl, amely egyenlő vagy nagyobb, mint a minimális verzió van megadva, vagy a legújabb verzióját a parancsfájl nincs minimális verzió megadása adja vissza.</span><span class="sxs-lookup"><span data-stu-id="a5ae8-112">If the RequiredVersion parameter is not specified, Get-InstalledScript returns the latest version of the installed script that is equal to or greater than the minimum version specified or the latest version of the script if no minimum version is specified.</span></span>
  - <span data-ttu-id="a5ae8-113">A RequiredVersion paraméter van megadva, az Get-InstalledScript csak adja vissza a telepített parancsfájl, amely pontosan megegyezik a megadott version verzióját.</span><span class="sxs-lookup"><span data-stu-id="a5ae8-113">If the RequiredVersion parameter is specified, Get-InstalledScript only returns the version of installed script that exactly matches the specified version.</span></span>

## <a name="cmdlet-syntax"></a><span data-ttu-id="a5ae8-114">A parancsmag szintaxisa</span><span class="sxs-lookup"><span data-stu-id="a5ae8-114">Cmdlet syntax</span></span>

```powershell
Get-Command -Name Get-InstalledScript -Module PowerShellGet -Syntax
```

## <a name="cmdlet-online-help-reference"></a><span data-ttu-id="a5ae8-115">A parancsmag online Súgó-hivatkozás</span><span class="sxs-lookup"><span data-stu-id="a5ae8-115">Cmdlet online help reference</span></span>

[<span data-ttu-id="a5ae8-116">Get-InstalledScript</span><span class="sxs-lookup"><span data-stu-id="a5ae8-116">Get-InstalledScript</span></span>](http://go.microsoft.com/fwlink/?LinkId=619790)

## <a name="example-commands"></a><span data-ttu-id="a5ae8-117">Példa parancsok</span><span class="sxs-lookup"><span data-stu-id="a5ae8-117">Example commands</span></span>

```powershell

# Get all scripts installed using PowerShellGet cmdlets
Get-InstalledScript

# Get a specific installed script
Get-InstalledScript Show-Tree

Version    Name                                Repository           Description
-------    ----                                ----------           -----------
1.0.0      Show-Tree                           PSGallery            Script to show the layout of PowerShell namespaces (Tr...

# Get installed script with wildcards
Get-InstalledScript -Name *Azure*

# Get all versions of an installed script
Get-InstalledScript -Name Connect-O365 -AllVersions

# Get installed script with MinimumVersion
Get-InstalledScript -Name Connect-O365 -MinimumVersion 1.1

# Get installed script with MaximumVersion
Get-InstalledScript -Name Connect-O365 -MaximumVersion 1.6.3

# Get installed script with version range
Get-InstalledScript -Name Connect-O365 -MinimumVersion 1.1 -MaximumVersion 1.6.3

# Get installed script with RequiredVersion
Get-InstalledScript -Name Connect-O365 -RequiredVersion 1.4

# Properties of Get-InstalledScript returned object
Get-InstalledScript Show-Tree | Format-List * -Force

Name                       : Show-Tree
Version                    : 1.0.0
Type                       : Script
Description                : Script to show the layout of PowerShell namespaces (Trees) using ASCII
Author                     : Jeffrey Snover
CompanyName                : jsnover
Copyright                  : (C) Microsoft Corporation. All rights reserved.
PublishedDate              : 2/15/2016 10:15:35 PM
InstalledDate              : 5/4/2016 11:44:13 PM
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
AdditionalMetadata         : {description, installeddate, tags, PackageManagementProvider...}
InstalledLocation          : C:\Program Files\WindowsPowerShell\Scripts


```