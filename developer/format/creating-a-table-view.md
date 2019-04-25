---
title: Tábla nézet létrehozásával |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 1f405afb-70b5-4fe0-9986-bc07401d93fd
caps.latest.revision: 23
ms.openlocfilehash: 862f942facafff6cea66c4f8f1040772c6a62ec3
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62066838"
---
# <a name="creating-a-table-view"></a>Tábla nézet létrehozása

Táblázatos nézetre egy vagy több oszlop adatait jeleníti meg. A tábla minden sorára .NET-objektumokat, és a tábla minden oszlopához az objektum vagy egy parancsfájl érték tulajdonsága jelenti. Definiálhat egy objektumának tulajdonságait, vagy az objektum a tulajdonságok egy részének megjelenítő táblázat nézet.

## <a name="a-table-view-display"></a>Egy táblázat nézet megjelenítése

Az alábbi példa bemutatja, hogyan jelenítse meg a Windows PowerShell a [System.Serviceprocess.Servicecontroller](/dotnet/api/System.ServiceProcess.ServiceController) által visszaadott objektum a [Get-Service](/powershell/module/microsoft.powershell.management/get-service) parancsmagot. Az objektum, a Windows PowerShell definiálva van, amely megjeleníti a táblázatos nézetre a `Status` tulajdonság, a `Name` tulajdonság (Ez a tulajdonság egy aliast tulajdonsága nem a `ServiceName` tulajdonság), és a `DisplayName` tulajdonság. A tábla minden sorára a parancsmag által visszaadott objektumot jelöl.

```output
Status   Name               DisplayName
------   ----               -----------
Stopped  AJRouter           AllJoyn Router Service
Stopped  ALG                Application Layer Gateway Service
Stopped  AppIDSvc           Application Identity
Running  Appinfo            Application Information
```

## <a name="defining-the-table-view"></a>A táblázat nézet definiálása

A következő XML formátumú bemutatja a táblaséma megtekintése megjelenítése a [System.Serviceprocess.Servicecontroller? Displayproperty = Fullname](/dotnet/api/System.ServiceProcess.ServiceController) objektum. Meg kell adnia, hogy a tábla nézetben megjeleníteni kívánt minden egyes tulajdonság.

```xml
<View>
  <Name>service</Name>
  <ViewSelectedBy>
    <TypeName>System.ServiceProcess.ServiceController</TypeName>
  </ViewSelectedBy>
  <TableControl>
    <TableHeaders>
      <TableColumnHeader>
        <Width>8</Width>
      </TableColumnHeader>
      <TableColumnHeader>
        <Width>18</Width>
      </TableColumnHeader>
      <TableColumnHeader>
        <Width>38</Width>
      </TableColumnHeader>
    </TableHeaders>
    <TableRowEntries>
      <TableRowEntry>
        <TableColumnItems>
          <TableColumnItem>
           <PropertyName>Status</PropertyName>
          </TableColumnItem>
          <TableColumnItem>
            <PropertyName>Name</PropertyName>
          </TableColumnItem>
          <TableColumnItem>
            <PropertyName>DisplayName</PropertyName>
          </TableColumnItem>
        </TableColumnItems>
      </TableRowEntry>
    </TableRowEntries>
  </TableControl>
</View>
```

A következő XML-elemeket a lista nézet meghatározásához használják:

- A [nézet](./view-element-format.md) elem a szülőelemet, táblázat nézet. (Ez az az ugyanazon szülőelem széles, és egyéni nézetekben a listát.)

- A [neve](./name-element-for-view-format.md) elem azt határozza meg a nézet nevét. Ehhez az elemhez kötelező megadni az összes nézetben megtekinthetők.

- A [ViewSelectedBy](./viewselectedby-element-format.md) elem definiálja az objektumok, amelyek a nézetet. Ez az elem megadása kötelező.

- A [GroupBy](./groupby-element-for-view-format.md) (ebben a példában nem látható) elem határozza meg, ha az objektumok egy új csoport megjelenik. Egy új csoportot, ha az érték egy adott tulajdonságra vagy parancsfájl el van indítva. Ez az elem nem kötelező.

