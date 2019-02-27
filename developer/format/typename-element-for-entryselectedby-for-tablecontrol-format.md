---
title: EntrySelectedBy TableControl (formátum) a TypeName eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: fd872ada-d476-4c4d-a788-ccac3f983070
caps.latest.revision: 10
ms.openlocfilehash: 7bbb47268a23fcb37a34e2287a6ce949313a13bb
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56846619"
---
# <a name="typename-element-for-entryselectedby-for-tablecontrol-format"></a>A TableControl elemhez tartozó EntrySelectedBy TypeName eleme (Formátum)

Ez a bejegyzés a táblázat nézet használó .NET típust határozzon meg. A tábla bejegyzés adható meg-típusok száma nincs korlátozva van.

Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem TableControl elem (formátum) TableRowEntries elem (formátum) TableRowEntry elem (formátum) EntrySelectedBy elem (formátum) TypeName eleme EntrySelectedBy a TableRowEntry (formátum)

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
|[EntrySelectedBy elem (formátum)](./entryselectedby-element-for-tablerowentry-for-tablecontrol-format.md)|A .NET-típusokat, amelyek ezt a bejegyzést, vagy a feltétellel, hogy léteznie kell használni a bejegyzés határozza meg.|

## <a name="text-value"></a>Szöveges érték

Adja meg a .NET-típus nevét.

## <a name="remarks"></a>Megjegyzés

Minden egyes regisztrációslista-bejegyzés rendelkeznie kell legalább egy típusnév, kijelölés set vagy meghatározott kiválasztási feltételnek.

A táblázatos nézetre az összetevőivel kapcsolatos további információkért lásd: [tábla nézetek létrehozásával](./creating-a-table-view.md).

## <a name="see-also"></a>Lásd még:

[Tábla nézet létrehozása](./creating-a-table-view.md)

[EntrySelectedBy elem (formátum)](./entryselectedby-element-for-tablerowentry-for-tablecontrol-format.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
