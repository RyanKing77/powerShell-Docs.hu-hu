---
title: Lista nézet létrehozásával |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 8c7a40ca-1786-46f0-bab5-6ce229daa7ee
caps.latest.revision: 14
ms.openlocfilehash: 25d24063501196d44e0f806a55bb699c82f771ce
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62066855"
---
# <a name="creating-a-list-view"></a>Listanézet létrehozása

A listanézet csak egy oszlop (sorrendben) adatokat jeleníti meg. A listán megjelenített adatok lehetnek, a .NET-tulajdonság értéke, vagy egy parancsfájl értékét.

## <a name="a-list-view-display"></a>A lista nézet megjelenítése

A következő kimenetet jeleníti meg, hogyan jeleníti meg a Windows PowerShell tulajdonságainak [System.Serviceprocess.Servicecontroller? Displayproperty = Fullname](/dotnet/api/System.ServiceProcess.ServiceController) által visszaadott objektumok a [Get-Service](/powershell/module/microsoft.powershell.management/get-service) parancsmagot. Ebben a példában három objektumot adott vissza, az előző objektum különíteni egy üres sor minden objektumot.

```powershell
Get-Service | format-list
```

```output
Name                : AEADIFilters
DisplayName         : Andrea ADI Filters Service
Status              : Running
DependentServices   : {}
ServicesDependedOn  : {}
CanPauseAndContinue : False
CanShutdown         : False
CanStop             : True
ServiceType         : Win32OwnProcess

Name                : AeLookupSvc
DisplayName         : Application Experience
Status              : Running
DependentServices   : {}
ServicesDependedOn  : {}
CanPauseAndContinue : False
CanShutdown         : False
CanStop             : True
ServiceType         : Win32ShareProcess

Name                : AgereModemAudio
DisplayName         : Agere Modem Call Progress Audio
Status              : Running
DependentServices   : {}
ServicesDependedOn  : {}
CanPauseAndContinue : False
CanShutdown         : False
CanStop             : True
ServiceType         : Win32OwnProcess
...
```

## <a name="defining-the-list-view"></a>A lista nézet definiálása

A következő XML formátumú jeleníti meg a lista nézet séma számos tulajdonságainak megjelenítése a [System.Serviceprocess.Servicecontroller? Displayproperty = Fullname](/dotnet/api/System.ServiceProcess.ServiceController) objektum. Meg kell adnia, hogy a nézetben megjeleníteni kívánt minden egyes tulajdonság.

```xml
<View>
  <Name>System.ServiceProcess.ServiceController</Name>
  <ViewSelectedBy>
    <TypeName>System.ServiceProcess.ServiceController</TypeName>
  </ViewSelectedBy>
  <ListControl>
    <ListEntries>
      <ListEntry>
        <ListItems>
          <ListItem>
            <PropertyName>Name</PropertyName>
          </ListItem>
          <ListItem>
            <PropertyName>DisplayName</PropertyName>
          </ListItem>
          <ListItem>
            <PropertyName>Status</PropertyName>
          </ListItem>
          <ListItem>
            <PropertyName>ServiceType</PropertyName>
          </ListItem>
        </ListItems>
      </ListEntry>
    </ListEntries>
  </ListControl>
</View>
```

A következő XML-elemeket a lista nézet meghatározásához használják:

- A [nézet](./view-element-format.md) elem a lista nézet a szülőelemet. (Ez a táblához, széles és az egyéni vezérlő nézetek az ugyanazon szülőelem.)

- A [neve](./name-element-for-view-format.md) elem azt határozza meg a nézet nevét. Ehhez az elemhez kötelező megadni az összes nézetben megtekinthetők.

- A [ViewSelectedBy](./viewselectedby-element-format.md) elem definiálja az objektumok, amelyek a nézetet. Ez az elem megadása kötelező.

- A [GroupBy](./groupby-element-for-view-format.md) elem határozza meg, ha az objektumok egy új csoport megjelenik. Egy új csoportot, ha az érték egy adott tulajdonságra vagy parancsfájl el van indítva. Ez az elem nem kötelező.

