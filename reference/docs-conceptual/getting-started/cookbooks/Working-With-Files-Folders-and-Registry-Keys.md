---
ms.date: 06/05/2017
keywords: PowerShell parancsmag
title: Fájlmappák és beállításkulcsok használata
ms.assetid: e6cf87aa-b5f8-48d5-a75a-7cb7ecb482dc
ms.openlocfilehash: a09b127d4ba37d33cb4c0f0ce0819e645fd4b137
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
ms.locfileid: "30952307"
---
# <a name="working-with-files-folders-and-registry-keys"></a><span data-ttu-id="c6419-103">A fájlok, mappák és beállításkulcsok</span><span class="sxs-lookup"><span data-stu-id="c6419-103">Working With Files, Folders and Registry Keys</span></span>

<span data-ttu-id="c6419-104">A Windows PowerShell használja a főnév **elem** utal, egy Windows PowerShell-meghajtón található elemekre.</span><span class="sxs-lookup"><span data-stu-id="c6419-104">Windows PowerShell uses the noun **Item** to refer to items found on a Windows PowerShell drive.</span></span> <span data-ttu-id="c6419-105">A Windows PowerShell fájlrendszer-szolgáltatót, amikor egy **elem** lehet, hogy a fájl, mappa vagy a Windows PowerShell meghajtót.</span><span class="sxs-lookup"><span data-stu-id="c6419-105">When dealing with the Windows PowerShell FileSystem provider, an **Item** might be a file, a folder, or the Windows PowerShell drive.</span></span> <span data-ttu-id="c6419-106">Listázása, és ezek az elemek használata a legtöbb felügyeleti beállítások kritikus alapvető tevékenység, így azt szeretnénk, és beszéljék meg ezeket a feladatokat részletesen.</span><span class="sxs-lookup"><span data-stu-id="c6419-106">Listing and working with these items is a critical basic task in most administrative settings, so we want to discuss these tasks in detail.</span></span>

### <a name="enumerating-files-folders-and-registry-keys-get-childitem"></a><span data-ttu-id="c6419-107">Fájlok, mappák és beállításkulcsok (Get-ChildItem) számbavétele</span><span class="sxs-lookup"><span data-stu-id="c6419-107">Enumerating Files, Folders, and Registry Keys (Get-ChildItem)</span></span>

<span data-ttu-id="c6419-108">Elemek gyűjteménye lekérése egy adott helyen egy ilyen közös feladat, mivel a **Get-ChildItem** parancsmag célja kifejezetten a tárolóhoz, például egy mappában található elemeket.</span><span class="sxs-lookup"><span data-stu-id="c6419-108">Since getting a collection of items from a particular location is such a common task, the **Get-ChildItem** cmdlet is designed specifically to return all items found within a container such as a folder.</span></span>

<span data-ttu-id="c6419-109">Ha szeretne visszaállítani, minden fájl és mappa, amely közvetlenül a C: mappában található\\Windows, típus:</span><span class="sxs-lookup"><span data-stu-id="c6419-109">If you want to return all files and folders that are contained directly within the folder C:\\Windows, type:</span></span>

```
PS> Get-ChildItem -Path C:\Windows
    Directory: Microsoft.Windows PowerShell.Core\FileSystem::C:\Windows

Mode                LastWriteTime     Length Name
----                -------------     ------ ----
-a---        2006-05-16   8:10 AM          0 0.log
-a---        2005-11-29   3:16 PM         97 acc1.txt
-a---        2005-10-23  11:21 PM       3848 actsetup.log
...
```

<span data-ttu-id="c6419-110">A lista tartalmazza a következőhöz hasonló mi mutatunk be kell megadni a **dir** parancsot **Cmd.exe**, vagy a **ls** parancsot egy UNIX parancs-rendszerhéjban.</span><span class="sxs-lookup"><span data-stu-id="c6419-110">The listing looks similar to what you would see when you enter the **dir** command in **Cmd.exe**, or the **ls** command in a UNIX command shell.</span></span>

