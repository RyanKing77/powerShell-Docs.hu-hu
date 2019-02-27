---
title: SelectionSetName elemet a vezérlők (formátum) nézet SelectionCondition |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: daea8c6f-873a-4639-9eee-599642822958
caps.latest.revision: 6
ms.openlocfilehash: 697f2ea284393ebddd77a862c408f27f3d332900
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56846192"
---
# <a name="selectionsetname-element-for-selectioncondition-for-controls-for-view-format"></a>A Nézet Vezérlők eleméhez tartozó SelectionCondition SelectionSetName eleme (Formátum)

Megadja azt a feltételt .NET típusú. Az ebben a készletben típusok találhatók, ha a feltétel nem teljesül, és az objektum megjelenik a vezérlőelem használatával. Ez az elem szolgál a nézet által használható vezérlők meghatározásakor.

Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem vezérlők elem (formátum) vezérlőelem elem vezérlők, a nézet (formátum) CustomControl elem megtekintése (formátum) CustomEntries elemet a vezérlők a vezérlő CustomControl vezérlők, a vezérlők, a vezérlők, a vezérlők, a nézet (EntrySelectedBy megtekintése (formátum) SelectionCondition elemhez CustomEntry megtekintése (formátum) EntrySelectedBy elemhez CustomEntries megtekintése (formátum) CustomEntry elemhez Formátum) SelectionSetName eleme SelectionCondition vezérlők nézet (formátum)

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
|[Nézet (formátum) vezérlők EntrySelectedBy SelectionCondition elem.](./selectioncondition-element-for-entryselectedby-for-controls-for-view-format.md)|Határozza meg egy feltételt, amely a vezérlőelem definíciójában használt léteznie kell.|

## <a name="text-value"></a>Szöveges érték

Adja meg a kijelölt csoport nevét.

## <a name="remarks"></a>Megjegyzés

Kijelölés sets csoportjai közös nézeten, amely meghatározza a formázási fájl által használható .NET-objektumokat. Létrehozásával és a kijelölt csoportok hivatkozó kapcsolatos további információkért lásd: [meghatározása beállítja a kijelölés](./defining-selection-sets.md).

A kiválasztási feltétel egy kijelölés set vagy a .NET-típus is megadhat, de nem adható meg egyszerre. Kiválasztási feltételek használatával kapcsolatos további információkért lásd: [feltételek meghatározása az adatok megjelenítése](./defining-conditions-for-displaying-data.md).

## <a name="see-also"></a>Lásd még:

[Nézet (formátum) vezérlők EntrySelectedBy SelectionCondition elem.](./selectioncondition-element-for-entryselectedby-for-controls-for-view-format.md)

[Mikor jelenik meg adat feltételeinek meghatározása](./defining-conditions-for-displaying-data.md)

[Kijelölt csoportok meghatározása](./defining-selection-sets.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
