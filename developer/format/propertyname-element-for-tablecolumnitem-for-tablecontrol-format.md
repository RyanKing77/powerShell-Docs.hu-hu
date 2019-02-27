---
title: TableColumnItem TableControl (formátum) a PropertyName eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: fb26d72c-2f77-4801-badf-0537ccc55e31
caps.latest.revision: 10
ms.openlocfilehash: 6e86b6a0874b385703121802bc8108a0410442cd
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56849237"
---
# <a name="propertyname-element-for-tablecolumnitem-for-tablecontrol-format"></a>A TableControl TableColumnItem elemének PropertyName eleme (Formátum)

Megadja a tulajdonságot, amelynek értéke megjelenik a sor oszlopában.

Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem TableControl elem (formátum) TableRowEntries elem (formátum) TableRowEntry elem (formátum) TableColumnItems elem (formátum) TableColumnItem elem (formátum) A PropertyName eleme TableColumnItem (formátum)

## <a name="syntax"></a>Szintaxis

```xml
<PropertyName>.NetTypeProperty</PropertyName>
```

## <a name="attributes-and-elements"></a>Attribútumok és elemek

A következő szakaszok ismertetik az attribútumokat, gyermekelemek és szülőelemét a `PropertyName` elemet.

### <a name="attributes"></a>Attribútumok

Nincs.

### <a name="child-elements"></a>Gyermekelemek

Nincs.

### <a name="parent-elements"></a>Szülőelemek

|Elem|Leírás|
|-------------|-----------------|
|[TableColumnItem elem (formátum)](./tablecolumnitem-element-for-tablecolumnitems-for-tablecontrol-format.md)|A tulajdonság, vagy a parancsfájl, amelynek értéke megjelenik a sor oszlop határozza meg.|

## <a name="text-value"></a>Szöveges érték

Adja meg, amelynek értéke megjelenik a tulajdonság nevét.

## <a name="remarks"></a>Megjegyzés

A táblázatos nézetre az összetevőivel kapcsolatos további információkért lásd: [tábla nézetek létrehozásával](./creating-a-table-view.md).

## <a name="example"></a>Példa

Ez a példa bemutatja egy `TableColumnItem` elem, amely meghatározza a `Status` tulajdonságát a [System.Diagnostics.Process](/dotnet/api/System.Diagnostics.Process) objektum.

```xml
<TableColumnItem>
   <Alignment>Centered</Alignment>
  <PropertyName>Status</PropertyName>
</TableColumnItem>

```

## <a name="see-also"></a>Lásd még:

[Tábla nézet létrehozása](./creating-a-table-view.md)

[TableColumnItem elem (formátum)](./tablecolumnitem-element-for-tablecolumnitems-for-tablecontrol-format.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
