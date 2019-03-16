---
title: ListControl (formátum) a ListEntry EntrySelectedBy eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 0f7a74e9-764d-46ce-ab8e-8b9314ce1659
caps.latest.revision: 12
ms.openlocfilehash: 442565d25f60ae8e04501f3f9ffba35d486fbc8a
ms.sourcegitcommit: caac7d098a448232304c9d6728e7340ec7517a71
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/16/2019
ms.locfileid: "58054935"
---
# <a name="entryselectedby-element-for-listentry-for-listcontrol-format"></a>A ListControl elemhez tartozó ListEntry EntrySelectedBy eleme (Formátum)

A .NET-típusokat, amelyek a nézet definíciója vagy a feltétellel, hogy léteznie kell a definíció használandó határoz meg. A legtöbb esetben csak egyetlen definíciót lista nézetben van szükség. Azonban a listanézet víc definic biztosít, ha azt szeretné használni a ugyanabban listanézetet jelennek meg a különböző objektumok különböző adatok.

Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem ListControl elem (formátum) ListEntries elem ListControl (formátum) ListEntry elemhez tartozó ListEntry ListControl (formátum) EntrySelectedBy elemhez tartozó ListEntry a ListControl (formátum)

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
|[A ListControl (formátum) EntrySelectedBy SelectionCondition elem.](./selectioncondition-element-for-entryselectedby-for-listcontrol-format.md)|Nem kötelező eleme.<br /><br /> Határozza meg azt a feltételt, amelyet a lista nézet definíciójában használt léteznie kell.|
|[A ListControl (formátum) EntrySelectedBy SelectionSetName elem.](./selectionsetname-element-for-entryselectedby-for-listcontrol-format.md)|Nem kötelező eleme.<br /><br /> .NET-típusokat, amelyek a nézet definíciója egy halmazát határozza meg.|
|[EntrySelectedBy ListControl (formátum) a TypeName elem.](./typename-element-for-entryselectedby-for-listcontrol-format.md)|Nem kötelező eleme.<br /><br /> A nézet definíciója használó .NET típust határozzon meg.|

### <a name="parent-elements"></a>Szülőelemek

|Elem|Leírás|
|-------------|-----------------|
|[ListEntry eleme ListControl (formátum)](./listentry-element-for-listcontrol-format.md)|Határozza meg, hogy a lista a sorok jelennek meg.|

## <a name="remarks"></a>Megjegyzés

Meg kell adnia legalább egy típusa, a kijelölés készlet vagy a kiválasztási feltétel lista nézet definícióját. Nincs nem használható gyermekelemek számának maximális korlátot.

Kiválasztási feltételek segítségével határozhatók meg egy feltételt, amely megléte esetén használható, például ha egy objektum rendelkezik-e egy adott tulajdonságra a definíció, vagy egy adott tulajdonság értékét, vagy a parancsfájl kiértékelése `true`. További információ a kiválasztási feltételek: [feltételeinek meghatározása mikor jelenik meg adat](./defining-conditions-for-displaying-data.md).

Megjelenítheti az összetevőivel kapcsolatos további információk: [lista nézet létrehozásával](./creating-a-list-view.md).

## <a name="example"></a>Példa

Az alábbi példa bemutatja, hogyan definiálásához az adott nézet használata a .NET-típus neve.

```xml
<ListEntry>
  <EntrySelectedBy>
    <TypeName>NameofDotNetType</TypeName>>
  </EntrySelectedBy>
</ListEntry>
```

## <a name="see-also"></a>Lásd még:

[ListEntry eleme ListControl (formátum)](./listentry-element-for-listcontrol-format.md)

[A ListControl (formátum) EntrySelectedBy SelectionCondition elem.](./selectioncondition-element-for-entryselectedby-for-listcontrol-format.md)

[A ListControl (formátum) EntrySelectedBy SelectionSetName elem.](./selectionsetname-element-for-entryselectedby-for-listcontrol-format.md)

[EntrySelectedBy ListControl (formátum) a TypeName elem.](./typename-element-for-entryselectedby-for-listcontrol-format.md)

[Lista nézet létrehozása](./creating-a-list-view.md)

[Mikor jelenik meg adat feltételeinek meghatározása](./defining-conditions-for-displaying-data.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
