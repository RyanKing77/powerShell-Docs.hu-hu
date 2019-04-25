---
title: ItemSelectionCondition elemet a vezérlők (formátum) konfiguráció ExpressionBinding |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: fd3ddc33-b21c-4464-b3f2-a78dbe0062a8
caps.latest.revision: 8
ms.openlocfilehash: 4865d716ebe0460b662253a3019e93e82428b882
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62065509"
---
# <a name="itemselectioncondition-element-for-expressionbinding-for-controls-for-configuration-format"></a>A Konfiguráció Vezérlők eleméhez tartozó ExpressionBinding ItemSelectionCondition eleme (Formátum)

Határozza meg azt a feltételt, amelyet Pro tento ovládací prvek használandó léteznie kell. Ez az elem szolgál egy közös vezérlőelem a formázási fájlban az összes nézetek által használható meghatározásakor.

Konfigurációs elem (formátum) vezérlők elem Configuration (formátum) vezérlőelem elem vezérlők, a vezérlő konfigurációs (formátum) CustomEntries elemhez tartozó CustomControl Configuration (a Configuration (formátum) CustomControl elem Formátum) CustomEntry elemet a vezérlők, a vezérlők, a konfiguráció ExpressionBinding elem CustomItem vezérlők (formátum) konfiguráció esetén a CustomEntry Configuration (formátum) CustomItem elemhez CustomControl Konfiguráció (formátum) vezérlők ExpressionBinding ItemSelectionCondition elem.

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
|[Konfiguráció (formátum) vezérlők ItemSelectionCondition PropertyName elem.](./propertyname-element-for-itemseclectioncondition-for-controls-for-configuration-format.md)|Nem kötelező eleme.<br /><br /> Megadja a .NET-tulajdonság, amely elindítja a feltételt.|
|[Konfiguráció (formátum) vezérlők ItemSelectionCondition ScriptBlock eleme](./scriptblock-element-for-itemseclectioncondition-for-controls-for-configuration-format.md)|Nem kötelező eleme.<br /><br /> Megadja a parancsprogramot, amely elindítja a feltétel.|

### <a name="parent-elements"></a>Szülőelemek

|Elem|Leírás|
|-------------|-----------------|
|[Konfiguráció (formátum) vezérlők CustomItem ExpressionBinding elem.](./expressionbinding-element-for-customitem-for-controls-for-configuration-format.md)|Határozza meg a vezérlő által megjelenített adatokat.|

## <a name="remarks"></a>Megjegyzés

Egy tulajdonság neve vagy az ehhez a feltételhez parancsfájlt is megadhat, de nem adható meg egyszerre.

## <a name="see-also"></a>Lásd még:

[Konfiguráció (formátum) vezérlők ItemSelectionCondition PropertyName elem.](./propertyname-element-for-itemseclectioncondition-for-controls-for-configuration-format.md)

[Konfiguráció (formátum) vezérlők ItemSelectionCondition ScriptBlock eleme](./scriptblock-element-for-itemseclectioncondition-for-controls-for-configuration-format.md)

[Konfiguráció (formátum) vezérlők CustomItem ExpressionBinding elem.](./expressionbinding-element-for-customitem-for-controls-for-configuration-format.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
