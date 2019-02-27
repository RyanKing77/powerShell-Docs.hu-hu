---
title: Széles körű nézetek létrehozásával |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 2d4303c5-b451-4ccb-9831-b17a17ceac20
caps.latest.revision: 16
ms.openlocfilehash: 651de5d3bc2619f20438f3951ac5a8c4b0bf46d4
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56848558"
---
# <a name="creating-a-wide-view"></a>Széles nézet létrehozása

Egy széles nézetben minden objektum megjelenített egyetlen értéket jeleníti meg. A megjelenített érték lehet egy .NET-objektum tulajdonságának értéke vagy egy parancsfájl értékét. Alapértelmezés szerint nincs címke vagy fejléc ehhez a nézethez.

## <a name="a-wide-view-display"></a>Egy széles nézet megjelenítése

Az alábbi példa bemutatja, hogyan jelenítse meg a Windows PowerShell a [System.Diagnostics.Process](/dotnet/api/System.Diagnostics.Process) által visszaadott objektum a [Get-Process](/powershell/module/Microsoft.PowerShell.Management/Get-Process) parancsmagot, ha a kimenetet eredményez a [ Formátum kiterjedő](/powershell/module/Microsoft.PowerShell.Utility/Format-Wide) parancsmagot. (Alapértelmezés szerint a [Get-Process](/powershell/module/Microsoft.PowerShell.Management/Get-Process) parancsmag adja vissza egy táblázat nézet.) Ebben a példában a két oszlop segítségével a folyamat minden visszaadott objektum neve jelenik meg. Az objektum tulajdonság neve nem jelenik meg, csak a tulajdonság értékét.

```
Get-Process | format-wide
AEADISRV                     agrsmsvc
Ati2evxx                     Ati2evxx
audiodg                      CCC
CcmExec                      communicator
Crypserv                     csrss
csrss                        DevDtct2
DM1Service                   dpupdchk
dwm                          DxStudio
EXCEL                        explorer
GoogleToolbarNotifier        GrooveMonitor
hpqwmiex                     hpservice
Idle                         InoRpc
InoRT                        InoTask
ipoint                       lsass
lsm                          MOM
MSASCui                      notepad
...                          ...

```

## <a name="defining-the-wide-view"></a>A széles nézet definiálása

A következő XML formátumú széles nézet sémáját jeleníti meg a [System.Diagnostics.Process](/dotnet/api/System.Diagnostics.Process) objektum.

```xml
View>
  <Name>process</Name>
  <ViewSelectedBy>
    <TypeName>System.Diagnostics.Process</TypeName>
  </ViewSelectedBy>
  <GroupBy>...</GroupBy>
  <Controls>...</Controls>
  <WideControl>
    <WideEntries>
      <WideEntry>
        <WideItem>
          <PropertyName>ProcessName</PropertyName>
        </WideItem>
      </WideEntry>
    </WideEntries>
  </WideControl>
</View>

```

A következő XML-elemeket egy széles nézet meghatározásához használják:

- A [nézet](./view-element-format.md) elem a szülőelemet, a széles nézet. (Ez a táblázat, lista, és egyéni vezérlő nézetek az ugyanazon szülőelem.)

- A [neve](./name-element-for-view-format.md) elem azt határozza meg a nézet nevét. Ehhez az elemhez kötelező megadni az összes nézetben megtekinthetők.

- A [ViewSelectedBy](./viewselectedby-element-format.md) elem definiálja az objektumok, amelyek a nézetet. Ez az elem megadása kötelező.

- A [GroupBy](./groupby-element-for-view-format.md) elem határozza meg, ha az objektumok egy új csoport megjelenik. Egy új csoportot, ha az érték egy adott tulajdonságra vagy parancsfájl el van indítva. Ez az elem nem kötelező.

- A [vezérlők](./controls-element-for-view-format.md) elemek határozza meg az egyéni vezérlők, a széles nézet által meghatározott. Vezérlők további adja meg, hogyan jelenjen meg az adatokat egy módot biztosít. Ez az elem nem kötelező. Nézet definiálhat a saját egyéni vezérlők, vagy telepítheti a nézeten a formázási fájlban használt Gyakori vezérlők. Egyéni vezérlők kapcsolatos további információkért lásd: [egyéni vezérlők létrehozását](./creating-custom-controls.md).

- A [WideControl](./widecontrol-element-format.md) elem, és gyermekelemeinek határozza meg a nézetben jelenik meg. Az előző példában a nézet célja, hogy megjeleníti a [System.Diagnostics.Process.Processname](/dotnet/api/System.Diagnostics.Process.ProcessName) tulajdonság.

