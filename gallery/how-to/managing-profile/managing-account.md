---
ms.date: 09/05/2018
contributor: JKeithB
keywords: katalógus, a powershell, a parancsmag, a psgallery
title: PowerShell-galéria fiókjának beállításai
ms.openlocfilehash: ebe784ec5aae5ff3a4d444d12a168ef38aaef65f
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55687425"
---
# <a name="powershell-gallery-account-settings"></a>PowerShell-galéria fiókjának beállításai

A PowerShell-Galériabeli fiók országom nevét, amely az identitás van csatolva. Az identitáshoz vagy a Microsoft ID, például `user@hotmail.com` vagy `user@outlook.com`, vagy egy Azure Active Directory (AAD) fiókot.

A PowerShell-galériából a következő fiók beállításokat biztosítja:

- A PowerShell-galériából fiókjához társított e-mail-fiókot
- A PowerShell-galériából küldött e-mailekre vonatkozó beállításokat
- A PowerShell-Galériabeli fiók társított felhasználói fiók
- A képen látható, a PowerShell-galériából fiókjához társított

## <a name="email-address"></a>E-mail cím

Az e-mail-cím az a hely PowerShell-galériából az értesítésekhez. Nincs a bejelentkezési fiókjának megfelelő. Használhat bármilyen e-mail-fiók hozzáfér. Az e-mail-címét soha nem közvetlenül más felhasználók számára a PowerShell-galériából biztosítják.

![E-mail-cím megváltoztatása](../../Images/PSGallery_AcccountEmailAddress.png)

Amikor új e-mail címet, a PowerShell-galériából egy ellenőrző levelet küld, hogy a cím. Az ellenőrző e-mailt vissza a PowerShell-galériából, a folyamat befejezéséhez mutató hivatkozást tartalmaz. Az ellenőrzési folyamat befejezte, amíg az összes értesítések lesznek küldve a korábbi címre.

## <a name="email-notifications"></a>E-mail-értesítések

PowerShell-galériából a következő értesítési beállításokat biztosítja:

- Felhasználók felvehesse velem a kapcsolatot a PowerShell-galériából keresztül
- Értesítést kérek, ha egy csomagot a rendszer továbbítja a PowerShell-galériából saját fiók használatával

![E-mail-cím megváltoztatása](../../Images/PSGallery_AccountEmailOptions.png)

Az oldalon feltüntetett, mert a PowerShell-galériából kritikus fontosságú értesítések nem tiltható le.
Ezek a következők:

- A biztonsági értesítéseket
- A PowerShell-galériából rendszergazda fiók felügyeleti értesítések
- Értesítések a tesztek futtatásához a PowerShell-galériából, a végrehajtott módosítások

## <a name="change-your-login-account"></a>A bejelentkezési fiók módosítása

Ha módosítani szeretné a bejelentkezési fiókjának, kell bejelentkeznie a jelenlegi fiókkal jelentkezik be. A következő lépések segítségével elvégezheti a módosítást.

![Bejelentkezési beállítások](../../Images/PSGallery_LoginAccountSettings.png)

1. Kattintson a **fiók módosítása**. Egy előugró ablak azt ismerteti, hogy alkalmazza a bejelentkezési fiók módosítása a PowerShell-galériából a fiók összes felhasználását. Tekintse át az adatokat, majd kattintson a **OK** folytatásához.

   ![Bejelentkezési beállítások](../../Images/PSGallery_LoginAccountChange-1.png)

2. A program ekkor kéri, jelentkezzen be a _új fiók_.

   ![Bejelentkezési beállítások](../../Images/PSGallery_LoginAccountChange-2.png)

3. Amikor rákattint **tovább**, megjelenik egy üzenet, hogy be van jelentkezve a jelenlegi fiókkal.
   Kattintson a **jelentkezzen ki, és jelentkezzen be egy másik fiókkal**.

   ![Bejelentkezési beállítások](../../Images/PSGallery_LoginAccountChange-3.png)

4. Adja meg az új fiók jelszavát. Miután megadta a jelszót, amelyről a Fiókbeállítások lapra, amelyen látható, hogy a bejelentkezési fiókjának frissítése megtörtént.


## <a name="enable-two-factor-authentication-2fa"></a>A Kétfaktoros hitelesítés (2FA) engedélyezése

A kétfaktoros hitelesítés ajánlott minden felhasználó, aki manuálisan közzétenni a PowerShell-galériában. A kétfaktoros hitelesítés engedélyezéséhez a bejelentkezési fiókjának rendelkeznie kell legalább két űrlapos hitelesítés regisztrálva. Az egyik jelszó és egyéb lehet:

- Egy telefonszám, amely képes a szöveges üzenetet fogadni
- Egy regisztrált authenticator alkalmazás, például a Microsoft Authenticator a mobiltelefon

Ezek űrlapos hitelesítés az AAD-fiók adatait vagy a Microsoft ID-fiók biztonsági beállításokat kell konfigurálni.

2FA engedélyezését követően kell elvégezniük a konfigurált űrlapos hitelesítés minden alkalommal, amikor bejelentkezik a PowerShell-galériában.

> [!IMPORTANT]
> A PowerShell-galériából hely kétfaktoros hitelesítés engedélyezését nem kell minden, a bejelentkezési fiók használata 2FA engedélyezéséhez. További információkért lásd: [tudnivalók a kétlépéses ellenőrzés](https://support.microsoft.com/help/12408/microsoft-account-about-two-step-verification).

## <a name="change-your-profile-picture"></a>A profilkép módosítása

A PowerShell-galériából való tárolása és megjelenítése a képen látható, a profilhoz társított Gravatar támaszkodik. Frissíti a profilkép, látogasson el [Gravatar.com](http://www.gravatar.com/).
