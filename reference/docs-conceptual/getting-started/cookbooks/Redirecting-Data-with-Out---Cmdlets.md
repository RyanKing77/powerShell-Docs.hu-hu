---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: Adatátirányítás az Out-parancsmagokkal
ms.assetid: 2a4acd33-041d-43a5-a3e9-9608a4c52b0c
ms.openlocfilehash: f08879f436ce751b176af020aba21e90f09aa61f
ms.sourcegitcommit: 221b7daab7f597f8b2e4864cf9b5d9dda9b9879b
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 11/27/2018
ms.locfileid: "52321009"
---
# <a name="redirecting-data-with-out--cmdlets"></a>Adatátirányítás az Out-* parancsmagokkal

Windows PowerShell számos-parancsmagokat kínál, amelyek segítségével szabályozhatja, hogy közvetlenül a kimeneti adatokat. Ezek a parancsmagok két lényeges, azonosítandó paraméterek megosztani.

Először azok általánosan adatok átalakítása a valamilyen szöveget. Van így, mert ezek az adatok kimenetét szövegbevitel igénylő-összetevőkkel. Ez azt jelenti, hogy az objektumok tartozik szöveg van szükségük. A szöveg formátuma, ezért a Windows PowerShell konzol ablakában látható módon.

A második, ezeket a parancsmagokat használja-e a Windows PowerShell-műveletet **ki** mert azok adatokat küld a Windows Powershellből valahol máshol. A **élekről gazdagép** parancsmag ez sem kivétel: a fogadó ablakban megjelenített Windows PowerShell kívül esik. Ez azért fontos, mert adatküldést kívül a Windows PowerShell, ténylegesen eltávolítja azt. Ez, láthatja, ha létrehoz egy folyamatot, hogy a fogadó ablakban oldalak adatok próbálja, majd próbálja meg egy listaként formázandó itt látható módon:

```powershell
Get-Process | Out-Host -Paging | Format-List
```

Így várhatóan a parancs formátuma folyamatra vonatkozó információ a lapok megjelenítéséhez. Ehelyett azt jeleníti meg az alapértelmezett táblázatos listájában:

```output
Handles  NPM(K)    PM(K)      WS(K) VM(M)   CPU(s)     Id ProcessName
-------  ------    -----      ----- -----   ------     -- -----------
    101       5     1076       3316    32     0.05   2888 alg
...
    618      18    39348      51108   143   211.20    740 explorer
    257       8     9752      16828    79     3.02   2560 explorer
...
<SPACE> next page; <CR> next line; Q quit
...
```

A **élekről gazdagép** parancsmag elküldi az adatokat a konzolon, így a **Format-List** parancs soha nem kap semmit sem kell formázni.

Építse fel a parancs a megfelelő módon, hogy helyezze a **élekről gazdagép** parancsmag az alább látható módon a folyamat végén. Ennek hatására az adatfeldolgozás előtt lapozható és a megjelenő listában formázott.

```
PS> Get-Process | Format-List | Out-Host -Paging

Id      : 2888
Handles : 101
CPU     : 0.046875
Name    : alg
...

Id      : 740
Handles : 612
CPU     : 211.703125
Name    : explorer

Id      : 2560
Handles : 257
CPU     : 3.015625
Name    : explorer
...
<SPACE> next page; <CR> next line; Q quit
...
```

Ez vonatkozik az összes a **ki** parancsmagok. Egy **ki** parancsmag mindig meg kell jelennie a folyamat végén.

> [!NOTE]
> Az összes a **ki** parancsmagok az kimeneti használatával a formázás érvényben a konzolablakban, beleértve a sor hosszának korlátozása, szöveges formában jelennek meg.

#### <a name="paging-console-output-out-host"></a>Lapozófájl-konzolkimenet (élekről gazdagép)

Alapértelmezés szerint Windows PowerShell a gazdagép ablak, amely pontosan mit küld adatokat a kimenő irányú gazdagép parancsmag biztosítja. Az elsődleges funkciója a élekről gazdagép parancsmag a már volt szó korábbi lapozófájlok lehetőség. A következő parancsot használja például élekről tárolni a lapon a Get-Command parancsmag kimenete:

```powershell
Get-Command | Out-Host -Paging
```

Is használhatja a **további** oldaladatokat függvényt. A Windows PowerShellben **további** egy függvény meghívásához **élekről gazdagép-lapozás**. A következő parancs használatát mutatja be a **további** függvény lapon a Get-parancs kimenetében:

```powershell
Get-Command | more
```

