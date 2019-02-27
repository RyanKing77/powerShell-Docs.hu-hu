---
title: ItemSelectionCondition elemet a vezérlők (formátum) nézet ExpressionBinding |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 82c15014-2440-410d-b02d-b7f1a49240a0
caps.latest.revision: 7
ms.openlocfilehash: 80f375c53c205c793600655fa6031d114871618e
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56850903"
---
# <a name="itemselectioncondition-element-for-expressionbinding-for-controls-for-view-format"></a>A Nézet Vezérlők eleméhez tartozó ExpressionBinding ItemSelectionCondition eleme (Formátum)

Határozza meg azt a feltételt, amelyet Pro tento ovládací prvek használandó léteznie kell. Ez az elem szolgál a nézet által használható vezérlők meghatározásakor.

Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem vezérlők elem (formátum) vezérlőelem elem vezérlők, a nézet (formátum) CustomControl elem megtekintése (formátum) CustomEntries elemet a vezérlők a vezérlő A nézet (formátum) CustomEntry elem CustomEntries vezérlők, a vezérlők, a vezérlők (formátum) nézet CustomItem megtekintése (formátum) ExpressionBinding elemhez CustomEntry megtekintése (formátum) CustomItem elemhez tartozó CustomControl Nézet (formátum) vezérlők ExpressionBinding ItemSelectionCondition eleme

## <a name="syntax"></a>Szintaxis

```xml
<ItemSelectionCondition>
  <PropertyName>.NetTypeProperty</PropertyName>
  <ScriptBlock>ScriptToEvaluate</ScriptBlock>
</ItemSelectionCondition>
```

## <a name="attributes-and-elements"></a>Attribútumok és elemek

A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `ItemSelectionCondition` elemet.

### <a name="attributes"></a>Attribútumok

Nincs.

### <a name="child-elements"></a>Gyermekelemek

|Elem|Leírás|
|-------------|-----------------|
|[A PropertyName eleme ItemSelectionCondition vezérlők nézet (formátum)](./propertyname-element-for-itemselectioncondition-for-controls-for-view-format.md)|Nem kötelező eleme.<br /><br /> Megadja a .NET-tulajdonság, amely elindítja a feltételt.|
|[Nézet (formátum) vezérlők ItemSelectionCondition ScriptBlock elem.](./scriptblock-element-for-itemselectioncondition-for-controls-for-view-format.md)|Nem kötelező eleme.<br /><br /> Megadja a parancsprogramot, amely elindítja a feltétel.|

### <a name="parent-elements"></a>Szülőelemek

|Elem|Leírás|
|-------------|-----------------|
|[Nézet (formátum) vezérlők CustomItem ExpressionBinding elem.](./expressionbinding-element-for-customitem-for-controls-for-view-format.md)|Határozza meg a vezérlő által megjelenített adatokat.|

## <a name="remarks"></a>Megjegyzés

Egy tulajdonság neve vagy az ehhez a feltételhez parancsfájlt is megadhat, de nem adható meg egyszerre.

## <a name="see-also"></a>Lásd még:

[A PropertyName eleme ItemSelectionCondition vezérlők nézet (formátum)](./propertyname-element-for-itemselectioncondition-for-controls-for-view-format.md)

[Nézet (formátum) vezérlők ItemSelectionCondition ScriptBlock elem.](./scriptblock-element-for-itemselectioncondition-for-controls-for-view-format.md)

[Nézet (formátum) vezérlők CustomItem ExpressionBinding elem.](./expressionbinding-element-for-customitem-for-controls-for-view-format.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