- A [vezérlők](./controls-element-for-view-format.md) elem definiálja az egyéni vezérlők, a lista nézet által meghatározott. Vezérlők további adja meg, hogyan jelenjen meg az adatokat egy módot biztosít. Ez az elem nem kötelező. Nézet definiálhat a saját egyéni vezérlők, vagy telepítheti a nézeten a formázási fájlban használt Gyakori vezérlők. Egyéni vezérlők kapcsolatos további információkért lásd: [egyéni vezérlők létrehozását](./creating-custom-controls.md).

- A [ListControl](./listcontrol-element-format.md) elem definiálja a nézetben jelenik meg, és hogyan van formázva. Minden más nézetekhez hasonlóan, a listanézet jeleníthet meg az objektum tulajdonságainak vagy szkript által létrehozott értékek.

Egy példa egy teljes formázási fájl, amely meghatározza egy egyszerű lista nézet: [listanézet (alapszintű)](./list-view-basic.md).

## <a name="providing-definitions-for-your-list-view"></a>Így a lista nézet definíciói

Listanézetek biztosíthat egy vagy több definíciót alárendelt elemeinek használatával a [ListControl](./listcontrol-element-format.md) elemet. Nézet általában csak egyetlen definíciót fog rendelkezni. A következő példában a nézetet biztosít egy egyetlen definíciót, amely számos tulajdonságát megjeleníti a [System.Diagnostics.Process? Displayproperty = Fullname](/dotnet/api/System.Diagnostics.Process) objektum. A listanézet megjelenítheti egy tulajdonság értékét, vagy egy parancsfájl (a példában nem látható) értékét.

```xml
<ListControl>
    <ListEntries>
      <ListEntry>
        <ListItems>
          <ListItem>
            <PropertyName>Name</PropertyName>
          </ListItem>
          <ListItem>
            <PropertyName>DisplayName</PropertyName>
          </ListItem>
          <ListItem>
            <PropertyName>Status</PropertyName>
          </ListItem>
          <ListItem>
            <PropertyName>ServiceType</PropertyName>
          </ListItem>
        </ListItems>
      </ListEntry>
    </ListEntries>
  </ListControl>

```

A következő XML-elemeket adja meg az adott nézet definíciói használható:

- A [ListControl](./listcontrol-element-format.md) elem, és gyermekelemeinek határozza meg a nézetben jelenik meg.

- A [ListEntries](./listentries-element-for-listcontrol-format.md) elem a nézet a definíciókat tartalmazza. A legtöbb esetben a nézet csak egyetlen definíciót fog rendelkezni. Ez az elem megadása kötelező.

- A [ListEntry](./listentry-element-for-listcontrol-format.md) elem biztosít a nézet definíciójának. Legalább egy [ListEntry](./listentry-element-for-listcontrol-format.md) szükséges; azonban nem adhat hozzá elemek számának nincs maximális korlátot. A legtöbb esetben a nézet csak egyetlen definíciót fog rendelkezni.

- A [EntrySelectedBy](./entryselectedby-element-for-listentry-for-listcontrol-format.md) elem azt határozza meg az objektumok, amelyek egy adott definíciója szerint jelennek meg. Ez az elem nem kötelező, és csak a több meghatározása során van szükség [ListEntry](./listentry-element-for-listcontrol-format.md) elemek, amelyek a különböző objektumok megjelenítéséhez.

- A [ListItems elemek](./listitems-element-for-listentry-for-listcontrol-format.md) elem azt határozza meg, a tulajdonságok és a parancsfájlok, melynek értékei jelennek meg a listanézet sorait.

- A [ListItem](./listitems-element-for-listentry-for-listcontrol-format.md) elem azt határozza meg, egy tulajdonságot vagy parancsfájl, amelynek értéke megjelenik a lista nézet sorban. A listanézet adjon meg legalább egy tulajdonságot vagy parancsfájlt. Nincs maximális megadható sorok száma korlátozva van.

- A [PropertyName](./propertyname-element-for-listitem-for-listcontrol-format.md) elem azt határozza meg a tulajdonságot, amelynek értéke megjelenik a sorban. Adjon meg egy tulajdonságot vagy a parancsfájl azonban mindkettő megadására nincs lehetőség.

