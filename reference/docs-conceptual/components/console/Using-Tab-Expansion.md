---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: A parancssorbővítés használata
ms.assetid: c8730471-bf6a-43b8-ab1d-f9ef5a74f04e
ms.openlocfilehash: 3d047bf0691c8a304d7637aa50fba6ae99709a82
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62086935"
---
# <a name="using-tab-expansion"></a>A parancssorbővítés használata

Parancssori parancskörnyezet gyakran hardvermódosításainak fejezze be a nevét, illetve hosszú fájlok vagy parancsok automatikusan, felgyorsítva a parancs bejegyzést, és biztosítják, hogy. Windows PowerShell lehetővé teszi, hogy a fájlok és a parancsmag nevének lenyomásával töltse ki a **lapon** kulcsot.

> [!NOTE]
> A parancssorbővítés a belső függvény TabExpansion vagy TabExpansion2 vezérli. Mivel ez a függvény módosíthatják vagy felülírni, az adott vitafórum egy útmutató, amellyel a PowerShell alapértelmezett konfiguráció viselkedésének.

A fájlnév vagy elérési útját a rendelkezésre álló lehetőségek közül automatikusan kitölti, írja be a nevét, majd nyomja le a részét a **lapon** kulcsot. PowerShell lesz automatikusan bontsa ki a nevét az első egyezést talált. Nyomja le az **lapon** kulcs ismételt fog ciklus keresztül a rendelkezésre álló lehetőségek mindegyikét.

A parancssorbővítés parancsmag neve kismértékben eltér. A parancssorbővítés használata a parancsmag neve, írja be a nevét (művelet) és az azt követő kötőjel teljes első részét. Kitöltheti a további részleges nevét. Például, ha beírja **get-co** és nyomja le az **lapon** kulcs PowerShell automatikusan ki ezt a a **Get-Command** parancsmag (értesítés is megváltozik az eset a betűk a szabványos formában). Ha lenyomja **lapon** kulcs ismét PowerShell váltja fel a csak más névvel megegyező nevű parancsmagot, **Get-tartalom**.

A parancssorbővítés többször használható ugyanabban a sorban. Például használhatja a parancssorbővítés nevére a **Get-tartalom** parancsmag megadásával:

```
PS> Get-Con<Tab>
```

Amikor lenyomja a **lapon** kulcs, a parancs kibontja a:

```
PS> Get-Content
```

Ezután részben adja meg a naplófájl elérési útja a beállítás aktív, és újra a parancssorbővítés használata:

```
PS> Get-Content c:\windows\acts<Tab>
```

Amikor lenyomja a **lapon** kulcs, a parancs kibontja a:

```
PS> Get-Content C:\windows\actsetup.log
```

> [!NOTE]
> A lap csoportbővítési folyamatának egyik korlátozása, hogy lapok értelmezi kísérletek szó végrehajtásához. Ha másolja és illessze be a PowerShell-konzolt parancspéldákban, győződjön meg róla, hogy a minta nesmí obsahovat tabulátory; Ha igen, az eredmények előre nem látható lesz, és szinte biztosan nem kívánt.