---
title: ListControl (formátum) a ListItem ItemSelectionCondition eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: d2668aea-37e9-4753-a4e9-7980ae5ec2eb
caps.latest.revision: 10
ms.openlocfilehash: 6bc0ccbcc5bd62429f63ed220da66dc66f44f7ca
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56850917"
---
# <a name="itemselectioncondition-element-for-listitem-for-listcontrol-format"></a>A ListControl elemhez tartozó ListItem ItemSelectionCondition eleme (Formátum)

Határozza meg azt a feltételt, amelyet a listaelem használandó léteznie kell.

Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézet elem (formátum) ListControl elem (formátum) ListEntries eleme ListEntries ListControl (formátum) ListItems elemek elemhez tartozó ListEntry ListEntry eleme ListControl (formátum) a ListItems elemek ListControl (formátum) ItemSelectionCondition elemhez tartozó ListItem ListControl (formátum) a ListControl (formátum) ListItem elemhez

## <a name="syntax"></a>Szintaxis

```xml
<ItemSelectionCondition>
  <PropertyName>.NetTypeProperty</PropertyName>
  <ScriptBlock>ScriptToEvaluate</ScriptBlock>
</ItemSelectionCondition>
```

## <a name="attributes-and-elements"></a>Attribútumok és elemek

A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `ItemSelectionCondition` elemet.

### <a name="attributes"></a>Attribútumok

Nincs.

### <a name="child-elements"></a>Gyermekelemek

|Elem|Leírás|
|-------------|-----------------|
|[ItemSelectionCondition ListControl (formátum) a PropertyName elem.](./propertyname-element-for-itemselectioncondition-for-listcontrol-format.md)|Nem kötelező eleme.<br /><br /> Megadja a .NET-tulajdonság, amely elindítja a feltételt.|
|[ItemSelectionCondition ListControl (formátum) a scriptblock kulcsszót elem.](./scriptblock-element-for-itemselectioncondition-for-listcontrol-format.md)|Nem kötelező eleme.<br /><br /> Megadja a parancsprogramot, amely elindítja a feltétel.|

### <a name="parent-elements"></a>Szülőelemek

|Elem|Leírás|
|-------------|-----------------|
|[A ListControl (formátum) ListItems elemek ListItem elem.](./listitem-element-for-listitems-for-listcontrol-format.md)|A tulajdonság, vagy a parancsfájl, amelynek értéke megjelenik a lista nézet sorában lévő határoz meg.|

## <a name="remarks"></a>Megjegyzés

Egy tulajdonság neve vagy az ehhez a feltételhez parancsfájlt is megadhat, de nem adható meg egyszerre.

## <a name="see-also"></a>Lásd még:

[A ListControl (formátum) ListItems elemek ListItem elem.](./listitem-element-for-listitems-for-listcontrol-format.md)

[ItemSelectionCondition ListControl (formátum) a PropertyName elem.](./propertyname-element-for-itemselectioncondition-for-listcontrol-format.md)

[ItemSelectionCondition ListControl (formátum) a scriptblock kulcsszót elem.](./scriptblock-element-for-itemselectioncondition-for-listcontrol-format.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
