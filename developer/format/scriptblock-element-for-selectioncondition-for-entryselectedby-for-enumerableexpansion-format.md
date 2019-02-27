---
title: SelectionCondition EntrySelectedBy EnumerableExpansion (formátum) esetében a scriptblock kulcsszót eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 4126b799-c43d-4175-8513-6d761c65437e
caps.latest.revision: 9
ms.openlocfilehash: a51d8d22fa8b0c7f303a5e8f37edcc5e57724063
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56845968"
---
# <a name="scriptblock-element-for-selectioncondition-for-entryselectedby-for-enumerableexpansion-format"></a>Az EnumerableExpansion EntrySelectedBy eleméhez tartozó SelectionCondition ScriptBlock eleme (Formátum)

Megadja a parancsprogramot, amely elindítja a feltétel.

Konfigurációs elem (formátum) DefaultSettings elem (formátum) EnumerableExpansions elem (formátum) EnumerableExpansion elem (formátum) EntrySelectedBy elem esetében a EntrySelectedBy EnumerableExpansion (formátum) SelectionCondition elemhez SelectionCondition EntrySelectedBy EnumerableExpansion (formátum) esetében a scriptblock kulcsszót eleme EnumerableExpansion (formátum)

## <a name="syntax"></a>Szintaxis

```xml
<ScriptBlock>ScriptToEvaluate</ScriptBlock>
```

## <a name="attributes-and-elements"></a>Attribútumok és elemek

A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `ScriptBlock` elemet.

### <a name="attributes"></a>Attribútumok

Nincs.

### <a name="child-elements"></a>Gyermekelemek

Nincs.

### <a name="parent-elements"></a>Szülőelemek

|Elem|Leírás|
|-------------|-----------------|
|[A EnumerableExpansion (formátum) EntrySelectedBy SelectionCondition elem.](./selectioncondition-element-for-entryselectedby-for-enumerableexpansion-format.md)|Határozza meg azt a feltételt, amelyet a bontsa ki a gyűjtemény objektumokat, ez a definíció léteznie kell.|

## <a name="text-value"></a>Szöveges érték

Adja meg a parancsfájl, amely ki lesz értékelve.

## <a name="remarks"></a>Megjegyzés

A kiválasztási feltétel kiértékeléséhez, legalább egy parancsfájl vagy a tulajdonság nevét kell megadnia, de nem adható meg egyszerre. Kiválasztási feltételek használatával kapcsolatos további információkért lásd: [feltételeinek meghatározása mikor jelenik meg adat](./defining-conditions-for-displaying-data.md).

## <a name="see-also"></a>Lásd még:

[Mikor jelenik meg adat feltételeinek meghatározása](./defining-conditions-for-displaying-data.md)

[SelectionCondition EntrySelectedBy EnumerableExpansion (formátum) esetében a PropertyName elem.](./propertyname-element-for-selectioncondition-for-entryselectedby-for-enumerableexpansion-format.md)

[A EnumerableExpansion (formátum) EntrySelectedBy SelectionCondition elem.](./selectioncondition-element-for-entryselectedby-for-enumerableexpansion-format.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