- A [ScriptBlock](./scriptblock-element-for-listitem-for-listcontrol-format.md) elem megadja a parancsprogramot, amelynek értéke megjelenik a sorban. Meg kell adnia egy parancsfájl vagy a tulajdonságot azonban mindkettő megadására nincs lehetőség.

- A [címke](./label-element-for-listitem-for-listcontrol-format.md) elem azt határozza meg a címke bal oldalán a tulajdonság, vagy parancsprogram érték sorában megjelenik. Ez az elem nem kötelező. Ha nincs megadva címke, a tulajdonság, vagy a parancsfájl neve jelenik meg. Egy teljes példa: [listanézet (címkék)](./list-view-labels.md).

- A [ItemSelectionCondition](./itemselectioncondition-element-for-listitem-for-listcontrol-format.md) elem azt határozza meg egy feltételt, amely a megjeleníteni kívánt sor léteznie kell. A listanézet feltételek hozzáadásával kapcsolatos további információkért lásd: [feltételek meghatározása az adatok megjelenítése](./defining-conditions-for-displaying-data.md). Ez az elem nem kötelező.

- A [FormatString](./formatstring-element-for-listitem-for-listcontrol-format.md) elem azt határozza meg, amellyel meg az értéket a tulajdonság vagy parancsfájl mintát. Ez az elem nem kötelező.

Egy példa egy teljes formázási fájl, amely meghatározza egy egyszerű lista nézet: [listanézet (alapszintű)](./list-view-basic.md).

## <a name="defining-the-objects-that-use-the-list-view"></a>Az objektumok, amelyek a lista nézet definiálása

Két módon határozza meg, melyik .NET-objektumokat a listanézetet használja. Használhatja a [ViewSelectedBy](./viewselectedby-element-format.md) elem jeleníthető meg úgy a nézetet, vagy a definíciókat objektumok használhatja a [EntrySelectedBy](./entryselectedby-element-for-listentry-for-listcontrol-format.md) elem határozza meg, hogy mely objektumok szerint jelennek meg a a nézet adott meghatározása. A legtöbb esetben a nézet csak egyetlen definíciót, rendelkezik, ezért általában által meghatározott objektumok a [ViewSelectedBy](./viewselectedby-element-format.md) elemet.

Az alábbi példa bemutatja, hogyan jelennek meg a lista nézet használatával objektumok a [ViewSelectedBy](./viewselectedby-element-format.md) és [TypeName](./typename-element-for-viewselectedby-format.md) elemeket. Nem korlátozott számú [TypeName](./typename-element-for-viewselectedby-format.md) elemeket, hogy is megadhat, és a sorrendjük nem lényeges.

```xml
<View>
  <Name>System.ServiceProcess.ServiceController</Name>
  <ViewSelectedBy>
    <TypeName>System.Diagnostics.Process</TypeName>
  </ViewSelectedBy>
  <ListControl>...</ListControl>
</View>
```

A következő XML-elemeket adja meg az objektumokat a listanézet által használt használható:

- A [ViewSelectedBy](./viewselectedby-element-format.md) elem határozza meg, hogy mely objektumok szerint a listanézetet jelennek meg.

- A [TypeName](./typename-element-for-viewselectedby-format.md) elem azt határozza meg a .NET-objektum, amely szerint a nézet jelenik meg. A teljes .NET típusú név megadása kötelező. Meg kell adnia legalább egy típus vagy állítsa be a nézet a kijelölés, de nincs nem adható meg elemek maximális számát.

Egy teljes formázási fájl egy példa: [listanézet (alapszintű)](./list-view-basic.md).

Az alábbi példában a [ViewSelectedBy](./viewselectedby-element-format.md) és [SelectionSetName](./selectionsetname-element-for-viewselectedby-format.md) elemeket. Kijelölt csoportok használata több nézetet, például a lista nézetben definiált és a táblázatos nézetre használata ugyanazokat a megjelenített objektumok kapcsolódó készlete esetében. Hozzon létre egy kiválasztási kapcsolatos további információkért lásd: [kijelölt csoportok meghatározása](./defining-selection-sets.md).

```xml
<View>
  <Name>System.ServiceProcess.ServiceController</Name>
  <ViewSelectedBy>
    <SelectionSetName>.NET Type Set</SelectionSetName>
  </ViewSelectedBy>
  <ListControl>...</ListControl>
</View>
```

