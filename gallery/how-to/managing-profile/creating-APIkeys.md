---
ms.date: 09/10/2018
contributor: JKeithB
keywords: katalógus, a powershell, a parancsmag, a psgallery
title: API-kulcsok kezelése
ms.openlocfilehash: 954eb27c25babdb8efe50c13caf5f2d287c6b3e3
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62084364"
---
# <a name="managing-api-keys"></a><span data-ttu-id="1a6be-103">API-kulcsok kezelése</span><span class="sxs-lookup"><span data-stu-id="1a6be-103">Managing API keys</span></span>

<span data-ttu-id="1a6be-104">A PowerShell-galériából támogatja a közzététel követelményeinek számos támogatásához több API-kulcsok létrehozása.</span><span class="sxs-lookup"><span data-stu-id="1a6be-104">The PowerShell Gallery supports creating multiple API keys to support a range of publishing requirements.</span></span> <span data-ttu-id="1a6be-105">API-kulcs egy vagy több csomagot is alkalmazhat, bizonyos jogokat biztosít, és lejárati dátummal rendelkezik.</span><span class="sxs-lookup"><span data-stu-id="1a6be-105">An API key can apply to one or more packages, grants specific privileges, and has an expiration date.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1a6be-106">Felhasználók számára hatókörrel rendelkező API-kulcsok bevezetése előtt a PowerShell-galériában közzétett egy "teljes hozzáférés API-kulcs" lesz.</span><span class="sxs-lookup"><span data-stu-id="1a6be-106">Users who published to the PowerShell Gallery prior to the introduction of scoped API keys will have a "Full access API key".</span></span> <span data-ttu-id="1a6be-107">A teljes hozzáférési kulcsok nem rendelkezik a hatókörrel rendelkező API-kulcsok beépített biztonsági fejlesztések.</span><span class="sxs-lookup"><span data-stu-id="1a6be-107">The full access keys do not have the security improvements built into scoped API keys.</span></span> <span data-ttu-id="1a6be-108">Soha nem a teljes hozzáférési kulcsok lejár, és a alkalmazni a minden felhasználó a tulajdonosuk.</span><span class="sxs-lookup"><span data-stu-id="1a6be-108">The full access keys never expires and apply to everything owned by the user.</span></span> <span data-ttu-id="1a6be-109">Ha törli ezt a kulcsot, akkor nem kell újra létrehoznia.</span><span class="sxs-lookup"><span data-stu-id="1a6be-109">If you delete this key, it cannot be recreated.</span></span>

<span data-ttu-id="1a6be-110">Az alábbi képen látható a rendelkezésre álló lehetőségeket, egy hatókörrel rendelkező API-kulcs létrehozása során.</span><span class="sxs-lookup"><span data-stu-id="1a6be-110">The following image shows the options available when creating a scoped API key.</span></span>

![API-kulcsok létrehozása](../../Images/PSGallery_KeyScoped.png)

<span data-ttu-id="1a6be-112">Ebben a példában létrehoztunk egy API-kulcs nevű **AzureRMDataFactory**.</span><span class="sxs-lookup"><span data-stu-id="1a6be-112">In this example, we created an API key named **AzureRMDataFactory**.</span></span> <span data-ttu-id="1a6be-113">Ezt a kulcsértéket olyan nevekkel, amelyek "AzureRM.DataFactory" előtaggal kell kezdődnie, és 365 napig érvényes a csomagok leküldéses használható.</span><span class="sxs-lookup"><span data-stu-id="1a6be-113">This key value can be used to push packages with names that begin with 'AzureRM.DataFactory' and is valid for 365 days.</span></span> <span data-ttu-id="1a6be-114">Ez akkor jellemzően olyan helyzetben, amikor a az ugyanazon szervezeten belüli különböző csapatok dolgoznak a különböző csomagok.</span><span class="sxs-lookup"><span data-stu-id="1a6be-114">This is a typical scenario when different teams within the same organization work on different packages.</span></span> <span data-ttu-id="1a6be-115">A csapat tagjai egy kulcsot, amely engedélyezi őket az adott csomag működnek a jogosultságokkal rendelkezik.</span><span class="sxs-lookup"><span data-stu-id="1a6be-115">The members of the team have a key that grants them privileges for the specific package they work on.</span></span>
<span data-ttu-id="1a6be-116">A lejárati értéke megakadályozza, hogy az elavult vagy elfelejtett kulcsok használatát.</span><span class="sxs-lookup"><span data-stu-id="1a6be-116">The expiration value prevents the use of stale or forgotten keys.</span></span>

## <a name="using-glob-patterns"></a><span data-ttu-id="1a6be-117">Helyettesítése mintázatok használatával</span><span class="sxs-lookup"><span data-stu-id="1a6be-117">Using glob patterns</span></span>

