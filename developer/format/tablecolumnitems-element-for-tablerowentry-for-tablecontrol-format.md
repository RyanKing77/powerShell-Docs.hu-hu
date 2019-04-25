---
title: TableControl (formátum) a TableRowEntry TableColumnItems eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: d43684ce-7c3d-4d14-8dbd-061c111ee805
caps.latest.revision: 12
ms.openlocfilehash: d05437aaa9652e7f81d0854d1a746acffe145699
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62075392"
---
# <a name="tablecolumnitems-element-for-tablerowentry-for-tablecontrol-format"></a>A TableControl TableRowEntry elemének TableColumnItems eleme (Formátum)

A Tulajdonságok vagy parancsfájlok, melynek értékei jelennek meg a sor határoz meg.

Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem TableControl elem (formátum) TableRowEntries elem TableControl (formátum) TableRowEntry elemhez tartozó TableRowEntries TableControl (formátum) a A TableControl (formátum) TableControlEntry TableColumnItems elem.

## <a name="syntax"></a>Szintaxis

```xml
TableColumnItems>
  <TableColumnItem>...</TableColumnItem>
</TableColumnItems>
```

## <a name="attributes-and-elements"></a>Attribútumok és elemek

A következő szakaszok ismertetik az attribútumokat, gyermekelemek és szülőelemét a `TableColumnItems` elemet.

### <a name="attributes"></a>Attribútumok

Nincs.

### <a name="child-elements"></a>Gyermekelemek

|Elem|Leírás|
|-------------|-----------------|
|[A TableControl (formátum) TableColumnItems TableColumnItem elem.](./tablecolumnitem-element-for-tablecolumnitems-for-tablecontrol-format.md)|Szükséges eleme.<br /><br /> Határozza meg, tulajdonság vagy parancsfájl, amelynek értéke megjelenik a sor egy oszlopban.|

### <a name="parent-elements"></a>Szülőelemek

|Elem|Leírás|
|-------------|-----------------|
|[A TableControl (formátum) TableRowEntries TableRowEntry elem.](./tablerowentry-element-for-tablerowentries-for-tablecontrol-format.md)|Határozza meg, amely egy sort a táblában megjelennek az adatok.|

## <a name="remarks"></a>Megjegyzés

A `TableColumnItem` elem megadása kötelező a sor minden oszlophoz. Az első bejegyzés jelenik meg az első oszlopban a második bejegyzés a második oszlopban, és így tovább.

A táblázatos nézetre az összetevőivel kapcsolatos további információkért lásd: [tábla nézetek létrehozásával](./creating-a-table-view.md).

## <a name="example"></a>Példa

A következő példa bemutatja egy `TableColumnItems` elem, amely három tulajdonságainak meghatározása a [System.Diagnostics.Process](/dotnet/api/System.Diagnostics.Process) objektum.

```xml
<TableColumnItems>
  <TableColumnItem>
    <PropertyName>Status</PropertyName>
  </TableColumnItem>
  <TableColumnItem>
    <PropertyName>Name</PropertyName>
  </TableColumnItem>
  <TableColumnItem>
    <PropertyName>DisplayName</PropertyName>
  </TableColumnItem>
</TableColumnItems>

```

## <a name="see-also"></a>Lásd még:

[Tábla nézet létrehozása](./creating-a-table-view.md)

[TableColumnItem elem (formátum)](./tablecolumnitem-element-for-tablecolumnitems-for-tablecontrol-format.md)

[TableRowEntry elem (formátum)](./tablerowentry-element-for-tablerowentries-for-tablecontrol-format.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
