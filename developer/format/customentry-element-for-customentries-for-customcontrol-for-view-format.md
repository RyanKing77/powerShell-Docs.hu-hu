---
title: A nézet (formátum) CustomControl CustomEntries CustomEntry eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: ac3c0a25-f2ca-4e28-b3dc-9cb06a76d92a
caps.latest.revision: 11
ms.openlocfilehash: 7804155bffeb1f0df8339f797bf59f8def56a3fc
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62066447"
---
# <a name="customentry-element-for-customentries-for-customcontrol-for-view-format"></a>A Nézet CustomControl eleméhez tartozó CustomEntries CustomEntry eleme (Formátum)

Az egyéni vezérlő nézet definíciójának biztosít.

Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem CustomControl elem (formátum) CustomEntries eleme CustomControl megtekintése (formátum) CustomEntry elemhez tartozó CustomEntries nézet (formátum)

## <a name="syntax"></a>Szintaxis

```xml
<CustomEntry>
  <EntrySelectedBy>...</EntrySelectedBy>
  <CustomItem>...</CustomItem>
</CustomEntry>
```

## <a name="attributes-and-elements"></a>Attribútumok és elemek

A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `CustomEntry` elemet. Meg kell adnia a cikkeket a definíció szerint jelenik meg.

### <a name="attributes"></a>Attribútumok

Nincs.

### <a name="child-elements"></a>Gyermekelemek

|Elem|Leírás|
|-------------|-----------------|
|[A nézet (formátum) CustomEntry EntrySelectedBy elem](./entryselectedby-element-for-customentry-for-customcontrol-for-view-format.md)|Nem kötelező eleme.<br /><br /> A .NET-típusokat, amelyek az egyéni vezérlő nézet vagy a feltétellel, hogy léteznie kell a definíció használandó meghatározását, határozza meg.|
|[A nézet (formátum) CustomEntry CustomItem elem](./customitem-element-for-customentry-for-customcontrol-for-view-format.md)|Határozza meg az egyéni vezérlő definíciója egy vezérlőelemet.|

### <a name="parent-elements"></a>Szülőelemek

|Elem|Leírás|
|-------------|-----------------|
|[A nézet (formátum) CustomControl CustomEntries elem](./customentries-element-for-customcontrol-for-view-format.md)|Az egyéni vezérlő nézetében a definíciókat tartalmazza. Az egyéni vezérlő nézetében meg kell adnia egy vagy több definíciót.|

## <a name="remarks"></a>Megjegyzés

A legtöbb esetben csak egyetlen definíciót minden egyes egyéni vezérlőt nézet megadása kötelező, de lehetséges több definíciókkal rendelkeznek, ha ugyanabban a nézetben különböző .NET-objektumok megjelenítéséhez használandó. Ezekben az esetekben adja meg egy külön meghatározása az egyes objektumok vagy objektumok közül.

## <a name="see-also"></a>Lásd még:

[CustomControl elem nézet (formátum)](./customcontrol-element-for-view-format.md)

[A nézet (formátum) CustomEntry CustomItem elem](./customitem-element-for-customentry-for-customcontrol-for-view-format.md)

[A nézet (formátum) CustomEntry EntrySelectedBy elem](./entryselectedby-element-for-customentry-for-customcontrol-for-view-format.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
