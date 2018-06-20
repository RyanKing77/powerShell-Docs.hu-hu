---
ms.date: 06/05/2017
keywords: PowerShell parancsmag
title: Fájlmappák és beállításkulcsok használata
ms.assetid: e6cf87aa-b5f8-48d5-a75a-7cb7ecb482dc
ms.openlocfilehash: a09b127d4ba37d33cb4c0f0ce0819e645fd4b137
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
ms.locfileid: "30952307"
---
# <a name="working-with-files-folders-and-registry-keys"></a>A fájlok, mappák és beállításkulcsok

A Windows PowerShell használja a főnév **elem** utal, egy Windows PowerShell-meghajtón található elemekre. A Windows PowerShell fájlrendszer-szolgáltatót, amikor egy **elem** lehet, hogy a fájl, mappa vagy a Windows PowerShell meghajtót. Listázása, és ezek az elemek használata a legtöbb felügyeleti beállítások kritikus alapvető tevékenység, így azt szeretnénk, és beszéljék meg ezeket a feladatokat részletesen.

### <a name="enumerating-files-folders-and-registry-keys-get-childitem"></a>Fájlok, mappák és beállításkulcsok (Get-ChildItem) számbavétele

Elemek gyűjteménye lekérése egy adott helyen egy ilyen közös feladat, mivel a **Get-ChildItem** parancsmag célja kifejezetten a tárolóhoz, például egy mappában található elemeket.

Ha szeretne visszaállítani, minden fájl és mappa, amely közvetlenül a C: mappában található\\Windows, típus:

```
PS> Get-ChildItem -Path C:\Windows
    Directory: Microsoft.Windows PowerShell.Core\FileSystem::C:\Windows

Mode                LastWriteTime     Length Name
----                -------------     ------ ----
-a---        2006-05-16   8:10 AM          0 0.log
-a---        2005-11-29   3:16 PM         97 acc1.txt
-a---        2005-10-23  11:21 PM       3848 actsetup.log
...
```

A lista tartalmazza a következőhöz hasonló mi mutatunk be kell megadni a **dir** parancsot **Cmd.exe**, vagy a **ls** parancsot egy UNIX parancs-rendszerhéjban.

A paraméterek használatával nagyon összetett listaelemek végezheti el a **Get-ChildItem** parancsmag. Követően áttekintjük néhány olyan forgatókönyvet mellett. Megtekintheti a szintaxist a **Get-ChildItem** parancsmag beírásával:

```powershell
Get-Command -Name Get-ChildItem -Syntax
```

Ezek a paraméterek vegyes, és nagy mértékben testre szabott kimeneti beolvasandó egyezik.

#### <a name="listing-all-contained-items--recurse"></a>Minden tartalmazott elemek listázása (-Recurse)

A Windows mappában található elemek, mind az almappák belüli elemek megtekintéséhez használja a **Recurse** paramétere **Get-ChildItem**. Az átjáróra a listában jeleníti meg minden belül a Windows mappa és annak almappáiban található elemek. Például:

```
PS> Get-ChildItem -Path C:\WINDOWS -Recurse

    Directory: Microsoft.Windows PowerShell.Core\FileSystem::C:\WINDOWS
    Directory: Microsoft.Windows PowerShell.Core\FileSystem::C:\WINDOWS\AppPatch
Mode                LastWriteTime     Length Name
----                -------------     ------ ----
-a---        2004-08-04   8:00 AM    1852416 AcGenral.dll
...
```

#### <a name="filtering-items-by-name--name"></a>A Szűrés név alapján (-név)

Csak az elemek nevei megjelenítéséhez használja a **neve** paramétere **Get-Childitem**:

```
PS> Get-ChildItem -Path C:\WINDOWS -Name
addins
AppPatch
assembly
...
```

#### <a name="forcibly-listing-hidden-items--force"></a>Kényszerített módon a rejtett elemek listázása (-Force)

Elemek, amelyek normál esetben nem látható a Fájlkezelőben vagy a Cmd.exe nem jelennek meg a kimenete egy **Get-ChildItem** parancsot. Rejtett elemek megjelenítéséhez használja a **kényszerített** paramétere **Get-ChildItem**. Például:

```powershell
Get-ChildItem -Path C:\Windows -Force
```

Ez a paraméter neve kényszerített mert kényszerített felülírhatja, normál viselkedése a **Get-ChildItem** parancsot. Kényszerített kényszeríti egy műveletet, amely a parancsmag nem általában kell elvégeznie, bár nem hajt végre semmilyen művelet, amely a rendszer biztonsági gyengíti széles körben használt paramétereinek.

#### <a name="matching-item-names-with-wildcards"></a>A helyettesítő karakterek egyező elemek nevei

**A Get-ChildItem** parancs fogad el helyettesítő karakterek az elérési út az elemek listázásához.

Helyettesítő karakterek megfeleltetése végzi el a Windows PowerShell-motor, mert az összes parancsmag, amely támogatja a helyettesítő karakterek azonos jelöléssel, és rendelkezik a megfelelő viselkedést. A Windows PowerShell helyettesítő notation tartalmazza:

