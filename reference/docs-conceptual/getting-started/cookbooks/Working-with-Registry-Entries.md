---
ms.date: 2017-06-05
keywords: PowerShell parancsmag
title: "Beállításjegyzék-bejegyzések használata"
ms.assetid: fd254570-27ac-4cc9-81d4-011afd29b7dc
ms.openlocfilehash: 039203a1a6549d4ba33424a278e4803a5e143d4d
ms.sourcegitcommit: 74255f0b5f386a072458af058a15240140acb294
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/03/2017
---
# <a name="working-with-registry-entries"></a><span data-ttu-id="977c6-103">Beállításjegyzék-bejegyzések használata</span><span class="sxs-lookup"><span data-stu-id="977c6-103">Working with Registry Entries</span></span>
<span data-ttu-id="977c6-104">Mivel a beállításjegyzék-bejegyzések kulcsok tulajdonságainak, és mint ilyen, nem közvetlenül tallózható, igazolnia kell némileg eltérő megközelítést hajtson végre hozzájuk.</span><span class="sxs-lookup"><span data-stu-id="977c6-104">Because registry entries are properties of keys and, as such, cannot be directly browsed, we need to take a slightly different approach when working with them.</span></span>

### <a name="listing-registry-entries"></a><span data-ttu-id="977c6-105">Beállításjegyzék-bejegyzések listázása</span><span class="sxs-lookup"><span data-stu-id="977c6-105">Listing Registry Entries</span></span>
<span data-ttu-id="977c6-106">Vizsgálja meg a beállításjegyzék-bejegyzések számos különböző módja van.</span><span class="sxs-lookup"><span data-stu-id="977c6-106">There are many different ways to examine registry entries.</span></span> <span data-ttu-id="977c6-107">A legegyszerűbb módja a beolvasni a tulajdonság nevét, a kulcshoz tartozó.</span><span class="sxs-lookup"><span data-stu-id="977c6-107">The simplest way is to get the property names associated with a key.</span></span> <span data-ttu-id="977c6-108">Ahhoz, hogy a beállításkulcs bejegyzések például **HKEY_LOCAL_MACHINE\\szoftver\\Microsoft\\Windows\\CurrentVersion**, használjon **Get-elem** .</span><span class="sxs-lookup"><span data-stu-id="977c6-108">For example, to see the names of the entries in the registry key **HKEY_LOCAL_MACHINE\\Software\\Microsoft\\Windows\\CurrentVersion**, use **Get-Item**.</span></span> <span data-ttu-id="977c6-109">Beállításkulcsok rendelkezik tulajdonsággal általános nevű, "Property" Ez a kulcs a beállításjegyzék-bejegyzések listáját.</span><span class="sxs-lookup"><span data-stu-id="977c6-109">Registry keys have a property with the generic name of "Property" that is a list of registry entries in the key.</span></span> <span data-ttu-id="977c6-110">A következő parancsot a tulajdonság-tulajdonság kiválasztása, és kibontja az elemeket, hogy egy listán jelennek:</span><span class="sxs-lookup"><span data-stu-id="977c6-110">The following command selects the Property property and expands the items so that they are displayed in a list:</span></span>

```
PS> Get-Item -Path Registry::HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion | Select-Object -ExpandProperty Property
DevicePath
MediaPathUnexpanded
ProgramFilesDir
CommonFilesDir
ProductId
```

<span data-ttu-id="977c6-111">Segítségével olvashatóbb formátumban tekintheti a beállításjegyzék-bejegyzések **Get-ItemProperty**:</span><span class="sxs-lookup"><span data-stu-id="977c6-111">To view the registry entries in a more readable form, use **Get-ItemProperty**:</span></span>