<span data-ttu-id="1a6be-118">Ha a több csomagokat dolgozik, helyettesítés mintákat használhat a több csomag megfelelő csoportként.</span><span class="sxs-lookup"><span data-stu-id="1a6be-118">If you work on multiple packages, you can use globbing patterns to match multiple packages as a group.</span></span> <span data-ttu-id="1a6be-119">API-engedélyek vonatkoznak a helyettesítése mintának megfelelő minden új csomagokat.</span><span class="sxs-lookup"><span data-stu-id="1a6be-119">API key permissions apply to all new packages matching the glob pattern.</span></span> <span data-ttu-id="1a6be-120">Például az előző példában egy **helyettesítése minta** "AzureRM.DataFactory\*" értékét.</span><span class="sxs-lookup"><span data-stu-id="1a6be-120">For example, the previous example uses a **Glob Pattern** value of 'AzureRM.DataFactory\*'.</span></span> <span data-ttu-id="1a6be-121">Ezt a kulcsot használva, mert a csomag megfelel a helyettesítése mintának AzureRm.DataFactoryV2.Netcore nevű csomag küldhet.</span><span class="sxs-lookup"><span data-stu-id="1a6be-121">You can push a package named 'AzureRm.DataFactoryV2.Netcore' using this key since the package matches the glob pattern.</span></span>

## <a name="create-api-keys-securely"></a><span data-ttu-id="1a6be-122">Biztonságos API-kulcsok létrehozása</span><span class="sxs-lookup"><span data-stu-id="1a6be-122">Create API keys securely</span></span>

<span data-ttu-id="1a6be-123">A biztonság érdekében egy újonnan létrehozott kulcs értékét a képernyő nem jelenik meg, és csak akkor érhető el a Másolás gombra kattintva, ahogy az alábbi.</span><span class="sxs-lookup"><span data-stu-id="1a6be-123">For security, a newly created key value is never shown on the screen and is only available with the Copy button, as shown below.</span></span>

![Új API-kulcs értéke beszerzése](../../Images/PSGallery_CopyCreatedKey.png)

> [!IMPORTANT]
> <span data-ttu-id="1a6be-125">Után azonnal létrehozása vagy frissítése, azt csak az API-kulcs értéke lehet másolni.</span><span class="sxs-lookup"><span data-stu-id="1a6be-125">You can only copy the API key value immediately after creating or refreshing it.</span></span> <span data-ttu-id="1a6be-126">Nem jelenik meg, és nem lesz elérhető újra után az oldal frissítésekor.</span><span class="sxs-lookup"><span data-stu-id="1a6be-126">It will not be displayed, and will not be accessible again after the page is refreshed.</span></span> <span data-ttu-id="1a6be-127">Ha elveszíti a kulcs értékét, Regenerate használja, és az után azt újra létrehozzák azok másolására.</span><span class="sxs-lookup"><span data-stu-id="1a6be-127">If you lose the key value, you must use Regenerate, and copy the key after it is regenerated.</span></span>

## <a name="key-permissions-and-expiration"></a><span data-ttu-id="1a6be-128">Beállításkulcs-engedélyeit és a lejárata</span><span class="sxs-lookup"><span data-stu-id="1a6be-128">Key permissions and expiration</span></span>

<span data-ttu-id="1a6be-129">Hatókörrel rendelkező API-kulcsok rendelhet hozzá a következő engedélyek:</span><span class="sxs-lookup"><span data-stu-id="1a6be-129">Scoped API keys can assign any of the following permissions:</span></span>

- <span data-ttu-id="1a6be-130">Küldje le az új csomagok</span><span class="sxs-lookup"><span data-stu-id="1a6be-130">Push new packages</span></span>
- <span data-ttu-id="1a6be-131">Új leküldéses vagy -csomagok frissítése</span><span class="sxs-lookup"><span data-stu-id="1a6be-131">Push new or update packages</span></span>
- <span data-ttu-id="1a6be-132">Csomagok unlist</span><span class="sxs-lookup"><span data-stu-id="1a6be-132">Unlist packages</span></span>

<span data-ttu-id="1a6be-133">Minden új kulcsot egy lejárati rendelkezik.</span><span class="sxs-lookup"><span data-stu-id="1a6be-133">Every new key has an expiration.</span></span> <span data-ttu-id="1a6be-134">A lejárati értéke napokban mérjük.</span><span class="sxs-lookup"><span data-stu-id="1a6be-134">The expiration value is measured in days.</span></span> <span data-ttu-id="1a6be-135">A lejárati lehetséges értékei a következők:</span><span class="sxs-lookup"><span data-stu-id="1a6be-135">The possible values for expiration are:</span></span>

- <span data-ttu-id="1a6be-136">1 nap</span><span class="sxs-lookup"><span data-stu-id="1a6be-136">1 day</span></span>
- <span data-ttu-id="1a6be-137">90 nap</span><span class="sxs-lookup"><span data-stu-id="1a6be-137">90 days</span></span>
- <span data-ttu-id="1a6be-138">180 nap</span><span class="sxs-lookup"><span data-stu-id="1a6be-138">180 days</span></span>
- <span data-ttu-id="1a6be-139">270 naponta</span><span class="sxs-lookup"><span data-stu-id="1a6be-139">270 days</span></span>
- <span data-ttu-id="1a6be-140">365 nap (alapértelmezett)</span><span class="sxs-lookup"><span data-stu-id="1a6be-140">365 days (default)</span></span>

