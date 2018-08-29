---
ms.date: 08/27/2018
keywords: PowerShell, a parancsmag
title: Parancsok kapcsolatos információk lekérése
ms.assetid: 56f8e5b4-d97c-4e59-abbe-bf13e464eb0d
ms.openlocfilehash: f4238927f10b4204cd3e23f0b0453011f54cb04a
ms.sourcegitcommit: 59727f71dc204785a1bcdedc02716d8340a77aeb
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/28/2018
ms.locfileid: "43134010"
---
# <a name="getting-information-about-commands"></a>Parancsok kapcsolatos információk lekérése

A PowerShell `Get-Command` jeleníti meg a parancsok, amelyek használhatók az aktuális munkamenetben.
Ha futtatja a `Get-Command` parancsmagot, tekintse meg a következő kimenethez hasonló:

```output
CommandType     Name                    Version    Source
-----------     ----                    -------    ------
Cmdlet          Add-Computer            3.1.0.0    Microsoft.PowerShell.Management
Cmdlet          Add-Content             3.1.0.0    Microsoft.PowerShell.Management
Cmdlet          Add-History             3.0.0.0    Microsoft.PowerShell.Core
Cmdlet          Add-JobTrigger          1.1.0.0    PSScheduledJob
Cmdlet          Add-LocalGroupMember    1.0.0.0    Microsoft.PowerShell.LocalAccounts
Cmdlet          Add-Member              3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Add-PSSnapin            3.0.0.0    Microsoft.PowerShell.Core
Cmdlet          Add-Type                3.1.0.0    Microsoft.PowerShell.Utility
...
```

A kimeneti keresi sokkal cmd.exe súgó példához hasonlóan: belső parancsok táblázatos összegzését. Az a kivonat a `Get-Command` a fent látható minden parancs kimenete tartalmaz egy parancsmag CommandType parancsot. Egy parancsmag PowerShell belső parancs típusa. Ez a típus nagyjából megfelel, mint `dir` és `cd` a Cmd.exe vagy a Unix beépített parancsok ismertetése, például a bash.

A `Get-Command` parancsmag rendelkezik egy **szintaxis** paraméter, amely egyes parancsmagok szintaxisát adja vissza. Az alábbi példa bemutatja, hogyan szintaxisának lekérése a `Get-Help` parancsmagot:

```powershell
Get-Command Get-Help -Syntax
```

```output
Get-Help [[-Name] <String>] [-Path <String>] [-Category <String[]>] [-Component <String[]>] [-Functionality <String[]>]
 [-Role <String[]>] [-Full] [-Online] [-Verbose] [-Debug] [-ErrorAction <ActionPreference>] [-WarningAction <ActionPreference>] [-ErrorVariable <String>] [-WarningVariable <String>] [-OutVariable <String>] [-OutBuffer <Int32>]

Get-Help [[-Name] <String>] [-Path <String>] [-Category <String[]>] [-Component <String[]>] [-Functionality <String[]>]
 [-Role <String[]>] [-Detailed] [-Online] [-Verbose] [-Debug] [-ErrorAction <ActionPreference>] [-WarningAction <ActionPreference>] [-ErrorVariable <String>] [-WarningVariable <String>] [-OutVariable <String>] [-OutBuffer <Int32>]

Get-Help [[-Name] <String>] [-Path <String>] [-Category <String[]>] [-Component <String[]>] [-Functionality <String[]>]
 [-Role <String[]>] [-Examples] [-Online] [-Verbose] [-Debug] [-ErrorAction <ActionPreference>] [-WarningAction <ActionPreference>] [-ErrorVariable <String>] [-WarningVariable <String>] [-OutVariable <String>] [-OutBuffer <Int32>]

Get-Help [[-Name] <String>] [-Path <String>] [-Category <String[]>] [-Component <String[]>] [-Functionality <String[]>]
 [-Role <String[]>] [-Parameter <String>] [-Online] [-Verbose] [-Debug] [-ErrorAction <ActionPreference>] [-WarningAction <ActionPreference>] [-ErrorVariable <String>] [-WarningVariable <String>] [-OutVariable <String>] [-OutBuffer <Int32>]
```

## <a name="displaying-available-command-by-type"></a>Rendelkezésre álló parancssori megjelenítése típus szerint

A `Get-Command` parancs felsorolja a parancsmagok csak az aktuális munkamenetben. PowerShell ténylegesen parancsok számos egyéb típusú támogatja:

- Aliasok
- Funkciók
- Parancsfájlok

Külső végrehajtható fájlok, vagy egy regisztrált típus kezelőjének rendelkező fájlokat is besorolt parancsokat.

A munkamenet összes parancs kérni, írja be:

```powershell
Get-Command *
```

Ez a lista tartalmazza a keresési útvonalat a külső parancsok, így tartalmazhat, ezer elem.
Több hasznos, és tekintse meg a parancsok csökkentett készletét.

> [!NOTE]
> A csillag (\*) helyettesítő karakterek használata a PowerShell-parancs argumentumainak szolgál. A \* azt jelenti, hogy egyezik"egy vagy több bármilyen karaktert". Beírhatja `Get-Command a*` található betűvel kezdődő összes parancs "a". Ellentétben a Cmd.exe megfelelő helyettesítő PowerShell a helyettesítő karakter is meg fog egyezni egy ideig.

Használja a **CommandType** paraméterében `Get-Command` beolvasni a más típusú natív parancsokat.
-parancsmag futtatási eredményei között.

Első parancsaliasok, amelyek a hozzárendelt beceneveinek parancsokat, írja be:

```powershell
Get-Command -CommandType Alias
```

A függvények az aktuális munkamenet kérni, írja be:

```powershell
Get-Command -CommandType Function
```

A PowerShell a keresési útvonalat szkriptek jelennek meg, írja be:

```powershell
Get-Command -CommandType Script
```