---
title: Tevékenység-paraméterek |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 6e4e0cf6-19e0-44b8-8b40-d6f6075276cf
caps.latest.revision: 5
ms.openlocfilehash: 32e2b8acf33bc733c5e4cab94a721076ff46225d
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56849090"
---
# <a name="activity-parameters"></a>Tevékenység-paraméterek

A következő táblázat felsorolja a javasolt nevek és a funkciók a tevékenység-paraméterek.

Hozzáfűzés adattípus: SwitchParameter

Ez a paraméter valósítja meg, hogy a felhasználó hozzáadhat tartalmat erőforrás végére Ha paraméter meg van adva.

CaseSensitive adattípus: SwitchParameter

Végrehajtja ezt a paramétert, így a felhasználó megkövetelheti a kis-és nagybetűk, ha a paraméter meg van adva.

A parancs adattípus: Sztring

Végrehajtja ezt a paramétert, így a felhasználó is futtatása paranccsal karakterláncot kell megadni.

CompatibleVersion adattípus: System.Version objektum

Végrehajtja ezt a paramétert, így a felhasználó megadhatja a szemantika, amely a parancsmag korábbi verzióival való kompatibilitás érdekében kompatibilisnek kell lennie.

Tömörítés adattípus: SwitchParameter

Ez a paraméter valósítja meg, hogy az adatok tömörítésének használatos, ha a paraméter meg van adva.

Tömörítés adattípus: Kulcsszó

Ez a paraméter valósítja meg, hogy a felhasználó megadhatja a algoritmus használata az adatok tömörítés.

Folyamatos adattípus: SwitchParameter

Ez a paraméter valósítja meg, hogy az adatok feldolgozása mindaddig, amíg a felhasználó leállítja a parancsmag, ha a paraméter meg van adva. Ha a paraméter nincs megadva, a parancsmag egy előre meghatározott mennyiségű adatot dolgoz fel, és ezután befejezi a műveletet.

Hozzon létre adattípus: SwitchParameter

Ez a paraméter jelzi, hogy egy erőforrás létrejött-e, ha egy még nem létezik a paraméter megadásakor megvalósításához.

Törölje az adattípus: SwitchParameter

Ez a paraméter valósítja meg, hogy az erőforrások törlődnek, amikor a parancsmag befejezte a műveletet, ha a paraméter meg van adva.

Kiürítési adattípus: SwitchParameter

Ez a paraméter jelzi, hogy szálankénti függőben lévő munkaelemek feldolgozása előtt a parancsmag új adatokat dolgoz fel, ha a paraméter meg van adva megvalósításához. Ha a paraméter nincs megadva, a munkaelemek feldolgozása azonnal megtörténik.

Adattípus törlése: Int32

Ez a paraméter valósítja meg, hogy a felhasználó megadhatja, hogy hányszor erőforrás törölve lesz, mielőtt törölnénk őket.

ErrorLevel adattípus: Int32

Ez a paraméter valósítja meg, hogy a felhasználó megadhatja a jelentés hibák szintjét.

Adattípus kizárása: String]

Ez a paraméter valósítja meg, hogy a felhasználó lehet kizárni valami tevékenység. A bemeneti szűrők használatával kapcsolatos további információkért lásd: [bemeneti Szűrőparaméterrel](./input-filter-parameters.md).

Szűrés adattípus: Kulcsszó

Ez a paraméter valósítja meg, hogy a felhasználó megadhatja egy szűrőt, amely az erőforrásokat, amelyen a parancsmag a művelet végrehajtásához. A bemeneti szűrők használatával kapcsolatos további információkért lásd: [bemeneti Szűrőparaméterrel](./input-filter-parameters.md).

Hajtsa végre az adatok típusa: SwitchParameter

Ez a paraméter valósítja meg, hogy a folyamat nyomon követi, ha a paraméter meg van adva.

Kényszerített adattípus: SwitchParameter

Ez a paraméter jelzi, hogy a felhasználó egy művelet hajtható végre, akkor is, ha korlátozások vannak észlelt, amikor a paraméter meg van adva megvalósításához. A paraméter nem engedélyezi a biztonsági legyen feltörni. Például ez a paraméter lehetővé teszi, hogy egy felhasználó egy csak olvasható fájl felülírása.

Adatok típusa a következők: String]

Ez a paraméter valósítja meg, hogy a felhasználó belefoglalhatja a hiba egy tevékenységet. A bemeneti szűrők használatával kapcsolatos további információkért lásd: [bemeneti Szűrőparaméterrel](./input-filter-parameters.md).

A növekményes adatok típusa: SwitchParameter

Ez a paraméter jelzi, hogy a feldolgozás történik növekményes paraméter megadásakor megvalósításához. Például ez a paraméter lehetővé teszi, hogy a felhasználók, fájlok biztonsági mentése a legutóbbi biztonsági mentés óta csak növekményes biztonsági mentések végrehajtásához.

InputObject adattípus: Objektum

A parancsmag bemenete más parancsmagoknak a megvalósítási ezt a paramétert. Amikor határoz meg egy `InputObject` paramétert, mindig adja meg a `ValueFromPipeline` deklarálásakor kulcsszó a **paraméter** attribútum. A bemeneti szűrők használatával kapcsolatos további információkért lásd: [bemeneti Szűrőparaméterrel](./input-filter-parameters.md).

