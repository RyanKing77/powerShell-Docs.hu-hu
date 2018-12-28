---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: A kimeneti nézet módosítása formázási parancsokkal
ms.assetid: 63515a06-a6f7-4175-a45e-a0537f4f6d05
ms.openlocfilehash: 97d3a9e04abb61bb80a0b8c67d9fb9e885a0b91b
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/14/2018
ms.locfileid: "53404463"
---
# <a name="using-format-commands-to-change-output-view"></a>A kimeneti nézet módosítása formázási parancsokkal

Windows PowerShell-parancsmagokat, amelyek lehetővé teszik annak ellenőrzését, milyen tulajdonságok jelennek meg az adott objektumok rendelkezik. A parancsmagok minden kezdődik-e a művelet **formátum**. Segítségével válassza ki egy vagy több tulajdonságának megjelenítéséhez.

A **formátum** parancsmagok a következők **formátum kiterjedő**, **Format-List**, **Format-Table**, és **formátumban – egyéni**. Csak bemutatunk néhányat a **formátum kiterjedő**, **Format-List**, és **Format-Table** parancsmagok a felhasználói útmutató a.

Minden egyes formátum parancsmag rendelkezik, amelyek alkalmazva lesznek, ha nem adja meg a konkrét tulajdonságok megjeleníthető alapértelmezett tulajdonságai. Minden parancsmagot is használ ugyanabban a paraméternév megadásához, **tulajdonság**, hogy melyik megjeleníteni kívánt tulajdonságokat határozza meg. Mivel **formátum kiterjedő** csak jelenik meg, hogy egy adott tulajdonságra a **tulajdonság** paraméter mindössze egyetlen érték, de a tulajdonság paraméterei **Format-List** és **Format-Table** elfogadja a tulajdonság nevének listáját.

Ha a parancs **Get-Process - név powershell** két példánya fut a Windows PowerShell, a következőket kínálja a következőhöz hasonló kimenetet:

```output
Handles  NPM(K)    PM(K)      WS(K) VM(M)   CPU(s)     Id ProcessName
-------  ------    -----      ----- -----   ------     -- -----------
    995       9    30308      27996   152     2.73   2760 powershell
    331       9    23284      29084   143     1.06   3448 powershell
```

Ez a szakasz a többi tárgyaljuk fog használata **formátum** parancsmagok megváltoztatni a parancs kimenetének jelenik meg.

### <a name="using-format-wide-for-single-item-output"></a>Egyetlen elemből kimeneti formátum kiterjedő használatával

A **formátum kiterjedő** parancsmag alapértelmezés szerint jeleníti meg az objektumok csak az alapértelmezett tulajdonságait. Az egyes objektumok társított információkat egy oszlopban jelenik meg:

```
PS> Get-Process -Name powershell | Format-Wide

powershell                              powershell
```

Megadhat egy nem alapértelmezett tulajdonságot is:

```
PS> Get-Process -Name powershell | Format-Wide -Property Id

2760                                    3448
```

#### <a name="controlling-format-wide-display-with-column"></a>Formátum kiterjedő megjelenítendő oszlop szabályozása

Az a **formátum kiterjedő** parancsmagot egyszerre csak megjelenítheti egy-egy tulajdonság. Így egyszerű listák, azt mutatják be, soronként csak egy elem megjelenítése esetén hasznos. Egyszerű lista kapni, állítsa a **oszlop** paraméter 1 beírásával:

```powershell
Get-Command Format-Wide -Property Name -Column 1
```

### <a name="using-format-list-for-a-list-view"></a>Az adott nézet használata a Format-List

A **Format-List** címkével ellátott és a egy külön sorban jelenik meg minden egyes tulajdonság parancsmag megjeleníti az egy lista formájában objektum:

```
PS> Get-Process -Name powershell | Format-List

Id      : 2760
Handles : 1242
CPU     : 3.03125
Name    : powershell

Id      : 3448
Handles : 328
CPU     : 1.0625
Name    : powershell
```

A kívánt számú tulajdonságait is megadhatja:

```
PS> Get-Process -Name powershell | Format-List -Property ProcessName,FileVersion
,StartTime,Id

ProcessName : powershell
FileVersion : 1.0.9567.1
StartTime   : 2006-05-24 13:42:00
Id          : 2760

ProcessName : powershell
FileVersion : 1.0.9567.1
StartTime   : 2006-05-24 13:54:28
Id          : 3448
```

