---
ms.date: 06/05/2017
keywords: PowerShell parancsmag
title: Elemek közvetlen módosítása
ms.assetid: 8cbd4867-917d-41ea-9ff0-b8e765509735
ms.openlocfilehash: 688f9194bd16793331325999c69e88df3e94c976
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
ms.locfileid: "30953667"
---
# <a name="manipulating-items-directly"></a>Elemek közvetlen módosítása

A Windows PowerShell-meghajtók, például a fájlok és mappák a fájl rendszer meghajtókon és a beállításkulcsok a Windows PowerShell beállításjegyzék meghajtókon látható elemek nevezzük *elemek* a Windows PowerShellben. A parancsmag szolgálja a őket elem van a főnév **elem** a név.

A kimenetét a **Get-Command - főnév elem** parancs megjeleníti, hogy vannak-e kilenc cikk Windows PowerShell-parancsmagokat.

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

### <a name="creating-new-items-new-item"></a>Új elemek (új elem) létrehozása

A fájlrendszer új elem létrehozásához használja a **új elem** parancsmag. Tartalmazza a **elérési** paraméter a következő elem elérési útja és a **ItemType** paraméter, a "file" vagy "directory" értékű.

Például, hogy hozzon létre egy új könyvtárat neve "New.Directory"in a C:\\Temp könyvtárba, írja be:

```
PS> New-Item -Path c:\temp\New.Directory -ItemType Directory

    Directory: Microsoft.Windows PowerShell.Core\FileSystem::C:\temp

Mode                LastWriteTime     Length Name
----                -------------     ------ ----
d----        2006-05-18  11:29 AM            New.Directory
```

Hozzon létre egy fájlt, módosítsa az értékét a **ItemType** "file" paramétert. Például hozzon létre egy "file1.txt" New.Directory könyvtárban nevű fájlt, írja be:

```
PS> New-Item -Path C:\temp\New.Directory\file1.txt -ItemType file

    Directory: Microsoft.Windows PowerShell.Core\FileSystem::C:\temp\New.Directory

Mode                LastWriteTime     Length Name
----                -------------     ------ ----
-a---        2006-05-18  11:44 AM          0 file1
```

Ugyanaz a technika segítségével hozzon létre egy új beállításkulcsot. Egy beállításkulcs megadásával valójában könnyebben hozható létre, mert a Windows beállításjegyzékében csak elemtípus egy kulcsot. (Beállításjegyzék bejegyzései elem *tulajdonságok*.) Például a CurrentVersion alkulcs "_Test" nevű kulcs létrehozásához írja be:

```
PS> New-Item -Path HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion_Test

   Hive: Microsoft.PowerShell.Core\Registry::HKEY_LOCAL_MACHINE\SOFTWARE\Micros
oft\Windows\CurrentVersion

SKC  VC Name                           Property
---  -- ----                           --------
  0   0 _Test                          {}
```

Amikor beírja a beállításjegyzékbeli elérési út, ne felejtse el feltüntetni a kettőspont (**:**) a Windows PowerShell a meghajtó nevét, HKLM: és HKCU:. A kettőspont nélkül Windows PowerShell nem ismeri fel a meghajtó nevét, az elérési út.

### <a name="why-registry-values-are-not-items"></a>Miért beállításjegyzék-értékek nincsenek elemek

Ha a **Get-ChildItem** elemek kereséséhez egy beállításkulcsot, a parancsmag tényleges beállításjegyzékbeli bejegyzést, és azok értékeit soha nem jelenik.

Például a beállításkulcs **HKEY_LOCAL_MACHINE\\szoftver\\Microsoft\\Windows\\CurrentVersion\\futtatása** általában tartalmaz a több beállításjegyzék-bejegyzések a rendszer indításakor futtatott alkalmazásokat, amelyek jelölik.

Azonban használatakor **Get-ChildItem** látni fogja az összes van a gyermekincidenseket a kulcs kereséséhez a **OptionalComponents** a kulcs alkulcsainak:

```
PS> Get-ChildItem HKLM:\Software\Microsoft\Windows\CurrentVersion\Run

   Hive: Microsoft.PowerShell.Core\Registry::HKEY_LOCAL_MACHINE\Software\Micros
oft\Windows\CurrentVersion\Run
SKC  VC Name                           Property
---  -- ----                           --------
  3   0 OptionalComponents             {}
```

Annak ellenére, hogy szeretné kezelni a beállításjegyzék-bejegyzések elemek kényelmes, oly módon, amely biztosítja, hogy az egyedi nem adható meg a egy beállításjegyzékbeli bejegyzést elérési útját. Az elérési út notation nem különbözteti meg a beállításkulcsot, nevű **futtatása** és a **(alapértelmezett)** beállításjegyzékbeli bejegyzést a **futtatása** alkulcs. Továbbá mert a beállításjegyzék-bejegyzések neve tartalmazhat fordított perjellel (**\\**), ha rendszerleíró bejegyzések elemeket, majd segítségével különböztetheti meg egymástól a nevű beállításjegyzék-bejegyzés nem használhatja az elérési út notation  **Windows\\CurrentVersion\\futtatása** az adott elérési úton található alkulcsot.

### <a name="renaming-existing-items-rename-item"></a>Meglévő elemek (Elemátnevezés) átnevezése

