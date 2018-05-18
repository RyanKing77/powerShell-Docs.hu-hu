---
ms.date: 03/27/2018
contributor: JKeithB
keywords: gyűjtemény, a powershell, a psgallery, GDPR
title: PowerShell-Galériabeli GDPR megfelelőségi
ms.openlocfilehash: dca1a82952c284980a84caafa13b2807e47e25a0
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/16/2018
---
# <a name="powershell-gallery-gdpr-compliance"></a><span data-ttu-id="f677a-103">PowerShell-Galériabeli GDPR megfelelőségi</span><span class="sxs-lookup"><span data-stu-id="f677a-103">PowerShell Gallery GDPR compliance</span></span>

## <a name="overview"></a><span data-ttu-id="f677a-104">Áttekintés</span><span class="sxs-lookup"><span data-stu-id="f677a-104">Overview</span></span>

<span data-ttu-id="f677a-105">Előfordulhat, hogy 2018, az európai adatvédelmi törvény, az általános adatok védelmi szabályozás (GDPR), akkor lép érvénybe.</span><span class="sxs-lookup"><span data-stu-id="f677a-105">In May 2018, a European privacy law, the General Data Protection Regulation (GDPR), takes effect.</span></span>
<span data-ttu-id="f677a-106">A GDPR támaszt a vállalatok, állami intézményekhez, nem nyereség és más szervezetekkel, hogy az ajánlat termékek és szolgáltatások vállalatoknál az Európai Unió, vagy ha az adatgyűjtés és -elemzés EU lakosai kötve új szabályokat.</span><span class="sxs-lookup"><span data-stu-id="f677a-106">The GDPR imposes new rules on companies, government agencies, non-profits, and other organizations that offer goods and services to people in the European Union (EU), or that collect and analyze data tied to EU residents.</span></span>
<span data-ttu-id="f677a-107">A GDPR elhelyezkedő függetlenül érvényes.</span><span class="sxs-lookup"><span data-stu-id="f677a-107">The GDPR applies no matter where you are located.</span></span>

