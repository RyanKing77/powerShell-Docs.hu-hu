---
title: SelectionSetName elemet a vezérlők (formátum) konfiguráció SelectionCondition |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 7dcaeadb-4e79-47a0-96e2-8952af26abbe
caps.latest.revision: 7
ms.openlocfilehash: 5db35a8094ea2bb966c8d6a96802c72f64c05c17
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56848306"
---
# <a name="selectionsetname-element-for-selectioncondition-for-controls-for-configuration-format"></a>A Konfiguráció Vezérlők eleméhez tartozó SelectionCondition SelectionSetName eleme (Formátum)

Megadja azt a feltételt .NET típusú. Az ebben a készletben típusok találhatók, ha a feltétel nem teljesül, és az objektum megjelenik a vezérlőelem használatával. Ez az elem szolgál egy közös vezérlőelem a formázási fájlban az összes nézetek által használható meghatározásakor.

Konfigurációs elem (formátum) vezérlők elem Configuration (formátum) vezérlőelem elem vezérlők Configuration (formátum) CustomEntries elemhez tartozó CustomControl vezérlők, a vezérlő konfigurációja (formátum) CustomControl elemhez Konfiguráció (formátum) CustomEntry elemet a vezérlők, a Configuration (formátum) EntrySelectedBy elem CustomEntry vezérlők, a vezérlők, a EntrySelectedBy Configuration (formátum) SelectionCondition elemhez tartozó CustomControl Konfiguráció (formátum) SelectionSetName eleme SelectionCondition vezérlők konfiguráció (formátum)

## <a name="syntax"></a>Szintaxis

```xml
<SelectionSetName>NameofSelectionSet</SelectionSetName>
```

## <a name="attributes-and-elements"></a>Attribútumok és elemek

A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `SelectionSetName` elemet.

### <a name="attributes"></a>Attribútumok

Nincs.

### <a name="child-elements"></a>Gyermekelemek

Nincs.

### <a name="parent-elements"></a>Szülőelemek

|Elem|Leírás|
|-------------|-----------------|
|[Konfiguráció (formátum) vezérlők EntrySelectedBy SelectionCondition elem.](./selectioncondition-element-for-entryselectedby-for-controls-for-configuration-format.md)|Határozza meg egy feltételt, amely a vezérlőelem definíciójában használt léteznie kell.|

## <a name="text-value"></a>Szöveges érték

Adja meg a kijelölt csoport nevét.

## <a name="remarks"></a>Megjegyzés

Kijelölés sets csoportjai közös nézeten, amely meghatározza a formázási fájl által használható .NET-objektumokat. Létrehozásával és a kijelölt csoportok hivatkozó kapcsolatos további információkért lásd: [meghatározása beállítja az objektumok](./defining-selection-sets.md).

A kiválasztási feltétel egy kijelölés set vagy a .NET-típus is megadhat, de nem adható meg egyszerre. Kiválasztási feltételek használatával kapcsolatos további információkért lásd: [feltételek meghatározása az adatok megjelenítése](./defining-conditions-for-displaying-data.md).

## <a name="see-also"></a>Lásd még:

[Konfiguráció (formátum) vezérlők EntrySelectedBy SelectionCondition elem.](./selectioncondition-element-for-entryselectedby-for-controls-for-configuration-format.md)

[Mikor jelenik meg adat feltételeinek meghatározása](./defining-conditions-for-displaying-data.md)

[Kijelölt csoportok meghatározása](./defining-selection-sets.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
