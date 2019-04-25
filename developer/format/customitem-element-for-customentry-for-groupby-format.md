---
title: A GroupBy (formátum) CustomEntry CustomItem eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: f7c517aa-24f5-41ae-b82d-cb0fac81a245
caps.latest.revision: 7
ms.openlocfilehash: 2d821f5e3bc8d0f81ef8a8a040c6f9bcb1658bee
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62066397"
---
# <a name="customitem-element-for-customentry-for-groupby-format"></a>A GroupBy CustomEntry elemének CustomItem eleme (Formátum)

Határozza meg az egyéni vezérlőt a nézetben megjelenített adatok, és hogyan jelenik meg. Ez az elem szolgál, hogyan jelenjen meg az objektumok egy új csoportot meghatározásakor.

Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem GroupBy elem megtekintése (formátum) CustomControl elem a GroupBy (formátum) CustomItem elemhez tartozó CustomControl GroupBy (formátum) CustomEntries elemhez CustomEntry a GroupBy (formátum)

## <a name="syntax"></a>Szintaxis

```xml
<CustomItem>
  <ExpressionBinding>...</ExpressionBinding>
  <Frame>...</Frame>
  <NewLine/>
  <Text>TextToDisplay</Text>
</CustomItem>
```

## <a name="attributes-and-elements"></a>Attribútumok és elemek

A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `CustomItem` elemet.

### <a name="attributes"></a>Attribútumok

Nincs.

### <a name="child-elements"></a>Gyermekelemek

|Elem|Leírás|
|-------------|-----------------|
|[A GroupBy (formátum) CustomItem ExpressionBinding elem.](./expressionbinding-element-for-customitem-for-groupby-format.md)|Nem kötelező eleme.<br /><br /> Határozza meg a vezérlő által megjelenített adatokat.|
|[Keret eleme CustomItem a GroupBy (formátum)](./frame-element-for-customitem-for-groupby-format.md)|Nem kötelező eleme.<br /><br /> Határozza meg az egyéni vezérlőt a nézetben megjelenített adatok, és hogyan jelenik meg.|
|[A GroupBy (formátum) CustomItem soremelés elem.](./newline-element-for-customitem-for-groupby-format.md)|Nem kötelező eleme.<br /><br /> Egy üres sort ad hozzá a vezérlő megjelenését.|
|[Szöveg eleme CustomItem a GroupBy (formátum)](./text-element-for-customitem-for-groupby-format.md)|Nem kötelező eleme.<br /><br /> Adja meg a rendszer további szöveget a vezérlőelem által megjelenített adatokhoz.|

### <a name="parent-elements"></a>Szülőelemek

|Elem|Leírás|
|-------------|-----------------|
|[A GroupBy (formátum) CustomControl CustomEntry elem.](./customentry-element-for-customcontrol-for-groupby-format.md)|Az egyéni vezérlő nézet definíciójának biztosít.|

## <a name="remarks"></a>Megjegyzés

## <a name="see-also"></a>Lásd még:

[A GroupBy (formátum) CustomControl CustomEntry elem.](./customentry-element-for-customcontrol-for-groupby-format.md)

[A GroupBy (formátum) CustomItem ExpressionBinding elem.](./expressionbinding-element-for-customitem-for-groupby-format.md)

[Keret eleme CustomItem a GroupBy (formátum)](./frame-element-for-customitem-for-groupby-format.md)

[A GroupBy (formátum) CustomItem soremelés elem.](./newline-element-for-customitem-for-groupby-format.md)

[Szöveg eleme CustomItem a GroupBy (formátum)](./text-element-for-customitem-for-groupby-format.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