#### <a name="getting-detailed-information-by-using-format-list-with-wildcards"></a>Kezdeti lépéseket ismertető részletes információkat a helyettesítő karakterek használatával Format-List

A **Format-List** parancsmag használatát teszi lehetővé egy helyettesítő karaktert tartalmazó értéket annak **tulajdonság** paraméter. Ezáltal részletes információk megjelenítéséhez. Objektumok tartozhat több információt van szüksége, ezért a Windows PowerShell nem jeleníti meg az összes tulajdonságértékek alapértelmezés szerint. Az összes objektum tulajdonságainak megjelenítéséhez használja a **Format-List-tulajdonság \&#42;** parancsot. A következő parancsot a folyamat egyetlen kimeneti több mint 60 sor hoz létre:

```powershell
Get-Process -Name powershell | Format-List -Property *
```

Bár a **Format-List** parancs hasznos, hogy a részletes, ha azt szeretné, hogy hány elemet tartalmazó kimeneti áttekintése, egy egyszerűbb táblázatos nézet gyakran több hasznos.

### <a name="using-format-table-for-tabular-output"></a>A táblázatos kimenet Format-Table használatával

Ha használja a **Format-Table** nincs tulajdonságnevekkel rendelkező parancsmag kimenetének formázására megadott a **Get-Process** parancsot, ugyanúgy mint formázás végrehajtása nélkül kimeneti kap. Az oka, hogy a folyamatok általában megjelenik, táblázatos formában, amelyek a legtöbb Windows PowerShell-objektumok.

```
PS> Get-Process -Name powershell | Format-Table

Handles  NPM(K)    PM(K)      WS(K) VM(M)   CPU(s)     Id ProcessName
-------  ------    -----      ----- -----   ------     -- -----------
   1488       9    31568      29460   152     3.53   2760 powershell
    332       9    23140        632   141     1.06   3448 powershell
```

#### <a name="improving-format-table-output-autosize"></a>Format-Table kimeneti (automatikus méretezése) javítása

Bár egy táblázatos nézetben sok összehasonlítható adat megjelenítése esetén hasznos, nehéz értelmezni, ha a megjelenített adatok túl keskeny lehet. Például ha folyamat útvonala, Azonosítóját, nevét és a vállalat megjelenítéséhez, megkapja rövidített kimenet a folyamat elérési út és a vállalati oszlopot:

```
PS> Get-Process -Name powershell | Format-Table -Property Path,Name,Id,Company

Path                Name                                 Id Company
----                ----                                 -- -------
C:\Program Files... powershell                         2836 Microsoft Corpor...
```

Ha megad a **AutoSize** paramétert, ha futtatja a **Format-Table** parancsot a Windows PowerShell Oszlopszélességek szeretné megjeleníteni a tényleges adatok alapján számítja ki. Ez lehetővé teszi a **elérési út** olvasható oszlopot, de a céges oszlopot marad csonkolva:

```
PS> Get-Process -Name powershell | Format-Table -Property Path,Name,Id,Company -
AutoSize

Path                                                    Name         Id Company
----                                                    ----         -- -------
C:\Program Files\Windows PowerShell\v1.0\powershell.exe powershell 2836 Micr...
```

A **Format-Table** parancsmag továbbra is előfordulhat, hogy csonkolja az adatokat, de azt fogja csak ehhez a képernyő alján. Tulajdonságok, nem az utolsó jelenik meg, akár mérete, a leghosszabb adatelem helyes megjelenítéséhez az igény szerinti vannak megadva. Láthatja, hogy cég neve látható, de ha, cseréje a helyek, a rendszer csonkolja a elérési utat **elérési** és **vállalati** a a **tulajdonság** tartományérték-listája:

```
PS> Get-Process -Name powershell | Format-Table -Property Company,Name,Id,Path -
AutoSize

Company               Name         Id Path
-------               ----         -- ----
Microsoft Corporation powershell 2836 C:\Program Files\Windows PowerShell\v1...
```

A **Format-Table** parancs feltételezi, hogy a nearer tulajdonságot, hogy a tulajdonságlistában elején minél többet a fontos. Így megkísérli a legközelebbi elején a tulajdonságainak megjelenítéséhez teljesen. Ha a **Format-Table** parancs nem jeleníthető meg az összes tulajdonság, az egyes oszlopok eltávolítása a képernyőt, és adja meg a figyelmeztetést. Ha választja ki láthatja ezt a viselkedést **neve** az utolsó tulajdonság a listában:

