---
ms.date: 06/12/2017
contributor: JKeithB
keywords: katalógus, a powershell, a parancsmag, a psgallery
title: Keresési eredmények szűrése
ms.openlocfilehash: 13270a310613a974e1588a9f56d443a936cfebb8
ms.sourcegitcommit: 98b7cfd8ad5718efa8e320526ca76c3cc4141d78
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/25/2018
ms.locfileid: "50004122"
---
# <a name="filtering-search-results"></a><span data-ttu-id="8df4b-103">Keresési eredmények szűrése</span><span class="sxs-lookup"><span data-stu-id="8df4b-103">Filtering search results</span></span>

<span data-ttu-id="8df4b-104">A [csomagok lapján](https://www.powershellgallery.com/packages) jeleníti meg az összes elérhető csomagokat a PowerShell-galériában.</span><span class="sxs-lookup"><span data-stu-id="8df4b-104">The [Packages tab](https://www.powershellgallery.com/packages) displays all available packages in the PowerShell Gallery.</span></span>

<span data-ttu-id="8df4b-105">Számos módon szűrése, rendezése és keresése a csomagokat.</span><span class="sxs-lookup"><span data-stu-id="8df4b-105">There are several ways to filter, sort, and search the packages.</span></span>
<span data-ttu-id="8df4b-106">Egy adott csomag részleteinek megtekintéséhez kattintson a csomagot.</span><span class="sxs-lookup"><span data-stu-id="8df4b-106">To see more details about a particular package, click the package.</span></span>

## <a name="filter-by"></a><span data-ttu-id="8df4b-107">Szűrés</span><span class="sxs-lookup"><span data-stu-id="8df4b-107">Filter By</span></span>

<span data-ttu-id="8df4b-108">A legördülő "Szűrő által" alatt lehetővé teszi a felhasználóknak szűrheti az eredményeket:</span><span class="sxs-lookup"><span data-stu-id="8df4b-108">The drop-down under "Filter By" allows users to filter the results by:</span></span>
- <span data-ttu-id="8df4b-109">Előzetes verzió</span><span class="sxs-lookup"><span data-stu-id="8df4b-109">Include Prerelease</span></span>
- <span data-ttu-id="8df4b-110">Csak állandó</span><span class="sxs-lookup"><span data-stu-id="8df4b-110">Stable Only</span></span>

<span data-ttu-id="8df4b-111">"Előzetes" és "Stabil" kapcsolatos információkért lásd: [Prerelease Versioning adja hozzá a PowerShellGet és PowerShell-galériából](https://blogs.msdn.microsoft.com/powershell/2017/12/05/prerelease-versioning-added-to-powershellget-and-powershell-gallery/) a PowerShell csapatának blogját.</span><span class="sxs-lookup"><span data-stu-id="8df4b-111">For information about "Prerelease" and "Stable", see [Prerelease Versioning Added to PowerShellGet and PowerShell Gallery](https://blogs.msdn.microsoft.com/powershell/2017/12/05/prerelease-versioning-added-to-powershellget-and-powershell-gallery/) in the PowerShell Team Blog.</span></span>

<span data-ttu-id="8df4b-112">A jelölőnégyzetek alatt a legördülő engedélyezése a felhasználók által az eredmények szűréséhez:</span><span class="sxs-lookup"><span data-stu-id="8df4b-112">The checkboxes under the drop-down allow users to filter the results by:</span></span>
- <span data-ttu-id="8df4b-113">A csomagok</span><span class="sxs-lookup"><span data-stu-id="8df4b-113">Package Types</span></span>
  - <span data-ttu-id="8df4b-114">Modul</span><span class="sxs-lookup"><span data-stu-id="8df4b-114">Module</span></span>
  - <span data-ttu-id="8df4b-115">Parancsfájl</span><span class="sxs-lookup"><span data-stu-id="8df4b-115">Script</span></span>
- <span data-ttu-id="8df4b-116">Kategóriák</span><span class="sxs-lookup"><span data-stu-id="8df4b-116">Categories</span></span>
  - <span data-ttu-id="8df4b-117">Parancsmag</span><span class="sxs-lookup"><span data-stu-id="8df4b-117">Cmdlet</span></span>
  - <span data-ttu-id="8df4b-118">DSC-erőforrás</span><span class="sxs-lookup"><span data-stu-id="8df4b-118">DSC Resource</span></span>
  - <span data-ttu-id="8df4b-119">Függvény</span><span class="sxs-lookup"><span data-stu-id="8df4b-119">Function</span></span>
  - <span data-ttu-id="8df4b-120">Szerepkör-képesség</span><span class="sxs-lookup"><span data-stu-id="8df4b-120">Role Capability</span></span>
  - <span data-ttu-id="8df4b-121">A munkafolyamat</span><span class="sxs-lookup"><span data-stu-id="8df4b-121">Workflow</span></span>

<span data-ttu-id="8df4b-122">Csak a PowerShell-galériából a modulok megtekintéséhez ellenőrizze a csomag típusok modul.</span><span class="sxs-lookup"><span data-stu-id="8df4b-122">To see only modules in the PowerShell Gallery, check Module in the Package Types.</span></span>
<span data-ttu-id="8df4b-123">Ehhez hasonlóan a szeretné csak a PowerShell-galériából a parancsfájlokat, ellenőrizze a csomag típusok parancsfájlt.</span><span class="sxs-lookup"><span data-stu-id="8df4b-123">Similarly, to see only scripts in the PowerShell Gallery, check Script in the Package Types.</span></span>

> [!NOTE]
> <span data-ttu-id="8df4b-124">Szűrők jellegűek.</span><span class="sxs-lookup"><span data-stu-id="8df4b-124">Filters are inclusive.</span></span>
> <span data-ttu-id="8df4b-125">Példa: Parancsmagok és a functions tartalmazó csomag jelenik meg, ha a rendszer ellenőrzi a parancsmag vagy függvényben (vagy mindkettő).</span><span class="sxs-lookup"><span data-stu-id="8df4b-125">Example: A package containing both cmdlets and functions will appear if either Cmdlet or Function (or both) are checked.</span></span>
> <span data-ttu-id="8df4b-126">Ha egyik sincs kijelölve, a csomag nem jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="8df4b-126">If neither are selected, the package will not appear.</span></span>
> <span data-ttu-id="8df4b-127">Hasonlóképpen ha az összes kategória ki van jelölve, csak az ezekben a kategóriákban egyikét tartalmazó csomagok fog megjelenni.</span><span class="sxs-lookup"><span data-stu-id="8df4b-127">Similarly, if all categories are selected, only packages containing one of those categories will appear.</span></span>
> <span data-ttu-id="8df4b-128">**Csomagok, amelyek nem tartozik egyik ezekben a kategóriákban nem jelenik meg.**</span><span class="sxs-lookup"><span data-stu-id="8df4b-128">**Packages that do not belong to any of those categories will not appear.**</span></span>

## <a name="sort-by"></a><span data-ttu-id="8df4b-129">Rendezés szempontja:</span><span class="sxs-lookup"><span data-stu-id="8df4b-129">Sort By</span></span>

<span data-ttu-id="8df4b-130">A Rendezés legördülő lehetővé teszi, hogy a felhasználók által az eredmények rendezéséhez:</span><span class="sxs-lookup"><span data-stu-id="8df4b-130">The Sort By drop-down allows users to sort the results by:</span></span>
- <span data-ttu-id="8df4b-131">Népszerűség - népszerűsége letöltése száma határozza meg</span><span class="sxs-lookup"><span data-stu-id="8df4b-131">Popularity - Popularity is determined by Download Count</span></span>
- <span data-ttu-id="8df4b-132">A-Z - csomag neve alapján betűrendben</span><span class="sxs-lookup"><span data-stu-id="8df4b-132">A-Z - Alphabetically by package name</span></span>
- <span data-ttu-id="8df4b-133">Legutóbbi - csomagok megjelennek a közzététel dátuma sorrendje</span><span class="sxs-lookup"><span data-stu-id="8df4b-133">Recent - Packages appear in order of publish date</span></span>

## <a name="search-box"></a><span data-ttu-id="8df4b-134">Keresőmező</span><span class="sxs-lookup"><span data-stu-id="8df4b-134">Search Box</span></span>

<span data-ttu-id="8df4b-135">A keresőmezőbe lehetővé teszi a felhasználóknak a csomagokat a kulcsszavak keresése.</span><span class="sxs-lookup"><span data-stu-id="8df4b-135">The Search Box allows users to search the packages on keywords.</span></span>
<span data-ttu-id="8df4b-136">További információkért lásd: [Katalóguskeresési szintaxis](search-syntax.md).</span><span class="sxs-lookup"><span data-stu-id="8df4b-136">For more information, see [Gallery Search Syntax](search-syntax.md).</span></span>
