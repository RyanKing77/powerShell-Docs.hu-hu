---
ms.date: 2017-06-05
keywords: PowerShell parancsmag
title: "A fájlok és mappák"
ms.assetid: c0ceb96b-e708-45f3-803b-d1f61a48f4c1
ms.openlocfilehash: 73773df9f018c396c9c4237a40f2e9d2c841464e
ms.sourcegitcommit: 74255f0b5f386a072458af058a15240140acb294
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/03/2017
---
# <a name="working-with-files-and-folders"></a>A fájlok és mappák
Windows PowerShell-meghajtókat nézetre lépne, és azokat az elemeket kezelése hasonlít a fájlok és mappák Windows fizikai merevlemezeken kezelésére. Meghatározott fájlok és mappák adatkezelési feladatok ebben a szakaszban kezelése ismertetik.

### <a name="listing-all-the-files-and-folders-within-a-folder"></a>A fájlok és mappák egy mappában listázása
A közvetlenül az egyes mappákban lévő összes elemet is ki **Get-ChildItem**. Adja hozzá a választható **kényszerített** rejtett megjelenítése vagy rendszer elemek paraméter. A parancs például a Windows PowerShell meghajtót C (Ez ugyanaz, mint a Windows fizikai C meghajtó) közvetlen tartalmát jeleníti meg:

```
Get-ChildItem -Force C:\
```

A parancs csak közvetlenül a benne lévő elemeket tartalmazza, hasonlóan a Cmd.exe tartozó **DIR** parancs vagy **ls** egy UNIX rendszerhéj. Ahhoz, hogy a benne lévő elemek megjelenítése, meg kell adnia a **-Recurse** paramétert is. (Ez egy nagyon hosszú ideig eltarthat.) Minden, a C meghajtó listázásához:

```
Get-ChildItem -Force C:\ -Recurse
```

**Get-ChildItem** elemek szűrheti a **elérési**, **szűrő**, **Include**, és **kizárása** paraméterek, de azok csak a név általában alapulnak. Összetett szűrés használatával-elemek egyéb tulajdonságok alapján hajthat végre **Where-Object**.

A következő parancsot, amely legutóbbi módosításának 2005. október 1. után, és amelyeket nem kisebb, mint 1 megabájt, és nem nagyobb, mint 10 megabájt, a Program Files mappában található összes végrehajtható talál:

```
Get-ChildItem -Path $env:ProgramFiles -Recurse -Include *.exe | Where-Object -FilterScript {($_.LastWriteTime -gt "2005-10-01") -and ($_.Length -ge 1m) -and ($_.Length -le 10m)}
```

### <a name="copying-files-and-folders"></a>Fájlok és mappák másolása
Másolás történik a **elem**. A következő parancs készít biztonsági másolatot C:\\c: boot.ini\\boot.bak:

```
Copy-Item -Path c:\boot.ini -Destination c:\boot.bak
```

Ha a célfájl már létezik, a másolási kísérlet meghiúsul. Egy már meglévő cél felülírásához használja a Force paramétert:

```
Copy-Item -Path c:\boot.ini -Destination c:\boot.bak -Force
```

Ez a parancs is működik, ha a cél csak olvasható.

Mappa másolása ugyanúgy működik. Ez a parancs, másolja át a mappát a C:\\temp\\az új mappa c: Teszt1\\temp\\DeleteMe rekurzív módon:

```
Copy-Item C:\temp\test1 -Recurse c:\temp\DeleteMe
```

A kijelölt elemek is másolhatja. A következő parancsot a c: bármely részén lévő összes .txt fájlt másolja át\\c: adatok\\temp\\szöveg:

```
Copy-Item -Filter *.txt -Path c:\data -Recurse -Destination c:\temp\text
```

Más eszközök hajtható végre rendszer továbbra is használhatja. XCOPY, a ROBOCOPY és a COM-objektumok, például a **Scripting.FileSystemObject,** összes működik a Windows PowerShellben. Például használhatja a Windows Script Host **Scripting.FileSystem COM** osztály biztonsági mentése C:\\c: boot.ini\\boot.bak:

