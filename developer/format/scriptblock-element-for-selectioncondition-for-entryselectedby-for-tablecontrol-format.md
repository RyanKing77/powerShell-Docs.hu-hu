---
title: SelectionCondition EntrySelectedBy TableControl (formátum) esetében a scriptblock kulcsszót eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 2b11fbcf-3426-48ae-9319-2c847969f723
caps.latest.revision: 10
ms.openlocfilehash: 7afc834e68ef332bee1e23da782fb5c5527fcf54
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56846514"
---
# <a name="scriptblock-element-for-selectioncondition-for-entryselectedby-for-tablecontrol-format"></a>Az TableControl EntrySelectedBy eleméhez tartozó SelectionCondition S eleme (Formátum)

Adja meg a parancsprogram-blokkot, amely elindítja a feltételt. Ha ez a parancsfájl kiértékelése `true`, a feltétel nem teljesül, és a táblabejegyzés szolgál.

Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézet elem (formátum) TableControl elem (formátum) TableRowEntries elem (formátum) TableRowEntry elem (formátum) EntrySelectedBy elem a TableRowEntry (formátum) TableRowEntry (formátum) ScriptBlock elemhez tartozó SelectionCondition EntrySelectedBy TableRowEntry (formátum) esetében a EntrySelectedBy SelectionCondition elem.

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
|[A TableRowEntry (formátum) EntrySelectedBy SelectionCondition elem.](./selectioncondition-element-for-entryselectedby-for-tablecontrol-format.md)|Határozza meg azt a feltételt, amelyet a használandó tábla bejegyzéshez tartozó léteznie kell.|

## <a name="text-value"></a>Szöveges érték

Adja meg a parancsfájl, amely ki lesz értékelve.

## <a name="remarks"></a>Megjegyzés

A kiválasztási feltétel meg kell adnia legalább egy parancsfájl letiltása vagy a tulajdonság nevét, de nem adható meg egyszerre. Kiválasztási feltételek használatával kapcsolatos további információkért lásd: [definiáló vonatkozó feltételeket, amikor egy nézet bejegyzés vagy az elem](./defining-conditions-for-displaying-data.md).

A táblázatos nézetre az összetevőivel kapcsolatos további információkért lásd: [tábla nézetek létrehozásával](./creating-a-table-view.md).

## <a name="see-also"></a>Lásd még:

[Tábla nézet létrehozása](./creating-a-table-view.md)

[Mikor jelenik meg adat feltételeinek meghatározása](./defining-conditions-for-displaying-data.md)

[SelectionCondition EntrySelectedBy TableRowEntry (formátum) esetében a PropertyName elem.](./propertyname-element-for-selectioncondition-for-entryselectedby-for-tablerowentry-format.md)

[A TableRowEntry (formátum) EntrySelectedBy SelectionCondition elem.](./selectioncondition-element-for-entryselectedby-for-tablecontrol-format.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
