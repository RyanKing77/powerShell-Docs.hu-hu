---
ms.date: 06/12/2017
contributor: JKeithB
keywords: katalógus, a powershell, a parancsmag, a psgallery
title: Csomagok listázásának megszüntetése
ms.openlocfilehash: fb66fd23dae1d4640056a764c31426f61f56d910
ms.sourcegitcommit: 98b7cfd8ad5718efa8e320526ca76c3cc4141d78
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/25/2018
ms.locfileid: "50004095"
---
# <a name="unlisting-packages"></a><span data-ttu-id="79228-103">Unlisting csomagok</span><span class="sxs-lookup"><span data-stu-id="79228-103">Unlisting Packages</span></span>

<span data-ttu-id="79228-104">**Miért éppen eltávolítja egy csomagot a beállítás nem elérhető PowerShell-galériából?**</span><span class="sxs-lookup"><span data-stu-id="79228-104">**Why is removing a package from PowerShell Gallery not exposed as an option?**</span></span>

<span data-ttu-id="79228-105">A PowerShell-galériában nem támogatja a felhasználók végleges törlése a csomagokat.</span><span class="sxs-lookup"><span data-stu-id="79228-105">The PowerShell Gallery does not support users permanently deleting their packages.</span></span>
<span data-ttu-id="79228-106">Ez lehetővé teszi mások a csomagok a jövőben nem kell bajlódnunk lehetséges oldaltörések függőségek kibontakozni.</span><span class="sxs-lookup"><span data-stu-id="79228-106">This enables others to take dependencies on your packages without worrying about possible breaks in the future.</span></span>
<span data-ttu-id="79228-107">Például ha az Azure-modul függ, a Pester modul, és az Azure-modul el lesz távolítva a katalógusban, majd a felhasználó többé nem használja a Pester modul.</span><span class="sxs-lookup"><span data-stu-id="79228-107">For example, if the Pester module depends on the Azure module and the Azure module is removed from the gallery, then user can no longer uses the Pester module.</span></span>

<span data-ttu-id="79228-108">Ahelyett, hogy eltávolítaná egy csomagot, azonban akkor is unlist, helyette.</span><span class="sxs-lookup"><span data-stu-id="79228-108">Instead of removing an package, however, you can unlist it instead.</span></span>

<span data-ttu-id="79228-109">**Mire listázásának megszüntetése, tegye a PowerShell-galériából csomag?**</span><span class="sxs-lookup"><span data-stu-id="79228-109">**What does unlisting a package on PowerShell Gallery do?**</span></span>

<span data-ttu-id="79228-110">Például modul vagy a PowerShell-galériából a parancsfájl egy csomag listázásának megszüntetése eltávolítja azt a csomagok lapot. Ezenkívül fel nem sorolt csomagok nem észlelhető a Keresősáv használatával.</span><span class="sxs-lookup"><span data-stu-id="79228-110">Unlisting a package such as module or script on PowerShell Gallery will remove it from the Packages tab. In addition, unlisted packages will not be discoverable using the search bar.</span></span>
<span data-ttu-id="79228-111">Egy listán nem szereplő csomag csak úgy, hogy adja meg a pontos nevét és a csomag verzióját.</span><span class="sxs-lookup"><span data-stu-id="79228-111">The only way to download an unlisted package is to specify the exact name and version of the package.</span></span>
<span data-ttu-id="79228-112">Emiatt egy csomag listázásának megszüntetése nem megszakítja a más modulok vagy parancsfájlok, amelyek függnek tőle.</span><span class="sxs-lookup"><span data-stu-id="79228-112">Because of this, the unlisting of an package will not break other modules or scripts that depend on it.</span></span>

<span data-ttu-id="79228-113">A csomag unlist keresse fel a csomag Részletek lap, és válassza ki a modul törlése.</span><span class="sxs-lookup"><span data-stu-id="79228-113">To unlist your package, visit the package details page and select 'Delete Module'.</span></span> <span data-ttu-id="79228-114">Törölje a jelet az "Szerepel a listában" jelölőnégyzetből, és kattintson a Mentés gombra.</span><span class="sxs-lookup"><span data-stu-id="79228-114">Uncheck the 'Listed' checkbox, and click Save.</span></span>

<span data-ttu-id="79228-115">**Hogyan távolíthatok el egy csomagot?**</span><span class="sxs-lookup"><span data-stu-id="79228-115">**How can I remove an package?**</span></span>

<span data-ttu-id="79228-116">Ha egy olyan forgatókönyvet, ahol a csomag törlése szükség, lépjen kapcsolatba a PowerShell-galéria rendszergazdák.</span><span class="sxs-lookup"><span data-stu-id="79228-116">If you experience a scenario where package deletion is necessary, contact the PowerShell Gallery Administrators.</span></span>
<span data-ttu-id="79228-117">Érvényes törlés forgatókönyvek a következők:</span><span class="sxs-lookup"><span data-stu-id="79228-117">Valid deletion scenarios are:</span></span>
- <span data-ttu-id="79228-118">A szerzői jogsértés problémákat.</span><span class="sxs-lookup"><span data-stu-id="79228-118">Issues of copyright infringement.</span></span>
- <span data-ttu-id="79228-119">A csomag tartalma potenciálisan káros.</span><span class="sxs-lookup"><span data-stu-id="79228-119">Package contains potentially harmful content.</span></span>
- <span data-ttu-id="79228-120">A csomagban bizalmas adatokat.</span><span class="sxs-lookup"><span data-stu-id="79228-120">Package contains sensitive data.</span></span>

<span data-ttu-id="79228-121">Egy törlése csomag kérelmet a PowerShell-galéria rendszergazdáknak küldéséhez látogasson el a csomag részletei lapon, és válassza ki a forduljon az ügyfélszolgálathoz.</span><span class="sxs-lookup"><span data-stu-id="79228-121">To submit a Delete Package Request to the PowerShell Gallery Administrators, visit your package's detail page and select Contact Support.</span></span>
