---
title: GroupBy (formátum)-keret FirstLineHanging elem |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 1cdcf66e-96a5-47b5-9269-b4330bde29f2
caps.latest.revision: 6
ms.openlocfilehash: 08db1f2d89c3fe6c1e9a5a522de3071425042c3f
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62065832"
---
# <a name="firstlinehanging-element-for-frame-for-groupby-format"></a>A GroupBy elemhez tartozó Keret FirstLineHanging eleme (Formátum)

Megadja a bal oldali adatok első sora úgy, hogy hány karakter. Ez az elem szolgál, hogyan jelenjen meg az objektumok egy új csoportot meghatározásakor.

Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem GroupBy elem megtekintése (formátum) CustomControl elem a GroupBy (formátum) CustomEntry elemhez tartozó CustomControl GroupBy (formátum) CustomEntries elemhez GroupBy (formátum) CustomItem elem CustomEntry CustomItem GroupBy (formátum)-keret GroupBy (formátum) FirstLineHanging elemhez tartozó GroupBy (formátum) keret elemhez tartozó CustomControl

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
|[Keret eleme CustomItem a GroupBy (formátum)](./frame-element-for-customitem-for-groupby-format.md)|Határozza meg, hogyan egy jelennek meg, például az adatok pótlása jobbra vagy balra.|

## <a name="text-value"></a>A szöveges érték

Adja meg, hogy az adatok első sora shift kívánt karakterek száma.

## <a name="remarks"></a>Megjegyzés

Ha ez az elem meg van adva, nem adható meg a [FirstLineIndent](./firstlineindent-element-for-frame-for-groupby-format.md) elemet.

## <a name="see-also"></a>Lásd még:

[GroupBy (formátum)-keret FirstLineIndent elem](./firstlineindent-element-for-frame-for-groupby-format.md)

[Keret eleme CustomItem a GroupBy (formátum)](./frame-element-for-customitem-for-groupby-format.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
