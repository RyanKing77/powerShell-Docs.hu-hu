---
title: CustomControlName elemet a vezérlők (formátum) konfiguráció ExpressionBinding |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: c5242935-2782-4d23-84f5-2446b2b7ba83
caps.latest.revision: 8
ms.openlocfilehash: c9abd9f22907b87323c16d603a9f75bb3d375a03
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62066634"
---
# <a name="customcontrolname-element-for-expressionbinding-for-controls-for-configuration-format"></a>A Konfiguráció Vezérlők eleméhez tartozó ExpressionBinding CustomControlName eleme (Formátum)

Megadja egy közös vezérlőelem neve. Ez az elem szolgál egy közös vezérlőelem a formázási fájlban az összes nézetek által használható meghatározásakor.

Konfigurációs elem (formátum) vezérlők elem Configuration (formátum) vezérlőelem elem vezérlők, a vezérlő konfigurációs (formátum) CustomEntries elemhez tartozó CustomControl Configuration (a Configuration (formátum) CustomControl elem Formátum) CustomEntry elemet a vezérlők, a Configuration (formátum) CustomItem elemet a vezérlők, a konfiguráció ExpressionBinding elemet a vezérlők, a Configuration (formátum) CustomControlName CustomItem CustomEntry CustomControl Konfiguráció (formátum) vezérlők ExpressionBinding elem.

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
|[Konfiguráció (formátum) vezérlők CustomItem ExpressionBinding elem.](./expressionbinding-element-for-customitem-for-controls-for-configuration-format.md)|Határozza meg a vezérlő által megjelenített adatokat.|

## <a name="text-value"></a>A szöveges érték

Adja meg a vezérlő nevét.

## <a name="remarks"></a>Megjegyzés

A formázási fájl összes nézetek által használt Gyakori vezérlők hozhat létre, és hozhat létre, amely egy adott nézet által használható vezérlőkre. A következő elemeket adja meg, hogy ezek a vezérlők nevét:

- [A vezérlési konfiguráció (formátum) vezérlők Name elemet](./name-element-for-control-for-controls-for-configuration-format.md)

- [Vezérlő (formátum) nézet vezérlők Name elemet](./name-element-for-control-for-controls-for-view-format.md)

## <a name="see-also"></a>Lásd még:

[A vezérlési konfiguráció (formátum) vezérlők Name elemet](./name-element-for-control-for-controls-for-configuration-format.md)

[Vezérlő (formátum) nézet vezérlők Name elemet](./name-element-for-control-for-controls-for-view-format.md)

[Konfiguráció (formátum) vezérlők CustomItem ExpressionBinding elem.](./expressionbinding-element-for-customitem-for-controls-for-configuration-format.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
