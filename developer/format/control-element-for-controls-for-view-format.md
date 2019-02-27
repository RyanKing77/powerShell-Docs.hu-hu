---
title: Elem vezérlők megtekintése (formátum) vezérlőelemet |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 1fd53f55-698d-4df5-bb9a-fe28dc3193e1
caps.latest.revision: 11
ms.openlocfilehash: df568ccb36a2646b983622cdf95718dd5cac62c3
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56845219"
---
# <a name="control-element-for-controls-for-view--format"></a>A Nézet Vezérlők elemének vezérlőeleme (Formátum)

Határozza meg olyan vezérlő, amely a nézet és a neve, amellyel hivatkozni a vezérlő által használható.

Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézet elem (formátum) szabályozza elem (formátum) vezérlőelem elem vezérlők megtekintése (formátum)

## <a name="syntax"></a>Szintaxis

```xml
<Control>
  <Name>NameOfControl</Name>
  <CustomControl>...</CustomControl>
</Control>
```

## <a name="attributes-and-elements"></a>Attribútumok és elemek

A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `Control` elemet.

### <a name="attributes"></a>Attribútumok

Nincs.

### <a name="child-elements"></a>Gyermekelemek

|Elem|Leírás|
|-------------|-----------------|
|[Vezérlő (formátum) nézet Name elemet](./name-element-for-control-for-controls-for-view-format.md)|Szükséges eleme.<br /><br /> Megadja a vezérlő nevét.|
|[Vezérlő (formátum) nézet vezérlők CustomControl elem](./customcontrol-element-for-control-for-controls-for-view-format.md)|Szükséges eleme.<br /><br /> Ez a nézet által használt vezérlő határozza meg.|

### <a name="parent-elements"></a>Szülőelemek

|Elem|Leírás|
|-------------|-----------------|
|[Vezérlők elem (formátum)](./controls-element-for-view-format.md)|Határozza meg a nézet szabályozza, hogy egy adott nézet is lehet.|

## <a name="remarks"></a>Megjegyzés

Ez a vezérlő határozhatja meg a következő elemeket:

- [Nézet (formátum) vezérlők ExpressionBinding CustomControlName elem.](./customcontrolname-element-for-expressionbinding-for-controls-for-view-format.md)

- [A nézet (formátum) CustomControl ExpressionBinding CustomControlName elem.](./customcontrolname-element-for-expressionbinding-for-customcontrol-for-view-format.md)

- [A GroupBy (formátum) ExpressionBinding CustomControlName elem.](./customcontrolname-element-for-expressionbinding-for-groupby-format.md)

- [GroupBy (formátum) CustomControlName elem.](./customcontrolname-element-for-groupby-format.md)

## <a name="see-also"></a>Lásd még:

[Vezérlő (formátum) nézet vezérlők CustomControl elem](./customcontrol-element-for-control-for-controls-for-view-format.md)

[Nézet (formátum) vezérlők ExpressionBinding CustomControlName elem.](./customcontrolname-element-for-expressionbinding-for-controls-for-view-format.md)

[A nézet (formátum) CustomControl ExpressionBinding CustomControlName elem.](./customcontrolname-element-for-expressionbinding-for-customcontrol-for-view-format.md)

[A GroupBy (formátum) ExpressionBinding CustomControlName elem.](./customcontrolname-element-for-expressionbinding-for-groupby-format.md)

[A GroupBy (formátum) ExpressionBinding CustomControlName elem.](./customcontrolname-element-for-expressionbinding-for-groupby-format.md)

[Vezérlők elem (formátum)](./controls-element-for-view-format.md)

[Vezérlő (formátum) nézet vezérlők Name elemet](./name-element-for-control-for-controls-for-view-format.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
