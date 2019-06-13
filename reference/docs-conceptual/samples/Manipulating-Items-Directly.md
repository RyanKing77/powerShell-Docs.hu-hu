---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: Elemek közvetlen módosítása
ms.openlocfilehash: 50aed569cf6b876297abe3cf1544eba70f6279ce
ms.sourcegitcommit: a6f13c16a535acea279c0ddeca72f1f0d8a8ce4c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2019
ms.locfileid: "67030124"
---
# <a name="manipulating-items-directly"></a><span data-ttu-id="67321-103">Elemek közvetlen módosítása</span><span class="sxs-lookup"><span data-stu-id="67321-103">Manipulating Items Directly</span></span>

<span data-ttu-id="67321-104">A Windows PowerShell-meghajtók, például a fájlokat és mappákat a fájl rendszermeghajtók, és a Windows PowerShell-beállításjegyzék meghajtó, a beállításkulcsok látható elemeket az úgynevezett *elemek* a Windows PowerShellben.</span><span class="sxs-lookup"><span data-stu-id="67321-104">The elements that you see in Windows PowerShell drives, such as the files and folders in the file system drives, and the registry keys in the Windows PowerShell registry drives, are called *items* in Windows PowerShell.</span></span> <span data-ttu-id="67321-105">A parancsmagok a velük végzett munkát elem van a főnév **elem** nevükben.</span><span class="sxs-lookup"><span data-stu-id="67321-105">The cmdlets for working with them item have the noun **Item** in their names.</span></span>

<span data-ttu-id="67321-106">A kimenetét a **Get-Command - főnév elem** -parancs bemutatja, hogy nincsenek-e kilenc Windows PowerShell item-parancsmagokkal.</span><span class="sxs-lookup"><span data-stu-id="67321-106">The output of the **Get-Command -Noun Item** command shows that there are nine Windows PowerShell item cmdlets.</span></span>

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

## <a name="creating-new-items-new-item"></a><span data-ttu-id="67321-107">Új elemek (új elem) létrehozása</span><span class="sxs-lookup"><span data-stu-id="67321-107">Creating New Items (New-Item)</span></span>

<span data-ttu-id="67321-108">A fájlrendszer egy új elem létrehozásához használja a **New-cikk** parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="67321-108">To create a new item in the file system, use the **New-Item** cmdlet.</span></span> <span data-ttu-id="67321-109">Tartalmazza a **elérési** paramétert az elem elérési útja és a **ItemType** paraméter "fájl" vagy "könyvtár" értékkel.</span><span class="sxs-lookup"><span data-stu-id="67321-109">Include the **Path** parameter with path to the item, and the **ItemType** parameter with a value of "file" or "directory".</span></span>

<span data-ttu-id="67321-110">Például, hogy hozzon létre egy új könyvtárat neve "a C: New.Directory"in\\írja be a Temp könyvtárában:</span><span class="sxs-lookup"><span data-stu-id="67321-110">For example, to create a new directory named "New.Directory"in the C:\\Temp directory,  type:</span></span>

```
PS> New-Item -Path c:\temp\New.Directory -ItemType Directory

    Directory: Microsoft.Windows PowerShell.Core\FileSystem::C:\temp

Mode                LastWriteTime     Length Name
----                -------------     ------ ----
d----        2006-05-18  11:29 AM            New.Directory
```

<span data-ttu-id="67321-111">Hozzon létre egy fájlt, módosítsa az értékét a **ItemType** "file" paraméterként.</span><span class="sxs-lookup"><span data-stu-id="67321-111">To create a file, change the value of the **ItemType** parameter to "file".</span></span> <span data-ttu-id="67321-112">Például hozzon létre egy New.Directory a címtárban "file1.txt" nevű fájlt, írja be:</span><span class="sxs-lookup"><span data-stu-id="67321-112">For example, to create a file named "file1.txt" in the New.Directory directory, type:</span></span>

```
PS> New-Item -Path C:\temp\New.Directory\file1.txt -ItemType file

    Directory: Microsoft.Windows PowerShell.Core\FileSystem::C:\temp\New.Directory

Mode                LastWriteTime     Length Name
----                -------------     ------ ----
-a---        2006-05-18  11:44 AM          0 file1
```

