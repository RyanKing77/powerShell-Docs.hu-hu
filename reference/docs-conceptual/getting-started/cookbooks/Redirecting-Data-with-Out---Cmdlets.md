---
ms.date: 06/05/2017
keywords: PowerShell parancsmag
title: Adatátirányítás az Out-parancsmagokkal
ms.assetid: 2a4acd33-041d-43a5-a3e9-9608a4c52b0c
ms.openlocfilehash: 3ca7984e831a995e80cbd8a4d83ae9225c2a4f4c
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="redirecting-data-with-out--cmdlets"></a>Az Out - adatok átirányítása * parancsmagok

A Windows PowerShell számos-parancsmagokat kínál, amelyekkel szabályozhatja, hogy közvetlenül a kimeneti adatok. Ezeket a parancsmagokat a megosztás két lényeges, azonosítandó paraméterek.

Először azokat általában átalakítási valamilyen szöveges adatokat. Van így, mert azok kimeneti szöveg beavatkozást igénylő rendszerösszetevők az adatokat. Ez azt jelenti, hogy az objektumokat képviseli szövegként van szükségük. A-szöveg formátuma, ezért a Windows PowerShell konzol ablakban látható módon.

Második, ezek a parancsmagok a Windows PowerShell-művelet használata **kimenő** mert azok adatokat küld a Windows PowerShell valahol máshol. A **kimenő gazdagép** parancsmag nincs kivétel: a fogadó ablakban megjelenített Windows PowerShell kívül esik. Ez azért fontos, mert a Windows PowerShell kívül adatokat küldi el, ha az ténylegesen törlődik. Erre úgy tekinthet, ha hozzon létre egy folyamatot, hogy a fogadó ablakban lapok az adatok, majd próbálja meg formázni a listában, ahogy az itt látható:

```powershell
Get-Process | Out-Host -Paging | Format-List
```

A parancs folyamatra vonatkozó információ oldalain megjelenő listaformátumot várt. Ehelyett az alapértelmezett táblázatos listáját jeleníti meg:

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

A **kimenő gazdagép** parancsmag elküldi az adatokat közvetlenül a konzol, ezért a **Format-List** parancs soha nem kap semmit formázásához.

A helyes-e ez a parancs szerkezeti módja, amelyre az a **kimenő gazdagép** parancsmag az alább látható módon a folyamat végén. Ez azt eredményezi, hogy a folyamat adatok listaként lapozható és a megjelenített előtt kell formázni.

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

Ez vonatkozik az összes a **kimenő** parancsmagok. Egy **kimenő** parancsmag mindig megjelenjen-e a folyamat végén.

> [!NOTE]
> Minden a **kimenő** parancsmagok szöveg, a formázást érvényben a konzolablakban, ideértve a sor hossza határok kimenet megjelenítése.

#### <a name="paging-console-output-out-host"></a>Lapozás a konzol kimeneti (kimenő gazdagép)

Alapértelmezés szerint a Windows PowerShell adatokat küldi el a gazdagép ablak, amely pontosan mi a kimenő gazdagép parancsmag biztosítja. Az elsődleges funkciója a kimenő gazdagép parancsmag lapozófájlok, mint korábban tárgyalt. Például a következő parancs használatát kimenő gazdagépről a Get-Command parancsmag kimenetét lapon:

```powershell
Get-Command | Out-Host -Paging
```

Használhatja a **további** oldaladatokat függvényt. A Windows PowerShell parancssorába **további** egy funkciója, amely behívja **kimenő gazdagép-lapozást**. Az alábbi parancs bemutatja, használja a **további** működnek, mint a Get-parancs kimenetében lapon:

```powershell
Get-Command | more
```

Ha egy vagy több fájlt adja meg a további függvény argumentumaként, a függvény a megadott fájlok olvasását, és azok tartalmát, a fogadó oldalon:

```
PS> more c:\boot.ini
[boot loader]
timeout=5
default=multi(0)disk(0)rdisk(0)partition(1)\WINDOWS
[operating systems]
...
```

#### <a name="discarding-output-out-null"></a>Kimeneti elvetése (kimenő Null)

