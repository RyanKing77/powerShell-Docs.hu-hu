---
ms.date: 2017-06-05
keywords: PowerShell parancsmag
title: "Beállításkulcsok használata"
ms.assetid: 91bfaecd-8684-48b4-ad86-065dfe6dc90a
ms.openlocfilehash: e7c16fe5f03330da3ea8f60b141d9e35eed474b9
ms.sourcegitcommit: cd5a1f054cbf9eb95c5242a995f9741e031ddb24
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 11/28/2017
---
# <a name="working-with-registry-keys"></a><span data-ttu-id="7543d-103">Beállításkulcsok használata</span><span class="sxs-lookup"><span data-stu-id="7543d-103">Working with Registry Keys</span></span>
<span data-ttu-id="7543d-104">Mert beállításkulcsok a Windows PowerShell-meghajtókon elem, azok használata hasonlít a fájlok és mappák.</span><span class="sxs-lookup"><span data-stu-id="7543d-104">Because registry keys are items on Windows PowerShell drives, working with them is very similar to working with files and folders.</span></span> <span data-ttu-id="7543d-105">Egy kritikus különbség az, hogy minden eleme egy beállításjegyzék-alapú Windows PowerShell-meghajtón-e a tároló, csakúgy, mint a fájlrendszer meghajtóján az egyik mappájába.</span><span class="sxs-lookup"><span data-stu-id="7543d-105">One critical difference is that every item on a registry-based Windows PowerShell drive is a container, just like a folder on a file system drive.</span></span> <span data-ttu-id="7543d-106">Beállításjegyzék-bejegyzések és a hozzájuk tartozó értékek tulajdonságok az elemek nem különálló elemek.</span><span class="sxs-lookup"><span data-stu-id="7543d-106">However, registry entries and their associated values are properties of the items, not distinct items.</span></span>

### <a name="listing-all-subkeys-of-a-registry-key"></a><span data-ttu-id="7543d-107">A beállításkulcs összes alkulcsához listázása</span><span class="sxs-lookup"><span data-stu-id="7543d-107">Listing All Subkeys of a Registry Key</span></span>
<span data-ttu-id="7543d-108">Használatával megjelenítheti az összes elemet közvetlenül egy beállításkulcs megadásával belül **Get-ChildItem**.</span><span class="sxs-lookup"><span data-stu-id="7543d-108">You can show all items directly within a registry key by using **Get-ChildItem**.</span></span> <span data-ttu-id="7543d-109">Adja hozzá a választható **kényszerített** rejtett megjelenítése vagy rendszer elemek paraméter.</span><span class="sxs-lookup"><span data-stu-id="7543d-109">Add the optional **Force** parameter to display hidden or system items.</span></span> <span data-ttu-id="7543d-110">Például a parancs megjeleníti az elemek közvetlenül a Windows PowerShell meghajtót HKCU belül:, amely megfelel a HKEY_CURRENT_USER beállításjegyzék-struktúrát:</span><span class="sxs-lookup"><span data-stu-id="7543d-110">For example, this command displays the items directly within Windows PowerShell drive HKCU:, which corresponds to the HKEY_CURRENT_USER registry hive:</span></span>

```
PS> Get-ChildItem -Path hkcu:\

   Hive: Microsoft.PowerShell.Core\Registry::HKEY_CURRENT_USER

SKC  VC Name                           Property
---  -- ----                           --------
  2   0 AppEvents                      {}
  7  33 Console                        {ColorTable00, ColorTable01, ColorTab...
 25   1 Control Panel                  {Opened}
  0   5 Environment                    {APR_ICONV_PATH, INCLUDE, LIB, TEMP...}
  1   7 Identities                     {Last Username, Last User ...
  4   0 Keyboard Layout                {}
...
```

<span data-ttu-id="7543d-111">Ezek a HKEY_CURRENT_USER a a Beállításszerkesztőt (Regedit.exe) látható legfelső szintű kulccsal.</span><span class="sxs-lookup"><span data-stu-id="7543d-111">These are the top-level keys visible under HKEY_CURRENT_USER in the Registry Editor (Regedit.exe).</span></span>

<span data-ttu-id="7543d-112">Azt is megadhatja a beállításjegyzékbeli elérési út megadásával a beállításjegyzék-szolgáltatójának neve követ "**::**".</span><span class="sxs-lookup"><span data-stu-id="7543d-112">You can also specify this registry path by specifying the registry provider's name, followed by "**::**".</span></span> <span data-ttu-id="7543d-113">A beállításjegyzék-szolgáltatójának teljes neve **Microsoft.PowerShell.Core\\beállításjegyzék**, de ez csak a lerövidíthető **beállításjegyzék**.</span><span class="sxs-lookup"><span data-stu-id="7543d-113">The registry provider's full name is **Microsoft.PowerShell.Core\\Registry**, but this can be shortened to just **Registry**.</span></span> <span data-ttu-id="7543d-114">A következő parancsok felsorolja közvetlenül alatt HKCU tartalma:</span><span class="sxs-lookup"><span data-stu-id="7543d-114">Any of the following commands will list the contents directly under HKCU:</span></span>

