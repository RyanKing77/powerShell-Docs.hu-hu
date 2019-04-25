---
title: Keretet elem számára CustomItem CustomControl a nézet (formátum) |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: e1a13100-41a4-4847-9f07-458c85783505
caps.latest.revision: 6
ms.openlocfilehash: 925ef86e61801f5a66f89dd25e0756f00dd35155
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62065580"
---
# <a name="frame-element-for-customitem-for-customcontrol-for-view-format"></a>A Nézet CustomControl eleméhez tartozó CustomItem Keret eleme (Formátum)

Határozza meg, hogyan egy jelennek meg, például az adatok pótlása jobbra vagy balra. Ehhez az elemhez használt egyéni vezérlő nézet definiálása.

Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézet elem (formátum) CustomControl elem (formátum) CustomEntries eleme CustomControl megtekintése (formátum) CustomEntry elem megtekintése (formátum) CustomItem elemhez tartozó CustomEntries számára CustomEntry CustomItem CustomControl nézet (formátum) esetében a CustomControlView (formátum) keret elemhez

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
|[FirstLineHanging elem](./firstlinehanging-element-for-frame-for-customcontrol-for-view-format.md)|Nem kötelező eleme.<br /><br /> Megadja a bal oldali adatok első sora úgy, hogy hány karakter.|
|[FirstLineIndent elem](./firstlineindent-element-for-frame-for-customcontrol-for-view-format.md)|Nem kötelező eleme.<br /><br /> Megadja az adatok első sorának jobb úgy, hogy hány karakter.|
|[LeftIndent elem](./leftindent-element-for-frame-for-customcontrol-for-view-format.md)|Nem kötelező eleme.<br /><br /> Itt adhatja meg az adatokat erről a bal oldali margó úgy, hogy hány karakter.|
|[RightIndent elem](./rightindent-element-for-frame-for-customcontrol-for-view-format.md)|Nem kötelező eleme.<br /><br /> Itt adhatja meg az adatokat erről a jobb oldali margó úgy, hogy hány karakter.|

### <a name="parent-elements"></a>Szülőelemek

|Elem|Leírás|
|-------------|-----------------|
|[A nézet (formátum) CustomEntry CustomItem elem](./customitem-element-for-customentry-for-customcontrol-for-view-format.md)|Határozza meg a vezérlő által megjelenített adatokat, és hogyan jelenik meg.|

## <a name="remarks"></a>Megjegyzés

Nem adható meg a [FirstLineHanging](./firstlinehanging-element-for-frame-for-customcontrol-for-view-format.md) és a [FirstLineIndent](./firstlineindent-element-for-frame-for-customcontrol-for-view-format.md) elemek ugyanazon `Frame` elemet.

## <a name="see-also"></a>Lásd még:

[FirstLineHanging elem](./firstlinehanging-element-for-frame-for-customcontrol-for-view-format.md)

[FirstLineIndent elem](./firstlineindent-element-for-frame-for-customcontrol-for-view-format.md)

[LeftIndent elem](./leftindent-element-for-frame-for-customcontrol-for-view-format.md)

[RightIndent elem](./rightindent-element-for-frame-for-customcontrol-for-view-format.md)

[A nézet (formátum) CustomEntry CustomItem elem](./customitem-element-for-customentry-for-customcontrol-for-view-format.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
