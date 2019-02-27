---
title: A GroupBy (formátum) SelectionCondition SelectionSetName eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 7b9a4912-d755-42f3-8058-53c0797e28e4
caps.latest.revision: 6
ms.openlocfilehash: 371913eda2b09ff6788494b68738f2ad53ccb115
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56847340"
---
# <a name="selectionsetname-element-for-selectioncondition-for-groupby-format"></a>A GroupBy elemhez tartozó SelectionCondition SelectionSetName eleme (Formátum)

Megadja azt a feltételt .NET típusú. Az ebben a készletben típusok találhatók, ha a feltétel nem teljesül, és az objektum megjelenik a vezérlőelem használatával. Ez az elem szolgál, hogyan jelenjen meg az objektumok egy új csoportot meghatározásakor.

Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem GroupBy elem megtekintése (formátum) CustomControl elem a GroupBy (formátum) CustomEntry elemhez tartozó CustomControl GroupBy (formátum) CustomEntries elemhez GroupBy (formátum) EntrySelectedBy elem CustomEntry EntrySelectedBy SelectionCondition GroupBy (formátum) esetében a GroupBy (formátum) SelectionSetName elemhez tartozó GroupBy (formátum) SelectionCondition elemhez tartozó CustomControl

## <a name="syntax"></a>Szintaxis

```xml
<SelectionSetName>NameofSelectionSet</SelectionSetName>
```

## <a name="attributes-and-elements"></a>Attribútumok és elemek

A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `SelectionSetName` elemet.

### <a name="attributes"></a>Attribútumok

Nincs.

### <a name="child-elements"></a>Gyermekelemek

Nincs.

### <a name="parent-elements"></a>Szülőelemek

|Elem|Leírás|
|-------------|-----------------|
|[A GroupBy (formátum) EntrySelectedBy SelectionCondition elem.](./selectioncondition-element-for-entryselectedby-for-groupby-format.md)|Határozza meg egy feltételt, amely a vezérlőelem definíciójában használt léteznie kell.|

## <a name="text-value"></a>Szöveges érték

Adja meg a kijelölt csoport nevét.

## <a name="remarks"></a>Megjegyzés

Kijelölés sets csoportjai közös nézeten, amely meghatározza a formázási fájl által használható .NET-objektumokat. Létrehozásával és a kijelölt csoportok hivatkozó kapcsolatos további információkért lásd: [meghatározása beállítja a kijelölés](./defining-selection-sets.md).

Ha ez az elem meg van adva, nem adható meg a [TypeName](./typename-element-for-selectioncondition-for-groupby-format.md) elemet. További információ a kiválasztási feltételek meghatározása: [feltételek meghatározása az adatok megjelenítése](./defining-conditions-for-displaying-data.md).

## <a name="see-also"></a>Lásd még:

[A GroupBy (formátum) SelectionCondition TypeName elem.](./typename-element-for-selectioncondition-for-groupby-format.md)

[A GroupBy (formátum) EntrySelectedBy SelectionCondition elem.](./selectioncondition-element-for-entryselectedby-for-groupby-format.md)

[Mikor jelenik meg adat feltételeinek meghatározása](./defining-conditions-for-displaying-data.md)

[Kijelölt csoportok meghatározása](./defining-selection-sets.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
