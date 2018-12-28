---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: Beállításjegyzék-bejegyzések használata
ms.assetid: fd254570-27ac-4cc9-81d4-011afd29b7dc
ms.openlocfilehash: bffdf80931fc4dc570b584623487077dc5d449dc
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/14/2018
ms.locfileid: "53404460"
---
# <a name="working-with-registry-entries"></a><span data-ttu-id="0558c-103">Beállításjegyzék-bejegyzések használata</span><span class="sxs-lookup"><span data-stu-id="0558c-103">Working with Registry Entries</span></span>

<span data-ttu-id="0558c-104">Mivel a beállításjegyzék-bejegyzések tulajdonságok kulcsokat, és mint ilyen, nem közvetlenül tallózható, ha a velük végzett munkát egy némileg eltérő megközelítést kell.</span><span class="sxs-lookup"><span data-stu-id="0558c-104">Because registry entries are properties of keys and, as such, cannot be directly browsed, we need to take a slightly different approach when working with them.</span></span>

### <a name="listing-registry-entries"></a><span data-ttu-id="0558c-105">Beállításjegyzék-bejegyzések listája</span><span class="sxs-lookup"><span data-stu-id="0558c-105">Listing Registry Entries</span></span>

<span data-ttu-id="0558c-106">Nincsenek számos különböző módon megvizsgálhatja a beállításjegyzékbeli bejegyzéseket.</span><span class="sxs-lookup"><span data-stu-id="0558c-106">There are many different ways to examine registry entries.</span></span> <span data-ttu-id="0558c-107">A legegyszerűbb módja, hogy a kulcshoz társított tulajdonságnevek kap.</span><span class="sxs-lookup"><span data-stu-id="0558c-107">The simplest way is to get the property names associated with a key.</span></span> <span data-ttu-id="0558c-108">Például ahhoz, hogy a beállításkulcs bejegyzések **HKEY_LOCAL_MACHINE\\szoftver\\Microsoft\\Windows\\CurrentVersion**, használjon **Get-Item** .</span><span class="sxs-lookup"><span data-stu-id="0558c-108">For example, to see the names of the entries in the registry key **HKEY_LOCAL_MACHINE\\Software\\Microsoft\\Windows\\CurrentVersion**, use **Get-Item**.</span></span> <span data-ttu-id="0558c-109">Beállításkulcsok rendelkezik egy tulajdonságot "Property" általános nevét, amely az a kulcsot a beállításjegyzék-bejegyzések listája.</span><span class="sxs-lookup"><span data-stu-id="0558c-109">Registry keys have a property with the generic name of "Property" that is a list of registry entries in the key.</span></span> <span data-ttu-id="0558c-110">A következő parancsot a tulajdonság tulajdonság kiválasztása, és kibontja az elemeket, hogy egy listában jelennek:</span><span class="sxs-lookup"><span data-stu-id="0558c-110">The following command selects the Property property and expands the items so that they are displayed in a list:</span></span>

```
PS> Get-Item -Path Registry::HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion | Select-Object -ExpandProperty Property
DevicePath
MediaPathUnexpanded
ProgramFilesDir
CommonFilesDir
ProductId
```

<span data-ttu-id="0558c-111">A beállításjegyzék-bejegyzések olvashatóbb formátumban megtekintéséhez használja **Get-ItemProperty**:</span><span class="sxs-lookup"><span data-stu-id="0558c-111">To view the registry entries in a more readable form, use **Get-ItemProperty**:</span></span>

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

<span data-ttu-id="0558c-112">A Windows PowerShell biztonsággal kapcsolatos tulajdonságok a kulcshoz tartozó összes előtaggal van "PS", mint például **PSPath**, **PSParentPath**, **PSChildName**, és **PSProvider** .</span><span class="sxs-lookup"><span data-stu-id="0558c-112">The Windows PowerShell-related properties for the key are all prefixed with "PS", such as **PSPath**, **PSParentPath**, **PSChildName**, and **PSProvider**.</span></span>

<span data-ttu-id="0558c-113">Használhatja a "**.**" jelölése címre az aktuális helyét.</span><span class="sxs-lookup"><span data-stu-id="0558c-113">You can use the "**.**" notation for referring to the current location.</span></span> <span data-ttu-id="0558c-114">Használhat **hely beállítása** módosítani a **CurrentVersion** registry container első:</span><span class="sxs-lookup"><span data-stu-id="0558c-114">You can use **Set-Location** to change to the **CurrentVersion** registry container first:</span></span>

```powershell
Set-Location -Path Registry::HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion
```

