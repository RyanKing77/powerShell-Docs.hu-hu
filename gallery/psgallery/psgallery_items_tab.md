---
ms.date: 2017-06-12
contributor: JKeithB
ms.topic: conceptual
keywords: "gyűjtemény, a powershell, a parancsmag, a psgallery"
title: psgallery_items_tab
ms.openlocfilehash: 8704091542de5c19817ab0b4f77fd98987084b5d
ms.sourcegitcommit: 1a0a0928c1e3cae4e8df8d79b0737bd7ed6b4e47
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/21/2017
---
# <a name="items-tab"></a>Elemek lap

A [elemek lap](https://www.powershellgallery.com/items) a PowerShell-galériában összes rendelkezésre álló elemek megjelenítése.

Számos módon szűrése, rendezése és az elemek.
Egy adott elem részletes adatainak megtekintéséhez kattintson az elemet.

## <a name="filter-by"></a>Szűrés

A legördülő listán a "Szűrő által" lehetővé teszi a felhasználók által az eredmények szűréséhez:
* Előzetes tartalmazza
* Csak állandó

"Prerelease" és "Stable" kapcsolatos információkért lásd: [Prerelease Versioning PowerShellGet és a PowerShell-galériában hozzáadja](https://blogs.msdn.microsoft.com/powershell/2017/12/05/prerelease-versioning-added-to-powershellget-and-powershell-gallery/) a PowerShell csapatának blogját.

A jelölőnégyzet alatti legördülő engedélyezése a felhasználók által az eredmények szűréséhez:
* Konfigurációelem-típusok
  - Modul
  - Parancsfájl
* Kategóriák
  - Parancsmag
  - A DSC-erőforrás
  - Függvény
  - Szerepkör-funkció
  - munkafolyamat

Tekintse meg a PowerShell-galériában csak modulok, ellenőrizze a Konfigurációelem-típusok modulja.
Csak a PowerShell-galériában parancsfájlok megtekintéséhez hasonlóan ellenőrizze a Konfigurációelem-típusok parancsfájl.

> [!NOTE]
> Szűrők jellegűek.
> Példa: Egy elemet tartalmazó parancsmag és funkció is megjelenik, ha a rendszer ellenőrzi az parancsmag vagy függvényt (vagy mindkettőt).
> Ha nem választja, az elem nem jelenik meg.
> Ehhez hasonlóan az összes kategória van kiválasztva, ha csak az ezekben a kategóriákban egyikét tartalmazó elemek jelenik meg.
> **Nem tartoznak sem, ezen kategóriák elemek nem jelennek meg.**

## <a name="sort-by"></a>Rendezési szempont

A Rendezés legördülő lista lehetővé teszi a felhasználóknak szűrje az eredményeket:
* Népszerűségét - népszerűségét letöltése száma határozza meg
* A-Z - elem név szerint
* Legutóbbi - elemek jelennek meg a közzétételi dátum szerinti sorrendben

## <a name="search-box"></a>Keresés mezőbe

A keresőmezőbe lehetővé teszi, hogy a felhasználóknak a kulcsszavak elemeket.
További információkért lásd: [gyűjtemény keresési szintaxisának](psgallery_search_syntax.md).
