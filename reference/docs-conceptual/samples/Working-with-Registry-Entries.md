---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: Beállításjegyzék-bejegyzések használata
ms.openlocfilehash: c1fd6f57f13240eb2039f2d5756796678800aee0
ms.sourcegitcommit: a6f13c16a535acea279c0ddeca72f1f0d8a8ce4c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2019
ms.locfileid: "67030733"
---
# <a name="working-with-registry-entries"></a><span data-ttu-id="cd328-103">Beállításjegyzék-bejegyzések használata</span><span class="sxs-lookup"><span data-stu-id="cd328-103">Working with Registry Entries</span></span>

<span data-ttu-id="cd328-104">Mivel a beállításjegyzék-bejegyzések tulajdonságok kulcsokat, és mint ilyen, nem közvetlenül tallózható, ha a velük végzett munkát egy némileg eltérő megközelítést kell.</span><span class="sxs-lookup"><span data-stu-id="cd328-104">Because registry entries are properties of keys and, as such, cannot be directly browsed, we need to take a slightly different approach when working with them.</span></span>

## <a name="listing-registry-entries"></a><span data-ttu-id="cd328-105">Beállításjegyzék-bejegyzések listája</span><span class="sxs-lookup"><span data-stu-id="cd328-105">Listing Registry Entries</span></span>

<span data-ttu-id="cd328-106">Nincsenek számos különböző módon megvizsgálhatja a beállításjegyzékbeli bejegyzéseket.</span><span class="sxs-lookup"><span data-stu-id="cd328-106">There are many different ways to examine registry entries.</span></span> <span data-ttu-id="cd328-107">A legegyszerűbb módja, hogy a kulcshoz társított tulajdonságnevek kap.</span><span class="sxs-lookup"><span data-stu-id="cd328-107">The simplest way is to get the property names associated with a key.</span></span> <span data-ttu-id="cd328-108">Például ahhoz, hogy a beállításkulcs bejegyzések `HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion`, használjon `Get-Item`.</span><span class="sxs-lookup"><span data-stu-id="cd328-108">For example, to see the names of the entries in the registry key `HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion`, use `Get-Item`.</span></span> <span data-ttu-id="cd328-109">Beállításkulcsok rendelkezik egy tulajdonságot "Property" általános nevét, amely az a kulcsot a beállításjegyzék-bejegyzések listája.</span><span class="sxs-lookup"><span data-stu-id="cd328-109">Registry keys have a property with the generic name of "Property" that is a list of registry entries in the key.</span></span>
<span data-ttu-id="cd328-110">A következő parancsot a tulajdonság tulajdonság kiválasztása, és kibontja az elemeket, hogy egy listában jelennek:</span><span class="sxs-lookup"><span data-stu-id="cd328-110">The following command selects the Property property and expands the items so that they are displayed in a list:</span></span>

```powershell
Get-Item -Path Registry::HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion |
  Select-Object -ExpandProperty Property
```

```Output
DevicePath
MediaPathUnexpanded
ProgramFilesDir
CommonFilesDir
ProductId
```

<span data-ttu-id="cd328-111">A beállításjegyzék-bejegyzések olvashatóbb formátumban megtekintéséhez használja `Get-ItemProperty`:</span><span class="sxs-lookup"><span data-stu-id="cd328-111">To view the registry entries in a more readable form, use `Get-ItemProperty`:</span></span>

```powershell
Get-ItemProperty -Path Registry::HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion
```