<span data-ttu-id="67321-113">Ugyanezen technika használatával hozzon létre egy új beállításkulcsot.</span><span class="sxs-lookup"><span data-stu-id="67321-113">You can use the same technique to create a new registry key.</span></span> <span data-ttu-id="67321-114">Valójában a beállításkulcs lehet egyszerűen hozható létre, mert a csak jelentéselem-típus szerepel a Windows beállításjegyzék-kulcsot.</span><span class="sxs-lookup"><span data-stu-id="67321-114">In fact, a registry key is easier to create because the only item type in the Windows registry is a key.</span></span> <span data-ttu-id="67321-115">(Beállításjegyzék bejegyzései elem *tulajdonságok*.) Írja be például a CurrentVersion alkulcsban "_hitelesítő" nevű kulcs létrehozásához:</span><span class="sxs-lookup"><span data-stu-id="67321-115">(Registry entries are item *properties*.) For example, to create a key named "_Test" in the CurrentVersion subkey, type:</span></span>

```
PS> New-Item -Path HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion_Test

   Hive: Microsoft.PowerShell.Core\Registry::HKEY_LOCAL_MACHINE\SOFTWARE\Micros
oft\Windows\CurrentVersion

SKC  VC Name                           Property
---  -- ----                           --------
  0   0 _Test                          {}
```

<span data-ttu-id="67321-116">Amikor beírja egy beállításjegyzékbeli elérési út, így feltétlenül foglalja bele a kettőspont ( **:** ) a Windows PowerShellben meghajtó a nevek, HKLM: és HKCU:.</span><span class="sxs-lookup"><span data-stu-id="67321-116">When typing a registry path, be sure to include the colon (**:**) in the Windows PowerShell drive names, HKLM: and HKCU:.</span></span> <span data-ttu-id="67321-117">Windows PowerShell a kettőspont nélkül nem ismeri fel a meghajtó nevét, az elérési út.</span><span class="sxs-lookup"><span data-stu-id="67321-117">Without the colon, Windows PowerShell does not recognize the drive name in the path.</span></span>

## <a name="why-registry-values-are-not-items"></a><span data-ttu-id="67321-118">Miért beállításjegyzék értékei nem elemek</span><span class="sxs-lookup"><span data-stu-id="67321-118">Why Registry Values are not Items</span></span>

<span data-ttu-id="67321-119">Használatakor a **Get-ChildItem** parancsmaggal azon elemeinek megkeresése egy beállításkulcsot, soha nem láthatja tényleges beállításjegyzék-bejegyzések és azok értékei.</span><span class="sxs-lookup"><span data-stu-id="67321-119">When you use the **Get-ChildItem** cmdlet to find the items in a registry key, you will never see actual registry entries or their values.</span></span>

<span data-ttu-id="67321-120">Például a beállításkulcs **HKEY_LOCAL_MACHINE\\szoftver\\Microsoft\\Windows\\CurrentVersion\\futtatása** általában tartalmaz számos beállításjegyzék-bejegyzések amelyek az alkalmazások futtatására, amikor a rendszer.</span><span class="sxs-lookup"><span data-stu-id="67321-120">For example, the registry key **HKEY_LOCAL_MACHINE\\Software\\Microsoft\\Windows\\CurrentVersion\\Run** usually contains several registry entries that represent applications that run when the system starts.</span></span>

<span data-ttu-id="67321-121">Azonban, ha használ **Get-ChildItem** keresse ki a kulcsot a gyermekelemek, látni fogja az összes van a **OptionalComponents** a kulcs alkulcs:</span><span class="sxs-lookup"><span data-stu-id="67321-121">However, when you use **Get-ChildItem** to look for child items in the key, all you will see is the **OptionalComponents** subkey of the key:</span></span>

```
PS> Get-ChildItem HKLM:\Software\Microsoft\Windows\CurrentVersion\Run

   Hive: Microsoft.PowerShell.Core\Registry::HKEY_LOCAL_MACHINE\Software\Micros
oft\Windows\CurrentVersion\Run
SKC  VC Name                           Property
---  -- ----                           --------
  3   0 OptionalComponents             {}
```