```
PS> Get-ItemProperty -Path Registry::HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion

PSPath              : Microsoft.PowerShell.Core\Registry::HKEY_LOCAL_MACHINE\SO
                      FTWARE\Microsoft\Windows\CurrentVersion
PSParentPath        : Microsoft.PowerShell.Core\Registry::HKEY_LOCAL_MACHINE\SO
                      FTWARE\Microsoft\Windows
PSChildName         : CurrentVersion
PSDrive             : HKLM
PSProvider          : Microsoft.PowerShell.Core\Registry
DevicePath          : C:\WINDOWS\inf
MediaPathUnexpanded : C:\WINDOWS\Media
ProgramFilesDir     : C:\Program Files
CommonFilesDir      : C:\Program Files\Common Files
ProductId           : 76487-338-1167776-22465
WallPaperDir        : C:\WINDOWS\Web\Wallpaper
MediaPath           : C:\WINDOWS\Media
ProgramFilesPath    : C:\Program Files
PF_AccessoriesName  : Accessories
(default)           :
```

<span data-ttu-id="977c6-112">A kulcs a Windows PowerShell-kapcsolódó tulajdonságok vannak összes előzi meg a "PS", például a **PSPath**, **PSParentPath**, **PSChildName**, és **PSProvider** .</span><span class="sxs-lookup"><span data-stu-id="977c6-112">The Windows PowerShell-related properties for the key are all prefixed with "PS", such as **PSPath**, **PSParentPath**, **PSChildName**, and **PSProvider**.</span></span>

<span data-ttu-id="977c6-113">Használhatja a "**.**" jelölése a jelenlegi helyre hivatkozik.</span><span class="sxs-lookup"><span data-stu-id="977c6-113">You can use the "**.**" notation for referring to the current location.</span></span> <span data-ttu-id="977c6-114">Használhat **hely beállítása** átállítása a **CurrentVersion** beállításjegyzék tároló első:</span><span class="sxs-lookup"><span data-stu-id="977c6-114">You can use **Set-Location** to change to the **CurrentVersion** registry container first:</span></span>

```
Set-Location -Path Registry::HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion
```

<span data-ttu-id="977c6-115">Másik lehetőségként használhatja a beépített HKLM PSDrive rendelkező **hely beállítása**:</span><span class="sxs-lookup"><span data-stu-id="977c6-115">Alternatively, you can use the built-in HKLM PSDrive with **Set-Location**:</span></span>

```
Set-Location -Path hklm:\SOFTWARE\Microsoft\Windows\CurrentVersion
```

<span data-ttu-id="977c6-116">Ezután használhatja a "**.**" jelöléssel a jelenlegi helyhez egy teljes elérési út megadása nélkül a tulajdonságok listázásához:</span><span class="sxs-lookup"><span data-stu-id="977c6-116">You can then use the "**.**" notation for the current location to list the properties without specifying a full path:</span></span>

```
PS> Get-ItemProperty -Path .
...
DevicePath          : C:\WINDOWS\inf
MediaPathUnexpanded : C:\WINDOWS\Media
ProgramFilesDir     : C:\Program Files
...
```

<span data-ttu-id="977c6-117">Elérési út bővítése ugyanúgy működik, mint a fájlrendszeren belül a következő helyről érheti a **ItemProperty** listázásakor **HKLM:\\szoftver\\Microsoft\\Windows \\Súgó** használatával **Get-ItemProperty-elérési út... \\Súgó**.</span><span class="sxs-lookup"><span data-stu-id="977c6-117">Path expansion works the same as it does within the file system, so from this location you can get the **ItemProperty** listing for **HKLM:\\SOFTWARE\\Microsoft\\Windows\\Help** by using **Get-ItemProperty -Path ..\\Help**.</span></span>

### <a name="getting-a-single-registry-entry"></a><span data-ttu-id="977c6-118">Egyetlen bejegyzés beolvasása</span><span class="sxs-lookup"><span data-stu-id="977c6-118">Getting a Single Registry Entry</span></span>
<span data-ttu-id="977c6-119">Ha szeretné beolvasni egy meghatározott bejegyzés egy beállításkulcsot, több lehetséges módszer egyikét használhatja.</span><span class="sxs-lookup"><span data-stu-id="977c6-119">If you want to retrieve a specific entry in a registry key, you can use one of several possible approaches.</span></span> <span data-ttu-id="977c6-120">Ebben a példában a értékének megkeresése **DevicePath** a **HKEY_LOCAL_MACHINE\\szoftver\\Microsoft\\Windows\\CurrentVersion**.</span><span class="sxs-lookup"><span data-stu-id="977c6-120">This example finds the value of **DevicePath** in **HKEY_LOCAL_MACHINE\\SOFTWARE\\Microsoft\\Windows\\CurrentVersion**.</span></span>

