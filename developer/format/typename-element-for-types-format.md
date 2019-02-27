---
title: TypeName elem esetében (formátum) |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 0595b99e-b438-4240-b47b-555cf0316f33
caps.latest.revision: 15
ms.openlocfilehash: 4f463ac6b70a00f628c5b93b112c5fa510ff3bfb
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56845114"
---
# <a name="typename-element-for-types-format"></a>A Típusok TypeName eleme (Formátum)

Megadja a .NET-típus egy objektum, amely a kijelölt csoporthoz tartozik.

Konfigurációs elem (formátum) SelectionSets elem (formátum) SelectionSet elem (formátum) típusú elem (formátum) TypeName elem típusú (formátum)

## <a name="syntax"></a>Szintaxis

```xml
<TypeName>Nameof.NetType</Name>
```

## <a name="attributes-and-elements"></a>Attribútumok és elemek

A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `TypeName` elemet. Legalább egy `TypeName` elemének szerepelnie kell a kijelölés beállítása.

### <a name="attributes"></a>Attribútumok

Nincs.

### <a name="child-elements"></a>Gyermekelemek

Nincs.

### <a name="parent-elements"></a>Szülőelemek

|Elem|Leírás|
|-------------|-----------------|
|[Típusok elem (formátum)](./types-element-for-selectionset-format.md)|Meghatározza a .NET-objektumok, amelyek a kijelölés beállítva.|

## <a name="text-value"></a>Szöveges érték

Adja meg a teljes nevet, a .NET-típus.

## <a name="remarks"></a>Megjegyzés

Kijelölt csoportok is használhatja, ha egyetlen nevet, például az öröklődés kapcsolódó objektumok közül a hivatkozni kívánt kapcsolódó objektumok közül. A nézetek meghatározásakor a neve helyett az egyes nézetek összes objektumához ajánlati beállítása a kijelölt objektumok készlete is megadhat.

A formázási fájl a nézetek meghatározásakor általános kijelölt csoportok neve szerint vannak megadva. Ezekben az esetekben a `SelectionSetName` gyermekeleme a `ViewSelectedBy` a nézet elem megadja. Azonban a nézetek különböző bejegyzés is megadhatók azok kijelölés csak adott tételre a nézetet. Kijelölt csoportok kapcsolatos további információkért lásd: [meghatározása beállítja az objektumok](./defining-selection-sets.md).

## <a name="example"></a>Példa

A következő példa bemutatja egy `SelectionSet` elem, amely négy .NET típusa határozza meg.

```
<SelectionSets>
  <SelectionSet>
    <Name>FileSystemTypes</Name>
    <Types>
     <TypeName>System.IO.DirectoryInfo</TypeName>
     <TypeName>System.IO.FileInfo</TypeName>
     <TypeName>Deserialized.System.IO.DirectoryInfo</TypeName>
     <TypeName>Deserialized.System.IO.FileInfo</TypeName>
    </Types>
  </SelectionSet>
</SelectionSets>
```

## <a name="see-also"></a>Lásd még:

[Kijelölt csoportok meghatározása](./defining-selection-sets.md)

[SelectionSet elem (formátum)](./selectionset-element-format.md)

[SelectionSets elem (formátum)](./selectionsets-element-format.md)

[Típusok elem (formátum)](./types-element-for-selectionset-format.md)

[Egy Windows PowDefining részhalmazához ObjecterShell formázás fájl írása](./writing-a-powershell-formatting-file.md)
