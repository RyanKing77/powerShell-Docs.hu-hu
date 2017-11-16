---
ms.date: 2017-06-05
keywords: PowerShell parancsmag
title: "Elemek közvetlenül módosítása"
ms.assetid: 8cbd4867-917d-41ea-9ff0-b8e765509735
ms.openlocfilehash: d9aa95dcb0da2e8203cbe32d64b95bf33d914166
ms.sourcegitcommit: 74255f0b5f386a072458af058a15240140acb294
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/03/2017
---
# <a name="manipulating-items-directly"></a><span data-ttu-id="55dd9-103">Elemek közvetlenül módosítása</span><span class="sxs-lookup"><span data-stu-id="55dd9-103">Manipulating Items Directly</span></span>
<span data-ttu-id="55dd9-104">A Windows PowerShell-meghajtók, például a fájlok és mappák a fájl rendszer meghajtókon és a beállításkulcsok a Windows PowerShell beállításjegyzék meghajtókon látható elemek nevezzük *elemek* a Windows PowerShellben.</span><span class="sxs-lookup"><span data-stu-id="55dd9-104">The elements that you see in Windows PowerShell drives, such as the files and folders in the file system drives, and the registry keys in the Windows PowerShell registry drives, are called *items* in Windows PowerShell.</span></span> <span data-ttu-id="55dd9-105">A parancsmag szolgálja a őket elem van a főnév **elem** a név.</span><span class="sxs-lookup"><span data-stu-id="55dd9-105">The cmdlets for working with them item have the noun **Item** in their names.</span></span>

<span data-ttu-id="55dd9-106">A kimenetét a **Get-Command - főnév elem** parancs megjeleníti, hogy vannak-e kilenc cikk Windows PowerShell-parancsmagokat.</span><span class="sxs-lookup"><span data-stu-id="55dd9-106">The output of the **Get-Command -Noun Item** command shows that there are nine Windows PowerShell item cmdlets.</span></span>

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

### <a name="creating-new-items-new-item"></a><span data-ttu-id="55dd9-107">Új elemek (új elem) létrehozása</span><span class="sxs-lookup"><span data-stu-id="55dd9-107">Creating New Items (New-Item)</span></span>
<span data-ttu-id="55dd9-108">A fájlrendszer új elem létrehozásához használja a **új elem** parancsmag.</span><span class="sxs-lookup"><span data-stu-id="55dd9-108">To create a new item in the file system, use the **New-Item** cmdlet.</span></span> <span data-ttu-id="55dd9-109">Tartalmazza a **elérési** paraméter a következő elem elérési útja és a **ItemType** paraméter, a "file" vagy "directory" értékű.</span><span class="sxs-lookup"><span data-stu-id="55dd9-109">Include the **Path** parameter with path to the item, and the **ItemType** parameter with a value of "file" or "directory".</span></span>

<span data-ttu-id="55dd9-110">Például, hogy hozzon létre egy új könyvtárat neve "New.Directory"in a C:\\Temp könyvtárba, írja be:</span><span class="sxs-lookup"><span data-stu-id="55dd9-110">For example, to create a new directory named "New.Directory"in the C:\\Temp directory,  type:</span></span>

```
PS> New-Item -Path c:\temp\New.Directory -ItemType Directory

    Directory: Microsoft.Windows PowerShell.Core\FileSystem::C:\temp

Mode                LastWriteTime     Length Name
----                -------------     ------ ----
d----        2006-05-18  11:29 AM            New.Directory
```

<span data-ttu-id="55dd9-111">Hozzon létre egy fájlt, módosítsa az értékét a **ItemType** "file" paramétert.</span><span class="sxs-lookup"><span data-stu-id="55dd9-111">To create a file, change the value of the **ItemType** parameter to "file".</span></span> <span data-ttu-id="55dd9-112">Például hozzon létre egy "file1.txt" New.Directory könyvtárban nevű fájlt, írja be:</span><span class="sxs-lookup"><span data-stu-id="55dd9-112">For example, to create a file named "file1.txt" in the New.Directory directory, type:</span></span>

```
PS> New-Item -Path C:\temp\New.Directory\file1.txt -ItemType file

    Directory: Microsoft.Windows PowerShell.Core\FileSystem::C:\temp\New.Directory

Mode                LastWriteTime     Length Name
----                -------------     ------ ----
-a---        2006-05-18  11:44 AM          0 file1
```

