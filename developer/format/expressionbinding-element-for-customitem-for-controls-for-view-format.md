---
title: ExpressionBinding elemet a vezérlők (formátum) nézet CustomItem |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 2b9da6c5-548b-480f-86ae-6de6fecabaca
caps.latest.revision: 8
ms.openlocfilehash: 06089730008839f18c471711a4b4411722f99c38
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56848418"
---
# <a name="expressionbinding-element-for-customitem-for-controls-for-view-format"></a>A Nézet Vezérlők eleméhez tartozó CustomItem ExpressionBinding eleme (Formátum)

Határozza meg a vezérlő által megjelenített adatokat. Ez az elem szolgál a nézet által használható vezérlők meghatározásakor.

Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem vezérlők elem (formátum) vezérlőelem elem vezérlők, a nézet (formátum) CustomControl elem megtekintése (formátum) CustomEntries elemet a vezérlők a vezérlő A nézet (formátum) CustomEntry elem CustomEntries vezérlők, a vezérlők, a vezérlők (formátum) nézet CustomItem megtekintése (formátum) ExpressionBinding elemhez CustomEntry megtekintése (formátum) CustomItem elemhez tartozó CustomControl

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
|[Nézet (formátum) vezérlők ExpressionBinding CustomControlName elem.](./customcontrolname-element-for-expressionbinding-for-controls-for-view-format.md)|Nem kötelező eleme.<br /><br /> Megadja egy közös vezérlőelem vagy a nézet nevét.|
|[Nézet (formátum) vezérlők ExpressionBinding EnumerateCollection elem.](./enumeratecollection-element-for-expressionbinding-for-controls-for-view-format.md)|Nem kötelező eleme.<br /><br /> Itt adhatja meg, hogy megjelenik-e a gyűjtemény elemeinek.|
|[Nézet (formátum) vezérlők ExpressionBinding ItemSelectionCondition eleme](./itemselectioncondition-element-for-expressionbinding-for-controls-for-view-format.md)|Nem kötelező eleme.<br /><br /> Határozza meg azt a feltételt, amelyet Pro tento ovládací prvek használandó léteznie kell.|
|[A PropertyName eleme ExpressionBinding vezérlők nézet (formátum)](./propertyname-element-for-expressionbinding-for-controls-for-view-format.md)|Nem kötelező eleme.<br /><br /> Megadja a .NET-tulajdonságot, amelynek értéke megjelenik a vezérlőelem által.|
|[Nézet (formátum) vezérlők ExpressionBinding ScriptBlock elem.](./scriptblock-element-for-expressionbinding-for-controls-for-view-format.md)|Nem kötelező eleme.<br /><br /> Megadja a parancsprogramot, amelynek értéke megjelenik a vezérlőelem által.|

### <a name="parent-elements"></a>Szülőelemek

|Elem|Leírás|
|-------------|-----------------|
|[Nézet (formátum) vezérlők CustomEntry CustomItem elem.](./customitem-element-for-customentry-for-controls-for-view-format.md)|Határozza meg a vezérlő által megjelenített adatokat, és hogyan jelenik meg.|

## <a name="remarks"></a>Megjegyzés

## <a name="see-also"></a>Lásd még:

[Nézet (formátum) vezérlők CustomEntry CustomItem elem.](./customitem-element-for-customentry-for-controls-for-view-format.md)

[Nézet (formátum) vezérlők ExpressionBinding CustomControlName elem.](./customcontrolname-element-for-expressionbinding-for-controls-for-view-format.md)

[Nézet (formátum) vezérlők ExpressionBinding EnumerateCollection elem.](./enumeratecollection-element-for-expressionbinding-for-controls-for-view-format.md)

[Nézet (formátum) vezérlők ExpressionBinding ItemSelectionCondition eleme](./itemselectioncondition-element-for-expressionbinding-for-controls-for-view-format.md)

[A PropertyName eleme ExpressionBinding vezérlők nézet (formátum)](./propertyname-element-for-expressionbinding-for-controls-for-view-format.md)

[Nézet (formátum) vezérlők ExpressionBinding ScriptBlock elem.](./scriptblock-element-for-expressionbinding-for-controls-for-view-format.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
