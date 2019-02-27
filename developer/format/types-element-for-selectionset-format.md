---
title: Elem SelectionSet (formátum)-típusokat |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 4606fec0-ff31-4d36-af68-227405335ec3
caps.latest.revision: 15
ms.openlocfilehash: 0427367efa2c8a7e352d718706d1341a0c8e3621
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56851274"
---
# <a name="types-element-for-selectionset-format"></a>A SelectionSet Típusok eleme (Formátum)

Meghatározza a .NET-objektumok, amelyek a kijelölés beállítva.

Konfigurációs elem (formátum) SelectionSets elem (formátum) SelectionSet elem (formátum) típusú elem (formátum)

## <a name="syntax"></a>Szintaxis

```xml
<Types>
  <TypeName>Nameof.NetType</TypeName>
</Types>

```

## <a name="attributes-and-elements"></a>Attribútumok és elemek

A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `Types` elemet. Legalább egy gyermek elemnek kell lennie, de nem adható hozzá gyermek elemek számának maximális korlátozott.

### <a name="attributes"></a>Attribútumok

Nincs.

### <a name="child-elements"></a>Gyermekelemek

|Elem|Leírás|
|-------------|-----------------|
|[TypeName elem típusú (formátum)](./typename-element-for-types-format.md)|Szükséges eleme.<br /><br /> Megadja a .NET-objektum, amely a kijelölt csoporthoz tartozik.|

### <a name="parent-elements"></a>Szülőelemek

|Elem|Leírás|
|-------------|-----------------|
|[SelectionSet elem (formátum)](./selectionset-element-format.md)|Meghatároz egy .NET-objektumokat a készlet neve szerint lehet hivatkozni.|

## <a name="remarks"></a>Megjegyzés

Az objektumok, ez az elem által meghatározott nézet definíciójának által a nézet által használható kijelölés csoportjának győződjön meg arról, (nézetek rendelkezhet több definíciókat), vagy egy kiválasztási feltétel megadásakor.  Kijelölt csoportok kapcsolatos további információkért lásd: [meghatározása beállítja az objektumok](./defining-selection-sets.md).

## <a name="example"></a>Példa

Ez a példa bemutatja egy `SelectionSet` elem, amely négy .NET típusa határozza meg.

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

[Az objektumok csoportok meghatározása](./defining-selection-sets.md)

[SelectionSet elem (formátum)](./selectionset-element-format.md)

[TypeName elem típusú (formátum)](./typename-element-for-types-format.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