<span data-ttu-id="55dd9-113">Ugyanaz a technika segítségével hozzon létre egy új beállításkulcsot.</span><span class="sxs-lookup"><span data-stu-id="55dd9-113">You can use the same technique to create a new registry key.</span></span> <span data-ttu-id="55dd9-114">Egy beállításkulcs megadásával valójában könnyebben hozható létre, mert a Windows beállításjegyzékében csak elemtípus egy kulcsot.</span><span class="sxs-lookup"><span data-stu-id="55dd9-114">In fact, a registry key is easier to create because the only item type in the Windows registry is a key.</span></span> <span data-ttu-id="55dd9-115">(Beállításjegyzék bejegyzései elem *tulajdonságok*.) Például a CurrentVersion alkulcs "_Test" nevű kulcs létrehozásához írja be:</span><span class="sxs-lookup"><span data-stu-id="55dd9-115">(Registry entries are item *properties*.) For example, to create a key named "_Test" in the CurrentVersion subkey, type:</span></span>

```
PS> New-Item -Path HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion_Test

   Hive: Microsoft.PowerShell.Core\Registry::HKEY_LOCAL_MACHINE\SOFTWARE\Micros
oft\Windows\CurrentVersion

SKC  VC Name                           Property
---  -- ----                           --------
  0   0 _Test                          {}
```

<span data-ttu-id="55dd9-116">Amikor beírja a beállításjegyzékbeli elérési út, ne felejtse el feltüntetni a kettőspont (**:**) a Windows PowerShell a meghajtó nevét, HKLM: és HKCU:.</span><span class="sxs-lookup"><span data-stu-id="55dd9-116">When typing a registry path, be sure to include the colon (**:**) in the Windows PowerShell drive names, HKLM: and HKCU:.</span></span> <span data-ttu-id="55dd9-117">A kettőspont nélkül Windows PowerShell nem ismeri fel a meghajtó nevét, az elérési út.</span><span class="sxs-lookup"><span data-stu-id="55dd9-117">Without the colon, Windows PowerShell does not recognize the drive name in the path.</span></span>

### <a name="why-registry-values-are-not-items"></a><span data-ttu-id="55dd9-118">Miért beállításjegyzék-értékek nincsenek elemek</span><span class="sxs-lookup"><span data-stu-id="55dd9-118">Why Registry Values are not Items</span></span>
<span data-ttu-id="55dd9-119">Ha a **Get-ChildItem** elemek kereséséhez egy beállításkulcsot, a parancsmag tényleges beállításjegyzékbeli bejegyzést, és azok értékeit soha nem jelenik.</span><span class="sxs-lookup"><span data-stu-id="55dd9-119">When you use the **Get-ChildItem** cmdlet to find the items in a registry key, you will never see actual registry entries or their values.</span></span>

<span data-ttu-id="55dd9-120">Például a beállításkulcs **HKEY_LOCAL_MACHINE\\szoftver\\Microsoft\\Windows\\CurrentVersion\\futtatása** általában tartalmaz a több beállításjegyzék-bejegyzések a rendszer indításakor futtatott alkalmazásokat, amelyek jelölik.</span><span class="sxs-lookup"><span data-stu-id="55dd9-120">For example, the registry key **HKEY_LOCAL_MACHINE\\Software\\Microsoft\\Windows\\CurrentVersion\\Run** usually contains several registry entries that represent applications that run when the system starts.</span></span>

<span data-ttu-id="55dd9-121">Azonban használatakor **Get-ChildItem** látni fogja az összes van a gyermekincidenseket a kulcs kereséséhez a **OptionalComponents** a kulcs alkulcsainak:</span><span class="sxs-lookup"><span data-stu-id="55dd9-121">However, when you use **Get-ChildItem** to look for child items in the key, all you will see is the **OptionalComponents** subkey of the key:</span></span>

```
PS> Get-ChildItem HKLM:\Software\Microsoft\Windows\CurrentVersion\Run
   Hive: Microsoft.PowerShell.Core\Registry::HKEY_LOCAL_MACHINE\Software\Micros
oft\Windows\CurrentVersion\Run
SKC  VC Name                           Property
---  -- ----                           --------
  3   0 OptionalComponents             {}
```

