---
ms.date: 2017-06-12
contributor: manikb
ms.topic: reference
keywords: "gyűjtemény, a powershell, a parancsmag, a psget"
title: "Keresés – DscResource"
ms.openlocfilehash: 37ba7925d6f73c453126f25e0818b3f8839d3b3b
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2017
---
# <a name="find-dscresource"></a><span data-ttu-id="1bed5-103">Keresés – DscResource</span><span class="sxs-lookup"><span data-stu-id="1bed5-103">Find-DscResource</span></span>

<span data-ttu-id="1bed5-104">A DSC-erőforrásokat keresi az modulok.</span><span class="sxs-lookup"><span data-stu-id="1bed5-104">Finds DSC Resources in modules.</span></span>

## <a name="description"></a><span data-ttu-id="1bed5-105">Leírás</span><span class="sxs-lookup"><span data-stu-id="1bed5-105">Description</span></span>

<span data-ttu-id="1bed5-106">A keresés-DscResource parancsmagot talál [kívánt állapot konfigurációs szolgáltatása (DSC)](https://msdn.microsoft.com/en-us/PowerShell/dsc/overview) regisztrált tárházak találhatók a megadott feltételeknek megfelelő modulban található erőforrást.</span><span class="sxs-lookup"><span data-stu-id="1bed5-106">The Find-DscResource cmdlet finds [Desired State Configuration (DSC)](https://msdn.microsoft.com/en-us/PowerShell/dsc/overview) resources contained in modules that match the specified criteria from registered repositories.</span></span>
<span data-ttu-id="1bed5-107">Minden modul a parancsmag által megtalált keresés-DscResource telepítés-modulhoz, amely a parancsmag visszaadja erőforrásokat tartalmazó moduljainak telepítése egy átadható PSGetDscResourceInfo objektum beállítása/beolvasása.</span><span class="sxs-lookup"><span data-stu-id="1bed5-107">For each module that this cmdlet finds, Find-DscResource returns a PSGetDscResourceInfo object that you can pipe to Install-Module to install the modules containing the resources that this cmdlet returns.</span></span>

<span data-ttu-id="1bed5-108">A DSC-ből egy olyan új felügyeleti platformot, amely lehetővé teszi a telepítésével és konfigurációs adatokat a szoftver szolgáltatások kezelése és a környezet, amelyben a szolgáltatások futnak kezelése a Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1bed5-108">DSC is a new management platform in Windows PowerShell that enables deploying and managing configuration data for software services and managing the environment in which these services run.</span></span>

<span data-ttu-id="1bed5-109">A kívánt állapot konfigurációs szolgáltatása (DSC) forrásokban a építőelemeket DSC-konfiguráció.</span><span class="sxs-lookup"><span data-stu-id="1bed5-109">Desired State Configuration (DSC) Resources provide the building blocks for a DSC configuration.</span></span> <span data-ttu-id="1bed5-110">Egy erőforrás konfigurált (séma), valamint a PowerShell parancsfájl olyan függvényeket tartalmaz, hogy "," meghívja a helyi Configuration Manager (LCM) tulajdonságok közzététele.</span><span class="sxs-lookup"><span data-stu-id="1bed5-110">A resource exposes properties that can be configured (schema) and contains the PowerShell script functions that the Local Configuration Manager (LCM) calls to "make it so".</span></span>

<span data-ttu-id="1bed5-111">Egy erőforrás modellezhető valamilyen általános fájlként, vagy egy olyan IIS-kiszolgálói beállítást legpontosabb.</span><span class="sxs-lookup"><span data-stu-id="1bed5-111">A resource can model something as generic as a file or as specific as an IIS server setting.</span></span> <span data-ttu-id="1bed5-112">Például erőforrások csoportja, amelyek rendszerezi az összes szükséges fájlt a hordozható, és a metaadatok azonosítására, hogyan a az erőforrásokhoz való használatra készült tartalmazó struktúrára DSC modulra van összevonva.</span><span class="sxs-lookup"><span data-stu-id="1bed5-112">Groups of like resources are combined in to a DSC Module, which organizes all the required files in to a structure that is portable and includes metadata to identify how the resources are intended to be used.</span></span>

- <span data-ttu-id="1bed5-113">Keresés-DscResource verzió paraméterekkel szűrheti: MinimumVersion, RequiredVersion, AllVersions.</span><span class="sxs-lookup"><span data-stu-id="1bed5-113">Find-DscResource can filter with version parameters: MinimumVersion, RequiredVersion, AllVersions.</span></span>
  - <span data-ttu-id="1bed5-114">Ezek a paraméterek kölcsönösen kizárják egymást.</span><span class="sxs-lookup"><span data-stu-id="1bed5-114">These parameters are mutually exclusive.</span></span>
  - <span data-ttu-id="1bed5-115">Ezen verzió paraméterek csak nevű egy modul nélkül a helyettesítő karakterek megengedettek.</span><span class="sxs-lookup"><span data-stu-id="1bed5-115">These version parameters are allowed only with the single module name without any wildcards.</span></span>
  - <span data-ttu-id="1bed5-116">A RequiredVersion paraméter nincs megadva, ha a keresés-DscResource a modult, amely egyenlő vagy nagyobb, mint a minimális verzió van megadva, vagy a legújabb verzióját a modul esetén nincs minimális verzió van megadva a legújabb verzióját adja vissza.</span><span class="sxs-lookup"><span data-stu-id="1bed5-116">If the RequiredVersion parameter is not specified, Find-DscResource returns the latest version of the module that is equal to or greater than the minimum version specified or the latest version of the module if no minimum version is specified.</span></span>
  - <span data-ttu-id="1bed5-117">A RequiredVersion paraméter van megadva, ha keresés-DscResource, az csak a modult, amely pontosan megegyezik a megadott version verzióját adja vissza.</span><span class="sxs-lookup"><span data-stu-id="1bed5-117">If the RequiredVersion parameter is specified, Find-DscResource only returns the version of the module that exactly matches the specified version.</span></span>
- <span data-ttu-id="1bed5-118">Keresés – DscResource szűrést végezhet a modul metaadatai paraméterrel - címke</span><span class="sxs-lookup"><span data-stu-id="1bed5-118">Find-DscResource can filter on module metadata with the -Tag parameter</span></span>
- <span data-ttu-id="1bed5-119">Keresés – DscResource szűrést végezhet a tárház vonatkozó keresést nyelvi paraméterrel - szűrő.</span><span class="sxs-lookup"><span data-stu-id="1bed5-119">Find-DscResource can filter on repository-specific search language with the -Filter parameter.</span></span>
- <span data-ttu-id="1bed5-120">Keresés – DscResource modulok vagy kevés a regisztrált adattárak végezhet.</span><span class="sxs-lookup"><span data-stu-id="1bed5-120">Find-DscResource can filter on modules from all or few of the registered repositories.</span></span>

## <a name="cmdlet-syntax"></a><span data-ttu-id="1bed5-121">A parancsmag szintaxisa</span><span class="sxs-lookup"><span data-stu-id="1bed5-121">Cmdlet syntax</span></span>
```powershell
Get-Command -Name Find-DscResource -Module PowerShellGet -Syntax
```

## <a name="cmdlet-online-help-reference"></a><span data-ttu-id="1bed5-122">A parancsmag online Súgó-hivatkozás</span><span class="sxs-lookup"><span data-stu-id="1bed5-122">Cmdlet online help reference</span></span>

[<span data-ttu-id="1bed5-123">Keresés – DscResource</span><span class="sxs-lookup"><span data-stu-id="1bed5-123">Find-DscResource</span></span>](http://go.microsoft.com/fwlink/?LinkId=517196)

## <a name="example-commands"></a><span data-ttu-id="1bed5-124">Példa parancsok</span><span class="sxs-lookup"><span data-stu-id="1bed5-124">Example commands</span></span>
```powershell

# Find a specific DSC Resource
Find-DscResource -Name xIisFeatureDelegation

Name                                Version    ModuleName                          Repository
----                                -------    ----------                          ----------
xIisFeatureDelegation               1.10.0.0   xWebAdministration                  PSGallery

# Find all available DSC Resources from all registered repositories
Find-DscResource

# Find a DSC resource by name
Find-DscResource -Name xWebsite

# Find multiple DSC Resources
Find-DscResource -Name xIisHandler, xFirewall

# Find all DSC resources contained within a specific module
Find-DscResource -ModuleName xNetworking
Find-DscResource -ModuleName xWebAdministration

# Find all DSC resources in modules with DSCResourceKit or DesiredStateConfiguration
Find-DscResource -Tag DesiredStateConfiguration, DSCResourceKit

# Find available DSC Resources from few registered repositories
Find-DscResource -Repository PSGallery,PrivatePSGallery

# Find all DSC Resources in a specified repository
Find-DscResource -Repository PSGallery

# Find DSC Resources from all versions of a module
Find-DscResource -ModuleName xNetworking -AllVersions

# Find DSC Resources with module name and MinimumVersion.
Find-DscResource -ModuleName xNetworking -MinimumVersion 1.1

# Find DSC Resources with module name and exact version
Find-DscResource -ModuleName xNetworking -RequiredVersion 2.1.1

# Find DSC Resources defined modules with -Filter based search. -Filter searches in description and module names
Find-DscResource -Filter Domain

# Find all DSC Resources with tags Azure or DSC in module metadata
Find-DscResource -Tag Azure, DSC

```

