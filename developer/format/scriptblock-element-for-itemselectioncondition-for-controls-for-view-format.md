---
title: ScriptBlock elemet a vezérlők (formátum) nézet ItemSelectionCondition |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: b4191157-bf01-4831-b221-6f8cc581cd53
caps.latest.revision: 6
ms.openlocfilehash: 0cbefbb48427b56d4ae2a5ae27c7726dcfad7b84
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56847326"
---
# <a name="scriptblock-element-for-itemselectioncondition-for-controls-for-view-format"></a>A Nézet Vezérlők eleméhez tartozó ItemSelectionCondition ScriptBlock eleme (Formátum)

Megadja a parancsprogramot, amely elindítja a feltétel. Ha ez a parancsfájl kiértékelése `true`, a feltétel nem teljesül, és a vezérlő használatos. Ez az elem szolgál a nézet által használható vezérlők meghatározásakor.

Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem vezérlők elem (formátum) vezérlőelem elem vezérlők, a nézet (formátum) CustomControl elem megtekintése (formátum) CustomEntries elemet a vezérlők a vezérlő A nézet (formátum) CustomEntry elem CustomEntries vezérlők, a vezérlők, a vezérlők (formátum) nézet CustomItem megtekintése (formátum) ExpressionBinding elemhez CustomEntry megtekintése (formátum) CustomItem elemhez tartozó CustomControl Vezérlők megtekintése (formátum) ScriptBlock elem a vezérlők (formátum) nézet ItemSelectionCondition ExpressionBinding ItemSelectionCondition eleme

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
|[Nézet (formátum) vezérlők ExpressionBinding ItemSelectionCondition eleme](./itemselectioncondition-element-for-expressionbinding-for-controls-for-view-format.md)|Határozza meg azt a feltételt, amelyet Pro tento ovládací prvek használandó léteznie kell.|

## <a name="text-value"></a>Szöveges érték

Adja meg a parancsfájl, amely ki lesz értékelve.

## <a name="remarks"></a>Megjegyzés

Ha ez az elem használata esetén nem adható meg a [PropertyName](./propertyname-element-for-itemselectioncondition-for-controls-for-view-format.md) elemet a kiválasztási feltétel meghatározásakor.

## <a name="see-also"></a>Lásd még:

[A PropertyName eleme ItemSelectionCondition vezérlők nézet (formátum)](./propertyname-element-for-itemselectioncondition-for-controls-for-view-format.md)

[Nézet (formátum) vezérlők ExpressionBinding ItemSelectionCondition eleme](./itemselectioncondition-element-for-expressionbinding-for-controls-for-view-format.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
