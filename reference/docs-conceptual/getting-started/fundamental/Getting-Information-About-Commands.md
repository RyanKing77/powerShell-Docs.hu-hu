---
ms.date: 2017-06-05
keywords: PowerShell parancsmag
title: "Parancsok kapcsolatos információk beolvasásakor"
ms.assetid: 56f8e5b4-d97c-4e59-abbe-bf13e464eb0d
ms.openlocfilehash: 98e449110860ea81939d6ec0b7b1a8534a2da2aa
ms.sourcegitcommit: 74255f0b5f386a072458af058a15240140acb294
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/03/2017
---
# <a name="getting-information-about-commands"></a>Parancsok kapcsolatos információk beolvasásakor
A Windows PowerShell **Get-Command** parancsmag lekéri az aktuális munkamenetben rendelkezésre álló összes parancsot. Amikor beírja **Get-Command** egy Windows PowerShell parancssorába, a következőhöz hasonló kimenetet fog látni:

```
PS> Get-Command
CommandType     Name                            Definition
-----------     ----                            ----------
Cmdlet          Add-Content                     Add-Content [-Path] <String[...
Cmdlet          Add-History                     Add-History [[-InputObject] ...
Cmdlet          Add-Member                      Add-Member [-MemberType] <PS...
...
```

Ez a kimeneti keres sokkal például a Cmd.exe súgó kimenete: belső parancsok táblázatos összegzését. A kivonat a a **Get-Command** a fent látható minden parancs látható kimeneti rendelkezik egy parancsmag CommandType parancsot. A parancsmag típus Windows PowerShell belső parancs - olyan típusú, amely a nagyjából megfelel a **dir** és **cd** Cmd.exe, valamint a UNIX ismertetése, például a BASH built-ins parancsok.

A kimenet a **Get-Command** parancsot, a definíciók végződhet folytatást jelző pontokra (...), annak jelzésére, hogy a PowerShell nem tudja megjeleníteni a tartalmat a rendelkezésre álló területet. Windows PowerShell kimenet megjelenítése, ha a kimeneti szövegként formázza, és azt, hogy az adatok szabályszerűen felelnek meg az ablak majd elrendezése. Előadás a későbbi szakaszában a is.

A **Get-Command** parancsmagja rendelkezik egy **szintaxis** paraméter, amely minden parancsmag szintaxisa a következő lekérdezi. Ahhoz, hogy a Get-Help parancsmag szintaxisa a következő, a következő paranccsal:

**Get-Help Get-Command-szintaxis**

```
Get-Help [[-Name] <String>] [-Path <String>] [-Category <String[]>] [-Component <String[]>] [-Functionality <String[]>]
 [-Role <String[]>] [-Full] [-Online] [-Verbose] [-Debug] [-ErrorAction <ActionPreference>] [-WarningAction <ActionPreference>] [-ErrorVariable <String>] [-WarningVariable <String>] [-OutVariable <String>] [-OutBuffer <Int32>]

Get-Help [[-Name] <String>] [-Path <String>] [-Category <String[]>] [-Component <String[]>] [-Functionality <String[]>]
 [-Role <String[]>] [-Detailed] [-Online] [-Verbose] [-Debug] [-ErrorAction <ActionPreference>] [-WarningAction <ActionPreference>] [-ErrorVariable <String>] [-WarningVariable <String>] [-OutVariable <String>] [-OutBuffer <Int32>]

Get-Help [[-Name] <String>] [-Path <String>] [-Category <String[]>] [-Component <String[]>] [-Functionality <String[]>]
 [-Role <String[]>] [-Examples] [-Online] [-Verbose] [-Debug] [-ErrorAction <ActionPreference>] [-WarningAction <ActionPreference>] [-ErrorVariable <String>] [-WarningVariable <String>] [-OutVariable <String>] [-OutBuffer <Int32>]

Get-Help [[-Name] <String>] [-Path <String>] [-Category <String[]>] [-Component <String[]>] [-Functionality <String[]>]
 [-Role <String[]>] [-Parameter <String>] [-Online] [-Verbose] [-Debug] [-ErrorAction <ActionPreference>] [-WarningAction <ActionPreference>] [-ErrorVariable <String>] [-WarningVariable <String>] [-OutVariable <String>] [-OutBuffer <Int32>]
```

### <a name="displaying-available-command-types"></a>Elérhető parancstípusok megjelenítése
A **Get-Command** parancs nem szerepel minden elérhető Windows PowerShell parancsot. Ehelyett a **Get-Command** parancs csak a parancsmagokat a jelenlegi munkamenet jeleníti meg. A Windows PowerShell ténylegesen támogatja több más típusú parancsokat. Aliasok, függvények és parancsfájlok egyaránt Windows PowerShell-parancsok, bár a nem a Windows PowerShell felhasználói útmutatója részletes ismertetése. Külső fájlok, amelyeknek is végrehajtható, vagy egy regisztrált típus kezelőjének is besorolt parancsok.

Ahhoz, hogy minden parancs a munkamenetben, írja be:

```
Get-Command *
```

Mivel ebben a listában a keresési elérési út külső fájlokat tartalmazza, ezrei között válogathat tartalmazhat. Több célszerű egy meghatározott parancsok közül.

Más típusú natív parancsok használatához a **CommandType** paramétere a **Get-Command** parancsmag.

> [!NOTE]
> A csillag (\*) helyettesítő karakterek használata a Windows PowerShell parancssori argumentumok szolgál. A \* azt jelenti, hogy "egyezik egy vagy több szereplő olyan karakterek". Beírhatja **Get-Command egy\&#42;** található a betűvel kezdődő minden parancs "a". Ellentétben a Cmd.exe megfelelő helyettesítő a Windows PowerShell helyettesítő is fog egyezni időtartamra.

Get parancs aliasok, amelyek a hozzárendelt becenevet parancsokat, írja be:

```
Get-Command -CommandType Alias
```

A funkciók eléréséhez a jelenlegi munkamenet, írja be:

```
Get-Command -CommandType Function
```

A Windows PowerShell keresési út parancsfájlok megjelenítéséhez írja be:

```
Get-Command -CommandType Script
```

