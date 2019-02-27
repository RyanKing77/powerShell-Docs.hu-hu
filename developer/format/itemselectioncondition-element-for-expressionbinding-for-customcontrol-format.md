---
title: CustomControl (formátum) a ExpressionBinding ItemSelectionCondition eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: f4bea9d8-27ad-410e-ad48-287f807d3e4e
caps.latest.revision: 7
ms.openlocfilehash: 18b0113c9b7b0895a1093cb0b56cd2d02c74a6c1
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56848341"
---
# <a name="itemselectioncondition-element-for-expressionbinding-for-customcontrol-format"></a>A CustomControl elemhez tartozó ExpressionBinding ItemSelectionCondition eleme (Formátum)

Határozza meg azt a feltételt, amelyet Pro tento ovládací prvek használandó léteznie kell. Van egy vezérlő elemhez megadható kiválasztási feltételek száma nincs korlátozva. Ehhez az elemhez használt egyéni vezérlő nézet definiálása.

Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézet elem (formátum) CustomControl elem (formátum) CustomEntries eleme CustomControl megtekintése (formátum) CustomEntry elem megtekintése (formátum) CustomItem elemhez tartozó CustomEntries számára CustomEntry CustomItem CustomControl megtekintése (formátum) ItemSelectionCondition elemhez tartozó kifejezés kötésének CustomControl nézet (formátum) esetében a nézet (formátum) ExpressionBinding elemhez

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
|[A nézet (formátum CustomControl ItemSelectionCondition PropertyName elem.](./propertyname-element-for-itemselectioncondition-for-customcontrol-for-view-format.md)|Nem kötelező eleme.<br /><br /> Megadja a .NET-tulajdonság, amely elindítja a feltételt.|
|[A nézet (formátum) CustomControl ItemSelectionCondition ScriptBlock eleme](./scriptblock-element-for-itemselectioncondition-for-customcontrol-for-view-format.md)|Nem kötelező eleme.<br /><br /> Megadja a parancsprogramot, amely elindítja a feltétel.|

### <a name="parent-elements"></a>Szülőelemek

|Elem|Leírás|
|-------------|-----------------|
|[A nézet (formátum) CustomControl CustomItem ExpressionBinding elem.](./expressionbinding-element-for-customitem-for-customcontrol-for-view-format.md)|Határozza meg a vezérlő által megjelenített adatokat.|

## <a name="remarks"></a>Megjegyzés

Egy tulajdonság neve vagy az ehhez a feltételhez parancsfájlt is megadhat, de nem adható meg egyszerre.

## <a name="see-also"></a>Lásd még:

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)

[A nézet (formátum) CustomControl CustomItem ExpressionBinding elem.](./expressionbinding-element-for-customitem-for-customcontrol-for-view-format.md)
