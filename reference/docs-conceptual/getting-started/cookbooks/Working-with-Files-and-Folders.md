---
ms.date: 06/05/2017
keywords: PowerShell parancsmag
title: Fájlok és mappák használata
ms.assetid: c0ceb96b-e708-45f3-803b-d1f61a48f4c1
ms.openlocfilehash: e47ea00c9d90d7e04a7af0cb1348849410a6e357
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="working-with-files-and-folders"></a><span data-ttu-id="b624a-103">Fájlok és mappák használata</span><span class="sxs-lookup"><span data-stu-id="b624a-103">Working with Files and Folders</span></span>

<span data-ttu-id="b624a-104">Windows PowerShell-meghajtókat nézetre lépne, és azokat az elemeket kezelése hasonlít a fájlok és mappák Windows fizikai merevlemezeken kezelésére.</span><span class="sxs-lookup"><span data-stu-id="b624a-104">Navigating through Windows PowerShell drives and manipulating the items on them is similar to manipulating files and folders on Windows physical disk drives.</span></span> <span data-ttu-id="b624a-105">Meghatározott fájlok és mappák adatkezelési feladatok ebben a szakaszban kezelése ismertetik.</span><span class="sxs-lookup"><span data-stu-id="b624a-105">We will discuss how to deal with specific file and folder manipulation tasks in this section.</span></span>

### <a name="listing-all-the-files-and-folders-within-a-folder"></a><span data-ttu-id="b624a-106">A fájlok és mappák egy mappában listázása</span><span class="sxs-lookup"><span data-stu-id="b624a-106">Listing All the Files and Folders Within a Folder</span></span>

<span data-ttu-id="b624a-107">A közvetlenül az egyes mappákban lévő összes elemet is ki **Get-ChildItem**.</span><span class="sxs-lookup"><span data-stu-id="b624a-107">You can get all items directly within a folder by using **Get-ChildItem**.</span></span> <span data-ttu-id="b624a-108">Adja hozzá a választható **kényszerített** rejtett megjelenítése vagy rendszer elemek paraméter.</span><span class="sxs-lookup"><span data-stu-id="b624a-108">Add the optional **Force** parameter to display hidden or system items.</span></span> <span data-ttu-id="b624a-109">A parancs például a Windows PowerShell meghajtót C (Ez ugyanaz, mint a Windows fizikai C meghajtó) közvetlen tartalmát jeleníti meg:</span><span class="sxs-lookup"><span data-stu-id="b624a-109">For example, this command displays the direct contents of Windows PowerShell Drive C (which is the same as the Windows physical drive C):</span></span>

```powershell
Get-ChildItem -Force C:\
```

<span data-ttu-id="b624a-110">A parancs csak közvetlenül a benne lévő elemeket tartalmazza, hasonlóan a Cmd.exe tartozó **DIR** parancs vagy **ls** egy UNIX rendszerhéj.</span><span class="sxs-lookup"><span data-stu-id="b624a-110">The command lists only the directly contained items, much like using Cmd.exe's **DIR** command or **ls** in a UNIX shell.</span></span> <span data-ttu-id="b624a-111">Ahhoz, hogy a benne lévő elemek megjelenítése, meg kell adnia a **-Recurse** paramétert is.</span><span class="sxs-lookup"><span data-stu-id="b624a-111">In order to show contained items, you need to specify the **-Recurse** parameter as well.</span></span> <span data-ttu-id="b624a-112">(Ez egy nagyon hosszú ideig eltarthat.) Minden, a C meghajtó listázásához:</span><span class="sxs-lookup"><span data-stu-id="b624a-112">(This can take an extremely long time to complete.) To list everything on the C drive:</span></span>

```powershell
Get-ChildItem -Force C:\ -Recurse
```

<span data-ttu-id="b624a-113">**Get-ChildItem** elemek szűrheti a **elérési**, **szűrő**, **Include**, és **kizárása** paraméterek, de azokat, amelyek általában csak a neve alapján.</span><span class="sxs-lookup"><span data-stu-id="b624a-113">**Get-ChildItem** can filter items with its **Path**, **Filter**, **Include**, and **Exclude** parameters, but those are typically based only on name.</span></span> <span data-ttu-id="b624a-114">Összetett szűrés használatával-elemek egyéb tulajdonságok alapján hajthat végre **Where-Object**.</span><span class="sxs-lookup"><span data-stu-id="b624a-114">You can perform complex filtering based on other properties of items by using **Where-Object**.</span></span>

