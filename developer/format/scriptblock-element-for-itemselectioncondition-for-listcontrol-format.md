---
title: ItemSelectionCondition ListControl (formátum) a scriptblock kulcsszót eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: c929a6df-d050-416a-9de0-e913dd5a035c
caps.latest.revision: 8
ms.openlocfilehash: a0768a9c1ac66cd9dcf1848c4b031ccbc722b4c2
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62064407"
---
# <a name="scriptblock-element-for-itemselectioncondition-for-listcontrol-format"></a>A ListControl elemhez tartozó ItemSelectionCondition ScriptBlock eleme (Formátum)

Megadja a parancsprogramot, amely elindítja a feltétel. Ha ez a parancsfájl kiértékelése `true`, a feltétel nem teljesül, és a listaelem szolgál. Ez az elem akkor használatos, ha a lista nézet definiálása.

Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézet elem (formátum) ListControl elem (formátum) ListEntries eleme ListEntries ListControl (formátum) ListItems elemek elemhez tartozó ListEntry ListEntry eleme ListControl (formátum) ListControl (formátum) ListItem elem a lista ListItems elemek szabályozása (formátum) ItemSelectionCondition eleme ListItem ListControl (formátum) ScriptBlock elemhez tartozó ItemSelectionCondition ListControl (formátum)

## <a name="syntax"></a>Szintaxis

```xml
<ScriptBlock>ScriptToEvaluate</ScriptBlock>
```

## <a name="attributes-and-elements"></a>Attribútumok és elemek

A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a szülő elemei a `ScriptBlock` elemet.

### <a name="attributes"></a>Attribútumok

Nincs.

### <a name="child-elements"></a>Gyermekelemek

Nincs.

### <a name="parent-elements"></a>Szülőelemek

|Elem|Leírás|
|-------------|-----------------|
|[A ListControl (formátum) ListItem ItemSelectionCondition eleme](./itemselectioncondition-element-for-listitem-for-listcontrol-format.md)|Határozza meg azt a feltételt, amelyet a listaelem használandó léteznie kell.|

## <a name="text-value"></a>A szöveges érték

Adja meg a parancsfájl, amely ki lesz értékelve.

## <a name="remarks"></a>Megjegyzés

Ha ez az elem használata esetén nem adható meg a `PropertyName` elemet a kiválasztási feltétel meghatározásakor.

## <a name="see-also"></a>Lásd még:

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
