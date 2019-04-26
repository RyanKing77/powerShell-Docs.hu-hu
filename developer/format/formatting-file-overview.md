---
title: Formázás – áttekintés |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: fe888fee-1fe9-459f-9d62-35732c19a7f8
caps.latest.revision: 13
ms.openlocfilehash: d418cff70c1197aa3c331eed909f49198da139e9
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62065733"
---
# <a name="formatting-file-overview"></a>Formázási fájl – Áttekintés

Parancsok (parancsmagok, függvények és parancsfájlok) által visszaadott objektumaihoz tartozó megjelenítési formátuma formázási fájlok (format.ps1xml) segítségével határozzák meg. Több ilyen fájllal határozza meg azokat az objektumokat által biztosított PowerShell-parancsok, például a visszaadott megjelenítési formátumát a PowerShell által biztosított a [System.Diagnostics.Process](/dotnet/api/System.Diagnostics.Process) által visszaadott objektum a `Get-Process` parancsmagot. Azonban is létrehozhat saját egyéni formázási fájlok felülírja az alapértelmezett megjelenítési formátum, vagy írhat meghatározásához a saját parancsok által visszaadott objektumok megjelenítéséhez egyéni formázási fájlt.

> [!IMPORTANT]
> Formázási fájlokat nem határozzák meg a folyamat visszaadott objektum elemét. Visszaadott objektum a folyamat, amikor az objektum összes tagja érhetők el még akkor is, ha némelyike nem jelenik meg.

PowerShell a formázási ezeket a fájlokat az adatok segítségével határozza meg, mi jelenjen meg, és a megjelenített adatok formázását. A megjelenített adatok az objektum tulajdonságainak és a egy parancsfájl értékét tartalmazhatnak. Parancsprogramok akkor használhatók, ha azt szeretné, néhány érték, amely nem érhető el közvetlenül a objektumot, például hozzáadása egy objektum két tulajdonság értékét, és ezután megjelenítése az összeg, az adatok tulajdonságainak megjelenítéséhez. A megjelenített adatok formázása a megjeleníteni kívánt objektumok nézetek definiálásával történik. Megadhatja, hogy egyetlen nézetben minden objektum esetén, meghatározhatja, hogy egyetlen nézetben több objektumon, vagy megadhat több nézetet ugyanahhoz az objektumhoz. Nincs nem definiálható nézetek száma nincs korlátozva.

## <a name="common-features-of-formatting-files"></a>A formázási fájlok általános szolgáltatások

Minden egyes formázási fájl a következő összetevők határozzák meg a fájl minden nézetek között megosztható definiálhatja:

- Alapértelmezés szerint a konfigurációs beállítások, például hogy a táblák sorait megjelenített adatok jelennek meg a következő sorban hosszabb, mint az oszlop szélessége adatok esetén. Ezekkel a beállításokkal kapcsolatos további információkért lásd: [közös konfigurációs beállítások meghatározása](./defining-common-configuration-features.md).

- A formázási fájl nézetek által megjelenített objektumok készleteit. További információ ezen készletek (néven *kijelölt csoportok*), lásd: [meghatározása beállítja az objektumok](./defining-selection-sets.md).

- A formázási fájl összes nézetek által használt Gyakori vezérlők. Vezérlők teszik lehetővé az adatok megjelenítésének lehet finomabb szabályozásra. Vezérlők kapcsolatos további információkért lásd: [egyéni vezérlők meghatározása](./creating-custom-controls.md).

## <a name="formatting-views"></a>Formázási nézetek

Formázási nézetek objektumokat megjelenítheti egy táblázatos formátumú, listaformátumban, széles és egyéni formátum. Minden egyes formázási definíció többségében, a nézet leíró XML-címkék csoportja által leírása. Mindegyik nézetről tartalmaz a nézet nevét az objektumok, amelyek a nézet és az elemek a nézetet, például az oszlopok és sorok információk a táblázatos nézetre.

Táblázat nézet egy objektum vagy egy parancsfájl blokk értéket egy vagy több oszlop tulajdonságait. Minden oszlop egy egyetlen tulajdonságát az objektum vagy egy parancsfájl értéket képvisel. Definiálhat egy objektumot, vagy a tulajdonságok és parancsfájl-értékek, a tulajdonságok egy részének objektum tulajdonságait megjelenítő táblázat nézet. A táblázat minden egyes sorára jelenti. a visszaadott objektum. Tábla nézet létrehozásával nagyon hasonlít mikor egy objektum, kanálu a `Format-Table` parancsmagot. Ez a nézet kapcsolatos további információkért lásd: [táblázatos nézetre](./creating-a-table-view.md).

Nézet megjeleníti a tulajdonságok listázásához egy objektum vagy egy parancsfájl egyetlen oszlop értéke. A lista minden egyes sorára egy nem kötelező címke vagy tulajdonság vagy parancsfájl értékét a tulajdonság nevét jeleníti meg. Lista nézet létrehozásával nagyon hasonlít egy objektum átirányításával a `Format-List` parancsmagot. Ez a nézet kapcsolatos további információkért lásd: [listanézet](./creating-a-list-view.md).

Széles nézet egy objektum vagy egy parancsfájl értéket egy vagy több oszlop egyetlen tulajdonságát sorolja fel. Nincs címke vagy fejléc ehhez a nézethez. Széles körű nézetek létrehozásával nagyon hasonlít egy objektum átirányításával a `Format-Wide` parancsmagot. Ez a nézet kapcsolatos további információkért lásd: [széles nézet](./creating-a-wide-view.md).

