---
title: WideItem WideControl (formátum) a scriptblock kulcsszót eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: e00e8f36-76f2-49a0-9b02-3a2a7fceb2dd
caps.latest.revision: 8
ms.openlocfilehash: 6534e9dbfbe0dedf60dadd6467cff9ad9b447ba4
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62064203"
---
# <a name="scriptblock-element-for-wideitem-for-widecontrol-format"></a>A WideControl WideControl elemének ScriptBlock eleme (Formátum)

Megadja a parancsprogramot, amelynek az értéke az széles nézetben jelenik meg.

Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem WideControl elem (formátum) WideEntries elem (formátum) WideEntry elem (formátum) WideItem elem (formátum) ScriptBlock eleme WideItem (formátum)

## <a name="syntax"></a>Szintaxis

```xml
<ScriptBlock>ScriptToExecute</ScriptBlock>
```

## <a name="attributes-and-elements"></a>Attribútumok és elemek

A következő szakaszok ismertetik az attribútumokat, gyermekelemek és szülőelemét a `ScriptBlock` elemet.

### <a name="attributes"></a>Attribútumok

Nincs.

### <a name="child-elements"></a>Gyermekelemek

Nincs.

### <a name="parent-elements"></a>Szülőelemek

|Elem|Leírás|
|-------------|-----------------|
|[WideItem elem (formátum)](./wideitem-element-for-widecontrol-format.md)|Meghatározza a tulajdonság, vagy parancsprogram blokkot, amelynek az értéke az széles nézetben jelenik meg.|

## <a name="text-value"></a>A szöveges érték

Adja meg a parancsfájl, amelynek értéke megjelenik.

## <a name="remarks"></a>Megjegyzés

Egy széles nézet az összetevőivel kapcsolatos további információkért lásd: [széles nézet létrehozásával](./creating-a-wide-view.md).

## <a name="example"></a>Példa

Ez a példa bemutatja egy `WideItem` elem, amely meghatározza egy parancsfájlt, amelynek értéke megjelenik a nézetben.

```xml
<WideItem>
  <ScriptBlock>ScriptToExecute</ScriptBlock>
</WideItem>
```

## <a name="see-also"></a>Lásd még:

[WideItem elem (formátum)](./wideitem-element-for-widecontrol-format.md)

[Egy széles nézet létrehozása](./creating-a-wide-view.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
