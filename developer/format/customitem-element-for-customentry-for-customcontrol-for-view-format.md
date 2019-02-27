---
title: A nézet (formátum) CustomControl CustomEntry CustomItem eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 98708c1d-6f39-4a76-b454-31153a6ade8c
caps.latest.revision: 12
ms.openlocfilehash: 3c110bd5fe3ef2f790ef136556afa7c29d0b5b29
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56846941"
---
# <a name="customitem-element-for-customentry-for-customcontrol-for-view-format"></a>A Nézet CustomControl eleméhez tartozó CustomEntry CustomItem eleme (Formátum)

Határozza meg az egyéni vezérlőt a nézetben megjelenített adatok, és hogyan jelenik meg. Ehhez az elemhez használt egyéni vezérlő nézet definiálása.

Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézet elem (formátum) CustomControl elem (formátum) CustomEntries eleme CustomControl megtekintése (formátum) CustomEntry elem megtekintése (formátum) CustomItem elemhez tartozó CustomEntries számára CustomEntry nézet (formátum)

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
|[A nézet (formátum) CustomControl CustomItem ExpressionBinding elem.](./expressionbinding-element-for-customitem-for-customcontrol-for-view-format.md)|Nem kötelező eleme.<br /><br /> Határozza meg a vezérlő által megjelenített adatokat.|
|[A nézet (formátum) CustomControl CustomItem keret elem.](./frame-element-for-customitem-for-customcontrol-for-view-format.md)|Nem kötelező eleme.<br /><br /> Határozza meg az egyéni vezérlőt a nézetben megjelenített adatok, és hogyan jelenik meg.|
|[Egyéni vezérlő nézet (formátum) CustomItem soremelés elem.](./newline-element-for-customitem-for-customcontrol-for-view-format.md)|Nem kötelező eleme.<br /><br /> Egy üres sort ad hozzá a vezérlő megjelenését.|
|[A nézet (formátum) CustomControl CustomItem szöveg eleme](./text-element-for-customitem-for-customview-for-view-format.md)|Nem kötelező eleme.<br /><br /> Adja meg a rendszer további szöveget a vezérlőelem által megjelenített adatokhoz.|

### <a name="parent-elements"></a>Szülőelemek

|Elem|Leírás|
|-------------|-----------------|
|[A nézet (formátum) CustomControl CustomEntries CustomEntry elem.](./customentry-element-for-customentries-for-customcontrol-for-view-format.md)|Az egyéni vezérlő nézet definíciójának biztosít.|

## <a name="remarks"></a>Megjegyzés

## <a name="see-also"></a>Lásd még:

[A nézet (formátum) CustomEntries CustomEntry elem](./customentry-element-for-customentries-for-customcontrol-for-view-format.md)

[A nézet (formátum) CustomControl CustomItem ExpressionBinding elem.](./expressionbinding-element-for-customitem-for-customcontrol-for-view-format.md)

[A nézet (formátum) CustomControl CustomItem keret elem.](./frame-element-for-customitem-for-customcontrol-for-view-format.md)

[A nézet (formátum) CustomControl CustomItem soremelés elem.](./newline-element-for-customitem-for-customcontrol-for-view-format.md)

[A nézet (formátum) CustomControl CustomItem szöveg eleme](./text-element-for-customitem-for-customview-for-view-format.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
