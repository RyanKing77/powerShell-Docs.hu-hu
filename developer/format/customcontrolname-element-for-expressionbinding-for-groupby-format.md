---
title: A GroupBy (formátum) ExpressionBinding CustomControlName eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 9e11da8f-1e75-4d3d-b4c8-b500dec3028e
caps.latest.revision: 6
ms.openlocfilehash: 32f8a71e9818c8c1a052f3b96f442f169c1bda4a
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62066568"
---
# <a name="customcontrolname-element-for-expressionbinding-for-groupby-format"></a>A GroupBy elem ExpressionBinding CustomControlName eleme (Formátum)

Megadja egy közös vezérlőelem vagy a nézet nevét. Ez az elem szolgál, hogyan jelenjen meg az objektumok egy új csoportot meghatározásakor.

Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem GroupBy elem megtekintése (formátum) CustomControl elem a GroupBy (formátum) CustomEntry elemhez tartozó CustomControl GroupBy (formátum) CustomEntries elemhez GroupBy (formátum) CustomItem elem CustomEntry CustomItem ExpressionBinding GroupBy (formátum) esetében a GroupBy (formátum) CustomControlName elemhez tartozó GroupBy (formátum) ExpressionBinding elemhez tartozó CustomControl

## <a name="syntax"></a>Szintaxis

```xml
<CustomControlName>NameofCustomControl</CustomControlName>
```

## <a name="attributes-and-elements"></a>Attribútumok és elemek

A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `CustomControlName` elemet.

### <a name="attributes"></a>Attribútumok

Nincs.

### <a name="child-elements"></a>Gyermekelemek

Nincs.

### <a name="parent-elements"></a>Szülőelemek

|Elem|Leírás|
|-------------|-----------------|
|[A GroupBy (formátum) CustomItem ExpressionBinding elem.](./expressionbinding-element-for-customitem-for-groupby-format.md)|Határozza meg a vezérlő által megjelenített adatokat.|

## <a name="text-value"></a>A szöveges érték

Adja meg a vezérlő nevét.

## <a name="remarks"></a>Megjegyzés

A formázási fájl összes nézetek által használt Gyakori vezérlők hozhat létre, és hozhat létre, amely egy adott nézet által használható vezérlőkre. A következő elemeket adja meg, hogy ezek a vezérlők nevét:

- [A vezérlési konfiguráció (formátum) vezérlők Name elemet](./name-element-for-control-for-controls-for-configuration-format.md)

- [Vezérlő (formátum) nézet vezérlők Name elemet](./name-element-for-control-for-controls-for-view-format.md)

## <a name="see-also"></a>Lásd még:

[A vezérlési konfiguráció (formátum) vezérlők Name elemet](./name-element-for-control-for-controls-for-configuration-format.md)

[Vezérlő (formátum) nézet vezérlők Name elemet](./name-element-for-control-for-controls-for-view-format.md)

[A GroupBy (formátum) CustomItem ExpressionBinding elem.](./expressionbinding-element-for-customitem-for-groupby-format.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