```Output
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

<span data-ttu-id="cd328-112">A Windows PowerShell biztonsággal kapcsolatos tulajdonságok a kulcshoz tartozó összes előtaggal van "PS", mint például **PSPath**, **PSParentPath**, **PSChildName**, és **PSProvider** .</span><span class="sxs-lookup"><span data-stu-id="cd328-112">The Windows PowerShell-related properties for the key are all prefixed with "PS", such as **PSPath**, **PSParentPath**, **PSChildName**, and **PSProvider**.</span></span>

<span data-ttu-id="cd328-113">Használhatja a `*.*` jelölése címre az aktuális helyét.</span><span class="sxs-lookup"><span data-stu-id="cd328-113">You can use the `*.*` notation for referring to the current location.</span></span> <span data-ttu-id="cd328-114">Használhat `Set-Location` módosítani a **CurrentVersion** registry container első:</span><span class="sxs-lookup"><span data-stu-id="cd328-114">You can use `Set-Location` to change to the **CurrentVersion** registry container first:</span></span>

```powershell
Set-Location -Path Registry::HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion
```

<span data-ttu-id="cd328-115">Másik lehetőségként használhatja a beépített HKLM PSDrive az `Set-Location`:</span><span class="sxs-lookup"><span data-stu-id="cd328-115">Alternatively, you can use the built-in HKLM PSDrive with `Set-Location`:</span></span>

```powershell
Set-Location -Path hklm:\SOFTWARE\Microsoft\Windows\CurrentVersion
```

<span data-ttu-id="cd328-116">Ezután a `*.*` jelöléssel aktuális helyének teljes elérési út megadása nélkül a tulajdonságok listázásához:</span><span class="sxs-lookup"><span data-stu-id="cd328-116">You can then use the `*.*` notation for the current location to list the properties without specifying a full path:</span></span>

```powershell
Get-ItemProperty -Path .
```

```Output
...
DevicePath          : C:\WINDOWS\inf
MediaPathUnexpanded : C:\WINDOWS\Media
ProgramFilesDir     : C:\Program Files
...
```

<span data-ttu-id="cd328-117">Elérési út bővítése működik ugyanaz, mint a fájlrendszeren belüli ennek a helynek, így a **ItemProperty** listázásakor `HKLM:\SOFTWARE\Microsoft\Windows\Help` használatával `Get-ItemProperty -Path ..\Help`.</span><span class="sxs-lookup"><span data-stu-id="cd328-117">Path expansion works the same as it does within the file system, so from this location you can get the **ItemProperty** listing for `HKLM:\SOFTWARE\Microsoft\Windows\Help` by using `Get-ItemProperty -Path ..\Help`.</span></span>

## <a name="getting-a-single-registry-entry"></a><span data-ttu-id="cd328-118">Egyetlen bejegyzés beolvasása</span><span class="sxs-lookup"><span data-stu-id="cd328-118">Getting a Single Registry Entry</span></span>

<span data-ttu-id="cd328-119">Ha szeretné lekérdezni egy adott bejegyzést egy beállításkulcsot, több lehetséges módszer egyikét használhatja.</span><span class="sxs-lookup"><span data-stu-id="cd328-119">If you want to retrieve a specific entry in a registry key, you can use one of several possible approaches.</span></span> <span data-ttu-id="cd328-120">Ebben a példában találja értékét **DevicePath** a `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion`.</span><span class="sxs-lookup"><span data-stu-id="cd328-120">This example finds the value of **DevicePath** in `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion`.</span></span>

<span data-ttu-id="cd328-121">Használatával `Get-ItemProperty`, használja a **elérési** paraméterrel adja meg annak a kulcsnak a nevét, és a **neve** paramétert adja meg a nevét a **DevicePath** bejegyzés.</span><span class="sxs-lookup"><span data-stu-id="cd328-121">Using `Get-ItemProperty`, use the **Path** parameter to specify the name of the key, and the **Name** parameter to specify the name of the **DevicePath** entry.</span></span>

```powershell
Get-ItemProperty -Path HKLM:\Software\Microsoft\Windows\CurrentVersion -Name DevicePath
```

```Output
PSPath       : Microsoft.PowerShell.Core\Registry::HKEY_LOCAL_MACHINE\Software\
               Microsoft\Windows\CurrentVersion
PSParentPath : Microsoft.PowerShell.Core\Registry::HKEY_LOCAL_MACHINE\Software\
               Microsoft\Windows
