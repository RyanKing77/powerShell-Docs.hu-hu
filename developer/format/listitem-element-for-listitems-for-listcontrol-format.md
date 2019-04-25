---
title: ListControl (formátum) a ListItems elemek ListItem eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 0f96f4f5-8bd5-43ed-95e7-a7358115999a
caps.latest.revision: 11
ms.openlocfilehash: 1e0a1b2d20853650328b8cfd1513a08f7e167cd6
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62065767"
---
# <a name="listitem-element-for-listitems-for-listcontrol-format"></a>A ListControl elemhez tartozó ListItems ListItem eleme (Formátum)

A tulajdonság, vagy a parancsfájl, amelynek értéke megjelenik a lista nézet sorában lévő határoz meg.

Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem ListControl elem (formátum) ListEntries elem ListControl (formátum) ListEntry elem ListControl (formátum) ListItems elemek elemhez tartozó ListControl (formátum) Listaelem ListControl elemhez (formátum)

## <a name="syntax"></a>Szintaxis

```xml
<ListItem>
  <PropertyName>PropertyToDisplay</PropertyName>
  <ScriptBlock>ScriptToExecute</ScriptBlock>
  <Label>LabelToDisplay</Label>
  <FormatString>FormatPattern</FormatString>
  <ItemSelectionCondition>...</ItemSelectionCondition>
</ListItem>
```

## <a name="attributes-and-elements"></a>Attribútumok és elemek

A következő szakaszok ismertetik az attribútumokat, gyermekelemek és szülőelemét a `ListItem` elemet. Csak egy tulajdonságot vagy parancsfájl adható meg.

### <a name="attributes"></a>Attribútumok

Egyik sem

### <a name="child-elements"></a>Gyermekelemek

|Elem|Leírás|
|-------------|-----------------|
|[Listaelem ListControl (formátum) a FormatString elem.](./formatstring-element-for-listitem-for-listcontrol-format.md)|Nem kötelező eleme.<br /><br /> Megadja egy formázó karakterlánc, amely meghatározza, hogy a tulajdonság vagy parancsfájl érték hogyan jelenjen meg.|
|[A ListControl (formátum) ListItem ItemSelectionCondition eleme](./itemselectioncondition-element-for-listitem-for-listcontrol-format.md)|Nem kötelező eleme.<br /><br /> Határozza meg azt a feltételt, amelyet a listaelem használandó léteznie kell.|
|[Listaelem ListControl (formátum) a címke elem.](./label-element-for-listitem-for-listcontrol-format.md)|Választható elem<br /><br /> Adja meg a címke bal oldalán a tulajdonság, vagy parancsprogram érték sorában megjelenik.|
|[Listaelem ListControl (formátum) a PropertyName elem.](./propertyname-element-for-listitem-for-listcontrol-format.md)|Nem kötelező eleme.<br /><br /> Adja meg azt a .NET tulajdonságot, amelynek értéke megjelenik a sorban.|
|[Listaelem ListControl (formátum) a scriptblock kulcsszót elem.](./scriptblock-element-for-listitem-for-listcontrol-format.md)|Nem kötelező eleme.<br /><br /> Megadja a parancsprogramot, amelynek értéke megjelenik a sorban.|

### <a name="parent-elements"></a>Szülőelemek

|Elem|Leírás|
|-------------|-----------------|
|[ListItems elemek elem a lista vezérlőelem (formátum)](./listitems-element-for-listentry-for-listcontrol-format.md)|Meghatározza a tulajdonságok és a parancsfájlok, melynek értékei jelennek meg a listanézetben.|

## <a name="remarks"></a>Megjegyzés

Megjelenítheti az összetevőivel kapcsolatos további információk: [lista nézet létrehozásával](./creating-a-list-view.md).

## <a name="example"></a>Példa

Ez a példa bemutatja az XML-elemeket, amelyek meghatározzák a listanézet három sort. Az első két sort a .NET-tulajdonság értéket jeleníti meg, és az utolsó sort a szkript által létrehozott értéket jeleníti meg.

```xml
<ListEntry>
    <ListItems>
      <ListItem>
        <Label>Property1: </Label>
        <PropertyName>DotNetProperty1</PropertyName>
      </ListItem>
      <ListItem>
        <PropertyName>DotNetProperty2</PropertyName>
      </ListItem>
      <ListItem>
        <ScriptBlock>$_.ProcessName + ":" $_.Id</ScriptBlock>
      </ListItem>
    </ListItems>
</ListEntry>

```

## <a name="see-also"></a>Lásd még:

[ListItems elemek elem (formátum)](./listitems-element-for-listentry-for-listcontrol-format.md)

[FormatString eleme ListItem (formátum)](./formatstring-element-for-listitem-for-listcontrol-format.md)

[Címke eleme ListItem (formátum)](./label-element-for-listitem-for-listcontrol-format.md)

[A PropertyName eleme ListItem (formátum)](./propertyname-element-for-listitem-for-listcontrol-format.md)

[ScriptBlock eleme ListItem (formátum)](./scriptblock-element-for-listitem-for-listcontrol-format.md)

[Lista nézet létrehozása](./creating-a-list-view.md)

[Egy Windows PowerShell formázás és a fájl típusai](./writing-a-powershell-formatting-file.md)
