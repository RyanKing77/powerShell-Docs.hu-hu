---
ms.date: 06/12/2017
contributor: manikb
ms.topic: reference
keywords: gyűjtemény, a powershell, a parancsmag, a psget
title: Keresés – RoleCapability
ms.openlocfilehash: 89aacd604d54f6a5e9752790be65cc3bcc77c8e1
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="find-rolecapability"></a><span data-ttu-id="772ed-103">Keresés – RoleCapability</span><span class="sxs-lookup"><span data-stu-id="772ed-103">Find-RoleCapability</span></span>

<span data-ttu-id="772ed-104">Megkeresi a szerepkör képességek modulban.</span><span class="sxs-lookup"><span data-stu-id="772ed-104">Finds role capabilities in modules.</span></span>

## <a name="description"></a><span data-ttu-id="772ed-105">Leírás</span><span class="sxs-lookup"><span data-stu-id="772ed-105">Description</span></span>
<span data-ttu-id="772ed-106">A keresés-RoleCapability parancsmag PowerShell szerepkör képességek modulok talál.</span><span class="sxs-lookup"><span data-stu-id="772ed-106">The Find-RoleCapability cmdlet finds PowerShell role capabilities in modules.</span></span> <span data-ttu-id="772ed-107">Keresés – RoleCapability modulok regisztrált adattárak keresi.</span><span class="sxs-lookup"><span data-stu-id="772ed-107">Find-RoleCapability searches modules in registered repositories.</span></span>
<span data-ttu-id="772ed-108">Az egyes szerepkör képesség, ez a parancsmag által megtalált egy PSGetRoleCapabilityInfo objektum beállítása/beolvasása.</span><span class="sxs-lookup"><span data-stu-id="772ed-108">For each role capability that this cmdlet finds, it returns a PSGetRoleCapabilityInfo object.</span></span> <span data-ttu-id="772ed-109">A modul, amely tartalmazza a szerepkör funkció telepítése a telepítés-modul a parancsmag egy PSGetRoleCapabilityInfo objektumot tud átadni.</span><span class="sxs-lookup"><span data-stu-id="772ed-109">You can pass a PSGetRoleCapabilityInfo object to the Install-Module cmdlet to install the module that contains the role capability.</span></span>
<span data-ttu-id="772ed-110">PowerShell szerepkör képességek határozza meg, amely parancsokat, alkalmazásokat, és így tovább egy felhasználó egy csak elég adminisztrációs (JEA) végpont elérhető.</span><span class="sxs-lookup"><span data-stu-id="772ed-110">PowerShell role capabilities define which commands, applications, and so on are available to a user at a Just Enough Administration (JEA) endpoint.</span></span> <span data-ttu-id="772ed-111">Szerepkör képességek .psrc kiterjesztésű fájlok határozzák meg.</span><span class="sxs-lookup"><span data-stu-id="772ed-111">Role capabilities are defined by files with a .psrc extension.</span></span>

- <span data-ttu-id="772ed-112">Keresés-RoleCapability verzió paraméterekkel szűrheti: MinimumVersion, RequiredVersion, AllVersions.</span><span class="sxs-lookup"><span data-stu-id="772ed-112">Find-RoleCapability can filter with version parameters: MinimumVersion, RequiredVersion, AllVersions.</span></span>
  - <span data-ttu-id="772ed-113">Ezek a paraméterek kölcsönösen kizárják egymást.</span><span class="sxs-lookup"><span data-stu-id="772ed-113">These parameters are mutually exclusive.</span></span>
  - <span data-ttu-id="772ed-114">Ezen verzió paraméterek csak nevű egy modul nélkül a helyettesítő karakterek megengedettek.</span><span class="sxs-lookup"><span data-stu-id="772ed-114">These version parameters are allowed only with the single module name without any wildcards.</span></span>
  - <span data-ttu-id="772ed-115">A RequiredVersion paraméter nincs megadva, ha a keresés-RoleCapability a modult, amely egyenlő vagy nagyobb, mint a minimális verzió van megadva, vagy a legújabb verzióját a modul esetén nincs minimális verzió van megadva a legújabb verzióját adja vissza.</span><span class="sxs-lookup"><span data-stu-id="772ed-115">If the RequiredVersion parameter is not specified, Find-RoleCapability returns the latest version of the module that is equal to or greater than the minimum version specified or the latest version of the module if no minimum version is specified.</span></span>
  - <span data-ttu-id="772ed-116">A RequiredVersion paraméter van megadva, ha keresés-RoleCapability, az csak a modult, amely pontosan megegyezik a megadott version verzióját adja vissza.</span><span class="sxs-lookup"><span data-stu-id="772ed-116">If the RequiredVersion parameter is specified, Find-RoleCapability only returns the version of the module that exactly matches the specified version.</span></span>
