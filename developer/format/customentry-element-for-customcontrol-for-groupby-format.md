---
title: A GroupBy (formátum) CustomControl CustomEntry eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 2987cb45-f646-45d4-b81b-7871e77af36f
caps.latest.revision: 5
ms.openlocfilehash: dcf4f8b2bbd422067ffdf9b3b4972e279e91edf9
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62066484"
---
# <a name="customentry-element-for-customcontrol-for-groupby-format"></a>A GroupBy CustomControl elemének CustomEntry eleme (Formátum)

A vezérlőelem egy definíciót tartalmaz. Ez az elem szolgál, hogyan jelenjen meg az objektumok egy új csoportot meghatározásakor.

Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem GroupBy elem megtekintése (formátum) CustomControl elem a GroupBy (formátum) CustomEntry elemhez tartozó CustomControl GroupBy (formátum) CustomEntries elemhez CustomControl a GroupBy (formátum)

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
|[A GroupBy (formátum) CustomEntry EntrySelectedBy elem.](./entryselectedby-element-for-customentry-for-groupby-format.md)|Nem kötelező eleme.<br /><br /> A .NET-típusokat, amelyek a vezérlő definition vagy a feltétellel, hogy léteznie kell a definíció használandó határozza meg.|
|[A GroupBy (formátum) CustomEntry CustomItem elem.](./customitem-element-for-customentry-for-groupby-format.md)|Szükséges eleme.<br /><br /> Határozza meg, hogyan a vezérlőelem megjeleníti-e az adatokat.|

### <a name="parent-elements"></a>Szülőelemek

|Elem|Leírás|
|-------------|-----------------|
|[A GroupBy (formátum) CustomControl CustomEntries elem.](./customentries-element-for-customcontrol-for-groupby-format.md)|A definíciók vezérlő biztosít.|

## <a name="remarks"></a>Megjegyzés

## <a name="see-also"></a>Lásd még:

[A GroupBy (formátum) CustomEntry EntrySelectedBy elem.](./entryselectedby-element-for-customentry-for-groupby-format.md)

[A GroupBy (formátum) CustomEntry CustomItem elem.](./customitem-element-for-customentry-for-groupby-format.md)

[A GroupBy (formátum) CustomControl CustomEntries elem.](./customentries-element-for-customcontrol-for-groupby-format.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
