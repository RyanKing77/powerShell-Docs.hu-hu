---
title: Nevezze el elem vezérlő vezérlők (formátum) nézet |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 26437467-d578-4e8d-8cdd-17dfe644957a
caps.latest.revision: 7
ms.openlocfilehash: 7e24aa60f7abae5768707d2527826c452b709002
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62065101"
---
# <a name="name-element-for-control-for-controls-for-view-format"></a>A Nézet Vezérlők eleméhez tartozó Vezérlő Név eleme (Formátum)

Megadja a vezérlő nevét.

Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézet elem (formátum) szabályozza elem (formátum) vezérlőelem elem vezérlők megtekintése (formátum) elemhez vezérlő nézet (formátum)

## <a name="syntax"></a>Szintaxis

```xml
<Name>ControlName</Name>
```

## <a name="attributes-and-elements"></a>Attribútumok és elemek

A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `Name` elemet.

### <a name="attributes"></a>Attribútumok

Nincs.

### <a name="child-elements"></a>Gyermekelemek

Nincs.

### <a name="parent-elements"></a>Szülőelemek

|Elem|Leírás|
|-------------|-----------------|
|[Vezérlő elemet a vezérlők megjelenítéséhez (formátum)](./control-element-for-controls-for-view-format.md)|Határozza meg olyan vezérlő, amely a nézet és a neve, amellyel hivatkozni a vezérlő által használható.|

## <a name="text-value"></a>A szöveges érték

Adja meg a nevét, amely a vezérlőelem hivatkozni.

## <a name="remarks"></a>Megjegyzés

Az itt megadott név a vezérlő hivatkozni a következő elemeket is használható.

- Egy táblázat, lista, szélesre vagy egyéni vezérlő nézetében létrehozásakor, a vezérlő határozhatja meg a következő elemet: [GroupBy elem nézet (formátum)](./groupby-element-for-view-format.md)

- Egy másik vezérlő létrehozása, amely a nézet által használható, ha ez a vezérlő is megadható a következő elemet: [Nézet (formátum) vezérlők CustomItem ExpressionBinding elem.](./expressionbinding-element-for-customitem-for-controls-for-view-format.md)

## <a name="see-also"></a>Lásd még:

[GroupBy elem nézet (formátum)](./groupby-element-for-view-format.md)

[Nézet (formátum) vezérlők CustomItem ExpressionBinding elem.](./expressionbinding-element-for-customitem-for-controls-for-view-format.md)

[Vezérlő elemet a vezérlők megjelenítéséhez (formátum)](./control-element-for-controls-for-view-format.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