<span data-ttu-id="67321-122">Annak ellenére, hogy szeretné kezelni a beállításjegyzék-bejegyzések elemek kényelmes, úgy, hogy gondoskodik róla, hogy azt az egyedi nem adható meg a egy beállításjegyzékbeli bejegyzést elérési útját.</span><span class="sxs-lookup"><span data-stu-id="67321-122">Although it would be convenient to treat registry entries as items, you cannot specify a path to a registry entry in a way that ensures that it is unique.</span></span> <span data-ttu-id="67321-123">Az elérési út jelölés nem különbözteti meg a beállításkulcsot nevű **futtatása** és a **(alapértelmezett)** beállításjegyzékbeli bejegyzést a **futtatása** alkulcs.</span><span class="sxs-lookup"><span data-stu-id="67321-123">The path notation does not distinguish between the registry subkey named **Run** and the **(Default)** registry entry in the **Run** subkey.</span></span> <span data-ttu-id="67321-124">Továbbá mert a beállításjegyzék-bejegyzések neve tartalmazhat fordított perjellel ( **\\** ), ha beállításjegyzék-bejegyzések elemet, majd különbséget tenni egy nevű beállításjegyzék-bejegyzés nem tudta használni az elérési út jelöléssel  **Windows\\CurrentVersion\\futtatása** származó az alkulcs az adott elérési úton található.</span><span class="sxs-lookup"><span data-stu-id="67321-124">Furthermore, because registry entry names can contain the backslash character (**\\**), if registry entries were items, then you could not use the path notation to distinguish a registry entry named **Windows\\CurrentVersion\\Run** from the subkey that is located in that path.</span></span>

## <a name="renaming-existing-items-rename-item"></a><span data-ttu-id="67321-125">Meglévő elemeket (Rename-elem) átnevezése</span><span class="sxs-lookup"><span data-stu-id="67321-125">Renaming Existing Items (Rename-Item)</span></span>

<span data-ttu-id="67321-126">Egy fájl vagy mappa neve módosításához használja a **Rename-cikk** parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="67321-126">To change the name of a file or folder, use the **Rename-Item** cmdlet.</span></span> <span data-ttu-id="67321-127">A következő parancs módosítja a nevét a **file1.txt** fájlt **fileOne.txt**.</span><span class="sxs-lookup"><span data-stu-id="67321-127">The following command changes the name of the **file1.txt** file to **fileOne.txt**.</span></span>

```powershell
Rename-Item -Path C:\temp\New.Directory\file1.txt fileOne.txt
```

<span data-ttu-id="67321-128">A **Rename-cikk** parancsmaggal módosíthatja egy fájl vagy mappa nevét, de egy elem nem helyezhető át.</span><span class="sxs-lookup"><span data-stu-id="67321-128">The **Rename-Item** cmdlet can change the name of a file or a folder, but it cannot move an item.</span></span> <span data-ttu-id="67321-129">A következő parancs sikertelen lesz, mivel megkísérli helyezze át a fájlt a New.Directory-könyvtár Temp könyvtárában.</span><span class="sxs-lookup"><span data-stu-id="67321-129">The following command fails because it attempts to move the file from the New.Directory directory to the Temp directory.</span></span>

```
PS> Rename-Item -Path C:\temp\New.Directory\fileOne.txt c:\temp\fileOne.txt
Rename-Item : Cannot rename because the target specified is not a path.
At line:1 char:12
+ Rename-Item  <<<< -Path C:\temp\New.Directory\fileOne c:\temp\fileOne.txt
```

## <a name="moving-items-move-item"></a><span data-ttu-id="67321-130">Elemek (elem áthelyezése)</span><span class="sxs-lookup"><span data-stu-id="67321-130">Moving Items (Move-Item)</span></span>

<span data-ttu-id="67321-131">Egy fájl vagy mappa áthelyezéséhez használja a **elem áthelyezése** parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="67321-131">To move a file or folder, use the **Move-Item** cmdlet.</span></span>

<span data-ttu-id="67321-132">Ha például a következő parancsot helyezi át a New.Directory könyvtár a C:\\ideiglenes könyvtárat a C: meghajtó gyökérkönyvtárába.</span><span class="sxs-lookup"><span data-stu-id="67321-132">For example, the following command moves the New.Directory directory from the C:\\temp directory to the root of the C: drive.</span></span> <span data-ttu-id="67321-133">Annak ellenőrzéséhez, hogy az elem került, például a **PassThru** paraméterében a **elem áthelyezése** parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="67321-133">To verify that the item was moved, include the **PassThru** parameter of the **Move-Item** cmdlet.</span></span> <span data-ttu-id="67321-134">Nélkül **Passthru**, a **elem áthelyezése** parancsmag nem jelenít meg eredményt.</span><span class="sxs-lookup"><span data-stu-id="67321-134">Without **Passthru**, the **Move-Item** cmdlet does not display any results.</span></span>

