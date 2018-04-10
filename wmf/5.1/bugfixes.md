---
ms.date: 06/12/2017
author: JKeithB
ms.topic: reference
keywords: WMF, powershell, beállítás
title: A WMF 5.1 hibajavítások
ms.openlocfilehash: dfd9ead447edfe9b7bdae23be14785df4b182bbc
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="bug-fixes-in-wmf-51"></a>A WMF 5.1# hibajavítások

## <a name="bug-fixes"></a>Hibajavítások ##

A következő fontos hibákat WMF 5.1 Fix:

### <a name="module-auto-discovery-fully-honors-envpsmodulepath"></a>A modul automatikus felderítési teljesen eleget tegyen `$env:PSModulePath` ###

WMF 3 bevezetett modul automatikus felderítését (betöltése modulok automatikusan egy explicit Import-Module parancs meghívásakor nélkül).
Amikor jelenik meg, PowerShell-parancsok ellenőrzi `$PSHome\Modules` használata előtt `$env:PSModulePath`.

WMF 5.1 módosítja ezt a viselkedést tiszteletben `$env:PSModulePath` teljesen.
Ez lehetővé teszi, hogy egy felhasználó által létrehozott modul, amely meghatározza a PowerShell által biztosított parancsok (pl. `Get-ChildItem`) automatikus-betöltését és megfelelően felülírja a beépített parancsot.

### <a name="file-redirection-no-longer-hard-codes--encoding-unicode"></a>Átirányítás nem hosszabb paraméterekként fájl `-Encoding Unicode` ###

PowerShell korábbi verzióiban szabályozásához használja a fájl átirányító operátort, pl. kódolása lehetetlen volt `Get-ChildItem > out.txt` mivel adja meg a PowerShell `-Encoding Unicode`.

WMF 5.1 kezdve, módosíthatja a fájlkódolás átirányítás úgy, hogy `$PSDefaultParameterValues`:

```
$PSDefaultParameterValues["Out-File:Encoding"] = "Ascii"
```

### <a name="fixed-a-regression-in-accessing-members-of-systemreflectiontypeinfo"></a>Rögzített egy regressziós tagjai eléréséhez `System.Reflection.TypeInfo` ###

A WMF 5.0 rendszerben bevezetett regressziós túllépte elérése során tagjai `System.Reflection.RuntimeType`, pl. `[int].ImplementedInterfaces`.
Ez a hiba kijavítása WMF 5.1.


### <a name="fixed-some-issues-with-com-objects"></a>Bizonyos problémák rögzített COM-objektumok ###

WMF 5.0 rendszerben jelent meg egy új COM kötő hívása módszerek COM objektum és a COM-objektumok tulajdonságainak elérése során.
Az új kötő jelentősen növeli a teljesítményt, de is bevezetni az egyes hibák, amelyek WMF 5.1 rögzített.

#### <a name="argument-conversions-were-not-always-performed-correctly"></a>Argumentum átalakítások nem mindig elvégzett megfelelően ####

A következő példa:

```
$obj = New-Object -ComObject WScript.Shell
$obj.SendKeys([char]173)
```

A SendKeys metódus karakterláncot vár, de a PowerShell nem konvertálható a char, karakterlánc késleltető IDispatch::Invoke, amely VariantChangeType használja az átalakítás, amely ebben a példában a kulcsokat, "1", "7" és "3" helyett küldése átalakítása a várt Volume.Mute kulcs.

#### <a name="enumerable-com-objects-not-always-handled-correctly"></a>Enumerálható COM-objektumok nem mindig megfelelő kezelése ####

PowerShell általában a legtöbb enumerálható objektum enumerálása, de a WMF 5.0 rendszerben bevezetett regressziós miatt nem sikerült az IEnumerable illesztőfelületet megvalósító COM-objektumok számbavétele.  Például:

```
function Get-COMDictionary
{
    $d = New-Object -ComObject Scripting.Dictionary
    $d.Add('a', 2)
    $d.Add('b', 2)
    return $d
}

$x = Get-COMDictionary
```

A fenti példában WMF 5.0 nem megfelelően megírt a Scripting.Dictionary az adatcsatornához helyett a kulcs/érték párok enumerálása.

Ez is módosítja címek [adja ki a Connect 1752224](https://connect.microsoft.com/PowerShell/feedback/details/1752224)

### <a name="ordered-was-not-allowed-inside-classes"></a>`[ordered]` nem volt engedélyezett osztályok ###

WMF 5.0 rendszerben jelent meg osztályok osztályok használt típus szövegkonstans-érvényesítéssel.
`[ordered]` a következőképpen néz típusú szövegkonstansnak, de nincs true .NET-típus.
WMF 5.0 helytelenül jelentett hiba `[ordered]` osztály belül:

```
class CThing
{
    [object] foo($i)
    {
        [ordered]@{ Thing = $i }
    }
}
```


### <a name="help-on-about-topics-with-multiple-versions-does-not-work"></a>A használatára vonatkozó súgó megjelenítéséhez többféle verzióját tartalmazó témakörök nem működik. ###

WMF 5.1, ha volt a telepített modulokban különböző verzióinak és állnak az adott témakör, például megosztott about_PSReadline, mielőtt `help about_PSReadline` meghaladná a megfelelő módszer valós súgójának megtekintéséhez több témakör.

WMF 5.1 Ez javítja, vissza a Súgó gombra a témakör a legújabb verzióját.

`Get-Help` nem biztosít annak meghatározására, hogy melyik verzió a súgóját meg szeretné tekinteni.
Ez elkerülhető, keresse meg a modulok könyvtárát, és tekintse át a közvetlenül az egy eszköz, például a kedvenc szerkesztő súgóját.

### <a name="powershellexe-reading-from-stdin-stopped-working"></a>a STDIN olvasásakor PowerShell.exe leállt

Az ügyfelek `powershell -command -` a PowerShell végrehajtása natív alkalmazás való átadása a parancsfájlban szereplő keresztül STDIN Sajnos ez volt miatt hibás más jellegű módosítását a konzol állomás.

https://windowsserver.uservoice.com/forums/301869-powershell/suggestions/15854689-powershell-exe-command-is-broken-on-windows-10

### <a name="powershellexe-creates-spike-in-cpu-usage-on-startup"></a>PowerShell.exe csúcs a CPU-használat indításakor hoz létre.

PowerShell WMI-lekérdezés segítségével ellenőrizze, hogy a késleltetést okoz a bejelentkezési elkerülése érdekében a csoportházirend segítségével indítása.
A WMI-lekérdezést említi tzres.mui.dll beszúrva a rendszer minden folyamatba, mivel a WMI Win32_Process osztály megpróbálja beolvasni a helyi időzóna adatait.
Ennek eredményeképp a nagy CPU-csúcs az igények wmiprvse (a WMI szolgáltató fogadó).
Javítsa ki, hogy Win32 API-hívások használja ugyanazokat az információkat a WMI használata helyett.