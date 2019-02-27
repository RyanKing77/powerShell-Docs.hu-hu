---
title: Keret (formátum) konfiguráció vezérlők FirstLineIndent elem |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 2f489720-11f6-4019-940e-07f423d4278d
caps.latest.revision: 6
ms.openlocfilehash: c5b2d971fe1590116f96b024ae8769334768acf2
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56847053"
---
# <a name="firstlineindent-element-for-frame-for-controls-for-configuration-format"></a>A Konfiguráció Vezérlők eleméhez tartozó Keret FirstLineIndent eleme (Formátum)

Megadja az adatok első sorának jobb úgy, hogy hány karakter. Ez az elem szolgál egy közös vezérlőelem a formázási fájlban az összes nézetek által használható meghatározásakor.

Konfigurációs elem (formátum) vezérlők elem Configuration (formátum) vezérlőelem elem vezérlők, a vezérlő konfigurációs (formátum) CustomEntries elemhez tartozó CustomControl Configuration (a Configuration (formátum) CustomControl elem Formátum) CustomEntry elemet a vezérlők, a Configuration (formátum) CustomItem elemet a vezérlők, a konfiguráció keret elemet a vezérlők, a Configuration (formátum) FirstLineIndent elem keret CustomItem CustomEntry CustomControl vezérlők, a Configuration (formátum)

## <a name="syntax"></a>Szintaxis

```xml
<FirstLineIndent>NumberOfCharactersToShift</FirstLineIndent>
```

## <a name="attributes-and-elements"></a>Attribútumok és elemek

A következő szakaszok ismertetik az attribútumokat, gyermekelemek és szülőelemét a `FirstLineIndent` elemet.

### <a name="attributes"></a>Attribútumok

Nincs.

### <a name="child-elements"></a>Gyermekelemek

Nincs.

### <a name="parent-elements"></a>Szülőelemek

|Elem|Leírás|
|-------------|-----------------|
|[Keret eleme CustomItem vezérlők konfiguráció (formátum)](./frame-element-for-customitem-for-controls-for-configuration-format.md)|Határozza meg, hogyan egy jelennek meg, például az adatok pótlása jobbra vagy balra.|

## <a name="text-value"></a>Szöveges érték

Adja meg, hogy az adatok első sora shift kívánt karakterek száma.

## <a name="remarks"></a>Megjegyzés

Ha ez az elem meg van adva, nem adható meg a [FirstLineHanging](./firstlinehanging-element-for-frame-for-controls-for-configuration-format.md) elemet.

## <a name="see-also"></a>Lásd még:

[Keret (formátum) konfiguráció vezérlők FirstLineHanging elem.](./firstlinehanging-element-for-frame-for-controls-for-configuration-format.md)

[Keret eleme CustomItem vezérlők konfiguráció (formátum)](./frame-element-for-customitem-for-controls-for-configuration-format.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