Ha további függvény argumentumaként adja meg egy vagy több fájlt, a függvény a megadott fájlok olvasásához, és azok tartalmát, a fogadó oldalon:

```
PS> more c:\boot.ini
[boot loader]
timeout=5
default=multi(0)disk(0)rdisk(0)partition(1)\WINDOWS
[operating systems]
...
```

#### <a name="discarding-output-out-null"></a>Kimeneti elvetése (élekről Null)

A **élekről Null** célja, hogy a parancsmag azonnal elveti fogad semmilyen bemenetet. Ez akkor hasznos, ami miatt elvetette a szükségtelen adatokat, mellékhatása futtat egy parancsot kap. Amikor beírja a következő parancsot, nem kap semmit újra a parancsot:

```powershell
Get-Command | Out-Null
```

A **élekről Null** parancsmag nem elveti hibakimenet. Például ha ad meg a következő parancsot, megjelenik egy üzenet, amely tájékoztatja, hogy Windows PowerShell nem ismeri fel a "Van – NotACommand":

```
PS> Get-Command Is-NotACommand | Out-Null
Get-Command : 'Is-NotACommand' is not recognized as a cmdlet, function, operabl
e program, or script file.
At line:1 char:12
+ Get-Command  <<<< Is-NotACommand | Out-Null
```

#### <a name="printing-data-out-printer"></a>Nyomtatás adatok (Out-nyomtató)

Adatok használatával kinyomtathatja a **Out-nyomtató** parancsmagot. A **Out-nyomtató** parancsmag fogja használni az alapértelmezett nyomtató, ha nem ad meg a nyomtató neve. Bármely Windows-alapú nyomtató használhatja a megjelenített név megadásával. Hiba esetén nem kell a nyomtató- vagy a tényleges fizikai nyomtató bármilyen típusú. Például ha rendelkezik a Microsoft Office dokumentum lemezkép-készítési eszközök telepíteni, elküldheti az adatok képfájlra mutató beírásával:

```powershell
Get-Command Get-Command | Out-Printer -Name 'Microsoft Office Document Image Writer'
```

#### <a name="saving-data-out-file"></a>Adatok mentése (out-File)

Egy fájl helyett a konzolablakban kimeneti a használatával küldhet a **out-File** parancsmagot. A következő parancsot a folyamatok listáját küld a fájl **C:\\temp\\processlist.txt**:

```powershell
Get-Process | Out-File -FilePath C:\temp\processlist.txt
```

Az eredményeket a a **out-File** parancsmag nem lehet várt hagyományos kimenet átirányítása való használatakor. Szeretné megtudni, annak viselkedését, figyelembe kell venni a környezet, amelyben a **out-File** parancsmag működik.

Alapértelmezés szerint a **out-File** parancsmag létrehoz egy Unicode-fájlt. Ez az ajánlott alapértelmezett hosszú távon, de az azt jelenti, hogy eszközöket, amelyek hatással vannak az ASCII-fájlokat nem működik megfelelően az alapértelmezett kimeneti formátum. ASCII az alapértelmezett kimeneti formátum a használatával módosíthatja a **kódolás** paramétert:

```powershell
Get-Process | Out-File -FilePath C:\temp\processlist.txt -Encoding ASCII
```

**Out-File** formátumok tartalmát a konzol kimenete a következőképpen néznek fájlt. Ez azt eredményezi, hogy az eredmény csonkolva lesznek, mint a legtöbb esetben a konzolablakban van. Ha például a következő parancsot:

```powershell
Get-Command | Out-File -FilePath c:\temp\output.txt
```

A kimenet a következőképpen jelenik meg:

```output
CommandType     Name                            Definition
-----------     ----                            ----------
Cmdlet          Add-Content                     Add-Content [-Path] <String[...
Cmdlet          Add-History                     Add-History [[-InputObject] ...
...
```

Szeretne kapni, amely nem kényszeríti a sor burkolja szélességét a megfelelő kimeneti, használhatja a **szélesség** paraméterrel megadhatja a vonal vastagsága. Mivel **szélesség** van a 32 bites egész szám paramétert, a maximális megadható értéke 2147483647. Írja be a következő, a maximális értékre a vonalvastagság:

```powershell
Get-Command | Out-File -FilePath c:\temp\output.txt -Width 2147483647
```

A **out-File** parancsmag akkor hasznos, ha a kimeneti menti, ahogyan kellene rendelkeznek a konzolon. Kimeneti formátum szabályozásához kell speciális eszközök. Az alábbiakban tájékozódhat a következő fejezet, és néhány információ az objektum adatkezelési lévőket.