<span data-ttu-id="c6419-111">A paraméterek használatával nagyon összetett listaelemek végezheti el a **Get-ChildItem** parancsmag.</span><span class="sxs-lookup"><span data-stu-id="c6419-111">You can perform very complex listings by using parameters of the **Get-ChildItem** cmdlet.</span></span> <span data-ttu-id="c6419-112">Követően áttekintjük néhány olyan forgatókönyvet mellett.</span><span class="sxs-lookup"><span data-stu-id="c6419-112">We will look at a few scenarios next.</span></span> <span data-ttu-id="c6419-113">Megtekintheti a szintaxist a **Get-ChildItem** parancsmag beírásával:</span><span class="sxs-lookup"><span data-stu-id="c6419-113">You can see the syntax the **Get-ChildItem** cmdlet by typing:</span></span>

```powershell
Get-Command -Name Get-ChildItem -Syntax
```

<span data-ttu-id="c6419-114">Ezek a paraméterek vegyes, és nagy mértékben testre szabott kimeneti beolvasandó egyezik.</span><span class="sxs-lookup"><span data-stu-id="c6419-114">These parameters can be mixed and matched to get highly customized output.</span></span>

#### <a name="listing-all-contained-items--recurse"></a><span data-ttu-id="c6419-115">Minden tartalmazott elemek listázása (-Recurse)</span><span class="sxs-lookup"><span data-stu-id="c6419-115">Listing all Contained Items (-Recurse)</span></span>

<span data-ttu-id="c6419-116">A Windows mappában található elemek, mind az almappák belüli elemek megtekintéséhez használja a **Recurse** paramétere **Get-ChildItem**.</span><span class="sxs-lookup"><span data-stu-id="c6419-116">To see both the items inside a Windows folder and any items that are contained within the subfolders, use the **Recurse** parameter of **Get-ChildItem**.</span></span> <span data-ttu-id="c6419-117">Az átjáróra a listában jeleníti meg minden belül a Windows mappa és annak almappáiban található elemek.</span><span class="sxs-lookup"><span data-stu-id="c6419-117">The listing displays everything within the Windows folder and the items in its subfolders.</span></span> <span data-ttu-id="c6419-118">Például:</span><span class="sxs-lookup"><span data-stu-id="c6419-118">For example:</span></span>

```
PS> Get-ChildItem -Path C:\WINDOWS -Recurse

    Directory: Microsoft.Windows PowerShell.Core\FileSystem::C:\WINDOWS
    Directory: Microsoft.Windows PowerShell.Core\FileSystem::C:\WINDOWS\AppPatch
Mode                LastWriteTime     Length Name
----                -------------     ------ ----
-a---        2004-08-04   8:00 AM    1852416 AcGenral.dll
...
```

#### <a name="filtering-items-by-name--name"></a><span data-ttu-id="c6419-119">A Szűrés név alapján (-név)</span><span class="sxs-lookup"><span data-stu-id="c6419-119">Filtering Items by Name (-Name)</span></span>

<span data-ttu-id="c6419-120">Csak az elemek nevei megjelenítéséhez használja a **neve** paramétere **Get-Childitem**:</span><span class="sxs-lookup"><span data-stu-id="c6419-120">To display only the names of items, use the **Name** parameter of **Get-Childitem**:</span></span>

```
PS> Get-ChildItem -Path C:\WINDOWS -Name
addins
AppPatch
assembly
...
```

#### <a name="forcibly-listing-hidden-items--force"></a><span data-ttu-id="c6419-121">Kényszerített módon a rejtett elemek listázása (-Force)</span><span class="sxs-lookup"><span data-stu-id="c6419-121">Forcibly Listing Hidden Items (-Force)</span></span>

