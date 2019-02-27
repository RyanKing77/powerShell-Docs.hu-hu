---
title: ViewSelectedBy elem (formátum) |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: acdeef4d-3554-4f39-a7e6-a684e3848fd7
caps.latest.revision: 19
ms.openlocfilehash: efc1c5d1338889ecd0be7150b7733842ce78979e
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56851841"
---
# <a name="viewselectedby-element-format"></a>ViewSelectedBy elem (Formátum)

A .NET-objektumokat a nézet által megjelenített határozza meg. Minden egyes nézet adjon meg legalább egy .NET-objektumokat.

ViewDefinitions elem (formátum) nézetben (formátum) elem ViewSelectedBy elem (formátum)

## <a name="syntax"></a>Szintaxis

```xml
<ViewSelectedBy>
  <TypeName>Nameof.NetType</TypeName>
  <SelectionSetName>SelectionSet</SelectionSetName>
</ViewSelectedBy>
```

## <a name="attributes-and-elements"></a>Attribútumok és elemek

A következő szakaszok ismertetik az attribútumokat, gyermekelemek és szülőelemét a `ViewSelectedBy` elemet. Ezt az elemet kell tartalmaznia kell legalább egy `TypeName` vagy `SelectionSetName` gyermekelemet. Nem adható meg gyermekelemek száma korlátozott, sem a sorrend fontos.

### <a name="attributes"></a>Attribútumok

Nincs.

### <a name="child-elements"></a>Gyermekelemek

|Elem|Leírás|
|-------------|-----------------|
|[TypeName eleme ViewSelectedBy (formátum)](./typename-element-for-viewselectedby-format.md)|Nem kötelező eleme.<br /><br /> Megadja a nézet által megjelenített .NET-objektumokat.|
|[SelectionSetName eleme ViewSelectedBy (formátum)](./selectionsetname-element-for-viewselectedby-format.md)|Nem kötelező eleme.<br /><br /> .NET-objektumokat a nézet által megjelenített egy halmazát határozza meg.|

### <a name="parent-elements"></a>Szülőelemek

|Elem|Leírás|
|-------------|-----------------|
|[Nézet elem (formátum)](./view-element-format.md)|Legalább egy .NET-objektumokat megjelenítő nézet határozza meg.|

## <a name="remarks"></a>Megjegyzés

Ez az elem használatának módja a következőben különböző nézeteket kapcsolatos további információkért lásd: [táblázat nézet összetevők](./creating-a-table-view.md), [lista nézet összetevők](./creating-a-list-view.md), [széles nézet összetevők](./creating-a-wide-view.md), és [Egyéni vezérlő összetevők](./creating-custom-controls.md).

A `SelectionSetName` elem szolgál, ha a formázási fájl határozza meg, amely több nézetek által megjelenített objektumok közül. Kijelölt csoportok definiált és hivatkozott hogyan kapcsolatos további információkért lásd: [meghatározása beállítja az objektumok](./defining-selection-sets.md).

## <a name="example"></a>Példa

Az alábbi példa bemutatja, hogyan adja meg a [System.Serviceprocess.Servicecontroller](/dotnet/api/System.ServiceProcess.ServiceController) objektum az adott nézet. Tábla, széles és egyéni nézetekben használható ugyanazzal a sémával.

```xml
<View>
  <Name>System.ServiceProcess.ServiceController</Name>
  <ViewSelectedBy>
    <TypeName>System.ServiceProcess.ServiceController</TypeName>
  </ViewSelectedBy>
  <ListControl>...</ListControl>
</View>
```

## <a name="see-also"></a>Lásd még:

[Lista nézet létrehozása](./creating-a-list-view.md)

[Tábla nézet létrehozása](./creating-a-table-view.md)

[Egy széles nézet létrehozása](./creating-a-wide-view.md)

[Egyéni vezérlők létrehozását](./creating-custom-controls.md)

[Kijelölt csoportok meghatározása](./defining-selection-sets.md)

[SelectionSetName eleme ViewSelectedBy (formátum)](./selectionsetname-element-for-viewselectedby-format.md)

[TypeName elem (formátum)](./typename-element-for-viewselectedby-format.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