Egy példa egy teljes formázási fájl, amely meghatározza egy egyszerű széles nézet: [széles nézet (alapszintű)](./wide-view-basic.md).

## <a name="providing-definitions-for-your-wide-view"></a>Így a széles nézet definíciói

Széles körű nézetek biztosíthat egy vagy több definíciót alárendelt elemeinek használatával a [WideControl](./widecontrol-element-format.md) elemet. Nézet általában csak egyetlen definíciót fog rendelkezni. A következő példában a nézetet biztosít, amelyek értékét jeleníti meg egyetlen meghatározást az [System.Diagnostics.Process.Processname](/dotnet/api/System.Diagnostics.Process.ProcessName) tulajdonság. Egy széles nézet megjelenítheti egy tulajdonság értékét, vagy egy parancsfájl (a példában nem látható) értékét.

```xml
<WideControl>
  <AutoSize/>
  <ColumnNumber></ColumnNumber>
  <WideEntries>
    <WideEntry>
      <WideItem>
        <PropertyName>ProcessName</PropertyName>
      </WideItem>
    </WideEntry>
  </WideEntries>
</WideControl>
```

A következő XML-elemeket adjon meg egy széles nézet definíciói használható:

- A [WideControl](./widecontrol-element-format.md) elem, és gyermekelemeinek határozza meg a nézetben jelenik meg.

- A [AutoSize](./autosize-element-for-widecontrol-format.md) elem azt határozza meg, hogy az oszlop méretét és az oszlopok számát módosulnak az adatok mérete alapján. Ez az elem nem kötelező.

- A [ColumnNumber](./columnnumber-element-for-widecontrol-format.md) elem azt határozza meg, a széles nézetben megjelenített oszlopok számát. Ez az elem nem kötelező.

- A [WideEntries](./wideentries-element-for-widecontrol-format.md) elem a nézet a definíciókat tartalmazza. A legtöbb esetben a nézet csak egyetlen definíciót fog rendelkezni. Ez az elem megadása kötelező.

- A [WideEntry](./wideentry-element-for-widecontrol-format.md) elem biztosít a nézet definíciójának. Legalább egy [WideEntry](./wideentry-element-for-widecontrol-format.md) szükséges; azonban nem adhat hozzá elemek számának nincs maximális korlátot. A legtöbb esetben a nézet csak egyetlen definíciót fog rendelkezni.

- A [EntrySelectedBy](./entryselectedby-element-for-wideentry-format.md) elem azt határozza meg az objektumok, amelyek egy adott definíciója szerint jelennek meg. Ez az elem nem kötelező, és csak a több meghatározása során van szükség [WideEntry](./wideentry-element-for-widecontrol-format.md) elemek, amelyek a különböző objektumok megjelenítéséhez.

- A [WideItem](./wideitem-element-for-widecontrol-format.md) elem azt határozza meg a nézet által megjelenített adatokat. Nézetek más típusú szakembereket széles vezérlőelem megjelenítheti csak egy elemet.

- A [PropertyName](./propertyname-element-for-wideitem-for-widecontrol-format.md) elem azt határozza meg a tulajdonságot, amelynek értéke megjelenik a nézet által. Adjon meg egy tulajdonságot vagy a parancsfájl azonban mindkettő megadására nincs lehetőség.

- A [ScriptBlock](./scriptblock-element-for-wideitem-for-widecontrol-format.md) eleme megadja a parancsprogramot, amelynek értéke megjelenik a nézet által. Meg kell adnia egy parancsfájl vagy a tulajdonságot azonban mindkettő megadására nincs lehetőség.

- A [FormatString](./formatstring-element-for-wideitem-for-widecontrol-format.md) elem azt határozza meg olyan minta, amely az adatok megjelenítésére szolgál. Ez az elem nem kötelező.

Egy teljes formázási fájl, amely meghatározza egy széles nézet definícióját egy példa: [széles nézet (alapszintű)](./wide-view-basic.md).

## <a name="defining-the-objects-that-use-the-wide-view"></a>Az objektumok, amelyek a számos nézet definiálása