- A [vezérlők](./controls-element-for-view-format.md) (ebben a példában nem látható) elem definiálja az egyéni vezérlők a tábla nézet által meghatározott. Vezérlők további adja meg, hogyan jelenjen meg az adatokat egy módot biztosít. Ez az elem nem kötelező. Nézet definiálhat a saját egyéni vezérlők, vagy telepítheti a nézeten a formázási fájlban használt Gyakori vezérlők. Egyéni vezérlők kapcsolatos további információkért lásd: [egyéni vezérlők létrehozását](./creating-custom-controls.md).

- A [HideTableHeaders](./hidetableheaders-element-format.md) elem (nem látszik ebben a példában), adja meg, hogy a tábla nem jelenik meg a tábla tetején lévő címkéket. Ez az elem nem kötelező.

- A [TableControl](./tablecontrol-element-format.md) elem, amely meghatározza a fejlécet és a sor információkat a táblázat. Minden más nézetekhez hasonlóan táblázatos nézetre jeleníthet meg az objektum tulajdonságainak vagy parancsfájlok által létrehozott értékek.

## <a name="defining-column-headers"></a>Oszlopfejlécek meghatározása

1. A [TableHeaders](./tableheaders-element-format.md) elem, és gyermekelemeinek határozza meg a tábla tetején jelenik meg.

2. A [TableColumnHeader](./tablecolumnheader-element-format.md) elem definiálja a tábla egy oszlop tetején jelenik meg. Adja meg ezeket az elemeket a ahhoz, hogy szeretné-e a fejlécek jelenik meg.

   Nem használható ezen elem száma, de száma korlátozott [TableColumnHeader](./tablecolumnheader-element-format.md) elemeit a táblázatos nézetre számának egyenlőnek kell lennie [TableRowEntry](./tablerowentry-element-for-tablerowentries-for-tablecontrol-format.md) elemeket, amelyeket használhat.

3. A [címke](./label-element-for-tablecolumnheader-for-tablecontrol-format.md) elem azt határozza meg a megjelenített szöveget. Ez az elem nem kötelező.

4. A [szélesség](./width-element-for-tablecolumnheader-for-tablecontrol-format.md) elem azt határozza meg az oszlop szélessége (a karakter). Ez az elem nem kötelező.

5. A [igazítás](./alignment-element-for-tablecolumnheader-for-tablecontrol-format.md) elem azt határozza meg, hogyan jelenjen meg a címke. A címke lehet balra, jobbra, vagy közepén. Ez az elem nem kötelező.

## <a name="defining-the-table-rows"></a>A táblázat sorait meghatározása

Nézetek biztosíthat egy vagy több adja meg, milyen adatokat a sorokat a tábla jelenik meg, az alárendelt összetevők használatával kapcsolatos definíciókat a [TableRowEntries](./tablerowentries-element-for-tablecontrol-format.md) elemet. Figyelje meg, hogy a sorokat a tábla több definícióit is megadhat, de a fejlécek, a sorok változatlan marad, függetlenül attól, milyen sor definition használja. Egy tábla általában csak egyetlen definíciót tartalmazza.

A következő példában a nézetet biztosít, amely több tulajdonságának értékét jeleníti meg egyetlen meghatározást az [System.Diagnostics.Process? Displayproperty = Fullname](/dotnet/api/System.Diagnostics.Process) objektum. Táblázatos nézetre megjelenítheti egy tulajdonság értékét, vagy egy parancsfájl (a példában nem látható) értékét a sorokat.

```xml
<TableRowEntries>
      <TableRowEntry>
        <TableColumnItems>
          <TableColumnItem>
           <PropertyName>Status</PropertyName>
          </TableColumnItem>
          <TableColumnItem>
            <PropertyName>Name</PropertyName>
          </TableColumnItem>
          <TableColumnItem>
            <PropertyName>DisplayName</PropertyName>
          </TableColumnItem>
        </TableColumnItems>
      </TableRowEntry>
    </TableRowEntries>

```

A következő XML-elemeket adjon meg egy olyan sor definíciók használható:

- A [TableRowEntries](./tablerowentries-element-for-tablecontrol-format.md) elem és a gyermekelemeinek határozza meg, mi jelenjen meg a tábla sorait.

- A [TableRowEntry](./listentry-element-for-listcontrol-format.md) elem biztosít a sor meghatározását. Legalább egy [TableRowEntry](./listentry-element-for-listcontrol-format.md) szükséges; azonban nem adhat hozzá elemek számának nincs maximális korlátot. A legtöbb esetben a nézet csak egyetlen definíciót fog rendelkezni.

- A [EntrySelectedBy](./entryselectedby-element-for-tablerowentry-for-tablecontrol-format.md) elem azt határozza meg az objektumok, amelyek egy adott definíciója szerint jelennek meg. Ez az elem nem kötelező, és csak a több meghatározása során van szükség [TableRowEntry](./listentry-element-for-listcontrol-format.md) elemek, amelyek a különböző objektumok megjelenítéséhez.

- A [burkolása](./wrap-element-for-tablerowentry-for-tablecontrol-format.md) elem azt határozza meg, hogy a következő sorban megjelenik-e a szöveg, amely meghaladja az oszlopok szélességét. Alapértelmezés szerint a rendszer csonkolja szöveg, amely meghaladja az oszlopok szélességét.

- A [TableColumnItems](./tablecolumnitems-element-for-tablerowentry-for-tablecontrol-format.md) elem definiálja a Tulajdonságok vagy parancsfájlok, melynek értékei jelennek meg a sorban.

- A [TableColumnItem](./tablecolumnitem-element-for-tablecolumnitems-for-tablecontrol-format.md) elem definiálja a tulajdonságot, vagy a parancsfájl, amelynek értéke megjelenik a sor oszlopában. A [TableColumnItem](./tablecolumnitem-element-for-tablecolumnitems-for-tablecontrol-format.md) elem megadása kötelező a sor minden oszlophoz. Az első bejegyzés jelenik meg az első oszlopban a második bejegyzés a második oszlopban, és így tovább.

- A [PropertyName](./propertyname-element-for-tablecolumnitem-for-tablecontrol-format.md) elem azt határozza meg a tulajdonságot, amelynek értéke megjelenik a sorban. Adjon meg egy tulajdonságot vagy a parancsfájl azonban mindkettő megadására nincs lehetőség.

- A [ScriptBlock](./scriptblock-element-for-tablecolumnitem-for-tablecontrol-format.md) elem megadja a parancsprogramot, amelynek értéke megjelenik a sorban. Meg kell adnia egy parancsfájl vagy a tulajdonságot azonban mindkettő megadására nincs lehetőség.

- A [FormatString](./label-element-for-listitem-for-listcontrol-format.md) elem azt határozza meg, amely meghatározza, hogyan jelenjen meg a tulajdonság vagy parancsfájl érték formátuma mintát. Ez az elem nem kötelező.

- A [igazítás](./alignment-element-for-tablecolumnitem-for-tablecontrol-format.md) elem azt határozza meg, hogyan jelenjen meg az érték a tulajdonság vagy parancsfájl. Az érték lehet balra, jobbra, vagy közepén. Ez az elem nem kötelező.

## <a name="defining-the-objects-that-use-the-table-view"></a>Az objektumok, amelyek a táblázatos nézetre meghatározása

Két módon határozza meg, mely a .NET-objektumok használata a táblázatos nézetre. Használhatja a [ViewSelectedBy](./viewselectedby-element-format.md) elem jeleníthető meg úgy a nézetet, vagy a definíciókat objektumok használhatja a [EntrySelectedBy](./entryselectedby-element-for-listentry-for-listcontrol-format.md) elem határozza meg, hogy mely objektumok szerint jelennek meg a a nézet adott meghatározása. A legtöbb esetben a nézet csak egyetlen definíciót, rendelkezik, ezért általában által meghatározott objektumok a [ViewSelectedBy](./viewselectedby-element-format.md) elemet.

