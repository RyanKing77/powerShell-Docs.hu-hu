---
title: EntrySelectedBy ListEntry (formátum) esetében a SelectionCondition SelectionSetName eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: eae67e47-6c60-4741-8430-78d2cb6067b1
caps.latest.revision: 10
ms.openlocfilehash: ccfc0b772ad3b2d1979c7c832a5153de870035d7
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56851148"
---
# <a name="selectionsetname-element-for-selectioncondition-for-entryselectedby-for-listentry-format"></a>Az ListEntry EntrySelectedBy eleméhez tartozó SelectionCondition SelectionSetName eleme (Formátum)

Megadja azt a feltételt .NET típusú. Az ebben a készletben típusok találhatók, ha a feltétel nem teljesül, és az objektum megjelenik ez a definíció a listanézet használatával.

Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézet elem (formátum) ListControl elem (formátum) ListEntries elem (formátum) ListEntry elem (formátum) EntrySelectedBy elem ListEntry (formátum) SelectionCondition elem számára EntrySelectedBy ListEntry (formátum) SelectionSetName elemhez tartozó SelectionCondition EntrySelectedBy ListEntry (formátum) esetében a

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
|[A ListEntry (formátum) EntrySelectedBy SelectionCondition elem.](./selectioncondition-element-for-entryselectedby-for-listcontrol-format.md)|Határozza meg azt a feltételt, amelyet ez a definíció a listanézet használata léteznie kell.|

## <a name="text-value"></a>Szöveges érték

Adja meg a kijelölt csoport nevét.

## <a name="remarks"></a>Megjegyzés

A kiválasztási feltétel egy kijelölés set vagy a .NET-típus is megadhat, de nem adható meg egyszerre. Kiválasztási feltételek használatával kapcsolatos további információkért lásd: [feltételeinek meghatározása mikor jelenik meg adat](./defining-conditions-for-displaying-data.md).

Kijelölés sets csoportjai közös nézeten, amely meghatározza a formázási fájl által használható .NET-objektumokat. Létrehozásával és a kijelölt csoportok hivatkozó kapcsolatos további információkért lásd: [meghatározása beállítja az objektumok](./defining-selection-sets.md).

A listanézet egyéb összetevőivel kapcsolatos további információkért lásd: [lista nézet létrehozásával](./creating-a-list-view.md).

## <a name="see-also"></a>Lásd még:

[Lista nézet létrehozása](./creating-a-list-view.md)

[Mikor jelenik meg adat feltételeinek meghatározása](./defining-conditions-for-displaying-data.md)

[A ListEntry (formátum) EntrySelectedBy SelectionCondition elem.](./selectioncondition-element-for-entryselectedby-for-listcontrol-format.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
