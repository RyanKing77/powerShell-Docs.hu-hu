---
title: WideControl (formátum) a EntrySelectedBy SelectionCondition eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: b7a9f086-b1ca-4400-9be7-9ec1ec8880f3
caps.latest.revision: 11
ms.openlocfilehash: f20679e3392b99a049c075f24c7712262bab08e1
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62063991"
---
# <a name="selectioncondition-element-for-entryselectedby-for-widecontrol-format"></a>A WideControl elemhez tartozó EntrySelectedBy SelectionCondition eleme (Formátum)

Határozza meg azt a feltételt, amelyet a definíció használandó léteznie kell. Kiválasztási feltételek széles bejegyzés-definíció adható meg száma nincs korlátozva van.

Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézet elem (formátum) WideControl elem (formátum) WideEntries elem (formátum) WideEntry elem (formátum) EntrySelectedBy elem WideEntry (formátum) SelectionCondition elem számára EntrySelectedBy a WideEntry (formátum)

## <a name="syntax"></a>Szintaxis

```xml
<SelectionCondition>
  <TypeName>Nameof.NetType</TypeName>
  <SelectionSetName>NameofSelectionSet</SelectionSetName>
  <PropertyName>.NetTypeProperty</PropertyName>
  <ScriptBlock>ScriptToEvaluate</ScriptBlock>
</SelectionCondition>
```

## <a name="attributes-and-elements"></a>Attribútumok és elemek

A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `SelectionCondition` elemet. Meg kell adnia egy `PropertyName` vagy `ScriptBlock` elemet. A `SelectionSetName` és `TypeName` elemek egyike sem kötelező. Mindkét elem kiválaszthat egyet.

### <a name="attributes"></a>Attribútumok

Nincs.

### <a name="child-elements"></a>Gyermekelemek

|Elem|Leírás|
|-------------|-----------------|
|[SelectionCondition EntrySelectedBy WideEntry (formátum) esetében a PropertyName elem.](./propertyname-element-for-selectioncondition-for-entryselectedby-for-wideentry-format.md)|Nem kötelező eleme.<br /><br /> Megadja a .NET-tulajdonság, amely elindítja a feltételt.|
|[SelectionCondition EntrySelectedBy WideEntry (formátum) esetében a scriptblock kulcsszót elem.](./scriptblock-element-for-selectioncondition-for-entryselectedby-for-widecontrol-format.md)|Nem kötelező eleme.<br /><br /> Adja meg a parancsprogram-blokkot, amely elindítja a feltételt.|
|[A EntrySelectedBy WideEntry (formátum) a SelectionCondition SelectionSetName eleme](./selectionsetname-element-for-selectioncondition-for-entryselectedby-for-wideentry-format.md)|Nem kötelező eleme.<br /><br /> Megadja a .NET-típusok, amely elindítja a feltételt.|
|[SelectionCondition EntrySelectedBy WideEntry (formátum) esetében a TypeName elem.](./typename-element-for-selectioncondition-for-entryselectedby-for-widecontrol-format.md)|Nem kötelező eleme.<br /><br /> A .NET típusát, amely elindítja a feltételt határozza meg.|

### <a name="parent-elements"></a>Szülőelemek

|Elem|Leírás|
|-------------|-----------------|
|[EntrySelectedBy eleme WideEntry (formátum)](./entryselectedby-element-for-wideentry-format.md)|A .NET-típusokat, amelyek a széles körű bejegyzés vagy a feltétellel, hogy léteznie kell használni a bejegyzés határozza meg.|

## <a name="remarks"></a>Megjegyzés

Minden széles bejegyzés rendelkeznie kell legalább egy típusnév, kijelölés set vagy meghatározott kiválasztási feltételnek.

Meghatározásakor kiválasztási feltétel, a következő követelményeknek kell teljesülnie:

- A kiválasztási feltételnek legalább egy tulajdonság nevét, vagy parancsprogram-blokkot kell megadnia, de nem adható meg egyszerre.

- A kiválasztási feltétel adhat meg minden olyan .NET-típusok száma vagy a kiválasztási állítja be, de nem adható meg egyszerre.

Kiválasztási feltételek használatával kapcsolatos további információkért lásd: [definiáló vonatkozó feltételeket, amikor egy nézet bejegyzés vagy az elem](./defining-conditions-for-displaying-data.md).

Egy széles nézet egyéb összetevőivel kapcsolatos további információkért lásd: [széles nézet létrehozásával](./creating-a-wide-view.md).

## <a name="see-also"></a>Lásd még:

[Egy széles nézet létrehozása](./creating-a-wide-view.md)

[Mikor jelenik meg adat feltételeinek meghatározása](./defining-conditions-for-displaying-data.md)

[EntrySelectedBy eleme WideEntry (formátum)](./entryselectedby-element-for-wideentry-format.md)

[SelectionCondition EntrySelectedBy WideEntry (formátum) esetében a PropertyName elem.](./propertyname-element-for-selectioncondition-for-entryselectedby-for-wideentry-format.md)

[SelectionCondition EntrySelectedBy WideEntry (formátum) esetében a scriptblock kulcsszót elem.](./scriptblock-element-for-selectioncondition-for-entryselectedby-for-widecontrol-format.md)

[A EntrySelectedBy WideEntry (formátum) a SelectionCondition SelectionSetName eleme](./selectionsetname-element-for-selectioncondition-for-entryselectedby-for-wideentry-format.md)

[SelectionCondition EntrySelectedBy WideEntry (formátum) esetében a TypeName elem.](./typename-element-for-selectioncondition-for-entryselectedby-for-widecontrol-format.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