<span data-ttu-id="c6419-122">Elemek, amelyek normál esetben nem látható a Fájlkezelőben vagy a Cmd.exe nem jelennek meg a kimenete egy **Get-ChildItem** parancsot.</span><span class="sxs-lookup"><span data-stu-id="c6419-122">Items that are normally invisible in File Explorer or Cmd.exe are not displayed in the output of a **Get-ChildItem** command.</span></span> <span data-ttu-id="c6419-123">Rejtett elemek megjelenítéséhez használja a **kényszerített** paramétere **Get-ChildItem**.</span><span class="sxs-lookup"><span data-stu-id="c6419-123">To display hidden items, use the **Force** parameter of **Get-ChildItem**.</span></span> <span data-ttu-id="c6419-124">Például:</span><span class="sxs-lookup"><span data-stu-id="c6419-124">For example:</span></span>

```powershell
Get-ChildItem -Path C:\Windows -Force
```

<span data-ttu-id="c6419-125">Ez a paraméter neve kényszerített mert kényszerített felülírhatja, normál viselkedése a **Get-ChildItem** parancsot.</span><span class="sxs-lookup"><span data-stu-id="c6419-125">This parameter is named Force because you can forcibly override the normal behavior of the **Get-ChildItem** command.</span></span> <span data-ttu-id="c6419-126">Kényszerített kényszeríti egy műveletet, amely a parancsmag nem általában kell elvégeznie, bár nem hajt végre semmilyen művelet, amely a rendszer biztonsági gyengíti széles körben használt paramétereinek.</span><span class="sxs-lookup"><span data-stu-id="c6419-126">Force is a widely used parameter that forces an action that a cmdlet would not normally perform, although it will not perform any action that compromises the security of the system.</span></span>

#### <a name="matching-item-names-with-wildcards"></a><span data-ttu-id="c6419-127">A helyettesítő karakterek egyező elemek nevei</span><span class="sxs-lookup"><span data-stu-id="c6419-127">Matching Item Names with Wildcards</span></span>

<span data-ttu-id="c6419-128">**A Get-ChildItem** parancs fogad el helyettesítő karakterek az elérési út az elemek listázásához.</span><span class="sxs-lookup"><span data-stu-id="c6419-128">**The Get-ChildItem** command accepts wildcards in the path of the items to list.</span></span>

<span data-ttu-id="c6419-129">Helyettesítő karakterek megfeleltetése végzi el a Windows PowerShell-motor, mert az összes parancsmag, amely támogatja a helyettesítő karakterek azonos jelöléssel, és rendelkezik a megfelelő viselkedést.</span><span class="sxs-lookup"><span data-stu-id="c6419-129">Because wildcard matching is handled by the Windows PowerShell engine, all cmdlets that accepts wildcards use the same notation and have the same matching behavior.</span></span> <span data-ttu-id="c6419-130">A Windows PowerShell helyettesítő notation tartalmazza:</span><span class="sxs-lookup"><span data-stu-id="c6419-130">The Windows PowerShell wildcard notation includes:</span></span>

- <span data-ttu-id="c6419-131">A csillag karakter (\*) bármely karakter nulla vagy több előfordulásának felel meg.</span><span class="sxs-lookup"><span data-stu-id="c6419-131">Asterisk (\*)matches zero or more occurrences of any character.</span></span>

- <span data-ttu-id="c6419-132">A kérdőjel (?) felel meg pontosan egy karaktert.</span><span class="sxs-lookup"><span data-stu-id="c6419-132">Question mark (?) matches exactly one character.</span></span>

- <span data-ttu-id="c6419-133">Nyitó szögletes zárójel (\[) szögletes zárójel (]) és karakter között legyen, megfeleltethetők karakterek.</span><span class="sxs-lookup"><span data-stu-id="c6419-133">Left bracket (\[) character and right bracket (]) character surround a set of characters to be matched.</span></span>

<span data-ttu-id="c6419-134">Az alábbiakban néhány olyan helyettesítő specification működése.</span><span class="sxs-lookup"><span data-stu-id="c6419-134">Here are some examples of how wildcard specification works.</span></span>

