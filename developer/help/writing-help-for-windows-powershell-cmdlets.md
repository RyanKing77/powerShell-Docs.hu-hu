---
title: A PowerShell-parancsmagok súgóinak |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 55908d67-7cbe-482a-a105-5a6da93c5311
caps.latest.revision: 4
ms.openlocfilehash: 8d692cf88d1d356886ef973f0989294d6b51ee6d
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56848110"
---
# <a name="writing-help-for-powershell-cmdlets"></a>PowerShell-parancsmagok súgójának írása

PowerShell-parancsmagokkal lehet hasznos, de, kivéve, ha a súgótémakörök egyértelműen ismertetik a parancsmag funkciója, és hogyan kell használni, a parancsmag nem get használja, vagy még rosszabb, akkor előfordulhat, hogy akadályozná felhasználók.
Az XML-alapú parancsmag súgó-fájlformátum fokozza a konzisztencia, de nagyszerű sokkal igényel.

Ha soha nem írt parancsmag súgójában, tekintse át az alábbi útmutatást.
A szükséges ahhoz, hogy a parancsmag súgó-témakörének XML-séma a következő szakaszban leírt.
Kezdje [a parancsmag súgóját fájl létrehozása](./how-to-create-the-cmdlet-help-file.md).
A témakör a felső szintű XML-csomópontnak leírását tartalmazza.

## <a name="writing-guidelines-for-cmdlet-help"></a>A parancsmag súgóját írása irányelvek

### <a name="write-well"></a>Jól írása
Semmi nem váltja fel egy jól megírt témakört.
Ha nem egy professzionális író, író vagy szerkesztő segítségével keresése.
Másik lehetőségként a súgószöveg másolja be a Microsoft Word, és a szintaxis használata, és helyesírás-ellenőrzés ellenőrzi, hogy a munkahelyi javítása.

### <a name="write-simply"></a>Írás egyszerűen
Egyszerű szavak és kifejezések használata.
Kerülje a beszédben.
Vegye figyelembe, hogy sok olvasók felszerelt csak egy idegen nyelvű szótárban, és a Súgó-témakör.

### <a name="write-consistently"></a>Folyamatosan írása
Súgó kapcsolódó parancsmagok (a példában a get-x és a set-x) hasonló lesz.
A standard szintű leírások használata szabványos paraméterek, például **kényszerített** és **InputObject**.
(Másolja be azokat a Súgó a fő parancsmagjainak.) Normál használati használja.
Például használja "paraméter", nem "argumentum", és használja a "parancsmag" nem "parancs" vagy "parancsmagot."

### <a name="start-the-synopsis-with-a-verb"></a>Indítsa el a szinopszist és a egy művelet
A szinopszist mező tájékoztatja a felhasználót, mely a parancsmag nem, mi és működését.
Műveletek hozzon létre egy feladatalapú utasításban, amely tájékoztatja a felhasználókat, ha ez a parancsmag megfelel a követelményeknek.
Használhat egyszerű műveleteket, például a "get", "create" és "módosítása".
Kerülje a "set", amely lehet például a "módosítása" országról és divatos szavakat.

### <a name="focus-on-objects"></a>Összpontosítson az objektumok
A legtöbb "get" parancsmagok megjelenítési hiba, de az elsődleges funkciója, hogy az objektum lekérése.
A segítségre van szüksége dolgozni az objektumot, így a felhasználóknak megérteni, hogy az alapértelmezett megjelenítést egyike legyen, és, hogy használhatják-e a módszerek és a lekért számukra különböző módon objektum tulajdonságait.

### <a name="write-detailed-descriptions"></a>Részletes leírását írása
Röviden listája mindent, ami a parancsmag részletes leírása a végezheti el.
A fő függvényt egy tulajdonság, de a parancsmag az összes tulajdonságait módosíthatja, ha listájában ez a részletes leírása.

### <a name="use-conventional-syntax"></a>A hagyományos szintaxissal
A standard Backus-Naur formátum, amely Windows és UNIX rendszerű parancssori súgó gyakori használja.

### <a name="use-microsoft-net-framework-types-for-parameter-values"></a>A Microsoft .NET-keretrendszer típusok használata paraméterértékek
A helyőrzőket az paramétereket (a szintaxist és a paraméter leírása) a .NET-keretrendszer az objektumtípus, amely elfogadja a paraméter megjelenítése.
A PowerShell csapata az egyezmény bemutatja a .NET-keretrendszer segítségével fejlesztett ki.

### <a name="write-complete-parameter-descriptions"></a>A paraméter teljes leírását írása
Paraméter leírása kell tájékoztatni a felhasználókat két dolgokat: milyen a paraméter nem (a hatás), és mit kell írniuk a paraméterértékeket.

### <a name="write-practical-examples"></a>Gyakorlati példák írása
A példákból kell használata az összes paramétert, de a legfontosabb, hogy a parancsmag használata a való életből vett feladatok megjelenítése.
Kezdje egy egyszerű példa, és egyre összetettebb példák írása.
Az utolsó példában szemléltetik a parancsmag használata egy folyamatban.

### <a name="use-the-notes-field"></a>A megjegyzések mezője használata
Használja a megjegyzések mezője annak magyarázata, hogy felhasználóknak tisztában kell lenniük a parancsmag fogalmakat.
Megjegyzések használatával segítség a felhasználóknak a gyakori hibák elkerülése érdekében.
Kerülje az URL-címek, ahogy változnak.
Ehelyett adja meg a felhasználók használati kereséséhez.

### <a name="test-your-help"></a>A Súgó tesztelése
Tesztelje a Súgó, ugyanúgy, mint a tesztelhetnek.
Barátok és munkatársakkal olvassa el a Súgó tartalma, és visszajelzést.
Akkor is hozzájárulásával hírcsoportokat visszajelzést is.

## <a name="see-also"></a>Lásd még:

 [A parancsmag súgóját fájl létrehozása](./how-to-create-the-cmdlet-help-file.md)

 [A parancsmag neve és a Szinopszist parancsmag Súgó-témakör hozzáadása](./how-to-add-the-cmdlet-name-and-synopsis-to-a-cmdlet-help-topic.md)

 [A részletes leírás egy parancsmag Súgó-témakör hozzáadása](./how-to-add-a-cmdlet-description.md)

 [Szintaxis egy parancsmag Súgó-témakör hozzáadása](./how-to-add-syntax-to-a-cmdlet-help-topic.md)

 [Egy parancsmag súgó-témakörének paraméterek hozzáadása](./how-to-add-parameter-information.md)

 [Bemeneti típusok egy parancsmag Súgó-témakör hozzáadása](./how-to-add-input-types-to-a-cmdlet-help-topic.md)

 [Visszaadott értékeket a parancsmag Súgó-témakör hozzáadása](./how-to-add-return-values-to-a-cmdlet-help-topic.md)

 [Egy parancsmag súgó-témakörének megjegyzések hozzáadása](./how-to-add-notes-to-a-cmdlet-help-topic.md)

 [Példák, a parancsmag Súgó-témakör hozzáadása](./how-to-add-examples-to-a-cmdlet-help-topic.md)

 [Kapcsolódó hivatkozások hozzáadása egy parancsmag Súgó-témakör](./how-to-add-related-links-to-a-cmdlet-help-topic.md)

 [Windows PowerShell SDK](../windows-powershell-reference.md)