Illessze be az adat típusa: SwitchParameter

Ez a paraméter valósítja meg, hogy a parancsmag egy elemet szúr be, ha a paraméter meg van adva.

Interaktív adatok típusa: SwitchParameter

Ez a paraméter valósítja meg, hogy a parancsmag működését interaktív módon a felhasználóval, ha a paraméter meg van adva.

Intervallum adattípus: Kivonattábla

Ez a paraméter valósítja meg, hogy a felhasználó úgy adhat meg a kulcsszavak egy kivonattábla, amely tartalmazza az értékeket. Az alábbi példa bemutatja mintaértékek a `Interval` paraméter: `-interval @{ResumeScan=15; Retry=3}`.

Jelentkezzen be az adat típusa: SwitchParameter

Megvalósítási Ez a paraméter naplózási műveletek a parancsmag a paraméter meg van adva.

NoClobber adattípus: SwitchParameter

Ez a paraméter valósítja meg, hogy az erőforrás nem írható felül, ha a paraméter meg van adva. Ez a paraméter általában parancsmagok, amelyek felülírják a meglévő objektumok ugyanazzal a névvel megelőzhető, hogy új objektumok létrehozására vonatkozik.

Értesítés adattípus: SwitchParameter

Ez a paraméter valósítja meg, hogy a felhasználó értesítést kap, hogy a tevékenység befejeződött, ha a paraméter meg van adva.

NotifyAddress adattípus: E-mail cím

Végrehajtja ezt a paramétert, hogy a felhasználó megadhatja azt az e-mail címet, egy értesítés küldéséhez során a `Notify` paraméter meg van adva.

Felülírás adattípus: SwitchParameter

Ez a paraméter valósítja meg, hogy a parancsmag felülírja a meglévő adatokat, ha a paraméter meg van adva.

Rákérdezés adattípus: Sztring

Ez a paraméter valósítja meg, hogy a felhasználó megadhatja a parancsmag egy parancssort.

Csendes adattípus: SwitchParameter

Ez a paraméter valósítja meg, hogy a parancsmag a műveletek során elrejti felhasználói visszajelzéseket, ha a paraméter meg van adva.

Recurse adattípus: SwitchParameter

Ez a paraméter valósítja meg, hogy a parancsmag rekurzív módon annak műveleteket erőforrásokon hajtja végre, ha a paraméter meg van adva.

Írja be a javítási adatok: SwitchParameter

Ez a paraméter valósítja meg, hogy a parancsmag javítása valamit a hibás állapotból, ha a paraméter meg van adva.

RepairString adattípus: Sztring

Végrehajtja ezt a paramétert, hogy a felhasználó megadhatja egy karakterláncot szeretne használni, amikor a `Repair` paraméter meg van adva.

Ismételje meg az adattípus: Int32

Végrehajtja ezt a paramétert, így a felhasználó megadhatja a parancsmag megkísérli a művelet hányszor.

Adatok típusának kiválasztása: Kulcsszó tömb

Ez a paraméter valósítja meg, hogy a felhasználó megadhatja, milyen típusú elemek tömbjét.

Stream-adattípus: SwitchParameter

Végrehajtja ezt a paramétert, így a felhasználó streamelheti a folyamat több kimeneti objektumok, ha a paraméter meg van adva.

A szigorú adattípus: SwitchParameter

Ez a paraméter valósítja meg, hogy az összes hiba kezelésének megszakító hibaként, amikor a paraméter meg van adva.

TempLocation adattípus: Sztring

Hajtja végre ezt a paramétert, így a felhasználó megadhatja a parancsmag a művelet során használt ideiglenes adatokat helyét.

Időtúllépés adattípus: Int32

Ez a paraméter valósítja meg, hogy a felhasználó megadhatja az időtúllépési időköz (ezredmásodpercben).

TRUNCATE adattípus: SwitchParameter

Ez a paraméter valósítja meg, hogy a parancsmag csonkolja a műveleteket, ha a paraméter meg van adva. Ha a paraméter nincs megadva, a parancsmag egy másik műveletet hajt végre.

Ellenőrizze az adatok típusát: SwitchParameter

Ez a paraméter valósítja meg, hogy a parancsmag tesztelni fogja meghatározni, hogy művelet történt-e, ha a paraméter meg van adva.

Várjon, adattípus: SwitchParameter

Ez a paraméter valósítja meg, hogy a parancsmag várakozik a felhasználói bevitelhez, ha a paraméter meg van adva a folytatás előtt.

Várakozási idő adattípus: Int32

Végrehajtja ezt a paramétert, hogy a felhasználó megadhatja a időtartama (másodpercben), hogy a felhasználó várakozik a parancsmag bemeneti mikor a `Wait` paraméter meg van adva.

## <a name="see-also"></a>Lásd még:

[Parancsmag-paraméterek](./cmdlet-parameters.md)

[Egy Windows PowerShell-parancsmag írása](./writing-a-windows-powershell-cmdlet.md)

[Windows PowerShell SDK](../windows-powershell-reference.md)
