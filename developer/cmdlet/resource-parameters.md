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
ms.openlocfilehash: f58e8ecb67238939e90d4c5650bddd03da3c9409
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56851750"
---
# <a name="resource-parameters"></a>Erőforrás-paraméterek

Az alábbi táblázat felsorolja a javasolt nevek és erőforrás-paraméterek funkciót. Ezeket a paramétereket az erőforrások lehet a szerelvényt, amely tartalmazza a parancsmag osztály vagy, amelyek a parancsmagot a gazdaalkalmazást.

Alkalmazás-adattípus: Sztring

Ez a paraméter valósítja meg, hogy a felhasználó egy alkalmazást adhat meg.

Szerelvény adattípus: Sztring

Ez a paraméter valósítja meg, hogy a felhasználó megadhatja a szerelvényt.

Az attribútum adattípusát: Sztring

Ez a paraméter valósítja meg, hogy a felhasználó megadhatja egy attribútumot.

Osztály adattípus: Sztring

Ez a paraméter valósítja meg, hogy a felhasználó megadhatja a Microsoft .NET-keretrendszer osztály.

Írja be a fürt adatai: Sztring

Ez a paraméter valósítja meg, hogy a felhasználó megadhatja a fürt.

Kulturális környezet adattípus: Sztring

Ez a paraméter valósítja meg, hogy a felhasználó megadhatja a kulturális környezet, amelyben a parancsmag futtatásához.

Tartomány-adattípus: Sztring

Ez a paraméter valósítja meg, hogy a felhasználó megadhatja a tartomány nevét.

Meghajtó adattípus: Sztring

Ez a paraméter valósítja meg, hogy a felhasználó megadhatja a meghajtó neve.

Eseményadatok írja be: Sztring

Ez a paraméter valósítja meg, hogy a felhasználó megadhatja az esemény nevét.

Kapcsolat adatok típusa: Sztring

Ez a paraméter valósítja meg, hogy a felhasználó megadhatja a hálózati adapter neve.

IpAddress Data type: Sztring

Ez a paraméter valósítja meg, hogy a felhasználó úgy adhat meg az IP-címet.

Feladat adatainak típusa: Sztring

Ez a paraméter valósítja meg, hogy a felhasználó megadhatja a feladatot.

LiteralPath adattípus: Sztring

Ez a paraméter valósítja meg, hogy a felhasználó megadhatja a erőforrás elérési útja, ha a helyettesítő karakterek használata nem támogatott. (Használja a `Path` paramétert, ha a helyettesítő karakterek használata támogatott.)

Mac-adattípus: Sztring

Ez a paraméter valósítja meg, hogy a felhasználó megadhatja a tartományvezérlő (MAC) cím.

ParentId adattípus: Sztring

Ez a paraméter valósítja meg, hogy a felhasználó megadhatja a szülő azonosítója.

Elérési út adatok típusa: Karakterlánc, karakterlánc]

Ez a paraméter valósítja meg, hogy a felhasználó jelezheti az erőforrás elérési útja, ha a helyettesítő karakterek használata támogatott. (Használja a `LiteralPath` paramétert, ha helyettesítő karakterek használata nem támogatott.)

Azt javasoljuk, hogy fejleszteni ezt a paramétert, hogy a szolgáltató által használt teljes "szolgáltató: elérési útja" szintaxis támogatja. Azt javasoljuk, hogy fejleszt, így a lehető legtöbb szolgáltatók működik.

Port adattípus: Egész szám, karakterlánc

Ez a paraméter valósítja meg, hogy a felhasználó úgy adhat meg, a hálózatkezeléshez egész szám vagy egy olyan karakterláncértéket, például a port egyéb "biztalk".

Nyomtató-adattípus: Egész szám, karakterlánc

Ez a paraméter valósítja meg, hogy a felhasználó megadhatja a nyomtatót, a parancsmag használatához.

Adattípus mérete: Int32

Ez a paraméter valósítja meg, hogy a felhasználó megadhatja a méretét.

Írja be a TID adatokat: Sztring

Ez a paraméter valósítja meg, hogy a felhasználó megadhatja a parancsmag egy tranzakció azonosítója (TID).

Írja be az adat típusa: Sztring

Ez a paraméter valósítja meg, hogy a felhasználó megadhatja a kívánt erőforrás típusát.

Adattípus URL-címe: Sztring

Ez a paraméter valósítja meg, hogy a felhasználó megadhatja egy egységes erőforrás-lokátor (URL).

Írja be a felhasználói adatokat: Sztring

Ez a paraméter valósítja meg, hogy a felhasználó megadhatja a saját nevét, vagy egy másik felhasználó nevét.

## <a name="see-also"></a>Lásd még:

[Parancsmag-paraméterek](./cmdlet-parameters.md)

[Egy Windows PowerShell-parancsmag írása](./writing-a-windows-powershell-cmdlet.md)

[Windows PowerShell SDK](../windows-powershell-reference.md)