Két módon határozza meg, mely a .NET-objektumokká széles nézet használata. Használhatja a [ViewSelectedBy](./viewselectedby-element-format.md) elem jeleníthető meg úgy a nézetet, vagy a definíciókat objektumok használhatja a [EntrySelectedBy](./entryselectedby-element-for-wideentry-format.md) elem határozza meg, hogy mely objektumok szerint jelennek meg a a nézet adott meghatározása. A legtöbb esetben a nézet csak egyetlen definíciót, rendelkezik, ezért általában által meghatározott objektumok a [ViewSelectedBy](./viewselectedby-element-format.md) elemet.

Az alábbi példa bemutatja, hogyan használatával széles nézetben megjelenített objektumok a [ViewSelectedBy](./viewselectedby-element-format.md) és [TypeName](./typename-element-for-viewselectedby-format.md) elemeket. Nem korlátozott számú [TypeName](./typename-element-for-viewselectedby-format.md) elemeket, hogy is megadhat, és a sorrendjük nem lényeges.

```xml
<View>
  <Name>System.ServiceProcess.ServiceController</Name>
  <ViewSelectedBy>
    <TypeName>System.Diagnostics.Process</TypeName>
  </ViewSelectedBy>
  <WideControl>...</WideControl>
</View>
```

A következő XML-elemeket adja meg az objektumokat, a széles nézet által használt használható:

- A [ViewSelectedBy](./viewselectedby-element-format.md) elem határozza meg, hogy mely objektumok szerint a széles nézetben jelennek meg.

- A [TypeName](./typename-element-for-viewselectedby-format.md) elem azt határozza meg a .NET, amely szerint a nézet jelenik meg. A teljes .NET típusú név megadása kötelező. Meg kell adnia legalább egy típus vagy állítsa be a nézet a kijelölés, de nincs nem adható meg elemek maximális számát.

Egy teljes formázási fájl egy példa: [széles nézet (alapszintű)](./wide-view-basic.md).

Az alábbi példában a [ViewSelectedBy](./viewselectedby-element-format.md) és [SelectionSetName](./selectionsetname-element-for-viewselectedby-format.md) elemeket. Használja a kijelölt csoportok használatával több nézetet, például amikor egy széles nézet határozza meg, és a táblázatos nézetre a ugyanazon objektumok megjelenített objektumok kapcsolódó készlete esetében. Hozzon létre egy kiválasztási kapcsolatos további információkért lásd: [kijelölt csoportok meghatározása](./defining-selection-sets.md).

```xml
<View>
  <Name>System.ServiceProcess.ServiceController</Name>
  <ViewSelectedBy>
    <SelectionSetName>.NET Type Set</SelectionSetName>
  </ViewSelectedBy>
  <WideControl>...</WideControl>
</View>
```

A következő XML-elemeket adja meg az objektumokat, a széles nézet által használt használható:

- A [ViewSelectedBy](./viewselectedby-element-format.md) elem határozza meg, hogy mely objektumok szerint a széles nézetben jelennek meg.

- A [SelectionSetName](./selectionsetname-element-for-viewselectedby-format.md) elem azt határozza meg a nézetben megjelenített objektumok közül. Meg kell adnia legalább egy készlet kiválasztása vagy a nézet típusa, de nincs nem adható meg elemek maximális számát.

Az alábbi példa bemutatja, hogyan adhat meg az objektumokat, a széles nézet használatával egy adott definíciója szerint jelenik meg a [EntrySelectedBy](./entryselectedby-element-for-wideentry-format.md) elemet. Ez az elem használatával, megadhatja az objektum, objektumok kiválasztása csoportja, vagy egy kiválasztási feltétel, amely meghatározza a definíció használatakor .NET nevét. A kiválasztási feltételek létrehozásával kapcsolatos további információkért lásd: [feltételek meghatározása az adatok megjelenítése](./defining-conditions-for-displaying-data.md).

```xml
<WideEntry>
  <EntrySelectedBy>
    <TypeName>.NET Type</TypeName>
  </EntrySelectedBy>
</WideEntry>
```

A következő XML-elemeket adja meg az objektumokat, a széles nézet egy adott definíciója által használt használható:

- A [EntrySelectedBy](./entryselectedby-element-for-wideentry-format.md) elem határozza meg, hogy mely objektumok jelennek meg a definíció szerint.

- A [TypeName](./typename-element-for-viewselectedby-format.md) elem azt határozza meg a .NET, a definíció szerint jelenik meg. Ez az elem használatakor a teljes .NET típusú nevének megadása kötelező. Meg kell adnia legalább egy típus, kijelölés set vagy kijelölés feltételt a definíciójában, de nincs nem adható meg elemek maximális számát.