<span data-ttu-id="0558c-115">Másik lehetőségként használhatja a beépített HKLM PSDrive az **hely beállítása**:</span><span class="sxs-lookup"><span data-stu-id="0558c-115">Alternatively, you can use the built-in HKLM PSDrive with **Set-Location**:</span></span>

```powershell
Set-Location -Path hklm:\SOFTWARE\Microsoft\Windows\CurrentVersion
```

<span data-ttu-id="0558c-116">Ezután használhatja a "**.**" jelöléssel aktuális helyének teljes elérési út megadása nélkül a tulajdonságok listázásához:</span><span class="sxs-lookup"><span data-stu-id="0558c-116">You can then use the "**.**" notation for the current location to list the properties without specifying a full path:</span></span>

```
PS> Get-ItemProperty -Path .
...
DevicePath          : C:\WINDOWS\inf
MediaPathUnexpanded : C:\WINDOWS\Media
ProgramFilesDir     : C:\Program Files
...
```

<span data-ttu-id="0558c-117">Elérési út bővítése működik ugyanaz, mint a fájlrendszeren belüli ennek a helynek, így a **ItemProperty** listázásakor **HKLM:\\szoftver\\Microsoft\\Windows \\Súgó** használatával **Get-ItemProperty-elérési út... \\Súgó**.</span><span class="sxs-lookup"><span data-stu-id="0558c-117">Path expansion works the same as it does within the file system, so from this location you can get the **ItemProperty** listing for **HKLM:\\SOFTWARE\\Microsoft\\Windows\\Help** by using **Get-ItemProperty -Path ..\\Help**.</span></span>

### <a name="getting-a-single-registry-entry"></a><span data-ttu-id="0558c-118">Egyetlen bejegyzés beolvasása</span><span class="sxs-lookup"><span data-stu-id="0558c-118">Getting a Single Registry Entry</span></span>

<span data-ttu-id="0558c-119">Ha szeretné lekérdezni egy adott bejegyzést egy beállításkulcsot, több lehetséges módszer egyikét használhatja.</span><span class="sxs-lookup"><span data-stu-id="0558c-119">If you want to retrieve a specific entry in a registry key, you can use one of several possible approaches.</span></span> <span data-ttu-id="0558c-120">Ebben a példában találja értékét **DevicePath** a **HKEY_LOCAL_MACHINE\\szoftver\\Microsoft\\Windows\\CurrentVersion**.</span><span class="sxs-lookup"><span data-stu-id="0558c-120">This example finds the value of **DevicePath** in **HKEY_LOCAL_MACHINE\\SOFTWARE\\Microsoft\\Windows\\CurrentVersion**.</span></span>

<span data-ttu-id="0558c-121">Használatával **Get-ItemProperty**, használja a **elérési** paraméterrel adja meg annak a kulcsnak a nevét, és a **neve** paramétert adja meg a nevét a **DevicePath** bejegyzés.</span><span class="sxs-lookup"><span data-stu-id="0558c-121">Using **Get-ItemProperty**, use the **Path** parameter to specify the name of the key, and the **Name** parameter to specify the name of the **DevicePath** entry.</span></span>

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

<span data-ttu-id="0558c-122">Ez a parancs visszaadja a standard szintű Windows PowerShell tulajdonságait, valamint a **DevicePath** tulajdonság.</span><span class="sxs-lookup"><span data-stu-id="0558c-122">This command returns the standard Windows PowerShell properties as well as the **DevicePath** property.</span></span>

> [!NOTE]
> <span data-ttu-id="0558c-123">Bár a **Get-ItemProperty** rendelkezik **szűrő**, **Belefoglalás**, és **kizárása** paraméterek, nem használható a név tulajdonság szerint szűrheti.</span><span class="sxs-lookup"><span data-stu-id="0558c-123">Although **Get-ItemProperty** has **Filter**, **Include**, and **Exclude** parameters, they cannot be used to filter by property name.</span></span> <span data-ttu-id="0558c-124">Tekintse meg ezeket a paramétereket beállításkulcsok – elem elérési utak minősülő – és nem a beállításjegyzék-bejegyzések – amelyeket elem tulajdonságai.</span><span class="sxs-lookup"><span data-stu-id="0558c-124">These parameters refer to registry keys—which are item paths—and not registry entries—which are item properties.</span></span>

