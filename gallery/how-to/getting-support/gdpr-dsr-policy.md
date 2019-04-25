---
ms.date: 03/27/2018
contributor: JKeithB
keywords: katalógus, a powershell, a psgallery, GDPR
title: PowerShell-galéria GDPR-megfelelőség
ms.openlocfilehash: fb1191d8a1cd12d5994e41238c384eb504d0c261
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62084232"
---
# <a name="powershell-gallery-gdpr-compliance"></a><span data-ttu-id="b862f-103">PowerShell-galéria GDPR-megfelelőség</span><span class="sxs-lookup"><span data-stu-id="b862f-103">PowerShell Gallery GDPR compliance</span></span>

## <a name="overview"></a><span data-ttu-id="b862f-104">Áttekintés</span><span class="sxs-lookup"><span data-stu-id="b862f-104">Overview</span></span>

<span data-ttu-id="b862f-105">A 2018 május az európai adatvédelmi törvény, az általános adatvédelmi rendelet (GDPR), érvénybe vett igénybe.</span><span class="sxs-lookup"><span data-stu-id="b862f-105">In May 2018, a European privacy law, the General Data Protection Regulation (GDPR), took effect.</span></span>
<span data-ttu-id="b862f-106">Az általános adatvédelmi rendelet új szabályokat a vállalatok, kormányzati szerveknek, non-profit és más szervezetek számára, hogy az ajánlat termékek és szolgáltatások, az Európai Unió (EU), vagy hogy a felhasználók adatokat gyűjthet és elemezhet kötött EU-polgárokkal kapcsolatos ír elő.</span><span class="sxs-lookup"><span data-stu-id="b862f-106">The GDPR imposes new rules on companies, government agencies, non-profits, and other organizations that offer goods and services to people in the European Union (EU), or that collect and analyze data tied to EU residents.</span></span>
<span data-ttu-id="b862f-107">Az általános adatvédelmi rendelet vonatkozik, bárhol is található.</span><span class="sxs-lookup"><span data-stu-id="b862f-107">The GDPR applies no matter where you are located.</span></span>

