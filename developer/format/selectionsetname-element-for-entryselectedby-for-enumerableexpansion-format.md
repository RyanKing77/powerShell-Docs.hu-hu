---
title: EnumerableExpansion (formátum) a EntrySelectedBy SelectionSetName eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 936d09f2-2c48-49e8-ab2d-0c8729199a2e
caps.latest.revision: 8
ms.openlocfilehash: 8ba8931ea5e34f610878351396cad42023393ad6
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56851533"
---
# <a name="selectionsetname-element-for-entryselectedby-for-enumerableexpansion-format"></a>Az EnumerableExpansion elemhez tartozó EntrySelectedBy SelectionSetName eleme (Formátum)

Megadja, hogy ez a definíció szerint bontva .NET típusú.

Konfigurációs elem (formátum) DefaultSettings elem (formátum) EnumerableExpansions elem (formátum) EnumerableExpansion elem (formátum) EntrySelectedBy elem esetében a EntrySelectedBy EnumerableExpansion (formátum) SelectionSetName elemhez EnumerableExpansion (formátum)

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
|[EntrySelectedBy eleme EnumerableExpansion (formátum)](./entryselectedby-element-for-enumerableexpansion-format.md)|Meghatározza a .NET-gyűjtemény objektumok, amelyek a definíció szerint bontva.|

## <a name="text-value"></a>Szöveges érték

Adja meg a kijelölt csoport nevét.

## <a name="remarks"></a>Megjegyzés

Minden egyes definíciójában meg kell adni, egy vagy több típus nevét, egy kijelölt készlet vagy kiválasztási feltétel.

Kijelölt csoportok általában akkor használják, ha meg szeretné több nézetében lévő meghatározott felhasználói csoporttal használt objektumok. Például előfordulhat, hogy szeretne létrehozni a táblázatos nézetre, és megjelenítheti a ugyanazt az objektumhalmazt tartalmazza. Kijelölt csoportok meghatározása kapcsolatos további információkért lásd: [meghatározása beállítja az objektumok megjelenítéséhez](./defining-selection-sets.md).

## <a name="see-also"></a>Lásd még:

[Kijelölt csoportok meghatározása](./defining-selection-sets.md)

[EntrySelectedBy eleme EnumerableExpansion (formátum)](./entryselectedby-element-for-enumerableexpansion-format.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
