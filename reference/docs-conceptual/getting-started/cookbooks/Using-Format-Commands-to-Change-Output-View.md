---
ms.date: 06/05/2017
keywords: PowerShell parancsmag
title: A kimeneti nézet módosítása formázási parancsokkal
ms.assetid: 63515a06-a6f7-4175-a45e-a0537f4f6d05
ms.openlocfilehash: 97d3a9e04abb61bb80a0b8c67d9fb9e885a0b91b
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="using-format-commands-to-change-output-view"></a>A kimeneti nézet módosítása formázási parancsokkal

A Windows PowerShell-parancsmagok lehetővé teszik annak ellenőrzését, mely tulajdonságok jelennek meg az adott objektumok rendelkezik. A parancsmagok neve kezdődhet művelet **formátum**. Segítségükkel jelöljön ki egy vagy több tulajdonságot megjelenítése.

A **formátum** parancsmagok **formátum kiterjedő**, **Format-List**, **Format-Table**, és **formátum-egyéni**. Csak ismerteti, hogy a **formátum kiterjedő**, **Format-List**, és **Format-Table** parancsmagok a felhasználói útmutatóban.

Mindegyik formátum parancsmagja rendelkezik, amelyek alkalmazva lesznek, ha nem adja meg a megjelenítendő tulajdonságokat alapértelmezett tulajdonságok. Minden parancsmagot is ugyanolyan névvel paraméter, **tulajdonság**, mely tulajdonságainak kívánja megjeleníteni. Mivel **formátum kiterjedő** csak mutatja egy-egy tulajdonság, a **tulajdonság** paraméter mindössze egyetlen értéket, de a tulajdonság paraméterei **Format-List** és **Format-Table** elfogadja a tulajdonságnevek listáját.

A parancs **Get-Process - név powershell** két példányban fut a Windows PowerShell, a kapott kimenete a következőképpen néz ki:

```output
Handles  NPM(K)    PM(K)      WS(K) VM(M)   CPU(s)     Id ProcessName
-------  ------    -----      ----- -----   ------     -- -----------
    995       9    30308      27996   152     2.73   2760 powershell
    331       9    23284      29084   143     1.06   3448 powershell
```

Ez a szakasz a többi, hogyan használhatja néhány **formátum** parancsmagok segítségével módosíthatja, miként jelenik meg ez a parancs kimenetét.

### <a name="using-format-wide-for-single-item-output"></a>Egyetlen elem kimeneti formátum kiterjedő használatával

A **formátum kiterjedő** parancsmag, alapértelmezés szerint csak az alapértelmezett tulajdonság az objektum megjeleníti. Az információk is társítva vannak az egyes objektumok egy oszlopban jelenik meg:

```
PS> Get-Process -Name powershell | Format-Wide

powershell                              powershell
```

Azt is megadhatja a nem alapértelmezett tulajdonság:

```
PS> Get-Process -Name powershell | Format-Wide -Property Id

2760                                    3448
```

#### <a name="controlling-format-wide-display-with-column"></a>Ellenőrző formátum kiterjedő megjelenített oszlop

Az a **formátum kiterjedő** parancsmag, egy adott tulajdonságra egyszerre csak megjeleníteni. Így hasznos, ha csak egy elem soronként egyszerű listák megjelenítése. Ahhoz, hogy egy egyszerű listázása, állítsa a **oszlop** paraméter 1 beírásával:

```powershell
Get-Command Format-Wide -Property Name -Column 1
```

### <a name="using-format-list-for-a-list-view"></a>Az adott nézet formátum-lista használatával

A **Format-List** parancsmag formátumban jeleníti meg az objektum a listaelem, minden egyes tulajdonsággal címkével, és külön sorban jelenik meg:

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

Megadhatja, hogy a kívánt annyi tulajdonságokat:

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

#### <a name="getting-detailed-information-by-using-format-list-with-wildcards"></a>A helyettesítő karakterek formátum-lista használatával beolvasásakor részletes információk

