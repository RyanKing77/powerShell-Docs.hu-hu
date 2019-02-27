---
title: GroupBy elem (formátum) nézet |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 67a2b061-2a4a-4ad1-84f9-cdbefb64aaab
caps.latest.revision: 8
ms.openlocfilehash: abb8b91626128b3deaa2db24a9fd8b34a6563410
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56849279"
---
# <a name="groupby-element-for-view-format"></a>A Nézet GroupBy eleme (Formátum)

Határozza meg, hogyan jelenjen meg az objektumok egy új csoportot. Ez az elem szolgál egy táblázat, lista, szélesre vagy egyéni vezérlő nézetében meghatározásakor.

Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem GroupBy elem nézet (formátum)

## <a name="syntax"></a>Szintaxis

```xml
<GroupBy>
  <PropertyName>.NetTypeProperty</PropertyName>
  <ScriptBlock>ScriptToEvaluate</ScriptBlock>
  <Label>TextToDisplay</Label>
  <CustomControl>...</CustomControl>
  <CustomControlName>NameOfControl</CustomControlName>
</GroupBy>
```

## <a name="attributes-and-elements"></a>Attribútumok és elemek

A következő szakaszok ismertetik az attribútumokat, a gyermekelemek és a szülő elemeket.

### <a name="attributes"></a>Attribútumok

Nincs.

### <a name="child-elements"></a>Gyermekelemek

|Elem|Leírás|
|-------------|-----------------|
|[GroupBy (formátum) CustomControl elem.](./customcontrol-element-for-groupby-format.md)|Nem kötelező eleme.<br /><br /> Határozza meg az egyéni vezérlő, amely az új csoport megjelenítéséhez.|
|[GroupBy (formátum) CustomControlName elem.](./customcontrolname-element-for-groupby-format.md)|Nem kötelező eleme.<br /><br /> Megadja egy olyan vezérlőelem, amellyel megjelenjen az új csoport nevét.|
|[Címke elemet a GroupBy (formátum)](./label-element-for-groupby-format.md)|Nem kötelező eleme.<br /><br /> Meghatározza a felirat jelenik meg, ha egy új csoportot észlelt.|
|[A PropertyName elemet a GroupBy (formátum)](./propertyname-element-for-groupby-format.md)|Nem kötelező eleme.<br /><br /> Megadja a .NET-tulajdonság a elindul egy új csoportot, amikor annak értéke módosul.|
|[GroupBy (formátum) a scriptblock kulcsszót elem](./scriptblock-element-for-groupby-format.md)|Nem kötelező eleme.<br /><br /> Adja meg a parancsfájl, amely elindítja egy új csoportot, amikor annak értéke módosul.|

### <a name="parent-elements"></a>Szülőelemek

|Elem|Leírás|
|-------------|-----------------|
|[Nézet elem (formátum)](./view-element-format.md)|Legalább egy .NET-objektumokat megjelenítő nézet határozza meg.|

## <a name="remarks"></a>Megjegyzés

Határozza meg, hogyan jelenjen meg az objektumok egy új csoportot, amikor meg kell adnia a tulajdonságot vagy parancsfájlt, amely megkezdi az új csoport; azonban mindkettő megadására nincs lehetőség.

## <a name="see-also"></a>Lásd még:

[GroupBy (formátum) CustomControlName elem.](./customcontrolname-element-for-groupby-format.md)

[Címke elemet a GroupBy (formátum)](./label-element-for-groupby-format.md)

[A PropertyName elemet a GroupBy (formátum)](./propertyname-element-for-groupby-format.md)

[GroupBy (formátum) a scriptblock kulcsszót elem](./scriptblock-element-for-groupby-format.md)

[Nézet elem (formátum)](./view-element-format.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
