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
# <a name="working-with-files-and-folders"></a><span data-ttu-id="60df8-103">Fájlok és mappák használata</span><span class="sxs-lookup"><span data-stu-id="60df8-103">Working with Files and Folders</span></span>

<span data-ttu-id="60df8-104">A Windows PowerShell meghajtókon keresztüli navigálás és a rajtuk lévő elemek módosítása hasonló a fájlok és mappák Windows fizikai lemezmeghajtón való kezeléséhez.</span><span class="sxs-lookup"><span data-stu-id="60df8-104">Navigating through Windows PowerShell drives and manipulating the items on them is similar to manipulating files and folders on Windows physical disk drives.</span></span> <span data-ttu-id="60df8-105">Ebből a szakaszból megtudhatja, hogyan kezelheti a fájlok és mappák kezelésére szolgáló feladatokat a PowerShell használatával.</span><span class="sxs-lookup"><span data-stu-id="60df8-105">This section discusses how to deal with specific file and folder manipulation tasks using PowerShell.</span></span>

## <a name="listing-all-the-files-and-folders-within-a-folder"></a><span data-ttu-id="60df8-106">A mappában található összes fájl és mappa listázása</span><span class="sxs-lookup"><span data-stu-id="60df8-106">Listing All the Files and Folders Within a Folder</span></span>

<span data-ttu-id="60df8-107">A **Get-ChildItem**használatával közvetlenül a mappában található összes elem beolvasható.</span><span class="sxs-lookup"><span data-stu-id="60df8-107">You can get all items directly within a folder by using **Get-ChildItem**.</span></span> <span data-ttu-id="60df8-108">Adja hozzá a nem kötelező **kényszerített** paramétert a rejtett vagy a rendszerelemek megjelenítéséhez.</span><span class="sxs-lookup"><span data-stu-id="60df8-108">Add the optional **Force** parameter to display hidden or system items.</span></span> <span data-ttu-id="60df8-109">Ez a parancs például a C Windows PowerShell-meghajtó közvetlen tartalmát jeleníti meg (amely megegyezik a Windows fizikai meghajtóval):</span><span class="sxs-lookup"><span data-stu-id="60df8-109">For example, this command displays the direct contents of Windows PowerShell Drive C (which is the same as the Windows physical drive C):</span></span>

```powershell
Get-ChildItem -Path C:\ -Force
```

<span data-ttu-id="60df8-110">A parancs csak a közvetlenül foglalt elemeket listázza, hasonlóan a cmd. exe **dir** parancsához vagy az **ls** -hoz egy UNIX-rendszerhéjban.</span><span class="sxs-lookup"><span data-stu-id="60df8-110">The command lists only the directly contained items, much like using Cmd.exe's **DIR** command or **ls** in a UNIX shell.</span></span> <span data-ttu-id="60df8-111">A befoglalt elemek megjelenítéséhez a **-recurse** paramétert is meg kell adnia.</span><span class="sxs-lookup"><span data-stu-id="60df8-111">In order to show contained items, you need to specify the **-Recurse** parameter as well.</span></span> <span data-ttu-id="60df8-112">(Ez nagyon hosszú időt vehet igénybe.) A C meghajtón található összes elem listázása:</span><span class="sxs-lookup"><span data-stu-id="60df8-112">(This can take an extremely long time to complete.) To list everything on the C drive:</span></span>

```powershell
Get-ChildItem -Path C:\ -Force -Recurse
```

<span data-ttu-id="60df8-113">A **Get-ChildItem** képes az elemeket az **elérési úttal**, **szűréssel**, **belefoglalási**és **kizárási** paraméterekkel szűrni, de ezek jellemzően csak a névben alapulnak.</span><span class="sxs-lookup"><span data-stu-id="60df8-113">**Get-ChildItem** can filter items with its **Path**, **Filter**, **Include**, and **Exclude** parameters, but those are typically based only on name.</span></span> <span data-ttu-id="60df8-114">A **Where-Object**lehetőség használatával összetett szűrést végezhet az elemek egyéb tulajdonságai alapján.</span><span class="sxs-lookup"><span data-stu-id="60df8-114">You can perform complex filtering based on other properties of items by using **Where-Object**.</span></span>

<span data-ttu-id="60df8-115">A következő parancs megkeresi az összes olyan végrehajtható fájlt a program Files mappában, amelyet a 2005. október 1. után módosítottak, és amelyek nem kisebbek, mint 1 megabájt, és nem nagyobb 10 megabájtnál:</span><span class="sxs-lookup"><span data-stu-id="60df8-115">The following command finds all executables within the Program Files folder that were last modified after October 1, 2005 and which are neither smaller than 1 megabyte nor larger than 10 megabytes:</span></span>

