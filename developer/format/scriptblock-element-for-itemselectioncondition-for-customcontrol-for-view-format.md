---
title: ItemSelectionCondition CustomControl nézet (formátum) a scriptblock kulcsszót eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 946cd2b5-ac37-4a13-bb49-29fbc70ec8d7
caps.latest.revision: 6
ms.openlocfilehash: 0c07ab0e5d04c4056a7e7215bfa55773bfccb41d
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56851176"
---
# <a name="scriptblock-element-for-itemselectioncondition-for-customcontrol-for-view-format"></a>A Nézet CustomControl eleméhez tartozó ItemSelectionCondition ScriptBlock eleme (Formátum)

Megadja a parancsprogramot, amely elindítja a feltétel. Ha ez a parancsfájl kiértékelése `true`, a feltétel nem teljesül, és a vezérlő használatos. Ehhez az elemhez használt egyéni vezérlő nézet definiálása.

Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézet elem (formátum) CustomControl elem (formátum) CustomEntries eleme CustomControl megtekintése (formátum) CustomEntry elem megtekintése (formátum) CustomItem elemhez tartozó CustomEntries számára A nézet (formátum) ExpressionBinding elem a CustomItem CustomControl megtekintése (formátum) ScriptBlock elem ItemSelectionCondition az a kifejezés CustomControl kötése a nézet (formátum) ItemSelectionCondition elemhez tartozó CustomEntry CustomControl nézet (formátum)

## <a name="syntax"></a>Szintaxis

```xml
<ScriptBlock>ScriptToEvaluate</ScriptBlock>
```

## <a name="attributes-and-elements"></a>Attribútumok és elemek

A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `ScriptBlock` elemet.

### <a name="attributes"></a>Attribútumok

Nincs.

### <a name="child-elements"></a>Gyermekelemek

Nincs.

### <a name="parent-elements"></a>Szülőelemek

|Elem|Leírás|
|-------------|-----------------|
|[A nézet (formátum) kifejezés CustomControl kötésének ItemSelectionCondition elem](./itemselectioncondition-element-for-expressionbinding-for-customcontrol-format.md)|Határozza meg azt a feltételt, amelyet Pro tento ovládací prvek használandó léteznie kell.|

## <a name="text-value"></a>Szöveges érték

Adja meg a parancsfájl, amely ki lesz értékelve.

## <a name="remarks"></a>Megjegyzés

Ha ez az elem használata esetén nem adható meg a [PropertyName](./propertyname-element-for-itemselectioncondition-for-customcontrol-for-view-format.md) elemet a kiválasztási feltétel meghatározásakor.

## <a name="see-also"></a>Lásd még:

[A nézet (formátum) CustomControl ItemSelectionCondition PropertyName elem.](./propertyname-element-for-itemselectioncondition-for-customcontrol-for-view-format.md)

[A nézet (formátum) kifejezés CustomControl kötésének ItemSelectionCondition elem](./itemselectioncondition-element-for-expressionbinding-for-customcontrol-format.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
