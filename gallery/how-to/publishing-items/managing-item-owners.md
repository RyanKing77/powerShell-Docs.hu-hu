---
ms.date: 06/12/2017
contributor: JKeithB
ms.topic: conceptual
keywords: gyűjtemény, a powershell, a parancsmag, a psgallery
title: Elemtulajdonosok kezelése
ms.openlocfilehash: 20380972ffe365ec9a479073fdf7e7f0eb1ee34e
ms.sourcegitcommit: e9ad4d85fd7eb72fb5bc37f6ca3ae1282ae3c6d7
ms.contentlocale: hu-HU
ms.lasthandoff: 05/10/2018
---
# <a name="managing-item-owners"></a><span data-ttu-id="c28af-103">Elemtulajdonosok kezelése</span><span class="sxs-lookup"><span data-stu-id="c28af-103">Managing item owners</span></span>

<span data-ttu-id="c28af-104">A PowerShell-galériában elemének tulajdonjogát ki az elemet a katalógusban közzétett határozzák meg.</span><span class="sxs-lookup"><span data-stu-id="c28af-104">Ownership of an item in the PowerShell Gallery is defined by who published the item to the gallery.</span></span>
<span data-ttu-id="c28af-105">Egyes esetekben a metaadatok kell lennie az első elem közzétételét, ami azt jelenti, hogy a tulajdonos metaadatok kell lennie változtatható, amíg az elemet nem túl.</span><span class="sxs-lookup"><span data-stu-id="c28af-105">Sometimes this metadata needs to be managed beyond the initial item publishing, which means the owner metadata needs to be mutable while the item itself is not.</span></span>

<span data-ttu-id="c28af-106">Az összes elem tulajdonosok társak.</span><span class="sxs-lookup"><span data-stu-id="c28af-106">All item owners are peers.</span></span>
<span data-ttu-id="c28af-107">Ez azt jelenti, hogy bármely tulajdonosa közzététele egy elemet egy új verziója.</span><span class="sxs-lookup"><span data-stu-id="c28af-107">This means any item owner can publish a new version of an item.</span></span> <span data-ttu-id="c28af-108">Azt is jelenti, hogy bármely tulajdonosa távolíthatja bármely más tulajdonosa.</span><span class="sxs-lookup"><span data-stu-id="c28af-108">It also means that any item owner can remove any other item owner.</span></span>
<span data-ttu-id="c28af-109">Nincs a tulajdonosnak további hatóság, mint más tulajdonosai.</span><span class="sxs-lookup"><span data-stu-id="c28af-109">No owner has more authority than other owners.</span></span>

## <a name="setting-an-items-initial-owner"></a><span data-ttu-id="c28af-110">Egy elem kezdeti tulajdonos beállítása</span><span class="sxs-lookup"><span data-stu-id="c28af-110">Setting an Item's Initial Owner</span></span>

<span data-ttu-id="c28af-111">PowerShell-galériában egy új elemet tesznek közzé, ha a felhasználót, hogy az elem közzétett határozza meg a kezdeti tulajdonosa.</span><span class="sxs-lookup"><span data-stu-id="c28af-111">When a new item is published to PowerShell Gallery, the initial owner is defined by the user that published the item.</span></span> <span data-ttu-id="c28af-112">Ez határozza meg, amelynek API által a Publish-modul a parancsmag a kulcs lett megadva.</span><span class="sxs-lookup"><span data-stu-id="c28af-112">This is determined by whose API key was used in the Publish-Module cmdlet.</span></span>

## <a name="adding-owners"></a><span data-ttu-id="c28af-113">Tulajdonosok hozzáadása</span><span class="sxs-lookup"><span data-stu-id="c28af-113">Adding Owners</span></span>

<span data-ttu-id="c28af-114">Amint egy elem közzé lett téve a PowerShell-galériában, nem hívhat meg a legyen, egy elem tulajdonosainak további felhasználók.</span><span class="sxs-lookup"><span data-stu-id="c28af-114">Once an item has been published to the PowerShell Gallery, it's easy to invite additional users to become owners of an item.</span></span>