<span data-ttu-id="55dd9-122">Annak ellenére, hogy szeretné kezelni a beállításjegyzék-bejegyzések elemek kényelmes, oly módon, amely biztosítja, hogy az egyedi nem adható meg a egy beállításjegyzékbeli bejegyzést elérési útját.</span><span class="sxs-lookup"><span data-stu-id="55dd9-122">Although it would be convenient to treat registry entries as items, you cannot specify a path to a registry entry in a way that ensures that it is unique.</span></span> <span data-ttu-id="55dd9-123">Az elérési út notation nem különbözteti meg a beállításkulcsot, nevű **futtatása** és a **(alapértelmezett)** beállításjegyzékbeli bejegyzést a **futtatása** alkulcs.</span><span class="sxs-lookup"><span data-stu-id="55dd9-123">The path notation does not distinguish between the registry subkey named **Run** and the **(Default)** registry entry in the **Run** subkey.</span></span> <span data-ttu-id="55dd9-124">Továbbá mert a beállításjegyzék-bejegyzések neve tartalmazhat fordított perjellel (**\\**), ha rendszerleíró bejegyzések elemeket, majd segítségével különböztetheti meg egymástól a nevű beállításjegyzék-bejegyzés nem használhatja az elérési út notation  **Windows\\CurrentVersion\\futtatása** az adott elérési úton található alkulcsot.</span><span class="sxs-lookup"><span data-stu-id="55dd9-124">Furthermore, because registry entry names can contain the backslash character (**\\**), if regsitry entries were items, then you could not use the path notation to distinguish a registry entry named **Windows\\CurrentVersion\\Run** from the subkey that is located in that path.</span></span>

### <a name="renaming-existing-items-rename-item"></a><span data-ttu-id="55dd9-125">Meglévő elemek (Elemátnevezés) átnevezése</span><span class="sxs-lookup"><span data-stu-id="55dd9-125">Renaming Existing Items (Rename-Item)</span></span>
<span data-ttu-id="55dd9-126">A fájl vagy mappa neve módosításához használja a **Elemátnevezés** parancsmag.</span><span class="sxs-lookup"><span data-stu-id="55dd9-126">To change the name of a file or folder, use the **Rename-Item** cmdlet.</span></span> <span data-ttu-id="55dd9-127">A következő parancs módosítja a nevét a **file1.txt** fájl **fileOne.txt**.</span><span class="sxs-lookup"><span data-stu-id="55dd9-127">The following command changes the name of the **file1.txt** file to **fileOne.txt**.</span></span>

```
PS> Rename-Item -Path C:\temp\New.Directory\file1.txt fileOne.txt
```

<span data-ttu-id="55dd9-128">A **Elemátnevezés** parancsmaggal módosíthatja egy fájl vagy mappa nevét, de az elem nem helyezhető át.</span><span class="sxs-lookup"><span data-stu-id="55dd9-128">The **Rename-Item** cmdlet can change the name of a file or a folder, but it cannot move an item.</span></span> <span data-ttu-id="55dd9-129">A következő parancsot sikertelen lesz, mivel a rendszer megkísérli a New.Directory könyvtárból a fájl áthelyezéséhez a Temp könyvtárba.</span><span class="sxs-lookup"><span data-stu-id="55dd9-129">The following command fails because it attempts to move the file from the New.Directory directory to the Temp directory.</span></span>

```
PS> Rename-Item -Path C:\temp\New.Directory\fileOne.txt c:\temp\fileOne.txt
Rename-Item : Cannot rename because the target specified is not a path.
At line:1 char:12
+ Rename-Item  <<<< -Path C:\temp\New.Directory\fileOne c:\temp\fileOne.txt
```

### <a name="moving-items-move-item"></a><span data-ttu-id="55dd9-130">Elemek (elem áthelyezése)</span><span class="sxs-lookup"><span data-stu-id="55dd9-130">Moving Items (Move-Item)</span></span>
<span data-ttu-id="55dd9-131">A fájl vagy mappa áthelyezéséhez használja a **elem áthelyezése** parancsmag.</span><span class="sxs-lookup"><span data-stu-id="55dd9-131">To move a file or folder, use the **Move-Item** cmdlet.</span></span>

<span data-ttu-id="55dd9-132">A következő parancs például a New.Directory directory helyez a C:\\ideiglenes könyvtárat a c meghajtó gyökérkönyvtárában.</span><span class="sxs-lookup"><span data-stu-id="55dd9-132">For example, the following command moves the New.Directory directory from the C:\\temp directory to the root of the C: drive.</span></span> <span data-ttu-id="55dd9-133">Győződjön meg arról, hogy az elem lett áthelyezve, közé tartozik a **PassThru** paramétere a **elem áthelyezése** parancsmag.</span><span class="sxs-lookup"><span data-stu-id="55dd9-133">To verify that the item was moved, include the **PassThru** parameter of the **Move-Item** cmdlet.</span></span> <span data-ttu-id="55dd9-134">Nélkül **Passthru**, a **elem áthelyezése** parancsmag, eredmények nem jelennek meg.</span><span class="sxs-lookup"><span data-stu-id="55dd9-134">Without **Passthru**, the **Move-Item** cmdlet does not display any results.</span></span>

