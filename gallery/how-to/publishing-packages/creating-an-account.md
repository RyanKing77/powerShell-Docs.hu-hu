---
ms.date: 09/11/2018
contributor: JKeithB
keywords: katalógus, a powershell, a parancsmag, a psgallery
title: PowerShell-Galériabeli fiók létrehozása
ms.openlocfilehash: e4cf73edb03267cff6bbcc0cf3b754225e45be9f
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62084220"
---
# <a name="creating-a-powershell-gallery-account"></a>PowerShell-Galériabeli fiók létrehozása

Semmit a PowerShell-galériából történő közzététele előtt létre kell hoznia egy PowerShell-Galériabeli fiók.
PowerShell-galériából fiókokhoz kell társítani egy levelezési bejelentkezési fiókot. Ez a fiók lehet egy Azure Active Directory-fiókot, vagy a Microsoft ID, például az Outlook.com-os vagy hotmail.com-os e-mail-fiók.

PowerShell-Galériabeli fiók létrehozásához lépjen a [ https://PowerShellGallery.com ](https://PowerShellGallery.com) , majd kattintson a **jelentkezzen be a** az alábbi képen látható módon.

![Új fiók regisztrálása](../../Images/CreateAccount-Register.png)

Az Azure Active Directory-fiók használatához válassza **munkahelyi vagy iskolai fiókkal**, és jelentkezzen be a fiókjával. A Microsoft ID használatához válasszon **személyes fiók** , és jelentkezzen be.

Ezután kéri felhasználónevét, a PowerShell-galériából létrehozásához. Tekintse át a használati feltételeket és adatvédelmi szabályzatát, írjon be egy felhasználónevet, és kattintson **regisztrálása**.

> [!NOTE]
> A fiók neve a létrehozásuk után nem módosítható. További információkért lásd: [csomag tulajdonosainak kezelése](managing-package-owners.md).

## <a name="recommended-practices-for-powershell-gallery-accounts"></a>PowerShell-galériából fiókok ajánlott eljárásai

Fontos aktívan figyeljük a PowerShell-galériából fiókjához használt e-mail-fiók. A PowerShell-galériából csomagok tulajdonosok folytatott minden kommunikáció az e-mail-cím keresztül történik. Ha a PowerShell-galéria üzemeltetési csapat tud kapcsolatba lépni a csomag tulajdonosát, hogy fiókdíjat csomag törlése.

Szervezetek számára, amelyek gyakran közzététele a PowerShell-galériában erre a célra hozzon létre egy egyedi külső fiókot. Azt javasoljuk, hogy e-mail továbbítás használatával értesítések címre továbbítsa a szervezeten belül.

Ha több tulajdonosok társítva a csomaghoz, minden PowerShell-galériából értesítést kapnak összes tulajdonos. További információkért lásd: [csomag tulajdonosainak kezelése](managing-package-owners.md).
