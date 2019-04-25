---
title: CustomEntries elemet a vezérlők (formátum) nézet CustomControl |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 3485958a-ba87-4932-907c-a8f140c4abdb
caps.latest.revision: 8
ms.openlocfilehash: 4856aee930285781a101868bd6cb67824585bce1
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62066583"
---
# <a name="customentries-element-for-customcontrol-for-controls-for-view-format"></a>A Nézet Vezérlők eleméhez tartozó CustomControl CustomEntries eleme (Formátum)

A definíciók vezérlő biztosít. Ez az elem szolgál a nézet által használható vezérlők meghatározásakor.

Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem vezérlők elem (formátum) vezérlőelem elem vezérlők, a nézet (formátum) CustomControl elem megtekintése (formátum) CustomEntries elemet a vezérlők a vezérlő CustomControl vezérlők nézet (formátum)

## <a name="syntax"></a>Szintaxis

```xml
<CustomEntries>
  <CustomEntry>...</CustomEntry>
</CustomEntries>
```

## <a name="attributes-and-elements"></a>Attribútumok és elemek

A következő szakaszok ismertetik az attribútumokat, a gyermekelemek és a szülő elemei a `CustomEntries` elemet. Nincs maximális megadható az alárendelt elemek száma korlátozva van.

### <a name="attributes"></a>Attribútumok

Nincs.

### <a name="child-elements"></a>Gyermekelemek

|Elem|Leírás|
|-------------|-----------------|
|[Nézet (formátum) vezérlők CustomEntries CustomEntry elem.](./customentry-element-for-customentries-for-controls-for-view-format.md)|Szükséges eleme.<br /><br /> A vezérlőelem egy definíciót tartalmaz.|

### <a name="parent-elements"></a>Szülőelemek

|Elem|Leírás|
|-------------|-----------------|
|[Vezérlő (formátum) nézet vezérlők CustomControl elem](./customcontrol-element-for-control-for-controls-for-view-format.md)|Határozza meg a nézet által használt vezérlő.|

## <a name="remarks"></a>Megjegyzés

A legtöbb esetben egy vezérlőelem még csak egy definíciót, amely egy megadott `CustomEntry` elemet. Azonban úgy is víc definic adja meg, ha különböző .NET-objektumok megjelenítése ugyanazon vezérlő használata. Ezekben az esetekben definiálhat egy `CustomEntry` elem az egyes objektumok vagy objektumok közül.

## <a name="see-also"></a>Lásd még:

[Nézet (formátum) vezérlők CustomEntries CustomEntry elem.](./customentry-element-for-customentries-for-controls-for-view-format.md)

[Vezérlő (formátum) nézet vezérlők CustomControl elem](./customcontrol-element-for-control-for-controls-for-view-format.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
