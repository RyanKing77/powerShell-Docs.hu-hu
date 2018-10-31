---
ms.date: 06/12/2017
contributor: JKeithB
keywords: katalógus, a powershell, a parancsmag, a psgallery
title: Csomag tulajdonosainak kezelése
ms.openlocfilehash: 5cf26a7195ac446177cbb7f3a055e8e0a78569cc
ms.sourcegitcommit: 98b7cfd8ad5718efa8e320526ca76c3cc4141d78
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/25/2018
ms.locfileid: "50004123"
---
# <a name="managing-package-owners"></a><span data-ttu-id="c1e7f-103">Csomag tulajdonosainak kezelése</span><span class="sxs-lookup"><span data-stu-id="c1e7f-103">Managing package owners</span></span>

<span data-ttu-id="c1e7f-104">A PowerShell-galériából a csomag tulajdonjogát ki a csomagot a katalógusban közzétett határozzák meg.</span><span class="sxs-lookup"><span data-stu-id="c1e7f-104">Ownership of a package in the PowerShell Gallery is defined by who published the package to the gallery.</span></span>
<span data-ttu-id="c1e7f-105">Egyes esetekben a metaadatok kell kezelni a kezdeti csomag közzétételét, ami azt jelenti, hogy a tulajdonos metaadatok kell lennie módosítható, bár a csomagba nem túl.</span><span class="sxs-lookup"><span data-stu-id="c1e7f-105">Sometimes this metadata needs to be managed beyond the initial package publishing, which means the owner metadata needs to be mutable while the package itself is not.</span></span>

<span data-ttu-id="c1e7f-106">Minden csomag olyan társakhoz.</span><span class="sxs-lookup"><span data-stu-id="c1e7f-106">All package owners are peers.</span></span>
<span data-ttu-id="c1e7f-107">Ez azt jelenti, hogy minden olyan csomag tulajdonosával teheti közzé a csomag új verziójának.</span><span class="sxs-lookup"><span data-stu-id="c1e7f-107">This means any package owner can publish a new version of an package.</span></span> <span data-ttu-id="c1e7f-108">Azt is jelenti, hogy minden olyan csomag tulajdonosa távolíthatja el bármilyen egyéb csomag tulajdonosával.</span><span class="sxs-lookup"><span data-stu-id="c1e7f-108">It also means that any package owner can remove any other package owner.</span></span>
<span data-ttu-id="c1e7f-109">Nincs tulajdonosa, mint a más tulajdonosok több szolgáltató nem.</span><span class="sxs-lookup"><span data-stu-id="c1e7f-109">No owner has more authority than other owners.</span></span>

## <a name="setting-a-packages-initial-owner"></a><span data-ttu-id="c1e7f-110">A csomag kezdeti tulajdonos beállítása</span><span class="sxs-lookup"><span data-stu-id="c1e7f-110">Setting a Package's Initial Owner</span></span>

<span data-ttu-id="c1e7f-111">Ha a PowerShell-galériában közzétett új csomagot, a felhasználót, hogy a csomag közzétett határozza meg a kezdeti tulajdonos.</span><span class="sxs-lookup"><span data-stu-id="c1e7f-111">When a new package is published to PowerShell Gallery, the initial owner is defined by the user that published the package.</span></span> <span data-ttu-id="c1e7f-112">Ez határozza meg, amelynek API key használták a Publish-Module parancsmaggal.</span><span class="sxs-lookup"><span data-stu-id="c1e7f-112">This is determined by whose API key was used in the Publish-Module cmdlet.</span></span>

## <a name="adding-owners"></a><span data-ttu-id="c1e7f-113">Tulajdonosok hozzáadása</span><span class="sxs-lookup"><span data-stu-id="c1e7f-113">Adding Owners</span></span>

<span data-ttu-id="c1e7f-114">Ha egy csomag közzé lett téve a PowerShell-galériából, könnyebbé vált a csomag tulajdonosai lesznek további felhasználókat meghívni.</span><span class="sxs-lookup"><span data-stu-id="c1e7f-114">Once a package has been published to the PowerShell Gallery, it's easy to invite additional users to become owners of a package.</span></span>