<span data-ttu-id="b624a-115">A következő parancsot, amely legutóbbi módosításának 2005. október 1. után, és amelyeket nem kisebb, mint 1 megabájt, és nem nagyobb, mint 10 megabájt, a Program Files mappában található összes végrehajtható talál:</span><span class="sxs-lookup"><span data-stu-id="b624a-115">The following command finds all executables within the Program Files folder that were last modified after October 1, 2005 and which are neither smaller than 1 megabyte nor larger than 10 megabytes:</span></span>

```powershell
Get-ChildItem -Path $env:ProgramFiles -Recurse -Include *.exe | Where-Object -FilterScript {($_.LastWriteTime -gt '2005-10-01') -and ($_.Length -ge 1mb) -and ($_.Length -le 10mb)}
```

### <a name="copying-files-and-folders"></a><span data-ttu-id="b624a-116">Fájlok és mappák másolása</span><span class="sxs-lookup"><span data-stu-id="b624a-116">Copying Files and Folders</span></span>

<span data-ttu-id="b624a-117">Másolás történik a **elem**.</span><span class="sxs-lookup"><span data-stu-id="b624a-117">Copying is done with **Copy-Item**.</span></span> <span data-ttu-id="b624a-118">A következő parancs készít biztonsági másolatot C:\\c: boot.ini\\boot.bak:</span><span class="sxs-lookup"><span data-stu-id="b624a-118">The following command backs up C:\\boot.ini to C:\\boot.bak:</span></span>

```powershell
Copy-Item -Path c:\boot.ini -Destination c:\boot.bak
```

<span data-ttu-id="b624a-119">Ha a célfájl már létezik, a másolási kísérlet meghiúsul.</span><span class="sxs-lookup"><span data-stu-id="b624a-119">If the destination file already exists, the copy attempt fails.</span></span> <span data-ttu-id="b624a-120">Egy már meglévő cél felülírásához használja a Force paramétert:</span><span class="sxs-lookup"><span data-stu-id="b624a-120">To overwrite a pre-existing destination, use the Force parameter:</span></span>

```powershell
Copy-Item -Path c:\boot.ini -Destination c:\boot.bak -Force
```

<span data-ttu-id="b624a-121">Ez a parancs is működik, ha a cél csak olvasható.</span><span class="sxs-lookup"><span data-stu-id="b624a-121">This command works even when the destination is read-only.</span></span>

<span data-ttu-id="b624a-122">Mappa másolása ugyanúgy működik.</span><span class="sxs-lookup"><span data-stu-id="b624a-122">Folder copying works the same way.</span></span> <span data-ttu-id="b624a-123">Ez a parancs, másolja át a mappát a C:\\temp\\az új mappa c: Teszt1\\temp\\DeleteMe rekurzív módon:</span><span class="sxs-lookup"><span data-stu-id="b624a-123">This command copies the folder C:\\temp\\test1 to the new folder c:\\temp\\DeleteMe recursively:</span></span>

```powershell
Copy-Item C:\temp\test1 -Recurse c:\temp\DeleteMe
```

<span data-ttu-id="b624a-124">A kijelölt elemek is másolhatja.</span><span class="sxs-lookup"><span data-stu-id="b624a-124">You can also copy a selection of items.</span></span> <span data-ttu-id="b624a-125">A következő parancsot a c: bármely részén lévő összes .txt fájlt másolja át\\c: adatok\\temp\\szöveg:</span><span class="sxs-lookup"><span data-stu-id="b624a-125">The following command copies all .txt files contained anywhere in c:\\data to c:\\temp\\text:</span></span>

```powershell
Copy-Item -Filter *.txt -Path c:\data -Recurse -Destination c:\temp\text
```

