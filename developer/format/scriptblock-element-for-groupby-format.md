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
ms.openlocfilehash: f2f6b9af7740b1231881294c2f32bf97b5a1568b
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62064509"
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

Windows PowerShell elindul egy új csoportot, minden alkalommal, amikor ez a szkript értékét módosítja.

Ha ez az elem meg van adva, nem adható meg a [PropertyName](http://msdn.microsoft.com/en-us/396dede0-039a-4a87-a5ef-3ecabb729676) elem elindítani egy új csoportot.

## <a name="see-also"></a>Lásd még:

[A PropertyName elemet a GroupBy (formátum)](./propertyname-element-for-groupby-format.md)

[GroupBy elem nézet (formátum)](./groupby-element-for-view-format.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
