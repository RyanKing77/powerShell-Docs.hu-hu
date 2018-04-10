---
ms.date: 06/05/2017
keywords: PowerShell parancsmag
title: A parancssorbővítés használata
ms.assetid: c8730471-bf6a-43b8-ab1d-f9ef5a74f04e
ms.openlocfilehash: 3d047bf0691c8a304d7637aa50fba6ae99709a82
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="using-tab-expansion"></a>A parancssorbővítés használata

Parancssori ismertetése gyakran hardvermódosításainak végezze el automatikusan, a hosszú fájlok és parancsok nevében parancs bejegyzés felgyorsítása és kezeléséről. Windows PowerShell lehetővé teszi a fájlok és parancsmag nevének billentyűkombináció lenyomásával töltse ki a **lapon** kulcs.

> [!NOTE]
> A belső függvény TabExpansion vagy TabExpansion2 lapon bővítése szabályozza. Mivel ez a funkció módosíthatják vagy felül, ismertető az alapértelmezett PowerShell konfiguráció viselkedésének útmutatóját.

A fájlnév vagy az elérési út, a rendelkezésre álló lehetőségek automatikusan kitölti, írja be a nevet, majd kattintson a részét a **lapon** kulcs. PowerShell lesz automatikusan bontsa ki a nevét az első találatra talált. Nyomja le az **lapon** kulcs ismételten értéke között fog minden a választható.

A parancsmagok neve lap bővítése kis mértékben eltér. A parancsmag neve lap bővítése használatához írja be a teljes első részét a nevét (művelet) és az azt követő kötőjelet. Kitöltése több részleges egyezéssel a nevét. Például, ha beírja **get-co** és nyomja le az **lapon** kulcs, PowerShell lesz automatikusan bontsa ki a a **Get-Command** parancsmag (értesítés is módosítja az eset a betűk a szabványos formában). Ha lenyomja az **lapon** kulcs újra, PowerShell váltja fel a csak más névvel megegyező nevű parancsmag, **Get-tartalom**.

Lapon bővítése ismételten használható ugyanabban a sorban. Például használhatja lapon bővítése nevét a **Get-tartalom** parancsmag megadásával:

```
PS> Get-Con<Tab>
```

Amikor lenyomja az a **lapon** kulcs, a parancs bontja ki:

```
PS> Get-Content
```

Ezután részben adja meg a naplófájl elérési útja a telepítő aktív, és újra lapon bővítése használja:

```
PS> Get-Content c:\windows\acts<Tab>
```

Amikor lenyomja az a **lapon** kulcs, a parancs bontja ki:

```
PS> Get-Content C:\windows\actsetup.log
```

> [!NOTE]
> A lap bővítése folyamat egy korlátozása, hogy lapok értelmezi szót befejezése megkísérli. Ha másolja, és parancspéldákban illessze be a PowerShell-konzolban, győződjön meg arról, hogy a minta nem tartalmaz-e lapok; Ha igen, az eredmények előre nem látható lesz, és szinte biztosan nem lesz szándékainak.