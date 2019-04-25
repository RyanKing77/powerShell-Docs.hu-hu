---
title: CustomItem elemet a vezérlők (formátum) nézet CustomEntry |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 33cb5350-73ef-4b79-a879-0edf051869e4
caps.latest.revision: 7
ms.openlocfilehash: 174ba6a14819f823ec39f72e49a626e781221d8c
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62066380"
---
# <a name="customitem-element-for-customentry-for-controls-for-view-format"></a>A Nézet Vezérlők eleméhez tartozó CustomEntry CustomItem eleme (Formátum)

Határozza meg a vezérlő által megjelenített adatokat, és hogyan jelenik meg. Ez az elem szolgál a nézet által használható vezérlők meghatározásakor.

Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem vezérlők elem (formátum) vezérlőelem elem vezérlők, a nézet (formátum) CustomControl elem megtekintése (formátum) CustomEntries elemet a vezérlők a vezérlő A nézet (formátum) CustomEntry elem CustomEntries vezérlők, a vezérlők (formátum) nézet CustomEntry megtekintése (formátum) CustomItem elemhez tartozó CustomControl

## <a name="syntax"></a>Szintaxis

```xml
<CustomItem>
  <ExpressionBinding>...</ExpressionBinding>
  <NewLine/>
  <Text>TextToDisplay</Text>
  <Frame>...<Frame>
</CustomItem>
```

## <a name="attributes-and-elements"></a>Attribútumok és elemek

A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `CustomItem` elemet. További információkért lásd a megjegyzések.

### <a name="attributes"></a>Attribútumok

Nincs.

### <a name="child-elements"></a>Gyermekelemek

|Elem|Leírás|
|-------------|-----------------|
|[Nézet (formátum) vezérlők CustomItem ExpressionBinding elem.](./expressionbinding-element-for-customitem-for-controls-for-view-format.md)|Nem kötelező eleme.<br /><br /> Határozza meg a vezérlő által megjelenített adatokat.|
|[Keret eleme CustomItem vezérlők nézet (formátum)](./frame-element-for-customitem-for-controls-for-view-format.md)|Nem kötelező eleme.<br /><br /> Határozza meg, hogyan egy jelennek meg, például az adatok pótlása jobbra vagy balra.|
|[Új sor eleme CustomItem vezérlők nézet (formátum)](./newline-element-for-customitem-for-controls-for-view-format.md)|Nem kötelező eleme.<br /><br /> Egy üres sort ad hozzá a vezérlő megjelenését.|
|[A vezérlők (formátum) nézet CustomItem elem](./text-element-for-customitem-for-controls-for-view-format.md)|Nem kötelező eleme.<br /><br /> Szöveg, például zárójelek vagy zárójelben ad hozzá a vezérlő megjelenését.|

### <a name="parent-elements"></a>Szülőelemek

|Elem|Leírás|
|-------------|-----------------|
|[Nézet (formátum) vezérlők CustomEntries CustomEntry elem.](./customentry-element-for-customentries-for-controls-for-view-format.md)|A vezérlőelem egy definíciót tartalmaz.|

## <a name="remarks"></a>Megjegyzés

Az alárendelt elemeinek megadásakor a `CustomItem` elem, vegye figyelembe a következőket:

- A gyermekelemek hozzá kell adni a következő sorrendben: `ExpressionBinding`, `NewLine`, `Text`, és `Frame`.

- Nincs maximális megadható feladatütemezések száma korlátozva van.

- Az egyes feladatütemezési nem nincs maximális számának korlátja `ExpressionBinding` elemeket, amelyeket használhat.

## <a name="see-also"></a>Lásd még:

[Nézet (formátum) vezérlők CustomItem ExpressionBinding elem.](./expressionbinding-element-for-customitem-for-controls-for-view-format.md)

[Keret eleme CustomItem vezérlők nézet (formátum)](./frame-element-for-customitem-for-controls-for-view-format.md)

[Új sor eleme CustomItem vezérlők nézet (formátum)](./newline-element-for-customitem-for-controls-for-view-format.md)

[A vezérlők (formátum) nézet CustomItem elem](./text-element-for-customitem-for-controls-for-view-format.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