A fájl vagy mappa neve módosításához használja a **Elemátnevezés** parancsmag. A következő parancs módosítja a nevét a **file1.txt** fájl **fileOne.txt**.

```powershell
Rename-Item -Path C:\temp\New.Directory\file1.txt fileOne.txt
```

A **Elemátnevezés** parancsmaggal módosíthatja egy fájl vagy mappa nevét, de az elem nem helyezhető át. A következő parancsot sikertelen lesz, mivel a rendszer megkísérli a New.Directory könyvtárból a fájl áthelyezéséhez a Temp könyvtárba.

```
PS> Rename-Item -Path C:\temp\New.Directory\fileOne.txt c:\temp\fileOne.txt
Rename-Item : Cannot rename because the target specified is not a path.
At line:1 char:12
+ Rename-Item  <<<< -Path C:\temp\New.Directory\fileOne c:\temp\fileOne.txt
```

### <a name="moving-items-move-item"></a>Elemek (elem áthelyezése)

A fájl vagy mappa áthelyezéséhez használja a **elem áthelyezése** parancsmag.

A következő parancs például a New.Directory directory helyez a C:\\ideiglenes könyvtárat a c meghajtó gyökérkönyvtárában. Győződjön meg arról, hogy az elem lett áthelyezve, közé tartozik a **PassThru** paramétere a **elem áthelyezése** parancsmag. Nélkül **Passthru**, a **elem áthelyezése** parancsmag, eredmények nem jelennek meg.

```
PS> Move-Item -Path C:\temp\New.Directory -Destination C:\ -PassThru

    Directory: Microsoft.Windows PowerShell.Core\FileSystem::C:\

Mode                LastWriteTime     Length Name
----                -------------     ------ ----
d----        2006-05-18  12:14 PM            New.Directory
```

### <a name="copying-items-copy-item"></a>Másolás elem (elem)

Ha jártas a másolási műveletek a más ismertetése, bizonyára hasznosnak találja a működését a **elem** szokatlan Windows PowerShell-parancsmagot. Másolásakor elem egyik helyről egy másikra, elem nem másolja át a tartalmát alapértelmezés szerint.

Például, ha másolja a **New.Directory** a C: meghajtó a könyvtárból a C:\\ideiglenes könyvtárat, a parancs végrehajtása sikeres, de nem kerülnek a New.Directory könyvtár.

```powershell
Copy-Item -Path C:\New.Directory -Destination C:\temp
```

Ha tartalmának megjelenítése **C:\\temp\\New.Directory**, látni fogja, hogy egyetlen fájlt tartalmaz:

```
PS> Get-ChildItem -Path C:\temp\New.Directory
PS>
```

Miért nem a **elem** parancsmag másolja az új hely tartalmát?

A **elem** parancsmag úgy lett kialakítva, hogy általános; nem csupán a fájlok és mappák másolása. Emellett akkor is, ha a fájlok és mappák másolása, érdemes csak a tároló és a nem szereplő elemek másolása.

Tartalmazza az összes egy mappa tartalmát, a **Recurse** paramétere a **elem** parancsmag a parancsban. Ha a könyvtár tartalmának nélkül már másolta, vegye fel a **kényszerített** paraméter, amely lehetővé teszi az üres mappa felülírásához.

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

### <a name="deleting-items-remove-item"></a>Elemek (Remove-cikk) törlése

Fájlok és mappák törléséhez használja a **Remove-cikk** parancsmag. A Windows PowerShell-parancsmagok, például a **Remove-cikk**, amely jelentős tehet, végleges változtatások gyakran felkéri megerősítést kér a parancs beírásakor. Például, ha el szeretné távolítani a **New.Directory** mappa, kérni fogja a parancs, mert a mappa fájlokat tartalmazza:

```
PS> Remove-Item C:\New.Directory

Confirm
The item at C:\temp\New.Directory has children and the -recurse parameter was not
specified. If you continue, all children will be removed with the item. Are you
 sure you want to continue?
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help
(default is "Y"):
```

Mivel **Igen** az alapértelmezett válasz, törölje a mappát és annak fájljait, nyomja meg a **Enter** kulcs. A következő mappa eltávolítása nélkül erősítse meg, használja a **-Recurse** paraméter.

```powershell
Remove-Item C:\temp\New.Directory -Recurse
```

### <a name="executing-items-invoke-item"></a>Végrehajtás alatt álló elemek (Invoke-elem)

A Windows PowerShell használja a **Invoke-cikk** parancsmag egy fájl vagy mappa egy alapértelmezett műveletet végrehajtani. Ez az alapértelmezett művelet határozza meg az alapértelmezett alkalmazás kezelő a beállításjegyzékben; a hatás ugyanúgy történik, ha duplán kattint a cikk a Fájlkezelőben is.

Tegyük fel, hogy a következő parancsot:

```powershell
Invoke-Item C:\WINDOWS
```

Egy ablak, amely C: található\\Windows jelenik meg, csak ha rendelkezett duplán kattint a C:\\Windows mappa.

Ha indít a **Boot.ini** fájl előtt a Windows Vista rendszeren:

```powershell
Invoke-Item C:\boot.ini
```

Ha a .ini fájl típusa nem Jegyzettömb társítva, a boot.ini fájl Jegyzettömbben nyílik meg.