Egyéni nézet nézetet jelenít meg egy testre szabható objektum tulajdonságai vagy parancsfájl értékek, amelyek nem követi a nézetek, a nézetek és a széles körű nézetek merev struktúráját. Meghatározhat egy különálló egyéni nézetet, vagy megadhat egy egyéni nézet, amelyet egy másik nézetre, például egy táblázat vagy lista nézetben. Egyéni nézet létrehozása nagyon hasonlít egy objektum átirányításával a `Format-Custom` parancsmagot. Ez a nézet kapcsolatos további információkért lásd: [egyéni nézet](./creating-custom-controls.md).

## <a name="components-of-a-view"></a>Nézet összetevői

A következő XML-példákat az alapvető XML-összetevők nézet megjelenítése. Az egyéni XML-elemeket eltérőek lehetnek attól függően, hogy melyik nézet szeretne létrehozni, de az alapvető összetevők nézetek azonos.

Első lépésként mindegyik nézetről tartalmaz egy `Name` elem, amely meghatározza egy felhasználóbarát nevet, amellyel hivatkozni a nézetet. egy `ViewSelectedBy` elem, amely meghatározza, mely a .NET-objektumok jelennek meg a nézet által és a egy *vezérlő* elem, amely meghatározza a nézetet.

```xml
<ViewDefinitions>
  <View>
    <Name>NameOfView</Name>
    <ViewSelectedBy>...</ViewSelectedBy>
    <TableControl>...</TableControl>
  </View>
  <View>
    <Name>NameOfView</Name>
    <ViewSelectedBy>...</ViewSelectedBy>
    <ListControl>...</ListControl>
  <View>
  <View>
    <Name>NameOfView</Name>
    <ViewSelectedBy>...</ViewSelectedBy>
    <WideControl>...</WideControl>
  <View>
  <View>
    <Name>NameOfView</Name>
    <ViewSelectedBy>...</ViewSelectedBy>
    <CustomControl>...</CustomControl>
  </View>
</ViewDefinitions>

```

A vezérlő elemen belül megadhat egy vagy több *bejegyzés* elemeket. Ha víc definic használ, meg kell adnia, mely .NET-objektumokká használata minden egyes definíciója. Általában csak egy bejegyzést, csak egyetlen definíciót, az egyes vezérlőelemek van szükség.

```xml
<ListControl>
  <ListEntries>
    <ListEntry>
      <EntrySelectedBy>...</EntrySelectedBy>
      <ListItems>...</ListItems>
    <ListEntry>
    <ListEntry>
        <EntrySelectedBy>...</EntrySelectedBy>
      <ListItems>...</ListItems>
    <ListEntry>
    <ListEntry>
        <EntrySelectedBy>...</EntrySelectedBy>
      <ListItems>...</ListItems>
    <ListEntry>
  </ListEntries>
</ListControl>

```

A nézetek minden egyes belépési elemen belül adjon meg a *elem* a .NET-tulajdonságok vagy parancsfájlok, amely a nézetben megjelenített meghatározó elemeket.

```xml

<ListItems>
  <ListItem>...</ListItem>
  <ListItem>...</ListItem>
  <ListItem>...</ListItem>
</ListItems>

```

Ahogyan az előző példák, a formázási fájlt tartalmazhat több nézetet, nézet víc definic is tartalmazhat, és minden egyes tartalmazhat több elem.

## <a name="example-of-a-table-view"></a>Példa a táblázatos nézetre

Az alábbi példa bemutatja a táblázatos nézetre, amely tartalmazza a két oszlopot definiáló XML-címkéket. A [ViewDefinitions](./viewdefinitions-element-format.md) elem a tároló eleme a formázási fájlban meghatározott összes nézetben megtekinthetők. A [nézet](./view-element-format.md) elem definiálja az adott tábla, list, szélesre vagy egyéni nézet. Belül [nézet](./view-element-format.md) elem, a [neve](./name-element-for-view-format.md) elem nevét adja meg a nézet a [ViewSelectedBy](./viewselectedby-element-format.md) elem definiálja a megtekintése, valamint a különböző objektumok szabályozhatja az elemeket (például a `TableControl` elem a következő példában látható) határozza meg a nézet típusa.

```xml
<ViewDefinitions>
  <View>
    <Name>Name of View</Name>
    <ViewSelectedBy>
      <TypeName>Object to display using this view</TypeName>
      <TypeName>Object to display using this view</TypeName>
    </ViewSelectedBy>
    <TableControl>
      <TableHeaders>
        <TableColumnHeader>
          <Width></Width>
        </TableColumnHeader>
        <TableColumnHeader>
          <Width></Width>
        </TableColumnHeader>
      </TableHeaders>
      <TableRowEntries>
        <TableRowEntry>
          <TableColumnItems>
            <TableColumnItem>
              <PropertyName>Header for column 1</PropertyName>
            </TableColumnItem>
            <TableColumnItem>
              <PropertyName>Header for column 2</PropertyName>
            </TableColumnItem>
          </TableColumnItems>
        </TableRowEntry>
      </TableRowEntries>
    </TableControl)
  </View>
</ViewDefinitions>

```

## <a name="see-also"></a>Lásd még:

[Lista nézet létrehozása](./creating-a-list-view.md)

[Tábla nézet létrehozása](./creating-a-table-view.md)

[Egy széles nézet létrehozása](./creating-a-wide-view.md)

[Egyéni vezérlők létrehozását](./creating-custom-controls.md)

[Egy PowerShell-formázást és típusok fájl írása](./writing-a-powershell-formatting-file.md)
