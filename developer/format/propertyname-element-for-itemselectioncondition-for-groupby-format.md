---
title: A GroupBy (formátum) ItemSelectionCondition PropertyName eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 221cbdc2-f794-4f3a-9d40-bfdd8cba1013
caps.latest.revision: 6
ms.openlocfilehash: aae65789cf5572cbcc9251eca802a2d43065e49f
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56848397"
---
# <a name="propertyname-element-for-itemselectioncondition-for-groupby-format"></a>A GroupBy elemhez tartozó ItemSelectionCondition PropertyName eleme (Formátum)

Megadja a .NET-tulajdonság, amely elindítja a feltételt. Ha ez a tulajdonság jelen-e, vagy ha való kiértékelése által `true`, a feltétel nem teljesül, és a vezérlő használatos. Ez az elem szolgál, hogyan jelenjen meg az objektumok egy új csoportot meghatározásakor.

Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem GroupBy elem megtekintése (formátum) CustomControl elem a GroupBy (formátum) CustomEntry elemhez tartozó CustomControl GroupBy (formátum) CustomEntries elemhez GroupBy (formátum) CustomItem elem CustomEntry CustomItem ExpressionBinding a GroupBy (formátum) PropertyName elemhez tartozó GroupBy (formátum) ItemSelectionCondition elemhez tartozó GroupBy (formátum) ExpressionBinding elemhez tartozó CustomControl ItemSelectionCondition a GroupBy (formátum)

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
|[A GroupBy (formátum) ExpressionBinding ItemSelectionCondition elem.](./itemselectioncondition-element-for-expressionbinding-for-groupby-format.md)|Határozza meg azt a feltételt, amelyet Pro tento ovládací prvek használandó léteznie kell.|

## <a name="text-value"></a>Szöveges érték

Adja meg a .NET-tulajdonság, amely elindítja a feltétel nevét.

## <a name="remarks"></a>Megjegyzés

Ha ez az elem használata esetén nem adható meg a [ScriptBlock](./scriptblock-element-for-itemselectioncondition-for-groupby-format.md) elemet a kiválasztási feltétel meghatározásakor.

## <a name="see-also"></a>Lásd még:

[ItemSelectionCondition GroupBy (formátum) a scriptblock kulcsszót elem.](./scriptblock-element-for-itemselectioncondition-for-groupby-format.md)

[A GroupBy (formátum) ExpressionBinding ItemSelectionCondition elem.](./itemselectioncondition-element-for-expressionbinding-for-groupby-format.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
