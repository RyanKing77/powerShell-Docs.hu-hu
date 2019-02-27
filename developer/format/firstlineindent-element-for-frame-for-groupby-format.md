---
title: GroupBy (formátum)-keret FirstLineIndent elem |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 33be3b9e-53c8-433f-8c11-c65b0d46744c
caps.latest.revision: 6
ms.openlocfilehash: 9ba6fc1b9924a4b0d5b56ee15290a2293217403c
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56848600"
---
# <a name="firstlineindent-element-for-frame-for-groupby-format"></a>A GroupBy elemhez tartozó Keret FirstLineIndent eleme (Formátum)

Megadja az adatok első sorának jobb úgy, hogy hány karakter. Ez az elem szolgál, hogyan jelenjen meg az objektumok egy új csoportot meghatározásakor.

Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem GroupBy elem megtekintése (formátum) CustomControl elem a GroupBy (formátum) CustomEntry elemhez tartozó CustomControl GroupBy (formátum) CustomEntries elemhez GroupBy (formátum) CustomItem elem CustomEntry CustomItem GroupBy (formátum)-keret GroupBy (formátum) FirstLineIndent elemhez tartozó GroupBy (formátum) keret elemhez tartozó CustomControl

## <a name="syntax"></a>Szintaxis

```xml
<FirstLineIndent>NumberOfCharactersToShift</FirstLineIndent>
```

## <a name="attributes-and-elements"></a>Attribútumok és elemek

A következő szakaszok ismertetik az attribútumokat, gyermekelemek és szülőelemét a `FirstLineIndent` elemet.

### <a name="attributes"></a>Attribútumok

Nincs.

### <a name="child-elements"></a>Gyermekelemek

Nincs.

### <a name="parent-elements"></a>Szülőelemek

|Elem|Leírás|
|-------------|-----------------|
|[Keret eleme CustomItem a GroupBy (formátum)](./frame-element-for-customitem-for-groupby-format.md)|Határozza meg, hogyan egy jelennek meg, például az adatok pótlása jobbra vagy balra.|

## <a name="text-value"></a>Szöveges érték

Adja meg, hogy az adatok első sora shift kívánt karakterek száma.

## <a name="remarks"></a>Megjegyzés

Ha ez az elem meg van adva, nem adható meg a [FirstLineHanging](./firstlinehanging-element-for-frame-for-groupby-format.md) elemet.

## <a name="see-also"></a>Lásd még:

[GroupBy (formátum)-keret FirstLineHanging elem](./firstlinehanging-element-for-frame-for-groupby-format.md)

[Keret eleme CustomItem a GroupBy (formátum)](./frame-element-for-customitem-for-groupby-format.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