<span data-ttu-id="b624a-126">Más eszközök hajtható végre rendszer továbbra is használhatja.</span><span class="sxs-lookup"><span data-stu-id="b624a-126">You can still use other tools to perform file system copies.</span></span> <span data-ttu-id="b624a-127">XCOPY, a ROBOCOPY és a COM-objektumok, például a **Scripting.FileSystemObject,** összes működik a Windows PowerShellben.</span><span class="sxs-lookup"><span data-stu-id="b624a-127">XCOPY, ROBOCOPY, and COM objects, such as the **Scripting.FileSystemObject,** all work in Windows PowerShell.</span></span> <span data-ttu-id="b624a-128">Például használhatja a Windows Script Host **Scripting.FileSystem COM** osztály biztonsági mentése C:\\c: boot.ini\\boot.bak:</span><span class="sxs-lookup"><span data-stu-id="b624a-128">For example, you can use the Windows Script Host **Scripting.FileSystem COM** class to back up C:\\boot.ini to C:\\boot.bak:</span></span>

```powershell
(New-Object -ComObject Scripting.FileSystemObject).CopyFile('c:\boot.ini', 'c:\boot.bak')
```

### <a name="creating-files-and-folders"></a><span data-ttu-id="b624a-129">Fájlok és mappák létrehozása</span><span class="sxs-lookup"><span data-stu-id="b624a-129">Creating Files and Folders</span></span>

<span data-ttu-id="b624a-130">Új elemek létrehozását működik, az összes Windows PowerShell-szolgáltató.</span><span class="sxs-lookup"><span data-stu-id="b624a-130">Creating new items works the same on all Windows PowerShell providers.</span></span> <span data-ttu-id="b624a-131">Ha egy Windows PowerShell-szolgáltató rendelkezik-e az elem egynél több típus – például a fájlrendszer Windows PowerShell-szolgáltatóval különbözteti meg a könyvtárak és fájlok között – meg kell adnia az elem típusa.</span><span class="sxs-lookup"><span data-stu-id="b624a-131">If a Windows PowerShell provider has more than one type of item—for example, the FileSystem Windows PowerShell provider distinguishes between directories and files—you need to specify the item type.</span></span>

<span data-ttu-id="b624a-132">Ez a parancs létrehoz egy új mappát C:\\temp\\új mappa:</span><span class="sxs-lookup"><span data-stu-id="b624a-132">This command creates a new folder C:\\temp\\New Folder:</span></span>

```powershell
New-Item -Path 'C:\temp\New Folder' -ItemType Directory
```

<span data-ttu-id="b624a-133">Ez a parancs létrehoz egy üres fájlt C:\\temp\\új mappa\\file.txt</span><span class="sxs-lookup"><span data-stu-id="b624a-133">This command creates a new empty file C:\\temp\\New Folder\\file.txt</span></span>

```powershell
New-Item -Path 'C:\temp\New Folder\file.txt' -ItemType File
```

### <a name="removing-all-files-and-folders-within-a-folder"></a><span data-ttu-id="b624a-134">Minden egyes mappákban lévő mappa és eltávolítása</span><span class="sxs-lookup"><span data-stu-id="b624a-134">Removing All Files and Folders Within a Folder</span></span>

<span data-ttu-id="b624a-135">Eltávolíthatja a benne lévő elemek használata **Remove-cikk**, de kérni fogja az eltávolítás megerősítéséhez, ha az elem tartalmaz dolgozott.</span><span class="sxs-lookup"><span data-stu-id="b624a-135">You can remove contained items using **Remove-Item**, but you will be prompted to confirm the removal if the item contains anything else.</span></span> <span data-ttu-id="b624a-136">Például, ha törli a mappát a C: próbál\\temp\\további elemeket tartalmazó DeleteMe, a Windows PowerShell jóváhagyást kér a mappa törlése előtt:</span><span class="sxs-lookup"><span data-stu-id="b624a-136">For example, if you attempt to delete the folder C:\\temp\\DeleteMe that contains other items, Windows PowerShell prompts you for confirmation before deleting the folder:</span></span>

```
Remove-Item C:\temp\DeleteMe

Confirm
The item at C:\temp\DeleteMe has children and the -recurse parameter was not
specified. If you continue, all children will be removed with the item. Are you
sure you want to continue?
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help
(default is "Y"):
```

<span data-ttu-id="b624a-137">Ha nem szeretné, hogy minden benne lévő elemhez kéri, adja meg a **Recurse** paraméter:</span><span class="sxs-lookup"><span data-stu-id="b624a-137">If you do not want to be prompted for each contained item, specify the **Recurse** parameter:</span></span>

```powershell
Remove-Item C:\temp\DeleteMe -Recurse
```

