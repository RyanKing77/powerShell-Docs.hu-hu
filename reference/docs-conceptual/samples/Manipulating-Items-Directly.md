---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: Elemek közvetlen módosítása
ms.assetid: 8cbd4867-917d-41ea-9ff0-b8e765509735
ms.openlocfilehash: 4caa7d2e0eecff9783556062d8503fe10e616fe5
ms.sourcegitcommit: 806cf87488b80800b9f50a8af286e8379519a034
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2019
ms.locfileid: "59293265"
---
# <a name="manipulating-items-directly"></a>Elemek közvetlen módosítása

A Windows PowerShell-meghajtók, például a fájlokat és mappákat a fájl rendszermeghajtók, és a Windows PowerShell-beállításjegyzék meghajtó, a beállításkulcsok látható elemeket az úgynevezett *elemek* a Windows PowerShellben. A parancsmagok a velük végzett munkát elem van a főnév **elem** nevükben.

A kimenetét a **Get-Command - főnév elem** -parancs bemutatja, hogy nincsenek-e kilenc Windows PowerShell item-parancsmagokkal.

```
PS> Get-Command -Noun Item

CommandType     Name                            Definition
-----------     ----                            ----------
Cmdlet          Clear-Item                      Clear-Item [-Path] <String[]...
Cmdlet          Copy-Item                       Copy-Item [-Path] <String[]>...
Cmdlet          Get-Item                        Get-Item [-Path] <String[]> ...
Cmdlet          Invoke-Item                     Invoke-Item [-Path] <String[...
Cmdlet          Move-Item                       Move-Item [-Path] <String[]>...
Cmdlet          New-Item                        New-Item [-Path] <String[]> ...
Cmdlet          Remove-Item                     Remove-Item [-Path] <String[...
Cmdlet          Rename-Item                     Rename-Item [-Path] <String>...
Cmdlet          Set-Item                        Set-Item [-Path] <String[]> ...
```

## <a name="creating-new-items-new-item"></a>Új elemek (új elem) létrehozása

A fájlrendszer egy új elem létrehozásához használja a **New-cikk** parancsmagot. Tartalmazza a **elérési** paramétert az elem elérési útja és a **ItemType** paraméter "fájl" vagy "könyvtár" értékkel.

Például, hogy hozzon létre egy új könyvtárat neve "a C: New.Directory"in\\írja be a Temp könyvtárában:

```
PS> New-Item -Path c:\temp\New.Directory -ItemType Directory

    Directory: Microsoft.Windows PowerShell.Core\FileSystem::C:\temp

Mode                LastWriteTime     Length Name
----                -------------     ------ ----
d----        2006-05-18  11:29 AM            New.Directory
```

Hozzon létre egy fájlt, módosítsa az értékét a **ItemType** "file" paraméterként. Például hozzon létre egy New.Directory a címtárban "file1.txt" nevű fájlt, írja be:

```
PS> New-Item -Path C:\temp\New.Directory\file1.txt -ItemType file

    Directory: Microsoft.Windows PowerShell.Core\FileSystem::C:\temp\New.Directory

Mode                LastWriteTime     Length Name
----                -------------     ------ ----
-a---        2006-05-18  11:44 AM          0 file1
```

Ugyanezen technika használatával hozzon létre egy új beállításkulcsot. Valójában a beállításkulcs lehet egyszerűen hozható létre, mert a csak jelentéselem-típus szerepel a Windows beállításjegyzék-kulcsot. (Beállításjegyzék bejegyzései elem *tulajdonságok*.) Írja be például a CurrentVersion alkulcsban "_hitelesítő" nevű kulcs létrehozásához:

```
PS> New-Item -Path HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion_Test

   Hive: Microsoft.PowerShell.Core\Registry::HKEY_LOCAL_MACHINE\SOFTWARE\Micros
oft\Windows\CurrentVersion

SKC  VC Name                           Property
---  -- ----                           --------
  0   0 _Test                          {}
```

Amikor beírja egy beállításjegyzékbeli elérési út, így feltétlenül foglalja bele a kettőspont (**:**) a Windows PowerShellben meghajtó a nevek, HKLM: és HKCU:. Windows PowerShell a kettőspont nélkül nem ismeri fel a meghajtó nevét, az elérési út.

