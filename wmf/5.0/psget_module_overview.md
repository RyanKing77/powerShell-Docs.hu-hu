---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: 9efc640dfda7e08e59d2c56746facd9658b1f9de
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/17/2018
---
# <a name="powershell-module-discovery-install-and-inventory-with-powershellget"></a><span data-ttu-id="4809d-102">PowerShell modul felderítési, telepítése és PowerShellGet készlethez</span><span class="sxs-lookup"><span data-stu-id="4809d-102">PowerShell Module Discovery, Install and Inventory with PowerShellGet</span></span>

<span data-ttu-id="4809d-103">Ebben a kiadásban a WMF PowerShellGet tartalmazza:</span><span class="sxs-lookup"><span data-stu-id="4809d-103">PowerShellGet is included in this release of WMF:</span></span>
-   <span data-ttu-id="4809d-104">Keresés-modul a modul metaadatai szűrheti az a – Tag paraméter</span><span class="sxs-lookup"><span data-stu-id="4809d-104">Find-Module can filter on module metadata with the -Tag parameter</span></span>
-   <span data-ttu-id="4809d-105">Keresés-modul szűrést végezhet a tárház vonatkozó keresést nyelvi paraméterrel - szűrő</span><span class="sxs-lookup"><span data-stu-id="4809d-105">Find-Module can filter on repository-specific search language with the -Filter parameter</span></span>
-   <span data-ttu-id="4809d-106">Keresés-modul is szűrő alapján a modul tartalmának a - paranccsal - DscResource, és - paramétereket tartalmaz</span><span class="sxs-lookup"><span data-stu-id="4809d-106">Find-Module can filter based on module contents with the -Command, -DscResource, and -Includes parameters</span></span>
-   <span data-ttu-id="4809d-107">Keresés – DscResource lehetővé teszi, hogy a tárolóhelyekkel egyes DSC erőforrásainak felderítése</span><span class="sxs-lookup"><span data-stu-id="4809d-107">Find-DscResource allows discovery of individual DSC resources in repositories</span></span>
-   <span data-ttu-id="4809d-108">A telepítés és a fájlmegosztások a NuGet közzétételi támogatása</span><span class="sxs-lookup"><span data-stu-id="4809d-108">Support for installing from and publishing to file shares with NuGet</span></span>

## <a name="example-commands"></a><span data-ttu-id="4809d-109">Példa parancsok</span><span class="sxs-lookup"><span data-stu-id="4809d-109">Example commands</span></span>
```powershell
\# Find all modules with tags Azure or DSC
Find-Module -Tag Azure, DSC

\# Find modules with a specific DscResource
Find-Module -DscResource xFirewall

\#Find modules with specific commands
Find-Module -Command Get-ScriptAnalyzerRule, Invoke-ScriptAnalyzer

\# Find all modules with Dsc resources
Find-Module -Includes DscResource

\# Find all modules with cmdlets
Find-Module -Includes Cmdlet

\# Find all modules with functions
Find-Module -Includes Function

\# Find all DSC resources
Find-DscResource

\# Find all DSC resources contained within a specific module
Find-DscResource -ModuleName xNetworking

\# Find all DSC resources in modules with DSCResourceKit or DesiredStateConfiguration
Find-DscResource -Tag DesiredStateConfiguration, DSCResourceKit

\# Find modules using -Filter parameter
\# Specified filter value is searched in Name and Description properties
Find-Module -Filter Cookbook -Repository PSGallery
Find-Module -Filter RBAC -Repository PSGallery
```

## <a name="new-features-in-powershellget"></a><span data-ttu-id="4809d-110">Az PowerShellGet új funkciói</span><span class="sxs-lookup"><span data-stu-id="4809d-110">New features in PowerShellGet</span></span>
-   <span data-ttu-id="4809d-111">Egymás melletti verzióinak támogatása a Windows PowerShell 5.0-s vagy újabb</span><span class="sxs-lookup"><span data-stu-id="4809d-111">Side-by-side version support on Windows PowerShell 5.0 or newer</span></span>
-   <span data-ttu-id="4809d-112">A modul függőségi telepítés támogatása</span><span class="sxs-lookup"><span data-stu-id="4809d-112">Module dependency installation support</span></span>
-   <span data-ttu-id="4809d-113">Három új parancsmagok</span><span class="sxs-lookup"><span data-stu-id="4809d-113">Three new cmdlets</span></span>
    -   <span data-ttu-id="4809d-114">Get-InstalledModule</span><span class="sxs-lookup"><span data-stu-id="4809d-114">Get-InstalledModule</span></span>
    -   <span data-ttu-id="4809d-115">Távolítsa el modul</span><span class="sxs-lookup"><span data-stu-id="4809d-115">Uninstall-Module</span></span>
    -   <span data-ttu-id="4809d-116">Mentés-modul</span><span class="sxs-lookup"><span data-stu-id="4809d-116">Save-Module</span></span>
