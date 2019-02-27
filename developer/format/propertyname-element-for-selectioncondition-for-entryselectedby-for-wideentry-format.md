---
title: SelectionCondition EntrySelectedBy WideEntry (formátum) esetében a PropertyName eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 340abb12-6df1-42f4-bdae-b0509c90952c
caps.latest.revision: 11
ms.openlocfilehash: 196877b97db9ed0592e357486c1318dc1e7efd31
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56849902"
---
# <a name="propertyname-element-for-selectioncondition-for-entryselectedby-for-wideentry-format"></a>Az WideEntry EntrySelectedBy eleméhez tartozó SelectionCondition PropertyName eleme (Formátum)

Megadja a .NET-tulajdonság, amely elindítja a feltételt. Ha ez a tulajdonság jelen-e, vagy ha való kiértékelése által `true`, a feltétel nem teljesül, és a definíció szolgál.

Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézet elem (formátum) WideControl elem (formátum) WideEntries elem (formátum) WideEntry elem (formátum) EntrySelectedBy elem WideEntry (formátum) SelectionCondition elem számára A PropertyName elem WideEntry (formátum) a SelectionCondition EntrySelectedBy WideEntry (formátum) esetében a EntrySelectedBy

## <a name="syntax"></a>Szintaxis

```xml
<PropertyName>.NetTypeProperty</PropertyName>
```

```csharp

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
|[A WideEntry (formátum) EntrySelectedBy SelectionCondition elem.](./selectioncondition-element-for-entryselectedby-for-widecontrol-format.md)|Határozza meg azt a feltételt, amelyet a definíció használandó léteznie kell.|

## <a name="text-value"></a>Szöveges érték

Adja meg a .NET-tulajdonság neve.

## <a name="remarks"></a>Megjegyzés

A kiválasztási feltétel meg kell adnia legalább egy tulajdonság neve vagy a parancsfájl kiértékelése, de nem adható meg egyszerre. Kiválasztási feltételek használatával kapcsolatos további információkért lásd: [feltételeinek meghatározása mikor jelenik meg adat](./defining-conditions-for-displaying-data.md).

Egy széles nézet egyéb összetevőivel kapcsolatos további információkért lásd: [széles nézet](./creating-a-wide-view.md).

## <a name="see-also"></a>Lásd még:

[Egy széles nézet létrehozása](./creating-a-wide-view.md)

[Mikor jelenik meg adat feltételeinek meghatározása](./defining-conditions-for-displaying-data.md)

[SelectionCondition EntrySelectedBy WideEntry (formátum) esetében a scriptblock kulcsszót elem.](./scriptblock-element-for-selectioncondition-for-entryselectedby-for-widecontrol-format.md)

[A WideEntry (formátum) EntrySelectedBy SelectionCondition elem.](./selectioncondition-element-for-entryselectedby-for-widecontrol-format.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
