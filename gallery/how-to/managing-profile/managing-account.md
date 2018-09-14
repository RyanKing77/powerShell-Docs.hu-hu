---
ms.date: 09/05/2018
contributor: JKeithB
keywords: katalógus, a powershell, a parancsmag, a psgallery
title: PowerShell-Galériabeli fiók beállításai
ms.openlocfilehash: dd7b8b3a99b5b7fbfec5d7f82b81dd6d5cfb906c
ms.sourcegitcommit: e46b868f56f359909ff7c8230b1d1770935cce0e
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/13/2018
ms.locfileid: "45523348"
---
# <a name="powershell-gallery-account-settings"></a><span data-ttu-id="3539b-103">PowerShell-Galériabeli fiók beállításai</span><span class="sxs-lookup"><span data-stu-id="3539b-103">PowerShell Gallery Account Settings</span></span>

<span data-ttu-id="3539b-104">A PowerShell-Galériabeli fiók országom nevét, amely az identitás van csatolva.</span><span class="sxs-lookup"><span data-stu-id="3539b-104">Your PowerShell Gallery account is a publicly visible name that is linked to an identity.</span></span> <span data-ttu-id="3539b-105">Az identitáshoz vagy a Microsoft ID, például `user@hotmail.com` vagy `user@outlook.com`, vagy egy Azure Active Directory (AAD) fiókot.</span><span class="sxs-lookup"><span data-stu-id="3539b-105">That identity is either a Microsoft ID, like `user@hotmail.com` or `user@outlook.com`, or an Azure Active Directory (AAD) account.</span></span>

<span data-ttu-id="3539b-106">A PowerShell-galériából a következő fiók beállításokat biztosítja:</span><span class="sxs-lookup"><span data-stu-id="3539b-106">The PowerShell Gallery provides the following account settings:</span></span>

- <span data-ttu-id="3539b-107">A PowerShell-galériából fiókjához társított e-mail-fiókot</span><span class="sxs-lookup"><span data-stu-id="3539b-107">The email account associated with your PowerShell Gallery account</span></span>
- <span data-ttu-id="3539b-108">A PowerShell-galériából küldött e-mailekre vonatkozó beállításokat</span><span class="sxs-lookup"><span data-stu-id="3539b-108">Options for email notifications sent from the PowerShell Gallery</span></span>
- <span data-ttu-id="3539b-109">A PowerShell-Galériabeli fiók társított felhasználói fiók</span><span class="sxs-lookup"><span data-stu-id="3539b-109">The user account associated with your PowerShell Gallery account</span></span>
- <span data-ttu-id="3539b-110">A képen látható, a PowerShell-galériából fiókjához társított</span><span class="sxs-lookup"><span data-stu-id="3539b-110">The picture associated with your PowerShell Gallery account</span></span>

## <a name="email-address"></a><span data-ttu-id="3539b-111">E-mail cím</span><span class="sxs-lookup"><span data-stu-id="3539b-111">Email address</span></span>

<span data-ttu-id="3539b-112">Az e-mail-cím az a hely PowerShell-galériából az értesítésekhez.</span><span class="sxs-lookup"><span data-stu-id="3539b-112">The email address is the destination for PowerShell Gallery notifications.</span></span> <span data-ttu-id="3539b-113">Nincs a bejelentkezési fiókjának megfelelő.</span><span class="sxs-lookup"><span data-stu-id="3539b-113">It does not have to match the login account.</span></span> <span data-ttu-id="3539b-114">Használhat bármilyen e-mail-fiók hozzáfér.</span><span class="sxs-lookup"><span data-stu-id="3539b-114">You may use any email account you have access to.</span></span> <span data-ttu-id="3539b-115">Az e-mail-címét soha nem közvetlenül más felhasználók számára a PowerShell-galériából biztosítják.</span><span class="sxs-lookup"><span data-stu-id="3539b-115">Your email address is never directly provided by the PowerShell Gallery to other users.</span></span>

![E-mail-cím megváltoztatása](../../Images/PSGallery_AcccountEmailAddress.png)

<span data-ttu-id="3539b-117">Amikor új e-mail címet, a PowerShell-galériából egy ellenőrző levelet küld, hogy a cím.</span><span class="sxs-lookup"><span data-stu-id="3539b-117">When you enter a new email address, the PowerShell Gallery sends a verification mail to that address.</span></span> <span data-ttu-id="3539b-118">Az ellenőrző e-mailt vissza a PowerShell-galériából, a folyamat befejezéséhez mutató hivatkozást tartalmaz.</span><span class="sxs-lookup"><span data-stu-id="3539b-118">The verification mail contains a link back to the PowerShell Gallery to complete the change process.</span></span> <span data-ttu-id="3539b-119">Az ellenőrzési folyamat befejezte, amíg az összes értesítések lesznek küldve a korábbi címre.</span><span class="sxs-lookup"><span data-stu-id="3539b-119">Until you complete the verification process, all notifications are sent to the previous address.</span></span>

