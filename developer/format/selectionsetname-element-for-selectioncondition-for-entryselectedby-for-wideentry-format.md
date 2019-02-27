---
title: EntrySelectedBy WideEntry (formátum) esetében a SelectionCondition SelectionSetName eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: a13a429c-a31b-4e29-828c-c0c0917b5415
caps.latest.revision: 11
ms.openlocfilehash: baea89e4b259611dfa45b6bcf94fa0bf2df6b9de
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56845499"
---
# <a name="selectionsetname-element-for-selectioncondition-for-entryselectedby-for-wideentry-format"></a>Az WideEntry EntrySelectedBy eleméhez tartozó SelectionCondition SelectionSetName eleme (Formátum)

Megadja azt a feltételt .NET típusú. Az ebben a készletben típusok találhatók, ha a feltétel nem teljesül, és az objektum megjelenik ez a definíció, a széles nézet használatával.

Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézet elem (formátum) WideControl elem (formátum) WideEntries elem (formátum) WideEntry elem (formátum) EntrySelectedBy elem WideEntry (formátum) SelectionCondition elem számára EntrySelectedBy WideEntry (formátum) SelectionSetName elemhez tartozó SelectionCondition EntrySelectedBy WideEntry (formátum) esetében a

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
|[A WideEntry (formátum) EntrySelectedBy SelectionCondition elem.](./selectioncondition-element-for-entryselectedby-for-widecontrol-format.md)|Határozza meg azt a feltételt, amelyet a definíció használandó léteznie kell.|

## <a name="text-value"></a>Szöveges érték

Adja meg a kijelölt csoport nevét.

## <a name="remarks"></a>Megjegyzés

A kiválasztási feltétel egy kijelölés set vagy a .NET-típus is megadhat, de nem adható meg egyszerre. Kiválasztási feltételek használatával kapcsolatos további információkért lásd: [feltételeinek meghatározása mikor jelenik meg adat](./defining-conditions-for-displaying-data.md).

Kijelölés sets csoportjai közös nézeten, amely meghatározza a formázási fájl által használható .NET-objektumokat. Létrehozásával és a kijelölt csoportok hivatkozó kapcsolatos további információkért lásd: [meghatározása beállítja az objektumok](./defining-selection-sets.md).

Egy széles nézet egyéb összetevőivel kapcsolatos további információkért lásd: [széles nézet létrehozásával](./creating-a-wide-view.md).

## <a name="see-also"></a>Lásd még:

[Egy széles nézet létrehozása](./creating-a-wide-view.md)

[Mikor jelenik meg adat feltételeinek meghatározása](./defining-conditions-for-displaying-data.md)

[Kijelölt csoportok meghatározása](./defining-selection-sets.md)

[A WideEntry (formátum) EntrySelectedBy SelectionCondition elem.](./selectioncondition-element-for-entryselectedby-for-widecontrol-format.md)

[SelectionCondition EntrySelectedBy WideEntry (formátum) esetében a TypeName elem.](./typename-element-for-selectioncondition-for-entryselectedby-for-widecontrol-format.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
