---
title: Listaelem ListControl (formátum) a scriptblock kulcsszót eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 74e30938-00ef-46fd-84e5-f0a83706a50e
caps.latest.revision: 11
ms.openlocfilehash: 76b600256af3f957f7fe0578f9fef810262aa5d5
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62064577"
---
# <a name="scriptblock-element-for-listitem-for-listcontrol-format"></a>A ListControl elemhez tartozó ListItem ScriptBlock eleme (Formátum)

Megadja a parancsprogramot, amelynek értéke megjelenik a sorban.

Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézet elem (formátum) ListControl elem (formátum) ListEntries eleme ListEntries ListControl (formátum) ListItems elemek elemhez tartozó ListEntry ListEntry eleme ListControl (formátum) a ListItems elemek ListControl (formátum) ScriptBlock elemhez tartozó ListItem ListControl (formátum) a ListControl (formátum) ListItem elemhez

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
|[Listaelem elem (formátum)](./listitem-element-for-listitems-for-listcontrol-format.md)|A tulajdonság, vagy a parancsfájl, amelynek értéke megjelenik a lista nézet sorában lévő határoz meg.|

## <a name="text-value"></a>A szöveges érték

Adja meg a parancsfájl, amelynek értéke megjelenik a sorban.

## <a name="remarks"></a>Megjegyzés

Ha ez az elem meg van adva, nem adható meg a [PropertyName](./propertyname-element-for-listitem-for-listcontrol-format.md) elemet.

Lista nézetben parancsfájlok megadásával kapcsolatos további információkért lásd: [listanézet](./creating-a-list-view.md).

## <a name="example"></a>Példa

Az alábbi példa bemutatja, hogyan adja meg a tulajdonságot, amelynek értéke megjelenik.

```xml
<ListItem>
  <ScriptBlock>$_.ProcessName + ":" $_.Id</ScriptBlock>
</ListItem>

```

## <a name="see-also"></a>Lásd még:

[Listaelem ListControl (formátum) a PropertyName elem.](./propertyname-element-for-listitem-for-listcontrol-format.md)

[Lista nézet létrehozása](./creating-a-list-view.md)

[A ListControl (formátum) ListItems elemek ListItem elem.](./listitem-element-for-listitems-for-listcontrol-format.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
