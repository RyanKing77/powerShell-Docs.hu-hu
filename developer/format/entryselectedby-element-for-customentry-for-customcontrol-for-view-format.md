---
title: A nézet (formátum) CustomControl CustomEntry EntrySelectedBy eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 7828b45b-eabf-4432-b127-131b4ef0c800
caps.latest.revision: 8
ms.openlocfilehash: e7176f9f6ef67116ea7c07a46797fb0ba84f915d
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56849321"
---
# <a name="entryselectedby-element-for-customentry-for-customcontrol-for-view-format"></a>A Nézet CustomControl eleméhez tartozó CustomEntry EntrySelectedBy eleme (Formátum)

A .NET-típusokat, amelyek egyéni tételhez vagy a feltétellel, hogy léteznie kell használni a bejegyzés határozza meg.

Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézet elem (formátum) CustomControl elem (formátum) CustomEntries eleme CustomControl számára a nézet (formátum) EntrySelectedBy CustomEntries megtekintése (formátum) CustomEntry elemhez Elem a CustomEntry nézet (formátum)

## <a name="syntax"></a>Szintaxis

```xml
<EntrySelectedBy>
  <TypeName>Nameof.NetType</TypeName>
  <SelectionSetName>NameofSelectionSet</SelectionSetName>
  <SelectionCondition>...</SelectionCondition>
</EntrySelectedBy>
```

## <a name="attributes-and-elements"></a>Attribútumok és elemek

A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `EntrySelectedBy` elemet.

### <a name="attributes"></a>Attribútumok

Nincs.

### <a name="child-elements"></a>Gyermekelemek

|Elem|Leírás|
|-------------|-----------------|
|[A CustomEntry (formátum) EntrySelectedBy SelectionCondition elem.](./selectioncondition-element-for-entryselectedby-for-customcontrol-format.md)|Nem kötelező eleme.<br /><br /> Határozza meg azt a feltételt, amelyet a definíció használandó léteznie kell.|
|[A CustomEntry (formátum) EntrySelectedBy SelectionSetName elem.](./selectionsetname-element-for-entryselectedby-for-customcontrol-for-view-format.md)|Nem kötelező eleme.<br /><br /> Ez a definíció, a vezérlő nézet használó .NET-típusok egy halmazát határozza meg.|
|[EntrySelectedBy CustomEntry (formátum) a TypeName elem.](./typename-element-for-selectioncondition-for-customcontrol-for-view-format.md)|Nem kötelező eleme.<br /><br /> Ez a definíció, a vezérlő nézet használó .NET típust határozzon meg.|

### <a name="parent-elements"></a>Szülőelemek

|Elem|Leírás|
|-------------|-----------------|
|[A nézet (formátum) CustomEntries CustomEntry elem](./customentry-element-for-customentries-for-customcontrol-for-view-format.md)|A .NET-objektumokká által használt funkciók határozza meg.|

## <a name="remarks"></a>Megjegyzés

Meg kell adnia legalább egy típus, kijelölés set vagy bejegyzés kiválasztási feltételnek. Nincs nem használható gyermekelemek számának maximális korlátot.

Kiválasztási feltételek segítségével határozhatók meg egy feltételt, amely léteznie kell használni a bejegyzést, például ha egy objektum rendelkezik-e egy adott tulajdonságra vagy ha egy adott tulajdonság értéke, vagy a parancsfájl kiértékelése `true`. További információ a kiválasztási feltételek: [definiáló vonatkozó feltételeket, amikor egy nézet bejegyzés vagy az elem](./defining-conditions-for-displaying-data.md).

Egyéni vezérlő nézet az összetevőivel kapcsolatos további információkért lásd: [egyéni vezérlő nézetében](./creating-custom-controls.md).

## <a name="see-also"></a>Lásd még:

[A CustomEntry (formátum) EntrySelectedBy SelectionCondition elem.](./selectioncondition-element-for-entryselectedby-for-customcontrol-format.md)

[A CustomEntry (formátum) EntrySelectedBy SelectionSetName elem.](./selectionsetname-element-for-entryselectedby-for-customcontrol-for-view-format.md)

[EntrySelectedBy CustomEntry (formátum) a TypeName elem.](./typename-element-for-selectioncondition-for-customcontrol-for-view-format.md)

[A nézet (formátum) CustomEntries CustomEntry elem](./customentry-element-for-customentries-for-customcontrol-for-view-format.md)

[Egyéni vezérlő nézetében.](./creating-custom-controls.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
