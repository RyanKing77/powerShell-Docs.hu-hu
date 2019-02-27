---
title: Elem keretet CustomItem számára a GroupBy (formátum) |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: ab2a5379-299d-4c97-86a2-b639ea890fae
caps.latest.revision: 6
ms.openlocfilehash: 7f9066c0fe0954fadff9dc8f0c35a62c6710f516
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56846003"
---
# <a name="frame-element-for-customitem-for-groupby-format"></a>A GroupBy elemhez tartozó CustomItem Keret eleme (Formátum)

Határozza meg, hogyan egy jelennek meg, például az adatok pótlása jobbra vagy balra. Ez az elem szolgál, hogyan jelenjen meg az objektumok egy új csoportot meghatározásakor.

Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem GroupBy elem megtekintése (formátum) CustomControl elem a GroupBy (formátum) CustomEntry elemhez tartozó CustomControl GroupBy (formátum) CustomEntries elemhez GroupBy (formátum) CustomItem elem CustomEntry CustomItem GroupBy (formátum) esetében a GroupBy (formátum) keret elemhez tartozó CustomControl

## <a name="syntax"></a>Szintaxis

```xml
<Frame>
  <LeftIndent>NumberOfCharactersToShift</LeftIndent>
  <RightIndent>NumberOfCharactersToShift</RightIndent>
  <FirstLineHanging>NumberOfCharactersToShift</FirstLineHanging>
  <FirstLineIndent>NumberOfCharactersToShift</FirstLineIndent>
  <CustomItem>...</CustomItem>
</Frame>
```

## <a name="attributes-and-elements"></a>Attribútumok és elemek

A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `Frame` elemet.

### <a name="attributes"></a>Attribútumok

Nincs.

### <a name="child-elements"></a>Gyermekelemek

|Elem|Leírás|
|-------------|-----------------|
|`CustomItem Element`|Kötelező elem|
|[GroupBy (formátum)-keret FirstLineHanging elem](./firstlinehanging-element-for-frame-for-groupby-format.md)|Nem kötelező eleme.<br /><br /> Megadja a bal oldali adatok első sora úgy, hogy hány karakter.|
|[GroupBy (formátum)-keret FirstLineIndent elem](./firstlineindent-element-for-frame-for-groupby-format.md)|Nem kötelező eleme.<br /><br /> Megadja az adatok első sorának jobb úgy, hogy hány karakter.|
|[GroupBy (formátum)-keret LeftIndent elem](./leftindent-element-for-frame-for-groupby-format.md)|Nem kötelező eleme.<br /><br /> Itt adhatja meg az adatokat erről a bal oldali margó úgy, hogy hány karakter.|
|[GroupBy (formátum)-keret RightIndent elem](./rightindent-element-for-frame-for-groupby-format.md)RightIndent elem|Nem kötelező eleme.<br /><br /> Itt adhatja meg az adatokat erről a jobb oldali margó úgy, hogy hány karakter.|

### <a name="parent-elements"></a>Szülőelemek

|Elem|Leírás|
|-------------|-----------------|
|[A GroupBy (formátum) CustomEntry CustomItem elem.](./customitem-element-for-customentry-for-groupby-format.md)|Határozza meg a vezérlő által megjelenített adatokat, és hogyan jelenik meg.|

## <a name="remarks"></a>Megjegyzés

Nem adható meg a [FirstLineHanging](./firstlinehanging-element-for-frame-for-groupby-format.md) és a [FirstLineIndent](./firstlineindent-element-for-frame-for-groupby-format.md) elemek ugyanazon `Frame` elemet.

## <a name="see-also"></a>Lásd még:

[GroupBy (formátum)-keret FirstLineHanging elem](./firstlinehanging-element-for-frame-for-groupby-format.md)

[GroupBy (formátum)-keret FirstLineIndent elem](./firstlineindent-element-for-frame-for-groupby-format.md)

[GroupBy (formátum)-keret LeftIndent elem](./leftindent-element-for-frame-for-groupby-format.md)

[GroupBy (formátum)-keret RightIndent elem](./rightindent-element-for-frame-for-groupby-format.md)

[A GroupBy (formátum) CustomEntry CustomItem elem.](./customitem-element-for-customentry-for-groupby-format.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
