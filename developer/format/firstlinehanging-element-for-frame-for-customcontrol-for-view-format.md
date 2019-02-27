---
title: Nézet (formátum) CustomControl-keret FirstLineHanging elem |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: c6ac3d86-0529-4b93-9bc7-ee94fcef9618
caps.latest.revision: 8
ms.openlocfilehash: ae4ad8ae3e6cb5d1174dc001b30aa84dd182a606
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56849776"
---
# <a name="firstlinehanging-element-for-frame-for-customcontrol-for-view-format"></a>A Nézet CustomControl eleméhez tartozó Keret FirstLineHanging eleme (Formátum)

Megadja a bal oldali adatok első sora úgy, hogy hány karakter. Ehhez az elemhez használt egyéni vezérlő nézet definiálása.

Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézet elem (formátum) CustomControl elem (formátum) CustomEntries eleme CustomControl megtekintése (formátum) CustomEntry elem megtekintése (formátum) CustomItem elemhez tartozó CustomEntries számára A CustomControl CustomControl nézet (formátum)-keret megtekintése (formátum) FirstLineHanging elemhez tartozó CustomItem CutomControlView (formátum) keret elemhez CustomEntry

## <a name="syntax"></a>Szintaxis

```xml
<FirstLineHanging>NumberOfCharactersToShift</FirstLineHanging>
```

## <a name="attributes-and-elements"></a>Attribútumok és elemek

A következő szakaszok ismertetik az attribútumokat, gyermekelemek és szülőelemét a `FirstLineHanging` elemet.

### <a name="attributes"></a>Attribútumok

Nincs.

### <a name="child-elements"></a>Gyermekelemek

Nincs.

### <a name="parent-elements"></a>Szülőelemek

|Elem|Leírás|
|-------------|-----------------|
|[A nézet (formátum) CustomControl CustomItem keret elem.](./frame-element-for-customitem-for-customcontrol-for-view-format.md)|Határozza meg, hogyan egy jelennek meg, például az adatok pótlása jobbra vagy balra.|

## <a name="text-value"></a>Szöveges érték

Adja meg, hogy az adatok első sora shift kívánt karakterek száma.

## <a name="remarks"></a>Megjegyzés

Ha ez az elem meg van adva, nem adható meg a [FirstLineIndent](./firstlineindent-element-for-frame-for-customcontrol-for-view-format.md) elemet.

## <a name="see-also"></a>Lásd még:

[A nézet (formátum) CustomControl keret FirstLineIndent eleme](./firstlineindent-element-for-frame-for-customcontrol-for-view-format.md)

[A nézet (formátum) CustomControl CustomItem keret elem.](./frame-element-for-customitem-for-customcontrol-for-view-format.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
