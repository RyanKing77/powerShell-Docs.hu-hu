---
title: TableControl (formátum) a TableRowEntroes TableRowEntry eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 18d86af7-7ff9-4968-81be-2caa61937d49
caps.latest.revision: 10
ms.openlocfilehash: 001d46debde61f928c338b2f68112fb201f96216
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56845121"
---
# <a name="tablerowentry-element-for-tablerowentroes-for-tablecontrol-format"></a>A TableControl elemhez tartozó TableRowEntries TableRowEntry eleme (Formátum)

Határozza meg, amely egy sort a táblában megjelennek az adatok.

Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem TableControl elem (formátum) TableRowEntries elem TableControl (formátum) TableRowEntry elemhez tartozó TableRowEntries TableControl (formátum) a

## <a name="syntax"></a>Szintaxis

```xml
<TableRowEntry>
  <Wrap/>
  <EntrySelectedBy>...</EntrySelectedBy>
  <TableColumnItems>...</TableColumnItems>
</TableRowEntry>
```

## <a name="attributes-and-elements"></a>Attribútumok és elemek

A következő szakaszok ismertetik az attribútumokat, gyermekelemek és szülőelemét a `TableRowEntry` elemet.

### <a name="attributes"></a>Attribútumok

Nincs.

### <a name="child-elements"></a>Gyermekelemek

|Elem|Leírás|
|-------------|-----------------|
|[A TableControl (formátum) TableRowEntry EntrySelectedBy elem.](./entryselectedby-element-for-tablerowentry-for-tablecontrol-format.md)|Szükséges eleme.<br /><br /> Meghatározza az objektumok, amelyek tulajdonság értékét a sorban jelenik meg.|
|[A TableControl (formátum) TableRowEntry TableColumnItems elem.](./tablecolumnitems-element-for-tablerowentry-for-tablecontrol-format.md)|Szükséges eleme.<br /><br /> Határozza meg a Tulajdonságok vagy parancsfájlok, melynek értékei jelennek meg.|
|[Elem burkolása TableRowEntry számára a TableCntrol (formátum)](./wrap-element-for-tablerowentry-for-tablecontrl-format.md)|Nem kötelező eleme.<br /><br /> Megadja a szöveg, amely meghaladja a Oszlopszélesség a következő sorban jelenik meg.|

### <a name="parent-elements"></a>Szülőelemek

|Elem|Leírás|
|-------------|-----------------|
|[TableRowEntries eleme TableControl (formátum)](./tablerowentries-element-for-tablecontrol-format.md)|Határozza meg a tábla sorait.|

## <a name="remarks"></a>Megjegyzés

Egy `TableColumnItems` elem és a egy `EntrySelectedBy` elemet meg kell adni.

A táblázatos nézetre az összetevőivel kapcsolatos további információkért lásd: [tábla nézetek létrehozásával](./creating-a-table-view.md).

## <a name="example"></a>Példa

A következő példa bemutatja egy `TableRowEntry` elem, amely meghatározza egy sort, amely két tulajdonságának értékét jeleníti meg a [System.Diagnostics.Process](/dotnet/api/System.Diagnostics.Process) objektum.

```xml
<TableRowEntry>
  <EntrySelectedBy>
    <TypeName>System.Diagnostics.Process</TypeName>
  </EntrySelectedBy>
  <TableColumnItems>
    <TableColumnItem>
      <PropertyName> Property for first column</PropertyName>
    </TableColumnItem>
    <TableColumnItem>
      <PropertyName> Property for second column</PropertyName>
    </TableColumnItem>
  </TableColumnItems>
</TableRowEntry>
```

## <a name="see-also"></a>Lásd még:

[Tábla nézet létrehozása](./creating-a-table-view.md)

[A TableControl (formátum) TableRowEntry EntrySelectedBy elem.](./entryselectedby-element-for-tablerowentry-for-tablecontrol-format.md)

[A TableControl (formátum) TableRowEntry TableColumnItems elem.](./tablecolumnitems-element-for-tablerowentry-for-tablecontrol-format.md)

[TableRowEntries eleme TableControl (formátum)](./tablerowentries-element-for-tablecontrol-format.md)

[A TableControl (formátum) TableRowEntries TableRowEntry elem.](./tablerowentry-element-for-tablerowentroes-for-tablecontrol-format.md)

[Elem burkolása TableRowEntry számára a TableCntrol (formátum)](./wrap-element-for-tablerowentry-for-tablecontrl-format.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
