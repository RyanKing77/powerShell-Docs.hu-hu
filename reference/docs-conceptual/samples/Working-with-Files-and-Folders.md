---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: Fájlok és mappák használata
ms.assetid: c0ceb96b-e708-45f3-803b-d1f61a48f4c1
ms.openlocfilehash: 393e886a4945222198d9b81019250c5d5b905ad3
ms.sourcegitcommit: f4bd4e116e22c8b5bfcb61680a7c42e58b4da93e
ms.translationtype: HT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/22/2019
ms.locfileid: "59984391"
---
# <a name="working-with-files-and-folders"></a>Fájlok és mappák használata

Navigálás a Windows PowerShell-meghajtók és a rajtuk az elemek módosítása kezelésére szolgáló fizikai merevlemezek Windows található fájlok és mappák hasonlít. Ez a szakasz leírja, hogyan meghatározott fájl- és fájlkezelési feladatok PowerShell-lel kezelésére.

## <a name="listing-all-the-files-and-folders-within-a-folder"></a>A fájlok és a egy mappában található mappák listázása

A közvetlenül egy mappában található minden elemet is kap **Get-ChildItem**. Adja hozzá a választható **kényszerített** rejtettek megjelenítése vagy rendszer elemek paramétert. Ez a parancs például a Windows PowerShell meghajtót C (Ez ugyanaz, mint a Windows fizikai meghajtó C) a közvetlen tartalmát jeleníti meg:

```powershell
Get-ChildItem -Path C:\ -Force
```

A parancs felsorolja a csak a közvetlenül benne lévő elemek, hasonlóan a Cmd.exe használatával **DIR** parancs vagy **ls** egy UNIX-rendszerhéjban. Annak érdekében, hogy a benne lévő elemek megjelenítése, meg kell adnia a **-Recurse** paramétert is. (Ez egy rendkívül hosszú ideig eltarthat.) Minden, a C meghajtó megjelenítése:

```powershell
Get-ChildItem -Path C:\ -Force -Recurse
```

**Get-ChildItem** szűrheti az elemeket a **elérési**, **szűrő**, **Belefoglalás**, és **kizárása** paraméterek, de ezek is általában csak a neve alapján. Összetett szűrését az egyéb elemek tulajdonságai alapján is végezhet **Where-Object**.

A következő parancsot, amely utoljára módosítva 2005. október 1. után, és amelyek sem a kisebb, mint 1 megabájt, sem a 10 MB-nál nagyobb a Program Files mappában található megkeresi az összes végrehajtható fájlok:

```powershell
Get-ChildItem -Path $env:ProgramFiles -Recurse -Include *.exe | Where-Object -FilterScript {($_.LastWriteTime -gt '2005-10-01') -and ($_.Length -ge 1mb) -and ($_.Length -le 10mb)}
```

## <a name="copying-files-and-folders"></a>Fájlok és mappák másolása

Másolás végzett **Copy-Item**. C: készít biztonsági másolatot a következő parancs\\Boot.ini fájlt a C:\\boot.bak:

```powershell
Copy-Item -Path C:\boot.ini -Destination C:\boot.bak
```

Ha a célfájl már létezik, a másolási kísérlet meghiúsul. Egy már létező célhelyre felülírásához használja a **kényszerített** paramétert:

```powershell
Copy-Item -Path C:\boot.ini -Destination C:\boot.bak -Force
```

Ez a parancs működik, akkor is, ha a cél csak olvasható.

Mappa másolása ugyanúgy működik. Ez a parancs másolja át a C: mappa\\temp\\az új mappába C: Teszt1\\temp\\DeleteMe rekurzív módon:

```powershell
Copy-Item C:\temp\test1 -Recurse C:\temp\DeleteMe
```

A kijelölt elemek is másolhatja. A következő parancsot az összes, bárhol szerepel a c: .txt fájlt másolja\\c: adatok\\temp\\szöveg:

```powershell
Copy-Item -Filter *.txt -Path c:\data -Recurse -Destination C:\temp\text
```