PSChildName  : CurrentVersion
PSDrive      : HKLM
PSProvider   : Microsoft.PowerShell.Core\Registry
DevicePath   : C:\WINDOWS\inf
```

<span data-ttu-id="cd328-122">Ez a parancs visszaadja a standard szintű Windows PowerShell tulajdonságait, valamint a **DevicePath** tulajdonság.</span><span class="sxs-lookup"><span data-stu-id="cd328-122">This command returns the standard Windows PowerShell properties as well as the **DevicePath** property.</span></span>

> [!NOTE]
> <span data-ttu-id="cd328-123">Bár a `Get-ItemProperty` rendelkezik **szűrő**, **Belefoglalás**, és **kizárása** paraméterek, nem használható a név tulajdonság szerint szűrheti.</span><span class="sxs-lookup"><span data-stu-id="cd328-123">Although `Get-ItemProperty` has **Filter**, **Include**, and **Exclude** parameters, they cannot be used to filter by property name.</span></span> <span data-ttu-id="cd328-124">Tekintse meg ezeket a paramétereket beállításkulcsokról, amelyek elem elérési utak és nem a beállításjegyzék-bejegyzések.</span><span class="sxs-lookup"><span data-stu-id="cd328-124">These parameters refer to registry keys, which are item paths and not registry entries.</span></span> <span data-ttu-id="cd328-125">Beállításjegyzék-bejegyzések, amelyek elem tulajdonságai.</span><span class="sxs-lookup"><span data-stu-id="cd328-125">Registry entries which are item properties.</span></span>

<span data-ttu-id="cd328-126">Egy másik lehetőség, hogy a Reg.exe parancssori eszközzel.</span><span class="sxs-lookup"><span data-stu-id="cd328-126">Another option is to use the Reg.exe command line tool.</span></span> <span data-ttu-id="cd328-127">Segítségre van szüksége a reg.exe, írja be a következőt `reg.exe /?` parancsot a parancssorba.</span><span class="sxs-lookup"><span data-stu-id="cd328-127">For help with reg.exe, type `reg.exe /?` at a command prompt.</span></span> <span data-ttu-id="cd328-128">A DevicePath bejegyzés megkereséséhez használja reg.exe, ahogyan az alábbi parancsot:</span><span class="sxs-lookup"><span data-stu-id="cd328-128">To find the DevicePath entry, use reg.exe as shown in the following command:</span></span>

```powershell
reg query HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion /v DevicePath
```

```Output
! REG.EXE VERSION 3.0

HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion
    DevicePath  REG_EXPAND_SZ   %SystemRoot%\inf
