---
title: TableControl elem (formátum) |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 1550b068-dfbc-4ae0-9aa1-72c9a680ec59
caps.latest.revision: 15
ms.openlocfilehash: 3942c008e026b0b99db3c77af4a0152b50fffc4e
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62063828"
---
# <a name="tablecontrol-element-format"></a>TableControl elem (Formátum)

Határozza meg a nézet táblázatos formában.

ViewDefinitions elem (formátum) nézetben (formátum) elem TableControl elem (formátum)

## <a name="syntax"></a>Szintaxis

```xml
<TableControl>
  <AutoSize/>
  <HideTableHeaders/>
  <TableHeaders>...</TableHeaders>
  <TableRowEntries>...</TableRowEntries>
</TableControl>

```

## <a name="attributes-and-elements"></a>Attribútumok és elemek

A következő szakaszok ismertetik az attribútumokat, gyermekelemek és szülőelemét a `TableControl` elemet. Meg kell adnia a tábla sorait. Minden más alárendelt elemek egyike sem kötelező.

### <a name="attributes"></a>Attribútumok

Nincs.

### <a name="child-elements"></a>Gyermekelemek

|Elem|Leírás|
|-------------|-----------------|
|[Automatikus méretezés eleme TableControl (formátum)](./autosize-element-for-tablecontrol-format.md)|Nem kötelező eleme.<br /><br /> Itt adhatja meg, hogy az oszlop méretét és az oszlopok számát módosulnak az adatok mérete alapján.|
|[HideTableHeaders eleme TableControl (formátum)](./hidetableheaders-element-format.md)|Nem kötelező eleme.<br /><br /> Azt jelzi, hogy a táblázat fejlécében nem jelenik meg.|
|[TableHeaders eleme TableControl (formátum)](./tableheaders-element-format.md)|Szükséges eleme.<br /><br /> A címkék a szélességet és az adatok az oszlopok a tábla nézet zarovnání határozza meg.|
|[TableRowEntries eleme TableControl (formátum)](./tablerowentries-element-for-tablecontrol-format.md)|Nem kötelező eleme.<br /><br /> A táblázatos nézetre a definíciókat tartalmazza.|

### <a name="parent-elements"></a>Szülőelemek

|Elem|Leírás|
|-------------|-----------------|
|[Nézet elem (formátum)](./view-element-format.md)|Meghatározza egy nézetet, amely egy vagy több objektum tagjait megjelenítésére szolgál.|

## <a name="remarks"></a>Megjegyzés

A táblázatos nézetre az összetevőivel kapcsolatos további információkért lásd: [tábla nézetek létrehozásával](./creating-a-table-view.md).

## <a name="example"></a>Példa

Ez a példa bemutatja egy `TableControl` elem, amellyel a tulajdonságainak megjelenítéséhez a [System.Serviceprocess.Servicecontroller](/dotnet/api/System.ServiceProcess.ServiceController) objektum.

```xml
<View>
  <Name>service</Name>
  <ViewSelectedBy>
    <TypeName>System.ServiceProcess.ServiceController</TypeName>
  </ViewSelectedBy>
  <TableControl>
    <TableHeaders>...</TableHeaders>
    <TableRowEntries>...</TableRowEntries>
  </TableControl>
</View>

```

## <a name="see-also"></a>Lásd még:

[Tábla nézet létrehozása](./creating-a-table-view.md)

[Nézet elem (formátum)](./view-element-format.md)

[Automatikus méretezés eleme TableControl (formátum)](./autosize-element-for-tablecontrol-format.md)

[HideTableHeaders elem (formátum)](./hidetableheaders-element-format.md)

[TableHeaders elem (formátum)](./tableheaders-element-format.md)

[TableRowEntries elem (formátum)](./tablerowentries-element-for-tablecontrol-format.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
