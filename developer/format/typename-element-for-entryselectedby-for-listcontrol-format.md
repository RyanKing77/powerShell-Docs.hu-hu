---
title: EntrySelectedBy ListControl (formátum) a TypeName eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 33c7345c-b808-4c1e-bd54-cb870b407432
caps.latest.revision: 14
ms.openlocfilehash: 0f7216d4dcc0380bceb47ea7c15b3d4a7e5ceeb2
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62084028"
---
# <a name="typename-element-for-entryselectedby-for-listcontrol-format"></a>A ListControl elemhez tartozó EntrySelectedBy TypeName eleme (Formátum)

Ez a bejegyzés a listanézet használó .NET típust határozzon meg. Regisztrációslista-bejegyzés adható meg-típusok száma nincs korlátozva van.

Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézet elem (formátum) ListControl elem (formátum) ListEntries elem (formátum) ListEntry elem (formátum) EntrySelectedBy elem ListEntry (formátum) TypeName elem számára EntrySelectedBy a ListControl (formátum)

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
|[EntrySelectedBy eleme ListEntry (formátum)](./entryselectedby-element-for-listentry-for-listcontrol-format.md)|A .NET-típusokat, amelyek a regisztrációslista-bejegyzés vagy a feltétellel, hogy léteznie kell használni a bejegyzés határozza meg.|

## <a name="text-value"></a>A szöveges érték

Adja meg például a .NET-típus teljes neve `System.IO.DirectoryInfo`.

## <a name="remarks"></a>Megjegyzés

Minden egyes regisztrációslista-bejegyzés rendelkeznie kell legalább egy típusnév, kijelölés set vagy meghatározott kiválasztási feltételnek.

Ez az elem használatának módja a következőben megjelenítheti kapcsolatos további információkért lásd: [listanézet](./creating-a-list-view.md).

## <a name="example"></a>Példa

Az alábbi példa bemutatja, hogyan adjon meg egy kiválasztása a lista nézet bejegyzés.

```xml
<ListEntry>
  <EntrySelectedBy>
    <TypeName>Nameof.NetType</TypeName>
  </EntrySelectedBy>
  <ListItems>...</ListItems>
</ListEntry>
```

## <a name="see-also"></a>Lásd még:

[Lista nézet létrehozása](./creating-a-list-view.md)

[EntrySelectedBy eleme ListEntry (formátum)](./entryselectedby-element-for-listentry-for-listcontrol-format.md)

[A ListEntry (formátum) EntrySelectedBy SelectionSetName elem.](./selectionsetname-element-for-entryselectedby-for-listcontrol-format.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
