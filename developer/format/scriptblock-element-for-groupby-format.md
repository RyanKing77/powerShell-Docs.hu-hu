---
title: GroupBy (formátum) a scriptblock kulcsszót elem |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 30183927-6f0e-4717-b6f5-f07a6e134cfb
caps.latest.revision: 6
ms.openlocfilehash: 37a297228eb33ff75daf94a12635d42b52c6cc9f
ms.sourcegitcommit: 58fb23c854f5a8b40ad1f952d3323aeeccac7a24
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/07/2019
ms.locfileid: "65229319"
---
# <a name="scriptblock-element-for-groupby-format"></a>A GroupBy ScriptBlock eleme (Formátum)

Adja meg a parancsfájl, amely elindítja egy új csoportot, amikor annak értéke módosul.

Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem GroupBy elem a scriptblock kulcsszót elem megtekintése (formátum) a GroupBy (formátum)

## <a name="syntax"></a>Szintaxis

```xml
<ScriptBlock>ScriptToEvaluate</ScriptBlock>
```

## <a name="attributes-and-elements"></a>Attribútumok és elemek

A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `ScriptBlock` elemet.

### <a name="attributes"></a>Attribútumok

Nincs.

### <a name="child-elements"></a>Gyermekelemek

Nincs.

### <a name="parent-elements"></a>Szülőelemek

|Elem|Leírás|
|-------------|-----------------|
|[GroupBy elem nézet (formátum)](./groupby-element-for-view-format.md)|Határozza meg, hogyan jelenjen meg a .NET-objektumokká csoportja.|

## <a name="text-value"></a>A szöveges érték

Adja meg a parancsfájl, amely ki lesz értékelve.

## <a name="remarks"></a>Megjegyzés

PowerShell elindul egy új csoportot, minden alkalommal, amikor ez a szkript értékét módosítja.

Ha ez az elem meg van adva, nem adható meg a [PropertyName](propertyname-element-for-groupby-format.md) elem elindítani egy új csoportot.

## <a name="see-also"></a>Lásd még:

[A PropertyName elemet a GroupBy (formátum)](propertyname-element-for-groupby-format.md)

[GroupBy elem nézet (formátum)](groupby-element-for-view-format.md)

[A fájl formázása PowerShell írása](writing-a-powershell-formatting-file.md)
