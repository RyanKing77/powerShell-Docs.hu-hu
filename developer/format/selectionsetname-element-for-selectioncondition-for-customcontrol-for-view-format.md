---
title: A nézet (formátum) CustomControl SelectionCondition SelectionSetName eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: a52b05a9-762e-4f1c-ad57-9d1710149722
caps.latest.revision: 10
ms.openlocfilehash: 25d46665ca5df3ddf49af5718d513b84c77988c8
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56851547"
---
# <a name="selectionsetname-element-for-selectioncondition-for-customcontrol-for-view-format"></a>A Nézet CustomControl eleméhez tartozó SelectionCondition SelectionSetName eleme (Formátum)

Megadja azt a feltételt .NET típusú. Az ebben a készletben típusok találhatók, ha a feltétel nem teljesül, és az objektum megjelenik a vezérlőelem használatával. Ehhez az elemhez használt egyéni vezérlő nézet definiálása.

Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézet elem (formátum) CustomControl elem (formátum) CustomEntries eleme CustomControl számára a nézet (formátum) EntrySelectedBy CustomEntries megtekintése (formátum) CustomEntry elemhez Elem a CustomEntry nézet (formátum)

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
|[A nézet (formátum) CustomControl EntrySelectedBy SelectionCondition elem.](./selectioncondition-element-for-entryselectedby-for-customcontrol-format.md)|Határozza meg egy feltételt, amely a vezérlőelem definíciójában használt léteznie kell.|

## <a name="text-value"></a>Szöveges érték

Adja meg a kijelölt csoport nevét.

## <a name="remarks"></a>Megjegyzés

Kijelölés sets csoportjai közös nézeten, amely meghatározza a formázási fájl által használható .NET-objektumokat. Létrehozásával és a kijelölt csoportok hivatkozó kapcsolatos további információkért lásd: [meghatározása beállítja az objektumok](./defining-selection-sets.md).

A kiválasztási feltétel egy kijelölés set vagy a .NET-típus is megadhat, de nem adható meg egyszerre. Kiválasztási feltételek használatával kapcsolatos további információkért lásd: [feltételeinek meghatározása mikor jelenik meg adat](./defining-conditions-for-displaying-data.md).

## <a name="see-also"></a>Lásd még:

[A nézet (formátum) CustomControl EntrySelectedBy SelectionCondition elem.](./selectioncondition-element-for-entryselectedby-for-customcontrol-format.md)

[Mikor jelenik meg adat feltételeinek meghatározása](./defining-conditions-for-displaying-data.md)

[Kijelölt csoportok meghatározása](./defining-selection-sets.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
