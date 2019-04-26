---
title: Címke elem a TableColumnHeader TableControl (formátum) a |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 7196f039-2f6a-41fd-b252-5b1623ebb9f9
caps.latest.revision: 11
ms.openlocfilehash: 09183a538c179f19347c3f1ed45b4ad38c2ca451
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62065750"
---
# <a name="label-element-for-tablecolumnheader-for-tablecontrol-format"></a>A TableControl TableColumnHeader elemének Címke eleme (Formátum)

Határozza meg a címke az oszlop tetején jelenik meg. Ez az elem szolgál a táblázatos nézetre meghatározásakor.

Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézet elem (formátum) TableControl elem (formátum) TableHeaders elem TableControl (formátum) TableColumnHeader elem a TableHeaders TableControl (formátum) címke elem számára TableColumnHeader a TableControl (formátum)

## <a name="syntax"></a>Szintaxis

```xml
<Label>DisplayedLabel</Label>

```

## <a name="attributes-and-elements"></a>Attribútumok és elemek

A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `Label` elemet. Csak egy címke minden oszlophoz engedélyezett.

### <a name="attributes"></a>Attribútumok

Nincs.

### <a name="child-elements"></a>Gyermekelemek

Nincs.

### <a name="parent-elements"></a>Szülőelemek

|Elem|Leírás|
|-------------|-----------------|
|[A TableControl (formátum) TableHeaders TableColumnHeader elem.](./tablecolumnheader-element-format.md)|Egy címke, a szélesség és az adatok egy oszlop a tábla zarovnání határozza meg.|

## <a name="text-value"></a>A szöveges érték

Adja meg az oszlop a tábla tetején megjelenő szöveg. Nem áll a korlátozott karakter oszlop címkére.

## <a name="remarks"></a>Megjegyzés

Ha nincs címke van megadva, a tulajdonságot, amelynek az értéke megjelenik a sorok nevét használja.

A táblázatos nézetre az összetevőivel kapcsolatos további információkért lásd: [tábla nézetek létrehozásával](./creating-a-table-view.md).

## <a name="example"></a>Példa

Ez a példa bemutatja egy `TableColumnHeader` elem, amelynek címkét az "1. oszlop".

```xml
<TableColumnHeader>
  <Label>Column 1</Label)
  <Width>16</Width>
  <Alignment>Left</Alignment>
</TableColumnHeader>
```

## <a name="see-also"></a>Lásd még:

[Tábla nézet létrehozása](./creating-a-table-view.md)

[TableColumnHeader elem (formátum)](./tablecolumnheader-element-format.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