A következő XML-elemeket adja meg az objektumokat a listanézet által használt használható:

- A [ViewSelectedBy](./viewselectedby-element-format.md) elem határozza meg, hogy mely objektumok szerint a listanézetet jelennek meg.

- A [SelectionSetName](./selectionsetname-element-for-viewselectedby-format.md) elem azt határozza meg a nézetben megjelenített objektumok közül. Meg kell adnia legalább egy készlet kiválasztása vagy a nézet típusa, de nincs nem adható meg elemek maximális számát.

Az alábbi példa bemutatja, hogyan adhat meg az objektumok egy adott lista nézet használatával definíciója szerint jelenik meg a [EntrySelectedBy](./entryselectedby-element-for-listentry-for-listcontrol-format.md) elemet. Ez az elem használatával, megadhatja az objektum, objektumok kiválasztása csoportja, vagy egy kiválasztási feltétel, amely meghatározza a definíció használatakor .NET nevét. A kiválasztási feltételek létrehozásával kapcsolatos további információkért lásd: [feltételek meghatározása az adatok megjelenítése](./defining-conditions-for-displaying-data.md).

```xml
<ListEntry>
  <EntrySelectedBy>
    <TypeName>.NET Type</TypeName>
  </EntrySelectedBy>
</ListEntry>
```

A következő XML-elemeket adja meg az objektumokat a listanézet adott definíciójának által használt használható:

- A [EntrySelectedBy](./entryselectedby-element-for-listentry-for-listcontrol-format.md) elem határozza meg, hogy mely objektumok jelennek meg a definíció szerint.

- A [TypeName](./typename-element-for-entryselectedby-for-listcontrol-format.md) elem azt határozza meg a .NET-objektum, amely a definíció szerint jelenik meg. Ez az elem használatakor a teljes .NET típusú név megadása kötelező. Meg kell adnia legalább egy típus, kijelölés set vagy kijelölés feltételt a definíciójában, de nincs nem adható meg elemek maximális számát.

- A [SelectionSetName](./selectionsetname-element-for-entryselectedby-for-listcontrol-format.md) (nem látható) elemet, adja meg a definíció megjelenített objektumok közül. Meg kell adnia legalább egy típus, kijelölés set vagy kijelölés feltételt a definíciójában, de nincs nem adható meg elemek maximális számát.

- A [SelectionCondition](./selectioncondition-element-for-entryselectedby-for-listcontrol-format.md) (nem látható) elemet, adja meg egy feltételt, amely a definíció használandó léteznie kell. Meg kell adnia legalább egy típus, kijelölés set vagy kijelölés feltételt a definíciójában, de nincs nem adható meg elemek maximális számát. További információ a kiválasztási feltételek meghatározása: [feltételek meghatározása az adatok megjelenítése](./defining-conditions-for-displaying-data.md).

## <a name="displaying-groups-of-objects-in-a-list-view"></a>Lista nézetben a csoportok objektumok megjelenítése

Elkülönítheti az objektumokat, amely szerint a lista nézet csoportokba jelennek meg. Ez nem jelenti azt, hogy Ön meghatározott felhasználói csoporttal, csak a Windows PowerShell elindul egy új csoportot, ha az érték egy adott tulajdonságra vagy egy parancsprogramtípusra. A következő példában elindul egy új csoportot, amikor az értékét a [System.Serviceprocess.Servicecontroller.Servicetype](/dotnet/api/System.ServiceProcess.ServiceController.ServiceType) tulajdonságukat módosítják.

```xml
<GroupBy>
  <Label>Service Type</Label>
  <PropertyName>ServiceType</PropertyName>
</GroupBy>

```

A következő XML-elemeket segítségével határozhatók meg, amikor egy csoportot:

- A [GroupBy](./groupby-element-for-view-format.md) elem definiálja a tulajdonságot vagy parancsfájlt, amely elindítja az új csoporthoz, és határozza meg, hogyan jelenjen meg a csoport.

- A [PropertyName](./propertyname-element-for-groupby-format.md) elem azt határozza meg a tulajdonság, amely elindítja egy új csoportot, amikor annak értéke módosul. Adjon meg egy tulajdonságot vagy a parancsfájl a csoport indítása, de mindkettő megadására nincs lehetőség.

