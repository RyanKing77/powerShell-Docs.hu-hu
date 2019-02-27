---
title: EntrySelectedBy WideEntry (formátum) a TypeName eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 81a91c74-6229-4b64-aa2b-9123e8b7e9e5
caps.latest.revision: 11
ms.openlocfilehash: be35f6e9e2ad0b2d9a21a91c053aa0f70cafaf9c
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56851463"
---
# <a name="typename-element-for-entryselectedby-for-wideentry-format"></a>A WideEntry elemhez tartozó EntrySelectedBy TypeName eleme (Formátum)

A definíció egy .NET típusát határozza meg. A definíció használatos, amikor az objektum jelenik meg.

Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem WideControl elem (formátum) WideEntries elem (formátum) WideEntry elem (formátum) EntrySelectedBy elem WideEntry (formátum) TypeName elemhez tartozó WideEntry) Formátum)

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
|[EntrySelectedBy eleme WideEntry (formátum)](./entryselectedby-element-for-wideentry-format.md)|A .NET-típusokat, amelyek a széles körű bejegyzés vagy a feltétellel, hogy léteznie kell használni a bejegyzés határozza meg.|

## <a name="text-value"></a>Szöveges érték

Adja meg a teljes nevet, a .NET-típus, például `System.IO.DirectoryInfo`.

## <a name="remarks"></a>Megjegyzés

Minden egyes széles bejegyzést adjon meg legalább egy .NET-típusok, egy kijelölt készlet vagy a kiválasztási feltételnek, amely a definíciójában használt léteznie kell.

Egy széles nézet egyéb összetevőivel kapcsolatos további információkért lásd: [széles nézet létrehozásával](./creating-a-wide-view.md).

## <a name="see-also"></a>Lásd még:

[Egy széles nézet létrehozása](./creating-a-wide-view.md)

[EntrySelectedBy eleme WideEntry (formátum)](./entryselectedby-element-for-wideentry-format.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
