---
title: CustomControl elemet a vezérlési konfiguráció (formátum) vezérlők |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: d9d92a9e-c680-46ca-962e-e82452726953
caps.latest.revision: 10
ms.openlocfilehash: 1d72ce5b18e89bd81c7f81b27f4b8c60bed99764
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56847977"
---
# <a name="customcontrol-element-for-control-for-controls-for-configuration-format"></a>A Konfiguráció Vezérlők eleméhez tartozó Vezérlő CustomControl eleme (Formátum)

Határozza meg olyan vezérlő. Ez az elem szolgál egy közös vezérlőelem a formázási fájlban az összes nézetek által használható meghatározásakor.

Konfigurációs elem (formátum) vezérlők elem Configuration (formátum) vezérlőelem elem vezérlők, a Configuration (formátum) CustomControl elem a vezérlési konfiguráció (formátum)

## <a name="syntax"></a>Szintaxis

```xml
<CustomControl>
  <CustomEntries>...</CustomEntries>
</CustomControl>
```

## <a name="attributes-and-elements"></a>Attribútumok és elemek

A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `CustomControl` elemet. Ez az elem rendelkeznie kell legalább egy gyermekelemet. Nincs maximális megadható az alárendelt elemek száma korlátozva van.

### <a name="attributes"></a>Attribútumok

Nincs.

### <a name="child-elements"></a>Gyermekelemek

|Elem|Leírás|
|-------------|-----------------|
|[Konfiguráció (formátum) CustomControl CustomEntries elem.](./customentries-element-for-customcontrol-for-controls-for-configuration-format.md)|Szükséges eleme.<br /><br /> A vezérlőelem definícióit tartalmazza.|

### <a name="parent-elements"></a>Szülőelemek

|Elem|Leírás|
|-------------|-----------------|
|[Vezérlő elemet a vezérlők konfiguráció (formátum)](./control-element-for-controls-for-configuration-format.md)|Meghatározza egy közös ellenőrzés, hogy a formázási fájlja és a neve, amellyel hivatkozni a vezérlőelem összes nézet is lehet.|

## <a name="remarks"></a>Megjegyzés

## <a name="see-also"></a>Lásd még:

[Vezérlő elemet a vezérlők konfiguráció (formátum)](./control-element-for-controls-for-configuration-format.md)

[Konfiguráció (formátum) CustomControl CustomEntries elem.](./customentries-element-for-customcontrol-for-controls-for-configuration-format.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
