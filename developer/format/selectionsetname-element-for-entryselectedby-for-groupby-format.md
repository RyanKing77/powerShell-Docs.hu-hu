---
title: A GroupBy (formátum) EntrySelectedBy SelectionSetName eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: d569c623-2277-49e3-933e-c26262b91cd5
caps.latest.revision: 6
ms.openlocfilehash: 69cd113c444b4e3c5dceabcdfddb439cd1376f6b
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56848810"
---
# <a name="selectionsetname-element-for-entryselectedby-for-groupby-format"></a>A GroupBy elemhez tartozó EntrySelectedBy SelectionSetName eleme (Formátum)

Regisztrációslista-bejegyzés a .NET-objektumokat egy halmazát határozza meg. Nincs kijelölt csoportok bejegyzés adható meg száma nincs korlátozva. Ez az elem szolgál, hogyan jelenjen meg az objektumok egy új csoportot meghatározásakor.

Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem GroupBy elem megtekintése (formátum) CustomControl elem a GroupBy (formátum) CustomEntry elemhez tartozó CustomControl GroupBy (formátum) CustomEntries elemhez GroupBy (formátum) EntrySelectedBy elem CustomEntry EntrySelectedBy GroupBy (formátum) esetében a GroupBy (formátum) SelectionSetName elemhez tartozó CustomControl

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
|[A GroupBy (formátum) CustomEntry EntrySelectedBy elem.](./entryselectedby-element-for-customentry-for-groupby-format.md)|A .NET-típusokat, amelyek egyéni tételhez vagy a feltétellel, hogy léteznie kell használni a bejegyzés határozza meg.|

## <a name="text-value"></a>Szöveges érték

Adja meg a kijelölt csoport nevét.

## <a name="remarks"></a>Megjegyzés

Minden egyes egyéni vezérlőt definíció rendelkeznie kell legalább egy típusnév, kijelölés set vagy meghatározott kiválasztási feltételnek.

Kijelölt csoportok általában akkor használják, ha meg szeretné több nézetében lévő meghatározott felhasználói csoporttal használt objektumok. Például előfordulhat, hogy szeretne létrehozni a táblázatos nézetre, és megjelenítheti a ugyanazt az objektumhalmazt tartalmazza. Kijelölt csoportok meghatározása kapcsolatos további információkért lásd: [meghatározása beállítja a kijelölés](./defining-selection-sets.md).

Egyéni vezérlő nézet az összetevőivel kapcsolatos további információkért lásd: [egyéni vezérlők létrehozását](./creating-custom-controls.md).

## <a name="see-also"></a>Lásd még:

[A GroupBy (formátum) CustomEntry EntrySelectedBy elem.](./entryselectedby-element-for-customentry-for-groupby-format.md)

[Egyéni vezérlők létrehozását](./creating-custom-controls.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
