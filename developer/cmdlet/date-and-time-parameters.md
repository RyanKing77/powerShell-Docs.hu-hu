---
title: Dátum és idő paraméterek |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 71da921b-7c32-4155-b2f8-b19f30ec774d
caps.latest.revision: 7
ms.openlocfilehash: 49f6c667b0fd9678586559af39a33f982de0a68c
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56846710"
---
# <a name="date-and-time-parameters"></a>Dátum- és időparaméterek

A következő táblázat felsorolja a javasolt nevek és funkciók a paramétereket, dátum és idő adatok kezelésére. Dátum és idő paraméterek jellemzően rögzíti, ha a hiba jön létre vagy érhető el.

Írja be az elért adatok: SwitchParameter

Végrehajtja ezt a paramétert, hogy mikor van megadva a parancsmag végre lesznek hajtva elért erőforrások alapján a megadott dátum és idő alapján a `Before` és `After` paramétereket.

Ha ez a paraméter van megadva, a `Created` és `Modified` kell lennie a paraméterek nem adható meg.

Adattípus: után DateTime

Ezzel a paraméterrel adja meg a dátum és idő, amely után a parancsmag értek megvalósításához. Az a `After` paraméter működjön, a parancsmag is rendelkeznie kell egy `Accessed`, `Created`, vagy `Modified` paraméter. És meg kell arra a paraméterre `true` amikor a parancsmag beszerzését kezdeményezték.

Mielőtt adattípus: DateTime

Ezzel a paraméterrel adja meg a dátum és idő, ameddig a parancsmag értek megvalósításához. Az a `Before` paraméter működjön, a parancsmag is rendelkeznie kell egy `Accessed`, `Created`, vagy `Modified` paraméter. És meg kell arra a paraméterre `true` amikor a parancsmag beszerzését kezdeményezték.

Hozza létre a típusú adatokat: SwitchParameter

Végrehajtja ezt a paramétert, hogy mikor van megadva a parancsmag végre lesznek hajtva a létrehozott erőforrások alapján a megadott dátum és idő alapján a `Before` és `After` paramétereket.

Ha ez a paraméter van megadva, a `Accessed` és `Modified` paraméter megadása nem kötelező.

Pontos adattípus: SwitchParameter

Ez a paraméter valósítja meg, hogy mikor van megadva az erőforrás kifejezés pontosan meg kell egyeznie az erőforrás neve. Ha a paraméter nincs megadva az erőforrás kifejezés és neve nem pontosan egyeznie kell.

Írja be a módosított adatokat: DateTime

Megvalósítani ezt a paramétert, hogy mikor van megadva a parancsmag végre lesznek hajtva megváltozott erőforrásokat alapján a megadott dátum és idő alapján a `Before` és `After` paramétereket.

Ha ez a paraméter van megadva, a `Accessed` és `Created` paraméter megadása nem kötelező.

## <a name="see-also"></a>Lásd még:

[Parancsmag-paraméterek](./cmdlet-parameters.md)

[Egy Windows PowerShell-parancsmag írása](./writing-a-windows-powershell-cmdlet.md)

[Windows PowerShell SDK](../windows-powershell-reference.md)
