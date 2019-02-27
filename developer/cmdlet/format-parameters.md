---
title: Paraméterek formázása |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 10e025c5-9aa6-45a5-b851-23d14db1f4cc
caps.latest.revision: 7
ms.openlocfilehash: 4f24af9b32f785695d156bfb4784aa03c97e8987
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56849419"
---
# <a name="format-parameters"></a>Formátumparaméterek

Az alábbi táblázat felsorolja a javasolt nevek és funkciók a paramétereket, formázását vagy az adatok létrehozása érdekében.

Adatok típusa: Kulcsszó

Ezzel a paraméterrel adja meg a parancsmag kimeneti formátum megvalósításához. A lehetséges értékek lehet például szöveg vagy parancsfájlt.

Bináris adattípus: SwitchParameter

Ez a paraméter jelzi, hogy a parancsmag kezeli-e a bináris értékek megvalósításához.

Kódolási adattípus: Kulcsszó

Ez a paraméter határozza meg a típusát, amely támogatott a kódolási megvalósításához. Ha például a lehetséges értékek lehet ASCII, UTF8, Unicode, UTF7, Toto, bájt, és karakterlánc.

Új sor adattípus: SwitchParameter

Ez a paraméter valósítja meg, hogy a sortörés karakterek támogatottak, ha a paraméter meg van adva.

A ShortName adattípus: SwitchParameter

Ez a paraméter valósítja meg, hogy rövid nevek használata támogatott, ha a paraméter meg van adva.

Szélesség adattípus: Int32

Ez a paraméter valósítja meg, hogy a felhasználó megadhatja a kimeneti eszköz szélességét.

Wrap adattípus: SwitchParameter

Ez a paraméter valósítja meg, hogy körbefuttatási használata támogatott, ha a paraméter meg van adva.

## <a name="see-also"></a>Lásd még:

[Parancsmag-paraméterek](./cmdlet-parameters.md)

[Egy Windows PowerShell-parancsmag írása](./writing-a-windows-powershell-cmdlet.md)

[Windows PowerShell SDK](../windows-powershell-reference.md)
