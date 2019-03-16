---
title: TableColumnHeader elem (formátum) |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 49ff3062-6396-4aa8-919b-3fd3ac60899a
caps.latest.revision: 19
ms.openlocfilehash: d3ad7fa563def17d43ce4dc64d155b65b650521f
ms.sourcegitcommit: caac7d098a448232304c9d6728e7340ec7517a71
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/16/2019
ms.locfileid: "58057875"
---
# <a name="tablecolumnheader-element-format"></a>TableColumnHeader elem (Formátum)

A címke, az oszlopok szélességét és a egy oszlop a tábla a címke zarovnání határozza meg.

Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem TableControl elem (formátum) TableHeaders elem TableControl (formátum) TableColumnHeader elemhez tartozó TableHeaders TableControl (formátum) a

## <a name="syntax"></a>Szintaxis

```xml
<TableColumnHeader>
  <Label>DisplayedLabel</Label>
  <Width>NumberOfCharacters</Width>
  <Alignment>Left, Right, or Centered</Alignment>
</TableColumnHeader>
```

## <a name="attributes-and-elements"></a>Attribútumok és elemek

A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `TableColumnHeader` elemet.

### <a name="attributes"></a>Attribútumok

Nincs.

### <a name="child-elements"></a>Gyermekelemek

|Elem|Leírás|
|-------------|-----------------|
|[Címke eleme TableColumnHeader a TableControl (formátum)](./label-element-for-tablecolumnheader-for-tablecontrol-format.md)|Nem kötelező eleme.<br /><br /> Határozza meg a címke az az oszlop tetején jelenik meg. Ha nincs címke van megadva, a tulajdonságot, amelynek az értéke megjelenik a sorok nevét használja.|
|[Szélesség eleme TableColumnHeader a TableControl (formátum)](./width-element-for-tablecolumnheader-for-tablecontrol-format.md)|Szükséges eleme.<br /><br /> Adja meg az oszlop szélessége (a karakter).|
|[Zarovnání eleme TableColumnHeader a TableControl (formátum)](./alignment-element-for-tablecolumnheader-for-tablecontrol-format.md)|Nem kötelező eleme.<br /><br /> Itt adhatja meg, hogyan jelenjen meg az oszlop a címkét. Ha igazítás nélkül van megadva, a címke a bal oldali van igazítva.|

### <a name="parent-elements"></a>Szülőelemek

|Elem|Leírás|
|-------------|-----------------|
|[TableHeaders elem (formátum)](./tableheaders-element-format.md)|Határozza meg az oszlopok számos táblázatos nézetre.|

## <a name="remarks"></a>Megjegyzés

Adja meg a tábla minden oszlopához fejlécét. Az oszlopok jelennek meg a sorrendet, amely a `TableColumnHeader` elemek vannak definiálva.

Egy táblának rendelkeznie kell azonos számú `TableColumnHeader` az elemek `TableRowEntry` elemeket. Az oszlop fejlécére határozza meg, hogyan jelenjen meg a tábla tetején lévő szöveg. A sor bejegyzések határozza meg, hogy milyen adatok jelenjenek meg a tábla sorait.

A táblázatos nézetre az összetevőivel kapcsolatos további információkért lásd: [táblázatos nézetre](./creating-a-table-view.md).

## <a name="example"></a>Példa

A következő példában két `TableColumnHeader` elemeket. Az első elemét határozza meg egy olyan oszlop, amelynek címke "1. oszlop", 16 karakterből álló szélessége és amelynek címke van igazítva a bal oldali. A második elem oszlop határozza meg, amelynek címke "2. oszlop", a 10 karakterből álló szélessége, és amelynek felirat az oszlopban közepén.

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

[Zarovnání eleme TableColumnHeader a TableControl (formátum)](./alignment-element-for-tablecolumnheader-for-tablecontrol-format.md)

[Tábla nézet létrehozása](./creating-a-table-view.md)

[Címke eleme TableColumnHeader a TableControl (formátum)](./label-element-for-tablecolumnheader-for-tablecontrol-format.md)

[TableHeaders eleme TableControl (formátum)](./tableheaders-element-format.md)

[TableColumnHeader TableControl elemhez (formátum) esetén a szélesség](./width-element-for-tablecolumnheader-for-tablecontrol-format.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
