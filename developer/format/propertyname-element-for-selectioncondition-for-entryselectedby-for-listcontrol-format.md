---
title: SelectionCondition EntrySelectedBy ListControl (formátum) esetében a PropertyName eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 71c3f1f6-6fe2-42f1-8260-6974d3871748
caps.latest.revision: 11
ms.openlocfilehash: f857f5944b9e971215a06d6f5c39f7c22c6cf99f
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56844918"
---
# <a name="propertyname-element-for-selectioncondition-for-entryselectedby-for-listcontrol-format"></a>Az ListControl EntrySelectedBy eleméhez tartozó SelectionCondition PropertyName eleme (Formátum)

Megadja a .NET-tulajdonság, amely elindítja a feltételt. Ha ez a tulajdonság jelen-e, vagy ha való kiértékelése által `true`, a feltétel nem teljesül, és a regisztrációslista-bejegyzés szolgál.

Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézet elem (formátum) ListControl elem (formátum) ListEntries elem (formátum) ListEntry elem (formátum) EntrySelectedBy elem ListEntry (formátum) SelectionCondition elem számára A PropertyName elem ListEntry (formátum) a SelectionCondition EmtrySelectedBy ListEntry (formátum) esetében a EntrySelectedBy

## <a name="syntax"></a>Szintaxis

```xml
<PropertyName>.NetTypeProperty</PropertyName>
```

## <a name="attributes-and-elements"></a>Attribútumok és elemek

A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `PropertyName` elemet.

### <a name="attributes"></a>Attribútumok

Nincs.

### <a name="child-elements"></a>Gyermekelemek

Nincs.

### <a name="parent-elements"></a>Szülőelemek

|Elem|Leírás|
|-------------|-----------------|
|[A ListEntry (formátum) EntrySelectedBy SelectionCondition elem.](./selectioncondition-element-for-entryselectedby-for-listcontrol-format.md)|Meghatározza a feltétellel, hogy a lista bejegyzés használandó léteznie kell.|

## <a name="text-value"></a>Szöveges érték

Adja meg a .NET-tulajdonság neve.

## <a name="remarks"></a>Megjegyzés

A kiválasztási feltételnek legalább egy tulajdonság nevét, vagy parancsprogram-blokkot kell megadnia, de nem adható meg egyszerre. Kiválasztási feltételek használatával kapcsolatos további információkért lásd: [definiáló vonatkozó feltételeket, amikor egy nézet bejegyzés vagy az elem](./defining-conditions-for-displaying-data.md).

A listanézet egyéb összetevőivel kapcsolatos további információkért lásd: [lista nézet létrehozása](./creating-a-list-view.md).

## <a name="see-also"></a>Lásd még:

[Lista nézet létrehozása](./creating-a-list-view.md)

[Megjelenik feltételeket, amikor adatok meghatározása](./defining-conditions-for-displaying-data.md)

[ListEntry elem (formátum)](./listentry-element-for-listcontrol-format.md)

[SelectionCondition EntrySelectedBy ListEntry (formátum) esetében a scriptblock kulcsszót elem.](./scriptblock-element-for-selectioncondition-for-entryselectedby-for-listcontrol-format.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