### <a name="mapping-a-local-folder-as-a-windows-accessible-drive"></a><span data-ttu-id="b624a-138">Egy helyi mappába elérhető Windows meghajtóként leképezése</span><span class="sxs-lookup"><span data-stu-id="b624a-138">Mapping a Local Folder as a Windows Accessible Drive</span></span>

<span data-ttu-id="b624a-139">Egy helyi mappát is leképezheti használatával a **subst** parancsot.</span><span class="sxs-lookup"><span data-stu-id="b624a-139">You can also map a local folder, using the **subst** command.</span></span> <span data-ttu-id="b624a-140">A következő parancsot a helyi Program Files mappában hozza létre egy helyi meghajtó P: feltört eszköz:</span><span class="sxs-lookup"><span data-stu-id="b624a-140">The following command creates a local drive P: rooted in the local Program Files directory:</span></span>

```powershell
subst p: $env:programfiles
```

<span data-ttu-id="b624a-141">Ugyanúgy, mint a hálózati meghajtó meghajtó képeznek le a Windows PowerShell használatával **subst** azonnal láthatók a Windows PowerShell felületet.</span><span class="sxs-lookup"><span data-stu-id="b624a-141">Just as with network drives, drives mapped within Windows PowerShell using **subst** are immediately visible to the Windows PowerShell shell.</span></span>

### <a name="reading-a-text-file-into-an-array"></a><span data-ttu-id="b624a-142">A tömb szövegfájlba olvasása</span><span class="sxs-lookup"><span data-stu-id="b624a-142">Reading a Text File into an Array</span></span>

<span data-ttu-id="b624a-143">A gyakori tárolási formátumok tartozó szöveges adatok egyik fájlba a különböző adatelemek számít külön sorban.</span><span class="sxs-lookup"><span data-stu-id="b624a-143">One of the more common storage formats for text data is in a file with separate lines treated as distinct data elements.</span></span> <span data-ttu-id="b624a-144">A **Get-tartalom** parancsmag segítségével olvassa el a teljes fájl egy lépésben, ahogy az itt látható:</span><span class="sxs-lookup"><span data-stu-id="b624a-144">The **Get-Content** cmdlet can be used to read an entire file in one step, as shown here:</span></span>

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

<span data-ttu-id="b624a-145">**Get-tartalom** már kezeli az adatokat a következő fájl olvasásának tömbként fájl tartalma soronként egy elemmel.</span><span class="sxs-lookup"><span data-stu-id="b624a-145">**Get-Content** already treats the data read from the file as an array, with one element per line of file content.</span></span> <span data-ttu-id="b624a-146">Ez alapján ellenőrizheti a **hossza** a visszaadott tartalom:</span><span class="sxs-lookup"><span data-stu-id="b624a-146">You can confirm this by checking the **Length** of the returned content:</span></span>

```
PS> (Get-Content -Path C:\boot.ini).Length
6
```

<span data-ttu-id="b624a-147">Ez a parancs esetén a leghasznosabb tudnak közvetlenül a Windows PowerShell rendszerbe információk listáját.</span><span class="sxs-lookup"><span data-stu-id="b624a-147">This command is most useful for getting lists of information into Windows PowerShell directly.</span></span> <span data-ttu-id="b624a-148">Például akkor lehet, hogy a számítógép nevét vagy IP-címek listáját egy fájlban tárolhatja C:\\temp\\domainMembers.txt, a fájl minden egyes sorban egy névvel.</span><span class="sxs-lookup"><span data-stu-id="b624a-148">For example, you might store a list of computer names or IP addresses in a file C:\\temp\\domainMembers.txt, with one name on each line of the file.</span></span> <span data-ttu-id="b624a-149">Használhat **Get-tartalom** kérhető le a fájl tartalmát, és helyezze őket a változó **$Computers**:</span><span class="sxs-lookup"><span data-stu-id="b624a-149">You can use **Get-Content** to retrieve the file contents and put them in the variable **$Computers**:</span></span>

```powershell
$Computers = Get-Content -Path C:\temp\DomainMembers.txt
```

<span data-ttu-id="b624a-150">**$Computers** mostantól egy tömb egyes elemei a számítógép nevét tartalmazó.</span><span class="sxs-lookup"><span data-stu-id="b624a-150">**$Computers** is now an array containing a computer name in each element.</span></span>