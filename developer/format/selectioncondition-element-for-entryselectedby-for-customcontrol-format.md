---
title: CustomControl (formátum) a EntrySelectedBy SelectionCondition eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 231e9c6d-09ec-4e68-80ee-0c8f7fe1b9f5
caps.latest.revision: 7
ms.openlocfilehash: 49e2c0cf09dfa55b535effcd431e980daf12fac3
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56848789"
---
# <a name="selectioncondition-element-for-entryselectedby-for-customcontrol-format"></a>A CustomControl elemhez tartozó EntrySelectedBy SelectionCondition eleme (Formátum)

Határozza meg egy feltételt, amely használható vezérlő definíció léteznie kell. Ehhez az elemhez használt egyéni vezérlő nézet definiálása.

Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézet elem (formátum) CustomControl elem a CustomControl megtekintése (formátum) CustomEntry elemhez tartozó CustomEntries CustomControl a nézet (a nézetben (formátum) CustomEntries elemhez CustomEntry CustomControl CustomControl EntrySelectedBy CustomControl nézet (formátum) esetében a nézet (formátum) SelectionCondition elemhez tartozó CustomEntry a nézet (formátum) EntrySelectedBy elemhez tartozó CustomItem eleme formátumban)

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
|[A nézet (formátum) CustomControl SelectionCondition PropertyName elem.](./propertyname-element-for-selectioncondition-for-customcontrol-for-view-format.md)|Nem kötelező eleme.<br /><br /> Megadja a .NET-tulajdonság, amely elindítja a feltétel.|
|[A nézet (formátum) CustomControl SelectionCondition ScriptBlock eleme](./scriptblock-element-for-selectioncondition-for-customcontrol-for-view-format.md)|Nem kötelező eleme.<br /><br /> Megadja a parancsprogramot, amely elindítja a feltétel.|
|[Egyéni vezérlő nézet (formátum) SelectionCondition SelectionSetName elem.](./selectionsetname-element-for-selectioncondition-for-customcontrol-for-view-format.md)|Nem kötelező eleme.<br /><br /> Megadja a .NET-típusok, amely elindítja a feltételt.|
|[A nézet (formátum) CustomControl SelectionCondition TypeName elem.](./typename-element-for-selectioncondition-for-customcontrol-for-view-format.md)|Nem kötelező eleme.<br /><br /> A .NET típusát, amely elindítja a feltételt határozza meg.|

### <a name="parent-elements"></a>Szülőelemek

|Elem|Leírás|
|-------------|-----------------|
|[A nézet (formátum) CustomControl CustomEntry EntrySelectedBy elem.](./entryselectedby-element-for-customentry-for-customcontrol-for-view-format.md)|A .NET-típusokat, amelyek a vezérlő definition vagy a feltétellel, hogy léteznie kell a definíció használandó határozza meg.|

## <a name="remarks"></a>Megjegyzés

Meghatározásakor kiválasztási feltétel, a következő követelményeknek kell teljesülnie:

- A kiválasztási feltételnek legalább egy tulajdonság nevét, vagy parancsprogram-blokkot kell megadnia, de nem adható meg egyszerre.

- A kiválasztási feltétel adhat meg minden olyan .NET-típusok száma vagy a kiválasztási állítja be, de nem adható meg egyszerre.

Kiválasztási feltételek használatával kapcsolatos további információkért lásd: [feltételeinek meghatározása mikor jelenik meg adat](./defining-conditions-for-displaying-data.md).

## <a name="see-also"></a>Lásd még:

[A nézet (formátum) CustomControl SelectionCondition PropertyName elem.](./propertyname-element-for-selectioncondition-for-customcontrol-for-view-format.md)

[A nézet (formátum) CustomControl SelectionCondition ScriptBlock eleme](./scriptblock-element-for-selectioncondition-for-customcontrol-for-view-format.md)

[Egyéni vezérlő nézet (formátum) SelectionCondition SelectionSetName elem.](./selectionsetname-element-for-selectioncondition-for-customcontrol-for-view-format.md)

[A nézet (formátum) CustomControl SelectionCondition TypeName elem.](./typename-element-for-selectioncondition-for-customcontrol-for-view-format.md)

[A nézet (formátum) CustomControl CustomEntry EntrySelectedBy elem.](./entryselectedby-element-for-customentry-for-customcontrol-for-view-format.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
