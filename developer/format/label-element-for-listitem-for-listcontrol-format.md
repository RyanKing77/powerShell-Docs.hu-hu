---
title: Címke elem a ListItem ListControl (formátum) a |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: c693ff46-d1ad-4dc7-93ac-41ff2fc6c103
caps.latest.revision: 9
ms.openlocfilehash: c1293d5a1f942704ac01388c66bd9009fd340e82
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62065427"
---
# <a name="label-element-for-listitem-for-listcontrol-format"></a>A ListControl elemhez tartozó ListItem Címke eleme (Formátum)

Adja meg a címke bal oldalán a tulajdonság, vagy parancsprogram érték sorában megjelenik.

Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem ListControl elem (formátum) ListEntries elem ListControl (formátum) ListEntry elemhez tartozó ListControl (formátum) ListItems elemek a ListEntry ListControl elem (a ListItems elemek ListControl (formátum) címke elemének ListItem ListControl (formátum) esetében a formátum) ListItem elem.

## <a name="syntax"></a>Szintaxis

```xml
<Label>Label for displayed value</Label>
```

## <a name="attributes-and-elements"></a>Attribútumok és elemek

A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `Label` elemet.

### <a name="attributes"></a>Attribútumok

Nincs.

### <a name="child-elements"></a>Gyermekelemek

Nincs.

### <a name="parent-elements"></a>Szülőelemek

|Elem|Leírás|
|-------------|-----------------|
|[A ListControl (formátum) ListItems elemek ListItem elem.](./listitem-element-for-listitems-for-listcontrol-format.md)|A tulajdonság, vagy a parancsfájl, amelynek értéke megjelenik a lista nézet sorában lévő határoz meg.|

## <a name="text-value"></a>A szöveges érték

Adja meg a címke a bal oldalon, a tulajdonság, vagy parancsprogram érték adatai jelennek meg.

## <a name="remarks"></a>Megjegyzés

Ha nincs megadva címke, a tulajdonság, vagy a parancsfájl neve jelenik meg. A listanézetben címkékkel kapcsolatos további információkért lásd: [lista nézet létrehozásával](./creating-a-list-view.md).

## <a name="example"></a>Példa

Az alábbi példa bemutatja, hogyan címke hozzáadása egy sort.

```xml
<ListItem>
  <Label>Property1: </Label>
  <PropertyName>DotNetProperty1</PropertyName>
</ListItem>

```

## <a name="see-also"></a>Lásd még:

[Lista nézet létrehozása](./creating-a-list-view.md)

[Listaelem elem (formátum)](./listitem-element-for-listitems-for-listcontrol-format.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
