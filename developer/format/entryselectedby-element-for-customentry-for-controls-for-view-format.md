---
title: EntrySelectedBy elemet a vezérlők (formátum) nézet CustomEntry |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: b3d80a7d-3797-4c46-ae74-ae5cda79b24f
caps.latest.revision: 8
ms.openlocfilehash: efb20c3f2077547e6eb3cb28240512b444f9c481
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62066243"
---
# <a name="entryselectedby-element-for-customentry-for-controls-for-view-format"></a>A Nézet Vezérlők eleméhez tartozó CustomEntry EntrySelectedBy eleme (Formátum)

A .NET-típusokat, amelyek a vezérlő definition vagy a feltétellel, hogy léteznie kell a definíció használandó határozza meg. Ez az elem szolgál a nézet által használható vezérlők meghatározásakor.

Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem vezérlők elem (formátum) vezérlőelem elem vezérlők, a nézet (formátum) CustomControl elem megtekintése (formátum) CustomEntries elemet a vezérlők a vezérlő CustomControl vezérlők, a vezérlők, a vezérlők (formátum) nézet CustomEntry megtekintése (formátum) EntrySelectedBy elemhez CustomEntries megtekintése (formátum) CustomEntry elemhez

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
|[Nézet (formátum) vezérlők EntrySelectedBy SelectionCondition elem.](./selectioncondition-element-for-entryselectedby-for-controls-for-view-format.md)|Nem kötelező eleme.<br /><br /> Határozza meg azt a feltételt, amelyet a definíció használandó léteznie kell.|
|[Nézet (formátum) vezérlők EntrySelectedBy SelectionSetName elem.](./selectionsetname-element-for-entryselectedby-for-controls-for-view-format.md)|Nem kötelező eleme.<br /><br /> Ez a definíció, a vezérlő használó .NET-típusok egy halmazát határozza meg.|
|[Nézet (formátum) vezérlők EntrySelectedBy TypeName elem.](./typename-element-for-entryselectedby-for-controls-for-view-format.md)|Nem kötelező eleme.<br /><br /> Ez a definíció, a vezérlő használó .NET típust határozzon meg.|

### <a name="parent-elements"></a>Szülőelemek

|Elem|Leírás|
|-------------|-----------------|
|[Nézet (formátum) vezérlők CustomEntries CustomEntry elem.](./customentry-element-for-customentries-for-controls-for-view-format.md)|A vezérlőelem egy definíciót tartalmaz.|

## <a name="remarks"></a>Megjegyzés

Kiválasztási feltételek segítségével határozhatók meg egy feltételt, amely léteznie kell a definíciójában használt, például ha egy objektum rendelkezik-e egy adott tulajdonságra vagy ha egy adott tulajdonság értéke, vagy a parancsfájl kiértékelése `true`. További információ a kiválasztási feltételek: [definiáló vonatkozó feltételeket, amikor egy nézet bejegyzés vagy az elem](./defining-conditions-for-displaying-data.md).

## <a name="see-also"></a>Lásd még:

[Nézet (formátum) vezérlők CustomEntries CustomEntry elem.](./customentry-element-for-customentries-for-controls-for-view-format.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