1. <span data-ttu-id="c1e7f-115">[Jelentkezzen be](https://powershellgallery.com/users/account/LogOn) azzal a fiókkal, a tulajdonos csomagot, a PowerShell-galériában.</span><span class="sxs-lookup"><span data-stu-id="c1e7f-115">[Log on](https://powershellgallery.com/users/account/LogOn) to the PowerShell Gallery with the account that is the current owner of a package.</span></span>
2. <span data-ttu-id="c1e7f-116">Keresse meg a csomag lapon használja az "Items" lapon, a Keresés vagy kattintson a felhasználónevére, majd [ **My-csomagok kezelése**](https://www.powershellgallery.com/account/Packages).</span><span class="sxs-lookup"><span data-stu-id="c1e7f-116">Navigate to a package page using the 'Items' tab, searching, or clicking your username and then [**Manage My Packages**](https://www.powershellgallery.com/account/Packages).</span></span>
3. <span data-ttu-id="c1e7f-117">Amikor bejelentkezett egy csomagot tulajdonosként, tulajdonosok kezelése kapcsolat van, kattintson a bal oldalon.</span><span class="sxs-lookup"><span data-stu-id="c1e7f-117">When logged on as an package's owner, there is a 'Manage Owners' link on the left side to click.</span></span>
4. <span data-ttu-id="c1e7f-118">Adja meg a tulajdonosként hozzáadni, és kattintson a "Hozzáadás" személy felhasználóneve.</span><span class="sxs-lookup"><span data-stu-id="c1e7f-118">Enter the username of the person to add as an owner and click 'Add'.</span></span>
5. <span data-ttu-id="c1e7f-119">E-mailt az új társtulajdonos, majd küldeni a meghívással csomag tulajdonosává válik.</span><span class="sxs-lookup"><span data-stu-id="c1e7f-119">An email is then sent to the new co-owner, as an invitation to become an owner of a package.</span></span>
6. <span data-ttu-id="c1e7f-120">Miután, hogy a felhasználó a hivatkozásra kattint, azok teljes társtulajdonos, teljes körűen felügyelve egy csomagot, beleértve a más felhasználók tulajdonosként való eltávolítása.</span><span class="sxs-lookup"><span data-stu-id="c1e7f-120">Once that user clicks the link, they are a full co-owner with full control over a package, including the ability to remove other users as owners.</span></span>

<span data-ttu-id="c1e7f-121">**Megjegyzés:**: mindaddig, amíg az új tulajdonos megerősíti, hogy tulajdonjoga, azok *nem fog* csomag tulajdonosának helyrendszerként legyen felsorolva.</span><span class="sxs-lookup"><span data-stu-id="c1e7f-121">**NOTE**: Until the new owner confirms ownership, they *will not* be listed as an owner of a package.</span></span>
<span data-ttu-id="c1e7f-122">Megtekintésekor a **tulajdonosainak kezelése** oldalon, a jelenlegi tulajdonos a "jóváhagyásra" bejegyzést fog látni.</span><span class="sxs-lookup"><span data-stu-id="c1e7f-122">When viewing the **Manage Owners** page, you will see a "pending approval" entry in the current owners.</span></span>
<span data-ttu-id="c1e7f-123">A meghívó távolíthatja el; ugyanúgy, mint a más tulajdonosok távolíthatja el.</span><span class="sxs-lookup"><span data-stu-id="c1e7f-123">That invitation can be removed; just as other owners can be removed.</span></span>
<span data-ttu-id="c1e7f-124">Ez a folyamat a Meghívók meggátolja, hogy a felhasználókat a tévesen tulajdonosaihoz csomagjaikat, a más felhasználók hozzáadásakor.</span><span class="sxs-lookup"><span data-stu-id="c1e7f-124">This process of invitations prevents users from falsely adding other users as owners of their packages.</span></span>

<span data-ttu-id="c1e7f-125">Vegye figyelembe, hogy a "Szerző" metaadatok tisztán szabadkézi szöveges; csak a "tulajdonos" szabályozza.</span><span class="sxs-lookup"><span data-stu-id="c1e7f-125">Note that the "Authors" metadata is purely freeform text; only "Owners" are controlled.</span></span>


## <a name="removing-owners"></a><span data-ttu-id="c1e7f-126">Tulajdonos eltávolítása</span><span class="sxs-lookup"><span data-stu-id="c1e7f-126">Removing Owners</span></span>

<span data-ttu-id="c1e7f-127">Ha egy csomag több tulajdonosok rendelkezik, és egyet ki kell vonni, a folyamat egyszerű:</span><span class="sxs-lookup"><span data-stu-id="c1e7f-127">When a package has multiple owners and one needs to be removed, the process is simple:</span></span>

1. <span data-ttu-id="c1e7f-128">[Jelentkezzen be](https://powershellgallery.com/users/account/LogOn) azzal a fiókkal, a csomag; tulajdonos PowerShell-galériában</span><span class="sxs-lookup"><span data-stu-id="c1e7f-128">[Log on](https://powershellgallery.com/users/account/LogOn) to PowerShell Gallery with the account that is the current owner of a package;</span></span>
2. <span data-ttu-id="c1e7f-129">Nyissa meg a csomag lapot csomagok lapján, a keresés, vagy kattintson a felhasználónevére, majd [ **My-csomagok kezelése**](https://www.powershellgallery.com/account/Packages).</span><span class="sxs-lookup"><span data-stu-id="c1e7f-129">Navigate to a package page using the Packages tab, searching, or clicking your username and then [**Manage My Packages**](https://www.powershellgallery.com/account/Packages).</span></span>
3. <span data-ttu-id="c1e7f-130">Ha be van jelentkezve, a csomag tulajdonosával, tulajdonosok kezelése kapcsolat van; kattintson a bal oldalon</span><span class="sxs-lookup"><span data-stu-id="c1e7f-130">When logged on as a package's owner, there is a 'Manage Owners' link on the left side to click;</span></span>
4. <span data-ttu-id="c1e7f-131">Kattintson a "remove" hivatkozást, el kell távolítani a tulajdonos mellett.</span><span class="sxs-lookup"><span data-stu-id="c1e7f-131">Click the 'remove' link next to the owner to be removed.</span></span>



## <a name="transferring-package-ownership"></a><span data-ttu-id="c1e7f-132">Csomag átruházása</span><span class="sxs-lookup"><span data-stu-id="c1e7f-132">Transferring Package Ownership</span></span>

<span data-ttu-id="c1e7f-133">Támogatási kérések tulajdonjogának csomag egy felhasználó egy másikra néha kapunk, de szinte mindig elvégezheti ezt Ön.</span><span class="sxs-lookup"><span data-stu-id="c1e7f-133">We sometimes get support requests to transfer package ownership from one user to another, but you can almost always accomplish this yourself.</span></span>
<span data-ttu-id="c1e7f-134">Egyszerűen csak a fenti két szolgáltatás kombinációja tulajdonjog visz át egy felhasználó egy másik.</span><span class="sxs-lookup"><span data-stu-id="c1e7f-134">Transferring ownership from one user to another is simply a combination of the two features above.</span></span>

1. <span data-ttu-id="c1e7f-135">A jelenlegi tulajdonos meghívót küld a társtulajdonos válik az új felhasználót, és az új felhasználó elfogadja a meghívást;</span><span class="sxs-lookup"><span data-stu-id="c1e7f-135">The current owner invites the new user to become a co-owner and the new user accepts the invite;</span></span>
2. <span data-ttu-id="c1e7f-136">Az új felhasználót a régi felhasználói távolít el, a tulajdonosok listája.</span><span class="sxs-lookup"><span data-stu-id="c1e7f-136">The new user removes the old user from the list of owners.</span></span>

<span data-ttu-id="c1e7f-137">Ezt a kérést néhány űrlapok alatt érkezett, de a folyamat ugyanúgy működik.</span><span class="sxs-lookup"><span data-stu-id="c1e7f-137">This request has come in under a couple forms but the process works the same.</span></span>

- <span data-ttu-id="c1e7f-138">A csomag tulajdonjogát módosul az egyik fejlesztő egy másikba</span><span class="sxs-lookup"><span data-stu-id="c1e7f-138">The package ownership is changing from one developer to another</span></span>
- <span data-ttu-id="c1e7f-139">A csomag véletlenül közzé lett téve a megfelelő fiók használatával</span><span class="sxs-lookup"><span data-stu-id="c1e7f-139">The package was accidentally published using the wrong account</span></span>


## <a name="orphaned-packages"></a><span data-ttu-id="c1e7f-140">Árva csomagok</span><span class="sxs-lookup"><span data-stu-id="c1e7f-140">Orphaned Packages</span></span>

<span data-ttu-id="c1e7f-141">Egy legutóbbi forgatókönyv történt, de nem több alkalommal.</span><span class="sxs-lookup"><span data-stu-id="c1e7f-141">One last scenario has occurred, but not many times.</span></span>
<span data-ttu-id="c1e7f-142">Csomagok sp_createorphan váltak, és az egyetlen csomag tulajdonosi fiók nem használható új tulajdonosok hozzáadása.</span><span class="sxs-lookup"><span data-stu-id="c1e7f-142">Packages have become orphans and the only package owner account cannot be used to add new owners.</span></span>
<span data-ttu-id="c1e7f-143">Íme néhány példa az ebben a forgatókönyvben:</span><span class="sxs-lookup"><span data-stu-id="c1e7f-143">Here are some examples of this scenario:</span></span>

- <span data-ttu-id="c1e7f-144">A tulajdonos fiókja már nem létezik olyan e-mail-címmel társított, és a felhasználó elfelejtette a jelszavát</span><span class="sxs-lookup"><span data-stu-id="c1e7f-144">The owner's account is associated with an email address that no longer exists and the user has forgotten their password</span></span>
- <span data-ttu-id="c1e7f-145">A regisztrált felhasználó elhagyta a vállalatot, amely a csomag nem érhető el a csomag tulajdonjogát frissítése</span><span class="sxs-lookup"><span data-stu-id="c1e7f-145">The registered owner has left the company that produces the package and cannot be reached to update the package ownership</span></span>
- <span data-ttu-id="c1e7f-146">Csak hatással vannak a csomagok milliós egy hiba miatt a csomag nincs valamilyen módon ownerless a katalógusban</span><span class="sxs-lookup"><span data-stu-id="c1e7f-146">Due to a bug that has only affected a handful of packages, the package is somehow ownerless on the gallery</span></span>

<span data-ttu-id="c1e7f-147">A PowerShell-galéria rendszergazdák férhetnek hozzá a tulajdonosok kezelése hivatkozásra bármelyik csomag.</span><span class="sxs-lookup"><span data-stu-id="c1e7f-147">The PowerShell Gallery Administrators can access the 'Manage Owners' link for any package.</span></span>
<span data-ttu-id="c1e7f-148">Ha egy csomagot a jogos tulajdonosa, és nem érhető el a jelenlegi tulajdonos a tulajdonjog jogosultságokat, majd használja a visszaélés jelentése hivatkozást a katalógusban a PowerShell-galéria rendszergazdák eléréséhez.</span><span class="sxs-lookup"><span data-stu-id="c1e7f-148">If you are the rightful owner of a package and cannot reach the current owner to gain ownership permissions, then use the 'Report Abuse' link on the gallery to reach the PowerShell Gallery Administrators.</span></span>
<span data-ttu-id="c1e7f-149">Ezután követjük egy folyamatot, hogy a csomag tulajdonosának ellenőrzését.</span><span class="sxs-lookup"><span data-stu-id="c1e7f-149">We will then follow a process to verify your ownership of the package.</span></span>
<span data-ttu-id="c1e7f-150">Ha azt állapítja meg, hogy a csomag tulajdonosának kell látnia, hogy lesz használja tulajdonosainak kezelése hivatkozást a csomag magunkat és tulajdonosa lesz a meghívót küldünk.</span><span class="sxs-lookup"><span data-stu-id="c1e7f-150">If we determine you should be an owner of the package, we will use the 'Manage Owners' link for the package ourselves and send you the invite to become an owner.</span></span>
<span data-ttu-id="c1e7f-151">Csak tesszük ez Miután ellenőrizte, hogy egy olyan tulajdonost kell, és ez a folyamat eltérő körülmények között.</span><span class="sxs-lookup"><span data-stu-id="c1e7f-151">We will only do this after verifying that you should be an owner and the process for this varies by circumstances.</span></span>
<span data-ttu-id="c1e7f-152">Gyakran, forduljon a projekt tulajdonosa megtalálni a csomag projekt URL-címet használjuk, de még a használjuk, Twitter, e-mailben vagy más módon vegye fel a kapcsolatot a projekt tulajdonosa.</span><span class="sxs-lookup"><span data-stu-id="c1e7f-152">Often times, we will use the package's Project URL to find a way to contact the project owner, but we may also use Twitter, Email, or other means for contacting the project owner.</span></span>