- A [ScriptBlock](./scriptblock-element-for-groupby-format.md) elem azt határozza meg, a parancsfájl, amely elindítja egy új csoportot, amikor annak értéke módosul. Meg kell adnia egy parancsfájl vagy a csoport indítása tulajdonság azonban mindkettő megadására nincs lehetőség.

- A [címke](./label-element-for-groupby-format.md) elemet definiál egy címke, amely az egyes csoportok elején jelenik meg. Ez az elem által meghatározott a szöveg mellett Windows PowerShell, amely az új csoport által aktivált, és hozzáad egy üres sort, előtt és után a felirat értékét jeleníti meg. Ez az elem nem kötelező.

- A [CustomControl](./customcontrol-element-for-groupby-format.md) elem határozza meg olyan vezérlő, amely az adatok megjelenítésére szolgál. Ez az elem nem kötelező.

- A [CustomControlName](./customcontrolname-element-for-groupby-format.md) elem azt határozza meg, egy közös vagy megtekintheti a vezérlő, amely az adatok megjelenítésére szolgál. Ez az elem nem kötelező.

Egy teljes formázási fájl, amely meghatározza a csoportok egy példa: [listanézet (GroupBy)](./list-view-groupby.md).

## <a name="using-format-strings"></a>Formázási karakterláncokat használatával

A nézet még jobban meghatározhatja, hogyan jelenjen meg az adatok formázási karakterláncokat is hozzáadhatók. Az alábbi példa bemutatja, hogyan definiáljon értékét formázási karakterláncot a `StartTime` tulajdonság.

```xml
<ListItem>
  <PropertyName>StartTime</PropertyName>
  <FormatString>{0:MMM} (0:DD) (0:HH):(0:MM)</FormatString>
</ListItem>
```

A következő XML-elemeket segítségével adjon meg egy Formátumminta:

- A [ListItem](./listitem-element-for-listitems-for-listcontrol-format.md) elem azt határozza meg a nézet által megjelenített adatokat.

- A [PropertyName](./propertyname-element-for-listitem-for-listcontrol-format.md) elem azt határozza meg a tulajdonságot, amelynek értéke megjelenik a nézet által. Adjon meg egy tulajdonságot vagy a parancsfájl azonban mindkettő megadására nincs lehetőség.

- A [FormatString](./formatstring-element-for-listitem-for-listcontrol-format.md) elem meghatározza formátumú mintát, amely meghatározza, hogy a tulajdonság vagy parancsfájl érték hogyan jelenjen meg a nézetben.

- A [ScriptBlock](./scriptblock-element-for-listitem-for-listcontrol-format.md) elem (nem látható) megadja a parancsprogramot, amelynek értéke megjelenik a nézet által. Meg kell adnia egy parancsfájl vagy a tulajdonságot azonban mindkettő megadására nincs lehetőség.

A következő példában a `ToString` módszert hívja meg a parancsfájl értékének. Parancsprogramok segítségével meghívhatja a bármely metódusát meghívná, egy objektumot. Ezért ha egy objektum tartozik egy módszer, például `ToString`, van formázási paramétereket, a parancsfájl segítségével meghívhatja a módszer a parancsfájl kimenete értékének.

```xml
<ListItem>
  <ScriptBlock>
    [String}::Format("(0,10) (1,8)", .LastWriteTime.ToString("d"),
    $_.LastWriteTime.Totring("t"))
  </ScriptBlock>
</ListItem>
```

A következő XML-elem segítségével hívása a `ToString` módszer:

- A [ListItem](./listitem-element-for-listitems-for-listcontrol-format.md) elem azt határozza meg a nézet által megjelenített adatokat.

- A [ScriptBlock](./scriptblock-element-for-listitem-for-listcontrol-format.md) elem (nem látható) megadja a parancsprogramot, amelynek értéke megjelenik a nézet által. Meg kell adnia egy parancsfájl vagy a tulajdonságot azonban mindkettő megadására nincs lehetőség.

## <a name="see-also"></a>Lásd még:

[Egy Windows PowerShell-parancsmag írása](../cmdlet/writing-a-windows-powershell-cmdlet.md)
