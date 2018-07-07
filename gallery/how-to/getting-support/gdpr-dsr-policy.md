---
ms.date: 03/27/2018
contributor: JKeithB
keywords: katalógus, a powershell, a psgallery, GDPR
title: PowerShell-galéria GDPR-megfelelőség
ms.openlocfilehash: 14b82fa07df52f02f0d7577cb0eef70faa4285a2
ms.sourcegitcommit: 8b076ebde7ef971d7465bab834a3c2a32471ef6f
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/06/2018
ms.locfileid: "37893246"
---
# <a name="powershell-gallery-gdpr-compliance"></a>PowerShell-galéria GDPR-megfelelőség

## <a name="overview"></a>Áttekintés

A 2018 május az európai adatvédelmi törvény, az általános adatvédelmi rendelet (GDPR), akkor lép érvénybe.
Az általános adatvédelmi rendelet új szabályokat a vállalatok, kormányzati szerveknek, non-profit és más szervezetek számára, hogy az ajánlat termékek és szolgáltatások, az Európai Unió (EU), vagy hogy a felhasználók adatokat gyűjthet és elemezhet kötött EU-polgárokkal kapcsolatos ír elő.
Az általános adatvédelmi rendelet vonatkozik, bárhol is található.

> [!NOTE]
> Ez a cikk ismerteti a személyes adatok törlése a PowerShell-galériából, és támogatja a GDPR szerint Ön nem használható. Ha az általános adatvédelmi rendelet kapcsolatos általános információkat keres, tekintse meg a [GDPR szakaszában a szolgáltatás Szolgáltatásmegbízhatósági portálon](https://servicetrust.microsoft.com/ViewPage/GDPRGetStarted).

## <a name="personally-identifiable-data"></a>Személyes azonosításra alkalmas adatok

A PowerShell-galériából a következő adatokat, a felhasználók, amelyek személyes adatokat tartalmazhatnak biztosított tárolja:

- PowerShell-Galériabeli fiók
- A PowerShell-galériában közzétett cikkek
- A PowerShell-galériából csapat váltott e-mailben

A legtöbb felhasználó ne hozzon létre egy PowerShell-Galériabeli fiók.
Egy fiók nem kötelező, kivéve, ha szeretné tegyen közzé egy elemet, vagy az "Ügyfél Owner" szolgáltatás használata a PowerShell-galériában.
E-mailek levelezés, a felhasználó által kezdeményezett, nem a PowerShell-galériában nem tárolja a személyes azonosításra alkalmas adatokat a felhasználók számára, akik nem hozott létre egy fiókot.

Felhasználók, akik egy PowerShell-Galériabeli fiók létrehozása a PowerShell-galériából elemek tehetnek közzé.
Azok az elemek várhatóan PowerShell-kódot, de egyéb információkat, ideértve a személyes adatokat is tartalmazhat.
Az alábbi információk jelennek meg, hogyan kezdheti az összes elem a PowerShell-galériából történő közzétételét.

## <a name="dsr-export-of-powershell-gallery-data"></a>PowerShell-galériából adatok DSR exportálása

A következő szakaszok ismertetik a PowerShell-galériából hogyan támogatja az adattulajdonosi kérelmek (DSR), a PowerShell-galériából a tárolt adatok exportálása és törlése, ez az információ kérésének elmagyarázza.

### <a name="email"></a>E-mail

E-mailek levelezést tartalmazhatja a következő:

- Elemek, ha megvizsgálja a kód elemzés észlelt egy tetszőleges elemre a PowerShell-galériában közzétett problémáját PowerShell-galériából tulajdonosainak küldött e-mail
- A PowerShell-galériából csapat az e-mail-cím használatával "a kapcsolatfelvétel" lapon a bárki által küldött e-mail [cgadmin@microsoft.com](mailto:cgadmin@microsoft.com)
- Regisztrált felhasználó, aki a PowerShell-galériából a "Forduljon Owner" szolgáltatás segítségével a PowerShell-galériából elemeire tulajdonosának e-mail küldése

Által vagy a PowerShell-galériában elküldött e-mailek 90 napos adatmegőrzési már támogatja a lehetséges biztonsági vizsgálatok kártevő kódja észleli a PowerShell-galériából.
E-mailek házirend 90 nap után törlődnek.

Minden e-mailek küldése az előző 90 napon belül, vagy az e-mail-címét és a PowerShell-galériából példányait kérheti.
Kérelem ezt a levelezését, küldjön egy e-mailek [ cgadmin@microsoft.com ](mailto:cgadmin@microsoft.com), és a cím: "Vonatkozó DSR-kérelmek ebbe a fiókba vonatkozó e-mailek".
Az üzenet törzsében, adja meg a kért információk (például:. küldje el a minden e-mailek küldött vagy erre a címre érkezett.) Használata esetén az e-mail-címét a kérelem számított 90 napon belül minden e-maileket küld üzleti 7 napon belül.

### <a name="powershell-gallery-account-information"></a>PowerShell-Galériabeli fiók adatait

Ha létrehozott egy PowerShell-Galériabeli fiók, annak az alábbi lépések megtételével a PowerShell-katalógusban tárolt személyes adatokat:

1. Jelentkezzen be a PowerShell-galériából, majd kattintson a felhasználónevére
2. A következő oldal jelenik meg a fiók oldal, amely megjeleníti a PowerShell-Galériabeli fiók használt e-mail-cím

Ha egynél több fiók található a PowerShell-galériából létrehozott, szüksége lesz a ismételje meg ezeket a lépéseket az egyes fiókok számára.

### <a name="items-in-the-powershell-gallery"></a>A PowerShell-galériából elemek

Megkönnyítése érdekében a PowerShell-galériában közzétett exportáló elemek, a Microsoft közzétette a parancsfájl "GetPSGalleryItemsForAuthor" a PowerShell-galériában.
Ez a szkript egy példányát minden eleméhez, a PowerShell-galériából, az elemben tárolt Szerző információk alapján üzembe minden egyes verziója exportálja.

> [!NOTE]
> A cikk közzétételekor a szerző az elemek jegyzéke tárolja.
> Nincs garancia arra, hogy a szerző stejnou identitou jako a PowerShell-galériából a használt fióknak-e.
> Ha más értéket az Author mező használata esetén kell adnia ezt az értéket, amikor ez a szkript használatával.

A szkript a következő PowerShell-parancs segítségével töltheti le:

```powershell
Save-Script Get-repository psgallery
```

A parancsfájl közvetlenül, majd futtassa a következő PowerShell-parancsok futtatásával:

```powershell
# cd <local folder location>
.\GetPSGalleryItemsForAuthor.ps1
```

A rendszer felkéri adja meg a szerző és a egy mappát a rendszer, ha azt szeretné, hogy a menteni kívánt elemeket.

## <a name="deleting-personal-data-from-the-powershell-gallery"></a>Személyes adatok törlése a PowerShell-galériából

A PowerShell-Galériabeli fiók vagy a PowerShell-galériából szereplő bármely elem törléséhez e-mailben cgadmin@microsoft.com nevű: "A GDPR-kérelmet ehhez a fiókhoz kapcsolódó elemek".
Az üzenet törzsében milyen információkat szeretne törölt állapotba. Például:

- Törölje a verzió x.y.z saját elem (elem name)
- Törölje az összes verzióját a saját item (elem name)
- Törölje a saját PowerShell-Galériabeli fiók

A PowerShell-galériából rendszergazdák 7 munkanapon belül választ fog kapni.
A megadott elemek törlődni fognak a kérés elküldése után 30 napon belül.