```powershell
Get-ChildItem -Path $env:ProgramFiles -Recurse -Include *.exe | Where-Object -FilterScript {($_.LastWriteTime -gt '2005-10-01') -and ($_.Length -ge 1mb) -and ($_.Length -le 10mb)}
```

## <a name="copying-files-and-folders"></a><span data-ttu-id="60df8-116">Fájlok és mappák másolása</span><span class="sxs-lookup"><span data-stu-id="60df8-116">Copying Files and Folders</span></span>

<span data-ttu-id="60df8-117">A másolás a másolási **elemmel**történik.</span><span class="sxs-lookup"><span data-stu-id="60df8-117">Copying is done with **Copy-Item**.</span></span> <span data-ttu-id="60df8-118">A következő parancs biztonsági mentést készít a\\c: boot. ini fájlról c:\\boot. bak fájlba:</span><span class="sxs-lookup"><span data-stu-id="60df8-118">The following command backs up C:\\boot.ini to C:\\boot.bak:</span></span>

```powershell
Copy-Item -Path C:\boot.ini -Destination C:\boot.bak
```

<span data-ttu-id="60df8-119">Ha a célfájl már létezik, a másolási kísérlet sikertelen lesz.</span><span class="sxs-lookup"><span data-stu-id="60df8-119">If the destination file already exists, the copy attempt fails.</span></span> <span data-ttu-id="60df8-120">Egy már létező célhely felülírásához használja a **Force** paramétert:</span><span class="sxs-lookup"><span data-stu-id="60df8-120">To overwrite a pre-existing destination, use the **Force** parameter:</span></span>

```powershell
Copy-Item -Path C:\boot.ini -Destination C:\boot.bak -Force
```

<span data-ttu-id="60df8-121">Ez a parancs akkor is működik, ha a célhely írásvédett.</span><span class="sxs-lookup"><span data-stu-id="60df8-121">This command works even when the destination is read-only.</span></span>

<span data-ttu-id="60df8-122">A mappa másolása ugyanúgy működik.</span><span class="sxs-lookup"><span data-stu-id="60df8-122">Folder copying works the same way.</span></span> <span data-ttu-id="60df8-123">Ez a parancs a c\\: Temp\\test1 mappát másolja át a c:\\Temp\\DeleteMe nevű új mappába:</span><span class="sxs-lookup"><span data-stu-id="60df8-123">This command copies the folder C:\\temp\\test1 to the new folder C:\\temp\\DeleteMe recursively:</span></span>

```powershell
Copy-Item C:\temp\test1 -Recurse C:\temp\DeleteMe
```

<span data-ttu-id="60df8-124">Lehetőség van egy kijelölt elem másolására is.</span><span class="sxs-lookup"><span data-stu-id="60df8-124">You can also copy a selection of items.</span></span> <span data-ttu-id="60df8-125">A következő parancs a c-ben bárhol tárolt összes. txt fájlt\\átmásolja a\\c\\: adatfájlból c: Temp szövegbe:</span><span class="sxs-lookup"><span data-stu-id="60df8-125">The following command copies all .txt files contained anywhere in c:\\data to c:\\temp\\text:</span></span>

```powershell
Copy-Item -Filter *.txt -Path c:\data -Recurse -Destination C:\temp\text
```

<span data-ttu-id="60df8-126">Továbbra is használhat más eszközöket a fájlrendszer másolatainak elvégzéséhez.</span><span class="sxs-lookup"><span data-stu-id="60df8-126">You can still use other tools to perform file system copies.</span></span> <span data-ttu-id="60df8-127">Az XCOPY, a ROBOCOPY és a COM-objektumok, például a **Scripting. FileSystemObject,** mind a Windows PowerShellben működnek.</span><span class="sxs-lookup"><span data-stu-id="60df8-127">XCOPY, ROBOCOPY, and COM objects, such as the **Scripting.FileSystemObject,** all work in Windows PowerShell.</span></span> <span data-ttu-id="60df8-128">Használhatja például a Windows Script Host **Scripting. filesystem com** osztályt a c:\\boot. ini fájlról c:\\boot. bak fájlba történő biztonsági mentéshez:</span><span class="sxs-lookup"><span data-stu-id="60df8-128">For example, you can use the Windows Script Host **Scripting.FileSystem COM** class to back up C:\\boot.ini to C:\\boot.bak:</span></span>

