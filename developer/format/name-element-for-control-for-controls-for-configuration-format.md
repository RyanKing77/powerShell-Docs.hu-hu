---
title: Nevezze el elem vezérlő vezérlők konfiguráció (formátum) |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: b4371d45-49a4-4303-8384-5b54105bd0d6
caps.latest.revision: 8
ms.openlocfilehash: 2704a530e0ae269efb772ac10e531bcbb12f6eff
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62065189"
---
# <a name="name-element-for-control-for-controls-for-configuration-format"></a>A Konfiguráció Vezérlők eleméhez tartozó Vezérlő Név eleme (Formátum)

Megadja a vezérlő nevét. Ez az elem szolgál egy közös vezérlőelem a formázási fájlban az összes nézetek által használható meghatározásakor.

Konfigurációs elem (formátum) vezérlők elem Configuration (formátum) vezérlőelem elem vezérlők vezérlők konfiguráció (formátum) vezérlő konfigurációs (formátum) neve elemhez

## <a name="syntax"></a>Szintaxis

```xml
<Name>NameOfControl</Name>

```

## <a name="attributes-and-elements"></a>Attribútumok és elemek

A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `Name` elemet.

### <a name="attributes"></a>Attribútumok

Nincs.

### <a name="child-elements"></a>Gyermekelemek

Nincs.

### <a name="parent-elements"></a>Szülőelemek

|Elem|Leírás|
|-------------|-----------------|
|[Vezérlő elemet a vezérlők konfiguráció (formátum)](./control-element-for-controls-for-configuration-format.md)|Meghatározza egy közös ellenőrzés, hogy a formázási fájlja és a neve, amellyel hivatkozni a vezérlőelem összes nézet is lehet.|

## <a name="text-value"></a>A szöveges érték

Adja meg a nevét, amely a vezérlőelem hivatkozni.

## <a name="remarks"></a>Megjegyzés

Az itt megadott név a vezérlő hivatkozni a következő elemeket is használható.

- Egy táblázat, lista, szélesre vagy egyéni vezérlő nézetében létrehozásakor, a vezérlő határozhatja meg a következő elemet: [GroupBy elem nézet (formátum)](./groupby-element-for-view-format.md)

- Egy másik gyakori vezérlő létrehozásakor ez a vezérlő határozhatja meg a következő elemet: [Konfiguráció (formátum) vezérlők CustomItem ExpressionBinding elem.](./expressionbinding-element-for-customitem-for-controls-for-configuration-format.md)

- Vezérlőelem létrehozása a nézet által használható, ha ez a vezérlő határozhatja meg a következő elemet: [Nézet (formátum) vezérlők CustomItem ExpressionBinding elem.](./expressionbinding-element-for-customitem-for-controls-for-view-format.md)

## <a name="see-also"></a>Lásd még:

[Vezérlő elemet a vezérlők konfiguráció (formátum)](./control-element-for-controls-for-configuration-format.md)

[Konfiguráció (formátum) vezérlők CustomItem ExpressionBinding elem.](./expressionbinding-element-for-customitem-for-controls-for-configuration-format.md)

[Nézet (formátum) vezérlők CustomItem ExpressionBinding elem.](./expressionbinding-element-for-customitem-for-controls-for-view-format.md)

[GroupBy elem nézet (formátum)](./groupby-element-for-view-format.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