```
PS> Move-Item -Path C:\temp\New.Directory -Destination C:\ -PassThru

    Directory: Microsoft.Windows PowerShell.Core\FileSystem::C:\

Mode                LastWriteTime     Length Name
----                -------------     ------ ----
d----        2006-05-18  12:14 PM            New.Directory
```

### <a name="copying-items-copy-item"></a><span data-ttu-id="55dd9-135">Másolás elem (elem)</span><span class="sxs-lookup"><span data-stu-id="55dd9-135">Copying Items (Copy-Item)</span></span>
<span data-ttu-id="55dd9-136">Ha jártas a másolási műveletek a más ismertetése, bizonyára hasznosnak találja a működését a **elem** szokatlan Windows PowerShell-parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="55dd9-136">If you are familiar with the copy operations in other shells, you might find the behavior of the **Copy-Item** cmdlet in Windows PowerShell to be unusual.</span></span> <span data-ttu-id="55dd9-137">Másolásakor elem egyik helyről egy másikra, elem nem másolja át a tartalmát alapértelmezés szerint.</span><span class="sxs-lookup"><span data-stu-id="55dd9-137">When you copy an item from one location to another, Copy-Item does not copy its contents by default.</span></span>

<span data-ttu-id="55dd9-138">Például, ha másolja a **New.Directory** a C: meghajtó a könyvtárból a C:\\ideiglenes könyvtárat, a parancs végrehajtása sikeres, de nem kerülnek a New.Directory könyvtár.</span><span class="sxs-lookup"><span data-stu-id="55dd9-138">For example, if you copy the **New.Directory** directory from the C: drive to the C:\\temp directory, the command succeeds, but the files in the New.Directory directory are not copied.</span></span>

```
PS> Copy-Item -Path C:\New.Directory -Destination C:\temp
```

<span data-ttu-id="55dd9-139">Ha tartalmának megjelenítése **C:\\temp\\New.Directory**, látni fogja, hogy egyetlen fájlt tartalmaz:</span><span class="sxs-lookup"><span data-stu-id="55dd9-139">If you display the contents of **C:\\temp\\New.Directory**, you will find that it contains no files:</span></span>

```
PS> Get-ChildItem -Path C:\temp\New.Directory
PS>
```

<span data-ttu-id="55dd9-140">Miért nem a **elem** parancsmag másolja az új hely tartalmát?</span><span class="sxs-lookup"><span data-stu-id="55dd9-140">Why doesn't the **Copy-Item** cmdlet copy the contents to the new location?</span></span>

<span data-ttu-id="55dd9-141">A **elem** parancsmag úgy lett kialakítva, hogy általános; nem csupán a fájlok és mappák másolása.</span><span class="sxs-lookup"><span data-stu-id="55dd9-141">The **Copy-Item** cmdlet was designed to be generic; it is not just for copying files and folders.</span></span> <span data-ttu-id="55dd9-142">Emellett akkor is, ha a fájlok és mappák másolása, érdemes csak a tároló és a nem szereplő elemek másolása.</span><span class="sxs-lookup"><span data-stu-id="55dd9-142">Also, even when copying files and folders, you might want to copy only the container and not the items within it.</span></span>

<span data-ttu-id="55dd9-143">Tartalmazza az összes egy mappa tartalmát, a **Recurse** paramétere a **elem** parancsmag a parancsban.</span><span class="sxs-lookup"><span data-stu-id="55dd9-143">To copy all of the contents of a folder, include the **Recurse** parameter of the **Copy-Item** cmdlet in the command.</span></span> <span data-ttu-id="55dd9-144">Ha a könyvtár tartalmának nélkül már másolta, vegye fel a **kényszerített** paraméter, amely lehetővé teszi az üres mappa felülírásához.</span><span class="sxs-lookup"><span data-stu-id="55dd9-144">If you have already copied the directory without its contents, add the **Force** parameter, which allows you to overwrite the empty folder.</span></span>

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

