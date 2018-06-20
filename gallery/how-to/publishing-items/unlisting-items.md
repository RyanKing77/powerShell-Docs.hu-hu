---
ms.date: 06/12/2017
contributor: JKeithB
keywords: gyűjtemény, a powershell, a parancsmag, a psgallery
title: Elemek listázásának megszüntetése
ms.openlocfilehash: bdcceba0ba18ade6a1d0f94602fd8d0f64af8936
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/16/2018
ms.locfileid: "34187534"
---
# <a name="unlisting-items"></a>Elemek listázásának megszüntetése

**Ezért egy elem éppen eltávolítja a PowerShell-galériából lehetőség nincs felfedve?**

A PowerShell-galériában nem támogatja a felhasználók saját elemek véglegesen törli.
Ez lehetővé teszi, hogy mások az elemek anélkül, hogy a jövőben lehetséges oldaltörések függőségek végrehajthat.
Például ha a Pester modul az Azure-moduljának függ, és az Azure rendszer eltávolítja a modult a gyűjteményből, akkor a felhasználó többé nem használja a Pester modul.

Helyett egy elem eltávolítása, azonban akkor is unlist, helyette.

**Mire unlisting hajtsa végre a megfelelő elemre a PowerShell-galériában?**

Egy elem modul vagy a PowerShell-galériában parancsfájl például unlisting eltávolítja a elemek lap. Listán nem szereplő elemek emellett nem lesz felderíthető Keresősáv használatával.
Töltse le a listán nem szereplő elem csak úgy adhatja meg a pontos nevét és verzióját, az elem.
Emiatt egy elem unlisting nem megszakítja más modulok vagy parancsfájlok, amelyek függenek.

A cikk unlist, keresse fel az elem részleteit megjelenítő oldalra, és törlése lehetőséggel. Törölje a jelet az "Felsorolt" jelölőnégyzetből, és kattintson a Mentés gombra.

**Hogyan távolíthatom elemet?**

Ha egy olyan forgatókönyvet, ahol elem törlését szükség, lépjen kapcsolatba a PowerShell-Galériabeli rendszergazdák.
Érvényes törlés forgatókönyvek a következők:
- Szerzői jogsértéssel kapcsolatos problémákat.
- Az elem tartalma potenciálisan káros tartalmaz.
- Az elem tartalmaz bizalmas adatokat.

Küldje el a törlése elem elküldeni a kérelmet a PowerShell-Galériabeli rendszergazdák, látogasson el a cikk információs lapját, és válassza ki a forduljon a támogatási szolgálathoz.