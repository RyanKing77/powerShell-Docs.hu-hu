---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: Beállításkulcsok használata
ms.assetid: 91bfaecd-8684-48b4-ad86-065dfe6dc90a
ms.openlocfilehash: e7b497ec2fccf9ba3934439a9c1e9be3cf70a705
ms.sourcegitcommit: f4bd4e116e22c8b5bfcb61680a7c42e58b4da93e
ms.translationtype: HT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/22/2019
ms.locfileid: "59983762"
---
# <a name="working-with-registry-keys"></a><span data-ttu-id="a3071-103">Beállításkulcsok használata</span><span class="sxs-lookup"><span data-stu-id="a3071-103">Working with Registry Keys</span></span>

<span data-ttu-id="a3071-104">Mivel beállításkulcsok a Windows PowerShell-meghajtókon lévő elemek, a használatukat a nagyon hasonló fájlok és mappák használata.</span><span class="sxs-lookup"><span data-stu-id="a3071-104">Because registry keys are items on Windows PowerShell drives, working with them is very similar to working with files and folders.</span></span> <span data-ttu-id="a3071-105">Egy fontos különbséggel, hogy minden eleme egy beállításjegyzék-alapú Windows PowerShell-meghajtón egy tárolóban, csakúgy, mint a fájlrendszer meghajtóján az egyik mappájába.</span><span class="sxs-lookup"><span data-stu-id="a3071-105">One critical difference is that every item on a registry-based Windows PowerShell drive is a container, just like a folder on a file system drive.</span></span> <span data-ttu-id="a3071-106">Azonban a beállításjegyzék-bejegyzések és a hozzájuk tartozó értékek azok az elemek nem különálló elemek tulajdonságai.</span><span class="sxs-lookup"><span data-stu-id="a3071-106">However, registry entries and their associated values are properties of the items, not distinct items.</span></span>

## <a name="listing-all-subkeys-of-a-registry-key"></a><span data-ttu-id="a3071-107">Egy beállításkulcs alkulcsait összes listázása</span><span class="sxs-lookup"><span data-stu-id="a3071-107">Listing All Subkeys of a Registry Key</span></span>

<span data-ttu-id="a3071-108">Közvetlenül egy beállításkulcs található minden elem megjelenítése használatával **Get-ChildItem**.</span><span class="sxs-lookup"><span data-stu-id="a3071-108">You can show all items directly within a registry key by using **Get-ChildItem**.</span></span> <span data-ttu-id="a3071-109">Adja hozzá a választható **kényszerített** rejtettek megjelenítése vagy rendszer elemek paramétert.</span><span class="sxs-lookup"><span data-stu-id="a3071-109">Add the optional **Force** parameter to display hidden or system items.</span></span> <span data-ttu-id="a3071-110">Ha például a parancs megjeleníti a közvetlenül a Windows PowerShell meghajtót HKCU található elem:, amely megfelel a HKEY_CURRENT_USER beállításjegyzék-struktúrát:</span><span class="sxs-lookup"><span data-stu-id="a3071-110">For example, this command displays the items directly within Windows PowerShell drive HKCU:, which corresponds to the HKEY_CURRENT_USER registry hive:</span></span>

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

<span data-ttu-id="a3071-111">Ezek a HKEY_CURRENT_USER a a Beállításszerkesztőt (Regedit.exe) alatt látható a legfelső szintű kulcsokat.</span><span class="sxs-lookup"><span data-stu-id="a3071-111">These are the top-level keys visible under HKEY_CURRENT_USER in the Registry Editor (Regedit.exe).</span></span>

<span data-ttu-id="a3071-112">Azt is beállíthatja a beállításjegyzékbeli elérési út megadásával a beállításjegyzék-szolgáltatójának neve, majd "**::**".</span><span class="sxs-lookup"><span data-stu-id="a3071-112">You can also specify this registry path by specifying the registry provider's name, followed by "**::**".</span></span> <span data-ttu-id="a3071-113">A beállításjegyzék-szolgáltató teljes neve **Microsoft.PowerShell.Core\\beállításjegyzék**, de ez csupán lerövidíthető **beállításjegyzék**.</span><span class="sxs-lookup"><span data-stu-id="a3071-113">The registry provider's full name is **Microsoft.PowerShell.Core\\Registry**, but this can be shortened to just **Registry**.</span></span> <span data-ttu-id="a3071-114">A következő parancsokhoz felsorolja a tartalmat közvetlenül a HKCU alatt:</span><span class="sxs-lookup"><span data-stu-id="a3071-114">Any of the following commands will list the contents directly under HKCU:</span></span>

```powershell
Get-ChildItem -Path Registry::HKEY_CURRENT_USER
Get-ChildItem -Path Microsoft.PowerShell.Core\Registry::HKEY_CURRENT_USER
Get-ChildItem -Path Registry::HKCU
Get-ChildItem -Path Microsoft.PowerShell.Core\Registry::HKCU
Get-ChildItem HKCU:
```

