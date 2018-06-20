---
ms.date: 06/12/2017
contributor: JKeithB
keywords: gyűjtemény, a powershell, a parancsmag, a psgallery
title: Keresési eredmények szűréséhez
ms.openlocfilehash: eafbc993a37eaee7413102ef9d669a6b07d6ff6e
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/16/2018
ms.locfileid: "34188808"
---
# <a name="filtering-search-results"></a><span data-ttu-id="a59fb-103">Keresési eredmények szűréséhez</span><span class="sxs-lookup"><span data-stu-id="a59fb-103">Filtering search results</span></span>

<span data-ttu-id="a59fb-104">A [elemek lap](https://www.powershellgallery.com/items) a PowerShell-galériában összes rendelkezésre álló elemek megjelenítése.</span><span class="sxs-lookup"><span data-stu-id="a59fb-104">The [Items tab](https://www.powershellgallery.com/items) displays all available items in the PowerShell Gallery.</span></span>

<span data-ttu-id="a59fb-105">Számos módon szűrése, rendezése és az elemek.</span><span class="sxs-lookup"><span data-stu-id="a59fb-105">There are several ways to filter, sort, and search the items.</span></span>
<span data-ttu-id="a59fb-106">Egy adott elem részletes adatainak megtekintéséhez kattintson az elemet.</span><span class="sxs-lookup"><span data-stu-id="a59fb-106">To see more details about a particular item, click the item.</span></span>

## <a name="filter-by"></a><span data-ttu-id="a59fb-107">Szűrés</span><span class="sxs-lookup"><span data-stu-id="a59fb-107">Filter By</span></span>

<span data-ttu-id="a59fb-108">A legördülő listán a "Szűrő által" lehetővé teszi a felhasználók által az eredmények szűréséhez:</span><span class="sxs-lookup"><span data-stu-id="a59fb-108">The drop-down under "Filter By" allows users to filter the results by:</span></span>
- <span data-ttu-id="a59fb-109">Előzetes tartalmazza</span><span class="sxs-lookup"><span data-stu-id="a59fb-109">Include Prerelease</span></span>
- <span data-ttu-id="a59fb-110">Csak állandó</span><span class="sxs-lookup"><span data-stu-id="a59fb-110">Stable Only</span></span>

<span data-ttu-id="a59fb-111">"Prerelease" és "Stable" kapcsolatos információkért lásd: [Prerelease Versioning PowerShellGet és a PowerShell-galériában hozzáadja](https://blogs.msdn.microsoft.com/powershell/2017/12/05/prerelease-versioning-added-to-powershellget-and-powershell-gallery/) a PowerShell csapatának blogját.</span><span class="sxs-lookup"><span data-stu-id="a59fb-111">For information about "Prerelease" and "Stable", see [Prerelease Versioning Added to PowerShellGet and PowerShell Gallery](https://blogs.msdn.microsoft.com/powershell/2017/12/05/prerelease-versioning-added-to-powershellget-and-powershell-gallery/) in the PowerShell Team Blog.</span></span>

<span data-ttu-id="a59fb-112">A jelölőnégyzet alatti legördülő engedélyezése a felhasználók által az eredmények szűréséhez:</span><span class="sxs-lookup"><span data-stu-id="a59fb-112">The checkboxes under the drop-down allow users to filter the results by:</span></span>
- <span data-ttu-id="a59fb-113">Konfigurációelem-típusok</span><span class="sxs-lookup"><span data-stu-id="a59fb-113">Item Types</span></span>
  - <span data-ttu-id="a59fb-114">Modul</span><span class="sxs-lookup"><span data-stu-id="a59fb-114">Module</span></span>
  - <span data-ttu-id="a59fb-115">Parancsfájl</span><span class="sxs-lookup"><span data-stu-id="a59fb-115">Script</span></span>
- <span data-ttu-id="a59fb-116">Kategóriák</span><span class="sxs-lookup"><span data-stu-id="a59fb-116">Categories</span></span>
  - <span data-ttu-id="a59fb-117">Parancsmag</span><span class="sxs-lookup"><span data-stu-id="a59fb-117">Cmdlet</span></span>
  - <span data-ttu-id="a59fb-118">A DSC-erőforrás</span><span class="sxs-lookup"><span data-stu-id="a59fb-118">DSC Resource</span></span>
  - <span data-ttu-id="a59fb-119">Függvény</span><span class="sxs-lookup"><span data-stu-id="a59fb-119">Function</span></span>
  - <span data-ttu-id="a59fb-120">Szerepkör-funkció</span><span class="sxs-lookup"><span data-stu-id="a59fb-120">Role Capability</span></span>
  - <span data-ttu-id="a59fb-121">munkafolyamat</span><span class="sxs-lookup"><span data-stu-id="a59fb-121">Workflow</span></span>

<span data-ttu-id="a59fb-122">Tekintse meg a PowerShell-galériában csak modulok, ellenőrizze a Konfigurációelem-típusok modulja.</span><span class="sxs-lookup"><span data-stu-id="a59fb-122">To see only modules in the PowerShell Gallery, check Module in the Item Types.</span></span>
<span data-ttu-id="a59fb-123">Csak a PowerShell-galériában parancsfájlok megtekintéséhez hasonlóan ellenőrizze a Konfigurációelem-típusok parancsfájl.</span><span class="sxs-lookup"><span data-stu-id="a59fb-123">Similarly, to see only scripts in the PowerShell Gallery, check Script in the Item Types.</span></span>

> [!NOTE]
> <span data-ttu-id="a59fb-124">Szűrők jellegűek.</span><span class="sxs-lookup"><span data-stu-id="a59fb-124">Filters are inclusive.</span></span>
> <span data-ttu-id="a59fb-125">Példa: Egy elemet tartalmazó parancsmag és funkció is megjelenik, ha a rendszer ellenőrzi az parancsmag vagy függvényt (vagy mindkettőt).</span><span class="sxs-lookup"><span data-stu-id="a59fb-125">Example: An item containing both cmdlets and functions will appear if either Cmdlet or Function (or both) are checked.</span></span>
> <span data-ttu-id="a59fb-126">Ha nem választja, az elem nem jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="a59fb-126">If neither are selected, the item will not appear.</span></span>
> <span data-ttu-id="a59fb-127">Ehhez hasonlóan az összes kategória van kiválasztva, ha csak az ezekben a kategóriákban egyikét tartalmazó elemek jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="a59fb-127">Similarly, if all categories are selected, only items containing one of those categories will appear.</span></span>
> <span data-ttu-id="a59fb-128">**Nem tartoznak sem, ezen kategóriák elemek nem jelennek meg.**</span><span class="sxs-lookup"><span data-stu-id="a59fb-128">**Items that do not belong to any of those categories will not appear.**</span></span>

## <a name="sort-by"></a><span data-ttu-id="a59fb-129">Rendezési szempont</span><span class="sxs-lookup"><span data-stu-id="a59fb-129">Sort By</span></span>

<span data-ttu-id="a59fb-130">A Rendezés legördülő lista lehetővé teszi a felhasználóknak szűrje az eredményeket:</span><span class="sxs-lookup"><span data-stu-id="a59fb-130">The Sort By drop-down allows users to sort the results by:</span></span>
- <span data-ttu-id="a59fb-131">Népszerűségét - népszerűségét letöltése száma határozza meg</span><span class="sxs-lookup"><span data-stu-id="a59fb-131">Popularity - Popularity is determined by Download Count</span></span>
- <span data-ttu-id="a59fb-132">A-Z - elem név szerint</span><span class="sxs-lookup"><span data-stu-id="a59fb-132">A-Z - Alphabetically by item name</span></span>
- <span data-ttu-id="a59fb-133">Legutóbbi - elemek jelennek meg a közzétételi dátum szerinti sorrendben</span><span class="sxs-lookup"><span data-stu-id="a59fb-133">Recent - Items appear in order of publish date</span></span>

## <a name="search-box"></a><span data-ttu-id="a59fb-134">Keresés mezőbe</span><span class="sxs-lookup"><span data-stu-id="a59fb-134">Search Box</span></span>

<span data-ttu-id="a59fb-135">A keresőmezőbe lehetővé teszi, hogy a felhasználóknak a kulcsszavak elemeket.</span><span class="sxs-lookup"><span data-stu-id="a59fb-135">The Search Box allows users to search the items on keywords.</span></span>
<span data-ttu-id="a59fb-136">További információkért lásd: [gyűjtemény keresési szintaxisának](search-syntax.md).</span><span class="sxs-lookup"><span data-stu-id="a59fb-136">For more information, see [Gallery Search Syntax](search-syntax.md).</span></span>