---
title: A GroupBy (formátum) CustomControl CustomEntries eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: af83c0f6-7fdd-4aa0-af12-efc62f632974
caps.latest.revision: 7
ms.openlocfilehash: f073142bf836ae892f161cf8c36ed16c35e311f5
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56845184"
---
# <a name="customentries-element-for-customcontrol-for-groupby-format"></a>A GroupBy CustomControl elemének CustomEntries eleme (Formátum)

A definíciók vezérlő biztosít. Ez az elem szolgál, hogyan jelenjen meg az objektumok egy új csoportot meghatározásakor.

Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem GroupBy elem megtekintése (formátum) CustomControl elem GroupBy (formátum) CustomEntries elemhez tartozó CustomControl a GroupBy (formátum)

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
|[A GroupBy (formátum) CustomControl CustomEntry elem.](./customentry-element-for-customcontrol-for-groupby-format.md)|Szükséges eleme.<br /><br /> A vezérlőelem egy definíciót tartalmaz.|

### <a name="parent-elements"></a>Szülőelemek

|Elem|Leírás|
|-------------|-----------------|
|[GroupBy (formátum) CustomControl elem.](./customcontrol-element-for-groupby-format.md)|Határozza meg az egyéni vezérlő, amely megjeleníti az új csoport.|

## <a name="remarks"></a>Megjegyzés

A legtöbb esetben egy vezérlőelem még csak egy definíciót, amely egy megadott `CustomEntry` elemet. Azonban úgy is víc definic adja meg, ha ugyanazon vezérlő használata a különböző csoportok megjelenítéséhez. Ezekben az esetekben definiálhat egy `CustomEntry` elem egy csoportra.

## <a name="see-also"></a>Lásd még:

[Nézet (formátum) vezérlők CustomEntries CustomEntry elem.](./customentry-element-for-customentries-for-controls-for-view-format.md)

[GroupBy (formátum) CustomControl elem.](./customcontrol-element-for-groupby-format.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
