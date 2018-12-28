---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: Fájlok és mappák használata
ms.assetid: c0ceb96b-e708-45f3-803b-d1f61a48f4c1
ms.openlocfilehash: a8d57a1c269d95e692db6c3f1ae10df49e305e4e
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/14/2018
ms.locfileid: "53404184"
---
# <a name="working-with-files-and-folders"></a><span data-ttu-id="f4d9f-103">Fájlok és mappák használata</span><span class="sxs-lookup"><span data-stu-id="f4d9f-103">Working with Files and Folders</span></span>

<span data-ttu-id="f4d9f-104">Navigálás a Windows PowerShell-meghajtók és a rajtuk az elemek módosítása kezelésére szolgáló fizikai merevlemezek Windows található fájlok és mappák hasonlít.</span><span class="sxs-lookup"><span data-stu-id="f4d9f-104">Navigating through Windows PowerShell drives and manipulating the items on them is similar to manipulating files and folders on Windows physical disk drives.</span></span> <span data-ttu-id="f4d9f-105">Ez a szakasz leírja, hogyan meghatározott fájl- és fájlkezelési feladatok PowerShell-lel kezelésére.</span><span class="sxs-lookup"><span data-stu-id="f4d9f-105">This section discusses how to deal with specific file and folder manipulation tasks using PowerShell.</span></span>

### <a name="listing-all-the-files-and-folders-within-a-folder"></a><span data-ttu-id="f4d9f-106">A fájlok és a egy mappában található mappák listázása</span><span class="sxs-lookup"><span data-stu-id="f4d9f-106">Listing All the Files and Folders Within a Folder</span></span>

<span data-ttu-id="f4d9f-107">A közvetlenül egy mappában található minden elemet is kap **Get-ChildItem**.</span><span class="sxs-lookup"><span data-stu-id="f4d9f-107">You can get all items directly within a folder by using **Get-ChildItem**.</span></span> <span data-ttu-id="f4d9f-108">Adja hozzá a választható **kényszerített** rejtettek megjelenítése vagy rendszer elemek paramétert.</span><span class="sxs-lookup"><span data-stu-id="f4d9f-108">Add the optional **Force** parameter to display hidden or system items.</span></span> <span data-ttu-id="f4d9f-109">Ez a parancs például a Windows PowerShell meghajtót C (Ez ugyanaz, mint a Windows fizikai meghajtó C) a közvetlen tartalmát jeleníti meg:</span><span class="sxs-lookup"><span data-stu-id="f4d9f-109">For example, this command displays the direct contents of Windows PowerShell Drive C (which is the same as the Windows physical drive C):</span></span>

```powershell
Get-ChildItem -Path C:\ -Force
```

<span data-ttu-id="f4d9f-110">A parancs felsorolja a csak a közvetlenül benne lévő elemek, hasonlóan a Cmd.exe használatával **DIR** parancs vagy **ls** egy UNIX-rendszerhéjban.</span><span class="sxs-lookup"><span data-stu-id="f4d9f-110">The command lists only the directly contained items, much like using Cmd.exe's **DIR** command or **ls** in a UNIX shell.</span></span> <span data-ttu-id="f4d9f-111">Annak érdekében, hogy a benne lévő elemek megjelenítése, meg kell adnia a **-Recurse** paramétert is.</span><span class="sxs-lookup"><span data-stu-id="f4d9f-111">In order to show contained items, you need to specify the **-Recurse** parameter as well.</span></span> <span data-ttu-id="f4d9f-112">(Ez egy rendkívül hosszú ideig eltarthat.) Minden, a C meghajtó megjelenítése:</span><span class="sxs-lookup"><span data-stu-id="f4d9f-112">(This can take an extremely long time to complete.) To list everything on the C drive:</span></span>

```powershell
Get-ChildItem -Path C:\ -Force -Recurse
```

<span data-ttu-id="f4d9f-113">**Get-ChildItem** szűrheti az elemeket a **elérési**, **szűrő**, **Belefoglalás**, és **kizárása** paraméterek, de ezek is általában csak a neve alapján.</span><span class="sxs-lookup"><span data-stu-id="f4d9f-113">**Get-ChildItem** can filter items with its **Path**, **Filter**, **Include**, and **Exclude** parameters, but those are typically based only on name.</span></span> <span data-ttu-id="f4d9f-114">Összetett szűrését az egyéb elemek tulajdonságai alapján is végezhet **Where-Object**.</span><span class="sxs-lookup"><span data-stu-id="f4d9f-114">You can perform complex filtering based on other properties of items by using **Where-Object**.</span></span>