```
Get-ChildItem -Path Registry::HKEY_CURRENT_USER
Get-ChildItem -Path Microsoft.PowerShell.Core\Registry::HKEY_CURRENT_USER
Get-ChildItem -Path Registry::HKCU
Get-ChildItem -Path Microsoft.PowerShell.Core\Registry::HKCU
Get-ChildItem HKCU:
```

<span data-ttu-id="7543d-115">Ezek a parancsok listában csak a közvetlenül a benne lévő elemek hasonlóan a Cmd.exe tartozó **DIR** parancs vagy **ls** egy UNIX rendszerhéj.</span><span class="sxs-lookup"><span data-stu-id="7543d-115">These commands list only the directly contained items, much like using Cmd.exe's **DIR** command or **ls** in a UNIX shell.</span></span> <span data-ttu-id="7543d-116">A befoglalt elemek megjelenítése, meg kell adnia a **Recurse** paraméter.</span><span class="sxs-lookup"><span data-stu-id="7543d-116">To show contained items, you need to specify the **Recurse** parameter.</span></span> <span data-ttu-id="7543d-117">Minden beállításkulcsok HKCU listájában, használja a következő parancsot (a művelet egy nagyon hosszú időt vehet igénybe.):</span><span class="sxs-lookup"><span data-stu-id="7543d-117">To list all registry keys in HKCU, use the following command (This operation can take an extremely long time.):</span></span>

```
Get-ChildItem -Path hkcu:\ -Recurse
```

<span data-ttu-id="7543d-118">**Get-ChildItem** összetett szűrési képességek segítségével végezheti a **elérési**, **szűrő**, **Include**, és **kizárása** általában alapú csak a name paraméterek, de ezeket a paramétereket.</span><span class="sxs-lookup"><span data-stu-id="7543d-118">**Get-ChildItem** can perform complex filtering capabilities through its **Path**, **Filter**, **Include**, and **Exclude** parameters, but those parameters are typically based only on name.</span></span> <span data-ttu-id="7543d-119">Összetett szűrés használatával-elemek egyéb tulajdonságok alapján hajthat végre a **Where-Object** parancsmag.</span><span class="sxs-lookup"><span data-stu-id="7543d-119">You can perform complex filtering based on other properties of items by using the **Where-Object** cmdlet.</span></span> <span data-ttu-id="7543d-120">A következő parancs megkeresi HKCU belül minden kulcs:\\szoftver, amely nem több kulcsot, és pontosan négy értékűek is:</span><span class="sxs-lookup"><span data-stu-id="7543d-120">The following command finds all keys within HKCU:\\Software that have no more than one subkey and also have exactly four values:</span></span>

```
Get-ChildItem -Path HKCU:\Software -Recurse | Where-Object -FilterScript {($_.SubKeyCount -le 1) -and ($_.ValueCount -eq 4) }
```

### <a name="copying-keys"></a><span data-ttu-id="7543d-121">Kulcsok másolása</span><span class="sxs-lookup"><span data-stu-id="7543d-121">Copying Keys</span></span>
<span data-ttu-id="7543d-122">Másolás történik a **elem**.</span><span class="sxs-lookup"><span data-stu-id="7543d-122">Copying is done with **Copy-Item**.</span></span> <span data-ttu-id="7543d-123">A következő parancsot, másolja át HKLM:\\szoftver\\Microsoft\\Windows\\CurrentVersion és az összes HKCU annak tulajdonságait:\\, "CurrentVersion" nevű új kulcs létrehozása:</span><span class="sxs-lookup"><span data-stu-id="7543d-123">The following command copies HKLM:\\SOFTWARE\\Microsoft\\Windows\\CurrentVersion and all of its properties to HKCU:\\, creating a new key named "CurrentVersion":</span></span>

```
Copy-Item -Path 'HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion' -Destination hkcu:
```

<span data-ttu-id="7543d-124">Ha megvizsgálja az új kulcsot, a Beállításszerkesztő vagy segítségével **Get-ChildItem**, megfigyelheti, hogy nem kell a benne lévő alkulcsok másolatát az új helyen.</span><span class="sxs-lookup"><span data-stu-id="7543d-124">If you examine this new key in the registry editor or by using **Get-ChildItem**, you will notice that you do not have copies of the contained subkeys in the new location.</span></span> <span data-ttu-id="7543d-125">Ahhoz, hogy a tároló tartalmának másolása, meg kell adnia a **Recurse** paraméter.</span><span class="sxs-lookup"><span data-stu-id="7543d-125">In order to copy all of the contents of a container, you need to specify the **Recurse** parameter.</span></span> <span data-ttu-id="7543d-126">Ahhoz, hogy az előző Másolás parancs rekurzív, akkor használja a parancsot:</span><span class="sxs-lookup"><span data-stu-id="7543d-126">To make the preceding copy command recursive, you would use this command:</span></span>

```
Copy-Item -Path 'HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion' -Destination hkcu: -Recurse
```