## <a name="email-notifications"></a><span data-ttu-id="3539b-120">E-mail-értesítések</span><span class="sxs-lookup"><span data-stu-id="3539b-120">Email notifications</span></span>

<span data-ttu-id="3539b-121">PowerShell-galériából a következő értesítési beállításokat biztosítja:</span><span class="sxs-lookup"><span data-stu-id="3539b-121">PowerShell Gallery provides the following notification options:</span></span>

- <span data-ttu-id="3539b-122">Felhasználók felvehesse velem a kapcsolatot a PowerShell-galériából keresztül</span><span class="sxs-lookup"><span data-stu-id="3539b-122">Users can contact me through the PowerShell Gallery</span></span>
- <span data-ttu-id="3539b-123">Értesítést kérek, ha egy elemet a rendszer továbbítja a PowerShell-galériából saját fiók használatával</span><span class="sxs-lookup"><span data-stu-id="3539b-123">Notify me when an item is pushed to the PowerShell Gallery using my account</span></span>

![E-mail-cím megváltoztatása](../../Images/PSGallery_AccountEmailOptions.png)

<span data-ttu-id="3539b-125">Az oldalon feltüntetett, mert a PowerShell-galériából kritikus fontosságú értesítések nem tiltható le.</span><span class="sxs-lookup"><span data-stu-id="3539b-125">As noted on the page, critical notifications from the PowerShell Gallery can't be disabled.</span></span>
<span data-ttu-id="3539b-126">Ezek a következők:</span><span class="sxs-lookup"><span data-stu-id="3539b-126">These include:</span></span>

- <span data-ttu-id="3539b-127">A biztonsági értesítéseket</span><span class="sxs-lookup"><span data-stu-id="3539b-127">Security notifications</span></span>
- <span data-ttu-id="3539b-128">A PowerShell-galériából rendszergazda fiók felügyeleti értesítések</span><span class="sxs-lookup"><span data-stu-id="3539b-128">Account management notifications from PowerShell Gallery administrators</span></span>
- <span data-ttu-id="3539b-129">Értesítések a tesztek futtatásához a PowerShell-galériából, a végrehajtott módosítások</span><span class="sxs-lookup"><span data-stu-id="3539b-129">Notifications about the tests run by the PowerShell Gallery for submissions you have made</span></span>

## <a name="change-your-login-account"></a><span data-ttu-id="3539b-130">A bejelentkezési fiók módosítása</span><span class="sxs-lookup"><span data-stu-id="3539b-130">Change your login account</span></span>

<span data-ttu-id="3539b-131">Ha módosítani szeretné a bejelentkezési fiókjának, kell bejelentkeznie a jelenlegi fiókkal jelentkezik be.</span><span class="sxs-lookup"><span data-stu-id="3539b-131">To change the login account, you must be signed in with the current account.</span></span> <span data-ttu-id="3539b-132">A következő lépések segítségével elvégezheti a módosítást.</span><span class="sxs-lookup"><span data-stu-id="3539b-132">Use the following steps to complete the change.</span></span>

![Bejelentkezési beállítások](../../Images/PSGallery_LoginAccountSettings.png)

1. <span data-ttu-id="3539b-134">Kattintson a **fiók módosítása**.</span><span class="sxs-lookup"><span data-stu-id="3539b-134">Click on **Change Account**.</span></span> <span data-ttu-id="3539b-135">Egy előugró ablak azt ismerteti, hogy alkalmazza a bejelentkezési fiók módosítása a PowerShell-galériából a fiók összes felhasználását.</span><span class="sxs-lookup"><span data-stu-id="3539b-135">A pop-up window explains that changing the login account applies to all uses of that account in the PowerShell Gallery.</span></span> <span data-ttu-id="3539b-136">Tekintse át az adatokat, majd kattintson a **OK** folytatásához.</span><span class="sxs-lookup"><span data-stu-id="3539b-136">Review the information, then click **OK** to continue.</span></span>

   ![Bejelentkezési beállítások](../../Images/PSGallery_LoginAccountChange-1.png)

2. <span data-ttu-id="3539b-138">A program ekkor kéri, jelentkezzen be a _új fiók_.</span><span class="sxs-lookup"><span data-stu-id="3539b-138">You are then prompted to sign in using the _new account_.</span></span>

   ![Bejelentkezési beállítások](../../Images/PSGallery_LoginAccountChange-2.png)

3. <span data-ttu-id="3539b-140">Amikor rákattint **tovább**, megjelenik egy üzenet, hogy be van jelentkezve a jelenlegi fiókkal.</span><span class="sxs-lookup"><span data-stu-id="3539b-140">When you click **Next**, you see a message that you are signed in using the current account.</span></span>
   <span data-ttu-id="3539b-141">Kattintson a **jelentkezzen ki, és jelentkezzen be egy másik fiókkal**.</span><span class="sxs-lookup"><span data-stu-id="3539b-141">Click **Sign out and sign in with a different account**.</span></span>

   ![Bejelentkezési beállítások](../../Images/PSGallery_LoginAccountChange-3.png)

