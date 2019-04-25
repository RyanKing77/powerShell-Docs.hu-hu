---
title: SelectionCondition elemet a vezérlők (formátum) nézet EntrySelectedBy |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 2623407e-fa10-4d27-a804-204f6d50ef22
caps.latest.revision: 6
ms.openlocfilehash: ea15e647a9dd7a7064718a0c536c4a3178d62d95
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62064231"
---
# <a name="selectioncondition-element-for-entryselectedby-for-controls-for-view-format"></a>A Nézet Vezérlők eleméhez tartozó EntrySelectedBy SelectionCondition eleme (Formátum)

Határozza meg egy feltételt, amely a vezérlőelem definíciójában használt léteznie kell. Ez az elem szolgál a nézet által használható vezérlők meghatározásakor.

Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem vezérlők elem (formátum) vezérlőelem elem vezérlők, a nézet (formátum) CustomControl elem megtekintése (formátum) CustomEntries elemet a vezérlők a vezérlő CustomControl vezérlők, a vezérlők, a vezérlők, a vezérlők, a nézet (EntrySelectedBy megtekintése (formátum) SelectionCondition elemhez CustomEntry megtekintése (formátum) EntrySelectedBy elemhez CustomEntries megtekintése (formátum) CustomEntry elemhez Formátum)

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
|[A PropertyName eleme SelectionCondition vezérlők nézet (formátum)](./propertyname-element-for-selectioncondition-for-controls-for-view-format.md)|Nem kötelező eleme.<br /><br /> Megadja a .NET-tulajdonság, amely elindítja a feltétel.|
|[Nézet (formátum) vezérlők SelectionCondition ScriptBlock elem.](./scriptblock-element-for-selectioncondition-for-controls-for-view-format.md)|Nem kötelező eleme.<br /><br /> Megadja a parancsprogramot, amely elindítja a feltétel.|
|[Nézet (formátum) vezérlők SelectionCondition SelectionSetName elem.](./selectionsetname-element-for-selectioncondition-for-controls-for-view-format.md)|Nem kötelező eleme.<br /><br /> Megadja a .NET-típusok, amely elindítja a feltételt.|
|[Nézet (formátum) vezérlők SelectionCondition TypeName elem.](./typename-element-for-selectioncondition-for-controls-for-view-format.md)|Nem kötelező eleme.<br /><br /> A .NET típusát, amely elindítja a feltételt határozza meg.|

### <a name="parent-elements"></a>Szülőelemek

|Elem|Leírás|
|-------------|-----------------|
|[Nézet (formátum) vezérlők CustomEntry EntrySelectedBy elem.](./entryselectedby-element-for-customentry-for-controls-for-view-format.md)|A .NET-típusokat, amelyek a vezérlő definition vagy a feltétellel, hogy léteznie kell a definíció használandó határozza meg.|

## <a name="remarks"></a>Megjegyzés

Meghatározásakor kiválasztási feltétel, a következő követelményeknek kell teljesülnie:

- A kiválasztási feltételnek legalább egy tulajdonság nevét, vagy parancsprogram-blokkot kell megadnia, de nem adható meg egyszerre.

- A kiválasztási feltétel adhat meg minden olyan .NET-típusok száma vagy a kiválasztási állítja be, de nem adható meg egyszerre.

Kiválasztási feltételek használatával kapcsolatos további információkért lásd: [feltételeinek meghatározása mikor jelenik meg adat](./defining-conditions-for-displaying-data.md).

## <a name="see-also"></a>Lásd még:

[A PropertyName eleme SelectionCondition vezérlők nézet (formátum)](./propertyname-element-for-selectioncondition-for-controls-for-view-format.md)

[Nézet (formátum) vezérlők SelectionCondition ScriptBlock elem.](./scriptblock-element-for-selectioncondition-for-controls-for-view-format.md)

[Nézet (formátum) vezérlők SelectionCondition SelectionSetName elem.](./selectionsetname-element-for-selectioncondition-for-controls-for-view-format.md)

[Nézet (formátum) vezérlők SelectionCondition TypeName elem.](./typename-element-for-selectioncondition-for-controls-for-view-format.md)

[Nézet (formátum) vezérlők CustomEntry EntrySelectedBy elem.](./entryselectedby-element-for-customentry-for-controls-for-view-format.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
