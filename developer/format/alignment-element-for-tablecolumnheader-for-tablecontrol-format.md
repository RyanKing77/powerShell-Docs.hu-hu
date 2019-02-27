---
title: Zarovnání eleme TableColumnHeader TableControl (formátum) a |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: ff85e83a-c9c2-4c37-accc-e6a27c182f3c
caps.latest.revision: 19
ms.openlocfilehash: 16b41535109ca503e679a135f5ba30054e33de5b
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56845240"
---
# <a name="alignment-element-for-tablecolumnheader-for-tablecontrol-format"></a>A TableControl TableColumnHeader elemének igazítási eleme (Formátum)

Határozza meg, hogyan jelenjen meg az adatok egy oszlopfejlécre.

Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézet elem (formátum) TableControl elem (formátum) TableHeaders elem (formátum) TableColumnHeader elem (formátum) igazítás elem a TableColumnHeader (formátum)

## <a name="syntax"></a>Szintaxis

```xml
<Alignment>AlignmentType</Alignment>
```

## <a name="attributes-and-elements"></a>Attribútumok és elemek

A következő szakaszok ismertetik az attribútumokat, gyermekelemek és szülőelemét a `Alignment` elemet.

### <a name="attributes"></a>Attribútumok

Nincs.

### <a name="child-elements"></a>Gyermekelemek

Nincs.

### <a name="parent-elements"></a>Szülőelemek

|Elem|Leírás|
|-------------|-----------------|
|[TableColumnHeader elem (formátum)](./tablecolumnheader-element-format.md)|Egy címke, a szélesség és az adatok egy oszlop a tábla zarovnání határozza meg.|

## <a name="text-value"></a>Szöveges érték

Adja meg a következő értékek egyikét. Ezek az értékek nem különböznek.

Balra igazítása jelennek meg az oszlopot a bal oldali Ez az alapértelmezés szerint ha ez az elem nincs megadva.

Jobbra igazítja az adatok az oszlopban látható a jobb oldalon.

Center központok az oszlopban megjelenített adatokat.

## <a name="remarks"></a>Megjegyzés

A táblázatos nézetre az összetevőivel kapcsolatos további információkért lásd: [tábla nézetek létrehozásával](./creating-a-table-view.md).

## <a name="example"></a>Példa

Ez a példa bemutatja egy `TableColumnHeader` elem, amelynek az adatait a bal oldali van igazítva.

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