1. <span data-ttu-id="c28af-115">[Jelentkezzen be](https://powershellgallery.com/users/account/LogOn) a fiókkal, amely a tulajdonos elem PowerShell gyűjteményébe.</span><span class="sxs-lookup"><span data-stu-id="c28af-115">[Log on](https://powershellgallery.com/users/account/LogOn) to the PowerShell Gallery with the account that is the current owner of an item.</span></span>
2. <span data-ttu-id="c28af-116">Nyissa meg az elem lapot "Elemek" lapján, a Keresés vagy kattintson a felhasználónevére, majd [ **saját elemek kezelése**](https://www.powershellgallery.com/account/Packages).</span><span class="sxs-lookup"><span data-stu-id="c28af-116">Navigate to an item page using the 'Items' tab, searching, or clicking your username and then [**Manage My Items**](https://www.powershellgallery.com/account/Packages).</span></span>
3. <span data-ttu-id="c28af-117">Amikor egy elem tulajdonosaként jelentkezik be, tulajdonosok kezelése kapcsolat van kattintson a bal oldalon.</span><span class="sxs-lookup"><span data-stu-id="c28af-117">When logged on as an item's owner, there is a 'Manage Owners' link on the left side to click.</span></span>
4. <span data-ttu-id="c28af-118">Adja meg a felhasználónevet, a tulajdonos, és kattintson a "Hozzáadás" személy.</span><span class="sxs-lookup"><span data-stu-id="c28af-118">Enter the username of the person to add as an owner and click 'Add'.</span></span>
5. <span data-ttu-id="c28af-119">E-mailt az új társtulajdonos lesz, majd küldi a meghívással elem tulajdonosa lesz.</span><span class="sxs-lookup"><span data-stu-id="c28af-119">An email is then sent to the new co-owner, as an invitation to become an owner of an item.</span></span>
6. <span data-ttu-id="c28af-120">Amennyiben az, hogy a felhasználó a hivatkozásra kattint, egy teljes társtulajdonos, elemre, beleértve a tulajdonos más felhasználók eltávolítása teljes hozzáféréssel rendelkező.</span><span class="sxs-lookup"><span data-stu-id="c28af-120">Once that user clicks the link, they are a full co-owner with full control over an item, including the ability to remove other users as owners.</span></span>

<span data-ttu-id="c28af-121">**Megjegyzés**: az új tulajdonos megerősíti, hogy tulajdonjoga, amíg azok *sem fog* tulajdonos elem jelenik.</span><span class="sxs-lookup"><span data-stu-id="c28af-121">**NOTE**: Until the new owner confirms ownership, they *will not* be listed as an owner of an item.</span></span>
<span data-ttu-id="c28af-122">Megtekintésekor a **tulajdonosok kezelése** lapon megjelenik egy "jóváhagyásra" bejegyzés aktuális tulajdonosai.</span><span class="sxs-lookup"><span data-stu-id="c28af-122">When viewing the **Manage Owners** page, you will see a "pending approval" entry in the current owners.</span></span>
<span data-ttu-id="c28af-123">A meghívó lehet eltávolítani; ugyanúgy, mint más tulajdonosok távolítható el.</span><span class="sxs-lookup"><span data-stu-id="c28af-123">That invitation can be removed; just as other owners can be removed.</span></span>
<span data-ttu-id="c28af-124">Ez a folyamat a meghívókat megakadályozza, hogy a felhasználók pontosan más felhasználók hozzáadása az elemek tulajdonosai.</span><span class="sxs-lookup"><span data-stu-id="c28af-124">This process of invitations prevents users from falsely adding other users as owners of their items.</span></span>

<span data-ttu-id="c28af-125">Vegye figyelembe, hogy a "Szerző" metaadatok tisztán Szabadkézi szöveg; csak a "tulajdonos" szabályozza.</span><span class="sxs-lookup"><span data-stu-id="c28af-125">Note that the "Authors" metadata is purely freeform text; only "Owners" are controlled.</span></span>


## <a name="removing-owners"></a><span data-ttu-id="c28af-126">Tulajdonosok eltávolítása</span><span class="sxs-lookup"><span data-stu-id="c28af-126">Removing Owners</span></span>

<span data-ttu-id="c28af-127">Ha több tulajdonosok elemnél, és egy ki kell vonni, a folyamat egyszerű történik:</span><span class="sxs-lookup"><span data-stu-id="c28af-127">When an item has multiple owners and one needs to be removed, the process is simple:</span></span>

1. <span data-ttu-id="c28af-128">[Jelentkezzen be](https://powershellgallery.com/users/account/LogOn) PowerShell gyűjteményébe a fiókkal, amely a tulajdonos elem;</span><span class="sxs-lookup"><span data-stu-id="c28af-128">[Log on](https://powershellgallery.com/users/account/LogOn) to PowerShell Gallery with the account that is the current owner of an item;</span></span>
2. <span data-ttu-id="c28af-129">Nyissa meg az elem lapot elemek lapján, a Keresés vagy kattintson a felhasználónevére, majd [ **saját elemek kezelése**](https://www.powershellgallery.com/account/Packages).</span><span class="sxs-lookup"><span data-stu-id="c28af-129">Navigate to an item page using the Items tab, searching, or clicking your username and then [**Manage My Items**](https://www.powershellgallery.com/account/Packages).</span></span>
3. <span data-ttu-id="c28af-130">Amikor egy elem tulajdonosaként jelentkezik be, tulajdonosok kezelése kapcsolat van a bal oldalon kattintson a;</span><span class="sxs-lookup"><span data-stu-id="c28af-130">When logged on as an item's owner, there is a 'Manage Owners' link on the left side to click;</span></span>
4. <span data-ttu-id="c28af-131">Kattintson az "Eltávolítás" hivatkozásra mellett a tulajdonos távolíthatók el.</span><span class="sxs-lookup"><span data-stu-id="c28af-131">Click the 'remove' link next to the owner to be removed.</span></span>



## <a name="transferring-item-ownership"></a><span data-ttu-id="c28af-132">Elem tulajdonjogának átadása</span><span class="sxs-lookup"><span data-stu-id="c28af-132">Transferring Item Ownership</span></span>

<span data-ttu-id="c28af-133">Néha kapunk támogatási kérelmek áthelyezni a elem egy felhasználó egy másikra, de szinte mindig saját kezűleg megvalósításához.</span><span class="sxs-lookup"><span data-stu-id="c28af-133">We sometimes get support requests to transfer item ownership from one user to another, but you can almost always accomplish this yourself.</span></span>
<span data-ttu-id="c28af-134">Tulajdonjog visz át egy felhasználó egy másik egyszerűen a fenti két funkció kombinációja.</span><span class="sxs-lookup"><span data-stu-id="c28af-134">Transferring ownership from one user to another is simply a combination of the two features above.</span></span>

1. <span data-ttu-id="c28af-135">A jelenlegi tulajdonos meghívja az új felhasználó a társtulajdonos lesz, és az új felhasználó elfogadja a meghívás;</span><span class="sxs-lookup"><span data-stu-id="c28af-135">The current owner invites the new user to become a co-owner and the new user accepts the invite;</span></span>
2. <span data-ttu-id="c28af-136">Az új felhasználó távolít el a régi felhasználói a tulajdonosok.</span><span class="sxs-lookup"><span data-stu-id="c28af-136">The new user removes the old user from the list of owners.</span></span>

<span data-ttu-id="c28af-137">Ezt a kérelmet néhány űrlapok alatt érkezett, de a folyamatot a ugyanúgy működik.</span><span class="sxs-lookup"><span data-stu-id="c28af-137">This request has come in under a couple forms but the process works the same.</span></span>

- <span data-ttu-id="c28af-138">A cikk tulajdonjoga egy fejlesztőtől származó módosítása egy másikra</span><span class="sxs-lookup"><span data-stu-id="c28af-138">The item ownership is changing from one developer to another</span></span>
- <span data-ttu-id="c28af-139">A cikk véletlenül lett közzétéve, a megfelelő fiók használatával</span><span class="sxs-lookup"><span data-stu-id="c28af-139">The item was accidentally published using the wrong account</span></span>


## <a name="orphaned-items"></a><span data-ttu-id="c28af-140">Árva elemeket</span><span class="sxs-lookup"><span data-stu-id="c28af-140">Orphaned Items</span></span>

<span data-ttu-id="c28af-141">Egy utolsó forgatókönyv történt, de nem sokszor.</span><span class="sxs-lookup"><span data-stu-id="c28af-141">One last scenario has occurred, but not many times.</span></span>
<span data-ttu-id="c28af-142">Elemek váltak árvaként, és az egyetlen elem tulajdonos fiók hozzáadása az új tulajdonos nem használható.</span><span class="sxs-lookup"><span data-stu-id="c28af-142">Items have become orphans and the only item owner account cannot be used to add new owners.</span></span>
<span data-ttu-id="c28af-143">Íme néhány példa az ebben a forgatókönyvben:</span><span class="sxs-lookup"><span data-stu-id="c28af-143">Here are some examples of this scenario:</span></span>

- <span data-ttu-id="c28af-144">A tulajdonos fiókhoz rendelve egy e-mail címet, amely már nem létezik, és a felhasználó elfelejtette a jelszavát</span><span class="sxs-lookup"><span data-stu-id="c28af-144">The owner's account is associated with an email address that no longer exists and the user has forgotten their password</span></span>
- <span data-ttu-id="c28af-145">A regisztrált felhasználó kilépett a vállalattól, hozza létre a cikk és frissítése a cikk tulajdonosa nem érhető el</span><span class="sxs-lookup"><span data-stu-id="c28af-145">The registered owner has left the company that produces the item and cannot be reached to update the item ownership</span></span>
- <span data-ttu-id="c28af-146">Egy hiba, néhány olyan elemek csak hatással vannak, mert a cikk található valamilyen módon ownerless a katalógusban</span><span class="sxs-lookup"><span data-stu-id="c28af-146">Due to a bug that has only affected a handful of items, the item is somehow ownerless on the gallery</span></span>

<span data-ttu-id="c28af-147">A PowerShell-Galériabeli rendszergazdák férhetnek hozzá a tulajdonosok kezelése hivatkozásra elemek.</span><span class="sxs-lookup"><span data-stu-id="c28af-147">The PowerShell Gallery Administrators can access the 'Manage Owners' link for any item.</span></span>
<span data-ttu-id="c28af-148">Ha a kártyának egy elemet, és nem érhető el a jelenlegi tulajdonos tulajdonosi jogosultságokat, használja a "Jelentés visszaélés" hivatkozásra a gyűjteményben lévő a PowerShell-Galériabeli rendszergazdák eléréséhez.</span><span class="sxs-lookup"><span data-stu-id="c28af-148">If you are the rightful owner of a item and cannot reach the current owner to gain ownership permissions, then use the 'Report Abuse' link on the gallery to reach the PowerShell Gallery Administrators.</span></span>
<span data-ttu-id="c28af-149">Azt fogja majd végrehajtásával ellenőrizze a cikk a tulajdonjogát.</span><span class="sxs-lookup"><span data-stu-id="c28af-149">We will then follow a process to verify your ownership of the item.</span></span>
<span data-ttu-id="c28af-150">Meg kell határozni egy olyan tulajdonost, az elem el, ha rendszer használja a "Tulajdonosok kezelése" hivatkozást a cikkhez ragozott formáival és küldeni a meghívás tulajdonosa lesz.</span><span class="sxs-lookup"><span data-stu-id="c28af-150">If we determine you should be an owner of the item, we will use the 'Manage Owners' link for the item ourselves and send you the invite to become an owner.</span></span>
<span data-ttu-id="c28af-151">Műveleteket végezzük el csak ezt követően ellenőrzi, hogy egy olyan tulajdonost kell lennie, és ez a folyamat függ a körülmények között.</span><span class="sxs-lookup"><span data-stu-id="c28af-151">We will only do this after verifying that you should be an owner and the process for this varies by circumstances.</span></span>
<span data-ttu-id="c28af-152">Gyakran, az elem projekt URL-cím segítségével tudja lépjen kapcsolatba a projekt tulajdonosa szorosa is használhatunk, Twitter, e-mailek vagy más módon való kapcsolódáshoz a projekt tulajdonosa.</span><span class="sxs-lookup"><span data-stu-id="c28af-152">Often times, we will use the item's Project URL to find a way to contact the project owner, but we may also use Twitter, Email, or other means for contacting the project owner.</span></span>