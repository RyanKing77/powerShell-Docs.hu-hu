---
ms.date: 06/12/2017
contributor: JKeithB
ms.topic: conceptual
keywords: gyűjtemény, a powershell, a parancsmag, a psgallery
title: Tulajdonosainak kezelése
ms.openlocfilehash: e550b74ebde00cfbb154dbf4fb1fa4ae0582e029
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="managing-item-owners"></a>Tulajdonosainak kezelése

A PowerShell-galériában elemének tulajdonjogát ki az elemet a katalógusban közzétett határozzák meg.
Egyes esetekben a metaadatok kell lennie az első elem közzétételét, ami azt jelenti, hogy a tulajdonos metaadatok kell lennie változtatható, amíg az elemet nem túl.

Az összes elem tulajdonosok társak.
Ez azt jelenti, hogy bármely tulajdonosa közzététele egy elemet egy új verziója. Azt is jelenti, hogy bármely tulajdonosa távolíthatja bármely más tulajdonosa.
Nincs a tulajdonosnak további hatóság, mint más tulajdonosai.

## <a name="setting-an-items-initial-owner"></a>Egy elem kezdeti tulajdonos beállítása

PowerShell-galériában egy új elemet tesznek közzé, ha a felhasználót, hogy az elem közzétett határozza meg a kezdeti tulajdonosa. Ez határozza meg, amelynek API által a Publish-modul a parancsmag a kulcs lett megadva.

## <a name="adding-owners"></a>Tulajdonosok hozzáadása

Amint egy elem közzé lett téve a PowerShell-galériában, nem hívhat meg a legyen, egy elem tulajdonosainak további felhasználók.

1. [Jelentkezzen be](https://powershellgallery.com/users/account/LogOn) a fiókkal, amely a tulajdonos elem PowerShell gyűjteményébe.
2. Nyissa meg az elem lapot "Elemek" lapján, a Keresés vagy kattintson a felhasználónevére, majd [ **saját elemek kezelése**](https://www.powershellgallery.com/account/Packages).
3. Amikor egy elem tulajdonosaként jelentkezik be, tulajdonosok kezelése kapcsolat van kattintson a bal oldalon.
4. Adja meg a felhasználónevet, a tulajdonos, és kattintson a "Hozzáadás" személy.
5. E-mailt az új társtulajdonos lesz, majd küldi a meghívással elem tulajdonosa lesz.
6. Amennyiben az, hogy a felhasználó a hivatkozásra kattint, egy teljes társtulajdonos, elemre, beleértve a tulajdonos más felhasználók eltávolítása teljes hozzáféréssel rendelkező.

**Megjegyzés**: az új tulajdonos megerősíti, hogy tulajdonjoga, amíg azok *sem fog* tulajdonos elem jelenik.
Megtekintésekor a **tulajdonosok kezelése** lapon megjelenik egy "jóváhagyásra" bejegyzés aktuális tulajdonosai.
A meghívó lehet eltávolítani; ugyanúgy, mint más tulajdonosok távolítható el.
Ez a folyamat a meghívókat megakadályozza, hogy a felhasználók pontosan más felhasználók hozzáadása az elemek tulajdonosai.

Vegye figyelembe, hogy a "Szerző" metaadatok tisztán Szabadkézi szöveg; csak a "tulajdonos" szabályozza.


## <a name="removing-owners"></a>Tulajdonosok eltávolítása
Ha több tulajdonosok elemnél, és egy ki kell vonni, a folyamat egyszerű történik:

1. [Jelentkezzen be](https://powershellgallery.com/users/account/LogOn) PowerShell gyűjteményébe a fiókkal, amely a tulajdonos elem;
2. Nyissa meg az elem lapot elemek lapján, a Keresés vagy kattintson a felhasználónevére, majd [ **saját elemek kezelése**](https://www.powershellgallery.com/account/Packages).
3. Amikor egy elem tulajdonosaként jelentkezik be, tulajdonosok kezelése kapcsolat van a bal oldalon kattintson a;
4. Kattintson az "Eltávolítás" hivatkozásra mellett a tulajdonos távolíthatók el.



## <a name="transferring-item-ownership"></a>Elem tulajdonjogának átadása
Néha kapunk támogatási kérelmek áthelyezni a elem egy felhasználó egy másikra, de szinte mindig saját kezűleg megvalósításához.
Tulajdonjog visz át egy felhasználó egy másik egyszerűen a fenti két funkció kombinációja.

1. A jelenlegi tulajdonos meghívja az új felhasználó a társtulajdonos lesz, és az új felhasználó elfogadja a meghívás;
2. Az új felhasználó távolít el a régi felhasználói a tulajdonosok.

Ezt a kérelmet néhány űrlapok alatt érkezett, de a folyamatot a ugyanúgy működik.

* A cikk tulajdonjoga egy fejlesztőtől származó módosítása egy másikra
* A cikk véletlenül lett közzétéve, a megfelelő fiók használatával


## <a name="orphaned-items"></a>Árva elemeket
Egy utolsó forgatókönyv történt, de nem sokszor.
Elemek váltak árvaként, és az egyetlen elem tulajdonos fiók hozzáadása az új tulajdonos nem használható.
Íme néhány példa az ebben a forgatókönyvben:

* A tulajdonos fiókhoz rendelve egy e-mail címet, amely már nem létezik, és a felhasználó elfelejtette a jelszavát
* A regisztrált felhasználó kilépett a vállalattól, hozza létre a cikk és frissítése a cikk tulajdonosa nem érhető el
* Egy hiba, néhány olyan elemek csak hatással vannak, mert a cikk található valamilyen módon ownerless a katalógusban

A PowerShell-Galériabeli rendszergazdák férhetnek hozzá a tulajdonosok kezelése hivatkozásra elemek.
Ha a kártyának egy elemet, és nem érhető el a jelenlegi tulajdonos tulajdonosi jogosultságokat, használja a "Jelentés visszaélés" hivatkozásra a gyűjteményben lévő a PowerShell-Galériabeli rendszergazdák eléréséhez.
Azt fogja majd végrehajtásával ellenőrizze a cikk a tulajdonjogát.
Meg kell határozni egy olyan tulajdonost, az elem el, ha rendszer használja a "Tulajdonosok kezelése" hivatkozást a cikkhez ragozott formáival és küldeni a meghívás tulajdonosa lesz.
Műveleteket végezzük el csak ezt követően ellenőrzi, hogy egy olyan tulajdonost kell lennie, és ez a folyamat függ a körülmények között.
Gyakran, az elem projekt URL-cím segítségével tudja lépjen kapcsolatba a projekt tulajdonosa szorosa is használhatunk, Twitter, e-mailek vagy más módon való kapcsolódáshoz a projekt tulajdonosa.