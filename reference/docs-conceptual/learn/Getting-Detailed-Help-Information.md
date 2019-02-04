---
ms.date: 08/27/2018
keywords: PowerShell, a parancsmag
title: Részletes súgóinformációk kérése
ms.assetid: 6fb4daf7-8607-4a3e-b692-f77631adc1b9
ms.openlocfilehash: 8b56f003fdef38b0f126cfe82eefcc145cc54783
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55684086"
---
# <a name="getting-detailed-help-information"></a>Részletes súgóinformációk kérése

PowerShell, amelyek bemutatják a PowerShell alapfogalmai és a PowerShell nyelv részletes cikkeket tartalmaz. Is találhatók Súgócikkek minden parancsmag és a szolgáltató, és számos függvények és parancsfájlok.

Ezek Súgócikkek jeleníthetők meg a parancssort vagy a legutóbb frissített verzióit a következő cikkeket megtekintése a [PowerShell](/powershell/scripting/overview) online dokumentációját.

## <a name="getting-help-for-cmdlets"></a>Súgó a parancsmagokhoz

PowerShell-parancsmagokkal kapcsolatos súgó lekéréséhez használja a [Get-Help](/powershell/module/microsoft.powershell.core/Get-Help) parancsmagot. Segítség kérése az a példában a `Get-ChildItem` parancsmagot, írja be:

```powershell
Get-Help Get-ChildItem
```

vagy a

```powershell
Get-ChildItem -?
```

A Get-Help parancsmag kapcsolatos még is kaphat segítséget. Például:

```powershell
Get-Help Get-Help
```

Súgócikkek az összes parancsmag listájának lekérése a munkamenetben, írja be:

```powershell
Get-Help -Category Cmdlet
```

Egyszerre csak egy oldal egyes súgócikk megjelenítéséhez használja a `help` függvény vagy az aliasával `man`.
Például Súgó megjelenítése a `Get-ChildItem` parancsmag típusa

```powershell
man Get-ChildItem
```

vagy a

```powershell
help Get-ChildItem
```

Részletes információk megjelenítéséhez használja a **részletes** paraméterében a `Get-Help` parancsmagot. Például részletes információkhoz juthat a `Get-ChildItem` parancsmagot, írja be:

```powershell
Get-Help Get-ChildItem -Detailed
```

A Súgó a cikkben minden tartalom megjelenítéséhez használja a **teljes** paraméterében a `Get-Help` parancsmagot. Ha például minden tartalom megjelenítéséhez a cikk segítséget a `Get-ChildItem` parancsmagot, írja be:

```powershell
Get-Help Get-ChildItem -Full
```

Első részletes súgó használatát egy parancsmag-paraméterekkel kapcsolatos a **paraméter** paraméterében a `Get-Help` parancsmagot. Például beolvasni a részletes súgót paramétereit a `Get-ChildItem` parancsmagot, írja be:

```powershell
Get-Help Get-ChildItem -Parameter *
```

A példákban csak a Súgó a cikkben megjelenítéséhez használja a **példák** paraméterében a `Get-Help`.
Ha például csak a példák megjelenítése a Súgó cikk a `Get-ChildItem `parancsmagot, írja be:

```powershell
Get-Help Get-ChildItem -Examples
```

Súgócikkek az írást parancsmagok írásával kapcsolatban további információkért lásd: [arról, hogy miként írhat parancsmag](/powershell/developer/help/writing-help-for-windows-powershell-cmdlets).

## <a name="getting-conceptual-help"></a>Fogalmi segítség kérése

A `Get-Help` parancsmag is információkat jelenít meg elméleti cikkek PowerShell-lel, beleértve a cikkeket a PowerShell nyelv tudnivalók. Cikkek kezdje a "about_" előtaggal, például a about_line_editing fogalmi segítséget. (A fogalmi cikkeinek kell megadni angol nyelven még a PowerShell nem angol nyelvű verziója.)

Elméleti cikkek listájának megjelenítéséhez írja be:

```powershell
Get-Help about_*
```

Egy adott súgócikk megjelenítéséhez írja be például a cikk neve:

```powershell
Get-Help about_command_syntax
```

A paraméterek a `Get-Help`, például **részletes**, **paraméter**, és **példák**, nem befolyásolják a fogalmi Súgócikkek megjelenítését.

## <a name="getting-help-about-providers"></a>Szolgáltatók kapcsolatos segítség

