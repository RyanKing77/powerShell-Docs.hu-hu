---
title: A GroupBy (formátum) EntrySelectedBy SelectionCondition eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 6dc2093a-dc54-42c4-ada3-c8d089ba1e8e
caps.latest.revision: 6
ms.openlocfilehash: a6738a7c4c934b2d6a16695a711f7c6c80afdd2d
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56846227"
---
# <a name="selectioncondition-element-for-entryselectedby-for-groupby-format"></a>A GroupBy elemhez tartozó EntrySelectedBy SelectionCondition eleme (Formátum)

Határozza meg egy feltételt, amely használható vezérlő definíció léteznie kell. Ez az elem szolgál, hogyan jelenjen meg az objektumok egy új csoportot meghatározásakor.

Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem GroupBy elem megtekintése (formátum) CustomControl elem a GroupBy (formátum) CustomEntry elemhez tartozó CustomControl GroupBy (formátum) CustomEntries elemhez GroupBy (formátum) EntrySelectedBy elem CustomEntry EntrySelectedBy GroupBy (formátum) esetében a GroupBy (formátum) SelectionCondition elemhez tartozó CustomControl

## <a name="syntax"></a>Szintaxis

```xml
<SelectionCondition>
  <TypeName>Nameof.NetType</TypeName>
  <SelectionSetName>NameofSelectionSet</SelectionSetName>
  <PropertyName>.NetTypeProperty</PropertyName>
  <ScriptBlock>ScriptToEvaluate</ScriptBlock>
</SelectionCondition>
```

## <a name="attributes-and-elements"></a>Attribútumok és elemek

A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `SelectionCondition` elemet.

### <a name="attributes"></a>Attribútumok

Nincs.

### <a name="child-elements"></a>Gyermekelemek

|Elem|Leírás|
|-------------|-----------------|
|[A GroupBy (formátum) SelectionCondition PropertyName elem.](./propertyname-element-for-selectioncondition-for-groupby-format.md)|Nem kötelező eleme.<br /><br /> Megadja a .NET-tulajdonság, amely elindítja a feltétel.|
|[SelectionCondition GroupBy (formátum) a scriptblock kulcsszót elem.](./scriptblock-element-for-selectioncondition-for-entryselectedby-for-groupby-format.md)|Nem kötelező eleme.<br /><br /> Megadja a parancsprogramot, amely elindítja a feltétel.|
|[A GroupBy (formátum) SelectionCondition SelectionSetName elem.](./selectionsetname-element-for-selectioncondition-for-groupby-format.md)|Nem kötelező eleme.<br /><br /> Megadja a .NET-típusok, amely elindítja a feltételt.|
|[A GroupBy (formátum) SelectionCondition TypeName elem.](./typename-element-for-selectioncondition-for-groupby-format.md)|Nem kötelező eleme.<br /><br /> A .NET típusát, amely elindítja a feltételt határozza meg.|

### <a name="parent-elements"></a>Szülőelemek

|Elem|Leírás|
|-------------|-----------------|
|[A GroupBy (formátum) CustomEntry EntrySelectedBy elem.](./entryselectedby-element-for-customentry-for-groupby-format.md)|A .NET-típusokat, amelyek a vezérlő definition vagy a feltétellel, hogy léteznie kell a definíció használandó határozza meg.|

## <a name="remarks"></a>Megjegyzés

Meghatározásakor kiválasztási feltétel, a következő követelményeknek kell teljesülnie:

- A kiválasztási feltételnek legalább egy tulajdonság nevét, vagy parancsprogram-blokkot kell megadnia, de nem adható meg egyszerre.

- A kiválasztási feltétel adhat meg minden olyan .NET-típusok száma vagy a kiválasztási állítja be, de nem adható meg egyszerre.

Kiválasztási feltételek használatával kapcsolatos további információkért lásd: [feltételeinek meghatározása mikor jelenik meg adat](./defining-conditions-for-displaying-data.md).

## <a name="see-also"></a>Lásd még:

[A nézet (formátum) CustomControl SelectionCondition PropertyName elem.](./propertyname-element-for-selectioncondition-for-customcontrol-for-view-format.md)

[A nézet (formátum) CustomControl SelectionCondition ScriptBlock eleme](./scriptblock-element-for-selectioncondition-for-customcontrol-for-view-format.md)

[Egyéni vezérlő nézet (formátum) SelectionCondition SelectionSetName elem.](./selectionsetname-element-for-selectioncondition-for-customcontrol-for-view-format.md)

[A GroupBy (formátum) SelectionCondition TypeName elem.](./typename-element-for-selectioncondition-for-groupby-format.md)

[A GroupBy (formátum) CustomEntry EntrySelectedBy elem.](./entryselectedby-element-for-customentry-for-groupby-format.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
