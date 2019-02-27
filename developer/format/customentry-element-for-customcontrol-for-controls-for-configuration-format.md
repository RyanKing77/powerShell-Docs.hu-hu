---
title: CustomEntry elemet a vezérlők (formátum) konfiguráció CustomControl |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 9dfba86f-29b2-473c-9e98-9d679176acce
caps.latest.revision: 11
ms.openlocfilehash: 497485a388d1cdc834ecc1d1079b0714a7d7f9db
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56849475"
---
# <a name="customentry-element-for-customcontrol-for-controls-for-configuration-format"></a>A Konfiguráció Vezérlők eleméhez tartozó CustomControl CustomEntry eleme (Formátum)

A közös ellenőrzési definíciójának biztosít. Ez az elem szolgál egy közös vezérlőelem a formázási fájlban az összes nézetek által használható meghatározásakor.

Konfigurációs elem (formátum) vezérlők elem Configuration (formátum) vezérlőelem elem vezérlők, a vezérlő konfigurációs (formátum) CustomEntries elemhez tartozó CustomControl Configuration (a Configuration (formátum) CustomControl elem Formátum) CustomEntry eleme CustomControl vezérlők konfiguráció (formátum)

## <a name="syntax"></a>Szintaxis

```xml
<CustomEntry>
  <EntrySelectedBy>...</EntrySelectedBy>
  <CustomItem>...</CustomItem>
</CustomEntry>

```

## <a name="attributes-and-elements"></a>Attribútumok és elemek

A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `CustomEntry` elemet. Meg kell adnia a cikkeket a definíció szerint jelenik meg.

### <a name="attributes"></a>Attribútumok

Nincs.

### <a name="child-elements"></a>Gyermekelemek

|Elem|Leírás|
|-------------|-----------------|
|[Konfiguráció (formátum) vezérlők CustomEntry EntrySelectedBy elem.](./entryselectedby-element-for-customentry-for-controls-for-configuration-format.md)|Nem kötelező eleme.<br /><br /> A .NET-típusokat, amelyek a közös vezérlőelem vagy a feltételt, amelyet Pro tento ovládací prvek használandó léteznie kell a definíció határozza meg.|
|[Konfiguráció vezérlők CustomEntry CustomItem elem.](./customitem-element-for-customentry-for-controls-for-configuration-format.md)|Szükséges eleme.<br /><br /> Határozza meg a vezérlő által megjelenített adatokat, és hogyan jelenik meg.|

### <a name="parent-elements"></a>Szülőelemek

|Elem|Leírás|
|-------------|-----------------|
|[Konfiguráció (formátum) CustomControl CustomEntries elem.](./customentries-element-for-customcontrol-for-controls-for-configuration-format.md)|A közös ellenőrzési a definíciókat tartalmazza.|

## <a name="remarks"></a>Megjegyzés

A legtöbb esetben csak egy-definícióra szükség minden egyes gyakori egyéni vezérlőt, de lehetséges több definíciókkal rendelkeznek, ha különböző .NET-objektumok megjelenítése ugyanazon vezérlő használata. Ezekben az esetekben adja meg egy külön meghatározása az egyes objektumok vagy objektumok közül.

## <a name="see-also"></a>Lásd még:

[Konfiguráció (formátum) CustomControl CustomEntries elem.](./customentries-element-for-customcontrol-for-controls-for-configuration-format.md)

[Konfiguráció vezérlők CustomEntry CustomItem elem.](./customitem-element-for-customentry-for-controls-for-configuration-format.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
