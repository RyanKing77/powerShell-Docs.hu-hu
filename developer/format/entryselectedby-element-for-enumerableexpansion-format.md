---
title: (Formátum) EnumerableExpansion EntrySelectedBy eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 3af6aff8-4c2d-4f08-9bb1-e1f3ed3e583e
caps.latest.revision: 11
ms.openlocfilehash: 6a371bdbb85d07730c32931a4a79ee40856ce298
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56846521"
---
# <a name="entryselectedby-element-for-enumerableexpansion-format"></a>Az EnumerableExpansion EntrySelectedBy eleme (Formátum)

A .NET-típusokat, amelyek a definition vagy a feltétellel, hogy léteznie kell a definíció használandó határozza meg.

Konfigurációs elem (formátum) DefaultSettings elem (formátum) EnumerableExpansions elem (formátum) EnumerableExpansion elem (formátum) EntrySelectedBy eleme EnumerableExpansion (formátum)

## <a name="syntax"></a>Szintaxis

```xml
<EntrySelectedBy>
  <TypeName>Nameof.NetType</TypeName>
  <SelectionSetName>NameofSelectionSet</SelectionSetName>
  <SelectionCondition>...</SelectionCondition>
</EntrySelectedBy>
```

## <a name="attributes-and-elements"></a>Attribútumok és elemek

A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `EntrySelectedBy` elemet.

### <a name="attributes"></a>Attribútumok

Nincs.

### <a name="child-elements"></a>Gyermekelemek

|Elem|Leírás|
|-------------|-----------------|
|[A EnumerableExpansion (formátum) EntrySelectedBy SelectionCondition elem.](./selectioncondition-element-for-entryselectedby-for-enumerableexpansion-format.md)|Nem kötelező eleme.<br /><br /> Határozza meg azt a feltételt, amelyet a bontsa ki a gyűjtemény objektumokat, ez a definíció léteznie kell.|
|[A EnumerableExpansion (formátum) EntrySelectedBy SelectionSetName elem.](./selectionsetname-element-for-entryselectedby-for-enumerableexpansion-format.md)|Nem kötelező eleme.<br /><br /> Ez a definíció, hogyan vannak bontva a gyűjtemény objektumokat használó .NET-típusok egy halmazát határozza meg.|
|[EntrySelectedBy EnumerableExpansion (formátum) a TypeName elem.](./typename-element-for-entryselectedby-for-enumerableexpansion-format.md)|Nem kötelező eleme.<br /><br /> Ez a definíció, hogyan vannak bontva a gyűjtemény objektumokat használó .NET típust határozzon meg.|

### <a name="parent-elements"></a>Szülőelemek

|Elem|Leírás|
|-------------|-----------------|
|[EnumerableExpansion elem (formátum)](./enumerableexpansion-element-format.md)|Határozza meg, hogyan adott .NET gyűjtemény objektumok kibontott nézetben megjelenésekor.|

## <a name="remarks"></a>Megjegyzés

Meg kell adnia legalább egy típusa, kijelölés set vagy a definíció bejegyzést kiválasztási feltétel. Nincs nem használható gyermekelemek számának maximális korlátot.

Kiválasztási feltételek segítségével határozhatók meg egy feltételt, amely megléte esetén használható, például ha egy objektum rendelkezik-e egy adott tulajdonságra a definíció, vagy egy adott tulajdonság értékét, vagy a parancsfájl kiértékelése `true`. További információ a kiválasztási feltételek: [feltételek meghatározása az adatok megjelenítése](./defining-conditions-for-displaying-data.md).

## <a name="see-also"></a>Lásd még:

[Adatok megjelenítése feltételek meghatározása](./defining-conditions-for-displaying-data.md)

[EnumerableExpansion elem (formátum)](./enumerableexpansion-element-format.md)

[A EnumerableExpansion (formátum) EntrySelectedBy SelectionCondition elem.](./selectioncondition-element-for-entryselectedby-for-enumerableexpansion-format.md)

[A EnumerableExpansion (formátum) EntrySelectedBy SelectionSetName elem.](./selectionsetname-element-for-entryselectedby-for-enumerableexpansion-format.md)

[EntrySelectedBy EnumerableExpansion (formátum) a TypeName elem.](./typename-element-for-entryselectedby-for-enumerableexpansion-format.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
