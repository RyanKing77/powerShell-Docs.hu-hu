---
title: A ListControl (formátum) ListEntry ListItems elemek eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: d2c1da6d-acc7-4fe8-9e7d-6dcddc2787cd
caps.latest.revision: 9
ms.openlocfilehash: c25f18489d9c7abd8889758499dbbacd6ee29304
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56848621"
---
# <a name="listitems-element-for-listentry-for-listcontrol-format"></a>A ListControl elemhez tartozó ListEntry ListItems eleme (Formátum)

A tulajdonságok és a parancsfájlok, melynek értékei jelennek meg a lista nézet sorainak határoz meg.

Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem ListControl elem (formátum) ListEntries elem a lista vezérlőelem (formátum) ListEntry elem ListControl (formátum) ListItems elemek elemhez tartozó ListControl (formátum)

## <a name="syntax"></a>Szintaxis

```xml
<ListItems>
  <ListItem>...</ListItem>
</ListItems>
```

## <a name="attributes-and-elements"></a>Attribútumok és elemek

A következő szakaszok ismertetik az attribútumokat, gyermekelemek és szülőelemét a `ListItems` elemet. Nincs nem adható meg az alárendelt elemek száma nincs korlátozva. Az alárendelt összetevők sorrendje határozza meg, hogy a listanézetet jelennek meg a értékei sorrendben.

### <a name="attributes"></a>Attribútumok

Nincs.

### <a name="child-elements"></a>Gyermekelemek

|Elem|Leírás|
|-------------|-----------------|
|[Listaelem eleme ListControl (formátum)](./listitem-element-for-listitems-for-listcontrol-format.md)|Szükséges eleme.<br /><br /> A tulajdonság vagy parancsfájl, amelynek értéke megjelenik a lista nézet szerint határozza meg.|

### <a name="parent-elements"></a>Szülőelemek

|Elem|Leírás|
|-------------|-----------------|
|[ListEntry eleme ListControl (formátum)](./listentry-element-for-listcontrol-format.md)|A lista nézet definíciójának biztosít.|

## <a name="remarks"></a>Megjegyzés

Az ilyen típusú nézet kapcsolatos további információkért lásd: [lista nézet létrehozásával](./creating-a-list-view.md).

## <a name="example"></a>Példa

Ez a példa bemutatja az XML-elemeket, amelyek meghatározzák a listanézet három sort.

```xml
<ListEntry>
    <ListItems>
      <ListItem>
        <Label>Property1: </Label>
        <PropertyName>.NetTypeProperty1</PropertyName>
      </ListItem>
      <ListItem>
        <PropertyName>.NetTypeProperty2</PropertyName>
      </ListItem>
      <ListItem>
        <ScriptBlock>$_.ProcessName + ":" $_.Id</ScriptBlock>
      </ListItem>
  </ListEntry>
```

## <a name="see-also"></a>Lásd még:

[ListEntry eleme ListControl (formátum)](./listentry-element-for-listcontrol-format.md)

[Listaelem eleme ListControl (formátum)](./listitem-element-for-listitems-for-listcontrol-format.md)

[Lista nézet létrehozása](./creating-a-list-view.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