<span data-ttu-id="f4d9f-115">A következő parancsot, amely utoljára módosítva 2005. október 1. után, és amelyek sem a kisebb, mint 1 megabájt, sem a 10 MB-nál nagyobb a Program Files mappában található megkeresi az összes végrehajtható fájlok:</span><span class="sxs-lookup"><span data-stu-id="f4d9f-115">The following command finds all executables within the Program Files folder that were last modified after October 1, 2005 and which are neither smaller than 1 megabyte nor larger than 10 megabytes:</span></span>

```powershell
Get-ChildItem -Path $env:ProgramFiles -Recurse -Include *.exe | Where-Object -FilterScript {($_.LastWriteTime -gt '2005-10-01') -and ($_.Length -ge 1mb) -and ($_.Length -le 10mb)}
```

### <a name="copying-files-and-folders"></a><span data-ttu-id="f4d9f-116">Fájlok és mappák másolása</span><span class="sxs-lookup"><span data-stu-id="f4d9f-116">Copying Files and Folders</span></span>

<span data-ttu-id="f4d9f-117">Másolás végzett **Copy-Item**.</span><span class="sxs-lookup"><span data-stu-id="f4d9f-117">Copying is done with **Copy-Item**.</span></span> <span data-ttu-id="f4d9f-118">C: készít biztonsági másolatot a következő parancs\\Boot.ini fájlt a C:\\boot.bak:</span><span class="sxs-lookup"><span data-stu-id="f4d9f-118">The following command backs up C:\\boot.ini to C:\\boot.bak:</span></span>

```powershell
Copy-Item -Path C:\boot.ini -Destination C:\boot.bak
```

<span data-ttu-id="f4d9f-119">Ha a célfájl már létezik, a másolási kísérlet meghiúsul.</span><span class="sxs-lookup"><span data-stu-id="f4d9f-119">If the destination file already exists, the copy attempt fails.</span></span> <span data-ttu-id="f4d9f-120">Egy már létező célhelyre felülírásához használja a **kényszerített** paramétert:</span><span class="sxs-lookup"><span data-stu-id="f4d9f-120">To overwrite a pre-existing destination, use the **Force** parameter:</span></span>

```powershell
Copy-Item -Path C:\boot.ini -Destination C:\boot.bak -Force
```

<span data-ttu-id="f4d9f-121">Ez a parancs működik, akkor is, ha a cél csak olvasható.</span><span class="sxs-lookup"><span data-stu-id="f4d9f-121">This command works even when the destination is read-only.</span></span>

<span data-ttu-id="f4d9f-122">Mappa másolása ugyanúgy működik.</span><span class="sxs-lookup"><span data-stu-id="f4d9f-122">Folder copying works the same way.</span></span> <span data-ttu-id="f4d9f-123">Ez a parancs másolja át a C: mappa\\temp\\az új mappába C: Teszt1\\temp\\DeleteMe rekurzív módon:</span><span class="sxs-lookup"><span data-stu-id="f4d9f-123">This command copies the folder C:\\temp\\test1 to the new folder C:\\temp\\DeleteMe recursively:</span></span>

```powershell
Copy-Item C:\temp\test1 -Recurse C:\temp\DeleteMe
```

<span data-ttu-id="f4d9f-124">A kijelölt elemek is másolhatja.</span><span class="sxs-lookup"><span data-stu-id="f4d9f-124">You can also copy a selection of items.</span></span> <span data-ttu-id="f4d9f-125">A következő parancsot az összes, bárhol szerepel a c: .txt fájlt másolja\\c: adatok\\temp\\szöveg:</span><span class="sxs-lookup"><span data-stu-id="f4d9f-125">The following command copies all .txt files contained anywhere in c:\\data to c:\\temp\\text:</span></span>

```powershell
Copy-Item -Filter *.txt -Path c:\data -Recurse -Destination C:\temp\text
```