<span data-ttu-id="1a6be-141">Ezek a beállítások nem lehet módosítani, a kulcs létrehozása után.</span><span class="sxs-lookup"><span data-stu-id="1a6be-141">These settings cannot be changed once the key is created.</span></span> <span data-ttu-id="1a6be-142">Nem hozhat létre egy új kulcsot, soha nem jár le.</span><span class="sxs-lookup"><span data-stu-id="1a6be-142">You cannot create a new key that never expires.</span></span>

## <a name="editing-and-deleting-existing-api-keys"></a><span data-ttu-id="1a6be-143">Szerkesztés és törlés meglévő API-kulcsok</span><span class="sxs-lookup"><span data-stu-id="1a6be-143">Editing and deleting existing API keys</span></span>

<span data-ttu-id="1a6be-144">Módosíthatja a meglévő kulcs bizonyos beállítások.</span><span class="sxs-lookup"><span data-stu-id="1a6be-144">You can change some settings of an existing key.</span></span> <span data-ttu-id="1a6be-145">Fent említetteknek nem módosítja a meglévő API-kulcsot a biztonsági hatókörhöz vagy módosítsa a lejárati.</span><span class="sxs-lookup"><span data-stu-id="1a6be-145">As previously noted, you cannot modify the security scope for an existing API key or change the expiration.</span></span> <span data-ttu-id="1a6be-146">A módosítható beállítások az alábbi képernyőfelvételen látható:</span><span class="sxs-lookup"><span data-stu-id="1a6be-146">The changeable options are shown in the following screenshot:</span></span>

![Új API-kulcs értéke beszerzése](../../Images/PSGallery_EditAPIKey.png)

<span data-ttu-id="1a6be-148">A csomagok szabályozza a kulcs módosításához válassza ki az egyes csomagokat a listából, vagy módosítsa a helyettesítése minta.</span><span class="sxs-lookup"><span data-stu-id="1a6be-148">To change the packages controlled by a key, you can choose individual packages from the list or change the glob pattern.</span></span>

<span data-ttu-id="1a6be-149">Kattintson a **újragenerálása** létrehoz egy új kulcs értéket.</span><span class="sxs-lookup"><span data-stu-id="1a6be-149">Clicking **Regenerate** creates a new key value.</span></span> <span data-ttu-id="1a6be-150">Ugyanúgy, mint ha kezdetben hozta létre a kulcsot, akkor meg kell **másolási** közvetlenül a frissítés után a kulcs értékét.</span><span class="sxs-lookup"><span data-stu-id="1a6be-150">Just like when you initially created the key, you must **Copy** the key value immediately after updating it.</span></span> <span data-ttu-id="1a6be-151">A **másolási** lehetőség nem érhető el, ha elhagyja az oldalt.</span><span class="sxs-lookup"><span data-stu-id="1a6be-151">The **Copy** option is not available once you leave this page.</span></span>

<span data-ttu-id="1a6be-152">Kattintson a **törlése** egy megerősítő üzenetet jelenít meg.</span><span class="sxs-lookup"><span data-stu-id="1a6be-152">Clicking **Delete** displays a confirmation message.</span></span> <span data-ttu-id="1a6be-153">A törölt egy kulcs használhatatlan lesz.</span><span class="sxs-lookup"><span data-stu-id="1a6be-153">Once a key is deleted, it will be unusable.</span></span>

## <a name="key-expiration"></a><span data-ttu-id="1a6be-154">Kulcsának lejárati dátuma</span><span class="sxs-lookup"><span data-stu-id="1a6be-154">Key expiration</span></span>

<span data-ttu-id="1a6be-155">A lejárat előtt 10 nappal a PowerShell-galériából figyelmeztető e-mailt küld a fióktulajdonos az API-kulcs.</span><span class="sxs-lookup"><span data-stu-id="1a6be-155">Ten days before the expiration, the PowerShell Gallery sends a warning email the account holder of the API key.</span></span> <span data-ttu-id="1a6be-156">Követően a kulcs nem használható.</span><span class="sxs-lookup"><span data-stu-id="1a6be-156">After expiration, the key is unusable.</span></span> <span data-ttu-id="1a6be-157">Az API kulcskezelés oldaláról, mely kulcsok már nem érvényesek tetején figyelmeztető üzenet jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="1a6be-157">A warning message is displayed at the top of the API key management page showing which keys are no longer valid.</span></span> <span data-ttu-id="1a6be-158">Létrehozhat egy új kulcs értékét.</span><span class="sxs-lookup"><span data-stu-id="1a6be-158">You can generate a new key value.</span></span>
