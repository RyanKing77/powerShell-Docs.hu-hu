---
title: (Formátum) WideEntry EntrySelectedBy eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: e0c98933-b7a5-4205-b811-06c0b0bf8988
caps.latest.revision: 9
ms.openlocfilehash: 54c7c261a23075721cd7bce75e530150dc0e0212
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56846094"
---
# <a name="entryselectedby-element-for-wideentry-format"></a>A WideEntry elem EntrySelectedBy eleme (Formátum)

A .NET-típusokat, amelyek a széles nézet vagy a feltételt, amelyet a definíció használandó léteznie kell a definíció határozza meg.

Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézet elem (formátum) WideControl elem (formátum) WideEntries elem (formátum) WideEntry elem (formátum) EntrySelectedBy elem a WideEntry (formátum)

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
|[A WideEntry (formátum) EntrySelectedBy SelectionCondition elem.](./selectioncondition-element-for-entryselectedby-for-widecontrol-format.md)|Nem kötelező eleme.<br /><br /> Határozza meg azt a feltételt, amelyet a széles nézet definíciójában használt léteznie kell.|
|[A WideEntry (formátum) EntrySelectedBy SelectionSetName elem.](./selectionsetname-element-for-entryselectedby-for-widecontrol-format.md)|Nem kötelező eleme.<br /><br /> .NET-típusokat, amelyek a széles nézet definícióját egy halmazát határozza meg.|
|[EntrySelectedBy WideEntry (formátum) a TypeName elem.](./typename-element-for-entryselectedby-for-wideentry-format.md)|Nem kötelező eleme.<br /><br /> A széles körű nézetdefiníció használó .NET típust határozzon meg.|

### <a name="parent-elements"></a>Szülőelemek

|Elem|Leírás|
|-------------|-----------------|
|[WideEntry elem (formátum)](./wideentry-element-for-widecontrol-format.md)|A széles nézet definíciójának biztosít.|

## <a name="remarks"></a>Megjegyzés

Meg kell adnia legalább egy típusa, a kijelölés készlet vagy a kiválasztási feltétel széles nézet definícióját. Nincs nem használható gyermekelemek számának maximális korlátot.

Kiválasztási feltételek segítségével határozhatók meg egy feltételt, amely megléte esetén használható, például ha egy objektum rendelkezik-e egy adott tulajdonságra a definíció, vagy egy adott tulajdonság értékét, vagy a parancsfájl érték kiértékelésének eredménye `true`. További információ a kiválasztási feltételek: [feltételek meghatározása az adatok megjelenítése](./defining-conditions-for-displaying-data.md).

Egy széles nézet egyéb összetevőivel kapcsolatos további információkért lásd: [széles nézet létrehozásával](./creating-a-wide-view.md).

## <a name="see-also"></a>Lásd még:

[WideEntry elem (formátum)](./wideentry-element-for-widecontrol-format.md)

[A WideEntry (formátum) EntrySelectedBy SelectionCondition elem.](./selectioncondition-element-for-entryselectedby-for-widecontrol-format.md)

[A WideEntry (formátum) EntrySelectedBy SelectionSetName elem.](./selectionsetname-element-for-entryselectedby-for-widecontrol-format.md)

[EntrySelectedBy WideEntry (formátum) a TypeName elem.](./typename-element-for-entryselectedby-for-wideentry-format.md)

[Egy széles nézet létrehozása](./creating-a-wide-view.md)

[Adatok megjelenítése feltételek meghatározása](./defining-conditions-for-displaying-data.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