Az alábbi példa bemutatja, hogyan jelennek meg a táblázat nézet használatával objektumok a [ViewSelectedBy](./viewselectedby-element-format.md) és [TypeName](./typename-element-for-viewselectedby-format.md) elemeket. Nem korlátozott számú [TypeName](./typename-element-for-viewselectedby-format.md) elemeket, hogy is megadhat, és a sorrendjük nem lényeges.

```xml
<View>
  <Name>System.ServiceProcess.ServiceController</Name>
  <ViewSelectedBy>
    <TypeName>System.ServiceProcess.ServiceController</TypeName>
  </ViewSelectedBy>
  <TableControl>...</TableControl>
</View>
```

A következő XML-elemeket adja meg az objektumokat a táblázatos nézetre által használt használható:

- A [ViewSelectedBy](./viewselectedby-element-format.md) elem határozza meg, hogy mely objektumok szerint a listanézetet jelennek meg.

- A [TypeName](./typename-element-for-viewselectedby-format.md) elem azt határozza meg a .NET-objektum, amely szerint a nézet jelenik meg. A teljes .NET típusú név megadása kötelező. Meg kell adnia legalább egy típus vagy állítsa be a nézet a kijelölés, de nincs nem adható meg elemek maximális számát.

Az alábbi példában a [ViewSelectedBy](./viewselectedby-element-format.md) és [SelectionSetName](./selectionsetname-element-for-viewselectedby-format.md) elemeket. Kijelölt csoportok használata több nézetet, például a lista nézetben definiált és a táblázatos nézetre használata ugyanazokat a megjelenített objektumok kapcsolódó készlete esetében. Hozzon létre egy kiválasztási kapcsolatos további információkért lásd: [kijelölt csoportok meghatározása](./defining-selection-sets.md).

```xml
<View>
  <Name>System.ServiceProcess.ServiceController</Name>
  <ViewSelectedBy>
    <SelectionSetName>.NET Type Set</SelectionSetName>
  </ViewSelectedBy>
  <TableControl>...</TableControl>
</View>
```

A következő XML-elemeket adja meg az objektumokat a listanézet által használt használható:

- A [ViewSelectedBy](./viewselectedby-element-format.md) elem határozza meg, hogy mely objektumok szerint a listanézetet jelennek meg.

- A [SelectionSetName](./selectionsetname-element-for-viewselectedby-format.md) elem azt határozza meg a nézetben megjelenített objektumok közül. Meg kell adnia legalább egy készlet kiválasztása vagy a nézet típusa, de nincs nem adható meg elemek maximális számát.

Az alábbi példa bemutatja, hogyan adhat meg a táblázat nézet használatával egy adott definíciója szerint jelenik meg az objektumok a [EntrySelectedBy](./entryselectedby-element-for-tablerowentry-for-tablecontrol-format.md) elemet. Ez az elem használatával, megadhatja az objektum, objektumok kiválasztása csoportja, vagy egy kiválasztási feltétel, amely meghatározza a definíció használatakor .NET nevét. A kiválasztási feltételek létrehozásával kapcsolatos további információkért lásd: [feltételek meghatározása az adatok megjelenítése](./defining-conditions-for-displaying-data.md).

> [!NOTE]
> A táblázatos nézetre víc definic létrehozásakor különböző oszlopfejlécek nem adható meg. Megadhatja, hogy csak a sorokat a tábla, például, hogy mely objektumok jelennek meg.

```xml
<TableRowEntry>
  <EntrySelectedBy>
    <TypeName>.NET Type</TypeName>
  </EntrySelectedBy>
</TableRowEntry>
```

A következő XML-elemeket adja meg az objektumokat a listanézet adott definíciójának által használt használható:

- A [EntrySelectedBy](./entryselectedby-element-for-tablerowentry-for-tablecontrol-format.md) elem határozza meg, hogy mely objektumok jelennek meg a definíció szerint.

- A [TypeName](./typename-element-for-entryselectedby-for-listcontrol-format.md) elem azt határozza meg a .NET-objektum, amely a definíció szerint jelenik meg. Ez az elem használatakor a teljes .NET típusú név megadása kötelező. Meg kell adnia legalább egy típus, kijelölés set vagy kijelölés feltételt a definíciójában, de nincs nem adható meg elemek maximális számát.