- A csillag karakter (\*) bármely karakter nulla vagy több előfordulásának felel meg.

- A kérdőjel (?) felel meg pontosan egy karaktert.

- Nyitó szögletes zárójel (\[) szögletes zárójel (]) és karakter között legyen, megfeleltethetők karakterek.

Az alábbiakban néhány olyan helyettesítő specification működése.

A utótagot a Windows könyvtárban található összes fájl **.log** , és pontosan öt karakter nevét, írja be a következő parancsot:

```
PS> Get-ChildItem -Path C:\Windows\?????.log

    Directory: Microsoft.Windows PowerShell.Core\FileSystem::C:\Windows
Mode                LastWriteTime     Length Name
----                -------------     ------ ----
...
-a---        2006-05-11   6:31 PM     204276 ocgen.log
-a---        2006-05-11   6:31 PM      22365 ocmsn.log
...
-a---        2005-11-11   4:55 AM         64 setup.log
-a---        2005-12-15   2:24 PM      17719 VxSDM.log
...
```

Található összes fájl, a betűvel kezdődő **x** a Windows könyvtárban, írja be:

```powershell
Get-ChildItem -Path C:\Windows\x*
```

Található összes fájl kezdődő **x** vagy **z**, típus:

```powershell
Get-ChildItem -Path C:\Windows\[xz]*
```

#### <a name="excluding-items--exclude"></a>Elemek kizárása (-kizárása)

Kizárhat meghatározott elemek használatával a **kizárása** Get-ChildItem paramétere. Ez lehetővé teszi összetett szűrést a egy utasítás végrehajtásához.

Tegyük fel például, a System32 mappában található a Windows idő szolgáltatás DLL kívánt, és az összes DLL-fájl nevére emlékszik, hogy a "W" szóval kezdődik, és rendelkezik-e "32" azt.

Egy kifejezés, például **w\&#42; 32\&#42;. dll** található összes DLL-fájl, amely megfelel a feltételeknek, de előfordulhat, hogy is vissza a Windows 95 és 16 bites Windows kompatibilitási DLL-fájl, amely tartalmazza az "95" vagy "16" a név. Fájlok, amelyek segítségével a név nem tartalmazhatják a számok, akkor kihagyhatja a **kizárása** mintájú paraméter  **\&#42;\[ 9516]\&#42;**:

```
PS> Get-ChildItem -Path C:\WINDOWS\System32\w*32*.dll -Exclude *[9516]*

Directory: Microsoft.PowerShell.Core\FileSystem::C:\WINDOWS\System32
Mode                LastWriteTime     Length Name
----                -------------     ------ ----
-a---        2004-08-04   8:00 AM     174592 w32time.dll
-a---        2004-08-04   8:00 AM      22016 w32topl.dll
-a---        2004-08-04   8:00 AM     101888 win32spl.dll
-a---        2004-08-04   8:00 AM     172032 wldap32.dll
-a---        2004-08-04   8:00 AM     264192 wow32.dll
-a---        2004-08-04   8:00 AM      82944 ws2_32.dll
-a---        2004-08-04   8:00 AM      42496 wsnmp32.dll
-a---        2004-08-04   8:00 AM      22528 wsock32.dll
-a---        2004-08-04   8:00 AM      18432 wtsapi32.dll
```

#### <a name="mixing-get-childitem-parameters"></a>Get-ChildItem paraméterek keverése

Több paramétereinek a **Get-ChildItem** parancsmagja ugyanezt a parancsot. Előtt kombinálhatók paraméterek, mindenképpen tájékozódjon a helyettesítő karakterek megfeleltetése. A következő parancs például nincs eredmény eredményt adja vissza:

```powershell
Get-ChildItem -Path C:\Windows\*.dll -Recurse -Exclude [a-y]*.dll
```

Annak ellenére, hogy van két dll, a Windows mappában található "z" betűvel kezdődő, nincsenek nem járt eredménnyel.

Nincs eredmény mert azt az elérési út egy része a helyettesítő megadva. Annak ellenére, hogy a parancs a következő volt rekurzív, a **Get-ChildItem** parancsmag elemeket korlátozva azokat, amelyeket a Windows mappában található ".dll" végződő nevű.

Fájlok, amelyek neve különleges mintát illeszteni rekurzív keresését megadásához használja a **-tartalmaznak** paraméter.

```
PS> Get-ChildItem -Path C:\Windows -Include *.dll -Recurse -Exclude [a-y]*.dll

    Directory: Microsoft.Windows PowerShell.Core\FileSystem::C:\Windows\System32\Setup

Mode                LastWriteTime     Length Name
----                -------------     ------ ----
-a---        2004-08-04   8:00 AM       8261 zoneoc.dll

    Directory: Microsoft.Windows PowerShell.Core\FileSystem::C:\Windows\System32

Mode                LastWriteTime     Length Name
----                -------------     ------ ----
-a---        2004-08-04   8:00 AM     337920 zipfldr.dll
```