---
title: SelectionCondition EntrySelectedBy WideControl (formátum) esetében a scriptblock kulcsszót eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 5ec68309-7826-4643-a521-e29c996663fb
caps.latest.revision: 11
ms.openlocfilehash: 649a978e21e9421a3f3e953261e1d309e23c3f9c
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56851673"
---
# <a name="scriptblock-element-for-selectioncondition-for-entryselectedby-for-widecontrol-format"></a>Az WideControl EntrySelectedBy eleméhez tartozó SelectionCondition S eleme (Formátum)

Megadja a parancsprogramot, amely elindítja a feltétel. Ha ez a parancsfájl kiértékelése `true`, a feltétel nem teljesül, és a széles körű bejegyzés definíciót használja.

Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézet elem (formátum) WideControl elem (formátum) WideEntries elem (formátum) WideEntry elem (formátum) EntrySelectedBy elem WideEntry (formátum) SelectionCondition elem számára EntrySelectedBy a SelectionCondition EntrySelectedBy WideEntry (formátum) esetében a scriptblock kulcsszót eleme WideEntry (formátum)

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
|[A WideEntry (formátum) EntrySelectedBy SelectionCondition elem.](./selectioncondition-element-for-entryselectedby-for-widecontrol-format.md)|Határozza meg azt a feltételt, amelyet a definíció használandó léteznie kell.|

## <a name="text-value"></a>Szöveges érték

Adja meg a parancsfájl, amely ki lesz értékelve.

## <a name="remarks"></a>Megjegyzés

A kiválasztási feltétel kiértékeléséhez, legalább egy parancsfájl vagy a tulajdonság nevét kell megadnia, de nem adható meg egyszerre. Kiválasztási feltételek használatával kapcsolatos további információkért lásd: [feltételeinek meghatározása mikor jelenik meg adat](./defining-conditions-for-displaying-data.md).

Egy széles nézet egyéb összetevőivel kapcsolatos további információkért lásd: [széles nézet](./creating-a-wide-view.md).

## <a name="see-also"></a>Lásd még:

[Egy széles nézet létrehozása](./creating-a-wide-view.md)

[Mikor jelenik meg adat feltételeinek meghatározása](./defining-conditions-for-displaying-data.md)

[SelectionCondition EntrySelectedBy WideEntry (formátum) esetében a PropertyName elem.](./propertyname-element-for-selectioncondition-for-entryselectedby-for-wideentry-format.md)

[A WideEntry (formátum) EntrySelectedBy SelectionCondition elem.](./selectioncondition-element-for-entryselectedby-for-widecontrol-format.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
