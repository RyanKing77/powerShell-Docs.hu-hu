---
title: (Formátum) WideControl WideItem eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 17352fc4-ba83-4f04-86bc-f591765d85a8
caps.latest.revision: 18
ms.openlocfilehash: fa9eda3ea1028c27dbfb3eb04747af3b817c1a81
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56851449"
---
# <a name="wideitem-element-for-widecontrol-format"></a>A WideControl WideItem eleme (Formátum)

Határozza meg, tulajdonság vagy parancsfájl, amelynek értéke megjelenik.

Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem WideControl elem (formátum) WideEntries elem (formátum) WideEntry elem (formátum) WideItem elem (formátum)

## <a name="syntax"></a>Szintaxis

```xml
<WideItem>
  <PropertyName>.NetTypeProperty</PropertyName>
  <ScriptBlock>ScriptToExecute</ScriptBlock>
  <FormatString>FormatPattern</FormatString>
</WideItem>
```

## <a name="attributes-and-elements"></a>Attribútumok és elemek

A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `WideItem` elemet. A `FormatString` elem nem kötelező. Azonban meg kell adnia egy `PropertyName` vagy `ScriptBlock` elem, de nem adható meg egyszerre.

### <a name="attributes"></a>Attribútumok

Nincs.

### <a name="child-elements"></a>Gyermekelemek

|Elem|Leírás|
|-------------|-----------------|
|[WideItem WideControl (formátum) a FormatString elem.](./formatstring-element-for-wideitem-for-widecontrol-format.md)|Nem kötelező eleme.<br /><br /> Meghatározza formátumú mintát, amely meghatározza, hogy a tulajdonság vagy parancsfájl érték hogyan jelenjen meg a nézetben.|
|[A PropertyName eleme WideItem (formátum)](./propertyname-element-for-wideitem-for-widecontrol-format.md)|Itt adhatja meg a tulajdonság az objektum, amelynek az értéke az széles nézetben jelenik meg.|
|[ScriptBlock eleme WideItem (formátum)](./scriptblock-element-for-wideitem-for-widecontrol-format.md)|Megadja a parancsprogramot, amelynek az értéke az széles nézetben jelenik meg.|

### <a name="parent-elements"></a>Szülőelemek

|Elem|Leírás|
|-------------|-----------------|
|[WideEntry elem (formátum)](./wideentry-element-for-widecontrol-format.md)|A széles nézet definíciójának biztosít.|

## <a name="remarks"></a>Megjegyzés

Egy széles nézet az összetevőivel kapcsolatos további információkért lásd: [széles nézet](./creating-a-wide-view.md).

## <a name="example"></a>Példa

A következő példa bemutatja egy `WideEntry` elem, amely meghatározza egy `WideItem` elemet. A `WideItem` elem definiálja a tulajdonságot, vagy a parancsfájl, amelynek értéke megjelenik a nézetben.

```xml
<WideEntry>
  <WideItem>
    <PropertyName>ProcessName</PropertyName>
  </WideItem>
</WideEntry>
```

Egy széles nézet egy teljes példa: [széles nézet (alapszintű)](./wide-view-basic.md).

## <a name="see-also"></a>Lásd még:

[WideItem WideControl (formátum) a FormatString elem.](./formatstring-element-for-wideitem-for-widecontrol-format.md)

[A PropertyName eleme WideItem (formátum)](./propertyname-element-for-wideitem-for-widecontrol-format.md)

[ScriptBlock eleme WideItem (formátum)](./scriptblock-element-for-wideitem-for-widecontrol-format.md)

[WideEntry elem (formátum)](./wideentry-element-for-widecontrol-format.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
