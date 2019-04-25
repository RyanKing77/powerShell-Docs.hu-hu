---
title: Keretet elem számára CustomItem vezérlők (formátum) a konfigurációhoz |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: d879c8ce-679d-4622-bc43-c207f6413871
caps.latest.revision: 9
ms.openlocfilehash: b11b154a94daccead57bdfb5e579e1de2c190c09
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62065563"
---
# <a name="frame-element-for-customitem-for-controls-for-configuration-format"></a>A Konfiguráció Vezérlők eleméhez tartozó CustomItem Keret eleme (Formátum)

Határozza meg, hogyan egy jelennek meg, például az adatok pótlása jobbra vagy balra. Ez az elem szolgál egy közös vezérlőelem a formázási fájlban az összes nézetek által használható meghatározásakor.

Konfigurációs elem (formátum) vezérlők elem Configuration (formátum) vezérlőelem elem vezérlők, a vezérlő konfigurációs (formátum) CustomEntries elemhez tartozó CustomControl Configuration (a Configuration (formátum) CustomControl elem Formátum) CustomEntry elemet a vezérlők, a vezérlők, a konfiguráció keret elem CustomItem vezérlők (formátum) konfiguráció esetén a CustomEntry Configuration (formátum) CustomItem elemhez CustomControl

## <a name="syntax"></a>Szintaxis

```xml
<Frame>
  <LeftIndent>NumberOfCharactersToShift</LeftIndent>
  <RightIndent>NumberOfCharactersToShift</RightIndent>
  <FirstLineHanging>NumberOfCharactersToShift</FirstLineHanging>
  <FirstLineIndent>NumberOfCharactersToShift</FirstLineIndent>
  <CustomItem>...</CustomItem>
</Frame>
```

## <a name="attributes-and-elements"></a>Attribútumok és elemek

A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `Frame` elemet.

### <a name="attributes"></a>Attribútumok

Nincs.

### <a name="child-elements"></a>Gyermekelemek

|Elem|Leírás|
|-------------|-----------------|
|`CustomItem Element`|Kötelező elem|
|[Keret (formátum) konfiguráció vezérlők FirstLineHanging elem.](./firstlinehanging-element-for-frame-for-controls-for-configuration-format.md)|Nem kötelező eleme.<br /><br /> Megadja a bal oldali adatok első sora úgy, hogy hány karakter.|
|[Keret (formátum) konfiguráció vezérlők FirstLineIndent elem.](./firstlineindent-element-for-frame-for-controls-for-configuration-format.md)|Nem kötelező eleme.<br /><br /> Megadja az adatok első sorának jobb úgy, hogy hány karakter.|
|[Keret (formátum) konfiguráció vezérlők LeftIndent elem.](./leftindent-element-for-frame-for-controls-for-configuration-format.md)|Nem kötelező eleme.<br /><br /> Itt adhatja meg az adatokat erről a bal oldali margó úgy, hogy hány karakter.|
|[Keret (formátum) konfiguráció vezérlők RightIndent elem.](./rightindent-element-for-frame-for-controls-for-configuration-format.md)|Nem kötelező eleme.<br /><br /> Itt adhatja meg az adatokat erről a jobb oldali margó úgy, hogy hány karakter.|

### <a name="parent-elements"></a>Szülőelemek

|Elem|Leírás|
|-------------|-----------------|
|[Konfiguráció vezérlők CustomEntry CustomItem elem.](./customitem-element-for-customentry-for-controls-for-configuration-format.md)|Határozza meg a vezérlő által megjelenített adatokat, és hogyan jelenik meg.|

## <a name="remarks"></a>Megjegyzés

Nem adható meg a [FirstLineHanging](./firstlinehanging-element-for-frame-for-controls-for-configuration-format.md) és a [FirstLineIndent](./firstlineindent-element-for-frame-for-controls-for-configuration-format.md) elemek ugyanazon `Frame` elemet.

## <a name="see-also"></a>Lásd még:

[Keret (formátum) konfiguráció vezérlők FirstLineHanging elem.](./firstlinehanging-element-for-frame-for-controls-for-configuration-format.md)

[Keret (formátum) konfiguráció vezérlők FirstLineIndent elem.](./firstlineindent-element-for-frame-for-controls-for-configuration-format.md)

[Keret (formátum) konfiguráció vezérlők LeftIndent elem.](./leftindent-element-for-frame-for-controls-for-configuration-format.md)

[Keret (formátum) konfiguráció vezérlők RightIndent elem.](./rightindent-element-for-frame-for-controls-for-configuration-format.md)

[Konfiguráció vezérlők CustomEntry CustomItem elem.](./customitem-element-for-customentry-for-controls-for-configuration-format.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