<span data-ttu-id="a3071-115">Ezek a parancsok listája csak a közvetlenül benne lévő elemek, hasonlóan a Cmd.exe használatával **DIR** parancs vagy **ls** egy UNIX-rendszerhéjban.</span><span class="sxs-lookup"><span data-stu-id="a3071-115">These commands list only the directly contained items, much like using Cmd.exe's **DIR** command or **ls** in a UNIX shell.</span></span> <span data-ttu-id="a3071-116">A befoglalt elemek megjelenítése, meg kell adnia a **Recurse** paraméter.</span><span class="sxs-lookup"><span data-stu-id="a3071-116">To show contained items, you need to specify the **Recurse** parameter.</span></span> <span data-ttu-id="a3071-117">Minden beállításkulcsok HKCU listájában, használja az alábbi parancsot (Ez a művelet egy rendkívül hosszú időbe telhet.):</span><span class="sxs-lookup"><span data-stu-id="a3071-117">To list all registry keys in HKCU, use the following command (This operation can take an extremely long time.):</span></span>

```powershell
Get-ChildItem -Path hkcu:\ -Recurse
```

<span data-ttu-id="a3071-118">**Get-ChildItem** összetett szűrési képességek segítségével elvégezheti a **elérési**, **szűrő**, **Belefoglalás**, és **kizárása**általában alapú csak a name paraméter, de ezeket a paramétereket.</span><span class="sxs-lookup"><span data-stu-id="a3071-118">**Get-ChildItem** can perform complex filtering capabilities through its **Path**, **Filter**, **Include**, and **Exclude** parameters, but those parameters are typically based only on name.</span></span> <span data-ttu-id="a3071-119">Összetett szűrését az egyéb elemek tulajdonságai alapján is végezhet a **Where-Object** parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="a3071-119">You can perform complex filtering based on other properties of items by using the **Where-Object** cmdlet.</span></span> <span data-ttu-id="a3071-120">A következő parancs megkeresi a HKCU belül az összes kulcs:\\szoftver, amely legfeljebb egy kulcsot, és pontosan négy értéket is rendelkeznek:</span><span class="sxs-lookup"><span data-stu-id="a3071-120">The following command finds all keys within HKCU:\\Software that have no more than one subkey and also have exactly four values:</span></span>

```powershell
Get-ChildItem -Path HKCU:\Software -Recurse | Where-Object -FilterScript {($_.SubKeyCount -le 1) -and ($_.ValueCount -eq 4) }
```

## <a name="copying-keys"></a><span data-ttu-id="a3071-121">Kulcsok másolása</span><span class="sxs-lookup"><span data-stu-id="a3071-121">Copying Keys</span></span>

<span data-ttu-id="a3071-122">Másolás végzett **Copy-Item**.</span><span class="sxs-lookup"><span data-stu-id="a3071-122">Copying is done with **Copy-Item**.</span></span> <span data-ttu-id="a3071-123">A következő parancsot, másolja át HKLM:\\szoftver\\Microsoft\\Windows\\CurrentVersion és az összes hozzá tartozó tulajdonságok HKCU:\\, "CurrentVersion" nevű új kulcs létrehozása:</span><span class="sxs-lookup"><span data-stu-id="a3071-123">The following command copies HKLM:\\SOFTWARE\\Microsoft\\Windows\\CurrentVersion and all of its properties to HKCU:\\, creating a new key named "CurrentVersion":</span></span>

```powershell
Copy-Item -Path 'HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion' -Destination hkcu:
```

<span data-ttu-id="a3071-124">Ha megvizsgálja az új kulcs a Beállításszerkesztő vagy a **Get-ChildItem**, megfigyelheti, hogy nem kell a tartalmazott alkulcsok másolatát az új helyen.</span><span class="sxs-lookup"><span data-stu-id="a3071-124">If you examine this new key in the registry editor or by using **Get-ChildItem**, you will notice that you do not have copies of the contained subkeys in the new location.</span></span> <span data-ttu-id="a3071-125">Annak érdekében, hogy a tároló tartalmának másolása, meg kell adnia a **Recurse** paraméter.</span><span class="sxs-lookup"><span data-stu-id="a3071-125">In order to copy all of the contents of a container, you need to specify the **Recurse** parameter.</span></span> <span data-ttu-id="a3071-126">Ahhoz, hogy az előző másolási parancs rekurzív, használja ezt a parancsot:</span><span class="sxs-lookup"><span data-stu-id="a3071-126">To make the preceding copy command recursive, you would use this command:</span></span>

```powershell
Copy-Item -Path 'HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion' -Destination hkcu: -Recurse
```