```powershell
(New-Object -ComObject Scripting.FileSystemObject).CopyFile('C:\boot.ini', 'C:\boot.bak')
```

## <a name="creating-files-and-folders"></a><span data-ttu-id="60df8-129">Fájlok és mappák létrehozása</span><span class="sxs-lookup"><span data-stu-id="60df8-129">Creating Files and Folders</span></span>

<span data-ttu-id="60df8-130">Az új elemek létrehozása ugyanúgy működik az összes Windows PowerShell-szolgáltatón.</span><span class="sxs-lookup"><span data-stu-id="60df8-130">Creating new items works the same on all Windows PowerShell providers.</span></span> <span data-ttu-id="60df8-131">Ha egy Windows PowerShell-szolgáltató egynél több típusú elemmel rendelkezik – például a fájlrendszer Windows PowerShell-szolgáltatója megkülönbözteti a címtárakat és a fájlokat –, meg kell adnia az elem típusát.</span><span class="sxs-lookup"><span data-stu-id="60df8-131">If a Windows PowerShell provider has more than one type of item—for example, the FileSystem Windows PowerShell provider distinguishes between directories and files—you need to specify the item type.</span></span>

<span data-ttu-id="60df8-132">Ez a parancs egy új, C:\\Temp\\új mappát hoz létre:</span><span class="sxs-lookup"><span data-stu-id="60df8-132">This command creates a new folder C:\\temp\\New Folder:</span></span>

```powershell
New-Item -Path 'C:\temp\New Folder' -ItemType Directory
```

<span data-ttu-id="60df8-133">Ez a parancs létrehoz egy új üres fájlt a\\C\\: Temp\\New Folder file. txt fájlban</span><span class="sxs-lookup"><span data-stu-id="60df8-133">This command creates a new empty file C:\\temp\\New Folder\\file.txt</span></span>

```powershell
New-Item -Path 'C:\temp\New Folder\file.txt' -ItemType File
```

## <a name="removing-all-files-and-folders-within-a-folder"></a><span data-ttu-id="60df8-134">Mappában lévő összes fájl és mappa eltávolítása</span><span class="sxs-lookup"><span data-stu-id="60df8-134">Removing All Files and Folders Within a Folder</span></span>

<span data-ttu-id="60df8-135">Az **Eltávolítás elem**használatával eltávolíthatja a tartalmazott elemeket, de a rendszer felszólítja, hogy erősítse meg az eltávolítást, ha az elem bármi mást tartalmaz.</span><span class="sxs-lookup"><span data-stu-id="60df8-135">You can remove contained items using **Remove-Item**, but you will be prompted to confirm the removal if the item contains anything else.</span></span> <span data-ttu-id="60df8-136">Ha például megpróbálja törölni a C:\\Temp\\DeleteMe mappát, amely más elemeket tartalmaz, a Windows PowerShell a mappa törlése előtt megkéri a megerősítést:</span><span class="sxs-lookup"><span data-stu-id="60df8-136">For example, if you attempt to delete the folder C:\\temp\\DeleteMe that contains other items, Windows PowerShell prompts you for confirmation before deleting the folder:</span></span>

```
Remove-Item -Path C:\temp\DeleteMe

Confirm
The item at C:\temp\DeleteMe has children and the -recurse parameter was not
specified. If you continue, all children will be removed with the item. Are you
sure you want to continue?
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help
(default is "Y"):
```

<span data-ttu-id="60df8-137">Ha nem kívánja megkérdezni az egyes befoglalt elemeket, akkor a **recurse** paramétert kell megadnia:</span><span class="sxs-lookup"><span data-stu-id="60df8-137">If you do not want to be prompted for each contained item, specify the **Recurse** parameter:</span></span>

```powershell
Remove-Item -Path C:\temp\DeleteMe -Recurse
```

## <a name="mapping-a-local-folder-as-a-drive"></a><span data-ttu-id="60df8-138">Helyi mappa leképezése meghajtóként</span><span class="sxs-lookup"><span data-stu-id="60df8-138">Mapping a Local Folder as a drive</span></span>

