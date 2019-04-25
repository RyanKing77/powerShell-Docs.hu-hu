---
title: TableHeaders elem (formátum) |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: f9fa2b6f-b99a-42de-9779-44e9cb583f71
caps.latest.revision: 15
ms.openlocfilehash: bd44fcf4878c858afe81fb071ce72f627ac465dc
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62075409"
---
# <a name="tableheaders-element-format"></a>TableHeaders elem (Formátum)

Meghatározza egy tábla oszlopait az fejlécek.

ViewDefinitions elem (formátum) nézetben (formátum) elem TableControl elem (formátum) TableHeaders elem TableControl (formátum)

## <a name="syntax"></a>Szintaxis

```xml
<TableHeaders>
  <TableColumnHeader>...</TableColumnHeader>
</TableHeaders>

```

## <a name="attributes-and-elements"></a>Attribútumok és elemek

A következő szakaszok ismertetik az attribútumokat, a gyermekelemek és a szülő elemei a `TableHeaders` elemet. A megjelenítendő objektum minden egyes tulajdonság gyermekelemet kell lennie. Az oszlop fejléc információk jelennek meg, hogy a gyermekelemek megadott sorrendben.

### <a name="attributes"></a>Attribútumok

Nincs.

### <a name="child-elements"></a>Gyermekelemek

|Elem|Leírás|
|-------------|-----------------|
|[TableColumnHeader elem (formátum)](./tablecolumnheader-element-format.md)|Nem kötelező eleme.<br /><br /> Határozza meg a címke, a szélesség és az adatokat egy oszlopában táblázatban igazítását.|

### <a name="parent-elements"></a>Szülőelemek

|Elem|Leírás|
|-------------|-----------------|
|[TableControl elem (formátum)](./tablecontrol-element-format.md)|Határozza meg a nézet táblázatos formában.|

## <a name="remarks"></a>Megjegyzés

A táblázatos nézetre az összetevőivel kapcsolatos további információkért lásd: [tábla nézetek létrehozásával](./creating-a-table-view.md).

## <a name="example"></a>Példa

Ez a példa bemutatja egy `TableHeaders` elem, amely meghatározza a két oszlopfejléceket.

```xml
<TableHeaders>
  <TableColumnHeader>
    <Label>Column 1</Label)
    <Width>16</Width>
    <Alignment>Left</Alignment>
  </TableColumnHeader>
  <TableColumnHeader>
    <Label>Column 2</Label)
    <Width>10</Width>
    <Alignment>Centered</Alignment>
  </TableColumnHeader>
</TableHeaders>
```

## <a name="see-also"></a>Lásd még:

[Tábla nézet létrehozása](./creating-a-table-view.md)

[TableColumnHeader elem (formátum)](./tablecolumnheader-element-format.md)

[TableControl elem (formátum)](./tablecontrol-element-format.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
