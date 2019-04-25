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
ms.openlocfilehash: 489d8bcdabe904d6a3d2bc6cdb9d7e23d09cbef2
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62075188"
---
# <a name="activity-parameters"></a>Tevékenység-paraméterek

A következő táblázat felsorolja a javasolt nevek és a funkciók a tevékenység-paraméterek.

|Paraméter|Funkció|
|---|---|
|**Hozzáfűzése**<br>Adattípus: SwitchParameter|Ez a paraméter valósítja meg, hogy a felhasználó hozzáadhat tartalmat erőforrás végére Ha paraméter meg van adva.|
|**CaseSensitive**<br>Adattípus: SwitchParameter|Végrehajtja ezt a paramétert, így a felhasználó megkövetelheti a kis-és nagybetűk, ha a paraméter meg van adva.|
|**Command**<br>Adattípus: Sztring|Végrehajtja ezt a paramétert, így a felhasználó is futtatása paranccsal karakterláncot kell megadni.|
|**CompatibleVersion**<br>Adattípus: System.Version objektum|Végrehajtja ezt a paramétert, így a felhasználó megadhatja a szemantika, amely a parancsmag korábbi verzióival való kompatibilitás érdekében kompatibilisnek kell lennie.|
|**tömörítése**<br>Adattípus: SwitchParameter|Ez a paraméter valósítja meg, hogy az adatok tömörítésének használatos, ha a paraméter meg van adva.|
|**tömörítése**<br>Adattípus: Kulcsszó|Ez a paraméter valósítja meg, hogy a felhasználó megadhatja a algoritmus használata az adatok tömörítés.|
|**Folyamatos**<br>Adattípus: SwitchParameter|Ez a paraméter valósítja meg, hogy az adatok feldolgozása mindaddig, amíg a felhasználó leállítja a parancsmag, ha a paraméter meg van adva. Ha a paraméter nincs megadva, a parancsmag egy előre meghatározott mennyiségű adatot dolgoz fel, és ezután befejezi a műveletet.|
|**Létrehozás**<br>Adattípus: SwitchParameter|Ez a paraméter jelzi, hogy egy erőforrás létrejött-e, ha egy még nem létezik a paraméter megadásakor megvalósításához.|
|**Törlés**<br>Adattípus: SwitchParameter|Ez a paraméter valósítja meg, hogy az erőforrások törlődnek, amikor a parancsmag befejezte a műveletet, ha a paraméter meg van adva.|
|**Kiürítési**<br>Adattípus: SwitchParameter|Ez a paraméter jelzi, hogy szálankénti függőben lévő munkaelemek feldolgozása előtt a parancsmag új adatokat dolgoz fel, ha a paraméter meg van adva megvalósításához. Ha a paraméter nincs megadva, a munkaelemek feldolgozása azonnal megtörténik.|
|**Tartalmának végleges törlése**<br>Adattípus: Int32|Ez a paraméter valósítja meg, hogy a felhasználó megadhatja, hogy hányszor erőforrás törölve lesz, mielőtt törölnénk őket.|
|**errorLevel**<br>Adattípus: Int32|Ez a paraméter valósítja meg, hogy a felhasználó megadhatja a jelentés hibák szintjét.|
|**Exclude**<br>Adattípus: String]|Ez a paraméter valósítja meg, hogy a felhasználó lehet kizárni valami tevékenység. A bemeneti szűrők használatával kapcsolatos további információkért lásd: [bemeneti Szűrőparaméterrel](input-filter-parameters.md).|
|**Szűrő**<br>Adattípus: Kulcsszó|Ez a paraméter valósítja meg, hogy a felhasználó megadhatja egy szűrőt, amely az erőforrásokat, amelyen a parancsmag a művelet végrehajtásához. A bemeneti szűrők használatával kapcsolatos további információkért lásd: [bemeneti Szűrőparaméterrel](./input-filter-parameters.md).|
|**Hajtsa végre a**<br>Adattípus: SwitchParameter|Ez a paraméter valósítja meg, hogy a folyamat nyomon követi, ha a paraméter meg van adva.|
|**Kényszerített**<br>Adattípus: SwitchParameter|Ez a paraméter jelzi, hogy a felhasználó egy művelet hajtható végre, akkor is, ha korlátozások vannak észlelt, amikor a paraméter meg van adva megvalósításához. A paraméter nem engedélyezi a biztonsági legyen feltörni. Például ez a paraméter lehetővé teszi, hogy egy felhasználó egy csak olvasható fájl felülírása.|
|**Belefoglalása**<br>Adattípus: String]|Ez a paraméter valósítja meg, hogy a felhasználó belefoglalhatja a hiba egy tevékenységet. A bemeneti szűrők használatával kapcsolatos további információkért lásd: [bemeneti Szűrőparaméterrel](input-filter-parameters.md).|
|**Növekményes**<br>Adattípus: SwitchParameter|Ez a paraméter jelzi, hogy a feldolgozás történik növekményes paraméter megadásakor megvalósításához. Például ez a paraméter lehetővé teszi, hogy a felhasználók, fájlok biztonsági mentése a legutóbbi biztonsági mentés óta csak növekményes biztonsági mentések végrehajtásához.|
|**InputObject**<br>Adattípus: Object|A parancsmag bemenete más parancsmagoknak a megvalósítási ezt a paramétert. Amikor határoz meg egy **InputObject** paramétert, mindig adja meg a **ValueFromPipeline** deklarálásakor kulcsszó a **paraméter** attribútum. A bemeneti szűrők használatával kapcsolatos további információkért lásd: [bemeneti Szűrőparaméterrel](./input-filter-parameters.md).|
|**Beszúrása**<br>Adattípus: SwitchParameter|Ez a paraméter valósítja meg, hogy a parancsmag egy elemet szúr be, ha a paraméter meg van adva.|
|**Interaktív**<br>Adattípus: SwitchParameter|Ez a paraméter valósítja meg, hogy a parancsmag működését interaktív módon a felhasználóval, ha a paraméter meg van adva.|
|**időköz**<br>Adattípus: Kivonattábla|Ez a paraméter valósítja meg, hogy a felhasználó úgy adhat meg a kulcsszavak egy kivonattábla, amely tartalmazza az értékeket. Az alábbi példa bemutatja mintaértékek a **időköz** paraméter: `-interval @{ResumeScan=15; Retry=3}`.|
|**Log**<br>Adattípus: SwitchParameter|Megvalósítási Ez a paraméter naplózási műveletek a parancsmag a paraméter meg van adva.|
|**NoClobber**<br>Adattípus: SwitchParameter|Ez a paraméter valósítja meg, hogy az erőforrás nem írható felül, ha a paraméter meg van adva. Ez a paraméter általában parancsmagok, amelyek felülírják a meglévő objektumok ugyanazzal a névvel megelőzhető, hogy új objektumok létrehozására vonatkozik.|
|**Értesítés**<br>Adattípus: SwitchParameter|Ez a paraméter valósítja meg, hogy a felhasználó értesítést kap, hogy a tevékenység befejeződött, ha a paraméter meg van adva.|
|**NotifyAddress**<br>Adattípus: E-mail cím|Végrehajtja ezt a paramétert, hogy a felhasználó megadhatja azt az e-mail címet, egy értesítés küldéséhez során a **értesítendő** paraméter meg van adva.|
|**Írja felül**<br>Adattípus: SwitchParameter|Ez a paraméter valósítja meg, hogy a parancsmag felülírja a meglévő adatokat, ha a paraméter meg van adva.|
|**Rákérdezés**<br>Adattípus: Sztring|Ez a paraméter valósítja meg, hogy a felhasználó megadhatja a parancsmag egy parancssort.|
|**csendes**<br>Adattípus: SwitchParameter|Ez a paraméter valósítja meg, hogy a parancsmag a műveletek során elrejti felhasználói visszajelzéseket, ha a paraméter meg van adva.|
|**Parancs recurse kapcsolójának**<br>Adattípus: SwitchParameter|Ez a paraméter valósítja meg, hogy a parancsmag rekurzív módon annak műveleteket erőforrásokon hajtja végre, ha a paraméter meg van adva.|
|**Javítás**<br>Adattípus: SwitchParameter|Ez a paraméter valósítja meg, hogy a parancsmag javítása valamit a hibás állapotból, ha a paraméter meg van adva.|
|**RepairString**<br>Adattípus: Sztring|Végrehajtja ezt a paramétert, hogy a felhasználó megadhatja egy karakterláncot szeretne használni, amikor a **javítási** paraméter meg van adva.|
|**Próbálkozzon újra**<br>Adattípus: Int32|Végrehajtja ezt a paramétert, így a felhasználó megadhatja a parancsmag megkísérli a művelet hányszor.|
|**Select**<br>Adattípus: Kulcsszó tömb|Ez a paraméter valósítja meg, hogy a felhasználó megadhatja, milyen típusú elemek tömbjét.|
|**Stream**<br>Adattípus: SwitchParameter|Végrehajtja ezt a paramétert, így a felhasználó streamelheti a folyamat több kimeneti objektumok, ha a paraméter meg van adva.|
|**A szigorú**<br>Adattípus: SwitchParameter|Ez a paraméter valósítja meg, hogy az összes hiba kezelésének megszakító hibaként, amikor a paraméter meg van adva.|
|**TempLocation**<br>Adattípus: Sztring|Hajtja végre ezt a paramétert, így a felhasználó megadhatja a parancsmag a művelet során használt ideiglenes adatokat helyét.|
|**Időtúllépés**<br>Adattípus: Int32|Ez a paraméter valósítja meg, hogy a felhasználó megadhatja az időtúllépési időköz (ezredmásodpercben).|
|**TRUNCATE**<br>Adattípus: SwitchParameter|Ez a paraméter valósítja meg, hogy a parancsmag csonkolja a műveleteket, ha a paraméter meg van adva. Ha a paraméter nincs megadva, a parancsmag egy másik műveletet hajt végre.|
|**Ellenőrizze**<br>Adattípus: SwitchParameter|Ez a paraméter valósítja meg, hogy a parancsmag tesztelni fogja meghatározni, hogy művelet történt-e, ha a paraméter meg van adva.|
|**Wait**<br>Adattípus: SwitchParameter|Ez a paraméter valósítja meg, hogy a parancsmag várakozik a felhasználói bevitelhez, ha a paraméter meg van adva a folytatás előtt.
|**WaitTime**<br>Adattípus: Int32|Végrehajtja ezt a paramétert, hogy a felhasználó megadhatja a időtartama (másodpercben), hogy a felhasználó várakozik a parancsmag bemeneti mikor a **várjon** paraméter meg van adva.|

## <a name="see-also"></a>Lásd még:

[Parancsmag-paraméterek](./cmdlet-parameters.md)

[Egy Windows PowerShell-parancsmag írása](./writing-a-windows-powershell-cmdlet.md)

[Windows PowerShell SDK](../windows-powershell-reference.md)
