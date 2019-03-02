---
title: Az erőforrás-paraméterek |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 460c43aa-f5c5-4a1a-a6f2-5e07db143de1
caps.latest.revision: 5
ms.openlocfilehash: 9752570e5c997ef4da56a08df14f39b77ba37a4a
ms.sourcegitcommit: ce46e5098786e19d521b4bf948ff62d2b90bc53e
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/02/2019
ms.locfileid: "57251200"
---
# <a name="resource-parameters"></a>Erőforrás-paraméterek

Az alábbi táblázat felsorolja a javasolt nevek és erőforrás-paraméterek funkciót. Ezeket a paramétereket az erőforrások lehet a szerelvényt, amely tartalmazza a parancsmag osztály vagy, amelyek a parancsmagot a gazdaalkalmazást.

|Paraméter|Funkció|
|---|---|
|**Alkalmazás**<br>Adattípus: Sztring|Ez a paraméter valósítja meg, hogy a felhasználó egy alkalmazást adhat meg.|
|**Sestavení**<br>Adattípus: Sztring|Ez a paraméter valósítja meg, hogy a felhasználó megadhatja a szerelvényt.|
|**Attribútum**<br>Adattípus: Sztring|Ez a paraméter valósítja meg, hogy a felhasználó megadhatja egy attribútumot.|
|**Osztály**<br>Adattípus: Sztring|Ez a paraméter valósítja meg, hogy a felhasználó megadhatja a Microsoft .NET-keretrendszer osztály.|
|**Fürt**<br>Adattípus: Sztring|Ez a paraméter valósítja meg, hogy a felhasználó megadhatja a fürt.|
|**kulturális környezet**<br>Adattípus: Sztring|Ez a paraméter valósítja meg, hogy a felhasználó megadhatja a kulturális környezet, amelyben a parancsmag futtatásához.|
|**Tartomány**<br>Adattípus: Sztring|Ez a paraméter valósítja meg, hogy a felhasználó megadhatja a tartomány nevét.|
|**Drive**<br>Adattípus: Sztring|Ez a paraméter valósítja meg, hogy a felhasználó megadhatja a meghajtó neve.|
|**Event**<br>Adattípus: Sztring|Ez a paraméter valósítja meg, hogy a felhasználó megadhatja az esemény nevét.|
|**Kapcsolat**<br>Adattípus: Sztring|Ez a paraméter valósítja meg, hogy a felhasználó megadhatja a hálózati adapter neve.|
|**IpAddress**<br>Adattípus: Sztring|Ez a paraméter valósítja meg, hogy a felhasználó úgy adhat meg az IP-címet.|
|**Feladat**<br>Adattípus: Sztring|Ez a paraméter valósítja meg, hogy a felhasználó megadhatja a feladatot.|
|**LiteralPath**<br>Adattípus: Sztring|Ez a paraméter valósítja meg, hogy a felhasználó megadhatja a erőforrás elérési útja, ha a helyettesítő karakterek használata nem támogatott. (Használja a **elérési út** paramétert, ha a helyettesítő karakterek használata támogatott.)|
|**Mac**<br>Adattípus: Sztring|Ez a paraméter valósítja meg, hogy a felhasználó megadhatja a tartományvezérlő (MAC) cím.|
|**ParentId**<br>Adattípus: Sztring|Ez a paraméter valósítja meg, hogy a felhasználó megadhatja a szülő azonosítója.|
|**Path**<br>Adattípus: Karakterlánc, karakterlánc]|Ez a paraméter valósítja meg, hogy a felhasználó jelezheti az erőforrás elérési útja, ha a helyettesítő karakterek használata támogatott. (Használja a **LiteralPath** paramétert, ha helyettesítő karakterek használata nem támogatott.) Azt javasoljuk, hogy a teljes támogatja ezt a paramétert fejleszteni `provider:path` szolgáltatók által használt szintaxis. Azt javasoljuk, hogy fejleszt, így a lehető legtöbb szolgáltatók működik.|
|**Port**<br>Adattípus: Egész szám, karakterlánc|Ez a paraméter valósítja meg, hogy a felhasználó úgy adhat meg, a hálózatkezeléshez egész szám vagy egy olyan karakterláncértéket, például a port egyéb "biztalk".|
|**Printer**<br>Adattípus: Egész szám, karakterlánc|Ez a paraméter valósítja meg, hogy a felhasználó megadhatja a nyomtatót, a parancsmag használatához.|
|**Méret**<br>Adattípus: Int32|Ez a paraméter valósítja meg, hogy a felhasználó megadhatja a méretét.|
|**TID**<br>Adattípus: Sztring|Ez a paraméter valósítja meg, hogy a felhasználó megadhatja a parancsmag egy tranzakció azonosítója (TID).|
|**Típus**<br>Adattípus: Sztring|Ez a paraméter valósítja meg, hogy a felhasználó megadhatja a kívánt erőforrás típusát.|
|**URL-cím**<br>Adattípus: Sztring|Ez a paraméter valósítja meg, hogy a felhasználó megadhatja egy egységes erőforrás-lokátor (URL).|
|**Felhasználó**<br>Adattípus: Sztring|Ez a paraméter valósítja meg, hogy a felhasználó megadhatja a saját nevét, vagy egy másik felhasználó nevét.|

## <a name="see-also"></a>Lásd még:

[Parancsmag-paraméterek](./cmdlet-parameters.md)

[Egy Windows PowerShell-parancsmag írása](./writing-a-windows-powershell-cmdlet.md)

[Windows PowerShell SDK](../windows-powershell-reference.md)