- A [SelectionSetName](./selectionsetname-element-for-viewselectedby-format.md) (nem látható) elemet, adja meg a definíció megjelenített objektumok közül. Meg kell adnia legalább egy típus, kijelölés set vagy kijelölés feltételt a definíciójában, de nincs nem adható meg elemek maximális számát.

- A [SelectionCondition](./selectioncondition-element-for-entryselectedby-for-widecontrol-format.md) (nem látható) elemet, adja meg egy feltételt, amely a definíció használandó léteznie kell. Meg kell adnia legalább egy típus, kijelölés set vagy kijelölés feltételt a definíciójában, de nincs nem adható meg elemek maximális számát. További információ a kiválasztási feltételek meghatározása: [feltételek meghatározása az adatok megjelenítése](./defining-conditions-for-displaying-data.md).

## <a name="displaying-groups-of-objects-in-a-wide-view"></a>Az objektumok csoportjaihoz széles nézet megjelenítése

Elkülönítheti az objektumokat, a széles körű képet kaphat csoportok szerint jelennek meg. Ez nem jelenti azt, hogy Ön meghatározott felhasználói csoporttal, csak a Windows PowerShell elindul egy új csoportot, ha az érték egy adott tulajdonságra vagy egy parancsprogramtípusra. A következő példában elindul egy új csoportot, amikor az értékét a [System.Serviceprocess.Servicecontroller.Servicetype](/dotnet/api/System.ServiceProcess.ServiceController.ServiceType) tulajdonságukat módosítják.

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

Egy teljes formázási fájl, amely meghatározza a csoportok egy példa: [széles nézet (GroupBy)](./wide-view-groupby.md).

## <a name="using-format-strings"></a>Formázási karakterláncokat használatával

Egy széles nézet még jobban meghatározhatja, hogyan jelenjen meg az adatok formázási karakterláncokat is hozzáadhatók. Az alábbi példa bemutatja, hogyan definiáljon értékét formázási karakterláncot a `StartTime` tulajdonság.

```xml
<WideItem>
  <PropertyName>StartTime</PropertyName>
  <FormatString>{0:MMM} (0:DD) (0:HH):(0:MM)</FormatString>
</WideItem>
```

A következő XML-elemeket segítségével adjon meg egy Formátumminta:

- A [WideItem](./wideitem-element-for-widecontrol-format.md) elem azt határozza meg a nézet által megjelenített adatokat.

- A [PropertyName](./propertyname-element-for-wideitem-for-widecontrol-format.md) elem azt határozza meg a tulajdonságot, amelynek értéke megjelenik a nézet által. Adjon meg egy tulajdonságot vagy a parancsfájl azonban mindkettő megadására nincs lehetőség.

- A [FormatString](./formatstring-element-for-wideitem-for-widecontrol-format.md) elem azt határozza meg, amely meghatározza, hogy a tulajdonság vagy parancsfájl érték hogyan jelenjen meg a nézetben egy Formátumminta

- A [ScriptBlock](./scriptblock-element-for-wideitem-for-widecontrol-format.md) elem (nem látható) megadja a parancsprogramot, amelynek értéke megjelenik a nézet által. Meg kell adnia egy parancsfájl vagy a tulajdonságot azonban mindkettő megadására nincs lehetőség.

A következő példában a `ToString` módszert hívja meg a parancsfájl értékének. Parancsprogramok segítségével meghívhatja a bármely metódusát meghívná, egy objektumot. Ezért ha egy objektum tartozik egy módszer, például `ToString`, van formázási paramétereket, a parancsfájl segítségével meghívhatja a módszer a parancsfájl kimenete értékének.

```xml
<WideItem>
  <ScriptBlock>
    [String}::Format("(0,10) (1,8)", .LastWriteTime.ToString("d"),
    $_.LastWriteTime.Totring("t"))
  </ScriptBlock>
</WideItem>
```

A következő XML-elem segítségével hívása a `ToString` módszer:

- A [WideItem](./wideitem-element-for-widecontrol-format.md) elem azt határozza meg a nézet által megjelenített adatokat.

- A [ScriptBlock](./scriptblock-element-for-wideitem-for-widecontrol-format.md) elem (nem látható) megadja a parancsprogramot, amelynek értéke megjelenik a nézet által. Meg kell adnia egy parancsfájl vagy a tulajdonságot azonban mindkettő megadására nincs lehetőség.

## <a name="see-also"></a>Lásd még:

[Széles nézet (alapszintű)](./wide-view-basic.md)

[Széles nézet (GroupBy)](./wide-view-groupby.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