### <a name="deleting-items-remove-item"></a><span data-ttu-id="55dd9-145">Elemek (Remove-cikk) törlése</span><span class="sxs-lookup"><span data-stu-id="55dd9-145">Deleting Items (Remove-Item)</span></span>
<span data-ttu-id="55dd9-146">Fájlok és mappák törléséhez használja a **Remove-cikk** parancsmag.</span><span class="sxs-lookup"><span data-stu-id="55dd9-146">To delete files and folders, use the **Remove-Item** cmdlet.</span></span> <span data-ttu-id="55dd9-147">A Windows PowerShell-parancsmagok, például a **Remove-cikk**, amely jelentős tehet, végleges változtatások gyakran felkéri megerősítést kér a parancs beírásakor.</span><span class="sxs-lookup"><span data-stu-id="55dd9-147">Windows PowerShell cmdlets, such as **Remove-Item**, that can make significant, irreversible changes will often prompt for confirmation when you enter its commands.</span></span> <span data-ttu-id="55dd9-148">Például, ha el szeretné távolítani a **New.Directory** mappa, kérni fogja a parancs, mert a mappa fájlokat tartalmazza:</span><span class="sxs-lookup"><span data-stu-id="55dd9-148">For example, if you try to remove the **New.Directory** folder, you will be prompted to confirm the command, because the folder contains files:</span></span>

```
PS> Remove-Item C:\New.Directory

Confirm
The item at C:\temp\New.Directory has children and the -recurse parameter was not
specified. If you continue, all children will be removed with the item. Are you
 sure you want to continue?
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help
(default is "Y"):
```

<span data-ttu-id="55dd9-149">Mivel **Igen** az alapértelmezett válasz, törölje a mappát és annak fájljait, nyomja meg a **Enter** kulcs.</span><span class="sxs-lookup"><span data-stu-id="55dd9-149">Because **Yes** is the default response, to delete the folder and its files, press the **Enter** key.</span></span> <span data-ttu-id="55dd9-150">A következő mappa eltávolítása nélkül erősítse meg, használja a **-Recurse** paraméter.</span><span class="sxs-lookup"><span data-stu-id="55dd9-150">To remove the folder without confirming, use the **-Recurse** parameter.</span></span>

```
PS> Remove-Item C:\temp\New.Directory -Recurse
```

### <a name="executing-items-invoke-item"></a><span data-ttu-id="55dd9-151">Végrehajtás alatt álló elemek (Invoke-elem)</span><span class="sxs-lookup"><span data-stu-id="55dd9-151">Executing Items (Invoke-Item)</span></span>
<span data-ttu-id="55dd9-152">A Windows PowerShell használja a **Invoke-cikk** parancsmag egy fájl vagy mappa egy alapértelmezett műveletet végrehajtani.</span><span class="sxs-lookup"><span data-stu-id="55dd9-152">Windows PowerShell uses the **Invoke-Item** cmdlet to perform a default action for a file or folder.</span></span> <span data-ttu-id="55dd9-153">Ez az alapértelmezett művelet határozza meg az alapértelmezett alkalmazás kezelő a beállításjegyzékben; a hatás ugyanúgy történik, ha duplán kattint a cikk a Fájlkezelőben is.</span><span class="sxs-lookup"><span data-stu-id="55dd9-153">This default action is determined by the default application handler in the registry; the effect is the same as if you double-click the item in File Explorer.</span></span>

<span data-ttu-id="55dd9-154">Tegyük fel, hogy a következő parancsot:</span><span class="sxs-lookup"><span data-stu-id="55dd9-154">For example, suppose you run the following command:</span></span>

```
PS> Invoke-Item C:\WINDOWS
```

<span data-ttu-id="55dd9-155">Egy ablak, amely C: található\\Windows jelenik meg, csak ha rendelkezett duplán kattint a C:\\Windows mappa.</span><span class="sxs-lookup"><span data-stu-id="55dd9-155">An Explorer window that is located in C:\\Windows appears, just as if you had double-clicked the C:\\Windows folder.</span></span>

<span data-ttu-id="55dd9-156">Ha indít a **Boot.ini** fájl előtt a Windows Vista rendszeren:</span><span class="sxs-lookup"><span data-stu-id="55dd9-156">If you invoke the **Boot.ini** file on a system prior to Windows Vista:</span></span>

```
PS> Invoke-Item C:\boot.ini
```

<span data-ttu-id="55dd9-157">Ha a .ini fájl típusa nem Jegyzettömb társítva, a boot.ini fájl Jegyzettömbben nyílik meg.</span><span class="sxs-lookup"><span data-stu-id="55dd9-157">If the .ini file type is associated with Notepad, the boot.ini file opens in Notepad.</span></span>

