---
title: EntrySelectedBy elemet a vezérlők (formátum) konfiguráció CustomEntry |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 30abae8f-c7f7-479d-ad85-19e07ddef204
caps.latest.revision: 10
ms.openlocfilehash: 81eca4f66f0057074612f2d60482b45adc36357b
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62066294"
---
# <a name="entryselectedby-element-for-customentry-for-controls-for-configuration-format"></a>A Konfiguráció Vezérlők eleméhez tartozó CustomEntry EntrySelectedBy eleme (Formátum)

A .NET-típusokat, amelyek a közös vezérlőelem vagy a feltételt, amelyet Pro tento ovládací prvek használandó léteznie kell a definíció határozza meg. Ez az elem szolgál egy közös vezérlőelem a formázási fájlban az összes nézetek által használható meghatározásakor.

Konfigurációs elem (formátum) vezérlők elem Configuration (formátum) vezérlőelem elem vezérlők, a vezérlő konfigurációs (formátum) CustomEntries elemhez tartozó CustomControl Configuration (a Configuration (formátum) CustomControl elem Formátum) CustomEntry elemet a vezérlők CustomEntry vezérlők (formátum) konfiguráció esetén a Configuration (formátum) EntrySelectedBy elemhez CustomControl

## <a name="syntax"></a>Szintaxis

```xml
<EntrySelectedBy>
  <TypeName>Nameof.NetType</TypeName>
  <SelectionSetName>SelectionSet</SelectionSetName>
  <SelectionCondition>...</SelectionCondition>
</EntrySelectedBy>
```

## <a name="attributes-and-elements"></a>Attribútumok és elemek

A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `EntrySelectedBy` elemet.

### <a name="attributes"></a>Attribútumok

Nincs.

### <a name="child-elements"></a>Gyermekelemek

|Elem|Leírás|
|-------------|-----------------|
|[Konfiguráció (formátum) vezérlők EntrySelectedBy SelectionCondition elem.](./selectioncondition-element-for-entryselectedby-for-controls-for-configuration-format.md)|Nem kötelező eleme.<br /><br /> Határozza meg azt a feltételt, amelyet a közös ellenőrzési definíciójában használt léteznie kell.|
|[Konfiguráció (formátum) vezérlők EntrySelectedBy SelectionSetName elem.](./selectionsetname-element-for-selectioncondition-for-controls-for-configuration-format.md)|Nem kötelező eleme.<br /><br /> Ez a definíció, a közös ellenőrzési használó .NET-típusok egy halmazát határozza meg.|
|[Konfiguráció (formátum) vezérlők EntrySelectedBy TypeName elem.](./typename-element-for-entryselectedby-for-controls-for-configuration-format.md)|Nem kötelező eleme.<br /><br /> Ez a definíció, a közös ellenőrzési használó .NET típust határozzon meg.|

### <a name="parent-elements"></a>Szülőelemek

|Elem|Leírás|
|-------------|-----------------|
|[Konfiguráció (formátum) vezérlők CustomControl CustomEntry elem.](./customentry-element-for-customcontrol-for-controls-for-configuration-format.md)|A közös ellenőrzési definíciójának biztosít.|

## <a name="remarks"></a>Megjegyzés

Legalább egyes definíció rendelkeznie kell legalább egy .NET-típus, kijelölés set vagy a megadott kiválasztási feltétel. Nincs típusa, a kijelölt csoportok, illetve a kiválasztási feltételek, Ön által megadott számú maximális korlátozva.

## <a name="see-also"></a>Lásd még:

[Konfiguráció (formátum) vezérlők EntrySelectedBy SelectionCondition elem.](./selectioncondition-element-for-entryselectedby-for-controls-for-configuration-format.md)

[Konfiguráció (formátum) vezérlők EntrySelectedBy SelectionSetName elem.](./selectionsetname-element-for-selectioncondition-for-controls-for-configuration-format.md)

[Konfiguráció (formátum) vezérlők CustomControl CustomEntry elem.](./customentry-element-for-customcontrol-for-controls-for-configuration-format.md)

[Konfiguráció (formátum) vezérlők EntrySelectedBy TypeName elem.](./typename-element-for-selectioncondition-for-controls-for-configuration-format.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
