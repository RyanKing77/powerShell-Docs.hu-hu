---
title: Listaelem ListControl (formátum) a PropertyName eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 01ae8cbe-acdc-4043-bd6e-1118a5691a55
caps.latest.revision: 12
ms.openlocfilehash: 405184f7bdbf1955f1df7766bf2723c244dcc27f
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56846626"
---
# <a name="propertyname-element-for-listitem-for-listcontrol-format"></a>A ListControl elemhez tartozó ListItem PropertyName eleme (Formátum)

Megadja a .NET-tulajdonságot, amelynek értéke megjelenik a listában.

Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézet elem (formátum) ListControl elem (formátum) ListEntries elem (formátum) ListEntry elem (formátum) ListItems elemek elem (formátum) ListItem elem (formátum) PropertyName elem számára Listaelem (formátum)

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
|[Listaelem elem (formátum)](./listitem-element-for-listitems-for-listcontrol-format.md)|A tulajdonság, vagy a parancsfájl, amelynek értéke megjelenik a lista nézet sorában határoz meg.|

## <a name="text-value"></a>Szöveges érték

Adja meg, amelynek értéke megjelenik a tulajdonság nevét.

## <a name="remarks"></a>Megjegyzés

Ha ez az elem meg van adva, nem adható meg a [ScriptBlock](./scriptblock-element-for-listitem-for-listcontrol-format.md) elemet.

Mellett megjelenítése a tulajdonság értéke, egy címke vagy egy formázó karakterlánc, amely segítségével a érték jelenjen meg az értéket is megadhatja. Lista nézetben adatok megadásával kapcsolatos további információkért lásd: [lista nézet létrehozásával](./creating-a-list-view.md).

## <a name="example"></a>Példa

Az alábbi példa bemutatja, hogyan adhatja meg a címke és a tulajdonságot, amelynek értéke megjelenik.

```xml
ListItem>
  <Label>NameOfProperty</Label>
  <PropertyName>.NetTypeProperty</PropertyName>
</ListItem>

```

## <a name="see-also"></a>Lásd még:

[Listaelem ListControl (formátum) a scriptblock kulcsszót elem.](./scriptblock-element-for-listitem-for-listcontrol-format.md)

[Lista nézet létrehozása](./creating-a-list-view.md)

[ListControl(Format) ListItem elem.](./listitem-element-for-listitems-for-listcontrol-format.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
