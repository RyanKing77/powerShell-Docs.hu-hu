---
title: (Formátum) ViewSelectedBy SelectionSetName eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 8ab0f033-df09-4435-a8bd-76ec2d01f13b
caps.latest.revision: 13
ms.openlocfilehash: d1de2b30860bac80bf17508f40eec33c2794c4b2
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62076225"
---
# <a name="selectionsetname-element-for-viewselectedby-format"></a>A ViewSelectedBy elem SelectionSetName eleme (Formátum)

.NET-objektumokat a nézet által megjelenített egy halmazát határozza meg.

Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem ViewSelectedBy elem (formátum) SelectionSetName eleme ViewSelectedBy (formátum)

## <a name="syntax"></a>Szintaxis

```xml
<SelectionSetName>Name of selection set<SelectionSetName>
```

## <a name="attributes-and-elements"></a>Attribútumok és elemek

A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `SelectionSetName` elemet.

### <a name="attributes"></a>Attribútumok

Nincs.

### <a name="child-elements"></a>Gyermekelemek

Nincs.

### <a name="parent-elements"></a>Szülőelemek

|Elem|Leírás|
|-------------|-----------------|
|[ViewSelectedBy elem (formátum)](./viewselectedby-element-format.md)|A .NET-objektumokat a nézet által megjelenített határozza meg.|

## <a name="text-value"></a>A szöveges érték

Adja meg a kijelölési beállítása által meghatározott nevét a `Name` elem a kijelölés van állítva.

## <a name="remarks"></a>Megjegyzés

Kijelölt csoportok is használhatja, ha egyetlen nevet, például az öröklődés kapcsolódó objektumok közül a hivatkozni kívánt kapcsolódó objektumok közül. Meghatározása és a kijelölt csoportok hivatkozó kapcsolatos további információkért lásd: [meghatározása beállítja az objektumok](./defining-selection-sets.md).

## <a name="example"></a>Példa

Az alábbi példa bemutatja, hogyan állítsa be az adott nézet kijelölés megadásához. Tábla, széles és egyéni nézetekben használható ugyanazzal a sémával.

```xml
<View>
  <Name>Name of View</Name>
  <ViewSelectedBy>
    <SelectionSetName>NameofSelectionSet</SelectionSetName>>
  </ViewSelectedBy>
  <ListControl>...</ListControl>
</View>
```

## <a name="see-also"></a>Lásd még:

[Kijelölt csoportok meghatározása](./defining-selection-sets.md)

[ViewSelectedBy elem (formátum)](./viewselectedby-element-format.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
