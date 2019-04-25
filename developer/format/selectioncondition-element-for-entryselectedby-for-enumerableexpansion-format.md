---
title: EnumerableExpansion (formátum) a EntrySelectedBy SelectionCondition eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 8c012115-9241-4851-9015-841eb508faf3
caps.latest.revision: 10
ms.openlocfilehash: d6adf2fa62384d671fd6a07dd185a941daa44cec
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62064135"
---
# <a name="selectioncondition-element-for-entryselectedby-for-enumerableexpansion-format"></a>Az EnumerableExpansion elemhez tartozó EntrySelectedBy SelectionCondition eleme (Formátum)

Határozza meg azt a feltételt, amelyet a bontsa ki a gyűjtemény objektumokat, ez a definíció léteznie kell.

Konfigurációs elem (formátum) DefaultSettings elem (formátum) EnumerableExpansions elem (formátum) EnumerableExpansion elem (formátum) EntrySelectedBy elem esetében a EntrySelectedBy EnumerableExpansion (formátum) SelectionCondition elemhez EnumerableExpansion (formátum)

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
|[SelectionCondition EntrySelectedBy EnumerableExpansion (formátum) esetében a PropertyName elem.](./propertyname-element-for-selectioncondition-for-entryselectedby-for-enumerableexpansion-format.md)|Nem kötelező eleme.<br /><br /> Megadja a .NET-tulajdonság, amely elindítja a feltételt.|
|[SelectionCondition EntrySelectedBy EnumerableExpansion (formátum) esetében a scriptblock kulcsszót elem.](./scriptblock-element-for-selectioncondition-for-entryselectedby-for-enumerableexpansion-format.md)|Nem kötelező eleme.<br /><br /> Megadja a parancsprogramot, amely elindítja a feltétel.|
|[SelectionSetName Element for SelectionCondition for EntrySelectedBy for EnumerableExpansion (Format)](./selectionsetname-element-for-selectioncondition-for-entryselectedby-for-enumerableexpansion-format.md)|Nem kötelező eleme.<br /><br /> Megadja a .NET-típusok, amely elindítja a feltételt.|
|[SelectionCondition EntrySelectedBy EnumerableExpansion (formátum) esetében a TypeName elem.](./typename-element-for-selectioncondition-for-entryselectedby-for-enumerableexpansion-format.md)|Nem kötelező eleme.<br /><br /> A .NET típusát, amely elindítja a feltételt határozza meg.|

### <a name="parent-elements"></a>Szülőelemek

|Elem|Leírás|
|-------------|-----------------|
|[EntrySelectedBy eleme EnumerableExpansion (formátum)](./entryselectedby-element-for-enumerableexpansion-format.md)|Határozza meg, melyik gyűjtemény .NET-objektumokat a definíció szerint bontva.|

## <a name="remarks"></a>Megjegyzés

Minden egyes definíció rendelkeznie kell legalább egy típusnév, kijelölés set vagy meghatározott kiválasztási feltételnek.

Meghatározásakor kiválasztási feltétel, a következő követelményeknek kell teljesülnie:

- A kiválasztási feltételnek legalább egy tulajdonság nevét, vagy parancsprogram-blokkot kell megadnia, de nem adható meg egyszerre.

- A kiválasztási feltétel adhat meg minden olyan .NET-típusok száma vagy a kiválasztási állítja be, de nem adható meg egyszerre.

Kiválasztási feltételek használatával kapcsolatos további információkért lásd: [feltételek meghatározása Diplaying adatok](./defining-conditions-for-displaying-data.md).

Egy széles nézet egyéb összetevőivel kapcsolatos további információkért lásd: [széles nézet](./creating-a-wide-view.md).

## <a name="see-also"></a>Lásd még:

[Mikor jelenik meg adat feltételeinek meghatározása](./defining-conditions-for-displaying-data.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
