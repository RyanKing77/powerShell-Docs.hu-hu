---
ms.date: 06/12/2017
contributor: JKeithB
ms.topic: conceptual
keywords: gyűjtemény, a powershell, a parancsmag, a psgallery
title: psgallery_unlist_items
ms.openlocfilehash: af48f2ca889dcc101d466e40f2ecbe0cdf62c066
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="unlisting-items"></a><span data-ttu-id="8b04b-103">Elemek listázásának megszüntetése</span><span class="sxs-lookup"><span data-stu-id="8b04b-103">Unlisting items</span></span>

<span data-ttu-id="8b04b-104">**Ezért egy elem éppen eltávolítja a PowerShell-galériából lehetőség nincs felfedve?**</span><span class="sxs-lookup"><span data-stu-id="8b04b-104">**Why is removing an item from PowerShell Gallery not exposed as an option?**</span></span>

<span data-ttu-id="8b04b-105">A PowerShell-galériában nem támogatja a felhasználók saját elemek véglegesen törli.</span><span class="sxs-lookup"><span data-stu-id="8b04b-105">The PowerShell Gallery does not support users permanently deleting their items.</span></span>
<span data-ttu-id="8b04b-106">Ez lehetővé teszi, hogy mások az elemek anélkül, hogy a jövőben lehetséges oldaltörések függőségek végrehajthat.</span><span class="sxs-lookup"><span data-stu-id="8b04b-106">This enables others to take dependencies on your items without worrying about possible breaks in the future.</span></span>
<span data-ttu-id="8b04b-107">Például ha a Pester modul az Azure-moduljának függ, és az Azure rendszer eltávolítja a modult a gyűjteményből, akkor a felhasználó többé nem használja a Pester modul.</span><span class="sxs-lookup"><span data-stu-id="8b04b-107">For example, if the Pester module depends on the Azure module and the Azure module is removed from the gallery, then user can no longer uses the Pester module.</span></span>

<span data-ttu-id="8b04b-108">Helyett egy elem eltávolítása, azonban akkor is unlist, helyette.</span><span class="sxs-lookup"><span data-stu-id="8b04b-108">Instead of removing an item, however, you can unlist it instead.</span></span>

<span data-ttu-id="8b04b-109">**Mire unlisting hajtsa végre a megfelelő elemre a PowerShell-galériában?**</span><span class="sxs-lookup"><span data-stu-id="8b04b-109">**What does unlisting an item on PowerShell Gallery do?**</span></span>

<span data-ttu-id="8b04b-110">Egy elem modul vagy a PowerShell-galériában parancsfájl például unlisting eltávolítja a elemek lap. Listán nem szereplő elemek emellett nem lesz felderíthető Keresősáv használatával.</span><span class="sxs-lookup"><span data-stu-id="8b04b-110">Unlisting an item such as module or script on PowerShell Gallery will remove it from the Items tab. In addition, unlisted items will not be discoverable using the search bar.</span></span>
<span data-ttu-id="8b04b-111">Töltse le a listán nem szereplő elem csak úgy adhatja meg a pontos nevét és verzióját, az elem.</span><span class="sxs-lookup"><span data-stu-id="8b04b-111">The only way to download an unlisted item is to specify the exact name and version of the item.</span></span>
<span data-ttu-id="8b04b-112">Emiatt egy elem unlisting nem megszakítja más modulok vagy parancsfájlok, amelyek függenek.</span><span class="sxs-lookup"><span data-stu-id="8b04b-112">Because of this, the unlisting of an item will not break other modules or scripts that depend on it.</span></span>

<span data-ttu-id="8b04b-113">A cikk unlist, keresse fel az elem részleteit megjelenítő oldalra, és törlése lehetőséggel.</span><span class="sxs-lookup"><span data-stu-id="8b04b-113">To unlist your item, visit the item details page and select 'Delete Item'.</span></span> <span data-ttu-id="8b04b-114">Törölje a jelet az "Felsorolt" jelölőnégyzetből, és kattintson a Mentés gombra.</span><span class="sxs-lookup"><span data-stu-id="8b04b-114">Uncheck the 'Listed' checkbox, and click Save.</span></span>

<span data-ttu-id="8b04b-115">**Hogyan távolíthatom elemet?**</span><span class="sxs-lookup"><span data-stu-id="8b04b-115">**How can I remove an item?**</span></span>

<span data-ttu-id="8b04b-116">Ha egy olyan forgatókönyvet, ahol elem törlését szükség, lépjen kapcsolatba a PowerShell-Galériabeli rendszergazdák.</span><span class="sxs-lookup"><span data-stu-id="8b04b-116">If you experience a scenario where item deletion is necessary, contact the PowerShell Gallery Administrators.</span></span>
<span data-ttu-id="8b04b-117">Érvényes törlés forgatókönyvek a következők:</span><span class="sxs-lookup"><span data-stu-id="8b04b-117">Valid deletion scenarios are:</span></span>
- <span data-ttu-id="8b04b-118">Szerzői jogsértéssel kapcsolatos problémákat.</span><span class="sxs-lookup"><span data-stu-id="8b04b-118">Issues of copyright infringement.</span></span>
- <span data-ttu-id="8b04b-119">Az elem tartalma potenciálisan káros tartalmaz.</span><span class="sxs-lookup"><span data-stu-id="8b04b-119">Item contains potentially harmful content.</span></span>
- <span data-ttu-id="8b04b-120">Az elem tartalmaz bizalmas adatokat.</span><span class="sxs-lookup"><span data-stu-id="8b04b-120">Item contains sensitive data.</span></span>

<span data-ttu-id="8b04b-121">Küldje el a törlése elem elküldeni a kérelmet a PowerShell-Galériabeli rendszergazdák, látogasson el a cikk információs lapját, és válassza ki a forduljon a támogatási szolgálathoz.</span><span class="sxs-lookup"><span data-stu-id="8b04b-121">To submit a Delete Item Request to the PowerShell Gallery Administrators, visit your item's detail page and select Contact Support.</span></span>