<span data-ttu-id="0558c-125">Egy másik lehetőség, hogy a Reg.exe parancssori eszközzel.</span><span class="sxs-lookup"><span data-stu-id="0558c-125">Another option is to use the Reg.exe command line tool.</span></span> <span data-ttu-id="0558c-126">Segítségre van szüksége a reg.exe, írja be a következőt **reg.exe /?**</span><span class="sxs-lookup"><span data-stu-id="0558c-126">For help with reg.exe, type **reg.exe /?**</span></span> <span data-ttu-id="0558c-127">a parancssorba.</span><span class="sxs-lookup"><span data-stu-id="0558c-127">at a command prompt.</span></span> <span data-ttu-id="0558c-128">A DevicePath bejegyzés megkereséséhez használja reg.exe, ahogyan az alábbi parancsot:</span><span class="sxs-lookup"><span data-stu-id="0558c-128">To find the DevicePath entry, use reg.exe as shown in the following command:</span></span>

```
PS> reg query HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion /v DevicePath

! REG.EXE VERSION 3.0

HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion
    DevicePath  REG_EXPAND_SZ   %SystemRoot%\inf
```

<span data-ttu-id="0558c-129">Is használhatja a **WshHej COM** objektum is található egyes beállításjegyzék-bejegyzések, bár ez a módszer nem működik nagy mennyiségű bináris adatot, vagy a beállításjegyzék-bejegyzések neve, amely tartalmazhat, mint például "\\").</span><span class="sxs-lookup"><span data-stu-id="0558c-129">You can also use the **WshShell COM** object as well to find some registry entries, although this method does not work with large binary data or with registry entry names that include characters such as "\\").</span></span> <span data-ttu-id="0558c-130">A tulajdonságnév hozzáfűzése a nézetelem elérési útja a egy \\ elválasztó:</span><span class="sxs-lookup"><span data-stu-id="0558c-130">Append the property name to the item path with a \\ separator:</span></span>

```
PS> (New-Object -ComObject WScript.Shell).RegRead("HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\DevicePath")
%SystemRoot%\inf
```

### <a name="creating-new-registry-entries"></a><span data-ttu-id="0558c-131">Új beállításjegyzék-bejegyzések létrehozása</span><span class="sxs-lookup"><span data-stu-id="0558c-131">Creating New Registry Entries</span></span>

<span data-ttu-id="0558c-132">"PowerShellPath" nevű új bejegyzés hozzáadása a **CurrentVersion** fő, használati **New-ItemProperty** az elérési útját a kulcsot, a bejegyzés neve és a bejegyzés értéke.</span><span class="sxs-lookup"><span data-stu-id="0558c-132">To add a new entry named "PowerShellPath" to the **CurrentVersion** key, use **New-ItemProperty** with the path to the key, the entry name, and the value of the entry.</span></span> <span data-ttu-id="0558c-133">Ebben a példában azt vesz igénybe a Windows PowerShell-változó értékét **$PSHome**, amely a telepítési könyvtár elérési útját tárolja a Windows PowerShell környezethez.</span><span class="sxs-lookup"><span data-stu-id="0558c-133">For this example, we will take the value of the Windows PowerShell variable **$PSHome**, which stores the path to the installation directory for Windows PowerShell.</span></span>

<span data-ttu-id="0558c-134">Adhat hozzá az új bejegyzést a kulcs a következő paranccsal, és a parancs is információval szolgál az új bejegyzést:</span><span class="sxs-lookup"><span data-stu-id="0558c-134">You can add the new entry to the key by using the following command, and the command also returns information about the new entry:</span></span>

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

