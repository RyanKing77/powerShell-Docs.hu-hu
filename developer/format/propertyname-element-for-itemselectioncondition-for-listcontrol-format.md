---
title: ItemSelectionCondition ListControl (formátum) a PropertyName eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: d5e707ae-3c84-4ceb-ba31-56b3ffde6d6c
caps.latest.revision: 7
ms.openlocfilehash: b15e26e18126f69eee7c3a857f9a461d4bdf5848
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56846486"
---
# <a name="propertyname-element-for-itemselectioncondition-for-listcontrol-format"></a>A ListControl elemhez tartozó ItemSelectionCondition PropertyName eleme (Formátum)

Megadja a .NET-tulajdonság, amely elindítja a feltételt. Ha ez a tulajdonság jelen-e, vagy ha való kiértékelése által `true`, a feltétel nem teljesül, és a nézetet használja. Ez az elem akkor használatos, ha a lista nézet definiálása.

Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézet elem (formátum) ListControl elem (formátum) ListEntries elem (formátum) ListEntry elem a ListControl (formátum) ListItem ListEntry a ListControl (formátum) ListItems elemek elemhez ListControl (formátum) ItemSelectionCondition elemhez tartozó ListItem ListControls PropertyName elemhez tartozó ItemSelectionCondition ListControl (formátum) a ListItems elemek elem.

## <a name="syntax"></a>Szintaxis

```xml
<PropertyName>.NetTypeProperty</PropertyName>
```

## <a name="attributes-and-elements"></a>Attribútumok és elemek

A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a szülő elemei a `PropertyName` elemet.

### <a name="attributes"></a>Attribútumok

Nincs.

### <a name="child-elements"></a>Gyermekelemek

Nincs.

### <a name="parent-elements"></a>Szülőelemek

|Elem|Leírás|
|-------------|-----------------|
|[A ListControl (formátum) ListItem ItemSelectionCondition eleme](./itemselectioncondition-element-for-listitem-for-listcontrol-format.md)||

## <a name="text-value"></a>Szöveges érték

Adja meg, amelynek értéke megjelenik a tulajdonság nevét.

## <a name="remarks"></a>Megjegyzés

Ha ez az elem használata esetén nem adható meg a [ScriptBlock](./scriptblock-element-for-itemselectioncondition-for-listcontrol-format.md) elemet a kiválasztási feltétel meghatározásakor.

## <a name="see-also"></a>Lásd még:

[ItemSelectionCondition ListIControl (formátum) a scriptblock kulcsszót elem.](./scriptblock-element-for-itemselectioncondition-for-listcontrol-format.md)

[A ListControl (formátum) ListItem ItemSelectionCondition eleme](./itemselectioncondition-element-for-listitem-for-listcontrol-format.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
