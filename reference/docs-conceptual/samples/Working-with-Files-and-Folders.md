---
ms.date: 06/05/2017
keywords: PowerShell, parancsmag
title: Fájlok és mappák használata
ms.openlocfilehash: 743e261d2f5e8bfa39f2731fca7fea6e5678c711
ms.sourcegitcommit: 02eed65c526ef19cf952c2129f280bb5615bf0c8
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/03/2019
ms.locfileid: "70215533"
---
# <a name="working-with-files-and-folders"></a>Fájlok és mappák használata

A Windows PowerShell meghajtókon keresztüli navigálás és a rajtuk lévő elemek módosítása hasonló a fájlok és mappák Windows fizikai lemezmeghajtón való kezeléséhez. Ebből a szakaszból megtudhatja, hogyan kezelheti a fájlok és mappák kezelésére szolgáló feladatokat a PowerShell használatával.

## <a name="listing-all-the-files-and-folders-within-a-folder"></a>A mappában található összes fájl és mappa listázása

A **Get-ChildItem**használatával közvetlenül a mappában található összes elem beolvasható. Adja hozzá a nem kötelező **kényszerített** paramétert a rejtett vagy a rendszerelemek megjelenítéséhez. Ez a parancs például a C Windows PowerShell-meghajtó közvetlen tartalmát jeleníti meg (amely megegyezik a Windows fizikai meghajtóval):

```powershell
Get-ChildItem -Path C:\ -Force
```

A parancs csak a közvetlenül foglalt elemeket listázza, hasonlóan a cmd. exe **dir** parancsához vagy az **ls** -hoz egy UNIX-rendszerhéjban. A befoglalt elemek megjelenítéséhez a **-recurse** paramétert is meg kell adnia. (Ez nagyon hosszú időt vehet igénybe.) A C meghajtón található összes elem listázása:

```powershell
Get-ChildItem -Path C:\ -Force -Recurse
```

A **Get-ChildItem** képes az elemeket az **elérési úttal**, **szűréssel**, **belefoglalási**és **kizárási** paraméterekkel szűrni, de ezek jellemzően csak a névben alapulnak. A **Where-Object**lehetőség használatával összetett szűrést végezhet az elemek egyéb tulajdonságai alapján.

A következő parancs megkeresi az összes olyan végrehajtható fájlt a program Files mappában, amelyet a 2005. október 1. után módosítottak, és amelyek nem kisebbek, mint 1 megabájt, és nem nagyobb 10 megabájtnál:

```powershell
Get-ChildItem -Path $env:ProgramFiles -Recurse -Include *.exe | Where-Object -FilterScript {($_.LastWriteTime -gt '2005-10-01') -and ($_.Length -ge 1mb) -and ($_.Length -le 10mb)}
```

## <a name="copying-files-and-folders"></a>Fájlok és mappák másolása

A másolás a másolási **elemmel**történik. A következő parancs biztonsági mentést készít a\\c: boot. ini fájlról c:\\boot. bak fájlba:

```powershell
Copy-Item -Path C:\boot.ini -Destination C:\boot.bak
```

Ha a célfájl már létezik, a másolási kísérlet sikertelen lesz. Egy már létező célhely felülírásához használja a **Force** paramétert:

```powershell
Copy-Item -Path C:\boot.ini -Destination C:\boot.bak -Force
```

Ez a parancs akkor is működik, ha a célhely írásvédett.

A mappa másolása ugyanúgy működik. Ez a parancs a c\\: Temp\\test1 mappát másolja át a c:\\Temp\\DeleteMe nevű új mappába:

```powershell
Copy-Item C:\temp\test1 -Recurse C:\temp\DeleteMe
```

Lehetőség van egy kijelölt elem másolására is. A következő parancs a c-ben bárhol tárolt összes. txt fájlt\\átmásolja a\\c\\: adatfájlból c: Temp szövegbe:

```powershell
Copy-Item -Filter *.txt -Path c:\data -Recurse -Destination C:\temp\text
```

Továbbra is használhat más eszközöket a fájlrendszer másolatainak elvégzéséhez. Az XCOPY, a ROBOCOPY és a COM-objektumok, például a **Scripting. FileSystemObject,** mind a Windows PowerShellben működnek. Használhatja például a Windows Script Host **Scripting. filesystem com** osztályt a c:\\boot. ini fájlról c:\\boot. bak fájlba történő biztonsági mentéshez:

