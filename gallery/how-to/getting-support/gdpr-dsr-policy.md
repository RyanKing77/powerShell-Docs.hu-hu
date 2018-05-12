---
ms.date: 03/27/2018
contributor: JKeithB
ms.topic: conceptual
keywords: gyűjtemény, a powershell, a psgallery, GDPR
title: PowerShell-Galériabeli GDPR megfelelőségi
ms.openlocfilehash: 0a9e76325a2a5cf8f509e1a6317c8ed88d133f1d
ms.sourcegitcommit: e9ad4d85fd7eb72fb5bc37f6ca3ae1282ae3c6d7
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/10/2018
---
# <a name="powershell-gallery-gdpr-compliance"></a>PowerShell-Galériabeli GDPR megfelelőségi

## <a name="overview"></a>Áttekintés

Előfordulhat, hogy 2018, az európai adatvédelmi törvény, az általános adatok védelmi szabályozás (GDPR), akkor lép érvénybe.
A GDPR támaszt a vállalatok, állami intézményekhez, nem nyereség és más szervezetekkel, hogy az ajánlat termékek és szolgáltatások vállalatoknál az Európai Unió, vagy ha az adatgyűjtés és -elemzés EU lakosai kötve új szabályokat.
A GDPR elhelyezkedő függetlenül érvényes.

> [!NOTE]
> Ez a cikk ismerteti a személyes adatok törlése a PowerShell-galériából lépéseit, és támogatja a GDPR a kötelezettségeit használható. Ha további általános információt GDPR van szüksége, tekintse meg a [GDPR szakasz a szolgáltatás megbízható portál](https://servicetrust.microsoft.com/ViewPage/GDPRGetStarted).

## <a name="personally-identifiable-data"></a>Személyes azonosításra alkalmas adatok

A PowerShell-galériában tárolja a felhasználók, amelyek tartalmazhatnak személyes adatokat is megadható a következő információkat:

* PowerShell-galériában fiók
* A PowerShell-galériában közzétett cikkek
* E-mailek levelezés, a PowerShell-galériában csoporttal

A legtöbb felhasználó ne hozzon létre egy PowerShell-galériában fiókot.
Egy fiók nincs szükség, kivéve, ha egy elem közzététele, vagy az "Ügyfél Owner" szolgáltatás használata a PowerShell-galériában fog.
Eltérő e-mail levelezés, a felhasználó által kezdeményezett a PowerShell-galériában nem tárolja a felhasználókra, akik nem hozott létre egy fiókot a személyazonosításra alkalmas adatokat.

Felhasználók, akik egy PowerShell-galériában-fiók létrehozása a PowerShell-galériában közzéteheti elemeket.
Ezen elemekre kellene lennie a PowerShell-kódot, de más információkat, ideértve a személyes adatokat is tartalmazhat.
Az alábbi információ jelenik meg, hogyan férhetnek elemeinek a PowerShell-galériában közzétett.

## <a name="dsr-export-of-powershell-gallery-data"></a>PowerShell-galériában adatok DSR exportálása

Az alábbi szakaszok azt ismertetik, hogyan a PowerShell-galériában támogatja tulajdonos kérelmek (DSR), azzal, hogy ismerteti a PowerShell-dokumentumtárban tárolt adatok exportálása és arról, hogyan kérhet az adatok törlése.

### <a name="email"></a>E-mail

E-mailek levelezés tartalmazhatja a következő:

* A PowerShell-galériában elemek, ha a kód elemző ellenőrzi bármely a PowerShell-galériában a közzétett cikk problémát észlelt a tulajdonosainak küldött e-mail
* Az e-mail cím használata "a kapcsolatfelvétel" lapon a PowerShell-galériában csoporthoz bárki által küldött e-mailek (cgadmin@microsoft.com)
* Regisztrált felhasználók, akik a PowerShell-galériában az "Ügyfél Owner" szolgáltatás segítségével e-mail küldéséhez a tulajdonos elem a PowerShell-galériában

Vagy a PowerShell-galériában által küldött e-mailek 90 napos adatmegőrzési már támogatja a lehetséges biztonsági vizsgálatok kártékony kódot észleli a PowerShell-galériában a.
E-mailek házirend 90 nap után törlődnek.

Másolja az összes e-mailek küldése az előző 90 napon belül, vagy az e-mail címét és a PowerShell-galériában kérheti.
E-mail küldése a levelezést kérelmezéséhez cgadmin@microsoft.com, és a cím: "Az e-mailekhez, ez a fiók vonatkozó DSR kérelem".
Az üzenet törzsében, állapot: a kért információkról (például: küldje el az összes e-mailek küldött és fogadott ezt az e-mail címet a.) Használata esetén az e-mail címet a kérelem 90 napon belül minden e-maileket küld 7 munkanapon belül.

### <a name="powershell-gallery-account-information"></a>PowerShell-galériában fiókadatok

Ha létrehozott egy PowerShell-galériában fiókot, az alábbi lépések megtételével a PowerShell-dokumentumtárban tárolt összes személyes információt találja meg:

1. Jelentkezzen be a PowerShell-galériában, majd kattintson a felhasználónevére
2. A következő oldal jelenik meg a fiók lapon, amely bemutatja az e-mail cím, a PowerShell-galériában fiókhoz használt

Ha egynél több fiók a PowerShell-galériában hozott létre, akkor ismételje meg ezeket a lépéseket az egyes fiókok számára.

### <a name="items-in-the-powershell-gallery"></a>A PowerShell-galériában szereplő elemek

Lehetővé teszi közzé a PowerShell-galériában exportáló elemek, azt hogy tette közzé a parancsfájl "GetPSGalleryItemsForAuthor" a PowerShell-galériában.
Ez a parancsfájl egy példányát minden elem kerüljenek a PowerShell-galériában elemben tárolt Szerző információk alapján a minden verziója exportálja.

> [!NOTE]
> A cikk közzétételekor a szerző tárolja a cikk jegyzékfájlt.
> Nincs nem garantálja, hogy a szerző identitása megegyezik a PowerShell-galériában használt fióknak-e.
> Ha más értéket használja az Author mező, szüksége lesz a adja meg ezt az értéket, ha a parancsfájl.

A parancsfájl a következő PowerShell-parancs segítségével töltheti le:

```powershell
Save-Script GetPSGalleryItemsForAuthor -path <local folder location> -repository psgallery
```

A parancsfájl közvetlenül, majd futtassa a következő PowerShell-parancsok futtatásával:

```powershell
cd <local folder location >
.\GetPSGalleryItemsForAuthor.ps1
```

Adja meg a szerző és a rendszer egy mappát, ahová menteni elemek kéri.

## <a name="deleting-personal-data-from-the-powershell-gallery"></a>Személyes adatok törlése a PowerShell-galériából

E-mail küldése a PowerShell-galériában fiók vagy a PowerShell-galériában saját elemek törléséhez cgadmin@microsoft.com és a cím: "GDPR kérelem ezzel a fiókkal kapcsolatos elemek".
Az üzenet törzsében milyen információkat szeretne törölt állapotban. Például:

* Törölje a cikk "elem neve" verzió x.y.z
* Törölje a "name elem" elem összes verziója
* Törölje a PowerShell-galériában fiókomat

A PowerShell-galériában rendszergazdák 7 munkanapon belül válaszol.
A megadott elemek törlődni fognak a kérelem után 30 napon belül.
