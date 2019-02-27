---
title: CustomEntries elemet a nézet (formátum) CustomControl |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: cb412831-94f7-4054-b19e-32c1b14c66dd
caps.latest.revision: 11
ms.openlocfilehash: 827baacd22ef258dd9b0c8a383a23fce7d975f7f
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56850798"
---
# <a name="customentries-element-for-customcontrol-for-view-format"></a>A Nézet CustomControl elemének CustomEntries eleme (Formátum)

Az egyéni vezérlő nézetében a definíciókat tartalmazza. Az egyéni vezérlő nézetében meg kell adnia egy vagy több definíciót.

Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem CustomControl elem (formátum) CustomEntries eleme CustomControl nézet (formátum)

## <a name="syntax"></a>Szintaxis

```xml
<CustomEntries>
  <CustomEntry>...</CustomEntry>
</CustomEntries>
```

## <a name="attributes-and-elements"></a>Attribútumok és elemek

A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `CustomControlEntries` elemet. Meg kell adnia egy vagy több gyermekelemet.

### <a name="attributes"></a>Attribútumok

Nincs.

### <a name="child-elements"></a>Gyermekelemek

|Elem|Leírás|
|-------------|-----------------|
|[A nézet (formátum) CustomEntries CustomEntry elem](./customentry-element-for-customentries-for-customcontrol-for-view-format.md)|Szükséges eleme.<br /><br /> Az egyéni vezérlő nézet definíciójának biztosít.|

### <a name="parent-elements"></a>Szülőelemek

|Elem|Leírás|
|-------------|-----------------|
|[CustomControl elem nézet (formátum)](./customcontrol-element-for-view-format.md)|Szükséges eleme.<br /><br /> A nézet egy egyéni vezérlő formátumát határozza meg.|

## <a name="remarks"></a>Megjegyzés

A legtöbb esetben egy vezérlőelem még csak egy definíciót, amely egy meghatározott `CustomEntry` elemet. Azonban lehetőség a több definíciókkal rendelkeznek, ha különböző .NET-objektumok megjelenítése ugyanazon vezérlő használata. Ezekben az esetekben definiálhat egy `CustomEntry` elem az egyes objektumok vagy objektumok közül.

## <a name="see-also"></a>Lásd még:

[CustomControl elem nézet (formátum)](./customcontrol-element-for-view-format.md)

[A nézet (formátum) CustomEntries CustomEntry elem](./customentry-element-for-customentries-for-customcontrol-for-view-format.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
