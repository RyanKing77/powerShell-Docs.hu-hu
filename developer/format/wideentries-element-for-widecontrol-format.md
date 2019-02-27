---
title: (Formátum) WideControl WideEntries eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 0c4bff45-0960-4b3a-95e7-47f2cee03ac5
caps.latest.revision: 12
ms.openlocfilehash: 083f3c8df8136858e32778ed231943ef983e47aa
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56844904"
---
# <a name="wideentries-element-for-widecontrol-format"></a>A WideControl WideEntries eleme (Formátum)

A széles nézet a definíciókat tartalmazza. A széles nézet meg kell adnia egy vagy több definíciót.

Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem WideControl elem (formátum) WideEntries elem (formátum)

## <a name="syntax"></a>Szintaxis

```xml
<WideEntries>
  <WideEntry>...</WideEntry>
</WideEntries>

```

## <a name="attributes-and-elements"></a>Attribútumok és elemek

A következő szakaszok ismertetik az attribútumokat, gyermekelemek és szülőelemét a `WideEntries` elemet. Meg kell adni legalább egy gyermekelemet.

### <a name="attributes"></a>Attribútumok

Nincs.

### <a name="child-elements"></a>Gyermekelemek

|Elem|Leírás|
|-------------|-----------------|
|[WideEntry elem (formátum)](./wideentry-element-for-widecontrol-format.md)|A széles nézet definíciójának biztosít.|

### <a name="parent-elements"></a>Szülőelemek

|Elem|Leírás|
|-------------|-----------------|
|[WideControl elem (formátum)](./widecontrol-element-format.md)|A wide (egyetlen érték) határozza meg a Nézet formátuma.|

## <a name="remarks"></a>Megjegyzés

A széles nézet olyan egyetlen tulajdonság értékét vagy az egyes objektumok parancsfájlérték megjelenítő lista formájában. Egy széles nézet az összetevőivel kapcsolatos további információkért lásd: [széles nézet összetevők](./creating-a-wide-view.md).

## <a name="example"></a>Példa

A következő példa bemutatja egy `WideEntries` elem, amely meghatározza egy `WideEntry` elemet. A `WideEntry` elem tartalmazza egyetlen `WideItem` elem, amely meghatározza, milyen tulajdonság, vagy parancsprogram érték jelenik meg a nézetben.

```xml
<WideControl>
  <WideEntries>
    <WideEntry>
      <WideItem>...</WideItem>
    <WideEntry>
  </WideEntries>
</WideControl>
```

Egy széles nézet egy teljes példa: [széles nézet (alapszintű)](./wide-view-basic.md).

## <a name="see-also"></a>Lásd még:

[Egy széles nézet létrehozása](./creating-a-wide-view.md)

[WideControl elem (formátum)](./widecontrol-element-format.md)

[WideEntry elem (formátum)](./wideentry-element-for-widecontrol-format.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