<span data-ttu-id="977c6-121">Használatával **Get-ItemProperty**, használja a **elérési** paraméterrel adhatja meg a kulcs nevét és a **neve** paraméterrel adhatja meg a nevét a **DevicePath** bejegyzés.</span><span class="sxs-lookup"><span data-stu-id="977c6-121">Using **Get-ItemProperty**, use the **Path** parameter to specify the name of the key, and the **Name** parameter to specify the name of the **DevicePath** entry.</span></span>

```
PS> Get-ItemProperty -Path HKLM:\Software\Microsoft\Windows\CurrentVersion -Name DevicePath

PSPath       : Microsoft.PowerShell.Core\Registry::HKEY_LOCAL_MACHINE\Software\
               Microsoft\Windows\CurrentVersion
PSParentPath : Microsoft.PowerShell.Core\Registry::HKEY_LOCAL_MACHINE\Software\
               Microsoft\Windows
PSChildName  : CurrentVersion
PSDrive      : HKLM
PSProvider   : Microsoft.PowerShell.Core\Registry
DevicePath   : C:\WINDOWS\inf
```

<span data-ttu-id="977c6-122">Ez a parancs visszaadja a szabványos Windows PowerShell tulajdonságait, valamint a **DevicePath** tulajdonság.</span><span class="sxs-lookup"><span data-stu-id="977c6-122">This command returns the standard Windows PowerShell properties as well as the **DevicePath** property.</span></span>

> [!NOTE]
> <span data-ttu-id="977c6-123">Bár **Get-ItemProperty** rendelkezik **szűrő**, **Include**, és **kizárása** paraméterek, a szűréshez tulajdonság neve nem használhatók.</span><span class="sxs-lookup"><span data-stu-id="977c6-123">Although **Get-ItemProperty** has **Filter**, **Include**, and **Exclude** parameters, they cannot be used to filter by property name.</span></span> <span data-ttu-id="977c6-124">Ezek a paraméterek tekintse meg a beállításkulcsok – amelyeket elem elérési utak – és nem a beállításjegyzék-bejegyzések – amelyeket elem tulajdonságai.</span><span class="sxs-lookup"><span data-stu-id="977c6-124">These parameters refer to registry keys—which are item paths—and not registry entries—which are item properties.</span></span>

<span data-ttu-id="977c6-125">Egy másik lehetőség, hogy a Reg.exe parancssori eszközt használja.</span><span class="sxs-lookup"><span data-stu-id="977c6-125">Another option is to use the Reg.exe command line tool.</span></span> <span data-ttu-id="977c6-126">Súgó a reg.exe, írja be a **reg.exe /?**</span><span class="sxs-lookup"><span data-stu-id="977c6-126">For help with reg.exe, type **reg.exe /?**</span></span> <span data-ttu-id="977c6-127">parancsot a parancssorba.</span><span class="sxs-lookup"><span data-stu-id="977c6-127">at a command prompt.</span></span> <span data-ttu-id="977c6-128">A DevicePath bejegyzés megkereséséhez használja reg.exe, ahogy az az alábbi parancsot:</span><span class="sxs-lookup"><span data-stu-id="977c6-128">To find the DevicePath entry, use reg.exe as shown in the following command:</span></span>

```
PS> reg query HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion /v DevicePath

! REG.EXE VERSION 3.0

HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion
    DevicePath  REG_EXPAND_SZ   %SystemRoot%\inf
```

<span data-ttu-id="977c6-129">Használhatja a **WshHej COM** objektum is található egyes beállításjegyzék-bejegyzések, bár ez a módszer nem működik a nagy bináris adatok vagy a beállításjegyzék-bejegyzések neve, amely olyan karaktereket, mint például "\\").</span><span class="sxs-lookup"><span data-stu-id="977c6-129">You can also use the **WshShell COM** object as well to find some registry entries, although this method does not work with large binary data or with registry entry names that include characters such as "\\").</span></span> <span data-ttu-id="977c6-130">Az elem elérési útját a tulajdonságnév hozzáfűzése egy \\ elválasztó:</span><span class="sxs-lookup"><span data-stu-id="977c6-130">Append the property name to the item path with a \\ separator:</span></span>

