---
title: A nézet (formátum) CustomControl ExpressionBinding CustomControlName eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: ea821e8b-4d65-4263-b7e4-6aeca9f534c2
caps.latest.revision: 9
ms.openlocfilehash: b44ced75bbaac7c0744f347bdc97f87365b8fe39
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62066617"
---
# <a name="customcontrolname-element-for-expressionbinding-for-customcontrol-for-view-format"></a>A Nézet CustomControl eleméhez tartozó ExpressionBinding CustomControlName eleme (Formátum)

Megadja egy közös vezérlőelem vagy a nézet nevét. Ehhez az elemhez használt egyéni vezérlő nézet definiálása.

Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem CustomControl elem CustomControl számára a nézet (formátum) CustomItem CustomEntries megtekintése (formátum) CustomEntry elemhez tartozó megtekintése (formátum) CustomEntries elemhez Elem a CustomEntry megtekintése (formátum) ExpressionBinding elem CustomItem (formátum) CustomControlName elemhez tartozó kifejezés kötésének CustomItem (formátum)

## <a name="syntax"></a>Szintaxis

```xml
<CustomControlName>NameofCustomControl</CustomControlName>
```

## <a name="attributes-and-elements"></a>Attribútumok és elemek

A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `CustomControlName` elemet.

### <a name="attributes"></a>Attribútumok

Nincs.

### <a name="child-elements"></a>Gyermekelemek

Nincs.

### <a name="parent-elements"></a>Szülőelemek

|Elem|Leírás|
|-------------|-----------------|
|[ExpressionBinding eleme CustomItem (formátum)](./expressionbinding-element-for-customitem-for-controls-for-configuration-format.md)|Határozza meg a vezérlő által megjelenített adatokat.|

## <a name="text-value"></a>A szöveges érték

Adja meg a vezérlő nevét.

## <a name="remarks"></a>Megjegyzés

Létrehozhat egy formázási fájl összes nézetek által használt Gyakori vezérlők és hozhat létre, amely egy adott nézet által használható vezérlőkre. Ezek a vezérlők nevét a következő elemek szerint vannak megadva.

- [A vezérlési konfiguráció (formátum) vezérlők Name elemet](./name-element-for-control-for-controls-for-configuration-format.md)

- [Vezérlő (formátum) nézet vezérlők Name elemet](./name-element-for-control-for-controls-for-view-format.md)

## <a name="see-also"></a>Lásd még:

[A vezérlési konfiguráció (formátum) vezérlők Name elemet](./name-element-for-control-for-controls-for-configuration-format.md)

[Vezérlő (formátum) nézet vezérlők Name elemet](./name-element-for-control-for-controls-for-view-format.md)

[ExpressionBinding eleme CustomItem (formátum)](./expressionbinding-element-for-customitem-for-controls-for-configuration-format.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