<span data-ttu-id="f4d9f-126">Más eszközök segítségével továbbra is rendszer fájlmásolás hajtható végre.</span><span class="sxs-lookup"><span data-stu-id="f4d9f-126">You can still use other tools to perform file system copies.</span></span> <span data-ttu-id="f4d9f-127">XCOPY ROBOCOPY és COM-objektumok, például a **Scripting.FileSystemObject,** összes működik a Windows PowerShellben.</span><span class="sxs-lookup"><span data-stu-id="f4d9f-127">XCOPY, ROBOCOPY, and COM objects, such as the **Scripting.FileSystemObject,** all work in Windows PowerShell.</span></span> <span data-ttu-id="f4d9f-128">Például használhatja a Windows Script Host **Scripting.FileSystem COM** biztonsági mentése a C: osztály\\Boot.ini fájlt a C:\\boot.bak:</span><span class="sxs-lookup"><span data-stu-id="f4d9f-128">For example, you can use the Windows Script Host **Scripting.FileSystem COM** class to back up C:\\boot.ini to C:\\boot.bak:</span></span>

```powershell
(New-Object -ComObject Scripting.FileSystemObject).CopyFile('C:\boot.ini', 'C:\boot.bak')
```

### <a name="creating-files-and-folders"></a><span data-ttu-id="f4d9f-129">Fájlok és mappák létrehozása</span><span class="sxs-lookup"><span data-stu-id="f4d9f-129">Creating Files and Folders</span></span>

<span data-ttu-id="f4d9f-130">Új elemek létrehozását ugyanúgy működik az összes Windows PowerShell-szolgáltató.</span><span class="sxs-lookup"><span data-stu-id="f4d9f-130">Creating new items works the same on all Windows PowerShell providers.</span></span> <span data-ttu-id="f4d9f-131">Ha egy Windows PowerShell-szolgáltatóval rendelkezik-e egynél több elem típusa – például a fájlrendszer Windows PowerShell-szolgáltatóban megkülönbözteti könyvtárak és fájlok – meg kell adni az elem típusa.</span><span class="sxs-lookup"><span data-stu-id="f4d9f-131">If a Windows PowerShell provider has more than one type of item—for example, the FileSystem Windows PowerShell provider distinguishes between directories and files—you need to specify the item type.</span></span>

<span data-ttu-id="f4d9f-132">Ez a parancs létrehoz egy új mappát C:\\temp\\új mappa:</span><span class="sxs-lookup"><span data-stu-id="f4d9f-132">This command creates a new folder C:\\temp\\New Folder:</span></span>

```powershell
New-Item -Path 'C:\temp\New Folder' -ItemType Directory
```

<span data-ttu-id="f4d9f-133">Ez a parancs létrehoz egy új üres fájlt C:\\temp\\új mappa\\file.txt</span><span class="sxs-lookup"><span data-stu-id="f4d9f-133">This command creates a new empty file C:\\temp\\New Folder\\file.txt</span></span>

```powershell
New-Item -Path 'C:\temp\New Folder\file.txt' -ItemType File
```

### <a name="removing-all-files-and-folders-within-a-folder"></a><span data-ttu-id="f4d9f-134">Összes fájlt és mappát egy mappában lévő eltávolítása</span><span class="sxs-lookup"><span data-stu-id="f4d9f-134">Removing All Files and Folders Within a Folder</span></span>

<span data-ttu-id="f4d9f-135">Eltávolíthatja a benne lévő elemek használatával **Remove-cikk**, de meg kell adnia az eltávolítás megerősítéséhez, ha az elem tartalmaz bármi más.</span><span class="sxs-lookup"><span data-stu-id="f4d9f-135">You can remove contained items using **Remove-Item**, but you will be prompted to confirm the removal if the item contains anything else.</span></span> <span data-ttu-id="f4d9f-136">Például, ha törli a mappát a C: próbál\\temp\\más elemeket tartalmazó DeleteMe, Windows PowerShell megerősítést kér a felhasználótól a mappa törlése előtt:</span><span class="sxs-lookup"><span data-stu-id="f4d9f-136">For example, if you attempt to delete the folder C:\\temp\\DeleteMe that contains other items, Windows PowerShell prompts you for confirmation before deleting the folder:</span></span>

```
Remove-Item -Path C:\temp\DeleteMe

Confirm
The item at C:\temp\DeleteMe has children and the -recurse parameter was not
specified. If you continue, all children will be removed with the item. Are you
sure you want to continue?
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help
(default is "Y"):
```

<span data-ttu-id="f4d9f-137">Ha nem szeretné, hogy a rendszer minden egyes tartalmazott cikkhez, adja meg a **Recurse** paramétert:</span><span class="sxs-lookup"><span data-stu-id="f4d9f-137">If you do not want to be prompted for each contained item, specify the **Recurse** parameter:</span></span>

```powershell
Remove-Item -Path C:\temp\DeleteMe -Recurse
```