A **Format-List** parancsmag lehetővé teszi, hogy egy helyettesítő értékeként a **tulajdonság** paraméter. Ez lehetővé teszi a részletes információk megjelenítéséhez. Objektumok gyakran, például a több információt van szüksége, ezért a Windows PowerShell nem szerepelnek alapértelmezés szerint minden tulajdonság értékével. Az összes objektum tulajdonságainak megjelenítéséhez használja a **Format-List-tulajdonság \&#42;** parancsot. A következő parancsot a folyamat egyetlen kimeneti több mint 60 sort hoz létre:

```powershell
Get-Process -Name powershell | Format-List -Property *
```

Bár a **Format-List** parancs akkor hasznos, ha a bemutató részletes, ha azt szeretné, hogy hány elemet tartalmazó kimeneti áttekintése, egy egyszerűbb táblázatos nézet gyakran több hasznos.

### <a name="using-format-table-for-tabular-output"></a>Táblázat formázása használatával táblázatos kimenet

Használatakor a **Format-Table** nem tulajdonságnevek parancsmagnak megadott formázásához kimenetét a **Get-Process** parancsban, ugyanúgy kimeneti, végrehajtása formázás nélkül teszi elérhetővé. Oka az, hogy folyamatok táblázatos formában, általában megjelenik, amelyek a legtöbb Windows PowerShell-objektum.

```
PS> Get-Process -Name powershell | Format-Table

Handles  NPM(K)    PM(K)      WS(K) VM(M)   CPU(s)     Id ProcessName
-------  ------    -----      ----- -----   ------     -- -----------
   1488       9    31568      29460   152     3.53   2760 powershell
    332       9    23140        632   141     1.06   3448 powershell
```

#### <a name="improving-format-table-output-autosize"></a>Táblázat formázása kimeneti (AutoSize) javítása

Bár a táblázatos nézet akkor hasznos, ha nagy mennyiségű összehasonlítható információk megjelenítése, ha a megjelenítési túl széleskörű, az adatok értelmezése nehéz lehet. Például ha folyamat elérési útját, Azonosítóját, nevét és vállalati megjelenítéséhez, akkor érhető el csonkolt kimeneti folyamat elérési útját és a vállalat oszlop:

```
PS> Get-Process -Name powershell | Format-Table -Property Path,Name,Id,Company

Path                Name                                 Id Company
----                ----                                 -- -------
C:\Program Files... powershell                         2836 Microsoft Corpor...
```

Ha megadja a **AutoSize** paraméter futtatásakor a **Format-Table** parancsot a Windows PowerShell oszlopszélességet is szeretné megjeleníteni a tényleges adatai alapján számítja ki. Ez lehetővé teszi a **elérési** olvasható oszlop, de a vállalati oszlop marad csonkolt:

```
PS> Get-Process -Name powershell | Format-Table -Property Path,Name,Id,Company -
AutoSize

Path                                                    Name         Id Company
----                                                    ----         -- -------
C:\Program Files\Windows PowerShell\v1.0\powershell.exe powershell 2836 Micr...
```

A **Format-Table** parancsmag továbbra is előfordulhat, hogy csonkolja adatokat, de ez csak elvégzi, a képernyő végén. Tulajdonságok, nem az utolsó jelenik meg, adta mértékű mérete, a leghosszabb adatelem helyes megjelenítéséhez van szükségük. Láthatja, hogy vállalatnév látható, de a elérési utat a függvény egésszé csonkítja helyeinek felcserélése, ha **elérési** és **vállalati** a a **tulajdonság** értékek listájából:

```
PS> Get-Process -Name powershell | Format-Table -Property Company,Name,Id,Path -
AutoSize

Company               Name         Id Path
-------               ----         -- ----
Microsoft Corporation powershell 2836 C:\Program Files\Windows PowerShell\v1...
```

A **Format-Table** parancs feltételezi, hogy a nearer egy tulajdonság az keresésitulajdonság-lista elejére annál a fontos. A rendszer megkísérli a kezdő legközelebbi tulajdonságok megjelenítése teljesen. Ha a **Format-Table** parancs nem jeleníti meg az összes tulajdonság, az egyes oszlopok eltávolítása a képernyőt, és adja meg a figyelmeztetést. Ha ez a viselkedés látható **neve** a lista utolsó tulajdonság:

```
PS> Get-Process -Name powershell | Format-Table -Property Company,Path,Id,Name -
AutoSize

WARNING: column "Name" does not fit into the display and was removed.

Company               Path                                                    I
                                                                              d
-------               ----                                                    -
Microsoft Corporation C:\Program Files\Windows PowerShell\v1.0\powershell.exe 6
```

A fenti kimenetben azonosító oszlopban a függvény egésszé csonkítja abba, hogy felelnek meg az átjáróra a listában, és az oszlopfejlécek vannak halmozott. Automatikus méretezés, az oszlopok nem mindig tegye azt szeretné.

#### <a name="wrapping-format-table-output-in-columns-wrap"></a>Alkalmazásburkoló táblázat formázása kimeneti oszlopok (sortörés)

Beállíthatja, hogy a hosszú **Format-Table** burkolása belül a megjelenítendő oszlop használatával adatok a **burkolása** paraméter. Használja a **burkolása** paraméter csak feltétlenül nem várt, mert az alapértelmezett beállítást használja, ha nem is meg **AutoSize**:

```
PS> Get-Process -Name powershell | Format-Table -Wrap -Property Name,Id,Company,
Path

Name                                 Id Company             Path
----                                 -- -------             ----
powershell                         2836 Microsoft Corporati C:\Program Files\Wi
                                        on                  ndows PowerShell\v1
                                                            .0\powershell.exe
```

Egy használatának előnye a **burkolása** önmagában paraméter megadása, hogy azt ne lassítsa le nagyon kevés feldolgozása. Egy rekurzív felsoroló nagy directory rendszert, akkor előfordulhat, hogy nagyon hosszú időt vehet igénybe, és nagy mennyiségű memóriát használja az első kimeneti elemek megjelenítése, ha használata előtt **AutoSize**.

Ha aggódik nem rendszerterhelés, majd **AutoSize** jól működik a **burkolása** paraméter. A kezdeti oszlopok vannak mindig engedélyezett módon elemek megjelenítése egy sorban, ugyanúgy, mint ha a szükséges mértékű szélesség **AutoSize** nélkül a **burkolása** paraméter. Az egyetlen különbség az, hogy az utolsó oszlopban lesz kell csomagolni, ha szükséges:

```
PS> Get-Process -Name powershell | Format-Table -Wrap -AutoSize -Property Name,I
d,Company,Path

Name         Id Company               Path
----         -- -------               ----
powershell 2836 Microsoft Corporation C:\Program Files\Windows PowerShell\v1.0\
                                      powershell.exe
```

Egyes oszlopok előfordulhat nem jelenik meg, ha először adja meg a legszélesebb oszlopok, hogy először a legkisebb adatelemek megadását legbiztonságosabb. A következő példában azt adja meg a rendkívül nagy elérésiút-elem első, és még az alkalmazásburkoló, azt még elveszíti a végleges **neve** oszlop:

```
PS> Get-Process -Name powershell | Format-Table -Wrap -AutoSize -Property Path,I
d,Company,Name

WARNING: column "Name" does not fit into the display and was removed.

Path                                                      Id Company
----                                                      -- -------
C:\Program Files\Windows PowerShell\v1.0\powershell.exe 2836 Microsoft Corporat
                                                             ion
```

#### <a name="organizing-table-output--groupby"></a>Táblázatos kimenete rendszerezéséhez (-GroupBy)

Egy másik hasznos táblázatos kimeneti vezérlővel paramétere **GroupBy**. Már táblázatos listaelemek különösen nehezen összehasonlítása lehet. A **GroupBy** paraméter kimeneti tulajdonság értéke alapján csoportosítja. Például azt csoportosíthatja, a vállalat értéket a tulajdonság listaelem kihagyásával könnyebb ellenőrzésre, vállalat által folyamatok:

```
PS> Get-Process -Name powershell | Format-Table -Wrap -AutoSize -Property Name,I
d,Path -GroupBy Company

   Company: Microsoft Corporation

Name         Id Path
----         -- ----
powershell 1956 C:\Program Files\Windows PowerShell\v1.0\powershell.exe
powershell 2656 C:\Program Files\Windows PowerShell\v1.0\powershell.exe
```