```
PS> Get-Process -Name powershell | Format-Table -Property Company,Path,Id,Name -
AutoSize

WARNING: column "Name" does not fit into the display and was removed.

Company               Path                                                    I
                                                                              d
-------               ----                                                    -
Microsoft Corporation C:\Program Files\Windows PowerShell\v1.0\powershell.exe 6
```

A fenti kimenetben a rendszer csonkolja az azonosító oszlop, hogy a listaelem illik, és az oszlopfejlécek vannak halmozott. Automatikus méretezés, az oszlopok nem mindig mit szeretne.

#### <a name="wrapping-format-table-output-in-columns-wrap"></a>Alkalmazásburkoló Format-Table kimeneti oszlopok (sortörés)

Kényszerítheti hosszadalmas **Format-Table** burkolása belül a megjelenítendő oszlop használatával az adatokat a **burkolása** paraméter. Használatával a **burkolása** önálló paraméter nem feltétlenül tesz program működésére nézve, mivel ha akkor is nem ad meg alapértelmezett beállításokat használja **AutoSize**:

```
PS> Get-Process -Name powershell | Format-Table -Wrap -Property Name,Id,Company,
Path

Name                                 Id Company             Path
----                                 -- -------             ----
powershell                         2836 Microsoft Corporati C:\Program Files\Wi
                                        on                  ndows PowerShell\v1
                                                            .0\powershell.exe
```

Egy használatának előnye a **burkolása** paraméter önmagában az, hogy azt ne lassítsa le nagy feldolgozási. Ha hajt végre egy nagy directory rendszer rekurzív fájl listája, akkor előfordulhat, hogy nagyon hosszú időt vehet igénybe, és sok memóriát használni, mielőtt az első kimeneti elemek megjelenítése, ha **AutoSize**.

Ha még nem érintett rendszer terhelési, majd **AutoSize** jól működik a **burkolása** paraméter. A kezdeti oszlopokat mindig van leállítaná a lehető szélesség elemek megjelenítéséhez egy sorban, ugyanúgy, mint ha igény szerinti **AutoSize** nélkül a **burkolása** paraméter. Az egyetlen különbség, hogy az utolsó oszlopban besorolva szükség esetén:

```
PS> Get-Process -Name powershell | Format-Table -Wrap -AutoSize -Property Name,I
d,Company,Path

Name         Id Company               Path
----         -- -------               ----
powershell 2836 Microsoft Corporation C:\Program Files\Windows PowerShell\v1.0\
                                      powershell.exe
```

Egyes oszlopok előfordulhat, hogy nem kell jelenik meg, ha először adja meg a legszélesebb körű oszlopokat, hogy legyen legbiztosabb megoldás, ha először adja meg a legkisebb adatelemeket. A következő példában azt adja meg a rendkívül széles elérésiút-elem először, és még az alkalmazásburkoló, hogy továbbra is elveszíti a végső **neve** oszlopban:

```
PS> Get-Process -Name powershell | Format-Table -Wrap -AutoSize -Property Path,I
d,Company,Name

WARNING: column "Name" does not fit into the display and was removed.

Path                                                      Id Company
----                                                      -- -------
C:\Program Files\Windows PowerShell\v1.0\powershell.exe 2836 Microsoft Corporat
                                                             ion
```

#### <a name="organizing-table-output--groupby"></a>Tábla kimeneti rendszerezése (-GroupBy)

Táblázatos kimenet ellenőrzése egy másik hasznos paraméter értéke nem **GroupBy**. Már táblázatos listaelemek különösen nehezen hasonlítsa össze lehet. A **GroupBy** paraméter kimenete egy tulajdonság értéke alapján csoportosítja. Például hogy csoportosíthatók a folyamatok könnyebb vizsgálatra kihagyása a cég érték a tulajdonság lista a vállalat által:

```
PS> Get-Process -Name powershell | Format-Table -Wrap -AutoSize -Property Name,I
d,Path -GroupBy Company

   Company: Microsoft Corporation

Name         Id Path
----         -- ----
powershell 1956 C:\Program Files\Windows PowerShell\v1.0\powershell.exe
powershell 2656 C:\Program Files\Windows PowerShell\v1.0\powershell.exe
```