```

<span data-ttu-id="cd328-129">Is használhatja a **WshHej** COM-objektum is található egyes beállításjegyzék-bejegyzések, bár ez a módszer nem működik nagy mennyiségű bináris adatot, vagy a beállításjegyzék-bejegyzések neve, amely tartalmazhat, mint például "\\").</span><span class="sxs-lookup"><span data-stu-id="cd328-129">You can also use the **WshShell** COM object as well to find some registry entries, although this method does not work with large binary data or with registry entry names that include characters such as "\\").</span></span> <span data-ttu-id="cd328-130">A tulajdonságnév hozzáfűzése a nézetelem elérési útja a egy \\ elválasztó:</span><span class="sxs-lookup"><span data-stu-id="cd328-130">Append the property name to the item path with a \\ separator:</span></span>

```powershell
(New-Object -ComObject WScript.Shell).RegRead("HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\DevicePath")
```

```Output
%SystemRoot%\inf
```

## <a name="setting-a-single-registry-entry"></a><span data-ttu-id="cd328-131">Egyetlen bejegyzés beállítása</span><span class="sxs-lookup"><span data-stu-id="cd328-131">Setting a Single Registry Entry</span></span>

<span data-ttu-id="cd328-132">Ha szeretné módosítani egy adott bejegyzést egy beállításkulcsot, több lehetséges módszer egyikét használhatja.</span><span class="sxs-lookup"><span data-stu-id="cd328-132">If you want to change a specific entry in a registry key, you can use one of several possible approaches.</span></span> <span data-ttu-id="cd328-133">Ez a példa módosítja a **elérési** bejegyzés alatt `HKEY_CURRENT_USER\Environment`.</span><span class="sxs-lookup"><span data-stu-id="cd328-133">This example modifies the **Path** entry under `HKEY_CURRENT_USER\Environment`.</span></span> <span data-ttu-id="cd328-134">A **elérési út** bejegyzés határozza meg, hogy hol található a végrehajtható fájlokat.</span><span class="sxs-lookup"><span data-stu-id="cd328-134">The **Path** entry specifies where to find executable files.</span></span>

1. <span data-ttu-id="cd328-135">Az aktuális értéket, a **elérési** bejegyzés használatával `Get-ItemProperty`.</span><span class="sxs-lookup"><span data-stu-id="cd328-135">Retrieve the current value of the **Path** entry using `Get-ItemProperty`.</span></span>
2. <span data-ttu-id="cd328-136">Adja hozzá az új értéket, és megadhat, az azt egy `;`.</span><span class="sxs-lookup"><span data-stu-id="cd328-136">Add the new value, separating it with a `;`.</span></span>
3. <span data-ttu-id="cd328-137">Használat `Set-ItemProperty` a megadott kulcs, bejegyzés neve és értéke módosíthatja a beállításjegyzék-bejegyzést.</span><span class="sxs-lookup"><span data-stu-id="cd328-137">Use `Set-ItemProperty` with the specified key, entry name, and value to modify the registry entry.</span></span>

```powershell
$value = Get-ItemProperty -Path HKCU:\Environment -Name Path
$newpath = $value.Path += ";C:\src\bin\"
Set-ItemProperty -Path HKCU:\Environment -Name Path -Value $newpath
```

> [!NOTE]
> <span data-ttu-id="cd328-138">Bár a `Set-ItemProperty` rendelkezik **szűrő**, **Belefoglalás**, és **kizárása** paraméterek, nem használható a név tulajdonság szerint szűrheti.</span><span class="sxs-lookup"><span data-stu-id="cd328-138">Although `Set-ItemProperty` has **Filter**, **Include**, and **Exclude** parameters, they cannot be used to filter by property name.</span></span> <span data-ttu-id="cd328-139">Tekintse meg ezeket a paramétereket beállításkulcsok – elem elérési utak minősülő – és nem a beállításjegyzék-bejegyzések – amelyeket elem tulajdonságai.</span><span class="sxs-lookup"><span data-stu-id="cd328-139">These parameters refer to registry keys—which are item paths—and not registry entries—which are item properties.</span></span>

<span data-ttu-id="cd328-140">Egy másik lehetőség, hogy a Reg.exe parancssori eszközzel.</span><span class="sxs-lookup"><span data-stu-id="cd328-140">Another option is to use the Reg.exe command line tool.</span></span> <span data-ttu-id="cd328-141">Segítségre van szüksége a reg.exe, írja be a következőt **reg.exe /?**</span><span class="sxs-lookup"><span data-stu-id="cd328-141">For help with reg.exe, type **reg.exe /?**</span></span>
<span data-ttu-id="cd328-142">a parancssorba.</span><span class="sxs-lookup"><span data-stu-id="cd328-142">at a command prompt.</span></span>

<span data-ttu-id="cd328-143">A következő példát módosítások a **elérési út** bejegyzés az elérési út hozzáadása a fenti példában eltávolításával.</span><span class="sxs-lookup"><span data-stu-id="cd328-143">The following example changes the **Path** entry by removing the path added in the example above.</span></span>
<span data-ttu-id="cd328-144">`Get-ItemProperty` továbbra is a jelenlegi érték elemzése a által visszaadott karakterlánc ne kelljen beolvasásához használt `reg query`.</span><span class="sxs-lookup"><span data-stu-id="cd328-144">`Get-ItemProperty` is still used to retrieve the current value to avoid having to parse the string returned from `reg query`.</span></span> <span data-ttu-id="cd328-145">A **SubString** és **LastIndexOf** módszerek használhatók a hozzáadott utolsó elérési beolvasni a **elérési út** bejegyzés.</span><span class="sxs-lookup"><span data-stu-id="cd328-145">The **SubString** and **LastIndexOf** methods are used to retrieve the last path added to the **Path** entry.</span></span>

```powershell
$value = Get-ItemProperty -Path HKCU:\Environment -Name Path
$newpath = $value.Path.SubString(0, $value.Path.LastIndexOf(';'))
reg add HKCU\Environment /v Path /d $newpath /f
```

```Output
The operation completed successfully.
```

## <a name="creating-new-registry-entries"></a><span data-ttu-id="cd328-146">Új beállításjegyzék-bejegyzések létrehozása</span><span class="sxs-lookup"><span data-stu-id="cd328-146">Creating New Registry Entries</span></span>

<span data-ttu-id="cd328-147">"PowerShellPath" nevű új bejegyzés hozzáadása a **CurrentVersion** fő, használati `New-ItemProperty` az elérési útját a kulcsot, a bejegyzés neve és a bejegyzés értéke.</span><span class="sxs-lookup"><span data-stu-id="cd328-147">To add a new entry named "PowerShellPath" to the **CurrentVersion** key, use `New-ItemProperty` with the path to the key, the entry name, and the value of the entry.</span></span> <span data-ttu-id="cd328-148">Ebben a példában azt vesz igénybe a Windows PowerShell-változó értékét `$PSHome`, amely a telepítési könyvtár elérési útját tárolja a Windows PowerShell környezethez.</span><span class="sxs-lookup"><span data-stu-id="cd328-148">For this example, we will take the value of the Windows PowerShell variable `$PSHome`, which stores the path to the installation directory for Windows PowerShell.</span></span>

<span data-ttu-id="cd328-149">Adhat hozzá az új bejegyzést a kulcs a következő paranccsal, és a parancs is információval szolgál az új bejegyzést:</span><span class="sxs-lookup"><span data-stu-id="cd328-149">You can add the new entry to the key by using the following command, and the command also returns information about the new entry:</span></span>

```powershell
New-ItemProperty -Path HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion -Name PowerShellPath -PropertyType String -Value $PSHome
```

```Output
PSPath         : Microsoft.PowerShell.Core\Registry::HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion
PSParentPath   : Microsoft.PowerShell.Core\Registry::HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows
PSChildName    : CurrentVersion
PSDrive        : HKLM
PSProvider     : Microsoft.PowerShell.Core\Registry
PowerShellPath : C:\Program Files\Windows PowerShell\v1.0
```

<span data-ttu-id="cd328-150">A **%d{PropertyType/** nevének kell lennie egy **Microsoft.Win32.RegistryValueKind** enumerálási tag a következő táblázatból:</span><span class="sxs-lookup"><span data-stu-id="cd328-150">The **PropertyType** must be the name of a **Microsoft.Win32.RegistryValueKind** enumeration member from the following table:</span></span>

|<span data-ttu-id="cd328-151">%D{PropertyType/ érték</span><span class="sxs-lookup"><span data-stu-id="cd328-151">PropertyType Value</span></span>|<span data-ttu-id="cd328-152">Jelentés</span><span class="sxs-lookup"><span data-stu-id="cd328-152">Meaning</span></span>|
|----------------------|-----------|
|<span data-ttu-id="cd328-153">Bináris</span><span class="sxs-lookup"><span data-stu-id="cd328-153">Binary</span></span>|<span data-ttu-id="cd328-154">Bináris adatok</span><span class="sxs-lookup"><span data-stu-id="cd328-154">Binary data</span></span>|
|<span data-ttu-id="cd328-155">DWord</span><span class="sxs-lookup"><span data-stu-id="cd328-155">DWord</span></span>|<span data-ttu-id="cd328-156">Egy szám, amely egy érvényes UInt32</span><span class="sxs-lookup"><span data-stu-id="cd328-156">A number that is a valid UInt32</span></span>|
|<span data-ttu-id="cd328-157">ExpandString</span><span class="sxs-lookup"><span data-stu-id="cd328-157">ExpandString</span></span>|<span data-ttu-id="cd328-158">Egy karakterlánc, amely dinamikusan bontva környezeti változókat is tartalmazhat.</span><span class="sxs-lookup"><span data-stu-id="cd328-158">A string that can contain environment variables that are dynamically expanded</span></span>|
|<span data-ttu-id="cd328-159">MultiString</span><span class="sxs-lookup"><span data-stu-id="cd328-159">MultiString</span></span>|<span data-ttu-id="cd328-160">Egy többsoros karakterlánc</span><span class="sxs-lookup"><span data-stu-id="cd328-160">A multiline string</span></span>|
|<span data-ttu-id="cd328-161">Sztring</span><span class="sxs-lookup"><span data-stu-id="cd328-161">String</span></span>|<span data-ttu-id="cd328-162">bármilyen karakterlánc típusú értéket</span><span class="sxs-lookup"><span data-stu-id="cd328-162">Any string value</span></span>|
|<span data-ttu-id="cd328-163">QWord</span><span class="sxs-lookup"><span data-stu-id="cd328-163">QWord</span></span>|<span data-ttu-id="cd328-164">8 bájtos bináris adatok</span><span class="sxs-lookup"><span data-stu-id="cd328-164">8 bytes of binary data</span></span>|

> [!NOTE]
> <span data-ttu-id="cd328-165">Adjon meg egy olyan értéktömböt a több helyre egy beállításjegyzékbeli bejegyzést is hozzáadhat a **elérési út** paramétert:</span><span class="sxs-lookup"><span data-stu-id="cd328-165">You can add a registry entry to multiple locations by specifying an array of values for the **Path** parameter:</span></span>

```powershell
New-ItemProperty -Name PowerShellPath -PropertyType String -Value $PSHome `
  -Path HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion, HKCU:\SOFTWARE\Microsoft\Windows\CurrentVersion
```

