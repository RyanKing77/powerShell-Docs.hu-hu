---
title: A nézet (formátum) CustomControl ItemSelectionCondition PropertyName eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: f2b12006-8d52-486b-91a3-e6224ca80e56
caps.latest.revision: 6
ms.openlocfilehash: 52d0b0816eaef6752220e0c3b1249e5a0e44a3ee
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56845961"
---
# <a name="propertyname-element-for-itemselectioncondition-for-customcontrol-for-view-format"></a>A Nézet CustomControl eleméhez tartozó ItemSelectionCondition PropertyName eleme (Formátum)

Megadja a .NET-tulajdonság, amely elindítja a feltételt. Ha ez a tulajdonság jelen-e, vagy ha való kiértékelése által `true`, a feltétel nem teljesül, és a vezérlő használatos. Ehhez az elemhez használt egyéni vezérlő nézet definiálása.

Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézet elem (formátum) CustomControl elem (formátum) CustomEntries eleme CustomControl megtekintése (formátum) CustomEntry elem megtekintése (formátum) CustomItem elemhez tartozó CustomEntries számára A nézet (formátum) ItemSelectionCondition elemhez tartozó kifejezés kötésének CustomControl megtekintése (formátum) PropertyName elemhez tartozó ItemSelectionCondition a CustomControl CustomItem a nézet (formátum) ExpressionBinding elemhez CustomEntry CustomControl nézet (formátum

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
|[A nézet (formátum) kifejezés CustomControl kötésének ItemSelectionCondition elem](./itemselectioncondition-element-for-expressionbinding-for-customcontrol-format.md)|Határozza meg azt a feltételt, amelyet Pro tento ovládací prvek használandó léteznie kell.|

## <a name="text-value"></a>Szöveges érték

Adja meg a .NET-tulajdonság, amely elindítja a feltétel nevét.

## <a name="remarks"></a>Megjegyzés

Ha ez az elem használata esetén nem adható meg a [ScriptBlock](./scriptblock-element-for-itemselectioncondition-for-customcontrol-for-view-format.md) elemet a kiválasztási feltétel meghatározásakor.

## <a name="see-also"></a>Lásd még:

[A nézet (formátum) CustomControl ItemSelectionCondition ScriptBlock eleme](./scriptblock-element-for-itemselectioncondition-for-customcontrol-for-view-format.md)

[A nézet (formátum) kifejezés CustomControl kötésének ItemSelectionCondition elem](./itemselectioncondition-element-for-expressionbinding-for-customcontrol-format.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
