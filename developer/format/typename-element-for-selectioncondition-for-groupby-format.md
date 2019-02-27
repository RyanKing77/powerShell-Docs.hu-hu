---
title: A GroupBy (formátum) SelectionCondition TypeName eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 290d38e3-b9bd-4382-9671-2e28b32b7260
caps.latest.revision: 6
ms.openlocfilehash: a4036b1e9de85da7e0029e02cca9e0eaed462f70
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56848775"
---
# <a name="typename-element-for-selectioncondition-for-groupby-format"></a>A GroupBy elemhez tartozó SelectionCondition TypeName eleme (Formátum)

A .NET típusát, amely elindítja a feltételt határozza meg. Ez az elem szolgál, hogyan jelenjen meg az objektumok egy új csoportot meghatározásakor.

Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem GroupBy elem megtekintése (formátum) CustomControl elem a GroupBy (formátum) CustomEntry elemhez tartozó CustomControl GroupBy (formátum) CustomEntries elemhez GroupBy (formátum) EntrySelectedBy elem CustomEntry EntrySelectedBy SelectionCondition GroupBy (formátum) esetében a GroupBy (formátum) TypeName elemhez tartozó GroupBy (formátum) SelectionCondition elemhez tartozó CustomControl

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
|[A GroupBy (formátum) EntrySelectedBy SelectionCondition elem.](./selectioncondition-element-for-entryselectedby-for-groupby-format.md)|Határozza meg egy feltételt, amely a vezérlőelem definíciójában használt léteznie kell.|

## <a name="text-value"></a>Szöveges érték

Adja meg a teljes nevet, a .NET-típus, például `System.IO.DirectoryInfo`.

## <a name="remarks"></a>Megjegyzés

Ha ez az elem meg van adva, nem adható meg a `SelectionSetName` elemet. További információ a kiválasztási feltételek meghatározása: [feltételek meghatározása az adatok megjelenítése](./defining-conditions-for-displaying-data.md).

## <a name="see-also"></a>Lásd még:

[A GroupBy (formátum) EntrySelectedBy SelectionCondition elem.](./selectioncondition-element-for-entryselectedby-for-groupby-format.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
