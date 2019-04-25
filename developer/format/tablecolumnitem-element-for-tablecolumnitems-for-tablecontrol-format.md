---
title: TableControl (formátum) a TableColumnItems TableColumnItem eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: ef8395aa-4b31-48c0-a0b8-b481fd0b3738
caps.latest.revision: 15
ms.openlocfilehash: 159f943f6bfb33c5403b5714380631351523789f
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62063938"
---
# <a name="tablecolumnitem-element-for-tablecolumnitems-for-tablecontrol-format"></a>A TableControl TableColumnItems elemének TableColumnItem eleme (Formátum)

A tulajdonság, vagy a parancsfájl, amelynek értéke megjelenik a sor oszlop határozza meg.

Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem TableControl elem (formátum) TableRowEntries elem TableControl (formátum) TableRowEntry elemhez tartozó TableRowEntries TableControl (formátum) a TableControl (formátum) TableColumnItem elemhez tartozó TableColumnItems TableControl (formátum) a TableControlEntry TableColumnItems elem.

## <a name="syntax"></a>Szintaxis

```xml
<TableColumnItem>
  <Alignment>Left, Right, or Center</Alignment>
  <PropertyName>Nameof.NetProperty</PropertyName>
  <ScriptBlock>ScriptToEvaluate</ScriptBlock>
</TableColumnItem>
```

## <a name="attributes-and-elements"></a>Attribútumok és elemek

A következő szakaszok ismertetik az attribútumokat, gyermekelemek és szülőelemét a `TableColumnItem` elemet.

### <a name="attributes"></a>Attribútumok

Nincs.

### <a name="child-elements"></a>Gyermekelemek

|Elem|Leírás|
|-------------|-----------------|
|[Zarovnání eleme TableColumnItem a TableControl (formátum)](./alignment-element-for-tablecolumnitem-for-tablecontrol-format.md)|Nem kötelező eleme.<br /><br /> Határozza meg, hogyan jelenjen meg a sor egy oszlopban lévő adatokat.|
|[TableColumnItem TableControl (formátum) a FormatString elem.](./formatstring-element-for-tablecolumnitem-for-tablecontrol-format.md)|Megadja a sor az oszlopban lévő adatok formázásához használt formátum mintát.|
|[TableColumnItem TableControl (formátum) a PropertyName elem.](./propertyname-element-for-tablecolumnitem-for-tablecontrol-format.md)|Nem kötelező eleme.<br /><br /> Meghatározza a tulajdonságot, amelynek értéke megjelenik a nevét.|
|[TableColumnItem TableControl (formátum) a scriptblock kulcsszót elem.](./scriptblock-element-for-tablecolumnitem-for-tablecontrol-format.md)|Nem kötelező eleme.<br /><br /> Megadja a parancsprogramot, amelynek az értéke az oszlop egy sor jelenik meg.|

### <a name="parent-elements"></a>Szülőelemek

|Elem|Leírás|
|-------------|-----------------|
|[A TableControl (formátum) TableControlEntry TableColumnItems elem.](./tablecolumnitems-element-for-tablerowentry-for-tablecontrol-format.md)|Határozza meg a Tulajdonságok vagy parancsfájlok, melynek értékei jelennek meg a sorban.|

## <a name="remarks"></a>Megjegyzés

A sor összes oszlopában egy tulajdonságát egy objektum vagy egy parancsfájlt is megadhat. Ha nincs alárendelt elem meg van adva, az elem nem egy helyőrző és adatok nem van megjelenítve.

A táblázatos nézetre az összetevőivel kapcsolatos további információkért lásd: [tábla nézetek létrehozásával](./creating-a-table-view.md).

## <a name="example"></a>Példa

Ez a példa bemutatja egy `TableColumnItem` elem, amely értékét jeleníti meg a `Status` tulajdonságát a [System.Diagnostics.Process](/dotnet/api/System.Diagnostics.Process) objektum.

```xml
<TableColumnItem>
   <Alignment>Centered</Alignment>
  <PropertyName>Status</PropertyName>
</TableColumnItem>

```

## <a name="see-also"></a>Lásd még:

[Tábla nézet létrehozása](./creating-a-table-view.md)

[Zarovnání eleme TableColumnItem a TableControl (formátum)](./alignment-element-for-tablecolumnitem-for-tablecontrol-format.md)

[TableColumnItems elem (formátum)](./tablecolumnitems-element-for-tablerowentry-for-tablecontrol-format.md)

[TableColumnItem TableControl (formátum) a FormatString elem.](./formatstring-element-for-tablecolumnitem-for-tablecontrol-format.md)

[TableColumnItem TableControl (formátum) a PropertyName elem.](./propertyname-element-for-tablecolumnitem-for-tablecontrol-format.md)

[TableColumnItem TableControl (formátum) a scriptblock kulcsszót elem.](./scriptblock-element-for-tablecolumnitem-for-tablecontrol-format.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
