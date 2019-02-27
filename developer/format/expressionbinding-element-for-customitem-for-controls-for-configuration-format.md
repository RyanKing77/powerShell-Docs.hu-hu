---
title: ExpressionBinding elemet a vezérlők (formátum) konfiguráció CustomItem |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: c6649d07-4762-4602-9b4b-d9e2e9e63312
caps.latest.revision: 13
ms.openlocfilehash: 531ff447f8407a737131a38351d7e4c6e7da90fb
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56846206"
---
# <a name="expressionbinding-element-for-customitem-for-controls-for-configuration-format"></a>A Konfiguráció Vezérlők eleméhez tartozó CustomItem ExpressionBinding eleme (Formátum)

Határozza meg a vezérlő által megjelenített adatokat. Ez az elem szolgál egy közös vezérlőelem a formázási fájlban az összes nézetek által használható meghatározásakor.

Konfigurációs elem (formátum) vezérlők elem Configuration (formátum) vezérlőelem elem vezérlők, a vezérlő konfigurációs (formátum) CustomEntries elemhez tartozó CustomControl Configuration (a Configuration (formátum) CustomControl elem Formátum) CustomEntry elemet a vezérlők, a vezérlők, a konfiguráció ExpressionBinding elem CustomItem vezérlők (formátum) konfiguráció esetén a CustomEntry Configuration (formátum) CustomItem elemhez CustomControl

## <a name="syntax"></a>Szintaxis

```xml
<ExpressionBinding>
  <CustomControl>...</CustomControl>
  <CustomControlName>NameofCommonCustomControl</CustomControlName>
  <EnumerateCollection/>
  <ItemSelectionCondition>...</ItemSelectionCondition>
  <PropertyName>Nameof.NetTypeProperty</PropertyName>
  <ScriptBlock>ScriptToEvaluate></ScriptBlock>
</ExpressionBinding>
```

## <a name="attributes-and-elements"></a>Attribútumok és elemek

A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `ExpressionBinding` elemet.

### <a name="attributes"></a>Attribútumok

Nincs.

### <a name="child-elements"></a>Gyermekelemek

|Elem|Leírás|
|-------------|-----------------|
|`CustomControl Element`|Nem kötelező eleme.<br /><br /> Határozza meg olyan vezérlő, amely használja ezt a vezérlőt.|
|[Konfiguráció (formátum) vezérlők ExpressionBinding CustomControlName elem.](./customcontrolname-element-for-expressionbinding-for-controls-for-configuration-format.md)|Nem kötelező eleme.<br /><br /> Megadja egy közös vezérlőelem vagy a nézet nevét.|
|[Konfiguráció (formátum) vezérlők ExpressionBinding EnumerateCollection elem.](./enumeratecollection-element-for-expressionbinding-for-controls-for-configuration-format.md)|Nem kötelező eleme.<br /><br /> A megadott, hogy az elemek a gyűjtemények jelennek meg a vezérlő által.|
|[Konfiguráció (formátum) vezérlők ExpressionBinding ItemSelectionCondition elem.](./itemselectioncondition-element-for-expressionbinding-for-controls-for-configuration-format.md)|Nem kötelező eleme.<br /><br /> Határozza meg azt a feltételt, amelyet a használt gyakori vezérlőelemnél léteznie kell.|
|[Konfiguráció (formátum) vezérlők ExpressionBinding PropertyName elem.](./propertyname-element-for-expressionbinding-for-controls-for-configuration-format.md)|Nem kötelező eleme.<br /><br /> Megadja a .NET tulajdonságot, amelynek értéke megjelenik a közös felügyelete által.|
|[Konfiguráció (formátum) vezérlők ExpressionBinding ScriptBlock eleme](./scriptblock-element-for-expressionbinding-for-controls-for-configuration-format.md)|Nem kötelező eleme.<br /><br /> Megadja a parancsprogramot, amelynek értéke megjelenik a közös felügyelete által.|

### <a name="parent-elements"></a>Szülőelemek

|Elem|Leírás|
|-------------|-----------------|
|[Konfiguráció vezérlők CustomEntry CustomItem elem.](./customitem-element-for-customentry-for-controls-for-configuration-format.md)|Határozza meg az egyéni vezérlőt a nézetben megjelenített adatok, és hogyan jelenik meg.|

## <a name="remarks"></a>Megjegyzés

## <a name="see-also"></a>Lásd még:

[Konfiguráció vezérlők CustomEntry CustomItem elem.](./customitem-element-for-customentry-for-controls-for-configuration-format.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