```
PS> (New-Object -ComObject WScript.Shell).RegRead("HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\DevicePath")
%SystemRoot%\inf
```

### <a name="creating-new-registry-entries"></a><span data-ttu-id="977c6-131">Új beállításjegyzék-bejegyzések létrehozása</span><span class="sxs-lookup"><span data-stu-id="977c6-131">Creating New Registry Entries</span></span>
<span data-ttu-id="977c6-132">"PowerShellPath" nevű új bejegyzés hozzáadása a **CurrentVersion** kulcshasználat, **New-ItemProperty** az elérési útját a kulcsot, a bejegyzés neve és a bejegyzés.</span><span class="sxs-lookup"><span data-stu-id="977c6-132">To add a new entry named "PowerShellPath" to the **CurrentVersion** key, use **New-ItemProperty** with the path to the key, the entry name, and the value of the entry.</span></span> <span data-ttu-id="977c6-133">Ehhez a példához most elindítjuk a Windows PowerShell-változó értékének **$PSHome**, amely a telepítési könyvtár elérési útjának tárolja a Windows PowerShell környezethez.</span><span class="sxs-lookup"><span data-stu-id="977c6-133">For this example, we will take the value of the Windows PowerShell variable **$PSHome**, which stores the path to the installation directory for Windows PowerShell.</span></span>

<span data-ttu-id="977c6-134">Az új bejegyzést adhat a kulcsot a következő paranccsal, és a parancs is az új bejegyzést információt ad vissza:</span><span class="sxs-lookup"><span data-stu-id="977c6-134">You can add the new entry to the key by using the following command, and the command also returns information about the new entry:</span></span>

```
PS> New-ItemProperty -Path HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion -Name PowerShellPath -PropertyType String -Value $PSHome

PSPath         : Microsoft.PowerShell.Core\Registry::HKEY_LOCAL_MACHINE\SOFTWAR
                 E\Microsoft\Windows\CurrentVersion
PSParentPath   : Microsoft.PowerShell.Core\Registry::HKEY_LOCAL_MACHINE\SOFTWAR
                 E\Microsoft\Windows
PSChildName    : CurrentVersion
PSDrive        : HKLM
PSProvider     : Microsoft.PowerShell.Core\Registry
PowerShellPath : C:\Program Files\Windows PowerShell\v1.0
```

<span data-ttu-id="977c6-135">A **PropertyType típusa** nevének kell lennie egy **Microsoft.Win32.RegistryValueKind** enumerálási tag a következő táblázatból:</span><span class="sxs-lookup"><span data-stu-id="977c6-135">The **PropertyType** must be the name of a **Microsoft.Win32.RegistryValueKind** enumeration member from the following table:</span></span>

