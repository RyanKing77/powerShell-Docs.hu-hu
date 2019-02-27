---
title: (Formátum) TableControl TableRowEntries eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: d10b68ca-256c-4c58-b503-73f7777b39ae
caps.latest.revision: 15
ms.openlocfilehash: d93750f919c1075f173dc9ac70324cc003e36879
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56851141"
---
# <a name="tablerowentries-element-for-tablecontrol-format"></a>A TableControl TableRowEntries eleme (Formátum)

Határozza meg a tábla sorait.

Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem TableControl elem (formátum) TableRowEntries eleme TableControl (formátum)

## <a name="syntax"></a>Szintaxis

```xml
<TableRowEntries>
  <TableRowEntry>...</TableRowEntry>
</TableRowEntries>
```

## <a name="attributes-and-elements"></a>Attribútumok és elemek

A következő szakaszok ismertetik az attribútumokat, gyermekelemek és szülőelemét a `TableRowEntries` elemet.

### <a name="attributes"></a>Attribútumok

Nincs.

### <a name="child-elements"></a>Gyermekelemek

|Elem|Leírás|
|-------------|-----------------|
|[A TableControl (formátum) TableRowEntries TableRowEntry elem.](./tablerowentry-element-for-tablerowentroes-for-tablecontrol-format.md)|Szükséges eleme.<br /><br /> Határozza meg, amely egy sort a táblában megjelennek az adatok.|

### <a name="parent-elements"></a>Szülőelemek

|Elem|Leírás|
|-------------|-----------------|
|[TableControl elem (formátum)](./tablecontrol-element-format.md)|Határozza meg a nézet táblázatos formában.|

## <a name="remarks"></a>Megjegyzés

Meg kell adnia egy vagy több `TableRowEntry` elemei a táblázatos nézetre. Nem maximális korlátozott számú `TableRowEntry` elemeket, amelyeket hozzáadhat se nem jelentős sorrendjét.

A táblázatos nézetre az összetevőivel kapcsolatos további információkért lásd: [tábla nézetek létrehozásával](./creating-a-table-view.md).

## <a name="example"></a>Példa

A következő példa bemutatja egy `TableRowEntries` elem, amely meghatározza egy sort, amely két tulajdonságának értékét jeleníti meg a [System.Diagnostics.Process](/dotnet/api/System.Diagnostics.Process) objektum.

```xml
<TableRowEntries>
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
</TableRowEntries>

```

## <a name="see-also"></a>Lásd még:

[Tábla nézet létrehozása](./creating-a-table-view.md)

[TableControl elem (formátum)](./tablecontrol-element-format.md)

[TableRowEntry elem (formátum)](./tablerowentry-element-for-tablerowentroes-for-tablecontrol-format.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
