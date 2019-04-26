---
title: CustomEntry elemet a vezérlők (formátum) nézet CustomEntries |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: c6739205-2bc9-4507-b2af-d19d548c2057
caps.latest.revision: 6
ms.openlocfilehash: b92b99d88992cf13dbf7bfbe88aad603615f3138
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62066498"
---
# <a name="customentry-element-for-customentries-for-controls-for-view-format"></a>A Nézet Vezérlők eleméhez tartozó CustomEntries CustomEntry eleme (Formátum)

A vezérlőelem egy definíciót tartalmaz. Ez az elem szolgál a nézet által használható vezérlők meghatározásakor.

Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem vezérlők elem (formátum) vezérlőelem elem vezérlők, a nézet (formátum) CustomControl elem megtekintése (formátum) CustomEntries elemet a vezérlők a vezérlő A vezérlők (formátum) nézet CustomEntries megtekintése (formátum) CustomEntry elemhez CustomControl

## <a name="syntax"></a>Szintaxis

```xml
<CustomEntry>
  <EntrySelectedBy>...</EntrySelectedBy>
  <CustomItem>...</CustomItem>
</CustomEntry>
```

## <a name="attributes-and-elements"></a>Attribútumok és elemek

A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a szülő elemei a `CustomEntry` elemet.

### <a name="attributes"></a>Attribútumok

Nincs.

### <a name="child-elements"></a>Gyermekelemek

|Elem|Leírás|
|-------------|-----------------|
|[Nézet (formátum) vezérlők CustomEntry EntrySelectedBy elem.](./entryselectedby-element-for-customentry-for-controls-for-view-format.md)|Nem kötelező eleme.<br /><br /> A .NET-típusokat, amelyek a vezérlő definition vagy a feltétellel, hogy léteznie kell a definíció használandó határozza meg.|
|[Nézet (formátum) vezérlők CustomEntry CustomItem elem.](./customitem-element-for-customentry-for-controls-for-view-format.md)|Szükséges eleme.<br /><br /> Határozza meg, hogyan a vezérlőelem megjeleníti-e az adatokat.|

### <a name="parent-elements"></a>Szülőelemek

|Elem|Leírás|
|-------------|-----------------|
|[A nézet (formátum) CustomControl CustomEntries elem](./customentries-element-for-customcontrol-for-view-format.md)|A definíciók vezérlő biztosít.|

## <a name="remarks"></a>Megjegyzés

## <a name="see-also"></a>Lásd még:

[A nézet (formátum) CustomControl CustomEntries elem](./customentries-element-for-customcontrol-for-view-format.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
