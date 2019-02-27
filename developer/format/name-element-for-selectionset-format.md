---
title: Elem name (formátum) SelectionSet |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 914917f7-0efc-4d1f-88bd-de714bedd98f
caps.latest.revision: 15
ms.openlocfilehash: 29dbdbd335511e4ca2706a625541554825838f23
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56848327"
---
# <a name="name-element-for-selectionset-format"></a>A SelectionSet Név eleme (Formátum)

Megadja a mutató hivatkozás a kijelölés-készlet nevét.

Konfigurációs elem (formátum) SelectionSets elem (formátum) SelectionSet elem (formátum) nevet eleme SelectionSet (formátum)

## <a name="syntax"></a>Szintaxis

```xml
<Name>Name of selection set</Name>
```

## <a name="attributes-and-elements"></a>Attribútumok és elemek

A következő szakaszok ismertetik az attribútumokat, gyermekelemek és szülőelemét a `Name` elemet.

### <a name="attributes"></a>Attribútumok

Nincs.

### <a name="child-elements"></a>Gyermekelemek

Nincs.

### <a name="parent-elements"></a>Szülőelemek

|Elem|Leírás|
|-------------|-----------------|
|[SelectionSet elem (formátum)](./selectionset-element-format.md)|Meghatároz egy egységes .NET-objektumokat a készlet neve szerint lehet hivatkozni.|

## <a name="text-value"></a>Szöveges érték

Adja meg a nevét, a kijelölés set hivatkozni. Nincsenek nem korlátozza a feltárhatja, hogy mely karakterek használhatók.

## <a name="remarks"></a>Megjegyzés

Az itt megadott név használatban van a `SelectionSetName` elemet. A nézet definíciója szerint a nézet által használható kijelölés set (nézetek rendelkezhet több definíciókat), vagy egy kiválasztási feltétel megadásakor. Kijelölt csoportok kapcsolatos további információkért lásd: [meghatározása beállítja az objektumok](./defining-selection-sets.md).

## <a name="example"></a>Példa

Ez a példa bemutatja egy `SelectionSet` elem, amely négy .NET típusa határozza meg. A kijelölt csoport név "FileSystemTypes".

```xml
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

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
