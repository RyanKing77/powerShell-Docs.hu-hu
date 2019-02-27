---
title: A nézet (formátum) CustomControl CustomItem ExpressionBinding eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 7f5ebea5-ee9c-4b90-a116-12a1daa28fc7
caps.latest.revision: 7
ms.openlocfilehash: 226bbea1d7613ad3099e05e8caa9817ff16c1f42
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56850091"
---
# <a name="expressionbinding-element-for-customitem-for-customcontrol-for-view-format"></a>A Nézet CustomControl eleméhez tartozó CustomItem ExpressionBinding eleme (Formátum)

Határozza meg a vezérlő által megjelenített adatokat. Ehhez az elemhez használt egyéni vezérlő nézet definiálása.

Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézet elem (formátum) CustomControl elem a CustomControl megtekintése (formátum) CustomEntry elemhez tartozó CustomEntries CustomControl a nézet (a nézetben (formátum) CustomEntries elemhez CustomControl CustomItem CustomControl nézet (formátum) esetében a nézet (formátum) ExpressionBinding elemhez tartozó CustomEntry CustomItem eleme formátumban)

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
|[A nézet (formátum) CustomControl ExpressionBinding CustomControlName elem.](./customcontrolname-element-for-expressionbinding-for-customcontrol-for-view-format.md)|Nem kötelező eleme.<br /><br /> Megadja egy közös vezérlőelem vagy a nézet nevét.|
|[A nézet (formátum) CustomControl ExpressionBinding EnumerateCollection elem.](./enumeratecollection-element-for-expressionbinding-for-customcontrol-for-view-format.md)|Nem kötelező eleme.<br /><br /> A megadott jelennek meg, hogy a gyűjtemény elemeit.|
|[A nézet (formátum) CustomControl ExpressionBinding ItemSelectionCondition elem.](./itemselectioncondition-element-for-expressionbinding-for-customcontrol-format.md)|Nem kötelező eleme.<br /><br /> Határozza meg azt a feltételt, amelyet Pro tento ovládací prvek használandó léteznie kell.|
|[A nézet (formátum) CustomControl ExpressionBinding PropertyName elem.](./propertyname-element-for-expressionbinding-for-customcontrol-for-view-format.md)|Nem kötelező eleme.<br /><br /> Megadja a .NET-tulajdonságot, amelynek értéke megjelenik a vezérlőelem által.|
|[A nézet (formátum) CustomCustomControl ExpressionBinding ScriptBlock eleme](./scriptblock-element-for-expressionbinding-for-customcontrol-for-view-format.md)|Nem kötelező eleme.<br /><br /> Megadja a parancsprogramot, amelynek értéke megjelenik a vezérlőelem által.|

### <a name="parent-elements"></a>Szülőelemek

|Elem|Leírás|
|-------------|-----------------|
|[A nézet (formátum) CustomControl CustomEntry CustomItem elem.](./customitem-element-for-customentry-for-customcontrol-for-view-format.md)|Határozza meg az egyéni vezérlőt a nézetben megjelenített adatok, és hogyan jelenik meg.|

## <a name="remarks"></a>Megjegyzés

## <a name="see-also"></a>Lásd még:

[A nézet (formátum) CustomControl ExpressionBinding CustomControlName elem.](./customcontrolname-element-for-expressionbinding-for-customcontrol-for-view-format.md)

[A nézet (formátum) CustomControl ExpressionBinding EnumerateCollection elem.](./enumeratecollection-element-for-expressionbinding-for-customcontrol-for-view-format.md)

[A nézet (formátum) CustomControl ExpressionBinding ItemSelectionCondition elem.](./itemselectioncondition-element-for-expressionbinding-for-customcontrol-format.md)

[A nézet (formátum) CustomControl ExpressionBinding PropertyName elem.](./propertyname-element-for-expressionbinding-for-customcontrol-for-view-format.md)

[A nézet (formátum) CustomControl ExpressionBinding ScriptBlock eleme](./scriptblock-element-for-expressionbinding-for-customcontrol-for-view-format.md)

[A nézet (formátum) CustomControl CustomEntry CustomItem elem.](./customitem-element-for-customentry-for-customcontrol-for-view-format.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