|<span data-ttu-id="977c6-136">PropertyType típusa érték</span><span class="sxs-lookup"><span data-stu-id="977c6-136">PropertyType Value</span></span>|<span data-ttu-id="977c6-137">Jelentés</span><span class="sxs-lookup"><span data-stu-id="977c6-137">Meaning</span></span>|
|----------------------|-----------|
|<span data-ttu-id="977c6-138">Bináris</span><span class="sxs-lookup"><span data-stu-id="977c6-138">Binary</span></span>|<span data-ttu-id="977c6-139">Bináris adatok</span><span class="sxs-lookup"><span data-stu-id="977c6-139">Binary data</span></span>|
|<span data-ttu-id="977c6-140">DWord</span><span class="sxs-lookup"><span data-stu-id="977c6-140">DWord</span></span>|<span data-ttu-id="977c6-141">Egy szám, amely egy érvényes UInt32</span><span class="sxs-lookup"><span data-stu-id="977c6-141">A number that is a valid UInt32</span></span>|
|<span data-ttu-id="977c6-142">ExpandString</span><span class="sxs-lookup"><span data-stu-id="977c6-142">ExpandString</span></span>|<span data-ttu-id="977c6-143">Karakterlánc, amely dinamikusan bontva környezeti változókat is tartalmazhat.</span><span class="sxs-lookup"><span data-stu-id="977c6-143">A string that can contain environment variables that are dynamically expanded</span></span>|
|<span data-ttu-id="977c6-144">Attribútummal rendelkező multistring karakterláncok</span><span class="sxs-lookup"><span data-stu-id="977c6-144">MultiString</span></span>|<span data-ttu-id="977c6-145">Egy többsoros karakterlánc</span><span class="sxs-lookup"><span data-stu-id="977c6-145">A multiline string</span></span>|
|<span data-ttu-id="977c6-146">Karakterlánc</span><span class="sxs-lookup"><span data-stu-id="977c6-146">String</span></span>|<span data-ttu-id="977c6-147">Bármilyen karakterlánc típusú értéket</span><span class="sxs-lookup"><span data-stu-id="977c6-147">Any string value</span></span>|
|<span data-ttu-id="977c6-148">Négyszó</span><span class="sxs-lookup"><span data-stu-id="977c6-148">QWord</span></span>|<span data-ttu-id="977c6-149">8 bájtos bináris adatok</span><span class="sxs-lookup"><span data-stu-id="977c6-149">8 bytes of binary data</span></span>|

> [!NOTE]
> <span data-ttu-id="977c6-150">Egy tömböt a megadásával több helyre egy beállításjegyzékbeli bejegyzést is hozzáadhat a **elérési** paraméter:</span><span class="sxs-lookup"><span data-stu-id="977c6-150">You can add a registry entry to multiple locations by specifying an array of values for the **Path** parameter:</span></span>

```
New-ItemProperty -Path HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion, HKCU:\SOFTWARE\Microsoft\Windows\CurrentVersion -Name PowerShellPath -PropertyType String -Value $PSHome
```

<span data-ttu-id="977c6-151">Egy már meglévő beállításazonosítót bejegyzés hozzáadásával is felülírhatja a **kényszerített** bármelyik paraméter **New-ItemProperty** parancsot.</span><span class="sxs-lookup"><span data-stu-id="977c6-151">You can also overwrite a pre-existing registry entry value by adding the **Force** parameter to any **New-ItemProperty** command.</span></span>

### <a name="renaming-registry-entries"></a><span data-ttu-id="977c6-152">Beállításjegyzék-bejegyzések átnevezése</span><span class="sxs-lookup"><span data-stu-id="977c6-152">Renaming Registry Entries</span></span>
<span data-ttu-id="977c6-153">Átnevezi a **PowerShellPath** "PSHome," használata bejegyzést **Rename-ItemProperty**:</span><span class="sxs-lookup"><span data-stu-id="977c6-153">To rename the **PowerShellPath** entry to "PSHome," use **Rename-ItemProperty**:</span></span>

```
Rename-ItemProperty -Path HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion -Name PowerShellPath -NewName PSHome
```

<span data-ttu-id="977c6-154">Az átnevezett értéket jeleníti meg, vegye fel a **PassThru** paramétert a parancshoz.</span><span class="sxs-lookup"><span data-stu-id="977c6-154">To display the renamed value, add the **PassThru** parameter to the command.</span></span>

```
Rename-ItemProperty -Path HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion -Name PowerShellPath -NewName PSHome -passthru
```

### <a name="deleting-registry-entries"></a><span data-ttu-id="977c6-155">Beállításjegyzék-bejegyzések törlése</span><span class="sxs-lookup"><span data-stu-id="977c6-155">Deleting Registry Entries</span></span>
<span data-ttu-id="977c6-156">A PSHome és a PowerShellPath beállításjegyzék-bejegyzések törléséhez használja **Remove-ItemProperty**:</span><span class="sxs-lookup"><span data-stu-id="977c6-156">To delete both the PSHome and PowerShellPath registry entries, use **Remove-ItemProperty**:</span></span>

```
Remove-ItemProperty -Path HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion -Name PSHome
Remove-ItemProperty -Path HKCU:\SOFTWARE\Microsoft\Windows\CurrentVersion -Name PowerShellPath
```

