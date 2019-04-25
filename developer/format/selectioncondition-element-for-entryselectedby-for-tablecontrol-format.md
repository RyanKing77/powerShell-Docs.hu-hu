---
title: TableControl (formátum) a EntrySelectedBy SelectionCondition eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 912f3e63-e4d5-41ce-8710-6dfd8c885dc2
caps.latest.revision: 12
ms.openlocfilehash: 2faca6021dc26878869bdd2d35bc4ffc64d0fe7b
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62075664"
---
# <a name="selectioncondition-element-for-entryselectedby-for-tablecontrol-format"></a>A TableControl elemhez tartozó EntrySelectedBy SelectionCondition eleme (Formátum)

Határozza meg azt a feltételt, amelyet ez a táblázat nézet definícióját használandó léteznie kell. Kiválasztási feltételek, amelyek a tábla definíciója adható meg száma nincs korlátozva van.

Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézet elem (formátum) TableControl elem (formátum) TableRowEntries elem (formátum) TableRowEntry elem (formátum) EntrySelectedBy elem a TableRowEntry (formátum) A TableRowEntry (formátum) EntrySelectedBy SelectionCondition elem.

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

A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a szülőelemet SelectionCondition prvku.

### <a name="attributes"></a>Attribútumok

Nincs.

### <a name="child-elements"></a>Gyermekelemek

|Elem|Leírás|
|-------------|-----------------|
|[SelectionCondition EntrySelectedBy TableRowEntry (formátum) esetében a PropertyName elem.](./propertyname-element-for-selectioncondition-for-entryselectedby-for-tablerowentry-format.md)|Nem kötelező eleme.<br /><br /> Megadja a .NET-tulajdonság, amely elindítja a feltételt.|
|[SelectionCondition EntrySelectedBy TableRowEntry (formátum) esetében a scriptblock kulcsszót elem.](./scriptblock-element-for-selectioncondition-for-entryselectedby-for-tablecontrol-format.md)|Nem kötelező eleme.<br /><br /> Megadja a parancsprogramot, amely elindítja a feltétel.|
|[A EntrySelectedBy TableRowEntry (formátum) a SelectionCondition SelectionSetName eleme](./selectionsetname-element-for-selectioncondition-for-entryselectedby-for-tablecontrol-format.md)|Nem kötelező eleme.<br /><br /> Megadja azt a feltételt .NET típusú.|
|[SelectionCondition EntrySelectedBy TableRowEntry (formátum) esetében a TypeName elem.](./typename-element-for-selectioncondition-for-entryselectedby-for-tablecontrol-format.md)|Nem kötelező eleme.<br /><br /> A .NET típusát, amely elindítja a feltételt határozza meg.|

### <a name="parent-elements"></a>Szülőelemek

|Elem|Leírás|
|-------------|-----------------|
|[EntrySelectedBy eleme TableRowEntry (formátum)](./entryselectedby-element-for-tablerowentry-for-tablecontrol-format.md)|Meghatározza a .NET-típusokat, amelyek a tábla bejegyzés vagy a feltétellel, hogy a bejegyzés használandó léteznie kell.|

## <a name="remarks"></a>Megjegyzés

Minden egyes regisztrációslista-bejegyzés rendelkeznie kell legalább egy típusnév, kijelölés set vagy meghatározott kiválasztási feltételnek.

Meghatározásakor kiválasztási feltétel, a következő követelményeknek kell teljesülnie:

- A kiválasztási feltételnek legalább egy tulajdonság nevét, vagy parancsprogram-blokkot kell megadnia, de nem adható meg egyszerre.

- A kiválasztási feltétel adhat meg minden olyan .NET-típusok száma vagy a kiválasztási állítja be, de nem adható meg egyszerre.

Kiválasztási feltételek használatával kapcsolatos további információkért lásd: [definiáló vonatkozó feltételeket, amikor egy nézet bejegyzés vagy az elem](./defining-conditions-for-displaying-data.md).

A táblázatos nézetre az összetevőivel kapcsolatos további információkért lásd: [tábla nézetek létrehozásával](./creating-a-table-view.md).

## <a name="see-also"></a>Lásd még:

[Tábla nézet létrehozása](./creating-a-table-view.md)

[Mikor jelenik meg adat feltételeinek meghatározása](./defining-conditions-for-displaying-data.md)

[EntrySelectedBy elem (formátum)](./entryselectedby-element-for-tablerowentry-for-tablecontrol-format.md)

[SelectionCondition EntrySelectedBy TableRowEntry (formátum) esetében a PropertyName elem.](./propertyname-element-for-selectioncondition-for-entryselectedby-for-tablerowentry-format.md)

[SelectionCondition EntrySelectedBy TableRowEntry (formátum) esetében a scriptblock kulcsszót elem.](./scriptblock-element-for-selectioncondition-for-entryselectedby-for-tablecontrol-format.md)

[A EntrySelectedBy TableRowEntry (formátum) a SelectionCondition SelectionSetName eleme](./selectionsetname-element-for-selectioncondition-for-entryselectedby-for-tablecontrol-format.md)

[SelectionCondition EntrySelectedBy TableRowEntry (formátum) esetében a TypeName elem.](./typename-element-for-selectioncondition-for-entryselectedby-for-tablecontrol-format.md)

[Egy Windows PowerShell formázás és a fájl típusai](./writing-a-powershell-formatting-file.md)