<span data-ttu-id="0558c-135">A **%d{PropertyType/** nevének kell lennie egy **Microsoft.Win32.RegistryValueKind** enumerálási tag a következő táblázatból:</span><span class="sxs-lookup"><span data-stu-id="0558c-135">The **PropertyType** must be the name of a **Microsoft.Win32.RegistryValueKind** enumeration member from the following table:</span></span>

|<span data-ttu-id="0558c-136">%D{PropertyType/ érték</span><span class="sxs-lookup"><span data-stu-id="0558c-136">PropertyType Value</span></span>|<span data-ttu-id="0558c-137">Jelentés</span><span class="sxs-lookup"><span data-stu-id="0558c-137">Meaning</span></span>|
|----------------------|-----------|
|<span data-ttu-id="0558c-138">Bináris</span><span class="sxs-lookup"><span data-stu-id="0558c-138">Binary</span></span>|<span data-ttu-id="0558c-139">A bináris adatok</span><span class="sxs-lookup"><span data-stu-id="0558c-139">Binary data</span></span>|
|<span data-ttu-id="0558c-140">Duplaszó</span><span class="sxs-lookup"><span data-stu-id="0558c-140">DWord</span></span>|<span data-ttu-id="0558c-141">Egy szám, amely egy érvényes UInt32</span><span class="sxs-lookup"><span data-stu-id="0558c-141">A number that is a valid UInt32</span></span>|
|<span data-ttu-id="0558c-142">ExpandString</span><span class="sxs-lookup"><span data-stu-id="0558c-142">ExpandString</span></span>|<span data-ttu-id="0558c-143">Egy karakterlánc, amely dinamikusan bontva környezeti változókat is tartalmazhat.</span><span class="sxs-lookup"><span data-stu-id="0558c-143">A string that can contain environment variables that are dynamically expanded</span></span>|
|<span data-ttu-id="0558c-144">MultiString</span><span class="sxs-lookup"><span data-stu-id="0558c-144">MultiString</span></span>|<span data-ttu-id="0558c-145">Egy többsoros karakterlánc</span><span class="sxs-lookup"><span data-stu-id="0558c-145">A multiline string</span></span>|
|<span data-ttu-id="0558c-146">Sztring</span><span class="sxs-lookup"><span data-stu-id="0558c-146">String</span></span>|<span data-ttu-id="0558c-147">Bármilyen karakterlánc típusú értéket</span><span class="sxs-lookup"><span data-stu-id="0558c-147">Any string value</span></span>|
|<span data-ttu-id="0558c-148">Négyszó típusú</span><span class="sxs-lookup"><span data-stu-id="0558c-148">QWord</span></span>|<span data-ttu-id="0558c-149">8 bájtos bináris adatok</span><span class="sxs-lookup"><span data-stu-id="0558c-149">8 bytes of binary data</span></span>|

> [!NOTE]
> <span data-ttu-id="0558c-150">Adjon meg egy olyan értéktömböt a több helyre egy beállításjegyzékbeli bejegyzést is hozzáadhat a **elérési út** paramétert:</span><span class="sxs-lookup"><span data-stu-id="0558c-150">You can add a registry entry to multiple locations by specifying an array of values for the **Path** parameter:</span></span>

```powershell
New-ItemProperty -Path HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion, HKCU:\SOFTWARE\Microsoft\Windows\CurrentVersion -Name PowerShellPath -PropertyType String -Value $PSHome
```

<span data-ttu-id="0558c-151">Egy már meglévő beállításazonosító bejegyzés hozzáadásával is felülírhatja a **kényszerített** paraméter sem **New-ItemProperty** parancsot.</span><span class="sxs-lookup"><span data-stu-id="0558c-151">You can also overwrite a pre-existing registry entry value by adding the **Force** parameter to any **New-ItemProperty** command.</span></span>

### <a name="renaming-registry-entries"></a><span data-ttu-id="0558c-152">Beállításjegyzék-bejegyzések átnevezése</span><span class="sxs-lookup"><span data-stu-id="0558c-152">Renaming Registry Entries</span></span>

<span data-ttu-id="0558c-153">Átnevezi a **PowerShellPath** bejegyzést a "PSHome," használata **Rename-ItemProperty**:</span><span class="sxs-lookup"><span data-stu-id="0558c-153">To rename the **PowerShellPath** entry to "PSHome," use **Rename-ItemProperty**:</span></span>

```powershell
Rename-ItemProperty -Path HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion -Name PowerShellPath -NewName PSHome
```

<span data-ttu-id="0558c-154">Átnevezett értéket jeleníti meg, adja hozzá a **PassThru** paramétert a parancshoz.</span><span class="sxs-lookup"><span data-stu-id="0558c-154">To display the renamed value, add the **PassThru** parameter to the command.</span></span>

```powershell
Rename-ItemProperty -Path HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion -Name PowerShellPath -NewName PSHome -passthru
```

### <a name="deleting-registry-entries"></a><span data-ttu-id="0558c-155">Beállításjegyzék-bejegyzések törlése</span><span class="sxs-lookup"><span data-stu-id="0558c-155">Deleting Registry Entries</span></span>

<span data-ttu-id="0558c-156">A PSHome és a PowerShellPath beállításjegyzék-bejegyzések törléséhez használja **Remove-ItemProperty**:</span><span class="sxs-lookup"><span data-stu-id="0558c-156">To delete both the PSHome and PowerShellPath registry entries, use **Remove-ItemProperty**:</span></span>

```powershell
Remove-ItemProperty -Path HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion -Name PSHome
Remove-ItemProperty -Path HKCU:\SOFTWARE\Microsoft\Windows\CurrentVersion -Name PowerShellPath
```