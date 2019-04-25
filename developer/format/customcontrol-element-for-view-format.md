---
title: Nézet (formátum) CustomControl elem |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 2edac16c-0b30-4985-ac84-0821aa9a9f6d
caps.latest.revision: 12
ms.openlocfilehash: bd0f7ca4de8dede97d1553cd62884ea45876e0c7
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62066668"
---
# <a name="customcontrol-element-for-view-format"></a>A Nézet CustomControl eleme (Formátum)

A nézet egy egyéni vezérlő formátumát határozza meg.

Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem CustomControl elem (formátum)

## <a name="syntax"></a>Szintaxis

```xml
<CustomControl>
  <CustomEntries>...</CustomEntries>
</CustomControl>
```

## <a name="attributes-and-elements"></a>Attribútumok és elemek

A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `CustomControl` elemet. Több gyermekelemet kell megadnia.

### <a name="attributes"></a>Attribútumok

Nincs.

### <a name="child-elements"></a>Gyermekelemek

|Elem|Leírás|
|-------------|-----------------|
|[A nézet (formátum) CustomControl CustomEntries elem](./customentries-element-for-customcontrol-for-view-format.md)|Szükséges eleme.<br /><br /> Az egyéni vezérlő nézetében a definíciókat tartalmazza.|

### <a name="parent-elements"></a>Szülőelemek

|Elem|Leírás|
|-------------|-----------------|
|[Nézet elem (formátum)](./view-element-format.md)|Meghatározza egy nézetet, amely legalább egy .NET-objektumokká megjelenítésére szolgál.|

## <a name="remarks"></a>Megjegyzés

A legtöbb esetben csak egyetlen definíciót minden vezérlő nézet megadása kötelező, de lehetséges víc definic adja meg, ha ugyanabban a nézetben különböző .NET-objektumok megjelenítéséhez használandó. Ezekben az esetekben adja meg egy külön meghatározása az egyes objektumok vagy objektumok közül.

## <a name="see-also"></a>Lásd még:

[A nézet (formátum) CustomControl CustomEntries elem](./customentries-element-for-customcontrol-for-view-format.md)

[Nézet elem (formátum)](./view-element-format.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