<span data-ttu-id="7543d-127">Már elérhető fájlrendszer hozza eszközök továbbra is használhatja.</span><span class="sxs-lookup"><span data-stu-id="7543d-127">You can still use other tools you already have available to perform filesystem copies.</span></span> <span data-ttu-id="7543d-128">A beállításjegyzék szerkesztőeszközeivel – beleértve a reg.exe regini.exe és regedit.exe—and COM objektumok, amelyek támogatják a beállításjegyzék szerkesztésével (például WScript.Shell és a WMI StdRegProv osztály) használhatja a Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7543d-128">Any registry editing tools—including reg.exe, regini.exe, and regedit.exe—and COM objects that support registry editing (such as WScript.Shell and WMI's StdRegProv class) can be used from within Windows PowerShell.</span></span>

### <a name="creating-keys"></a><span data-ttu-id="7543d-129">Kulcsok létrehozása</span><span class="sxs-lookup"><span data-stu-id="7543d-129">Creating Keys</span></span>
<span data-ttu-id="7543d-130">Új kulcsok létrehozása a beállításjegyzékben felügyelete egyszerűbb, mint egy fájlrendszer új elem létrehozásához.</span><span class="sxs-lookup"><span data-stu-id="7543d-130">Creating new keys in the registry is simpler than creating a new item in a file system.</span></span> <span data-ttu-id="7543d-131">Minden beállításkulcsok olyan tárolók, mert nem kell megadnia a elemtípus; egyszerűen megadnia explicit elérési utat, például:</span><span class="sxs-lookup"><span data-stu-id="7543d-131">Because all registry keys are containers, you do not need to specify the item type; you simply supply an explicit path, such as:</span></span>

```
New-Item -Path hkcu:\software_DeleteMe
```

<span data-ttu-id="7543d-132">A szolgáltató alapú elérési segítségével adjon meg egy kulcs:</span><span class="sxs-lookup"><span data-stu-id="7543d-132">You can also use a provider-based path to specify a key:</span></span>

```
New-Item -Path Registry::HKCU_DeleteMe
```

### <a name="deleting-keys"></a><span data-ttu-id="7543d-133">Kulcsok törlése</span><span class="sxs-lookup"><span data-stu-id="7543d-133">Deleting Keys</span></span>
<span data-ttu-id="7543d-134">Az elemek törlése lényegileg azonos összes szolgáltató.</span><span class="sxs-lookup"><span data-stu-id="7543d-134">Deleting items is essentially the same for all providers.</span></span> <span data-ttu-id="7543d-135">A következő parancsok csendes eltávolítja az elemet:</span><span class="sxs-lookup"><span data-stu-id="7543d-135">The following commands will silently remove items:</span></span>

```
Remove-Item -Path hkcu:\Software_DeleteMe
Remove-Item -Path 'hkcu:\key with spaces in the name'
```

### <a name="removing-all-keys-under-a-specific-key"></a><span data-ttu-id="7543d-136">Egy adott kulcs alatt minden kulcs eltávolítása</span><span class="sxs-lookup"><span data-stu-id="7543d-136">Removing All Keys Under a Specific Key</span></span>
<span data-ttu-id="7543d-137">Eltávolíthatja a benne lévő elemek használatával **Remove-cikk**, de kérni fogja az eltávolítás megerősítéséhez, ha az elem tartalmaz dolgozott.</span><span class="sxs-lookup"><span data-stu-id="7543d-137">You can remove contained items by using **Remove-Item**, but you will be prompted to confirm the removal if the item contains anything else.</span></span> <span data-ttu-id="7543d-138">Például, ha azt a HKCU törlésére tett kísérlet:\\CurrentVersion alkulcs létrehozott, ez látható:</span><span class="sxs-lookup"><span data-stu-id="7543d-138">For example, if we attempt to delete the HKCU:\\CurrentVersion subkey we created, we see this:</span></span>

```
Remove-Item -Path hkcu:\CurrentVersion

Confirm
The item at HKCU:\CurrentVersion\AdminDebug has children and the -recurse
parameter was not specified. If you continue, all children will be removed with
 the item. Are you sure you want to continue?
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help
(default is "Y"):
```

<span data-ttu-id="7543d-139">Törli a benne lévő elemek értesítése nélkül, adja meg a **-Recurse** paraméter:</span><span class="sxs-lookup"><span data-stu-id="7543d-139">To delete contained items without prompting, specify the **-Recurse** parameter:</span></span>

```
Remove-Item -Path HKCU:\CurrentVersion -Recurse
```

<span data-ttu-id="7543d-140">Ha eltávolítja az összes elemet HKCU belül:\\CurrentVersion, de nem HKCU:\\maga CurrentVersion, helyette használhatja:</span><span class="sxs-lookup"><span data-stu-id="7543d-140">If you wanted to remove all items within HKCU:\\CurrentVersion but not HKCU:\\CurrentVersion itself, you could instead use:</span></span>

```
Remove-Item -Path HKCU:\CurrentVersion\* -Recurse
```

