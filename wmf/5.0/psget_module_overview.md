---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: a0b1573611c5d4232082c19ca19b4cca79d0699e
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55685255"
---
# <a name="powershell-module-discovery-install-and-inventory-with-powershellget"></a><span data-ttu-id="16cd2-102">PowerShell-modulok felderítése, telepítése és Leltárazása a powershellgettel</span><span class="sxs-lookup"><span data-stu-id="16cd2-102">PowerShell Module Discovery, Install and Inventory with PowerShellGet</span></span>

<span data-ttu-id="16cd2-103">A PowerShellGet ebben a kiadásban a WMF tartalmazza:</span><span class="sxs-lookup"><span data-stu-id="16cd2-103">PowerShellGet is included in this release of WMF:</span></span>
-   <span data-ttu-id="16cd2-104">Modul metaadatainak szűrésével find-Module-a - Tag paraméter</span><span class="sxs-lookup"><span data-stu-id="16cd2-104">Find-Module can filter on module metadata with the -Tag parameter</span></span>
-   <span data-ttu-id="16cd2-105">Tárház-specifikus keresési nyelv szűrésével find-Module-a - Filter paraméter</span><span class="sxs-lookup"><span data-stu-id="16cd2-105">Find-Module can filter on repository-specific search language with the -Filter parameter</span></span>
-   <span data-ttu-id="16cd2-106">Find-Module is szűrés annak alapján, a modul tartalmának a - paranccsal, - DscResource, és - paramétereket</span><span class="sxs-lookup"><span data-stu-id="16cd2-106">Find-Module can filter based on module contents with the -Command, -DscResource, and -Includes parameters</span></span>
-   <span data-ttu-id="16cd2-107">Find-DscResource lehetővé teszi, hogy az egyes DSC-erőforrások tárházakban</span><span class="sxs-lookup"><span data-stu-id="16cd2-107">Find-DscResource allows discovery of individual DSC resources in repositories</span></span>
-   <span data-ttu-id="16cd2-108">A telepítés és NuGet fájlmegosztások közzétételét támogatása</span><span class="sxs-lookup"><span data-stu-id="16cd2-108">Support for installing from and publishing to file shares with NuGet</span></span>

## <a name="example-commands"></a><span data-ttu-id="16cd2-109">Példaparancsok</span><span class="sxs-lookup"><span data-stu-id="16cd2-109">Example commands</span></span>
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

## <a name="new-features-in-powershellget"></a><span data-ttu-id="16cd2-110">A PowerShellGet az új funkciói</span><span class="sxs-lookup"><span data-stu-id="16cd2-110">New features in PowerShellGet</span></span>
-   <span data-ttu-id="16cd2-111">Egymás melletti verzió támogatása a Windows PowerShell 5.0-s vagy újabb</span><span class="sxs-lookup"><span data-stu-id="16cd2-111">Side-by-side version support on Windows PowerShell 5.0 or newer</span></span>
-   <span data-ttu-id="16cd2-112">A modul függőséget telepítés támogatása</span><span class="sxs-lookup"><span data-stu-id="16cd2-112">Module dependency installation support</span></span>
-   <span data-ttu-id="16cd2-113">Három új parancsmagok</span><span class="sxs-lookup"><span data-stu-id="16cd2-113">Three new cmdlets</span></span>
    -   <span data-ttu-id="16cd2-114">Get-InstalledModule</span><span class="sxs-lookup"><span data-stu-id="16cd2-114">Get-InstalledModule</span></span>
    -   <span data-ttu-id="16cd2-115">Uninstall-Module</span><span class="sxs-lookup"><span data-stu-id="16cd2-115">Uninstall-Module</span></span>
    -   <span data-ttu-id="16cd2-116">Save-Module</span><span class="sxs-lookup"><span data-stu-id="16cd2-116">Save-Module</span></span>