### <a name="mapping-a-local-folder-as-a-windows-accessible-drive"></a><span data-ttu-id="f4d9f-138">Elérhető Windows meghajtóként egy helyi mappába leképezése</span><span class="sxs-lookup"><span data-stu-id="f4d9f-138">Mapping a Local Folder as a Windows Accessible Drive</span></span>

<span data-ttu-id="f4d9f-139">Emellett leképezhet egy helyi mappába használatával a **subst** parancsot.</span><span class="sxs-lookup"><span data-stu-id="f4d9f-139">You can also map a local folder, using the **subst** command.</span></span> <span data-ttu-id="f4d9f-140">A következő parancs létrehoz egy helyi meghajtóra P: feltörték a helyi programfájlok könyvtárban:</span><span class="sxs-lookup"><span data-stu-id="f4d9f-140">The following command creates a local drive P: rooted in the local Program Files directory:</span></span>

```powershell
subst p: $env:programfiles
```

<span data-ttu-id="f4d9f-141">Ugyanúgy mint a hálózati meghajtó, a meghajtók leképezve belül a Windows PowerShell használatával **subst** azonnal láthatók a Windows PowerShell parancshéj.</span><span class="sxs-lookup"><span data-stu-id="f4d9f-141">Just as with network drives, drives mapped within Windows PowerShell using **subst** are immediately visible to the Windows PowerShell shell.</span></span>

### <a name="reading-a-text-file-into-an-array"></a><span data-ttu-id="f4d9f-142">Egy tömbbe egy szöveges fájl olvasása</span><span class="sxs-lookup"><span data-stu-id="f4d9f-142">Reading a Text File into an Array</span></span>

<span data-ttu-id="f4d9f-143">A gyakori tároló formátumok szöveges adatok egyik, egy fájlban, a különböző adatelemek számít külön sorban.</span><span class="sxs-lookup"><span data-stu-id="f4d9f-143">One of the more common storage formats for text data is in a file with separate lines treated as distinct data elements.</span></span> <span data-ttu-id="f4d9f-144">A **Get-tartalom** parancsmag is használható egy teljes fájl egy lépésben elolvasható itt látható módon:</span><span class="sxs-lookup"><span data-stu-id="f4d9f-144">The **Get-Content** cmdlet can be used to read an entire file in one step, as shown here:</span></span>

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

<span data-ttu-id="f4d9f-145">**Get-tartalom** már kezeli egy tömb, a fájl tartalmának soronként egy elemet a fájlból beolvasott adatok.</span><span class="sxs-lookup"><span data-stu-id="f4d9f-145">**Get-Content** already treats the data read from the file as an array, with one element per line of file content.</span></span> <span data-ttu-id="f4d9f-146">Ezt úgy ellenőrizheti a **hossza** a visszaadott tartalom:</span><span class="sxs-lookup"><span data-stu-id="f4d9f-146">You can confirm this by checking the **Length** of the returned content:</span></span>

```
PS> (Get-Content -Path C:\boot.ini).Length
6
```

<span data-ttu-id="f4d9f-147">Ez a parancs esetén a leghasznosabb közvetlenül első listák, amelyek Windows PowerShell segítségével.</span><span class="sxs-lookup"><span data-stu-id="f4d9f-147">This command is most useful for getting lists of information into Windows PowerShell directly.</span></span> <span data-ttu-id="f4d9f-148">Például előfordulhat, hogy tárolása számítógépnevek vagy IP-címek listája egy fájlban C:\\temp\\domainMembers.txt, a fájl minden sorában egy névvel.</span><span class="sxs-lookup"><span data-stu-id="f4d9f-148">For example, you might store a list of computer names or IP addresses in a file C:\\temp\\domainMembers.txt, with one name on each line of the file.</span></span> <span data-ttu-id="f4d9f-149">Használhat **Get-tartalom** beolvasása a fájl tartalmát, és helyezze őket a változó **$Computers**:</span><span class="sxs-lookup"><span data-stu-id="f4d9f-149">You can use **Get-Content** to retrieve the file contents and put them in the variable **$Computers**:</span></span>

```powershell
$Computers = Get-Content -Path C:\temp\DomainMembers.txt
```

<span data-ttu-id="f4d9f-150">**$Computers** már az egyes elemei a számítógép nevét tartalmazó tömb.</span><span class="sxs-lookup"><span data-stu-id="f4d9f-150">**$Computers** is now an array containing a computer name in each element.</span></span>