```
PS> Move-Item -Path C:\temp\New.Directory -Destination C:\ -PassThru

    Directory: Microsoft.Windows PowerShell.Core\FileSystem::C:\

Mode                LastWriteTime     Length Name
----                -------------     ------ ----
d----        2006-05-18  12:14 PM            New.Directory
```

## <a name="copying-items-copy-item"></a><span data-ttu-id="67321-135">(Copy-Item) elemek másolása</span><span class="sxs-lookup"><span data-stu-id="67321-135">Copying Items (Copy-Item)</span></span>

<span data-ttu-id="67321-136">Ha ismeri a másolási műveletek más ismertetése, viselkedését találhatja a **Copy-Item** parancsmagot a Windows PowerShell a szokatlan.</span><span class="sxs-lookup"><span data-stu-id="67321-136">If you are familiar with the copy operations in other shells, you might find the behavior of the **Copy-Item** cmdlet in Windows PowerShell to be unusual.</span></span> <span data-ttu-id="67321-137">Ha az egyik helyről egy elem másolása egy másik, Copy-Item nem másolja a tartalmát alapértelmezés szerint.</span><span class="sxs-lookup"><span data-stu-id="67321-137">When you copy an item from one location to another, Copy-Item does not copy its contents by default.</span></span>

<span data-ttu-id="67321-138">Például, ha másolja a **New.Directory** könyvtárat abból a C: meghajtó a c:\\ideiglenes könyvtárat, a parancs végrehajtása sikeres, de nem másolódnak át a fájlokat a New.Directory címtárban.</span><span class="sxs-lookup"><span data-stu-id="67321-138">For example, if you copy the **New.Directory** directory from the C: drive to the C:\\temp directory, the command succeeds, but the files in the New.Directory directory are not copied.</span></span>

```powershell
Copy-Item -Path C:\New.Directory -Destination C:\temp
```

<span data-ttu-id="67321-139">Ha tartalmának megjelenítése **C:\\temp\\New.Directory**, tapasztalni fogja, hogy nem tartalmaz fájlokat:</span><span class="sxs-lookup"><span data-stu-id="67321-139">If you display the contents of **C:\\temp\\New.Directory**, you will find that it contains no files:</span></span>

```
PS> Get-ChildItem -Path C:\temp\New.Directory
PS>
```

<span data-ttu-id="67321-140">Miért nem a **Copy-Item** parancsmagot az új helyre másolja a tartalmat?</span><span class="sxs-lookup"><span data-stu-id="67321-140">Why doesn't the **Copy-Item** cmdlet copy the contents to the new location?</span></span>

<span data-ttu-id="67321-141">A **Copy-Item** parancsmag úgy tervezték, hogy lehet általános; ez már nem csak a fájlok és mappák másolása.</span><span class="sxs-lookup"><span data-stu-id="67321-141">The **Copy-Item** cmdlet was designed to be generic; it is not just for copying files and folders.</span></span> <span data-ttu-id="67321-142">Emellett akkor is, ha a fájlok és mappák másolása, érdemes csak a tároló és a nem a benne lévő elemek másolása.</span><span class="sxs-lookup"><span data-stu-id="67321-142">Also, even when copying files and folders, you might want to copy only the container and not the items within it.</span></span>

<span data-ttu-id="67321-143">Az összes olyan mappa tartalmát, például a **Recurse** paraméterében a **Copy-Item** parancsmag a parancsban.</span><span class="sxs-lookup"><span data-stu-id="67321-143">To copy all of the contents of a folder, include the **Recurse** parameter of the **Copy-Item** cmdlet in the command.</span></span> <span data-ttu-id="67321-144">Már a könyvtárat úgy, hogy a tartalmát másolta, adja hozzá a **kényszerített** paramétert, amely lehetővé teszi, hogy az üres mappa felülírásához.</span><span class="sxs-lookup"><span data-stu-id="67321-144">If you have already copied the directory without its contents, add the **Force** parameter, which allows you to overwrite the empty folder.</span></span>

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

## <a name="deleting-items-remove-item"></a><span data-ttu-id="67321-145">Elemek (Remove-elem) törlése</span><span class="sxs-lookup"><span data-stu-id="67321-145">Deleting Items (Remove-Item)</span></span>

