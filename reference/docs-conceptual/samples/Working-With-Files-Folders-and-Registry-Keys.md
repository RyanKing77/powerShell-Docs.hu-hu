---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: Fájlmappák és beállításkulcsok használata
ms.assetid: e6cf87aa-b5f8-48d5-a75a-7cb7ecb482dc
ms.openlocfilehash: cd20cc50b573435ba80b52b51e164e60625dc1b6
ms.sourcegitcommit: 806cf87488b80800b9f50a8af286e8379519a034
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2019
ms.locfileid: "59293095"
---
# <a name="working-with-files-folders-and-registry-keys"></a>Fájlok, mappák és beállításkulcsok használata

Windows PowerShell használja a főnév **elem** egy Windows PowerShell-meghajtón található elemekre utal. A Windows PowerShell fájlrendszer szolgáltató esetén egy **elem** lehet, hogy egy fájl, mappa vagy a Windows PowerShell meghajtót. Listázás, és ezek az elemek használata a kritikus alapszintű tevékenység a legtöbb felügyeleti beállítások, így szeretnénk ezeket a feladatokat részletesen ismertetjük.

## <a name="enumerating-files-folders-and-registry-keys-get-childitem"></a>Fájlok, mappák és beállításkulcsok (Get-ChildItem) számbavétele

Mivel az elemgyűjtemény lekérése egy adott helyen az ilyen gyakori feladat, a **Get-ChildItem** parancsmag célja kifejezetten olyan tárolóban, például egy mappában található összes elemet adja vissza.

Ha be szeretné olvasni a fájlt vagy mappát közvetlenül a C: mappa belüli lemezképcsomagban\\Windows, írja be:

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

Az eredményablakban hasonlít mi lenne láthatja, mikor, adja meg a **dir** parancsot **Cmd.exe**, vagy a **ls** parancsot egy UNIX parancs-rendszerhéjban.

A paraméterek használatával is elvégezheti a nagyon összetett listaelemek a **Get-ChildItem** parancsmagot. Tekintsük meg néhány forgatókönyv mellett. Láthatja, hogy a szintaxis a **Get-ChildItem** parancsmag beírásával:

```powershell
Get-Command -Name Get-ChildItem -Syntax
```

Ezeket a paramétereket is lehet vegyes és nagymértékben testre szabott kimeneti első megegyeznek.

### <a name="listing-all-contained-items--recurse"></a>Az összes tárolt elemek listázása (-Recurse)

A Windows mappában található elemek és a az almappák belüli lemezképcsomagban elemek megtekintéséhez használja a **Recurse** paraméterében **Get-ChildItem**. A listában jeleníti meg minden belül a Windows mappa és annak almappáiban található elemek. Például:

```
PS> Get-ChildItem -Path C:\WINDOWS -Recurse

    Directory: Microsoft.Windows PowerShell.Core\FileSystem::C:\WINDOWS
    Directory: Microsoft.Windows PowerShell.Core\FileSystem::C:\WINDOWS\AppPatch
Mode                LastWriteTime     Length Name
----                -------------     ------ ----
-a---        2004-08-04   8:00 AM    1852416 AcGenral.dll
...
```

### <a name="filtering-items-by-name--name"></a>A Szűrés név alapján (-név)

Csak a nevek elemek megjelenítéséhez használja a **neve** paraméterében **Get-Childitem**:

```
PS> Get-ChildItem -Path C:\WINDOWS -Name
addins
AppPatch
assembly
...
```

### <a name="forcibly-listing-hidden-items--force"></a>Rejtett elemek kényszerített listázása (-Force)

Elemek, amelyek normál esetben nem látható a fájlkezelő vagy a Cmd.exe nem jelennek meg a kimenetét egy **Get-ChildItem** parancsot. Rejtett elemek megjelenítéséhez használja a **kényszerített** paraméterében **Get-ChildItem**. Például:

```powershell
Get-ChildItem -Path C:\Windows -Force
```

Ez a paraméter neve kényszerített mert kényszerített felül lehet bírálni a normál viselkedését a **Get-ChildItem** parancsot. Kényszerített egy széles körben használt paraméter, amely arra kényszeríti a egy műveletet, amely a parancsmag nem megfelelően szeretné végrehajtani, de nem hajt végre semmilyen műveletet, amely a károsan befolyásolja a rendszer a biztonsági.

### <a name="matching-item-names-with-wildcards"></a>A helyettesítő karakterek az egyező elemek nevei

**A Get-ChildItem** parancs elfogadja a helyettesítő karaktereket a következő elérési az elemek listázásához.

A Windows PowerShell motor helyettesítő kezeli, mivel minden parancsmag, amely elfogadja a helyettesítő karaktereket azonos jelöléssel, és rendelkezik a megfelelő viselkedést. A Windows PowerShell helyettesítő jelöléssel tartalmazza:

- Csillag (\*) nulla vagy több karaktert helyettesít előfordulásának felel meg.

- Kérdőjel (?) pontosan egy karakterre illeszkedik.

- Bal oldali zárójelet (\[) záró zárójel (]) és karakter körülvevő karakterek egyezést kell keresni.

Az alábbiakban néhány példa a helyettesítő karakteres specifikáció működését.

A Windows könyvtárban a utótaggal rendelkező minden fájlt megtalál, **.log** pontosan öt karaktert a nevét, adja meg a következő parancsot:

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

Keresse meg az összes betűvel kezdődő **x** a Windows könyvtárban, írja be:

```powershell
Get-ChildItem -Path C:\Windows\x*
```

Keresse meg az összes kezdődő **x** vagy **z**, írja be:

```powershell
Get-ChildItem -Path C:\Windows\[xz]*
```

### <a name="excluding-items--exclude"></a>Elemek kizárása (-kizárása)

Használatával zárhat ki adott elemeket a **kizárása** Get-ChildItem paraméterében. Ez lehetővé teszi összetett szűrését egy utasítás végrehajtásához.

Tegyük fel például, próbált keresse meg a Windows idő DLL-t a System32 mappába, és minden DLL nevéről emlékszik, amellyel kezdődik "W" és "32" szerepel.

Egy kifejezés, például **w\&#42; 32\&#42;. dll** található összes DLL-fájl, amely megfelel a feltételeknek, de azt is visszaadhatnak a Windows 95 és 16-bites Windows kompatibilitási DLL-fájlok, amelyek tartalmazzák a "95" vagy "16" nevükben. Fájlok, amelyek ezeket a számokat a nevükben használatával, akkor kihagyhatja a **kizárása** mintával rendelkező paraméter  **\&#42;\[ 9516]\&#42;**:

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

### <a name="mixing-get-childitem-parameters"></a>Get-ChildItem paraméterek keverése

Több paramétereit a **Get-ChildItem** parancsmagja ugyanezt a parancsot. Mielőtt vegyesen paramétert figyeljen arra, hogy ismernie a helyettesítő karakterek megfeleltetése. Az alábbi parancs például nincs eredményeket ad vissza:

```powershell
Get-ChildItem -Path C:\Windows\*.dll -Recurse -Exclude [a-y]*.dll
```

Nincsenek eredmények, annak ellenére, hogy van két DLL-fájlok, amelyek a Windows mappában található a "–" z az a betűvel kezdődik.

Mivel a helyettesítő karakter az elérési út részeként megadott műveletnek nincs eredménye. Annak ellenére, hogy a parancs lett rekurzív, a **Get-ChildItem** parancsmag korlátozott elemek, amelyek az ".dll" végződés nevekkel a Windows mappában találhatók.

Adja meg egy rekurzív keresését, fájlok, amelyeknek a neve egyezik meg a speciális mintát, használja a **-tartalmaznak** paraméter.

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