- <span data-ttu-id="772ed-117">Keresés – RoleCapability szűrést végezhet a modul metaadatai paraméterrel - címke</span><span class="sxs-lookup"><span data-stu-id="772ed-117">Find-RoleCapability can filter on module metadata with the -Tag parameter</span></span>
- <span data-ttu-id="772ed-118">Keresés – RoleCapability szűrést végezhet a tárház vonatkozó keresést nyelvi paraméterrel - szűrő.</span><span class="sxs-lookup"><span data-stu-id="772ed-118">Find-RoleCapability can filter on repository-specific search language with the -Filter parameter.</span></span>
- <span data-ttu-id="772ed-119">Keresés – RoleCapability modulok vagy kevés a regisztrált adattárak végezhet.</span><span class="sxs-lookup"><span data-stu-id="772ed-119">Find-RoleCapability can filter on modules from all or few of the registered repositories.</span></span>

## <a name="cmdlet-syntax"></a><span data-ttu-id="772ed-120">A parancsmag szintaxisa</span><span class="sxs-lookup"><span data-stu-id="772ed-120">Cmdlet syntax</span></span>
```powershell
Get-Command -Name Find-RoleCapability -Module PowerShellGet -Syntax
```

## <a name="cmdlet-online-help-reference"></a><span data-ttu-id="772ed-121">A parancsmag online Súgó-hivatkozás</span><span class="sxs-lookup"><span data-stu-id="772ed-121">Cmdlet online help reference</span></span>

[<span data-ttu-id="772ed-122">Find-RoleCapability</span><span class="sxs-lookup"><span data-stu-id="772ed-122">Find-RoleCapability</span></span>](http://go.microsoft.com/fwlink/?LinkId=718029)

## <a name="example-commands"></a><span data-ttu-id="772ed-123">Példa parancsok</span><span class="sxs-lookup"><span data-stu-id="772ed-123">Example commands</span></span>
```powershell

# Find a specific role capability
Find-RoleCapability -Name Maintenance

Name                                Version    ModuleName                          Repository
----                                -------    ----------                          ----------
Maintenance                         1.5.0      RoleCapModule                       PrivatePSGallery

# Find multiple role capabilities
Find-RoleCapability -Name MyJeaRole, Maintenance

# Find all available role capabilities from all registered repositories
Find-RoleCapability

# Find available role capabilities from few registered repositories
Find-RoleCapability -Repository PSGallery,PrivatePSGallery

# Find all role capabilities in a specified repository
Find-RoleCapability -Repository PSGallery

# Find a role capability defined in a specific module
Find-RoleCapability -Name Maintenance -ModuleName RoleCapModule

# Find role capabilities from all versions of a module
Find-RoleCapability -ModuleName RoleCapModule -AllVersions

# Find role capabilities with module name and MinimumVersion.
Find-RoleCapability -ModuleName RoleCapModule -MinimumVersion 1.1

# Find role capabilities with module name and exact version
Find-RoleCapability -ModuleName RoleCapModule -RequiredVersion 1.4.0

# Find role capabilities defined modules with -Filter based search. -Filter searches in description and module names
Find-RoleCapability -Filter Cookbook
Find-RoleCapability -Filter RBAC

# Find all role capabilities with tags Azure or DSC in module metadata
Find-RoleCapability -Tag Azure, DSC

```