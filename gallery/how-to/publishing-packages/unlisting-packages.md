---
ms.date: 06/12/2017
contributor: JKeithB
keywords: katalógus, a powershell, a parancsmag, a psgallery
title: Csomagok listázásának megszüntetése
ms.openlocfilehash: fb66fd23dae1d4640056a764c31426f61f56d910
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62084113"
---
# <a name="unlisting-packages"></a>Csomagok eltávolítása a listáról

**Miért éppen eltávolítja egy csomagot a beállítás nem elérhető PowerShell-galériából?**

A PowerShell-galériában nem támogatja a felhasználók végleges törlése a csomagokat.
Ez lehetővé teszi mások a csomagok a jövőben nem kell bajlódnunk lehetséges oldaltörések függőségek kibontakozni.
Például ha az Azure-modul függ, a Pester modul, és az Azure-modul el lesz távolítva a katalógusban, majd a felhasználó többé nem használja a Pester modul.

Ahelyett, hogy eltávolítaná egy csomagot, azonban akkor is unlist, helyette.

**Mire listázásának megszüntetése, tegye a PowerShell-galériából csomag?**

Például modul vagy a PowerShell-galériából a parancsfájl egy csomag listázásának megszüntetése eltávolítja azt a csomagok lapot. Ezenkívül fel nem sorolt csomagok nem észlelhető a Keresősáv használatával.
Egy listán nem szereplő csomag csak úgy, hogy adja meg a pontos nevét és a csomag verzióját.
Emiatt egy csomag listázásának megszüntetése nem megszakítja a más modulok vagy parancsfájlok, amelyek függnek tőle.

A csomag unlist keresse fel a csomag Részletek lap, és válassza ki a modul törlése. Törölje a jelet az "Szerepel a listában" jelölőnégyzetből, és kattintson a Mentés gombra.

**Hogyan távolíthatok el egy csomagot?**

Ha egy olyan forgatókönyvet, ahol a csomag törlése szükség, lépjen kapcsolatba a PowerShell-galéria rendszergazdák.
Érvényes törlés forgatókönyvek a következők:
- A szerzői jogsértés problémákat.
- A csomag tartalma potenciálisan káros.
- A csomagban bizalmas adatokat.

Egy törlése csomag kérelmet a PowerShell-galéria rendszergazdáknak küldéséhez látogasson el a csomag részletei lapon, és válassza ki a forduljon az ügyfélszolgálathoz.