<span data-ttu-id="c6419-135">A utótagot a Windows könyvtárban található összes fájl **.log** , és pontosan öt karakter nevét, írja be a következő parancsot:</span><span class="sxs-lookup"><span data-stu-id="c6419-135">To find all files in the Windows directory with the suffix **.log** and exactly five characters in the base name, enter the following command:</span></span>

```
PS> Get-ChildItem -Path C:\Windows\?????.log

    Directory: Microsoft.Windows PowerShell.Core\FileSystem::C:\Windows
Mode                LastWriteTime     Length Name
----                -------------     ------ ----
...
-a---        2006-05-11   6:31 PM     204276 ocgen.log
-a---        2006-05-11   6:31 PM      22365 ocmsn.log
...
-a---        2005-11-11   4:55 AM         64 setup.log
-a---        2005-12-15   2:24 PM      17719 VxSDM.log
...
```

<span data-ttu-id="c6419-136">Található összes fájl, a betűvel kezdődő **x** a Windows könyvtárban, írja be:</span><span class="sxs-lookup"><span data-stu-id="c6419-136">To find all files that begin with the letter **x** in the Windows directory, type:</span></span>

```powershell
Get-ChildItem -Path C:\Windows\x*
```

<span data-ttu-id="c6419-137">Található összes fájl kezdődő **x** vagy **z**, típus:</span><span class="sxs-lookup"><span data-stu-id="c6419-137">To find all files whose names begin with **x** or **z**, type:</span></span>

```powershell
Get-ChildItem -Path C:\Windows\[xz]*
```

#### <a name="excluding-items--exclude"></a><span data-ttu-id="c6419-138">Elemek kizárása (-kizárása)</span><span class="sxs-lookup"><span data-stu-id="c6419-138">Excluding Items (-Exclude)</span></span>

<span data-ttu-id="c6419-139">Kizárhat meghatározott elemek használatával a **kizárása** Get-ChildItem paramétere.</span><span class="sxs-lookup"><span data-stu-id="c6419-139">You can exclude specific items by using the **Exclude** parameter of Get-ChildItem.</span></span> <span data-ttu-id="c6419-140">Ez lehetővé teszi összetett szűrést a egy utasítás végrehajtásához.</span><span class="sxs-lookup"><span data-stu-id="c6419-140">This lets you perform complex filtering in a single statement.</span></span>

<span data-ttu-id="c6419-141">Tegyük fel például, a System32 mappában található a Windows idő szolgáltatás DLL kívánt, és az összes DLL-fájl nevére emlékszik, hogy a "W" szóval kezdődik, és rendelkezik-e "32" azt.</span><span class="sxs-lookup"><span data-stu-id="c6419-141">For example, suppose you are trying to find the Windows Time Service DLL in the System32 folder, and all you can remember about the DLL name is that it begins with "W" and has "32" in it.</span></span>

<span data-ttu-id="c6419-142">Egy kifejezés, például **w\&#42; 32\&#42;. dll** található összes DLL-fájl, amely megfelel a feltételeknek, de előfordulhat, hogy is vissza a Windows 95 és 16 bites Windows kompatibilitási DLL-fájl, amely tartalmazza az "95" vagy "16" a név.</span><span class="sxs-lookup"><span data-stu-id="c6419-142">An expression like **w\&#42;32\&#42;.dll** will find all DLLs that satisfy the conditions, but it may also return the Windows 95 and 16-bit Windows compatibility DLLs that include "95" or "16" in their names.</span></span> <span data-ttu-id="c6419-143">Fájlok, amelyek segítségével a név nem tartalmazhatják a számok, akkor kihagyhatja a **kizárása** mintájú paraméter  **\&#42;\[ 9516]\&#42;**:</span><span class="sxs-lookup"><span data-stu-id="c6419-143">You can omit files that have any of these numbers in their names by using the **Exclude** parameter with the pattern **\&#42;\[9516]\&#42;**:</span></span>

