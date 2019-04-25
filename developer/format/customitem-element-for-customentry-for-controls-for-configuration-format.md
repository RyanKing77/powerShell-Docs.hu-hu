---
title: CustomItem elemet a vezérlők (formátum) konfiguráció CustomEntry |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 73fb11ee-0ebd-477a-ac36-acdfbb32e70d
caps.latest.revision: 7
ms.openlocfilehash: bd0cb69770817ec215ddb1862a43a838baddefcf
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62066430"
---
# <a name="customitem-element-for-customentry-for-controls-for-configuration-format"></a>A Konfiguráció Vezérlők eleméhez tartozó CustomEntry CustomItem eleme (Formátum)

Határozza meg a vezérlő által megjelenített adatokat, és hogyan jelenik meg. Ez az elem szolgál egy közös vezérlőelem a formázási fájlban az összes nézetek által használható meghatározásakor.

Konfigurációs elem (formátum) vezérlők elem Configuration (formátum) vezérlőelem elem vezérlők, a vezérlő konfigurációs (formátum) CustomEntries elemhez tartozó CustomControl Configuration (a Configuration (formátum) CustomControl elem Formátum) CustomEntry elemet a vezérlők, a vezérlők, a konfigurációhoz CustomEntry Configuration (formátum) CustomItem elemhez CustomControl

## <a name="syntax"></a>Szintaxis

```xml
<CustomItem>
  <ExpressionBinding>...</ExpressionBinding>
  <NewLine/>
  <Text>TextToDisplay</Text>
  <Frame>...</Frame>
</CustomItem>
```

## <a name="attributes-and-elements"></a>Attribútumok és elemek

A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `CustomItem` elemet. További információkért lásd a megjegyzések.

### <a name="attributes"></a>Attribútumok

Nincs.

### <a name="child-elements"></a>Gyermekelemek

|Elem|Leírás|
|-------------|-----------------|
|[Konfiguráció (formátum) vezérlők CustomItem ExpressionBinding elem.](./expressionbinding-element-for-customitem-for-controls-for-configuration-format.md)|Nem kötelező eleme.<br /><br /> Határozza meg a vezérlő által megjelenített adatokat.|
|[Keret eleme CustomItem vezérlők konfiguráció (formátum)](./frame-element-for-customitem-for-controls-for-configuration-format.md)|Nem kötelező eleme.<br /><br /> Határozza meg, hogyan egy jelennek meg, például az adatok pótlása jobbra vagy balra.|
|[Konfiguráció (formátum) vezérlők CustomItem soremelés elem.](./newline-element-for-customitem-for-controls-for-configuration-format.md)|Nem kötelező eleme.<br /><br /> Egy üres sort ad hozzá a vezérlő megjelenését.|
|[A vezérlők (formátum) konfiguráció CustomItem elem](./text-element-for-customitem-for-controls-for-configuration-format.md)|Nem kötelező eleme.<br /><br /> Szöveg, például zárójelek vagy zárójelben ad hozzá a vezérlő megjelenését.|

### <a name="parent-elements"></a>Szülőelemek

|Elem|Leírás|
|-------------|-----------------|
|[Konfiguráció (formátum) vezérlők CustomControl CustomEntry elem.](./customentry-element-for-customcontrol-for-controls-for-configuration-format.md)|A vezérlőelem egy definíciót tartalmaz.|

## <a name="remarks"></a>Megjegyzés

Az alárendelt elemeinek megadásakor a `CustomItem` elem, vegye figyelembe a következőket:

- A gyermekelemek hozzá kell adni a következő sorrendben: `ExpressionBinding`, `NewLine`, `Text`, és `Frame`.

- Nincs maximális megadható feladatütemezések száma korlátozva van.

- Az egyes feladatütemezési nem nincs maximális számának korlátja `ExpressionBinding` elemeket, amelyeket használhat.

## <a name="see-also"></a>Lásd még:

[Konfiguráció (formátum) vezérlők CustomItem ExpressionBinding elem.](./expressionbinding-element-for-customitem-for-controls-for-configuration-format.md)

[Keret eleme CustomItem vezérlők konfiguráció (formátum)](./frame-element-for-customitem-for-controls-for-configuration-format.md)

[Konfiguráció (formátum) vezérlők CustomItem soremelés elem.](./newline-element-for-customitem-for-controls-for-configuration-format.md)

[A vezérlők (formátum) konfiguráció CustomItem elem](./text-element-for-customitem-for-controls-for-configuration-format.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
