---
title: A GroupBy (formátum) EntrySelectedBy TypeName eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: b8b6739b-770c-432a-95ab-551c7507c51f
caps.latest.revision: 6
ms.openlocfilehash: 3b5ce60d3a0d76988af48f49445a5478a415d498
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56850777"
---
# <a name="typename-element-for-entryselectedby-for-groupby-format"></a>A GroupBy elemhez tartozó EntrySelectedBy TypeName eleme (Formátum)

Ez a definíció az egyéni vezérlő használó .NET típust határozzon meg. Ez az elem szolgál, hogyan jelenjen meg az objektumok egy új csoportot meghatározásakor.

Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem GroupBy elem megtekintése (formátum) CustomControl elem a GroupBy (formátum) CustomEntry elemhez tartozó CustomControl GroupBy (formátum) CustomEntries elemhez CustomControl GroupBy (formátum) EntrySelectedBy elemhez tartozó CustomEntry GroupBy (formátum) TypeName elemhez tartozó EntrySelectedBy a GroupBy (formátum)

## <a name="syntax"></a>Szintaxis

```xml
<TypeName>Nameof.NetType</TypeName>
```

## <a name="attributes-and-elements"></a>Attribútumok és elemek

A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `TypeName` elemet.

### <a name="attributes"></a>Attribútumok

Nincs.

### <a name="child-elements"></a>Gyermekelemek

Nincs.

### <a name="parent-elements"></a>Szülőelemek

|Elem|Leírás|
|-------------|-----------------|
|[A GroupBy (formátum) CustomEntry EntrySelectedBy elem.](./entryselectedby-element-for-customentry-for-groupby-format.md)|A .NET-típusokat, amelyek a vezérlő definition vagy a feltétellel, hogy léteznie kell a definíció használandó határozza meg.|

## <a name="text-value"></a>Szöveges érték

Adja meg a teljes nevet, a .NET-típus, például `System.IO.DirectoryInfo`.

## <a name="remarks"></a>Megjegyzés

Minden vezérlő definíció rendelkeznie kell legalább egy típusnév, kijelölés set vagy meghatározott kiválasztási feltételnek.

Egyéni vezérlő nézet az összetevőivel kapcsolatos további információkért lásd: [egyéni vezérlők létrehozását](./creating-custom-controls.md).

## <a name="see-also"></a>Lásd még:

[Egyéni vezérlők létrehozását](./creating-custom-controls.md)

[A GroupBy (formátum) CustomEntry EntrySelectedBy elem.](./entryselectedby-element-for-customentry-for-groupby-format.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
