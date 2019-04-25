---
title: Keretet elem számára CustomItem vezérlők (formátum) nézet |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: a5729091-78a9-4bc1-abac-210bc20c6dbe
caps.latest.revision: 7
ms.openlocfilehash: f93dc20a9c5f87c14605578062b1e60f5a3d25cf
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62065716"
---
# <a name="frame-element-for-customitem-for-controls-for-view-format"></a>A Nézet Vezérlők eleméhez tartozó CustomItem Keret eleme (Formátum)

Határozza meg, hogyan egy jelennek meg, például az adatok pótlása jobbra vagy balra. Ez az elem szolgál a nézet által használható vezérlők meghatározásakor.

Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem vezérlők elem (formátum) vezérlőelem elem vezérlők, a nézet (formátum) CustomControl elem megtekintése (formátum) CustomEntries elemet a vezérlők a vezérlő A nézet (formátum) CustomEntry elem CustomEntries vezérlők, a vezérlők, a vezérlők (formátum) nézet CustomItem megtekintése (formátum) keret elemhez CustomEntry megtekintése (formátum) CustomItem elemhez tartozó CustomControl

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
|[Keret (formátum) nézet vezérlők FirstLineHanging elem](./firstlinehanging-element-for-frame-for-controls-for-view-format.md)|Nem kötelező eleme.<br /><br /> Itt adhatja meg az első sor a bal oldali úgy, hogy hány karakter.|
|[Keret (formátum) nézet vezérlők FirstLineIndent elem](./firstlineindent-element-for-frame-for-controls-for-view-format.md)|Nem kötelező eleme.<br /><br /> Itt adhatja meg az első sor jobb úgy, hogy hány karakter.|
|[Keret (formátum) nézet vezérlők LeftIndent elem](./leftindent-element-for-frame-for-controls-for-view-format.md)|Nem kötelező eleme.<br /><br /> Itt adhatja meg az adatokat erről a bal oldali margó úgy, hogy hány karakter.|
|[Keret (formátum) nézet vezérlők RightIndent elem](./rightindent-element-for-frame-for-controls-for-view-format.md)|Nem kötelező eleme.<br /><br /> Itt adhatja meg az adatokat erről a jobb oldali margó úgy, hogy hány karakter.|

### <a name="parent-elements"></a>Szülőelemek

|Elem|Leírás|
|-------------|-----------------|
|[Nézet (formátum) vezérlők CustomEntry CustomItem elem.](./customitem-element-for-customentry-for-controls-for-view-format.md)|Határozza meg a vezérlő által megjelenített adatokat, és hogyan jelenik meg.|

## <a name="remarks"></a>Megjegyzés

Nem adható meg a [FirstLineHanging](./firstlinehanging-element-for-frame-for-controls-for-view-format.md) és a [FirstLineIndent](./firstlineindent-element-for-frame-for-controls-for-view-format.md) elemek ugyanazon `Frame` elemet.

## <a name="see-also"></a>Lásd még:

[Keret (formátum) nézet vezérlők FirstLineHanging elem](./firstlinehanging-element-for-frame-for-controls-for-view-format.md)

[Keret (formátum) nézet vezérlők FirstLineIndent elem](./firstlineindent-element-for-frame-for-controls-for-view-format.md)

[Keret (formátum) nézet vezérlők LeftIndent elem](./leftindent-element-for-frame-for-controls-for-view-format.md)

[Keret (formátum) nézet vezérlők RightIndent elem](./rightindent-element-for-frame-for-controls-for-view-format.md)

[Nézet (formátum) vezérlők CustomEntry CustomItem elem.](./customitem-element-for-customentry-for-controls-for-view-format.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
