---
title: Szélesség eleme TableColumnHeader TableControl (formátum) a |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 94eb0535-8002-4f17-9a2b-4be75ec20e5c
caps.latest.revision: 18
ms.openlocfilehash: 4a25c9d81df670dc10955065bfb66766cdb1bd33
ms.sourcegitcommit: caac7d098a448232304c9d6728e7340ec7517a71
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/16/2019
ms.locfileid: "58055189"
---
# <a name="width-element-for-tablecolumnheader-for-tablecontrol-format"></a>A TableControl TableColumnHeader elemének Szélesség eleme (Formátum)

Határozza meg az oszlopok szélességét (a karakter).

Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézet elem (formátum) TableControl elem (formátum) TableHeaders eleme TableControl (formátum) TableColumnHeader elem TableHeaders TableControl (formátum) szélesség elem számára TableColumnHeader a TableControl (formátum)

## <a name="syntax"></a>Szintaxis

```xml
<Width>NumberOfCharacters</Width>
```

## <a name="attributes-and-elements"></a>Attribútumok és elemek

A következő szakaszok ismertetik az attribútumokat, gyermekelemek és szülőelemét a `Width` elem oszlopfejlécek meghatározásakor.

### <a name="attributes"></a>Attribútumok

Nincs.

### <a name="child-elements"></a>Gyermekelemek

Nincs.

### <a name="parent-elements"></a>Szülőelemek

|Elem|Leírás|
|-------------|-----------------|
|[A TableControl (formátum) TableHeaders TableColumnHeader elem.](./tablecolumnheader-element-format.md)|Határozza meg, egy címke, a szélesség és a egy oszlop a tábla adatai igazítását.|

## <a name="text-value"></a>Szöveges érték

Amikor csak lehet, adja meg, amely nagyobb, mint a megjelenített tulajdonságértékek hossza szélessége (a karakter).

## <a name="remarks"></a>Megjegyzés

A táblázatos nézetre az összetevőivel kapcsolatos további információkért lásd: [tábla nézetek létrehozásával](./creating-a-table-view.md).

## <a name="example"></a>Példa

A következő példa bemutatja egy `TableColumnHeader` elem, amelynek 16 karakternél.

```xml
<TableColumnHeader>
  <Label>Column 1</Label)
  <Width>16</Width>
  <Alignment>Left</Alignment>
</TableColumnHeader>
```

## <a name="see-also"></a>Lásd még:

[Tábla nézet létrehozása](./creating-a-table-view.md)

[A TableControl (formátum) TableHeader TableColumnHeader elem.](./tablecolumnheader-element-format.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