<span data-ttu-id="67321-146">Fájlok és mappák törléséhez használja a **Remove-cikk** parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="67321-146">To delete files and folders, use the **Remove-Item** cmdlet.</span></span> <span data-ttu-id="67321-147">Windows PowerShell-parancsmagok, például **Remove-cikk**, végezhetnek jelentős, a végleges módosítások gyakran felkéri megerősítést kér a parancs beírásakor.</span><span class="sxs-lookup"><span data-stu-id="67321-147">Windows PowerShell cmdlets, such as **Remove-Item**, that can make significant, irreversible changes will often prompt for confirmation when you enter its commands.</span></span> <span data-ttu-id="67321-148">Például, ha el szeretné távolítani a **New.Directory** mappában, kérni fogja, erősítse meg a parancsot, mert a mappa fájlokat tartalmazza:</span><span class="sxs-lookup"><span data-stu-id="67321-148">For example, if you try to remove the **New.Directory** folder, you will be prompted to confirm the command, because the folder contains files:</span></span>

```
PS> Remove-Item C:\New.Directory

Confirm
The item at C:\temp\New.Directory has children and the -recurse parameter was not
specified. If you continue, all children will be removed with the item. Are you
 sure you want to continue?
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help
(default is "Y"):
```

<span data-ttu-id="67321-149">Mivel **Igen** az alapértelmezett válasz, törölje a mappát és annak fájljait nyomja le az **Enter** kulcsot.</span><span class="sxs-lookup"><span data-stu-id="67321-149">Because **Yes** is the default response, to delete the folder and its files, press the **Enter** key.</span></span> <span data-ttu-id="67321-150">Anélkül, hogy tájékoztat a mappa eltávolításához használja a **-Recurse** paraméter.</span><span class="sxs-lookup"><span data-stu-id="67321-150">To remove the folder without confirming, use the **-Recurse** parameter.</span></span>

```powershell
Remove-Item C:\temp\New.Directory -Recurse
```

## <a name="executing-items-invoke-item"></a><span data-ttu-id="67321-151">Elemek (Invoke-elem) végrehajtása</span><span class="sxs-lookup"><span data-stu-id="67321-151">Executing Items (Invoke-Item)</span></span>

<span data-ttu-id="67321-152">Használja a Windows PowerShell a **Invoke-cikk** parancsmag egy fájlhoz vagy mappához tartozó alapértelmezett művelet végrehajtásához.</span><span class="sxs-lookup"><span data-stu-id="67321-152">Windows PowerShell uses the **Invoke-Item** cmdlet to perform a default action for a file or folder.</span></span> <span data-ttu-id="67321-153">Ez az alapértelmezett művelet határozza meg az alapértelmezett alkalmazás kezelő a beállításjegyzék; a hatás megegyezik szerint, ha duplán kattint a cikk a Fájlkezelőben.</span><span class="sxs-lookup"><span data-stu-id="67321-153">This default action is determined by the default application handler in the registry; the effect is the same as if you double-click the item in File Explorer.</span></span>

<span data-ttu-id="67321-154">Tegyük fel például, a következő parancsot:</span><span class="sxs-lookup"><span data-stu-id="67321-154">For example, suppose you run the following command:</span></span>

```powershell
Invoke-Item C:\WINDOWS
```

<span data-ttu-id="67321-155">Egy intézőablakot lévő C:\\Windows megjelenik, ugyanúgy, mintha a C: kellett duplán kattintottunk\\Windows mappa.</span><span class="sxs-lookup"><span data-stu-id="67321-155">An Explorer window that is located in C:\\Windows appears, just as if you had double-clicked the C:\\Windows folder.</span></span>

<span data-ttu-id="67321-156">Ha indít el a **Boot.ini** fájl előtt a Windows Vista rendszeren:</span><span class="sxs-lookup"><span data-stu-id="67321-156">If you invoke the **Boot.ini** file on a system prior to Windows Vista:</span></span>

```powershell
Invoke-Item C:\boot.ini
```

<span data-ttu-id="67321-157">Az .ini fájl típusa társítva a Jegyzettömb, ha a boot.ini fájlt a Jegyzettömbben nyílik meg.</span><span class="sxs-lookup"><span data-stu-id="67321-157">If the .ini file type is associated with Notepad, the boot.ini file opens in Notepad.</span></span>
