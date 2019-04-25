---
ms.date: 06/12/2017
contributor: JKeithB
keywords: katalógus, a powershell, a parancsmag, a psgallery
title: Csomag tulajdonosainak kezelése
ms.openlocfilehash: 5cf26a7195ac446177cbb7f3a055e8e0a78569cc
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62084147"
---
# <a name="managing-package-owners"></a>Csomag tulajdonosainak kezelése

A PowerShell-galériából a csomag tulajdonjogát ki a csomagot a katalógusban közzétett határozzák meg.
Egyes esetekben a metaadatok kell kezelni a kezdeti csomag közzétételét, ami azt jelenti, hogy a tulajdonos metaadatok kell lennie módosítható, bár a csomagba nem túl.

Minden csomag olyan társakhoz.
Ez azt jelenti, hogy minden olyan csomag tulajdonosával teheti közzé a csomag új verziójának. Azt is jelenti, hogy minden olyan csomag tulajdonosa távolíthatja el bármilyen egyéb csomag tulajdonosával.
Nincs tulajdonosa, mint a más tulajdonosok több szolgáltató nem.

## <a name="setting-a-packages-initial-owner"></a>A csomag kezdeti tulajdonos beállítása

Ha a PowerShell-galériában közzétett új csomagot, a felhasználót, hogy a csomag közzétett határozza meg a kezdeti tulajdonos. Ez határozza meg, amelynek API key használták a Publish-Module parancsmaggal.

## <a name="adding-owners"></a>Tulajdonosok hozzáadása

Ha egy csomag közzé lett téve a PowerShell-galériából, könnyebbé vált a csomag tulajdonosai lesznek további felhasználókat meghívni.

1. [Jelentkezzen be](https://powershellgallery.com/users/account/LogOn) azzal a fiókkal, a tulajdonos csomagot, a PowerShell-galériában.
2. Keresse meg a csomag lapon használja az "Items" lapon, a Keresés vagy kattintson a felhasználónevére, majd [ **My-csomagok kezelése**](https://www.powershellgallery.com/account/Packages).
3. Amikor bejelentkezett egy csomagot tulajdonosként, tulajdonosok kezelése kapcsolat van, kattintson a bal oldalon.
4. Adja meg a tulajdonosként hozzáadni, és kattintson a "Hozzáadás" személy felhasználóneve.
5. E-mailt az új társtulajdonos, majd küldeni a meghívással csomag tulajdonosává válik.
6. Miután, hogy a felhasználó a hivatkozásra kattint, azok teljes társtulajdonos, teljes körűen felügyelve egy csomagot, beleértve a más felhasználók tulajdonosként való eltávolítása.

**MEGJEGYZÉS:**: Mindaddig, amíg az új tulajdonos megerősíti, hogy tulajdonjoga, azok *nem lesz* csomag tulajdonosának helyrendszerként legyen felsorolva.
Megtekintésekor a **tulajdonosainak kezelése** oldalon, a jelenlegi tulajdonos a "jóváhagyásra" bejegyzést fog látni.
A meghívó távolíthatja el; ugyanúgy, mint a más tulajdonosok távolíthatja el.
Ez a folyamat a Meghívók meggátolja, hogy a felhasználókat a tévesen tulajdonosaihoz csomagjaikat, a más felhasználók hozzáadásakor.

Vegye figyelembe, hogy a "Szerző" metaadatok tisztán szabadkézi szöveges; csak a "tulajdonos" szabályozza.


## <a name="removing-owners"></a>Tulajdonos eltávolítása

Ha egy csomag több tulajdonosok rendelkezik, és egyet ki kell vonni, a folyamat egyszerű:

1. [Jelentkezzen be](https://powershellgallery.com/users/account/LogOn) azzal a fiókkal, a csomag; tulajdonos PowerShell-galériában
2. Nyissa meg a csomag lapot csomagok lapján, a keresés, vagy kattintson a felhasználónevére, majd [ **My-csomagok kezelése**](https://www.powershellgallery.com/account/Packages).
3. Ha be van jelentkezve, a csomag tulajdonosával, tulajdonosok kezelése kapcsolat van; kattintson a bal oldalon
4. Kattintson a "remove" hivatkozást, el kell távolítani a tulajdonos mellett.



## <a name="transferring-package-ownership"></a>Csomag átruházása

Támogatási kérések tulajdonjogának csomag egy felhasználó egy másikra néha kapunk, de szinte mindig elvégezheti ezt Ön.
Egyszerűen csak a fenti két szolgáltatás kombinációja tulajdonjog visz át egy felhasználó egy másik.

1. A jelenlegi tulajdonos meghívót küld a társtulajdonos válik az új felhasználót, és az új felhasználó elfogadja a meghívást;
2. Az új felhasználót a régi felhasználói távolít el, a tulajdonosok listája.

Ezt a kérést néhány űrlapok alatt érkezett, de a folyamat ugyanúgy működik.

- A csomag tulajdonjogát módosul az egyik fejlesztő egy másikba
- A csomag véletlenül közzé lett téve a megfelelő fiók használatával


## <a name="orphaned-packages"></a>Árva csomagok

Egy legutóbbi forgatókönyv történt, de nem több alkalommal.
Csomagok sp_createorphan váltak, és az egyetlen csomag tulajdonosi fiók nem használható új tulajdonosok hozzáadása.
Íme néhány példa az ebben a forgatókönyvben:

- A tulajdonos fiókja már nem létezik olyan e-mail-címmel társított, és a felhasználó elfelejtette a jelszavát
- A regisztrált felhasználó elhagyta a vállalatot, amely a csomag nem érhető el a csomag tulajdonjogát frissítése
- Csak hatással vannak a csomagok milliós egy hiba miatt a csomag nincs valamilyen módon ownerless a katalógusban

A PowerShell-galéria rendszergazdák férhetnek hozzá a tulajdonosok kezelése hivatkozásra bármelyik csomag.
Ha egy csomagot a jogos tulajdonosa, és nem érhető el a jelenlegi tulajdonos a tulajdonjog jogosultságokat, majd használja a visszaélés jelentése hivatkozást a katalógusban a PowerShell-galéria rendszergazdák eléréséhez.
Ezután követjük egy folyamatot, hogy a csomag tulajdonosának ellenőrzését.
Ha azt állapítja meg, hogy a csomag tulajdonosának kell látnia, hogy lesz használja tulajdonosainak kezelése hivatkozást a csomag magunkat és tulajdonosa lesz a meghívót küldünk.
Csak tesszük ez Miután ellenőrizte, hogy egy olyan tulajdonost kell, és ez a folyamat eltérő körülmények között.
Gyakran, forduljon a projekt tulajdonosa megtalálni a csomag projekt URL-címet használjuk, de még a használjuk, Twitter, e-mailben vagy más módon vegye fel a kapcsolatot a projekt tulajdonosa.
