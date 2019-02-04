---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: WMF, powershell, beállítás
title: Hibajavításokat tartalmaz a WMF 5.1
ms.openlocfilehash: d2cf44753a7cb54897e76cf914a8fef0f4aecf1e
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55684149"
---
# <a name="bug-fixes-in-wmf-51"></a>Hibajavításokat tartalmaz a WMF 5.1-es #

## <a name="bug-fixes"></a>Hibajavítások ##

A következő jelentős programhibákat a WMF 5.1:

### <a name="module-auto-discovery-fully-honors-envpsmodulepath"></a>Teljes körűen figyelembe veszi az automatikus felderítési modul `$env:PSModulePath` ###

A modul automatikus felderítési (betöltése modulok automatikusan, egy explicit Import-Module-parancs meghívásakor nélkül) a WMF 3 jelent meg.
Vezetett be, amikor PowerShell ellenőrzi a parancsok `$PSHome\Modules` használata előtt `$env:PSModulePath`.

A WMF 5.1 módosítja ezt a viselkedést, hogy tartsa tiszteletben `$env:PSModulePath` teljesen.
Ez lehetővé teszi egy felhasználó által létrehozott modul, amely meghatározza a PowerShell által biztosított parancsok (pl. `Get-ChildItem`) automatikus – betöltését és a beépített parancsa megfelelően felülírása.

### <a name="file-redirection-no-longer-hard-codes--encoding-unicode"></a>Átirányítási fájlt nem hosszabb rögzített kódok `-Encoding Unicode` ###

PowerShell korábbi verzióiban lehetetlen szabályozhatja, hogy a fájl kódolása például a fájl átirányítás operátor által használt volt `Get-ChildItem > out.txt` mert PowerShell hozzáadott `-Encoding Unicode`.

A WMF 5.1-es verziótól kezdődően most módosíthatja a fájl kódolása átirányítás beállításával `$PSDefaultParameterValues`:

```
$PSDefaultParameterValues["Out-File:Encoding"] = "Ascii"
```

### <a name="fixed-a-regression-in-accessing-members-of-systemreflectiontypeinfo"></a>Rögzített elérése során tagjai regresszió `System.Reflection.TypeInfo` ###

A WMF 5.0 rendszerben bevezetett regresszió érvénytelenítése elérésére tagjai `System.Reflection.RuntimeType`, pl. `[int].ImplementedInterfaces`.
Ezt a hibát a WMF 5.1 megoldották.


### <a name="fixed-some-issues-with-com-objects"></a>Bizonyos problémák rögzített COM-objektumok ###

A WMF 5.0 bevezetett egy új COM vyvolání metody COM-objektumok és COM-objektumok elérésére tulajdonságait a Binder létrehozása.
Az új binder jelentősen javult a teljesítmény, de bizonyos hibák, amelyek kijavítása megtörtént a WMF 5.1 is bevezetett.

#### <a name="argument-conversions-were-not-always-performed-correctly"></a>Argumentum-átalakítás nem lettek mindig végrehajtva megfelelően ####

Az alábbi példában:

```
$obj = New-Object -ComObject WScript.Shell
$obj.SendKeys([char]173)
```

A SendKeys metódus karakterláncot vár, de a PowerShell nem konvertálható a char egy karakterlánc IDispatch::Invoke, amely VariantChangeType használnak az átalakítást, amely ebben a példában az "1", "7" és "3" kulcsok küldése inkább eredményezett való átalakítás elhalasztása a várt Volume.Mute kulcs.

#### <a name="enumerable-com-objects-not-always-handled-correctly"></a>COM-objektumok enumerálható nem mindig kezelése ####

PowerShell általában a legtöbb enumerálható objektumok enumerálása, de a WMF 5.0 rendszerben bevezetett regresszió miatt nem sikerült a valósítania az IEnumerable illesztőfelületet COM-objektumok enumerálása.  Például:

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

A fenti példában a WMF 5.0 helytelenül írt a Scripting.Dictionary számbavétele a kulcs/érték párok helyett a folyamat számára.

Ez a módosítás is címek [ki 1752224 a Connect webhelyen](https://connect.microsoft.com/PowerShell/feedback/details/1752224)

### <a name="ordered-was-not-allowed-inside-classes"></a>`[ordered]` nem volt engedélyezett osztályok ###

A WMF 5.0 osztályokat az osztályok a használt típusú literálok érvényesítése vezetett be.
`[ordered]` néz ki egy típusú konstans azonban nem igaz typ .NET.
A WMF 5.0 helytelenül jelentett hiba `[ordered]` osztály belül:

```
class CThing
{
    [object] foo($i)
    {
        [ordered]@{ Thing = $i }
    }
}
```


### <a name="help-on-about-topics-with-multiple-versions-does-not-work"></a>Súgó a többféle verzióját tartalmazó témakörök nem működik. ###

A WMF 5.1-es, ha már telepített modulokban több verzióját, és azok minden megosztott súgótémakör, például about_PSReadline, mielőtt `help about_PSReadline` több témakörök a megfelelő módszer a valódi súgójának megtekintéséhez adna vissza.

A WMF 5.1 javítja, ez visszaadó súgóját, a legújabb verzióra, a következő témakörben.

`Get-Help` nem biztosít annak meghatározására, hogy melyik verziót szeretné súgóját.
Ennek megoldásához keresse meg a modulok könyvtárát, és közvetlenül a olyan eszköz, például a kedvenc szerkesztőjében súgójának megtekintéséhez.

### <a name="powershellexe-reading-from-stdin-stopped-working"></a>a PowerShell.exe STDIN olvasásakor leállt

Az ügyfelek `powershell -command -` PowerShell végrehajtásához natív alkalmazásaitól a szkriptben Sajnos ez lett osztva más változtatások miatt STDIN keresztül adná azt át a konzol-gazdakörnyezethez.

https://windowsserver.uservoice.com/forums/301869-powershell/suggestions/15854689-powershell-exe-command-is-broken-on-windows-10

### <a name="powershellexe-creates-spike-in-cpu-usage-on-startup"></a>PowerShell.exe megnövekedett processzorhasználat az indítási hoz létre

PowerShell egy WMI-lekérdezést használja annak ellenőrzéséhez, hogy a késleltetést okoz a bejelentkezési elkerülése érdekében a csoportházirend segítségével lett elindítva.
A WMI-lekérdezést is említi tzres.mui.dll injektálásra összes folyamat, a rendszer, mivel a WMI Win32_Process osztály próbál lekérni a helyi időzóna adatait.
Ennek eredményeképpen a nagy CPU megnövekedett wmiprvse (a WMI szolgáltató gazda).
Javítsa ki, hogy ugyanazokat az információkat a WMI használata helyett Win32 API-hívás használatával.