<span data-ttu-id="cd328-166">Egy már meglévő beállításazonosító bejegyzés hozzáadásával is felülírhatja a **kényszerített** paraméter sem `New-ItemProperty` parancsot.</span><span class="sxs-lookup"><span data-stu-id="cd328-166">You can also overwrite a pre-existing registry entry value by adding the **Force** parameter to any `New-ItemProperty` command.</span></span>

## <a name="renaming-registry-entries"></a><span data-ttu-id="cd328-167">Beállításjegyzék-bejegyzések átnevezése</span><span class="sxs-lookup"><span data-stu-id="cd328-167">Renaming Registry Entries</span></span>

<span data-ttu-id="cd328-168">Átnevezi a **PowerShellPath** bejegyzést a "PSHome," használata `Rename-ItemProperty`:</span><span class="sxs-lookup"><span data-stu-id="cd328-168">To rename the **PowerShellPath** entry to "PSHome," use `Rename-ItemProperty`:</span></span>

```powershell
Rename-ItemProperty -Path HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion -Name PowerShellPath -NewName PSHome
```

<span data-ttu-id="cd328-169">Átnevezett értéket jeleníti meg, adja hozzá a **PassThru** paramétert a parancshoz.</span><span class="sxs-lookup"><span data-stu-id="cd328-169">To display the renamed value, add the **PassThru** parameter to the command.</span></span>

```powershell
Rename-ItemProperty -Path HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion -Name PowerShellPath -NewName PSHome -passthru
```

## <a name="deleting-registry-entries"></a><span data-ttu-id="cd328-170">Beállításjegyzék-bejegyzések törlése</span><span class="sxs-lookup"><span data-stu-id="cd328-170">Deleting Registry Entries</span></span>

<span data-ttu-id="cd328-171">A PSHome és a PowerShellPath beállításjegyzék-bejegyzések törléséhez használja `Remove-ItemProperty`:</span><span class="sxs-lookup"><span data-stu-id="cd328-171">To delete both the PSHome and PowerShellPath registry entries, use `Remove-ItemProperty`:</span></span>

```powershell
Remove-ItemProperty -Path HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion -Name PSHome
Remove-ItemProperty -Path HKCU:\SOFTWARE\Microsoft\Windows\CurrentVersion -Name PowerShellPath
```