> [!NOTE]
> <span data-ttu-id="b862f-108">Ez a cikk ismerteti a személyes adatok törlése a PowerShell-galériából, és támogatja a GDPR szerint Ön nem használható.</span><span class="sxs-lookup"><span data-stu-id="b862f-108">This article provides steps for how to delete personal data from the PowerShell Gallery and can be used to support your obligations under the GDPR.</span></span> <span data-ttu-id="b862f-109">Ha az általános adatvédelmi rendelet kapcsolatos általános információkat keres, tekintse meg a [GDPR szakaszában a szolgáltatás Szolgáltatásmegbízhatósági portálon](https://servicetrust.microsoft.com/ViewPage/GDPRGetStarted).</span><span class="sxs-lookup"><span data-stu-id="b862f-109">If you’re looking for general info about GDPR, see the [GDPR section of the Service Trust portal](https://servicetrust.microsoft.com/ViewPage/GDPRGetStarted).</span></span>

## <a name="personally-identifiable-data"></a><span data-ttu-id="b862f-110">Személyes azonosításra alkalmas adatok</span><span class="sxs-lookup"><span data-stu-id="b862f-110">Personally identifiable data</span></span>

<span data-ttu-id="b862f-111">A PowerShell-galériából a következő adatokat, a felhasználók, amelyek személyes adatokat tartalmazhatnak biztosított tárolja:</span><span class="sxs-lookup"><span data-stu-id="b862f-111">The PowerShell Gallery stores the following information that may be provided by users, which may contain personal information:</span></span>

- <span data-ttu-id="b862f-112">PowerShell-Galériabeli fiók</span><span class="sxs-lookup"><span data-stu-id="b862f-112">PowerShell Gallery account</span></span>
- <span data-ttu-id="b862f-113">A PowerShell-galériában közzétett csomagokat</span><span class="sxs-lookup"><span data-stu-id="b862f-113">Packages published to the PowerShell Gallery</span></span>
- <span data-ttu-id="b862f-114">A PowerShell-galériából csapat váltott e-mailben</span><span class="sxs-lookup"><span data-stu-id="b862f-114">Email correspondence with the PowerShell Gallery team</span></span>

<span data-ttu-id="b862f-115">A legtöbb felhasználó ne hozzon létre egy PowerShell-Galériabeli fiók.</span><span class="sxs-lookup"><span data-stu-id="b862f-115">Most users do not create a PowerShell Gallery account.</span></span>
<span data-ttu-id="b862f-116">Egy fiók nem kötelező, kivéve, ha egy csomag közzététele, vagy az "Ügyfél Owner" szolgáltatás használata a PowerShell-galériából kívánja.</span><span class="sxs-lookup"><span data-stu-id="b862f-116">An account is not required unless you are going to publish a package or use the "Contact Owner" feature in the PowerShell Gallery.</span></span>
<span data-ttu-id="b862f-117">E-mailek levelezés, a felhasználó által kezdeményezett, nem a PowerShell-galériában nem tárolja a személyes azonosításra alkalmas adatokat a felhasználók számára, akik nem hozott létre egy fiókot.</span><span class="sxs-lookup"><span data-stu-id="b862f-117">Other than email correspondence initiated by the user, the PowerShell Gallery does not store personally identifiable data for users who have not created an account.</span></span>

<span data-ttu-id="b862f-118">Felhasználók, akik egy PowerShell-Galériabeli fiók létrehozása a PowerShell-galériából csomagok tehetnek közzé.</span><span class="sxs-lookup"><span data-stu-id="b862f-118">Users who create a PowerShell Gallery account can publish packages to the PowerShell Gallery.</span></span>
<span data-ttu-id="b862f-119">Azokat a csomagokat várhatóan PowerShell-kódot, de egyéb információkat, ideértve a személyes adatokat is tartalmazhat.</span><span class="sxs-lookup"><span data-stu-id="b862f-119">Those packages are expected to be PowerShell code, but may contain other information including personal information.</span></span>
<span data-ttu-id="b862f-120">Az alábbi információk jelennek meg, hogyan kezdheti összes csomag közzétételét a PowerShell-galériában.</span><span class="sxs-lookup"><span data-stu-id="b862f-120">The information below will show how you can get all the packages you have published to the PowerShell Gallery.</span></span>

## <a name="dsr-export-of-powershell-gallery-data"></a><span data-ttu-id="b862f-121">PowerShell-galériából adatok DSR exportálása</span><span class="sxs-lookup"><span data-stu-id="b862f-121">DSR Export of PowerShell Gallery Data</span></span>

<span data-ttu-id="b862f-122">A következő szakaszok ismertetik a PowerShell-galériából hogyan támogatja az adattulajdonosi kérelmek (DSR), a PowerShell-galériából a tárolt adatok exportálása és törlése, ez az információ kérésének elmagyarázza.</span><span class="sxs-lookup"><span data-stu-id="b862f-122">The following sections describe how the PowerShell Gallery supports data subject requests (DSR), by explaining how to export information stored in the PowerShell Gallery, and how to request deletion of this information.</span></span>

### <a name="email"></a><span data-ttu-id="b862f-123">E-mail</span><span class="sxs-lookup"><span data-stu-id="b862f-123">Email</span></span>

<span data-ttu-id="b862f-124">E-mailek levelezést tartalmazhatja a következő:</span><span class="sxs-lookup"><span data-stu-id="b862f-124">Email correspondence may include any of the following:</span></span>

- <span data-ttu-id="b862f-125">A PowerShell-galériából csomagokat, ha megvizsgálja a kód elemzés minden olyan csomag, a PowerShell-galériában közzétett hibát észlelt a tulajdonosainak küldött e-mail</span><span class="sxs-lookup"><span data-stu-id="b862f-125">Email sent to the owners of PowerShell Gallery packages if the code analysis scans detected an issue with any package they have published to the PowerShell Gallery</span></span>
- <span data-ttu-id="b862f-126">A PowerShell-galériából csapat az e-mail-cím használatával "a kapcsolatfelvétel" lapon a bárki által küldött e-mail [cgadmin@microsoft.com](mailto:cgadmin@microsoft.com)</span><span class="sxs-lookup"><span data-stu-id="b862f-126">Email sent by anyone to the PowerShell Gallery team using the email address in the "Contact Us" page [cgadmin@microsoft.com](mailto:cgadmin@microsoft.com)</span></span>
- <span data-ttu-id="b862f-127">Regisztrált felhasználó, aki a PowerShell-galériából a "Forduljon Owner" szolgáltatás segítségével a PowerShell-galériából csomag tulajdonosának e-mail küldése</span><span class="sxs-lookup"><span data-stu-id="b862f-127">Registered users who use the "Contact Owner" feature in the PowerShell Gallery to send email to the owner of a package in the PowerShell Gallery</span></span>

<span data-ttu-id="b862f-128">Által vagy a PowerShell-galériában elküldött e-mailek 90 napos adatmegőrzési már támogatja a lehetséges biztonsági vizsgálatok kártevő kódja észleli a PowerShell-galériából.</span><span class="sxs-lookup"><span data-stu-id="b862f-128">Emails sent by or to the PowerShell Gallery have a retention policy of 90 days to support possible security investigations should malicious code be discovered on the PowerShell Gallery.</span></span>
<span data-ttu-id="b862f-129">E-mailek házirend 90 nap után törlődnek.</span><span class="sxs-lookup"><span data-stu-id="b862f-129">Emails are deleted by policy after 90 days.</span></span>

<span data-ttu-id="b862f-130">Minden e-mailek küldése az előző 90 napon belül, vagy az e-mail-címét és a PowerShell-galériából példányait kérheti.</span><span class="sxs-lookup"><span data-stu-id="b862f-130">You may request copies of all emails sent to or from your email address and the PowerShell Gallery within the previous 90 days.</span></span>
<span data-ttu-id="b862f-131">Kérelem ezt a levelezését, küldjön egy e-mailek [ cgadmin@microsoft.com ](mailto:cgadmin@microsoft.com), és a cím: "DSR kérése e-mailekhez, ez a fiók vonatkozó".</span><span class="sxs-lookup"><span data-stu-id="b862f-131">To request this correspondence, send an email to [cgadmin@microsoft.com](mailto:cgadmin@microsoft.com), with the title: "DSR Request for emails relating to this account".</span></span>
<span data-ttu-id="b862f-132">Az üzenet törzsében, adja meg a kért információk (például: Kérjük, küldjön minden e-mailek küldött vagy erre a címre érkezett.) Használata esetén az e-mail-címét a kérelem számított 90 napon belül minden e-maileket küld üzleti 7 napon belül.</span><span class="sxs-lookup"><span data-stu-id="b862f-132">In the body of the message, state what information you are requesting (for example: Please send all emails sent to or received from this email address.) All emails involving your email address within 90 days of the request will be sent within 7 business days.</span></span>

### <a name="powershell-gallery-account-information"></a><span data-ttu-id="b862f-133">PowerShell-Galériabeli fiók adatait</span><span class="sxs-lookup"><span data-stu-id="b862f-133">PowerShell Gallery Account Information</span></span>

<span data-ttu-id="b862f-134">Ha létrehozott egy PowerShell-Galériabeli fiók, annak az alábbi lépések megtételével a PowerShell-katalógusban tárolt személyes adatokat:</span><span class="sxs-lookup"><span data-stu-id="b862f-134">If you have created a PowerShell Gallery account, you can find all personal information that has been stored in PowerShell Gallery by taking the following steps:</span></span>

1. <span data-ttu-id="b862f-135">Jelentkezzen be a PowerShell-galériából, majd kattintson a felhasználónevére</span><span class="sxs-lookup"><span data-stu-id="b862f-135">Sign in to the PowerShell Gallery, then click on your username</span></span>
2. <span data-ttu-id="b862f-136">A következő oldal jelenik meg a fiók oldal, amely megjeleníti a PowerShell-Galériabeli fiók használt e-mail-cím</span><span class="sxs-lookup"><span data-stu-id="b862f-136">The next page displayed is the Account page, which shows the email address used for the PowerShell Gallery account</span></span>

<span data-ttu-id="b862f-137">Ha egynél több fiók található a PowerShell-galériából létrehozott, szüksége lesz a ismételje meg ezeket a lépéseket az egyes fiókok számára.</span><span class="sxs-lookup"><span data-stu-id="b862f-137">If you have created more than one account in the PowerShell Gallery, you will need to repeat these steps for each account.</span></span>

### <a name="packages-in-the-powershell-gallery"></a><span data-ttu-id="b862f-138">A PowerShell-galériából-csomagok</span><span class="sxs-lookup"><span data-stu-id="b862f-138">Packages in the PowerShell Gallery</span></span>

<span data-ttu-id="b862f-139">Megkönnyítése érdekében a PowerShell-galériában közzétett exportáló csomagokat, Microsoft közzétette a parancsfájl "GetPSGalleryItemsForAuthor" a PowerShell-galériában.</span><span class="sxs-lookup"><span data-stu-id="b862f-139">To facilitate exporting packages published to the PowerShell Gallery, we have published the script "GetPSGalleryItemsForAuthor" to the PowerShell Gallery.</span></span>
<span data-ttu-id="b862f-140">Ez a szkript exportál egy példányát minden egyes verziója minden csomag üzembe a PowerShell-galériából, a csomag tárolt Szerző információk alapján.</span><span class="sxs-lookup"><span data-stu-id="b862f-140">This script exports a copy of every version of every package put into the PowerShell Gallery based on the author information stored in the package.</span></span>

> [!NOTE]
> <span data-ttu-id="b862f-141">A szerző, a csomag közzétételekor tárolja a csomagjegyzéket.</span><span class="sxs-lookup"><span data-stu-id="b862f-141">The Author is stored in the package manifest when you publish your package.</span></span>
> <span data-ttu-id="b862f-142">Nincs garancia arra, hogy a szerző stejnou identitou jako a PowerShell-galériából a használt fióknak-e.</span><span class="sxs-lookup"><span data-stu-id="b862f-142">There is no guarantee that the Author is the same identity as the account you use in the PowerShell Gallery.</span></span>
> <span data-ttu-id="b862f-143">Ha más értéket az Author mező használata esetén kell adnia ezt az értéket, amikor ez a szkript használatával.</span><span class="sxs-lookup"><span data-stu-id="b862f-143">If you use some other value in the Author field, you will need to supply that value when using this script.</span></span>

<span data-ttu-id="b862f-144">A szkript a következő PowerShell-parancs segítségével töltheti le:</span><span class="sxs-lookup"><span data-stu-id="b862f-144">You may download the script by using the following PowerShell command:</span></span>

```powershell
Save-Script Get-repository psgallery
```

<span data-ttu-id="b862f-145">A parancsfájl közvetlenül, majd futtassa a következő PowerShell-parancsok futtatásával:</span><span class="sxs-lookup"><span data-stu-id="b862f-145">You can then run the script directly, by running the following PowerShell commands:</span></span>

```powershell
# cd <local folder location>
.\GetPSGalleryItemsForAuthor.ps1
```

<span data-ttu-id="b862f-146">Adja meg a szerző és a rendszer egy mappát, ahová a csomagokat menteni fogja kérni.</span><span class="sxs-lookup"><span data-stu-id="b862f-146">You will be prompted to supply the Author and a folder on your system where you want the packages to be saved.</span></span>

## <a name="deleting-personal-data-from-the-powershell-gallery"></a><span data-ttu-id="b862f-147">Személyes adatok törlése a PowerShell-galériából</span><span class="sxs-lookup"><span data-stu-id="b862f-147">Deleting Personal Data From The PowerShell Gallery</span></span>

<span data-ttu-id="b862f-148">A PowerShell-Galériabeli fiók vagy bármilyen saját a PowerShell-galériából a csomag törlésére, e-mailben cgadmin@microsoft.com és a cím: "Általános adatvédelmi rendelet kérése ehhez a fiókhoz kapcsolódó elemek".</span><span class="sxs-lookup"><span data-stu-id="b862f-148">To delete your PowerShell Gallery account or any package you own in the PowerShell Gallery, send email to cgadmin@microsoft.com with the title: "GDPR Request for items relating to this account".</span></span>
<span data-ttu-id="b862f-149">Az üzenet törzsében milyen információkat szeretne törölt állapotba.</span><span class="sxs-lookup"><span data-stu-id="b862f-149">In the body of the message state what information you want deleted.</span></span> <span data-ttu-id="b862f-150">Például:</span><span class="sxs-lookup"><span data-stu-id="b862f-150">For example:</span></span>

- <span data-ttu-id="b862f-151">Törölje a csomag "package name" verzió x.y.z</span><span class="sxs-lookup"><span data-stu-id="b862f-151">Please delete version x.y.z of my package "package name"</span></span>
- <span data-ttu-id="b862f-152">Törölje az összes verzióját a csomag "package name"</span><span class="sxs-lookup"><span data-stu-id="b862f-152">Please delete all versions of my package "package name"</span></span>
- <span data-ttu-id="b862f-153">Törölje a saját PowerShell-Galériabeli fiók</span><span class="sxs-lookup"><span data-stu-id="b862f-153">Please delete my PowerShell Gallery account</span></span>

<span data-ttu-id="b862f-154">A PowerShell-galériából rendszergazdák 7 munkanapon belül választ fog kapni.</span><span class="sxs-lookup"><span data-stu-id="b862f-154">The PowerShell Gallery administrators will reply within 7 business days.</span></span>
<span data-ttu-id="b862f-155">A megadott csomagokat a kérés elküldése után 30 napon belül törölve lesz.</span><span class="sxs-lookup"><span data-stu-id="b862f-155">The packages specified will be deleted within 30 days after the request is sent.</span></span>