```powershell
(New-Object -ComObject Scripting.FileSystemObject).CopyFile('C:\boot.ini', 'C:\boot.bak')
```

## <a name="creating-files-and-folders"></a>Fájlok és mappák létrehozása

Az új elemek létrehozása ugyanúgy működik az összes Windows PowerShell-szolgáltatón. Ha egy Windows PowerShell-szolgáltató egynél több típusú elemmel rendelkezik – például a fájlrendszer Windows PowerShell-szolgáltatója megkülönbözteti a címtárakat és a fájlokat –, meg kell adnia az elem típusát.

Ez a parancs egy új, C:\\Temp\\új mappát hoz létre:

```powershell
New-Item -Path 'C:\temp\New Folder' -ItemType Directory
```

Ez a parancs létrehoz egy új üres fájlt a\\C\\: Temp\\New Folder file. txt fájlban

```powershell
New-Item -Path 'C:\temp\New Folder\file.txt' -ItemType File
```

## <a name="removing-all-files-and-folders-within-a-folder"></a>Mappában lévő összes fájl és mappa eltávolítása

Az **Eltávolítás elem**használatával eltávolíthatja a tartalmazott elemeket, de a rendszer felszólítja, hogy erősítse meg az eltávolítást, ha az elem bármi mást tartalmaz. Ha például megpróbálja törölni a C:\\Temp\\DeleteMe mappát, amely más elemeket tartalmaz, a Windows PowerShell a mappa törlése előtt megkéri a megerősítést:

```
Remove-Item -Path C:\temp\DeleteMe

Confirm
The item at C:\temp\DeleteMe has children and the -recurse parameter was not
specified. If you continue, all children will be removed with the item. Are you
sure you want to continue?
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help
(default is "Y"):
```

Ha nem kívánja megkérdezni az egyes befoglalt elemeket, akkor a **recurse** paramétert kell megadnia:

```powershell
Remove-Item -Path C:\temp\DeleteMe -Recurse
```

## <a name="mapping-a-local-folder-as-a-drive"></a>Helyi mappa leképezése meghajtóként

A **New-PSDrive** parancs használatával egy helyi mappát is leképezheti. A következő parancs létrehoz egy helyi meghajtót (P: feltört a helyi programfájlok könyvtára), amely csak a PowerShell-munkamenetből látható:

```powershell
New-PSDrive -Name P -Root $env:ProgramFiles -PSProvider FileSystem
```

A hálózati meghajtókhoz hasonlóan a Windows PowerShellben leképezett meghajtók azonnal láthatók a Windows PowerShell-rendszerhéjban.
Ahhoz, hogy egy csatlakoztatott meghajtót a Fájlkezelőből hozzon létre, a **-megmaradás** paraméterre van szükség. Azonban csak a távoli elérési utak használhatók továbbra is.


## <a name="reading-a-text-file-into-an-array"></a>Szöveges fájl olvasása tömbbe

A szöveges adatokat a leggyakoribb tárolási formátumok egyike egy olyan fájlban található, amely külön, különálló adatelemként kezelt sorokból áll. A **Get-Content** parancsmag egy teljes fájl olvasására használható egy lépésben, ahogy az itt látható:

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

A **Get-Content** már a fájlból beolvasott adatokat tömbként kezeli, és soronként egy elemet. Ezt a visszaadott tartalom **hosszának** ellenőrzésével ellenőrizheti:

```
PS> (Get-Content -Path C:\boot.ini).Length
6
```

Ez a parancs akkor hasznos, ha közvetlenül a Windows PowerShellben jeleníti meg az információkat. Például a "C:\\Temp\\domainMembers. txt" fájlban tárolhatja a számítógépek nevét vagy IP-címeit, a fájl minden egyes sorában egy névvel. A **Get-Content** paranccsal lekérheti a fájl tartalmát, és elhelyezheti azokat a következő változóban **$Computers**:

```powershell
$Computers = Get-Content -Path C:\temp\DomainMembers.txt
```

**$Computers** mostantól egy olyan tömb, amely az egyes elemekben számítógépnevet tartalmaz.
