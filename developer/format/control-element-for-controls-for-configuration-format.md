---
title: Elem vezérlők Configuration (formátum) vezérlőelemet |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: bddf7ffa-04d3-4354-90b9-5e714e096260
caps.latest.revision: 13
ms.openlocfilehash: 26fe417c9ca60dda22bdc23d9d339d40135a0c9b
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62066793"
---
# <a name="control-element-for-controls-for-configuration-format"></a>A Konfiguráció Vezérlők elemének vezérlőeleme (Formátum)

Meghatározza egy közös ellenőrzés, hogy a formázási fájlja és a neve, amellyel hivatkozni a vezérlőelem összes nézet is lehet.

Konfigurációs elem (formátum) vezérlők elem Configuration (formátum) vezérlőelem elem vezérlők konfiguráció (formátum)

## <a name="syntax"></a>Szintaxis

```xml
<Control>
  <Name>NameOfControl</Name>
  <CustomControl>...</CustomControl>
</Control>
```

## <a name="attributes-and-elements"></a>Attribútumok és elemek

A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `Control` elemet. Minden gyermek elem csak az egyiket meg kell adnia.

### <a name="attributes"></a>Attribútumok

Nincs.

### <a name="child-elements"></a>Gyermekelemek

|Elem|Leírás|
|-------------|-----------------|
|[A vezérlési konfiguráció (formátum) vezérlők CustomControl elem](./customcontrol-element-for-control-for-controls-for-configuration-format.md)|Szükséges eleme.<br /><br /> Határozza meg a vezérlő.|
|[Name elemet a vezérlési konfiguráció (formátum)](./name-element-for-control-for-controls-for-configuration-format.md)|Szükséges eleme.<br /><br /> Megadja a mutató hivatkozás a vezérlő nevét.|

### <a name="parent-elements"></a>Szülőelemek

|Elem|Leírás|
|-------------|-----------------|
|[Vezérlők elem konfiguráció (formátum)](./controls-element-for-configuration-format.md)|Határozza meg a Gyakori vezérlők, amelyek az összes nézetben megtekinthetők a formázási fájl, vagy más vezérlőelemeket is használható.|

## <a name="remarks"></a>Megjegyzés

Ez a vezérlő neve a következő elemeket lehet hivatkozni:

- [ExpressionBinding eleme CustomItem (formátum)](./expressionbinding-element-for-customitem-for-controls-for-configuration-format.md)

- [GroupBy View(Format) elem.](./groupby-element-for-view-format.md)

## <a name="see-also"></a>Lásd még:

[Vezérlők elem konfiguráció (formátum)](./controls-element-for-configuration-format.md)

[CustomControl elemet a vezérlési konfiguráció (formátum)](./customcontrol-element-for-control-for-controls-for-configuration-format.md)

[ExpressionBinding eleme CustomItem (formátum)](./expressionbinding-element-for-customitem-for-controls-for-configuration-format.md)

[GroupBy View(Format) elem.](./groupby-element-for-view-format.md)

[A vezérlési konfiguráció (formátum) vezérlők Name elemet](./name-element-for-control-for-controls-for-configuration-format.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
