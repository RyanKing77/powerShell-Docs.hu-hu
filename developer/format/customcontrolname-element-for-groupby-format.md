---
title: GroupBy (formátum) CustomControlName eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 473d9b56-521b-479a-8010-67fe9f040063
caps.latest.revision: 8
ms.openlocfilehash: 3a386eff95044eae573c255a451c5c8b8f16714d
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62066540"
---
# <a name="customcontrolname-element-for-groupby-format"></a>A GroupBy CustomControlName eleme (Formátum)

Megadja az egyéni vezérlőt, amellyel megjelenjen az új csoport nevét. Ez az elem szolgál egy táblázat, lista, szélesre vagy egyéni vezérlő nézetében meghatározásakor.

Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem GroupBy elem megtekintése (formátum) CustomControlName eleméhez GroupBy (formátum)

## <a name="syntax"></a>Szintaxis

```xml
<CustomControlName>ControlName</CustomControlName>
```

## <a name="attributes-and-elements"></a>Attribútumok és elemek

A következő szakaszok ismertetik az attribútumokat, a gyermekelemek és a szülő elemei a `CustomControlName` elemet.

### <a name="attributes"></a>Attribútumok

Nincs.

### <a name="child-elements"></a>Gyermekelemek

Nincs.

### <a name="parent-elements"></a>Szülőelemek

|Elem|Leírás|
|-------------|-----------------|
|[GroupBy elem nézet (formátum)](./groupby-element-for-view-format.md)|Határozza meg, hogyan jeleníti meg a Windows PowerShell-objektumok egy új csoportot.|

## <a name="text-value"></a>A szöveges érték

Adja meg az egyéni vezérlő, amellyel új csoport megjelenítendő nevét.

## <a name="remarks"></a>Megjegyzés

A formázási fájl összes nézetek által használt Gyakori vezérlők hozhat létre, és hozhat létre, amely egy adott nézet által használható vezérlőkre. A következő elemeket adja meg az egyéni vezérlők nevét:

- [A vezérlési konfiguráció (formátum) vezérlők Name elemet](./name-element-for-control-for-controls-for-configuration-format.md)

- [Vezérlő (formátum) nézet vezérlők Name elemet](./name-element-for-control-for-controls-for-view-format.md)

## <a name="see-also"></a>Lásd még:

[GroupBy elem nézet (formátum)](./groupby-element-for-view-format.md)

[A vezérlési konfiguráció (formátum) vezérlők Name elemet](./name-element-for-control-for-controls-for-configuration-format.md)

[Vezérlő (formátum) nézet vezérlők Name elemet](./name-element-for-control-for-controls-for-view-format.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