<span data-ttu-id="a3071-127">Már elérhető fájlrendszer másolatok végrehajtásához más eszközök továbbra is használhatja.</span><span class="sxs-lookup"><span data-stu-id="a3071-127">You can still use other tools you already have available to perform filesystem copies.</span></span> <span data-ttu-id="a3071-128">Minden olyan beállításjegyzék szerkesztőeszközeihez – beleértve a beállításjegyzék szerkesztése (például WScript.Shell és a WMI StdRegProv osztály) támogató reg.exe regini.exe és regedit.exe—and COM-objektumok is használható a Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a3071-128">Any registry editing tools—including reg.exe, regini.exe, and regedit.exe—and COM objects that support registry editing (such as WScript.Shell and WMI's StdRegProv class) can be used from within Windows PowerShell.</span></span>

## <a name="creating-keys"></a><span data-ttu-id="a3071-129">Kulcsok létrehozása</span><span class="sxs-lookup"><span data-stu-id="a3071-129">Creating Keys</span></span>

<span data-ttu-id="a3071-130">Új kulcsok létrehozása a beállításjegyzékben egyszerűbb, mint a fájlrendszer egy új elem létrehozása.</span><span class="sxs-lookup"><span data-stu-id="a3071-130">Creating new keys in the registry is simpler than creating a new item in a file system.</span></span> <span data-ttu-id="a3071-131">Mivel az összes beállításkulcsok tárolók, nem kell megadnia a elemtípus; egyszerűen adhat meg explicit elérési utat, mint például:</span><span class="sxs-lookup"><span data-stu-id="a3071-131">Because all registry keys are containers, you do not need to specify the item type; you simply supply an explicit path, such as:</span></span>

```powershell
New-Item -Path hkcu:\software_DeleteMe
```

<span data-ttu-id="a3071-132">Olyan szolgáltató alapú elérési út használatával adja meg a kulcs:</span><span class="sxs-lookup"><span data-stu-id="a3071-132">You can also use a provider-based path to specify a key:</span></span>

```powershell
New-Item -Path Registry::HKCU_DeleteMe
```

## <a name="deleting-keys"></a><span data-ttu-id="a3071-133">Kulcsok törlése</span><span class="sxs-lookup"><span data-stu-id="a3071-133">Deleting Keys</span></span>

<span data-ttu-id="a3071-134">Elemek törlése lényegében ugyanúgy történik minden szolgáltató számára.</span><span class="sxs-lookup"><span data-stu-id="a3071-134">Deleting items is essentially the same for all providers.</span></span> <span data-ttu-id="a3071-135">Elemek csendes eltávolítja a következő parancsokat:</span><span class="sxs-lookup"><span data-stu-id="a3071-135">The following commands will silently remove items:</span></span>

```powershell
Remove-Item -Path hkcu:\Software_DeleteMe
Remove-Item -Path 'hkcu:\key with spaces in the name'
```

## <a name="removing-all-keys-under-a-specific-key"></a><span data-ttu-id="a3071-136">Egy adott kulcs alapján minden kulcs eltávolítása</span><span class="sxs-lookup"><span data-stu-id="a3071-136">Removing All Keys Under a Specific Key</span></span>

<span data-ttu-id="a3071-137">Eltávolíthatja a benne lévő elemek használatával **Remove-cikk**, de meg kell adnia az eltávolítás megerősítéséhez, ha az elem tartalmaz bármi más.</span><span class="sxs-lookup"><span data-stu-id="a3071-137">You can remove contained items by using **Remove-Item**, but you will be prompted to confirm the removal if the item contains anything else.</span></span> <span data-ttu-id="a3071-138">Ha például azt próbál meg törölni a HKCU:\\CurrentVersion alkulcs hoztunk létre, ez látható:</span><span class="sxs-lookup"><span data-stu-id="a3071-138">For example, if we attempt to delete the HKCU:\\CurrentVersion subkey we created, we see this:</span></span>

```
Remove-Item -Path hkcu:\CurrentVersion

Confirm
The item at HKCU:\CurrentVersion\AdminDebug has children and the -recurse
parameter was not specified. If you continue, all children will be removed with
 the item. Are you sure you want to continue?
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help
(default is "Y"):
```

<span data-ttu-id="a3071-139">Rákérdezés nélkül törli a benne lévő elemek, adja meg a **-Recurse** paramétert:</span><span class="sxs-lookup"><span data-stu-id="a3071-139">To delete contained items without prompting, specify the **-Recurse** parameter:</span></span>

```powershell
Remove-Item -Path HKCU:\CurrentVersion -Recurse
```

<span data-ttu-id="a3071-140">Ha szeretne HKCU található minden elem eltávolítása:\\CurrentVersion, de nem HKCU:\\maga CurrentVersion, Ehelyett használhatja:</span><span class="sxs-lookup"><span data-stu-id="a3071-140">If you wanted to remove all items within HKCU:\\CurrentVersion but not HKCU:\\CurrentVersion itself, you could instead use:</span></span>

```powershell
Remove-Item -Path HKCU:\CurrentVersion\* -Recurse
```