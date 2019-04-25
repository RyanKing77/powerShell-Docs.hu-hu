---
title: Címke elem a GroupBy (formátum) |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 3351d237-e8c2-4ec5-9500-4eceadb407c2
caps.latest.revision: 11
ms.openlocfilehash: e7158711c60d13c745bbdfab9b1b9fc7d98b34e2
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62065410"
---
# <a name="label-element-for-groupby-format"></a>A GroupBy Címke eleme (Formátum)

Meghatározza a felirat jelenik meg, ha egy új csoportot észlelt.

Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem GroupBy elem megtekintése (formátum) címke elem a GroupBy (formátum)

## <a name="syntax"></a>Szintaxis

```xml
<Label>DisplayedLabel</Label>
```

## <a name="attributes-and-elements"></a>Attribútumok és elemek

A következő szakaszok ismertetik az attribútumokat, gyermekelemek és szülőelemét a `Label` elemet.

### <a name="attributes"></a>Attribútumok

Nincs.

### <a name="child-elements"></a>Gyermekelemek

Nincs.

### <a name="parent-elements"></a>Szülőelemek

|Elem|Leírás|
|-------------|-----------------|
|[GroupBy elem nézet (formátum)](./groupby-element-for-view-format.md)|Határozza meg, hogyan jelenjen meg az objektumok egy új csoportot.|

## <a name="text-value"></a>A szöveges érték

Adja meg a szöveg, amelyet minden alkalommal, amikor Windows PowerShell találkozik egy új tulajdonság vagy parancsfájl érték jelenik meg.

## <a name="remarks"></a>Megjegyzés

Ez az elem által meghatározott a szöveg mellett a Windows PowerShell az új értéket, amely elindítja a csoportot, és hozzáad egy üres sort, előtt és után a csoport jeleníti meg.

## <a name="example"></a>Példa

Az alábbi példa bemutatja egy új csoportot a címkét. A megjelenített címke ehhez hasonlóan néz ki ez: `Service Type: NewValueofProperty`

```xml
<GroupBy>
  <Label>Service Type</Label>
  <PropertyName>ServiceType</PropertyName>
</GroupBy>

```

A teljes formázási fájl tartalmazza ezt az elemet egy példa: [széles nézet (GroupBy)](./wide-view-groupby.md).

## <a name="see-also"></a>Lásd még:

[GroupBy elem nézet (formátum)](./groupby-element-for-view-format.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