> [!NOTE]
> <span data-ttu-id="f677a-108">Ez a cikk ismerteti a személyes adatok törlése a PowerShell-galériából lépéseit, és támogatja a GDPR a kötelezettségeit használható.</span><span class="sxs-lookup"><span data-stu-id="f677a-108">This article provides steps for how to delete personal data from the PowerShell Gallery and can be used to support your obligations under the GDPR.</span></span> <span data-ttu-id="f677a-109">Ha további általános információt GDPR van szüksége, tekintse meg a [GDPR szakasz a szolgáltatás megbízható portál](https://servicetrust.microsoft.com/ViewPage/GDPRGetStarted).</span><span class="sxs-lookup"><span data-stu-id="f677a-109">If you’re looking for general info about GDPR, see the [GDPR section of the Service Trust portal](https://servicetrust.microsoft.com/ViewPage/GDPRGetStarted).</span></span>

## <a name="personally-identifiable-data"></a><span data-ttu-id="f677a-110">Személyes azonosításra alkalmas adatok</span><span class="sxs-lookup"><span data-stu-id="f677a-110">Personally identifiable data</span></span>

<span data-ttu-id="f677a-111">A PowerShell-galériában tárolja a felhasználók, amelyek tartalmazhatnak személyes adatokat is megadható a következő információkat:</span><span class="sxs-lookup"><span data-stu-id="f677a-111">The PowerShell Gallery stores the following information that may be provided by users, which may contain personal information:</span></span>

* <span data-ttu-id="f677a-112">PowerShell-galériában fiók</span><span class="sxs-lookup"><span data-stu-id="f677a-112">PowerShell Gallery account</span></span>
* <span data-ttu-id="f677a-113">A PowerShell-galériában közzétett cikkek</span><span class="sxs-lookup"><span data-stu-id="f677a-113">Items published to the PowerShell Gallery</span></span>
* <span data-ttu-id="f677a-114">E-mailek levelezés, a PowerShell-galériában csoporttal</span><span class="sxs-lookup"><span data-stu-id="f677a-114">Email correspondence with the PowerShell Gallery team</span></span>

<span data-ttu-id="f677a-115">A legtöbb felhasználó ne hozzon létre egy PowerShell-galériában fiókot.</span><span class="sxs-lookup"><span data-stu-id="f677a-115">Most users do not create a PowerShell Gallery account.</span></span>
<span data-ttu-id="f677a-116">Egy fiók nincs szükség, kivéve, ha egy elem közzététele, vagy az "Ügyfél Owner" szolgáltatás használata a PowerShell-galériában fog.</span><span class="sxs-lookup"><span data-stu-id="f677a-116">An account is not required unless you are going to publish an item or use the "Contact Owner" feature in the PowerShell Gallery.</span></span>
<span data-ttu-id="f677a-117">Eltérő e-mail levelezés, a felhasználó által kezdeményezett a PowerShell-galériában nem tárolja a felhasználókra, akik nem hozott létre egy fiókot a személyazonosításra alkalmas adatokat.</span><span class="sxs-lookup"><span data-stu-id="f677a-117">Other than email correspondence initiated by the user, the PowerShell Gallery does not store personally identifiable data for users who have not created an account.</span></span>

<span data-ttu-id="f677a-118">Felhasználók, akik egy PowerShell-galériában-fiók létrehozása a PowerShell-galériában közzéteheti elemeket.</span><span class="sxs-lookup"><span data-stu-id="f677a-118">Users who create a PowerShell Gallery account can publish items to the PowerShell Gallery.</span></span>
<span data-ttu-id="f677a-119">Ezen elemekre kellene lennie a PowerShell-kódot, de más információkat, ideértve a személyes adatokat is tartalmazhat.</span><span class="sxs-lookup"><span data-stu-id="f677a-119">Those items are expected to be PowerShell code, but may contain other information including personal information.</span></span>
<span data-ttu-id="f677a-120">Az alábbi információ jelenik meg, hogyan férhetnek elemeinek a PowerShell-galériában közzétett.</span><span class="sxs-lookup"><span data-stu-id="f677a-120">The information below will show how you can get all the items you have published to the PowerShell Gallery.</span></span>

## <a name="dsr-export-of-powershell-gallery-data"></a><span data-ttu-id="f677a-121">PowerShell-galériában adatok DSR exportálása</span><span class="sxs-lookup"><span data-stu-id="f677a-121">DSR Export of PowerShell Gallery Data</span></span>

<span data-ttu-id="f677a-122">Az alábbi szakaszok azt ismertetik, hogyan a PowerShell-galériában támogatja tulajdonos kérelmek (DSR), azzal, hogy ismerteti a PowerShell-dokumentumtárban tárolt adatok exportálása és arról, hogyan kérhet az adatok törlése.</span><span class="sxs-lookup"><span data-stu-id="f677a-122">The following sections describe how the PowerShell Gallery supports data subject requests (DSR), by explaining how to export information stored in the PowerShell Gallery, and how to request deletion of this information.</span></span>

### <a name="email"></a><span data-ttu-id="f677a-123">E-mail</span><span class="sxs-lookup"><span data-stu-id="f677a-123">Email</span></span>

<span data-ttu-id="f677a-124">E-mailek levelezés tartalmazhatja a következő:</span><span class="sxs-lookup"><span data-stu-id="f677a-124">Email correspondence may include any of the following:</span></span>

* <span data-ttu-id="f677a-125">A PowerShell-galériában elemek, ha a kód elemző ellenőrzi bármely a PowerShell-galériában a közzétett cikk problémát észlelt a tulajdonosainak küldött e-mail</span><span class="sxs-lookup"><span data-stu-id="f677a-125">Email sent to the owners of PowerShell Gallery items if the code analysis scans detected an issue with any item they have published to the PowerShell Gallery</span></span>
* <span data-ttu-id="f677a-126">Az e-mail cím használata "a kapcsolatfelvétel" lapon a PowerShell-galériában csoporthoz bárki által küldött e-mailek (cgadmin@microsoft.com)</span><span class="sxs-lookup"><span data-stu-id="f677a-126">Email sent by anyone to the PowerShell Gallery team using the email address in the "Contact Us" page (cgadmin@microsoft.com)</span></span>
* <span data-ttu-id="f677a-127">Regisztrált felhasználók, akik a PowerShell-galériában az "Ügyfél Owner" szolgáltatás segítségével e-mail küldéséhez a tulajdonos elem a PowerShell-galériában</span><span class="sxs-lookup"><span data-stu-id="f677a-127">Registered users who use the "Contact Owner" feature in the PowerShell Gallery to send email to the owner of an item in the PowerShell Gallery</span></span>

<span data-ttu-id="f677a-128">Vagy a PowerShell-galériában által küldött e-mailek 90 napos adatmegőrzési már támogatja a lehetséges biztonsági vizsgálatok kártékony kódot észleli a PowerShell-galériában a.</span><span class="sxs-lookup"><span data-stu-id="f677a-128">Emails sent by or to the PowerShell Gallery have a retention policy of 90 days to support possible security investigations should malicious code be discovered on the PowerShell Gallery.</span></span>
<span data-ttu-id="f677a-129">E-mailek házirend 90 nap után törlődnek.</span><span class="sxs-lookup"><span data-stu-id="f677a-129">Emails are deleted by policy after 90 days.</span></span>

<span data-ttu-id="f677a-130">Másolja az összes e-mailek küldése az előző 90 napon belül, vagy az e-mail címét és a PowerShell-galériában kérheti.</span><span class="sxs-lookup"><span data-stu-id="f677a-130">You may request copies of all emails sent to or from your email address and the PowerShell Gallery within the previous 90 days.</span></span>
<span data-ttu-id="f677a-131">E-mail küldése a levelezést kérelmezéséhez cgadmin@microsoft.com, és a cím: "Az e-mailekhez, ez a fiók vonatkozó DSR kérelem".</span><span class="sxs-lookup"><span data-stu-id="f677a-131">To request this correspondence, send an email to cgadmin@microsoft.com, with the title: "DSR Request for emails relating to this account".</span></span>
<span data-ttu-id="f677a-132">Az üzenet törzsében, állapot: a kért információkról (például: küldje el az összes e-mailek küldött és fogadott ezt az e-mail címet a.) Használata esetén az e-mail címet a kérelem 90 napon belül minden e-maileket küld 7 munkanapon belül.</span><span class="sxs-lookup"><span data-stu-id="f677a-132">In the body of the message, state what information you are requesting (for example: Please send all emails sent to or received from this email address.) All emails involving your email address within 90 days of the request will be sent within 7 business days.</span></span>

### <a name="powershell-gallery-account-information"></a><span data-ttu-id="f677a-133">PowerShell-galériában fiókadatok</span><span class="sxs-lookup"><span data-stu-id="f677a-133">PowerShell Gallery Account Information</span></span>

<span data-ttu-id="f677a-134">Ha létrehozott egy PowerShell-galériában fiókot, az alábbi lépések megtételével a PowerShell-dokumentumtárban tárolt összes személyes információt találja meg:</span><span class="sxs-lookup"><span data-stu-id="f677a-134">If you have created a PowerShell Gallery account, you can find all personal information that has been stored in PowerShell Gallery by taking the following steps:</span></span>

1. <span data-ttu-id="f677a-135">Jelentkezzen be a PowerShell-galériában, majd kattintson a felhasználónevére</span><span class="sxs-lookup"><span data-stu-id="f677a-135">Sign in to the PowerShell Gallery, then click on your username</span></span>
2. <span data-ttu-id="f677a-136">A következő oldal jelenik meg a fiók lapon, amely bemutatja az e-mail cím, a PowerShell-galériában fiókhoz használt</span><span class="sxs-lookup"><span data-stu-id="f677a-136">The next page displayed is the Account page, which shows the email address used for the PowerShell Gallery account</span></span>

<span data-ttu-id="f677a-137">Ha egynél több fiók a PowerShell-galériában hozott létre, akkor ismételje meg ezeket a lépéseket az egyes fiókok számára.</span><span class="sxs-lookup"><span data-stu-id="f677a-137">If you have created more than one account in the PowerShell Gallery, you will need to repeat these steps for each account.</span></span>

### <a name="items-in-the-powershell-gallery"></a><span data-ttu-id="f677a-138">A PowerShell-galériában szereplő elemek</span><span class="sxs-lookup"><span data-stu-id="f677a-138">Items in the PowerShell Gallery</span></span>

<span data-ttu-id="f677a-139">Lehetővé teszi közzé a PowerShell-galériában exportáló elemek, azt hogy tette közzé a parancsfájl "GetPSGalleryItemsForAuthor" a PowerShell-galériában.</span><span class="sxs-lookup"><span data-stu-id="f677a-139">To facilitate exporting items published to the PowerShell Gallery, we have published the script "GetPSGalleryItemsForAuthor" to the PowerShell Gallery.</span></span>
<span data-ttu-id="f677a-140">Ez a parancsfájl egy példányát minden elem kerüljenek a PowerShell-galériában elemben tárolt Szerző információk alapján a minden verziója exportálja.</span><span class="sxs-lookup"><span data-stu-id="f677a-140">This script exports a copy of every version of every item put into the PowerShell Gallery based on the author information stored in the item.</span></span>

> [!NOTE]
> <span data-ttu-id="f677a-141">A cikk közzétételekor a szerző tárolja a cikk jegyzékfájlt.</span><span class="sxs-lookup"><span data-stu-id="f677a-141">The Author is stored in the item manifest when you publish your item.</span></span>
> <span data-ttu-id="f677a-142">Nincs nem garantálja, hogy a szerző identitása megegyezik a PowerShell-galériában használt fióknak-e.</span><span class="sxs-lookup"><span data-stu-id="f677a-142">There is no guarantee that the Author is the same identity as the account you use in the PowerShell Gallery.</span></span>
> <span data-ttu-id="f677a-143">Ha más értéket használja az Author mező, szüksége lesz a adja meg ezt az értéket, ha a parancsfájl.</span><span class="sxs-lookup"><span data-stu-id="f677a-143">If you use some other value in the Author field, you will need to supply that value when using this script.</span></span>

<span data-ttu-id="f677a-144">A parancsfájl a következő PowerShell-parancs segítségével töltheti le:</span><span class="sxs-lookup"><span data-stu-id="f677a-144">You may download the script by using the following PowerShell command:</span></span>

```powershell
Save-Script GetPSGalleryItemsForAuthor -path <local folder location> -repository psgallery
```

<span data-ttu-id="f677a-145">A parancsfájl közvetlenül, majd futtassa a következő PowerShell-parancsok futtatásával:</span><span class="sxs-lookup"><span data-stu-id="f677a-145">You can then run the script directly, by running the following PowerShell commands:</span></span>

```powershell
cd <local folder location >
.\GetPSGalleryItemsForAuthor.ps1
```

<span data-ttu-id="f677a-146">Adja meg a szerző és a rendszer egy mappát, ahová menteni elemek kéri.</span><span class="sxs-lookup"><span data-stu-id="f677a-146">You will be prompted to supply the Author and a folder on your system where you want the items to be saved.</span></span>

## <a name="deleting-personal-data-from-the-powershell-gallery"></a><span data-ttu-id="f677a-147">Személyes adatok törlése a PowerShell-galériából</span><span class="sxs-lookup"><span data-stu-id="f677a-147">Deleting Personal Data From The PowerShell Gallery</span></span>

<span data-ttu-id="f677a-148">E-mail küldése a PowerShell-galériában fiók vagy a PowerShell-galériában saját elemek törléséhez cgadmin@microsoft.com és a cím: "GDPR kérelem ezzel a fiókkal kapcsolatos elemek".</span><span class="sxs-lookup"><span data-stu-id="f677a-148">To delete your PowerShell Gallery account or any item you own in the PowerShell Gallery, send email to cgadmin@microsoft.com with the title: "GDPR Request for items relating to this account".</span></span>
<span data-ttu-id="f677a-149">Az üzenet törzsében milyen információkat szeretne törölt állapotban.</span><span class="sxs-lookup"><span data-stu-id="f677a-149">In the body of the message state what information you want deleted.</span></span> <span data-ttu-id="f677a-150">Például:</span><span class="sxs-lookup"><span data-stu-id="f677a-150">For example:</span></span>

* <span data-ttu-id="f677a-151">Törölje a cikk "elem neve" verzió x.y.z</span><span class="sxs-lookup"><span data-stu-id="f677a-151">Please delete version x.y.z of my item "item name"</span></span>
* <span data-ttu-id="f677a-152">Törölje a "name elem" elem összes verziója</span><span class="sxs-lookup"><span data-stu-id="f677a-152">Please delete all versions of my item "item name"</span></span>
* <span data-ttu-id="f677a-153">Törölje a PowerShell-galériában fiókomat</span><span class="sxs-lookup"><span data-stu-id="f677a-153">Please delete my PowerShell Gallery account</span></span>

<span data-ttu-id="f677a-154">A PowerShell-galériában rendszergazdák 7 munkanapon belül válaszol.</span><span class="sxs-lookup"><span data-stu-id="f677a-154">The PowerShell Gallery administrators will reply within 7 business days.</span></span>
<span data-ttu-id="f677a-155">A megadott elemek törlődni fognak a kérelem után 30 napon belül.</span><span class="sxs-lookup"><span data-stu-id="f677a-155">The items specified will be deleted within 30 days after the request is sent.</span></span>
