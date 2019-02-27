---
title: SelectionCondition EntrySelectedBy EnumerableExpansion (formátum) esetében a PropertyName eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 9ae11924-0072-451e-bf70-c5ffb25dccc0
caps.latest.revision: 13
ms.openlocfilehash: 0c20512e660c8d2b61d063dbd7078b55b23efeb8
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56849349"
---
# <a name="propertyname-element-for-selectioncondition-for-entryselectedby-for-enumerableexpansion-format"></a>Az EnumerableExpansion EntrySelectedBy eleméhez tartozó SelectionCondition PropertyName eleme (Formátum)

Megadja a .NET-tulajdonság, amely elindítja a feltételt. Ha ez a tulajdonság jelen-e, vagy ha való kiértékelése által `true`, a feltétel nem teljesül, és a definíció szolgál.

Konfigurációs elem (formátum) DefaultSettings elem (formátum) EnumerableExpansions elem (formátum) EnumerableExpansion elem (formátum) EntrySelectedBy elem esetében a EntrySelectedBy EnumerableExpansion (formátum) SelectionCondition elemhez SelectionCondition EntrySelectedBy EnumerableExpansion (formátum) esetében a PropertyName eleme EnumerableExpansion (formátum)

## <a name="syntax"></a>Szintaxis

```xml
<PropertyName>.NetTypeProperty</PropertyName>
```

## <a name="attributes-and-elements"></a>Attribútumok és elemek

A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `PropertyName` elemet.

### <a name="attributes"></a>Attribútumok

Nincs.

### <a name="child-elements"></a>Gyermekelemek

Nincs.

### <a name="parent-elements"></a>Szülőelemek

|Elem|Leírás|
|-------------|-----------------|
|[A EnumerableExpansion (formátum) EntrySelectedBy SelectionCondition elem.](./selectioncondition-element-for-entryselectedby-for-enumerableexpansion-format.md)|Határozza meg azt a feltételt, amelyet a bontsa ki a gyűjtemény objektumokat, ez a definíció léteznie kell.|

## <a name="text-value"></a>Szöveges érték

Adja meg a .NET-tulajdonság neve.

## <a name="remarks"></a>Megjegyzés

A kiválasztási feltétel meg kell adnia legalább egy tulajdonság neve vagy a parancsfájl kiértékelése, de nem adható meg egyszerre. Kiválasztási feltételek használatával kapcsolatos további információkért lásd: [feltételeinek meghatározása mikor jelenik meg adat](./defining-conditions-for-displaying-data.md).

## <a name="see-also"></a>Lásd még:

[Megjelenik feltételeket, amikor adatok meghatározása](./defining-conditions-for-displaying-data.md)

[SelectionCondition EntrySelectedBy EnumerableExpansion (formátum) esetében a scriptblock kulcsszót elem.](./scriptblock-element-for-selectioncondition-for-entryselectedby-for-enumerableexpansion-format.md)

[A EnumerableExpansion (formátum) EntrySelectedBy SelectionCondition elem.](./selectioncondition-element-for-entryselectedby-for-enumerableexpansion-format.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
