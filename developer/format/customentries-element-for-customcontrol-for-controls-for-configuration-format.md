---
title: CustomEntries elemet a vezérlők (formátum) konfiguráció CustomControl |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 80fc4de2-208f-4506-9a6a-c2675bb83be4
caps.latest.revision: 11
ms.openlocfilehash: abef6c91500f665c2366f221496d4cfd6444f5c9
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56847025"
---
# <a name="customentries-element-for-customcontrol-for-controls-for-configuration-format"></a>A Konfiguráció Vezérlők eleméhez tartozó CustomControl CustomEntries eleme (Formátum)

A közös ellenőrzési definícióit tartalmazza. Ez az elem szolgál egy közös vezérlőelem a formázási fájlban az összes nézetek által használható meghatározásakor.

Konfigurációs elem (formátum) vezérlők elem Configuration (formátum) vezérlőelem elem vezérlők, a vezérlő konfigurációs (formátum) CustomEntries elemhez tartozó CustomControl Configuration (a Configuration (formátum) CustomControl elem Formátum)

## <a name="syntax"></a>Szintaxis

```xml
<CustomEntries>
  <CustomEntry>...</CustomEntry>
</CustomEntries>

```

## <a name="attributes-and-elements"></a>Attribútumok és elemek

A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `CustomEntries` elemet. Meg kell adnia egy vagy több gyermekelemet.

### <a name="attributes"></a>Attribútumok

Nincs.

### <a name="child-elements"></a>Gyermekelemek

|Elem|Leírás|
|-------------|-----------------|
|[Konfiguráció (formátum) vezérlők CustomControl CustomEntry elem.](./customentry-element-for-customcontrol-for-controls-for-configuration-format.md)|A közös ellenőrzési definíciójának biztosít.|

### <a name="parent-elements"></a>Szülőelemek

|Elem|Leírás|
|-------------|-----------------|
|[CustomControl elemet a vezérlési konfiguráció (formátum)](./customcontrol-element-for-control-for-controls-for-configuration-format.md)|A közös ellenőrzési határozza meg.|

## <a name="remarks"></a>Megjegyzés

A legtöbb esetben egy vezérlőelem még csak egy definíciót, amely egy meghatározott `CustomEntry` elemet. Azonban lehetőség a több definíciókkal rendelkeznek, ha különböző .NET-objektumok megjelenítése ugyanazon vezérlő használata. Ezekben az esetekben definiálhat egy `CustomEntry` elem az egyes objektumok vagy objektumok közül.

## <a name="see-also"></a>Lásd még:

[CustomControl elemet a vezérlési konfiguráció (formátum)](./customcontrol-element-for-control-for-controls-for-configuration-format.md)

[Konfiguráció (formátum) vezérlők CustomControl CustomEntry elem.](./customentry-element-for-customcontrol-for-controls-for-configuration-format.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
