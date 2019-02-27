---
title: TableControl (formátum) a EntrySelectedBy SelectionSetName eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 5dd0bd5d-f206-4cc6-a0f8-70700ee2c4b7
caps.latest.revision: 8
ms.openlocfilehash: 819906127e81355c45103ede85ef3608e1c1cfeb
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56846878"
---
# <a name="selectionsetname-element-for-entryselectedby-for-tablecontrol-format"></a>A TableControl elemhez tartozó EntrySelectedBy SelectionSetName eleme (Formátum)

Megadja a .NET készletét típusok használatát a bejegyzés a táblázat nézet. Nincs kijelölt csoportok bejegyzés adható meg száma nincs korlátozva.

Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézet elem (formátum) TableControl elem (formátum) TableRowEntries elem (formátum) TableRowEntry elem (formátum) EntrySelectedBy elem (formátum) SelectionSetName elem számára EntrySelectedBy a TableRowEntry (formátum)

## <a name="syntax"></a>Szintaxis

```xml
<SelectionSetName>NameofSelectionSet</SelectionSetName>
```

## <a name="attributes-and-elements"></a>Attribútumok és elemek

A következő szakaszok ismertetik az attribútumokat, a gyermekelemek és a szülő elemeket.

### <a name="attributes"></a>Attribútumok

Nincs.

### <a name="child-elements"></a>Gyermekelemek

Nincs.

### <a name="parent-elements"></a>Szülőelemek

|Elem|Leírás|
|-------------|-----------------|
|[EntrySelectedBy elem (formátum)](./entryselectedby-element-for-tablerowentry-for-tablecontrol-format.md)|A .NET-típusokat, amelyek ezt a bejegyzést, vagy a feltétellel, hogy léteznie kell használni a bejegyzés határozza meg.|

## <a name="text-value"></a>Szöveges érték

Adja meg a kijelölt csoport nevét.

## <a name="remarks"></a>Megjegyzés

Kijelölt csoportok általában akkor használják, ha meg szeretné több nézetében lévő meghatározott felhasználói csoporttal használt objektumok. Például előfordulhat, hogy szeretne létrehozni a táblázatos nézetre, és megjelenítheti a ugyanazt az objektumhalmazt tartalmazza. Kijelölt csoportok meghatározása kapcsolatos további információkért lásd: [meghatározása beállítja az objektumok megjelenítéséhez](./defining-selection-sets.md).

Ha megad egy kiválasztása a bejegyzés, típusnév nem adható meg. Typ .NET meghatározásával kapcsolatos további információkért lásd: [EntrySelectedBy TableRowEntry (formátum) a TypeName eleme](./typename-element-for-entryselectedby-for-tablecontrol-format.md).

A táblázatos nézetre az összetevőivel kapcsolatos további információkért lásd: [tábla nézetek létrehozásával](./creating-a-table-view.md).

## <a name="see-also"></a>Lásd még:

[EntrySelectedBy elem (formátum)](./entryselectedby-element-for-tablerowentry-for-tablecontrol-format.md)

[A nézet csoportjaira meghatározása](./defining-selection-sets.md)

[Tábla nézet létrehozása](./creating-a-table-view.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
