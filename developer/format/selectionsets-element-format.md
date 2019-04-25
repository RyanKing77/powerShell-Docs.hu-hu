---
title: SelectionSets elem (formátum) |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: ebbac73a-1c99-4388-9f47-703cd024dc6d
caps.latest.revision: 18
ms.openlocfilehash: a9356635d60d5f8c5d4dec4ec8b7d0aea2b037dd
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62063775"
---
# <a name="selectionsets-element-format"></a>SelectionSets elem (Formátum)

Határozza meg a gyakori eljárások egyikét a formázási fájl összes nézetek által használható .NET-objektumokat. A nézetek és a formázási fájl vezérlők csak a kijelölt csoport nevét az objektumok teljes készletének hivatkozhat.

Konfigurációs elem SelectionSets elem formátuma

## <a name="syntax"></a>Szintaxis

```xml
<SelectionSets>
  <SelectionSet>...</SelectionSet>
</SelectionSets>
```

## <a name="attributes-and-elements"></a>Attribútumok és elemek

A következő szakaszok ismertetik az attribútumokat, gyermekelemek és szülőelemét a `SelectionSets` elemet. Minden egyes gyermekelemet határozza meg azon objektumok, amely a készlet neve szerint lehet hivatkozni. Az alárendelt összetevők sorrendje nem lényeges.

### <a name="attributes"></a>Attribútumok

Nincs.

### <a name="child-elements"></a>Gyermekelemek

|Elem|Leírás|
|-------------|-----------------|
|[SelectionSet elem (formátum)](./selectionset-element-format.md)|Szükséges eleme.<br /><br /> Meghatároz egy egységes .NET-objektumokat a készlet neve szerint lehet hivatkozni.|

### <a name="parent-elements"></a>Szülőelemek

|Elem|Leírás|
|-------------|-----------------|
|[Konfigurációs elem](./configuration-element-format.md)|A legfelső szintű elem egy formázási fájl jelöli.|

## <a name="remarks"></a>Megjegyzés

Kijelölt csoportok is használhatja, ha egyetlen nevet, például az öröklődés kapcsolódó objektumok közül a hivatkozni kívánt kapcsolódó objektumok közül. A nézetek meghatározásakor a neve helyett az egyes nézetek összes objektumához ajánlati beállítása a kijelölt objektumok készlete is megadhat.

Közös kijelölt csoportok neve szerint vannak megadva, a nézetek a formázási fájl vagy a definíciók nézetek meghatározásakor. Ezekben az esetekben a `SelectionSetName` gyermekeleme a `ViewSelectedBy` és `EntrySelectedBy` elemek szolgáló megadja. Kijelölt csoportok kapcsolatos további információkért lásd: [meghatározása beállítja az objektumok](./defining-selection-sets.md).

## <a name="see-also"></a>Lásd még:

[Konfigurációs elem](./configuration-element-format.md)

[Kijelölt csoportok meghatározása](./defining-selection-sets.md)

[SelectionSet elem (formátum)](./selectionset-element-format.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
