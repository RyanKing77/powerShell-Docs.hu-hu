---
title: A nézet (formátum) CustomEntry EntrySelectedBy TypeName eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 76548af7-05bd-4d12-bf71-6fb69c434ef2
caps.latest.revision: 10
ms.openlocfilehash: c3dd761cd9b6c468d4833ea35b897ba5d425f598
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62083977"
---
# <a name="typename-element-for-entryselectedby-for-customentry-for-view-format"></a>A Nézet CustomEntry eleméhez tartozó EntrySelectedBy TypeName eleme (Formátum)

Ez a definíció az egyéni vezérlő nézet használó .NET típust határozzon meg. Nincs korlátozva a definíciófrissítés számára megadható típusok számával.

Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézet elem (formátum) CustomControl elem (formátum) CustomEntries eleme CustomControl számára a nézet (formátum) EntrySelectedBy CustomEntries megtekintése (formátum) CustomEntry elemhez Megtekintése (formátum) TypeName elemhez tartozó EntrySelectedBy CustomEntry nézet (formátum) a CustomEntry elem.

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
|[A nézet (formátum) CustomEntry EntrySelectedBy elem](./entryselectedby-element-for-customentry-for-customcontrol-for-view-format.md)|A .NET-típusokat, amelyek az egyéni vezérlő nézetdefinícióban, vagy a feltétellel, hogy léteznie kell a definíció használandó határoz meg.|

## <a name="text-value"></a>A szöveges érték

Adja meg a teljes nevet, a .NET-típus, például `System.IO.DirectoryInfo`.

## <a name="remarks"></a>Megjegyzés

Minden egyes egyéni vezérlőt nézetdefiníció rendelkeznie kell legalább egy típusnév, kijelölés set vagy meghatározott kiválasztási feltételnek.

Egyéni vezérlő nézet az összetevőivel kapcsolatos további információkért lásd: [egyéni vezérlők létrehozását](./creating-custom-controls.md).

## <a name="see-also"></a>Lásd még:

[Egyéni vezérlők létrehozását](./creating-custom-controls.md)

[A nézet (formátum) CustomEntry EntrySelectedBy elem](./entryselectedby-element-for-customentry-for-customcontrol-for-view-format.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