A **kimenő Null** parancsmag arra tervezték, hogy azonnal elveti az összes beviteli kap. Ez akkor hasznos, a kapott egyik mellékhatása fut egy parancs, mint a szükségtelen adatok törlésével. Ha írja be a következő parancsot, nem kap semmit újra a parancsot:

```powreshell
Get-Command | Out-Null
```

A **kimenő Null** parancsmag dobja kimeneti hiba. Például, ha a következő parancsot adja meg, egy üzenet jelenik meg tájékoztat, hogy a Windows PowerShell nem ismeri fel a "Rendszer-NotACommand":

```
PS> Get-Command Is-NotACommand | Out-Null
Get-Command : 'Is-NotACommand' is not recognized as a cmdlet, function, operabl
e program, or script file.
At line:1 char:12
+ Get-Command  <<<< Is-NotACommand | Out-Null
```

#### <a name="printing-data-out-printer"></a>Nyomtatás adatok (Out-nyomtató)

Adatok használatával kinyomtathatja a **Out-nyomtató** parancsmag. A **Out-nyomtató** parancsmag fogja használni az alapértelmezett nyomtató, ha a nyomtató neve nincs megadva. Bármely Windows-alapú nyomtató használhatja a megjelenített név megadásával. Nincs szükség a nyomtató- vagy a tényleges fizikai nyomtató bármilyen típusú. Például ha a Microsoft Office dokumentum a lemezképkészítés eszközöket, akkor is küldheti az adatokat képfájlra mutató beírásával:

```powershell
Get-Command Get-Command | Out-Printer -Name 'Microsoft Office Document Image Writer'
```

#### <a name="saving-data-out-file"></a>Adatok mentése (out-File)

Egy fájl helyett a konzolablakban kimeneti a használatával küldhet a **out-File** parancsmag. A következő parancssori folyamatok listájának küld a fájl **C:\\temp\\processlist.txt**:

```powershell
Get-Process | Out-File -FilePath C:\temp\processlist.txt
```

Az eredmények használatával a **out-File** parancsmag nem lehet várt a hagyományos kimenet átirányítása használata. Szeretné megtudni, annak viselkedését, figyelembe kell venni a környezet, amelyben a **out-File** parancsmag működik.

Alapértelmezés szerint a **out-File** parancsmag létrehoz egy Unicode-fájlt. Ez az ajánlott alapértelmezett hosszú távon, de az azt jelenti, hogy eszközök, amelyek ASCII fájlokat nem fog megfelelően működni az alapértelmezett kimeneti formátummal. Módosíthatja az alapértelmezett kimeneti formátum ASCII használatával a **kódolás** paraméter:

```powershell
Get-Process | Out-File -FilePath C:\temp\processlist.txt -Encoding ASCII
```

**Out-File** formátumok fájl tartalmát a konzol kimeneti tűnik. Ez azt eredményezi, hogy a kimeneti kell csonkolni, akárcsak a legtöbb esetben a konzolablakban. Ha például a következő parancsot:

```powershell
Get-Command | Out-File -FilePath c:\temp\output.txt
```

A kimeneti fog kinézni:

```output
CommandType     Name                            Definition
-----------     ----                            ----------
Cmdlet          Add-Content                     Add-Content [-Path] <String[...
Cmdlet          Add-History                     Add-History [[-InputObject] ...
...
```

Ahhoz, hogy a kimenet nem kényszerítik ki a sor becsomagolja szélességét a megfelelő, használhatja a **szélesség** paramétert vonalvastagságát. Mivel **szélesség** 32 bites egész paraméter, a megadható maximális érték érték 2147483647. A vonalvastagság ezen maximális értékre állítva a következőket írja be:

```powershell
Get-Command | Out-File -FilePath c:\temp\output.txt -Width 2147483647
```

A **out-File** parancsmag akkor hasznos, ha a kimeneti menti, akkor rendelkezik jelenik meg a konzolon. A kimeneti formátum részletesebben vezérelheti speciális eszközök kell. A következő fejezet bizonyos adatai használható együtt a következő fog keresni.