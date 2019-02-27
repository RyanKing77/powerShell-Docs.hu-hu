---
title: WideControl elem (formátum) |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 715ea055-037b-46ad-b70f-87b3f5134403
caps.latest.revision: 14
ms.openlocfilehash: 2742be0389a1bf04af100a490a59c0d938165811
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56849489"
---
# <a name="widecontrol-element-format"></a>WideControl elem (Formátum)

A wide (egyetlen érték) határozza meg a Nézet formátuma. Ez a nézet jeleníti meg, egy egyetlen tulajdonságát érték vagy parancsfájlt minden objektum esetén.

Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem WideControl elem (formátum)

## <a name="syntax"></a>Szintaxis

```xml
<WideControl>
  <AutoSize/>
  <ColumnNumber>PositiveInteger</ColumnNumber>
  <WideEntries>...</WideEntries>
</WideControl>
```

## <a name="attributes-and-elements"></a>Attribútumok és elemek

A következő szakaszok ismertetik az attribútumokat, gyermekelemek és szülőelemét a `WideControl` elemet. Nem adható meg a `AutoSize` és `ColumnNumber` elemek egy időben.

### <a name="attributes"></a>Attribútumok

Nincs.

### <a name="child-elements"></a>Gyermekelemek

|Elem|Leírás|
|-------------|-----------------|
|[Automatikus méretezés eleme WideControl (formátum)](./autosize-element-for-widecontrol-format.md)|Nem kötelező eleme.<br /><br /> Itt adhatja meg, hogy az oszlop méretét és az oszlopok számát módosulnak az adatok mérete alapján.|
|[ColumnNumber eleme WideControl (formátum)](./columnnumber-element-for-widecontrol-format.md)|Nem kötelező eleme.<br /><br /> A széles nézet oszlopainak számát adja meg.|
|[WideEntries elem (formátum)](./wideentries-element-for-widecontrol-format.md)|Szükséges eleme.<br /><br /> A széles nézet a definíciókat tartalmazza.|

### <a name="parent-elements"></a>Szülőelemek

|Elem|Leírás|
|-------------|-----------------|
|[Nézet elem (formátum)](./view-element-format.md)|Meghatározza egy nézetet, amely legalább egy .NET-objektumokká megjelenítésére szolgál.|

## <a name="remarks"></a>Megjegyzés

Egy széles nézet meghatározásakor adhat hozzá a `AutoSize` elem vagy a `ColumnNumber` , de nem adja hozzá mindkettőt.

A legtöbb esetben csak egyetlen definíciót minden széles nézet megadása kötelező, de lehetséges több definíciókkal rendelkeznek, ha ugyanabban a nézetben különböző .NET-objektumok megjelenítéséhez használandó. Ezekben az esetekben adja meg egy külön meghatározása az egyes objektumok vagy objektumok közül.

Egy széles nézet az összetevőivel kapcsolatos további információkért lásd: [széles nézet összetevők](./creating-a-wide-view.md).

## <a name="example"></a>Példa

A következő példa bemutatja egy `WideControl` elem, amely egy tulajdonságának megjelenítéséhez használja a [System.Diagnostics.Process](/dotnet/api/System.Diagnostics.Process) objektum.

```xml
<View>
  <Name>process</Name>
  <ViewSelectedBy>
    <TypeName>System.Diagnostics.Process</TypeName>
  </ViewSelectedBy>
  <WideControl>
    <WideEntries>...</WideEntries>
  </WideControl>
</View>
```

Egy széles nézet egy teljes példa: [széles nézet (alapszintű)](./wide-view-basic.md).

## <a name="see-also"></a>Lásd még:

[Automatikus méretezés eleme WideControl (formátum)](./autosize-element-for-widecontrol-format.md)

[ColumnNumber eleme WideControl (formátum)](./columnnumber-element-for-widecontrol-format.md)

[Nézet elem (formátum)](./view-element-format.md)

[WideEntries elem (formátum)](./wideentries-element-for-widecontrol-format.md)

[Széles nézet (alapszintű)](./wide-view-basic.md)

[Egy széles nézet létrehozása](./creating-a-wide-view.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
