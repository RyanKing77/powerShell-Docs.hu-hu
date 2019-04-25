---
title: TableControl (formátum) a TableRowEntry EntrySelectedBy eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 49623fcf-1238-4d20-a7ce-238d47d9d565
caps.latest.revision: 15
ms.openlocfilehash: 9302bfed0324773cb98d698acdcf608f34ee19c1
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62066158"
---
# <a name="entryselectedby-element-for-tablerowentry--for-tablecontrol-format"></a>A TableControl elemhez tartozó TableRowEntry EntrySelectedBy eleme (Formátum)

A .NET-típusokat, amelyek a táblázatos nézetre vagy a feltételt, amelyet a definíció használandó léteznie kell a definíció határozza meg.

Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem TableControl elem (formátum) TableRowEntries elem (formátum) TableRowEntry elem (formátum) EntrySelectedBy elem (formátum)

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
|[A TableControl (formátum) EntrySelectedBy SelectionCondition elem.](./selectioncondition-element-for-entryselectedby-for-tablecontrol-format.md)|Nem kötelező eleme.<br /><br /> Határozza meg azt a feltételt, amelyet a táblázat nézet definíció használandó léteznie kell.|
|[A TableControl (formátum) EntrySelectedBy SelectionSetName elem.](./selectionsetname-element-for-entryselectedby-for-tablecontrol-format.md)|Nem kötelező eleme.<br /><br /> .NET-típusokat, amelyek a tábla nézetdefiníció egy halmazát határozza meg.|
|[EntrySelectedBy TableControl (formátum) a TypeName elem.](./typename-element-for-entryselectedby-for-tablecontrol-format.md)|Nem kötelező eleme.<br /><br /> A tábla nézetdefiníció használó .NET típust határozzon meg.|

### <a name="parent-elements"></a>Szülőelemek

|Elem|Leírás|
|-------------|-----------------|
|[TableRowEntry eleme TableControl (formátum)](./tablerowentry-element-for-tablerowentries-for-tablecontrol-format.md)|Határozza meg, amely egy sort a táblában megjelennek az adatok.|

## <a name="remarks"></a>Megjegyzés

Meg kell adnia legalább egy típusa, a kijelölés készlet vagy a kiválasztási feltétel táblázat nézet definícióját. Nincs nem használható gyermekelemek számának maximális korlátot.

Kiválasztási feltételek segítségével határozhatók meg egy feltételt, amely megléte esetén használható, például ha egy objektum rendelkezik-e egy adott tulajdonságra a definíció, vagy egy adott tulajdonság értékét, vagy a parancsfájl kiértékelése `true`. További információ a kiválasztási feltételek: [definiáló vonatkozó feltételeket, amikor egy nézet bejegyzés vagy az elem](./defining-conditions-for-displaying-data.md).

A táblázatos nézetre az összetevőivel kapcsolatos további információkért lásd: [tábla nézetek létrehozásával](./creating-a-table-view.md).

## <a name="example"></a>Példa

A következő példa bemutatja egy `TableRowEntry` elem, amellyel a tulajdonságainak megjelenítéséhez a [System.Diagnostics.Process](/dotnet/api/System.Diagnostics.Process) objektum.

```xml
<TableRowEntry>
  <EntrySelectedBy>
    <TypeName>System.Diagnostics.Process</TypeName>
  </EntrySelectedBy>
  <TableColumnItems>
    <TableColumnItem>
      <PropertyName>PropertyForFirstColumn</PropertyName>
    </TableColumnItem>
    <TableColumnItem>
      <PropertyName>PropertyForSecondColumn</PropertyName>
    </TableColumnItem>
  </TableColumnItems>
</TableRowEntry>
```

## <a name="see-also"></a>Lásd még:

[Tábla nézet létrehozása](./creating-a-table-view.md)

[A TableControl (formátum) EntrySelectedBy SelectionCondition elem.](./selectioncondition-element-for-entryselectedby-for-tablecontrol-format.md)

[A TableControl (formátum) EntrySelectedBy SelectionSetName elem.](./selectionsetname-element-for-entryselectedby-for-tablecontrol-format.md)

[TableRowEntry eleme TableControl (formátum)](./tablerowentry-element-for-tablerowentries-for-tablecontrol-format.md)

[EntrySelectedBy TableControl (formátum) a TypeName elem.](./typename-element-for-entryselectedby-for-tablecontrol-format.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