<span data-ttu-id="60df8-139">A **New-PSDrive** parancs használatával egy helyi mappát is leképezheti.</span><span class="sxs-lookup"><span data-stu-id="60df8-139">You can also map a local folder, using the **New-PSDrive** command.</span></span> <span data-ttu-id="60df8-140">A következő parancs létrehoz egy helyi meghajtót (P: feltört a helyi programfájlok könyvtára), amely csak a PowerShell-munkamenetből látható:</span><span class="sxs-lookup"><span data-stu-id="60df8-140">The following command creates a local drive P: rooted in the local Program Files directory, visible only from the PowerShell session:</span></span>

```powershell
New-PSDrive -Name P -Root $env:ProgramFiles -PSProvider FileSystem
```

<span data-ttu-id="60df8-141">A hálózati meghajtókhoz hasonlóan a Windows PowerShellben leképezett meghajtók azonnal láthatók a Windows PowerShell-rendszerhéjban.</span><span class="sxs-lookup"><span data-stu-id="60df8-141">Just as with network drives, drives mapped within Windows PowerShell are immediately visible to the Windows PowerShell shell.</span></span>
<span data-ttu-id="60df8-142">Ahhoz, hogy egy csatlakoztatott meghajtót a Fájlkezelőből hozzon létre, a **-megmaradás** paraméterre van szükség.</span><span class="sxs-lookup"><span data-stu-id="60df8-142">In order to create a mapped drive visible from File Explorer, the parameter **-Persist** is needed.</span></span> <span data-ttu-id="60df8-143">Azonban csak a távoli elérési utak használhatók továbbra is.</span><span class="sxs-lookup"><span data-stu-id="60df8-143">However, only remote paths can be used with Persist.</span></span>


## <a name="reading-a-text-file-into-an-array"></a><span data-ttu-id="60df8-144">Szöveges fájl olvasása tömbbe</span><span class="sxs-lookup"><span data-stu-id="60df8-144">Reading a Text File into an Array</span></span>

<span data-ttu-id="60df8-145">A szöveges adatokat a leggyakoribb tárolási formátumok egyike egy olyan fájlban található, amely külön, különálló adatelemként kezelt sorokból áll.</span><span class="sxs-lookup"><span data-stu-id="60df8-145">One of the more common storage formats for text data is in a file with separate lines treated as distinct data elements.</span></span> <span data-ttu-id="60df8-146">A **Get-Content** parancsmag egy teljes fájl olvasására használható egy lépésben, ahogy az itt látható:</span><span class="sxs-lookup"><span data-stu-id="60df8-146">The **Get-Content** cmdlet can be used to read an entire file in one step, as shown here:</span></span>

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

<span data-ttu-id="60df8-147">A **Get-Content** már a fájlból beolvasott adatokat tömbként kezeli, és soronként egy elemet.</span><span class="sxs-lookup"><span data-stu-id="60df8-147">**Get-Content** already treats the data read from the file as an array, with one element per line of file content.</span></span> <span data-ttu-id="60df8-148">Ezt a visszaadott tartalom **hosszának** ellenőrzésével ellenőrizheti:</span><span class="sxs-lookup"><span data-stu-id="60df8-148">You can confirm this by checking the **Length** of the returned content:</span></span>

```
PS> (Get-Content -Path C:\boot.ini).Length
6
```

<span data-ttu-id="60df8-149">Ez a parancs akkor hasznos, ha közvetlenül a Windows PowerShellben jeleníti meg az információkat.</span><span class="sxs-lookup"><span data-stu-id="60df8-149">This command is most useful for getting lists of information into Windows PowerShell directly.</span></span> <span data-ttu-id="60df8-150">Például a "C:\\Temp\\domainMembers. txt" fájlban tárolhatja a számítógépek nevét vagy IP-címeit, a fájl minden egyes sorában egy névvel.</span><span class="sxs-lookup"><span data-stu-id="60df8-150">For example, you might store a list of computer names or IP addresses in a file C:\\temp\\domainMembers.txt, with one name on each line of the file.</span></span> <span data-ttu-id="60df8-151">A **Get-Content** paranccsal lekérheti a fájl tartalmát, és elhelyezheti azokat a következő változóban **$Computers**:</span><span class="sxs-lookup"><span data-stu-id="60df8-151">You can use **Get-Content** to retrieve the file contents and put them in the variable **$Computers**:</span></span>

```powershell
$Computers = Get-Content -Path C:\temp\DomainMembers.txt
```

<span data-ttu-id="60df8-152">**$Computers** mostantól egy olyan tömb, amely az egyes elemekben számítógépnevet tartalmaz.</span><span class="sxs-lookup"><span data-stu-id="60df8-152">**$Computers** is now an array containing a computer name in each element.</span></span>
