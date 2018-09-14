---
ms.date: 09/11/2018
contributor: JKeithB
keywords: katalógus, a powershell, a parancsmag, a psgallery
title: PowerShell-Galériabeli fiók létrehozása
ms.openlocfilehash: 08d18310d9e18b00bd9e22efcc552dfd29f8982c
ms.sourcegitcommit: e46b868f56f359909ff7c8230b1d1770935cce0e
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/13/2018
ms.locfileid: "45522836"
---
# <a name="creating-a-powershell-gallery-account"></a>PowerShell-Galériabeli fiók létrehozása

Semmit a PowerShell-galériából történő közzététele előtt létre kell hoznia egy PowerShell-Galériabeli fiók.
PowerShell-galériából fiókokhoz kell társítani egy levelezési bejelentkezési fiókot. Ez a fiók lehet egy Azure Active Directory-fiókot, vagy a Microsoft ID, például az Outlook.com-os vagy hotmail.com-os e-mail-fiók.

PowerShell-Galériabeli fiók létrehozásához lépjen a [ https://PowerShellGallery.com ](https://PowerShellGallery.com) , majd kattintson a **jelentkezzen be a** az alábbi képen látható módon.

![Új fiók regisztrálása](../../Images/CreateAccount-Register.png)

Az Azure Active Directory-fiók használatához válassza **munkahelyi vagy iskolai fiókkal**, és jelentkezzen be a fiókjával. A Microsoft ID használatához válasszon **személyes fiók** , és jelentkezzen be.

Ezután kéri felhasználónevét, a PowerShell-galériából létrehozásához. Tekintse át a használati feltételeket és adatvédelmi szabályzatát, írjon be egy felhasználónevet, és kattintson **regisztrálása**.

> [!NOTE]
> A fiók neve a létrehozásuk után nem módosítható. További információkért lásd: [Konfigurációelem tulajdonosainak kezelése](managing-item-owners.md).

## <a name="recommended-practices-for-powershell-gallery-accounts"></a>PowerShell-galériából fiókok ajánlott eljárásai

Fontos aktívan figyeljük a PowerShell-galériából fiókjához használt e-mail-fiók. PowerShell-galériából elemek tulajdonosok folytatott minden kommunikáció az e-mail-cím keresztül történik. Ha a PowerShell-galéria üzemeltetési csapat tud kapcsolatba lépni egy munkaelem tulajdonosa, hogy egy elem törléséhez fiókdíjat.

Szervezetek számára, amelyek gyakran közzététele a PowerShell-galériában erre a célra hozzon létre egy egyedi külső fiókot. Azt javasoljuk, hogy e-mail továbbítás használatával értesítések címre továbbítsa a szervezeten belül.

Több olyan elem társítva, amikor minden PowerShell-galériából értesítést kapnak összes tulajdonos. További információkért lásd: [Konfigurációelem tulajdonosainak kezelése](managing-item-owners.md).
