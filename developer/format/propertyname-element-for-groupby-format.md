---
title: A PropertyName elemet a GroupBy (formátum) |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: ddcecc46-ac75-43fa-b03a-802a68524ec3
caps.latest.revision: 10
ms.openlocfilehash: da6ac5abe7acbbee8f57b3e81529664f81800b86
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56851897"
---
# <a name="propertyname-element-for-groupby-format"></a>A GroupBy PropertyName eleme (Formátum)

Megadja a .NET-tulajdonságot, amely elindít egy új csoportot, amikor annak értéke módosul.

Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem GroupBy elem megtekintése (formátum) PropertyName elemhez tartozó GroupBy (formátum)

## <a name="syntax"></a>Szintaxis

```xml
<PropertyName>.NetTypeProperty</PropertyName>
```

## <a name="attributes-and-elements"></a>Attribútumok és elemek

A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `PropertyName` elemet.

### <a name="attributes"></a>Attribútumok

Nincs.

### <a name="child-elements"></a>Gyermekelemek

Nincs.

### <a name="parent-elements"></a>Szülőelemek

|Elem|Leírás|
|-------------|-----------------|
|[GroupBy elem nézet (formátum)](./groupby-element-for-view-format.md)|Határozza meg, hogyan jelenjen meg a .NET-objektumokká csoportja.|

## <a name="text-value"></a>Szöveges érték

Adja meg a .NET-tulajdonság neve.

## <a name="remarks"></a>Megjegyzés

Windows PowerShell elindul egy új csoportot, ha a ennek a tulajdonságnak az értéke módosul.

Ha ez az elem meg van adva, nem adható meg a [ScriptBlock](./scriptblock-element-for-groupby-format.md) elem elindítani egy új csoportot.

## <a name="example"></a>Példa

Az alábbi példa bemutatja, hogyan indítható egy új csoportot, ha egy tulajdonság értékét módosítja.

```xml
<GroupBy>
  <Label>Service Type</Label>
  <PropertyName>ServiceType</PropertyName>
</GroupBy>

```

A teljes formázási fájl tartalmazza ezt az elemet egy példa: [széles nézet (GroupBy)](./wide-view-groupby.md).

## <a name="see-also"></a>Lásd még:

[GroupBy elem nézet (formátum)](./groupby-element-for-view-format.md)

[GroupBy (formátum) a scriptblock kulcsszót elem](./scriptblock-element-for-groupby-format.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