## <a name="why-registry-values-are-not-items"></a>Miért beállításjegyzék értékei nem elemek

Használatakor a **Get-ChildItem** parancsmaggal azon elemeinek megkeresése egy beállításkulcsot, soha nem láthatja tényleges beállításjegyzék-bejegyzések és azok értékei.

Például a beállításkulcs **HKEY_LOCAL_MACHINE\\szoftver\\Microsoft\\Windows\\CurrentVersion\\futtatása** általában tartalmaz számos beállításjegyzék-bejegyzések amelyek az alkalmazások futtatására, amikor a rendszer.

Azonban, ha használ **Get-ChildItem** keresse ki a kulcsot a gyermekelemek, látni fogja az összes van a **OptionalComponents** a kulcs alkulcs:

```
PS> Get-ChildItem HKLM:\Software\Microsoft\Windows\CurrentVersion\Run

   Hive: Microsoft.PowerShell.Core\Registry::HKEY_LOCAL_MACHINE\Software\Micros
oft\Windows\CurrentVersion\Run
SKC  VC Name                           Property
---  -- ----                           --------
  3   0 OptionalComponents             {}
```

Annak ellenére, hogy szeretné kezelni a beállításjegyzék-bejegyzések elemek kényelmes, úgy, hogy gondoskodik róla, hogy azt az egyedi nem adható meg a egy beállításjegyzékbeli bejegyzést elérési útját. Az elérési út jelölés nem különbözteti meg a beállításkulcsot nevű **futtatása** és a **(alapértelmezett)** beállításjegyzékbeli bejegyzést a **futtatása** alkulcs. Továbbá mert a beállításjegyzék-bejegyzések neve tartalmazhat fordított perjellel (**\\**), ha beállításjegyzék-bejegyzések elemet, majd különbséget tenni egy nevű beállításjegyzék-bejegyzés nem tudta használni az elérési út jelöléssel  **Windows\\CurrentVersion\\futtatása** származó az alkulcs az adott elérési úton található.

## <a name="renaming-existing-items-rename-item"></a>Meglévő elemeket (Rename-elem) átnevezése

Egy fájl vagy mappa neve módosításához használja a **Rename-cikk** parancsmagot. A következő parancs módosítja a nevét a **file1.txt** fájlt **fileOne.txt**.

```powershell
Rename-Item -Path C:\temp\New.Directory\file1.txt fileOne.txt
```

A **Rename-cikk** parancsmaggal módosíthatja egy fájl vagy mappa nevét, de egy elem nem helyezhető át. A következő parancs sikertelen lesz, mivel megkísérli helyezze át a fájlt a New.Directory-könyvtár Temp könyvtárában.

```
PS> Rename-Item -Path C:\temp\New.Directory\fileOne.txt c:\temp\fileOne.txt
Rename-Item : Cannot rename because the target specified is not a path.
At line:1 char:12
+ Rename-Item  <<<< -Path C:\temp\New.Directory\fileOne c:\temp\fileOne.txt
```

## <a name="moving-items-move-item"></a>Elemek (elem áthelyezése)

Egy fájl vagy mappa áthelyezéséhez használja a **elem áthelyezése** parancsmagot.

Ha például a következő parancsot helyezi át a New.Directory könyvtár a C:\\ideiglenes könyvtárat a C: meghajtó gyökérkönyvtárába. Annak ellenőrzéséhez, hogy az elem került, például a **PassThru** paraméterében a **elem áthelyezése** parancsmagot. Nélkül **Passthru**, a **elem áthelyezése** parancsmag nem jelenít meg eredményt.

```
PS> Move-Item -Path C:\temp\New.Directory -Destination C:\ -PassThru

    Directory: Microsoft.Windows PowerShell.Core\FileSystem::C:\

Mode                LastWriteTime     Length Name
----                -------------     ------ ----
d----        2006-05-18  12:14 PM            New.Directory
```

## <a name="copying-items-copy-item"></a>(Copy-Item) elemek másolása

