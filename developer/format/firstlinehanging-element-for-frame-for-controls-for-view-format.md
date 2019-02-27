---
title: Keret (formátum) nézet vezérlők FirstLineHanging elem |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 53694f08-57f7-4185-b443-1636a0918afc
caps.latest.revision: 8
ms.openlocfilehash: 387340cd9b0aae2ad0419b187d96ab4fee183d5a
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56848712"
---
# <a name="firstlinehanging-element-for-frame-for-controls-for-view-format"></a>A Nézet Vezérlők eleméhez tartozó Keret FirstLineHanging eleme (Formátum)

Megadja a bal oldali adatok első sora úgy, hogy hány karakter. Ez az elem szolgál a nézet által használható vezérlők meghatározásakor.

Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem vezérlők elem (formátum) vezérlőelem elem vezérlők, a nézet (formátum) CustomControl elem megtekintése (formátum) CustomEntries elemet a vezérlők a vezérlő A nézet (formátum) CustomEntry elem CustomEntries vezérlők, a vezérlők, a nézet (formátum) keret elem CustomItem vezérlők megtekintése (formátum) FirstLineHanging eleméhez tartozó CustomEntry megtekintése (formátum) CustomItem elemhez tartozó CustomControl Keret vezérlők nézet (formátum)

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
|[Keret eleme CustomItem vezérlők nézet (formátum)](./frame-element-for-customitem-for-controls-for-view-format.md)|Határozza meg, hogyan egy jelennek meg, például az adatok pótlása jobbra vagy balra.|

## <a name="text-value"></a>Szöveges érték

Adja meg, hogy az adatok első sora shift kívánt karakterek száma.

## <a name="remarks"></a>Megjegyzés

Ha ez az elem meg van adva, nem adható meg a [FirstLineIndent](./firstlineindent-element-for-frame-for-controls-for-view-format.md) elemet.

## <a name="see-also"></a>Lásd még:

[Keret (formátum) nézet vezérlők FirstLineIndent elem.](./firstlineindent-element-for-frame-for-controls-for-view-format.md)

[Keret eleme CustomItem vezérlők nézet (formátum)](./frame-element-for-customitem-for-controls-for-view-format.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