Más eszközök segítségével továbbra is rendszer fájlmásolás hajtható végre. XCOPY ROBOCOPY és COM-objektumok, például a **Scripting.FileSystemObject,** összes működik a Windows PowerShellben. Például használhatja a Windows Script Host **Scripting.FileSystem COM** biztonsági mentése a C: osztály\\Boot.ini fájlt a C:\\boot.bak:

```powershell
(New-Object -ComObject Scripting.FileSystemObject).CopyFile('C:\boot.ini', 'C:\boot.bak')
```

## <a name="creating-files-and-folders"></a>Fájlok és mappák létrehozása

Új elemek létrehozását ugyanúgy működik az összes Windows PowerShell-szolgáltató. Ha egy Windows PowerShell-szolgáltatóval rendelkezik-e egynél több elem típusa – például a fájlrendszer Windows PowerShell-szolgáltatóban megkülönbözteti könyvtárak és fájlok – meg kell adni az elem típusa.

Ez a parancs létrehoz egy új mappát C:\\temp\\új mappa:

```powershell
New-Item -Path 'C:\temp\New Folder' -ItemType Directory
```

Ez a parancs létrehoz egy új üres fájlt C:\\temp\\új mappa\\file.txt

```powershell
New-Item -Path 'C:\temp\New Folder\file.txt' -ItemType File
```

## <a name="removing-all-files-and-folders-within-a-folder"></a>Összes fájlt és mappát egy mappában lévő eltávolítása

Eltávolíthatja a benne lévő elemek használatával **Remove-cikk**, de meg kell adnia az eltávolítás megerősítéséhez, ha az elem tartalmaz bármi más. Például, ha törli a mappát a C: próbál\\temp\\más elemeket tartalmazó DeleteMe, Windows PowerShell megerősítést kér a felhasználótól a mappa törlése előtt:

```
Remove-Item -Path C:\temp\DeleteMe

Confirm
The item at C:\temp\DeleteMe has children and the -recurse parameter was not
specified. If you continue, all children will be removed with the item. Are you
sure you want to continue?
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help
(default is "Y"):
```

Ha nem szeretné, hogy a rendszer minden egyes tartalmazott cikkhez, adja meg a **Recurse** paramétert:

```powershell
Remove-Item -Path C:\temp\DeleteMe -Recurse
```

## <a name="mapping-a-local-folder-as-a-windows-accessible-drive"></a>Elérhető Windows meghajtóként egy helyi mappába leképezése

Emellett leképezhet egy helyi mappába használatával a **subst** parancsot. A következő parancs létrehoz egy helyi meghajtóra P: feltörték a helyi programfájlok könyvtárban:

```powershell
subst p: $env:programfiles
```

Ugyanúgy mint a hálózati meghajtó, a meghajtók leképezve belül a Windows PowerShell használatával **subst** azonnal láthatók a Windows PowerShell parancshéj.

## <a name="reading-a-text-file-into-an-array"></a>Egy tömbbe egy szöveges fájl olvasása

A gyakori tároló formátumok szöveges adatok egyik, egy fájlban, a különböző adatelemek számít külön sorban. A **Get-tartalom** parancsmag is használható egy teljes fájl egy lépésben elolvasható itt látható módon:

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

**Get-tartalom** már kezeli egy tömb, a fájl tartalmának soronként egy elemet a fájlból beolvasott adatok. Ezt úgy ellenőrizheti a **hossza** a visszaadott tartalom:

```
PS> (Get-Content -Path C:\boot.ini).Length
6
```

Ez a parancs esetén a leghasznosabb közvetlenül első listák, amelyek Windows PowerShell segítségével. Például előfordulhat, hogy tárolása számítógépnevek vagy IP-címek listája egy fájlban C:\\temp\\domainMembers.txt, a fájl minden sorában egy névvel. Használhat **Get-tartalom** beolvasása a fájl tartalmát, és helyezze őket a változó **$Computers**:

```powershell
$Computers = Get-Content -Path C:\temp\DomainMembers.txt
```

**$Computers** már az egyes elemei a számítógép nevét tartalmazó tömb.
