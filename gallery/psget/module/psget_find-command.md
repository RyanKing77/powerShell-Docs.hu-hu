---
ms.date: 06/12/2017
contributor: manikb
ms.topic: reference
keywords: gyűjtemény, a powershell, a parancsmag, a psget
title: Keresés – parancs
ms.openlocfilehash: 26ddf4824816db245131a0fc95b7d2a88bef8f4c
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="find-command"></a><span data-ttu-id="8028a-103">Keresés – parancs</span><span class="sxs-lookup"><span data-stu-id="8028a-103">Find-Command</span></span>

<span data-ttu-id="8028a-104">Megkeresi a PowerShell-parancsok modulban.</span><span class="sxs-lookup"><span data-stu-id="8028a-104">Finds PowerShell commands in modules.</span></span>

## <a name="description"></a><span data-ttu-id="8028a-105">Leírás</span><span class="sxs-lookup"><span data-stu-id="8028a-105">Description</span></span>
<span data-ttu-id="8028a-106">A keresés-Command parancsmaggal megkeresi a PowerShell-parancsok, például a parancsmagok, aliasok, függvények és munkafolyamatok.</span><span class="sxs-lookup"><span data-stu-id="8028a-106">The Find-Command cmdlet finds PowerShell commands such as cmdlets, aliases, functions, and workflows.</span></span> <span data-ttu-id="8028a-107">Keresés – parancs modulok regisztrált adattárak keresi.</span><span class="sxs-lookup"><span data-stu-id="8028a-107">Find-Command searches modules in registered repositories.</span></span>
<span data-ttu-id="8028a-108">Az egyes parancsok, ez a parancsmag által megtalált egy PSGetCommandInfo objektum beállítása/beolvasása.</span><span class="sxs-lookup"><span data-stu-id="8028a-108">For each command that this cmdlet finds, it returns a PSGetCommandInfo object.</span></span> <span data-ttu-id="8028a-109">Az Install-modul parancsmag telepíti a modult, amely tartalmazza a parancsot egy PSGetCommandInfo objektumot tud átadni.</span><span class="sxs-lookup"><span data-stu-id="8028a-109">You can pass a PSGetCommandInfo object to the Install-Module cmdlet to install the module that contains the command.</span></span>

- <span data-ttu-id="8028a-110">Keresés-parancs verzió paraméterekkel szűrheti: MinimumVersion, RequiredVersion, AllVersions.</span><span class="sxs-lookup"><span data-stu-id="8028a-110">Find-Command can filter with version parameters: MinimumVersion, RequiredVersion, AllVersions.</span></span>
  - <span data-ttu-id="8028a-111">Ezek a paraméterek kölcsönösen kizárják egymást.</span><span class="sxs-lookup"><span data-stu-id="8028a-111">These parameters are mutually exclusive.</span></span>
  - <span data-ttu-id="8028a-112">Ezen verzió paraméterek csak nevű egy modul nélkül a helyettesítő karakterek megengedettek.</span><span class="sxs-lookup"><span data-stu-id="8028a-112">These version parameters are allowed only with the single module name without any wildcards.</span></span>
  - <span data-ttu-id="8028a-113">A RequiredVersion paraméter nincs megadva, ha a Keresés-parancs a modult, amely egyenlő vagy nagyobb, mint a minimális verzió van megadva, vagy a legújabb verzióját a modul esetén nincs minimális verzió van megadva a legújabb verzióját adja vissza.</span><span class="sxs-lookup"><span data-stu-id="8028a-113">If the RequiredVersion parameter is not specified, Find-Command returns the latest version of the module that is equal to or greater than the minimum version specified or the latest version of the module if no minimum version is specified.</span></span>
  - <span data-ttu-id="8028a-114">A RequiredVersion paraméter van megadva, ha Keresés-parancs, az csak a modult, amely pontosan megegyezik a megadott version verzióját adja vissza.</span><span class="sxs-lookup"><span data-stu-id="8028a-114">If the RequiredVersion parameter is specified, Find-Command only returns the version of the module that exactly matches the specified version.</span></span>
- <span data-ttu-id="8028a-115">Keresés – parancs szűrést végezhet a modul metaadatai paraméterrel - címke</span><span class="sxs-lookup"><span data-stu-id="8028a-115">Find-Command can filter on module metadata with the -Tag parameter</span></span>
- <span data-ttu-id="8028a-116">Keresés – parancs szűrést végezhet a tárház vonatkozó keresést nyelvi paraméterrel - szűrő.</span><span class="sxs-lookup"><span data-stu-id="8028a-116">Find-Command can filter on repository-specific search language with the -Filter parameter.</span></span>
- <span data-ttu-id="8028a-117">Keresés – parancs modulok vagy kevés a regisztrált adattárak végezhet.</span><span class="sxs-lookup"><span data-stu-id="8028a-117">Find-Command can filter on modules from all or few of the registered repositories.</span></span>

## <a name="cmdlet-syntax"></a><span data-ttu-id="8028a-118">A parancsmag szintaxisa</span><span class="sxs-lookup"><span data-stu-id="8028a-118">Cmdlet syntax</span></span>
```powershell
Get-Command -Name Find-Command -Module PowerShellGet -Syntax
```

## <a name="cmdlet-online-help-reference"></a><span data-ttu-id="8028a-119">A parancsmag online Súgó-hivatkozás</span><span class="sxs-lookup"><span data-stu-id="8028a-119">Cmdlet online help reference</span></span>

[<span data-ttu-id="8028a-120">Keresés – parancs</span><span class="sxs-lookup"><span data-stu-id="8028a-120">Find-Command</span></span>](http://go.microsoft.com/fwlink/?LinkId=733636)

## <a name="example-commands"></a><span data-ttu-id="8028a-121">Példa parancsok</span><span class="sxs-lookup"><span data-stu-id="8028a-121">Example commands</span></span>
```powershell

# Find a specific command
Find-Command -Name Get-ScriptAnalyzerRule

Name                                Version    ModuleName                          Repository
----                                -------    ----------                          ----------
Get-ScriptAnalyzerRule              1.5.0      PSScriptAnalyzer                    PSGallery

# Find multiple commands
Find-Command -Name Get-ScriptAnalyzerRule, Invoke-ScriptAnalyzer

# Find all available commands from all registered repositories
Find-Command

# Find available commands from few registered repositories
Find-Command -Repository PSGallery,PrivatePSGallery

# Find all commands in a specified repository
Find-Command -Repository PSGallery

# Find a command defined in a specific module
Find-Command -Name Get-ScriptAnalyzerRule -Module PSScriptAnalyzer

# Find commands from all versions of a module
Find-Command -ModuleName PSReadline -AllVersions

# Find commands with module name and MinimumVersion.
Find-Command -ModuleName PSReadline -MinimumVersion 1.1

# Find commands with module name and exact version
Find-Command -ModuleName AzureRM -RequiredVersion 1.4.0

# Find commands defined modules with -Filter based search. -Filter searches in description and module names
Find-Command -Filter Cookbook
Find-Command -Filter RBAC

# Find all commands with tags Azure or DSC in module metadata
Find-Command -Tag Azure, DSC

```