```
PS> Get-ChildItem -Path C:\WINDOWS\System32\w*32*.dll -Exclude *[9516]*

Directory: Microsoft.PowerShell.Core\FileSystem::C:\WINDOWS\System32
Mode                LastWriteTime     Length Name
----                -------------     ------ ----
-a---        2004-08-04   8:00 AM     174592 w32time.dll
-a---        2004-08-04   8:00 AM      22016 w32topl.dll
-a---        2004-08-04   8:00 AM     101888 win32spl.dll
-a---        2004-08-04   8:00 AM     172032 wldap32.dll
-a---        2004-08-04   8:00 AM     264192 wow32.dll
-a---        2004-08-04   8:00 AM      82944 ws2_32.dll
-a---        2004-08-04   8:00 AM      42496 wsnmp32.dll
-a---        2004-08-04   8:00 AM      22528 wsock32.dll
-a---        2004-08-04   8:00 AM      18432 wtsapi32.dll
```

#### <a name="mixing-get-childitem-parameters"></a><span data-ttu-id="c6419-144">Get-ChildItem paraméterek keverése</span><span class="sxs-lookup"><span data-stu-id="c6419-144">Mixing Get-ChildItem Parameters</span></span>

<span data-ttu-id="c6419-145">Több paramétereinek a **Get-ChildItem** parancsmagja ugyanezt a parancsot.</span><span class="sxs-lookup"><span data-stu-id="c6419-145">You can use several of the parameters of the **Get-ChildItem** cmdlet in the same command.</span></span> <span data-ttu-id="c6419-146">Előtt kombinálhatók paraméterek, mindenképpen tájékozódjon a helyettesítő karakterek megfeleltetése.</span><span class="sxs-lookup"><span data-stu-id="c6419-146">Before you mix parameters, be sure that you understand wildcard matching.</span></span> <span data-ttu-id="c6419-147">A következő parancs például nincs eredmény eredményt adja vissza:</span><span class="sxs-lookup"><span data-stu-id="c6419-147">For example, the following command returns no results:</span></span>

```powershell
Get-ChildItem -Path C:\Windows\*.dll -Recurse -Exclude [a-y]*.dll
```

<span data-ttu-id="c6419-148">Annak ellenére, hogy van két dll, a Windows mappában található "z" betűvel kezdődő, nincsenek nem járt eredménnyel.</span><span class="sxs-lookup"><span data-stu-id="c6419-148">There are no results, even though there are two DLLs that begin with the letter "z" in the Windows folder.</span></span>

<span data-ttu-id="c6419-149">Nincs eredmény mert azt az elérési út egy része a helyettesítő megadva.</span><span class="sxs-lookup"><span data-stu-id="c6419-149">No results were returned because we specified the wildcard as part of the path.</span></span> <span data-ttu-id="c6419-150">Annak ellenére, hogy a parancs a következő volt rekurzív, a **Get-ChildItem** parancsmag elemeket korlátozva azokat, amelyeket a Windows mappában található ".dll" végződő nevű.</span><span class="sxs-lookup"><span data-stu-id="c6419-150">Even though the command was recursive, the **Get-ChildItem** cmdlet restricted the items to those that are in the Windows folder with names ending with ".dll".</span></span>

<span data-ttu-id="c6419-151">Fájlok, amelyek neve különleges mintát illeszteni rekurzív keresését megadásához használja a **-tartalmaznak** paraméter.</span><span class="sxs-lookup"><span data-stu-id="c6419-151">To specify a recursive search for files whose names match a special pattern, use the **-Include** parameter.</span></span>

```
PS> Get-ChildItem -Path C:\Windows -Include *.dll -Recurse -Exclude [a-y]*.dll

    Directory: Microsoft.Windows PowerShell.Core\FileSystem::C:\Windows\System32\Setup

Mode                LastWriteTime     Length Name
----                -------------     ------ ----
-a---        2004-08-04   8:00 AM       8261 zoneoc.dll

    Directory: Microsoft.Windows PowerShell.Core\FileSystem::C:\Windows\System32

Mode                LastWriteTime     Length Name
----                -------------     ------ ----
-a---        2004-08-04   8:00 AM     337920 zipfldr.dll
```