```
(New-Object -ComObject Scripting.FileSystemObject).CopyFile("c:\boot.ini", "c:\boot.bak")
```

### <a name="creating-files-and-folders"></a>Fájlok és mappák létrehozása
Új elemek létrehozását működik, az összes Windows PowerShell-szolgáltató. Ha egy Windows PowerShell-szolgáltató rendelkezik-e az elem egynél több típus – például a fájlrendszer Windows PowerShell-szolgáltatóval különbözteti meg a könyvtárak és fájlok között – meg kell adnia az elem típusa.

Ez a parancs létrehoz egy új mappát C:\\temp\\új mappa:

```
New-Item -Path 'C:\temp\New Folder' -ItemType "directory"
```

Ez a parancs létrehoz egy üres fájlt C:\\temp\\új mappa\\file.txt

```
New-Item -Path 'C:\temp\New Folder\file.txt' -ItemType "file"
```

### <a name="removing-all-files-and-folders-within-a-folder"></a>Minden egyes mappákban lévő mappa és eltávolítása
Eltávolíthatja a benne lévő elemek használata **Remove-cikk**, de kérni fogja az eltávolítás megerősítéséhez, ha az elem tartalmaz dolgozott. Például, ha törli a mappát a C: próbál\\temp\\további elemeket tartalmazó DeleteMe, a Windows PowerShell jóváhagyást kér a mappa törlése előtt:

```
Remove-Item C:\temp\DeleteMe

Confirm
The item at C:\temp\DeleteMe has children and the -recurse parameter was not
specified. If you continue, all children will be removed with the item. Are you
sure you want to continue?
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help
(default is "Y"):
```

Ha nem szeretné, hogy minden benne lévő elemhez kéri, adja meg a **Recurse** paraméter:

```
Remove-Item C:\temp\DeleteMe -Recurse
```

### <a name="mapping-a-local-folder-as-a-windows-accessible-drive"></a>Egy helyi mappába elérhető Windows meghajtóként leképezése
Egy helyi mappát is leképezheti használatával a **subst** parancsot. A következő parancsot a helyi Program Files mappában hozza létre egy helyi meghajtó P: feltört eszköz:

```
subst p: $env:programfiles
```

Ugyanúgy, mint a hálózati meghajtó meghajtó képeznek le a Windows PowerShell használatával **subst** azonnal láthatók a Windows PowerShell felületet.

### <a name="reading-a-text-file-into-an-array"></a>A tömb szövegfájlba olvasása
A gyakori tárolási formátumok tartozó szöveges adatok egyik fájlba a különböző adatelemek számít külön sorban. A **Get-tartalom** parancsmag segítségével olvassa el a teljes fájl egy lépésben, ahogy az itt látható:

```
PS> Get-Content -Path C:\boot.ini
[boot loader]
timeout=5
default=multi(0)disk(0)rdisk(0)partition(1)\WINDOWS
[operating systems]
multi(0)disk(0)rdisk(0)partition(1)\WINDOWS="Microsoft Windows XP Professional"
 /noexecute=AlwaysOff /fastdetect
multi(0)disk(0)rdisk(0)partition(1)\WINDOWS=" Microsoft Windows XP Professional 
with Data Execution Prevention" /noexecute=optin /fastdetect
```

**Get-tartalom** már kezeli az adatokat a következő fájl olvasásának tömbként fájl tartalma soronként egy elemmel. Ez alapján ellenőrizheti a **hossza** a visszaadott tartalom:

```
PS> (Get-Content -Path C:\boot.ini).Length
6
```

Ez a parancs esetén a leghasznosabb tudnak közvetlenül a Windows PowerShell rendszerbe információk listáját. Például akkor lehet, hogy a számítógép nevét vagy IP-címek listáját egy fájlban tárolhatja C:\\temp\\domainMembers.txt, a fájl minden egyes sorban egy névvel. Használhat **Get-tartalom** kérhető le a fájl tartalmát, és helyezze őket a változó **$Computers**:

```
$Computers = Get-Content -Path C:\temp\DomainMembers.txt
```

**$Computers** mostantól egy tömb egyes elemei a számítógép nevét tartalmazó.