Ha ismeri a másolási műveletek más ismertetése, viselkedését találhatja a **Copy-Item** parancsmagot a Windows PowerShell a szokatlan. Ha az egyik helyről egy elem másolása egy másik, Copy-Item nem másolja a tartalmát alapértelmezés szerint.

Például, ha másolja a **New.Directory** könyvtárat abból a C: meghajtó a c:\\ideiglenes könyvtárat, a parancs végrehajtása sikeres, de nem másolódnak át a fájlokat a New.Directory címtárban.

```powershell
Copy-Item -Path C:\New.Directory -Destination C:\temp
```

Ha tartalmának megjelenítése **C:\\temp\\New.Directory**, tapasztalni fogja, hogy nem tartalmaz fájlokat:

```
PS> Get-ChildItem -Path C:\temp\New.Directory
PS>
```

Miért nem a **Copy-Item** parancsmagot az új helyre másolja a tartalmat?

A **Copy-Item** parancsmag úgy tervezték, hogy lehet általános; ez már nem csak a fájlok és mappák másolása. Emellett akkor is, ha a fájlok és mappák másolása, érdemes csak a tároló és a nem a benne lévő elemek másolása.

Az összes olyan mappa tartalmát, például a **Recurse** paraméterében a **Copy-Item** parancsmag a parancsban. Már a könyvtárat úgy, hogy a tartalmát másolta, adja hozzá a **kényszerített** paramétert, amely lehetővé teszi, hogy az üres mappa felülírásához.

```
PS> Copy-Item -Path C:\New.Directory -Destination C:\temp -Recurse -Force -Passthru

    Directory: Microsoft.Windows PowerShell.Core\FileSystem::C:\temp

Mode                LastWriteTime     Length Name
----                -------------     ------ ----
d----        2006-05-18   1:53 PM            New.Directory

    Directory: Microsoft.Windows PowerShell.Core\FileSystem::C:\temp\New.Directory

Mode                LastWriteTime     Length Name
----                -------------     ------ ----
-a---        2006-05-18  11:44 AM          0 file1
```

## <a name="deleting-items-remove-item"></a>Elemek (Remove-elem) törlése

Fájlok és mappák törléséhez használja a **Remove-cikk** parancsmagot. Windows PowerShell-parancsmagok, például **Remove-cikk**, végezhetnek jelentős, a végleges módosítások gyakran felkéri megerősítést kér a parancs beírásakor. Például, ha el szeretné távolítani a **New.Directory** mappában, kérni fogja, erősítse meg a parancsot, mert a mappa fájlokat tartalmazza:

```
PS> Remove-Item C:\New.Directory

Confirm
The item at C:\temp\New.Directory has children and the -recurse parameter was not
specified. If you continue, all children will be removed with the item. Are you
 sure you want to continue?
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help
(default is "Y"):
```

Mivel **Igen** az alapértelmezett válasz, törölje a mappát és annak fájljait nyomja le az **Enter** kulcsot. Anélkül, hogy tájékoztat a mappa eltávolításához használja a **-Recurse** paraméter.

```powershell
Remove-Item C:\temp\New.Directory -Recurse
```

## <a name="executing-items-invoke-item"></a>Elemek (Invoke-elem) végrehajtása

Használja a Windows PowerShell a **Invoke-cikk** parancsmag egy fájlhoz vagy mappához tartozó alapértelmezett művelet végrehajtásához. Ez az alapértelmezett művelet határozza meg az alapértelmezett alkalmazás kezelő a beállításjegyzék; a hatás megegyezik szerint, ha duplán kattint a cikk a Fájlkezelőben.

Tegyük fel például, a következő parancsot:

```powershell
Invoke-Item C:\WINDOWS
```

Egy intézőablakot lévő C:\\Windows megjelenik, ugyanúgy, mintha a C: kellett duplán kattintottunk\\Windows mappa.

Ha indít el a **Boot.ini** fájl előtt a Windows Vista rendszeren:

```powershell
Invoke-Item C:\boot.ini
```

Az .ini fájl típusa társítva a Jegyzettömb, ha a boot.ini fájlt a Jegyzettömbben nyílik meg.