A `Get-Help` parancsmag PowerShell szolgáltatók információit jeleníti meg. Súgó kérése egy szolgáltatót, írja be a `Get-Help` szolgáltató neve követ. Például a beállításjegyzék-szolgáltatójának súgójának megjelenítéséhez írja be:

```powershell
Get-Help registry
```

Súgócikkek az összes szolgáltatót listájának lekérése a munkamenetben, írja be a következőt

```powershell
Get-Help -Category provider
```

A paraméterek a `Get-Help`, például **részletes**, **paraméter**, és **példák**, nem befolyásolják a szolgáltató Súgócikkek megjelenítését.

## <a name="getting-help-about-scripts-and-functions"></a>Parancsfájlokban és függvényekben kapcsolatos segítség

Számos parancsfájlokban és függvényekben a PowerShellben kell a cikkeket. Használja a `Get-Help` parancsmaggal a Súgócikkek a parancsfájlokban és függvényekben.

A függvény súgójának megjelenítéséhez írja be a következőt `Get-Help` függvény neve követ. Segítség kérése az a példában a `Disable-PSRemoting` működik, írja be:

```powershell
Get-Help Disable-PSRemoting
```

A parancsfájl súgójának megjelenítéséhez írja be a parancsfájl elérési útját. Ha a parancsfájl nem szerepelnek a Path környezeti változóhoz elérési út, teljes elérési útját kell használnia.

Ha például a c: "TestScript.ps1" nevű parancsfájl rendelkezik\\PS-tesztelési címtárat, megjelenítése a Súgó a cikk a parancsfájl típusa:

```powershell
Get-Help c:\ps-test\TestScript.ps1
```

A paraméterek, a parancsmag súgójában működik a parancsfájl és a függvény értékek megjelenítésére lettek kialakítva segítségével túl. Azonban súgó a függvények és parancsfájlok nem látható futtatásakor `Get-Help *`.

Súgócikkek a függvények és parancsfájlok írása kapcsolatos információkért tekintse meg a következő cikkeket:

- [about_Functions](/powershell/module/microsoft.powershell.core/about/about_functions)
- [about_Scripts](/powershell/module/microsoft.powershell.core/about/about_scripts)
- [about_Comment_Based_Help](/powershell/module/microsoft.powershell.core/about/about_comment_based_help)

## <a name="getting-help-online"></a>Online súgó elérése

Online súgó cikkeinek az egyik legjobb módja, ha segítséget szeretne kérni. Online témájú cikkei például könnyebben frissítése, és adja meg a legfrissebb tartalmakat.

Online súgó lekéréséhez használja a **Online** paraméterében a `Get-Help` parancsmagot. A PowerShell-lel, beleértve a szolgáltató súgó származnak az összes Súgócikkek fogalmi (:), a cikkeket, és érhetők el online a [PowerShell](/powershell/scripting/powershell-scripting) dokumentációját.

> [!NOTE]
> Nem használhatja a **Online** fogalmi paraméterrel (about_\*) vagy a szolgáltató a cikkeket.
> Online súgó nem kötelező, így minden parancsmag, függvény vagy parancsfájl nem működik.

Például a súgócikk online verziójának beszerzéséhez a a `Get-ChildItem` parancsmagot, írja be:

```powershell
Get-Help Get-ChildItem -Online
```

PowerShell a cikk az alapértelmezett böngészőben nyílik meg. Online súgó egy súgócikk támogatott, ha az URL-címét a súgócikk is megtekintheti. Az URL-cím egy súgócikk kapcsolódó hivatkozások szakaszában jelenik meg.

Például az URL-cím, az Add-Computer parancsmag online verziójának megtekintéséhez írja be:

```powershell
Get-Help Add-Computer
```

A cikk a kapcsolódó hivatkozások szakasz első sorában az alábbiakban látható.

```Output
Online version: http://go.microsoft.com/fwlink/?LinkId=821564
```

Online-támogatást nyújt a Súgócikkek kapcsolatos információkért lásd: [about_Comment_Based_Help](/powershell/module/microsoft.powershell.core/about/about_comment_based_help).

## <a name="see-also"></a>Lásd még:

- [about_Functions](/powershell/module/microsoft.powershell.core/about/about_functions)
- [about_Scripts](/powershell/module/microsoft.powershell.core/about/about_scripts)
- [about_Comment_Based_Help](/powershell/module/microsoft.powershell.core/about/about_comment_based_help)
- [Get-Help](/powershell/module/microsoft.powershell.core/get-help)