4. <span data-ttu-id="3539b-143">Adja meg az új fiók jelszavát.</span><span class="sxs-lookup"><span data-stu-id="3539b-143">Enter the password of the new account.</span></span> <span data-ttu-id="3539b-144">Miután megadta a jelszót, amelyről a Fiókbeállítások lapra, amelyen látható, hogy a bejelentkezési fiókjának frissítése megtörtént.</span><span class="sxs-lookup"><span data-stu-id="3539b-144">After entering the password, you are returned to the Account Settings page showing you that the login account has been updated.</span></span>


## <a name="enable-two-factor-authentication-2fa"></a><span data-ttu-id="3539b-145">A Kétfaktoros hitelesítés (2FA) engedélyezése</span><span class="sxs-lookup"><span data-stu-id="3539b-145">Enable Two-Factor Authentication (2FA)</span></span>

<span data-ttu-id="3539b-146">A kétfaktoros hitelesítés ajánlott minden felhasználó, aki manuálisan közzétenni a PowerShell-galériában.</span><span class="sxs-lookup"><span data-stu-id="3539b-146">Two-factor authentication is recommended for all users who publish manually to the PowerShell Gallery.</span></span> <span data-ttu-id="3539b-147">A kétfaktoros hitelesítés engedélyezéséhez a bejelentkezési fiókjának rendelkeznie kell legalább két űrlapos hitelesítés regisztrálva.</span><span class="sxs-lookup"><span data-stu-id="3539b-147">To enable two-factor authentication, the login account must have at least two forms of authentication registered.</span></span> <span data-ttu-id="3539b-148">Az egyik jelszó és egyéb lehet:</span><span class="sxs-lookup"><span data-stu-id="3539b-148">One is a password and the other forms can be:</span></span>

- <span data-ttu-id="3539b-149">Egy telefonszám, amely képes a szöveges üzenetet fogadni</span><span class="sxs-lookup"><span data-stu-id="3539b-149">A phone number that can receive text messages</span></span>
- <span data-ttu-id="3539b-150">Egy regisztrált authenticator alkalmazás, például a Microsoft Authenticator a mobiltelefon</span><span class="sxs-lookup"><span data-stu-id="3539b-150">A registered authenticator application, such as Microsoft Authenticator for your mobile phone</span></span>

<span data-ttu-id="3539b-151">Ezek űrlapos hitelesítés az AAD-fiók adatait vagy a Microsoft ID-fiók biztonsági beállításokat kell konfigurálni.</span><span class="sxs-lookup"><span data-stu-id="3539b-151">These forms of authentication must be configured in your AAD account information or in your Microsoft ID Account Security settings.</span></span>

<span data-ttu-id="3539b-152">2FA engedélyezését követően kell elvégezniük a konfigurált űrlapos hitelesítés minden alkalommal, amikor bejelentkezik a PowerShell-galériában.</span><span class="sxs-lookup"><span data-stu-id="3539b-152">Once 2FA is enabled, you are required to authenticate using the configured forms of authentication every time you sign in to the PowerShell Gallery.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3539b-153">A PowerShell-galériából hely kétfaktoros hitelesítés engedélyezését nem kell minden, a bejelentkezési fiók használata 2FA engedélyezéséhez.</span><span class="sxs-lookup"><span data-stu-id="3539b-153">Enabling two-factor authentication for the PowerShell Gallery site does not require you to enable 2FA for all uses of your login account.</span></span> <span data-ttu-id="3539b-154">További információkért lásd: [tudnivalók a kétlépéses ellenőrzés](https://support.microsoft.com/help/12408/microsoft-account-about-two-step-verification).</span><span class="sxs-lookup"><span data-stu-id="3539b-154">For more information, see [About two-step verification](https://support.microsoft.com/help/12408/microsoft-account-about-two-step-verification).</span></span>

## <a name="change-your-profile-picture"></a><span data-ttu-id="3539b-155">A profilkép módosítása</span><span class="sxs-lookup"><span data-stu-id="3539b-155">Change your profile picture</span></span>

<span data-ttu-id="3539b-156">A PowerShell-galériából való tárolása és megjelenítése a képen látható, a profilhoz társított Gravatar támaszkodik.</span><span class="sxs-lookup"><span data-stu-id="3539b-156">The PowerShell Gallery relies on Gravatar to store and display the picture associated with your profile.</span></span> <span data-ttu-id="3539b-157">Frissíti a profilkép, látogasson el [Gravatar.com](http://www.gravatar.com/).</span><span class="sxs-lookup"><span data-stu-id="3539b-157">To update your profile image, visit [Gravatar.com](http://www.gravatar.com/).</span></span>
