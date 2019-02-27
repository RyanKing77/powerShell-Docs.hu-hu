---
title: ScriptBlock elemet a vezérlők (formátum) konfiguráció ItemSeclectionCondition |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 51f7aec9-7b01-4370-84f4-1e58508a851f
caps.latest.revision: 6
ms.openlocfilehash: e92b2dfff07358132c480c47c34279e5365fe400
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56850910"
---
# <a name="scriptblock-element-for-itemseclectioncondition-for-controls-for-configuration-format"></a>A Konfiguráció Vezérlők eleméhez tartozó ItemSelectionCondition ScriptBlock eleme (Formátum)

Megadja a parancsprogramot, amely elindítja a feltétel. Ha ez a parancsfájl kiértékelése `true`, a feltétel nem teljesül, és a vezérlő használatos. Ez az elem szolgál egy közös vezérlőelem a formázási fájlban az összes nézetek által használható meghatározásakor.

Konfigurációs elem (formátum) vezérlők elem Configuration (formátum) vezérlőelem elem vezérlők, a vezérlő konfigurációs (formátum) CustomEntries elemhez tartozó CustomControl Configuration (a Configuration (formátum) CustomControl elem Formátum) CustomEntry elemet a vezérlők, a vezérlők, a konfiguráció ExpressionBinding elem CustomItem vezérlők (formátum) konfiguráció esetén a CustomEntry Configuration (formátum) CustomItem elemhez CustomControl Vezérlők ItemSelectionCondition vezérlők (formátum) konfiguráció esetén a Configuration (formátum) ScriptBlock elemhez ExpressionBinding ItemSelectionCondition elem.

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
|[Konfiguráció (formátum) vezérlők ExpressionBinding ItemSelectionCondition elem.](./itemselectioncondition-element-for-expressionbinding-for-controls-for-configuration-format.md)|Határozza meg azt a feltételt, amelyet Pro tento ovládací prvek használandó léteznie kell.|

## <a name="text-value"></a>Szöveges érték

Adja meg a parancsfájl, amely ki lesz értékelve.

## <a name="remarks"></a>Megjegyzés

Ha ez az elem használata esetén nem adható meg a [PropertyName](./propertyname-element-for-itemseclectioncondition-for-controls-for-configuration-format.md) elemet a kiválasztási feltétel meghatározásakor.

## <a name="see-also"></a>Lásd még:

[Konfiguráció (formátum) vezérlők ItemSeclectionCondition PropertyName elem.](./propertyname-element-for-itemseclectioncondition-for-controls-for-configuration-format.md)

[Konfiguráció (formátum) vezérlők ExpressionBinding ItemSelectionCondition elem.](./itemselectioncondition-element-for-expressionbinding-for-controls-for-configuration-format.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
