---
title: SelectionSet elem (formátum) |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 848e7acd-d578-4fd1-a575-c0c3b9b5e68a
caps.latest.revision: 17
ms.openlocfilehash: c809aa6c3a40d16cfd2fd99065a846d265ec0f61
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62076310"
---
# <a name="selectionset-element-format"></a>SelectionSet elem (Formátum)

Meghatároz egy .NET-objektumokat a készlet neve szerint lehet hivatkozni.

Konfigurációs elem (formátum) SelectionSets elem (formátum) SelectionSet elem (formátum)

## <a name="syntax"></a>Szintaxis

```xml
<SelectionSet>
  <Name>SelectionSetName</Name>
  <Types>...</Types>
</SelectionSet>
```

## <a name="attributes-and-elements"></a>Attribútumok és elemek

A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `SelectionSet` elemet. Minden kijelölés set névvel kell rendelkeznie, és meg kell határoznia azt a .NET-objektumokat a készlet.

### <a name="attributes"></a>Attribútumok

Nincs.

### <a name="child-elements"></a>Gyermekelemek

|Elem|Leírás|
|-------------|-----------------|
|[Name elemet a SelectionSet (formátum)](./name-element-for-selectionset-format.md)|Szükséges eleme.<br /><br /> Megadja a mutató hivatkozás a kijelölés-készlet nevét.|
|[Típusok elem (formátum)](./types-element-for-selectionset-format.md)|Szükséges eleme.<br /><br /> Meghatározza a .NET-objektumok, amelyek a kijelölés beállítva.|

### <a name="parent-elements"></a>Szülőelemek

|Elem|Leírás|
|-------------|-----------------|
|[SelectionSets elem formátuma](./selectionsets-element-format.md)|Határozza meg a gyakori eljárások egyikét a formázási fájl összes nézetek által használható .NET-objektumokat.|

## <a name="remarks"></a>Megjegyzés

Kijelölt csoportok is használhatja, ha egyetlen nevet, például az öröklődés kapcsolódó objektumok közül a hivatkozni kívánt kapcsolódó objektumok közül. A nézetek meghatározásakor a neve helyett az egyes nézetek összes objektumához ajánlati beállítása a kijelölt objektumok készlete is megadhat.

Közös kijelölt csoportok neve szerint vannak megadva, a nézetek a formázási fájl vagy a definíciók nézetek meghatározásakor. Ezekben az esetekben a `SelectionSetName` gyermekeleme a `ViewSelectedBy` és `EntrySelectedBy` elemek szolgáló megadja. Kijelölt csoportok kapcsolatos további információkért lásd: [meghatározása beállítja az objektumok](./defining-selection-sets.md).

## <a name="example"></a>Példa

A következő példa bemutatja egy `SelectionSet` elem, amely négy .NET típusa határozza meg.

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

[Name elemet a SelectionSet (formátum)](./name-element-for-selectionset-format.md)

[SelectionSets elem (formátum)](./selectionsets-element-format.md)

[Típusok elem (formátum)](./types-element-for-selectionset-format.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
