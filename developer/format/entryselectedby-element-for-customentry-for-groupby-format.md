---
title: A GroupBy (formátum) CustomEntry EntrySelectedBy eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: a317d482-73cc-4c98-a002-1357fa879cd7
caps.latest.revision: 7
ms.openlocfilehash: cf1a80e845c38d97d71f26eba63c38a550958b79
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56851582"
---
# <a name="entryselectedby-element-for-customentry-for-groupby-format"></a>A GroupBy elemhez tartozó CustomEntry EntrySelectedBy eleme (Formátum)

A .NET-típusokat, amelyek a vezérlő definition vagy a feltétellel, hogy léteznie kell a definíció használandó határozza meg. Ez az elem szolgál, hogyan jelenjen meg az objektumok egy új csoportot meghatározásakor.

Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem GroupBy elem megtekintése (formátum) CustomControl elem a GroupBy (formátum) CustomEntry elemhez tartozó CustomControl GroupBy (formátum) CustomEntries elemhez CustomControl GroupBy (formátum) EntrySelectedBy elemhez tartozó CustomEntry a GroupBy (formátum)

## <a name="syntax"></a>Szintaxis

```xml
<EntrySelectedBy>
  <TypeName>Nameof.NetType</TypeName>
  <SelectionSetName>NameofSelectionSet</SelectionSetName>
  <SelectionCondition>...</SelectionCondition>
</EntrySelectedBy>
```

## <a name="attributes-and-elements"></a>Attribútumok és elemek

A következő szakaszok ismertetik az attribútumokat, gyermekelemek és szülőelemét a `EntrySelectedBy` elemet. Meg kell adnia legalább egy típusa, kijelölés set vagy -definíció kiválasztási feltételnek. Nincs nem használható gyermekelemek számának maximális korlátot.

### <a name="attributes"></a>Attribútumok

Nincs.

### <a name="child-elements"></a>Gyermekelemek

|Elem|Leírás|
|-------------|-----------------|
|[A GroupBy (formátum) EntrySelectedBy SelectionCondition elem.](./selectioncondition-element-for-entryselectedby-for-groupby-format.md)|Nem kötelező eleme.<br /><br /> Határozza meg azt a feltételt, amelyet a definíció használandó léteznie kell.|
|[A GroupBy (formátum) EntrySelectedBy SelectionSetName elem.](./selectionsetname-element-for-entryselectedby-for-groupby-format.md)|Nem kötelező eleme.<br /><br /> Ez a definíció, a vezérlő használó .NET-típusok egy halmazát határozza meg.|
|[A GroupBy (formátum) EntrySelectedBy TypeName elem.](./typename-element-for-entryselectedby-for-groupby-format.md)|Nem kötelező eleme.<br /><br /> Ez a definíció, a vezérlő használó .NET típust határozzon meg.|

### <a name="parent-elements"></a>Szülőelemek

|Elem|Leírás|
|-------------|-----------------|
|[A GroupBy (formátum) CustomControl CustomEntry elem.](./customentry-element-for-customcontrol-for-groupby-format.md)|A vezérlőelem egy definíciót tartalmaz.|

## <a name="remarks"></a>Megjegyzés

Kiválasztási feltételek segítségével határozhatók meg egy feltételt, amely léteznie kell a definíciójában használt, például ha egy objektum rendelkezik-e egy adott tulajdonságra vagy ha egy adott tulajdonság értéke, vagy a parancsfájl kiértékelése `true`. További információ a kiválasztási feltételek: [definiáló vonatkozó feltételeket, amikor egy nézet bejegyzés vagy az elem](./defining-conditions-for-displaying-data.md).

## <a name="see-also"></a>Lásd még:

[A GroupBy (formátum) EntrySelectedBy SelectionCondition elem.](./selectioncondition-element-for-entryselectedby-for-groupby-format.md)

[A GroupBy (formátum) EntrySelectedBy SelectionSetName elem.](./selectionsetname-element-for-entryselectedby-for-groupby-format.md)

[A GroupBy (formátum) EntrySelectedBy TypeName elem.](./typename-element-for-entryselectedby-for-groupby-format.md)

[Nézet (formátum) vezérlők CustomEntries CustomEntry elem.](./customentry-element-for-customentries-for-controls-for-view-format.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
