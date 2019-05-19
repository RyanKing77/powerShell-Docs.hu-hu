---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: WMF, powershell, beállítás
title: Hibajavításokat tartalmaz a WMF 5.1
ms.openlocfilehash: 8edf295eb6304dc04de2fa5d3792b1c2fc4b01f3
ms.sourcegitcommit: 01b81317029b28dd9b61d167045fd31f1ec7bc06
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/17/2019
ms.locfileid: "65856209"
---
# <a name="bug-fixes-in-wmf-51"></a>Hibajavításokat tartalmaz a WMF 5.1

## <a name="bug-fixes"></a>Hibajavítások

A következő jelentős programhibákat a WMF 5.1:

### <a name="module-auto-discovery-fully-honors-psmodulepath"></a>A modul automatikus felderítési teljes figyelembe veszi a PSModulePath

A modul automatikus felderítési (betöltése modulok automatikusan, egy explicit Import-Module-parancs meghívásakor nélkül) a WMF 3 jelent meg. Vezetett be, amikor PowerShell ellenőrzi a parancsok `$PSHome\Modules` használata előtt `$env:PSModulePath`.

A WMF 5.1 módosítja ezt a viselkedést, hogy tartsa tiszteletben `$env:PSModulePath` teljesen. Ez lehetővé teszi egy felhasználó által létrehozott modul, amely meghatározza a PowerShell által biztosított parancsok (pl. `Get-ChildItem`) automatikus – betöltését és a beépített parancsa megfelelően felülírása.

### <a name="file-redirection-no-longer-hard-codes--encoding-unicode"></a>Átirányítási fájlt nem hosszabb rögzített kódokat-Unicode kódolással

PowerShell korábbi verzióiban lehetetlen szabályozhatja, hogy a fájl kódolása a fájl átirányítási operátor által használt volt.

A WMF 5.1-es verziótól kezdődően most módosíthatja a fájl kódolása átirányítás beállításával `$PSDefaultParameterValues`:

```powershell
$PSDefaultParameterValues["Out-File:Encoding"] = "Ascii"
```

### <a name="fixed-a-regression-in-accessing-members-of-systemreflectiontypeinfo"></a>Rögzített elérése során System.Reflection.TypeInfo tagjai regresszió

A WMF 5.0 rendszerben bevezetett regresszió érvénytelenítése elérésére tagjai `System.Reflection.RuntimeType`, például `[int].ImplementedInterfaces`. Ezt a hibát a WMF 5.1 megoldották.

### <a name="fixed-some-issues-with-com-objects"></a>Bizonyos problémák rögzített COM-objektumok

A WMF 5.0 bevezetett egy új COM vyvolání metody COM-objektumok és COM-objektumok elérésére tulajdonságait a Binder létrehozása. Az új binder jelentősen javult a teljesítmény, de bizonyos hibák, amelyek kijavítása megtörtént a WMF 5.1 is bevezetett.

#### <a name="argument-conversions-were-not-always-performed-correctly"></a>Argumentum-átalakítás nem lettek mindig végrehajtva megfelelően

Az alábbi példában:

```powershell
$obj = New-Object -ComObject WScript.Shell
$obj.SendKeys([char]173)
```

A **SendKeys** metódus karakterláncot vár, de a PowerShell nem konvertálható a char karakterláncnak, a konvertálás késleltetésének **IDispatch::Invoke**, mely használ **VariantChangeType**ehhez az átalakítást. Ebben a példában ez eredményezett a kulcsok "1", "7" és "3" helyett a várt küldése **Volume.Mute** kulcsot.

#### <a name="enumerable-com-objects-not-always-handled-correctly"></a>COM-objektumok enumerálható nem mindig kezelése

PowerShell általában a legtöbb enumerálható objektumok enumerálása, de a WMF 5.0 rendszerben bevezetett regresszió miatt nem sikerült a valósítania az IEnumerable illesztőfelületet COM-objektumok enumerálása. Például:

```powershell
function Get-COMDictionary
{
    $d = New-Object -ComObject Scripting.Dictionary
    $d.Add('a', 2)
    $d.Add('b', 2)
    return $d
}

$x = Get-COMDictionary
```

A fenti példában, nem megfelelően írta a WMF 5.0 a **Scripting.Dictionary** számbavétele a kulcs/érték párok helyett a folyamat számára.

### <a name="ordered-was-not-allowed-inside-classes"></a>[rendezett] osztályok belüli nem engedélyezett

A WMF 5.0 osztályokat az osztályok a használt típusú literálok érvényesítése vezetett be. `[ordered]` néz ki egy típusú konstans azonban nem igaz typ .NET. A WMF 5.0 helytelenül jelentett hiba `[ordered]` osztály belül:

```powershell
class CThing
{
    [object] foo($i)
    {
        [ordered]@{ Thing = $i }
    }
}
```

### <a name="help-on-about-topics-with-multiple-versions-does-not-work"></a>Súgó a többféle verzióját tartalmazó témakörök nem működik.

A WMF 5.1-es, ha már telepített modulokban több verzióját, és azok minden megosztott súgótémakör, például about_PSReadline, mielőtt `help about_PSReadline` több témakörök a megfelelő módszer a valódi súgójának megtekintéséhez adna vissza.

A WMF 5.1 javítja, ez visszaadó súgóját, a legújabb verzióra, a következő témakörben.

`Get-Help` nem biztosít annak meghatározására, hogy melyik verziót szeretné súgóját. Ennek megoldásához keresse meg a modulok könyvtárát, és közvetlenül a olyan eszköz, például a kedvenc szerkesztőjében súgójának megtekintéséhez.

### <a name="powershellexe-reading-from-stdin-stopped-working"></a>a PowerShell.exe STDIN olvasásakor leállt

Az ügyfelek `powershell -command -` PowerShell végrehajtásához natív alkalmazásaitól átadja a szkriptben keresztül STDIN Sajnos ez volt működésképtelenné egyéb módosítások a konzol-gazdakörnyezethez.

Ez a Windows 10 Évfordulós frissítés az 5.1-es verzió javítását.

### <a name="powershellexe-creates-spike-in-cpu-usage-on-startup"></a>PowerShell.exe megnövekedett processzorhasználat az indítási hoz létre

PowerShell egy WMI-lekérdezést használja annak ellenőrzéséhez, hogy a késleltetést okoz a bejelentkezési elkerülése érdekében a csoportházirend segítségével lett elindítva. A WMI-lekérdezést is említi a rendszer minden egyes folyamat óta a WMI tzres.mui.dll injektálásra **Win32_Process** osztály próbál lekérni a helyi időzóna adatait. Ennek hatására a nagy CPU ugrásszerű **wmiprvse** (a WMI szolgáltató gazda). Javítsa ki, hogy ugyanazokat az információkat a WMI használata helyett Win32 API-hívás használatával.
