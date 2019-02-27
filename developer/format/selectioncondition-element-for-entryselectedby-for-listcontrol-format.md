---
title: ListControl (formátum) a EntrySelectedBy SelectionCondition eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 7649d5d0-2b56-49b5-a670-dde46caca343
caps.latest.revision: 11
ms.openlocfilehash: ec75945c5517c02fa001f0a38573c045ffcdbfd3
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56847851"
---
# <a name="selectioncondition-element-for-entryselectedby-for-listcontrol-format"></a>A ListControl elemhez tartozó EntrySelectedBy SelectionCondition eleme (Formátum)

Határozza meg azt a feltételt, amelyet ez a definíció a listanézet használata léteznie kell. Kiválasztási feltételek, amelyek egy definíciója adható meg száma nincs korlátozva van.

Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézet elem (formátum) ListControl elem (formátum) ListEntries elem (formátum) ListEntry elem (formátum) EntrySelectedBy elem ListEntry (formátum) SelectionCondition elem számára EntrySelectedBy a ListEntry (formátum)

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
|[SelectionCondition EmtrySelectedBy ListEntry (formátum) esetében a PropertyName elem.](./propertyname-element-for-selectioncondition-for-entryselectedby-for-listcontrol-format.md)|Nem kötelező eleme.<br /><br /> Megadja a .NET-tulajdonság, amely elindítja a feltételt.|
|[SelectionCondition EntrySelectedBy ListEntry (formátum) esetében a scriptblock kulcsszót elem.](./scriptblock-element-for-selectioncondition-for-entryselectedby-for-listcontrol-format.md)|Nem kötelező eleme.<br /><br /> Megadja a parancsprogramot, amely elindítja a feltétel.|
|[A EntrySelectedBy ListEntry (formátum) a SelectionCondition SelectionSetName eleme](./selectionsetname-element-for-selectioncondition-for-entryselectedby-for-listentry-format.md)|Nem kötelező eleme.<br /><br /> Megadja azt a feltételt .NET típusú.|
|[SelectionCondition EntrySelectedBy ListEntry (formátum) esetében a TypeName elem.](./typename-element-for-selectioncondition-for-entryselectedby-for-listcontrol-format.md)|Nem kötelező eleme.<br /><br /> A .NET típusát, amely elindítja a feltételt határozza meg.|

### <a name="parent-elements"></a>Szülőelemek

|Elem|Leírás|
|-------------|-----------------|
|[EntrySelectedBy eleme TableRowEntry (formátum)](./entryselectedby-element-for-tablerowentry-for-tablecontrol-format.md)|Meghatározza a .NET-típusokat, amelyek a tábla bejegyzés vagy a feltétellel, hogy a bejegyzés használandó léteznie kell.|

## <a name="remarks"></a>Megjegyzés

kiválasztási feltétel definiálása lWhen, az alábbi követelményeknek kell teljesülnie:

- A kiválasztási feltételnek legalább egy tulajdonság nevét, vagy parancsprogram-blokkot kell megadnia, de nem adható meg egyszerre.

- A kiválasztási feltétel adhat meg minden olyan .NET-típusok száma vagy a kiválasztási állítja be, de nem adható meg egyszerre.

Kiválasztási feltételek használatával kapcsolatos további információkért lásd: [feltételeinek meghatározása mikor jelenik meg adat](./defining-conditions-for-displaying-data.md).

A listanézet egyéb összetevőivel kapcsolatos további információkért lásd: [lista nézet létrehozásával](./creating-a-list-view.md).

## <a name="see-also"></a>Lásd még:

[Lista nézet létrehozása](./creating-a-list-view.md)

[Mikor jelenik meg adat feltételeinek meghatározása](./defining-conditions-for-displaying-data.md)

[ListEntry elem (formátum)](./listentry-element-for-listcontrol-format.md)

[A ListEntry (formátum) EnrtySelectedBy SelectionSetName elem.](./selectionsetname-element-for-entryselectedby-for-listcontrol-format.md)

[EntrySelectedBy ListEntry (formátum) a TypeName elem.](http://msdn.microsoft.com/en-us/fcd4daa6-f3fd-43f7-a468-03c582d34533)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
