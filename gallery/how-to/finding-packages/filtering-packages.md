---
ms.date: 06/12/2017
contributor: JKeithB
keywords: katalógus, a powershell, a parancsmag, a psgallery
title: Keresési eredmények szűrése
ms.openlocfilehash: 13270a310613a974e1588a9f56d443a936cfebb8
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62084402"
---
# <a name="filtering-search-results"></a>Keresési eredmények szűrése

A [csomagok lapján](https://www.powershellgallery.com/packages) jeleníti meg az összes elérhető csomagokat a PowerShell-galériában.

Számos módon szűrése, rendezése és keresése a csomagokat.
Egy adott csomag részleteinek megtekintéséhez kattintson a csomagot.

## <a name="filter-by"></a>Szűrés

A legördülő "Szűrő által" alatt lehetővé teszi a felhasználóknak szűrheti az eredményeket:
- Előzetes verzió
- Csak állandó

"Előzetes" és "Stabil" kapcsolatos információkért lásd: [Prerelease Versioning adja hozzá a PowerShellGet és PowerShell-galériából](https://blogs.msdn.microsoft.com/powershell/2017/12/05/prerelease-versioning-added-to-powershellget-and-powershell-gallery/) a PowerShell csapatának blogját.

A jelölőnégyzetek alatt a legördülő engedélyezése a felhasználók által az eredmények szűréséhez:
- A csomagok
  - Modul
  - Parancsfájl
- Categories
  - Parancsmag
  - DSC-erőforrás
  - Függvény
  - Szerepkör-képesség
  - Munkafolyamat

Csak a PowerShell-galériából a modulok megtekintéséhez ellenőrizze a csomag típusok modul.
Ehhez hasonlóan a szeretné csak a PowerShell-galériából a parancsfájlokat, ellenőrizze a csomag típusok parancsfájlt.

> [!NOTE]
> Szűrők jellegűek.
> Példa: Ha a rendszer ellenőrzi a parancsmag vagy függvényben (vagy mindkettő) parancsmagok és a functions tartalmazó csomag jelenik meg.
> Ha egyik sincs kijelölve, a csomag nem jelenik meg.
> Hasonlóképpen ha az összes kategória ki van jelölve, csak az ezekben a kategóriákban egyikét tartalmazó csomagok fog megjelenni.
> **Csomagok, amelyek nem tartozik egyik ezekben a kategóriákban nem jelenik meg.**

## <a name="sort-by"></a>Rendezés szempontja:

A Rendezés legördülő lehetővé teszi, hogy a felhasználók által az eredmények rendezéséhez:
- Népszerűség - népszerűsége letöltése száma határozza meg
- A-Z - csomag neve alapján betűrendben
- Legutóbbi - csomagok megjelennek a közzététel dátuma sorrendje

## <a name="search-box"></a>Keresőmező

A keresőmezőbe lehetővé teszi a felhasználóknak a csomagokat a kulcsszavak keresése.
További információkért lásd: [Katalóguskeresési szintaxis](search-syntax.md).
