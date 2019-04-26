---
title: A GroupBy (formátum) CustomItem ExpressionBinding eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 5eae5088-7605-4ef2-a703-faf3e5a5fc94
caps.latest.revision: 8
ms.openlocfilehash: 4714bfd1530585aa80aabc010b86d25bf0c7f9c4
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62065903"
---
# <a name="expressionbinding-element-for-customitem-for-groupby-format"></a>A GroupBy elemhez tartozó CustomItem ExpressionBinding eleme (Formátum)

Határozza meg a vezérlő által megjelenített adatokat. Ez az elem szolgál, hogyan jelenjen meg az objektumok egy új csoportot meghatározásakor.

Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem GroupBy elem megtekintése (formátum) CustomControl elem a GroupBy (formátum) CustomEntry elemhez tartozó CustomControl GroupBy (formátum) CustomEntries elemhez GroupBy (formátum) CustomItem elem CustomEntry CustomItem GroupBy (formátum) esetében a GroupBy (formátum) ExpressionBinding elemhez tartozó CustomControl

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
|[A GroupBy (formátum) ExpressionBinding CustomControlName elem.](./customcontrolname-element-for-expressionbinding-for-groupby-format.md)|Nem kötelező eleme.<br /><br /> Megadja egy közös vezérlőelem vagy a nézet nevét.|
|[A GroupBy (formátum) ExpressionBinding EnumerateCollection eleme](./enumeratecollection-element-for-expressionbinding-for-groupby-format.md)EnumerateCollection eleme ExpressionBinding a GroupBy (formátum)|Nem kötelező eleme.<br /><br /> A megadott jelennek meg, hogy a gyűjtemény elemeit.|
|[A GroupBy (formátum) ExpressionBinding ItemSelectionCondition elem.](./itemselectioncondition-element-for-expressionbinding-for-groupby-format.md)|Nem kötelező eleme.<br /><br /> Határozza meg azt a feltételt, amelyet Pro tento ovládací prvek használandó léteznie kell.|
|[A GroupBy (formátum) ExpressionBinding PropertyName elem.](./propertyname-element-for-expressionbinding-for-groupby-format.md)|Nem kötelező eleme.<br /><br /> Megadja a .NET-tulajdonságot, amelynek értéke megjelenik a vezérlőelem által.|
|[ExpressionBinding GroupBy (formátum) a scriptblock kulcsszót elem.](./scriptblock-element-for-expressionbinding-for-groupby-format.md)|Nem kötelező eleme.<br /><br /> Megadja a parancsprogramot, amelynek értéke megjelenik a vezérlőelem által.|

### <a name="parent-elements"></a>Szülőelemek

|Elem|Leírás|
|-------------|-----------------|
|[A GroupBy (formátum) CustomEntry CustomItem elem.](./customitem-element-for-customentry-for-groupby-format.md)|Határozza meg az egyéni vezérlőt a nézetben megjelenített adatok, és hogyan jelenik meg.|

## <a name="see-also"></a>Lásd még:

[A GroupBy (formátum) ExpressionBinding CustomControlName elem.](./customcontrolname-element-for-expressionbinding-for-groupby-format.md)

[A GroupBy (formátum) ExpressionBinding EnumerateCollection elem.](./enumeratecollection-element-for-expressionbinding-for-groupby-format.md)

[A GroupBy (formátum) ExpressionBinding ItemSelectionCondition elem.](./itemselectioncondition-element-for-expressionbinding-for-groupby-format.md)

[A GroupBy (formátum) ExpressionBinding PropertyName elem.](./propertyname-element-for-expressionbinding-for-groupby-format.md)

[ExpressionBinding GroupBy (formátum) a scriptblock kulcsszót elem.](./scriptblock-element-for-expressionbinding-for-groupby-format.md)

[A GroupBy (formátum) CustomEntry CustomItem elem.](./customitem-element-for-customentry-for-groupby-format.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