- A [SelectionSetName](./selectionsetname-element-for-entryselectedby-for-listcontrol-format.md) (nem látható) elemet, adja meg a definíció megjelenített objektumok közül. Meg kell adnia legalább egy típus, kijelölés set vagy kijelölés feltételt a definíciójában, de nincs nem adható meg elemek maximális számát.

- A [SelectionCondition](./selectioncondition-element-for-entryselectedby-for-listcontrol-format.md) (nem látható) elemet, adja meg egy feltételt, amely a definíció használandó léteznie kell. Meg kell adnia legalább egy típus, kijelölés set vagy kijelölés feltételt a definíciójában, de nincs nem adható meg elemek maximális számát. További információ a kiválasztási feltételek meghatározása: [feltételek meghatározása az adatok megjelenítése](./defining-conditions-for-displaying-data.md).

## <a name="using-format-strings"></a>Formázási karakterláncokat használatával

A nézet még jobban meghatározhatja, hogyan jelenjen meg az adatok formázási karakterláncokat is hozzáadhatók. Az alábbi példa bemutatja, hogyan definiáljon értékét formázási karakterláncot a `StartTime` tulajdonság.

```xml
<TableColumnItem>
  <PropertyName>StartTime</PropertyName>
  <FormatString>{0:MMM} (0:DD) (0:HH):(0:MM)</FormatString>
</TableColumnItem>
```

A következő XML-elemeket segítségével adjon meg egy Formátumminta:

- A [TableColumnItem](./tablecolumnitem-element-for-tablecolumnitems-for-tablecontrol-format.md) elem definiálja a tulajdonságot, vagy a parancsfájl, amelynek értéke megjelenik a sor oszlopában. A [TableColumnItem](./tablecolumnitem-element-for-tablecolumnitems-for-tablecontrol-format.md) elem megadása kötelező a sor minden oszlophoz. Az első bejegyzés jelenik meg az első oszlopban a második bejegyzés a második oszlopban, és így tovább.

- A [PropertyName](./propertyname-element-for-tablecolumnitem-for-tablecontrol-format.md) elem azt határozza meg a tulajdonságot, amelynek értéke megjelenik a sorban. Adjon meg egy tulajdonságot vagy a parancsfájl azonban mindkettő megadására nincs lehetőség.

- A [FormatString](./label-element-for-listitem-for-listcontrol-format.md) elem azt határozza meg, amely meghatározza, hogyan jelenjen meg a tulajdonság vagy parancsfájl érték formátuma mintát.

A következő példában a `ToString` módszert hívja meg a parancsfájl értékének. Parancsprogramok segítségével meghívhatja a bármely metódusát meghívná, egy objektumot. Ezért ha egy objektum tartozik egy módszer, például `ToString`, van formázási paramétereket, a parancsfájl segítségével meghívhatja a módszer a parancsfájl kimenete értékének.

```xml
<ListItem>
  <ScriptBlock>
    [String]::Format("(0,10) (1,8)", .LastWriteTime.ToString("d"),
    $_.LastWriteTime.Totring("t"))
  </ScriptBlock>
</ListItem>
```

A következő XML-elem segítségével hívása a `ToString` módszer:

- A [TableColumnItem](./tablecolumnitem-element-for-tablecolumnitems-for-tablecontrol-format.md) elem definiálja a tulajdonságot, vagy a parancsfájl, amelynek értéke megjelenik a sor oszlopában. A [TableColumnItem](./tablecolumnitem-element-for-tablecolumnitems-for-tablecontrol-format.md) elem megadása kötelező a sor minden oszlophoz. Az első bejegyzés jelenik meg az első oszlopban a második bejegyzés a második oszlopban, és így tovább.

- A [ScriptBlock](./scriptblock-element-for-tablecolumnitem-for-tablecontrol-format.md) elem megadja a parancsprogramot, amelynek értéke megjelenik a sorban. Meg kell adnia egy parancsfájl vagy a tulajdonságot azonban mindkettő megadására nincs lehetőség.

## <a name="see-also"></a>Lásd még:

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
