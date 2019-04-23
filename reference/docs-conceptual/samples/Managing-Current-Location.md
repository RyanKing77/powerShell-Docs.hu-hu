---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: Aktuális hely kezelése
ms.assetid: a9f9e7a7-3ea8-47d3-bbb4-6e437f6d4a4a
ms.openlocfilehash: f5e0653b2c3bbc9d2526c7a1c2ff88a8a6641695
ms.sourcegitcommit: f4bd4e116e22c8b5bfcb61680a7c42e58b4da93e
ms.translationtype: HT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/22/2019
ms.locfileid: "59984425"
---
# <a name="managing-current-location"></a><span data-ttu-id="16bf7-103">Aktuális hely kezelése</span><span class="sxs-lookup"><span data-stu-id="16bf7-103">Managing Current Location</span></span>

<span data-ttu-id="16bf7-104">A Fájlkezelőben mappa rendszerek navigáláskor általában rendelkeznek egy adott működő helyen -, az aktuális mappa megnyitása.</span><span class="sxs-lookup"><span data-stu-id="16bf7-104">When navigating folder systems in File Explorer, you usually have a specific working location - namely, the current open folder.</span></span> <span data-ttu-id="16bf7-105">Az aktuális mappa elemeinek rájuk kattintva könnyen kezelhetők.</span><span class="sxs-lookup"><span data-stu-id="16bf7-105">Items in the current folder can be manipulated easily by clicking them.</span></span> <span data-ttu-id="16bf7-106">Tartozó parancssori felületek, például a Cmd.exe Ha egy adott fájl ugyanabban a mappában, elérheti adjon meg egy viszonylag rövid, nem pedig mintha meg kellene adnia a fájl teljes elérési útja.</span><span class="sxs-lookup"><span data-stu-id="16bf7-106">For command-line interfaces such as Cmd.exe, when you are in the same folder as a particular file, you can access it by specifying a relatively short name, rather than needing to specify the entire path to the file.</span></span> <span data-ttu-id="16bf7-107">Az aktuális könyvtár neve a munkakönyvtárat.</span><span class="sxs-lookup"><span data-stu-id="16bf7-107">The current directory is called the working directory.</span></span>

<span data-ttu-id="16bf7-108">Windows PowerShell használja a főnév **hely** lehet hivatkozni a munkakönyvtárban és valósítja meg a családba tartozó parancsmagok vizsgálja meg, és a hely kezeléséhez.</span><span class="sxs-lookup"><span data-stu-id="16bf7-108">Windows PowerShell uses the noun **Location** to refer to the working directory, and implements a family of cmdlets to examine and manipulate your location.</span></span>

## <a name="getting-your-current-location-get-location"></a><span data-ttu-id="16bf7-109">Bevezetés az aktuális tartózkodási helyét (Get-hely)</span><span class="sxs-lookup"><span data-stu-id="16bf7-109">Getting Your Current Location (Get-Location)</span></span>

<span data-ttu-id="16bf7-110">Annak megállapításához, az aktuális könyvtár hely elérési útja, adja meg a **Get-Location** parancsot:</span><span class="sxs-lookup"><span data-stu-id="16bf7-110">To determine the path of your current directory location, enter the **Get-Location** command:</span></span>

```
PS> Get-Location
Path
----
C:\Documents and Settings\PowerUser
```

> [!NOTE]
> <span data-ttu-id="16bf7-111">A Get-Location parancsmag hasonlít a **pwd** parancs a bash.</span><span class="sxs-lookup"><span data-stu-id="16bf7-111">The Get-Location cmdlet is similar to the **pwd** command in the BASH shell.</span></span> <span data-ttu-id="16bf7-112">A hely beállítása parancsmag hasonlít a **cd** Cmd.exe parancsot.</span><span class="sxs-lookup"><span data-stu-id="16bf7-112">The Set-Location cmdlet is similar to the **cd** command in Cmd.exe.</span></span>

## <a name="setting-your-current-location-set-location"></a><span data-ttu-id="16bf7-113">Az aktuális tartózkodási helyét (hely beállítása) beállítást</span><span class="sxs-lookup"><span data-stu-id="16bf7-113">Setting Your Current Location (Set-Location)</span></span>

<span data-ttu-id="16bf7-114">A **Get-Location** parancs szolgál a **hely beállítása** parancsot.</span><span class="sxs-lookup"><span data-stu-id="16bf7-114">The **Get-Location** command is used with the **Set-Location** command.</span></span> <span data-ttu-id="16bf7-115">A **hely beállítása** parancs lehetővé teszi, hogy adja meg az aktuális könyvtár helyet.</span><span class="sxs-lookup"><span data-stu-id="16bf7-115">The **Set-Location** command allows you to specify your current directory location.</span></span>

```powershell
Set-Location -Path C:\Windows
```

<span data-ttu-id="16bf7-116">Miután megadta a parancs, megfigyelheti, hogy nem jelenik meg a parancs hatásáról közvetlen visszajelzést.</span><span class="sxs-lookup"><span data-stu-id="16bf7-116">After you enter the command, you will notice that you do not receive any direct feedback about the effect of the command.</span></span> <span data-ttu-id="16bf7-117">A legtöbb Windows PowerShell-parancsokat, amelyek egy műveletet állít elő alig vagy egyáltalán nem kimenetet, mert a kimenet nem mindig lehet hasznos.</span><span class="sxs-lookup"><span data-stu-id="16bf7-117">Most Windows PowerShell commands that perform an action produce little or no output because the output is not always useful.</span></span> <span data-ttu-id="16bf7-118">Ellenőrizze, hogy sikeres directory módosítás történt a megadásakor a **hely beállítása** parancshoz, például a **- PassThru** paraméter megadásakor a **Set-Location**parancsot:</span><span class="sxs-lookup"><span data-stu-id="16bf7-118">To verify that a successful directory change has occurred when you enter the **Set-Location** command, include the **-PassThru** parameter when you enter the **Set-Location** command:</span></span>

```
PS> Set-Location -Path C:\Windows -PassThru

Path
----
C:\WINDOWS
```

<span data-ttu-id="16bf7-119">A **- PassThru** paraméter az eredmény információt ad vissza, amelyben nem nincs alapértelmezett kimenet esetekben használható a Windows PowerShell számos Set-parancsokkal.</span><span class="sxs-lookup"><span data-stu-id="16bf7-119">The **-PassThru** parameter can be used with many Set commands in Windows PowerShell to return information about the result in cases in which there is no default output.</span></span>

<span data-ttu-id="16bf7-120">Megadhat elérési utak viszonyított jelenlegi tartózkodási ugyanúgy szerint, akkor a legtöbb UNIX- és Windows parancs ismertetése.</span><span class="sxs-lookup"><span data-stu-id="16bf7-120">You can specify paths relative to your current location in the same way as you would in most UNIX and Windows command shells.</span></span> <span data-ttu-id="16bf7-121">A relatív elérési utakat, a standard szintű jelölésrendszerben időszak (**.**) az aktuális mappában, és a egy doubled időszak jelöli (**...** ) szülőkönyvtára az aktuális tartózkodási helyét jelöli.</span><span class="sxs-lookup"><span data-stu-id="16bf7-121">In standard notation for relative paths, a period (**.**)represents your current folder, and a doubled period (**..**) represents the parent directory of your current location.</span></span>

<span data-ttu-id="16bf7-122">Például, ha a **C:\\Windows** mappa, pont (**.**) jelöli **C:\\Windows** és időszakok duplán (**...** ) képviselő **C:**.</span><span class="sxs-lookup"><span data-stu-id="16bf7-122">For example, if you are in the **C:\\Windows** folder, a period (**.**)represents **C:\\Windows** and double periods (**..**) represent **C:**.</span></span> <span data-ttu-id="16bf7-123">Módosíthatja az aktuális helyről a C: meghajtó gyökerébe beírásával:</span><span class="sxs-lookup"><span data-stu-id="16bf7-123">You can change from your current location to the root of the C: drive by typing:</span></span>

```
PS> Set-Location -Path .. -PassThru

Path
----
C:\
```

<span data-ttu-id="16bf7-124">Ugyanezen technika működik, amelyek nem akkor a fájl rendszert tartalmazó meghajtókon, például a Windows PowerShell-meghajtók **HKLM:**.</span><span class="sxs-lookup"><span data-stu-id="16bf7-124">The same technique works on Windows PowerShell drives that are not file system drives, such as **HKLM:**.</span></span> <span data-ttu-id="16bf7-125">A HKLM is beállíthatja az helyet\\szoftverkulcs írja be a beállításjegyzékben:</span><span class="sxs-lookup"><span data-stu-id="16bf7-125">You can set your location to the HKLM\\Software key in the registry by typing:</span></span>

```
PS> Set-Location -Path HKLM:\SOFTWARE -PassThru

Path
----
HKLM:\SOFTWARE
```

<span data-ttu-id="16bf7-126">Módosíthatja a könyvtár helye a a Windows PowerShell HKLM gyökere szülőkönyvtárhoz: meghajtó relatív elérési út használatával:</span><span class="sxs-lookup"><span data-stu-id="16bf7-126">You can then change the directory location to the parent directory, which is the root of the Windows PowerShell HKLM: drive, by using a relative path:</span></span>

```
PS> Set-Location -Path .. -PassThru

Path
----
HKLM:\
```

<span data-ttu-id="16bf7-127">Írja be a Set-helyet, vagy a Set-helye (cd, chdir, sl) használja a beépített Windows PowerShell-aliasok valamelyikét.</span><span class="sxs-lookup"><span data-stu-id="16bf7-127">You can type Set-Location or use any of the built-in Windows PowerShell aliases for Set-Location (cd, chdir, sl).</span></span> <span data-ttu-id="16bf7-128">Például:</span><span class="sxs-lookup"><span data-stu-id="16bf7-128">For example:</span></span>

```powershell
cd -Path C:\Windows
```

```powershell
chdir -Path .. -PassThru
```

```powershell
sl -Path HKLM:\SOFTWARE -PassThru
```

## <a name="saving-and-recalling-recent-locations-push-location-and-pop-location"></a><span data-ttu-id="16bf7-129">Mentés és a legutóbbi helyek (a leküldéses-hely és a csatlakozási pont – hely) visszahívása</span><span class="sxs-lookup"><span data-stu-id="16bf7-129">Saving and Recalling Recent Locations (Push-Location and Pop-Location)</span></span>

<span data-ttu-id="16bf7-130">Helyek módosításakor hasznos, ahol rendelkezik-e nyomon, és térjen vissza az előző helyre lehessen.</span><span class="sxs-lookup"><span data-stu-id="16bf7-130">When changing locations, it is helpful to keep track of where you have been and to be able to return to your previous location.</span></span> <span data-ttu-id="16bf7-131">A **leküldéses helymeghatározás** a Windows PowerShell parancsmag létrehoz egy rendezett előzmények (a "verem"), ahol rendelkezik-e, és Ön visszaléphet az elérési utak előzményeit a kiegészítő használatával elérési utak  **Csatlakozási pont – hely** parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="16bf7-131">The **Push-Location** cmdlet in Windows PowerShell creates a ordered history (a "stack") of directory paths where you have been, and you can step back through the history of directory paths by using the complementary **Pop-Location** cmdlet.</span></span>

<span data-ttu-id="16bf7-132">Ha például Windows PowerShell általában az a felhasználó kezdőkönyvtárának indítja el.</span><span class="sxs-lookup"><span data-stu-id="16bf7-132">For example, Windows PowerShell typically starts in the user's home directory.</span></span>

```
PS> Get-Location

Path
----
C:\Documents and Settings\PowerUser
```

> [!NOTE]
> <span data-ttu-id="16bf7-133">A word *stack* számos programozási beállításai, többek között a .NET-keretrendszer egy különleges jelentése van.</span><span class="sxs-lookup"><span data-stu-id="16bf7-133">The word *stack* has a special meaning in many programming settings, including .NET Framework.</span></span> <span data-ttu-id="16bf7-134">Fizikai stack elemek, például a legutóbbi helyezi a veremben elem az első elem, amely a verem ki kérheti le.</span><span class="sxs-lookup"><span data-stu-id="16bf7-134">Like a physical stack of items, the last item you put onto the stack is the first item that you can pull off the stack.</span></span> <span data-ttu-id="16bf7-135">Felvesz egy elemet egy verem colloquially nevezik "leküldése" a cikk a veremben.</span><span class="sxs-lookup"><span data-stu-id="16bf7-135">Adding an item to a stack is colloquially known as "pushing" the item onto the stack.</span></span> <span data-ttu-id="16bf7-136">Beolvasás a verem ki egy elemet colloquially nevezik "popping" a cikk a verem ki.</span><span class="sxs-lookup"><span data-stu-id="16bf7-136">Pulling an item off the stack is colloquially known as "popping" the item off the stack.</span></span>

<span data-ttu-id="16bf7-137">Küldje le az aktuális helyét a veremben, és helyezze át a helyi beállításokat mappába, írja be:</span><span class="sxs-lookup"><span data-stu-id="16bf7-137">To push the current location onto the stack, and then move to the Local Settings folder, type:</span></span>

```powershell
Push-Location -Path "Local Settings"
```

<span data-ttu-id="16bf7-138">Ezután küldje le a helyi beállításokat helyét a veremben, és írja be a Temp mappa áthelyezése:</span><span class="sxs-lookup"><span data-stu-id="16bf7-138">You can then push the Local Settings location onto the stack and move to the Temp folder by typing:</span></span>

```powershell
Push-Location -Path Temp
```

<span data-ttu-id="16bf7-139">Könyvtárak módosította beírásával ellenőrizheti a **Get-Location** parancsot:</span><span class="sxs-lookup"><span data-stu-id="16bf7-139">You can verify that you changed directories by entering the **Get-Location** command:</span></span>

```
PS> Get-Location

Path
----
C:\Documents and Settings\PowerUser\Local Settings\Temp
```

<span data-ttu-id="16bf7-140">Meg lehet majd pop az utoljára felkeresett címtárba megadásával a **jelenléti pont – hely** parancsot, és ellenőrizze a módosítást, írja be a **Get-hely** parancsot:</span><span class="sxs-lookup"><span data-stu-id="16bf7-140">You can then pop back into the most recently visited directory by entering the **Pop-Location** command, and verify the change by entering the **Get-Location** command:</span></span>

```
PS> Pop-Location
PS> Get-Location

Path
----
C:\Documents and Settings\me\Local Settings
```

<span data-ttu-id="16bf7-141">Az igény szerint a **hely beállítása** parancsmaggal, megadhatja a **- PassThru** paraméter megadásakor a **jelenléti pont – hely** parancsmaggal a megadott könyvtár:</span><span class="sxs-lookup"><span data-stu-id="16bf7-141">Just as with the **Set-Location** cmdlet, you can include the **-PassThru** parameter when you enter the **Pop-Location** cmdlet to display the directory that you entered:</span></span>

```
PS> Pop-Location -PassThru

Path
----
C:\Documents and Settings\PowerUser
```

<span data-ttu-id="16bf7-142">A hely parancsmagok hálózati elérési úttal is használhatja.</span><span class="sxs-lookup"><span data-stu-id="16bf7-142">You can also use the Location cmdlets with network paths.</span></span> <span data-ttu-id="16bf7-143">Ha egy kiszolgáló FS01 nevű nyilvános-megosztásban, módosíthatja írja be a hely</span><span class="sxs-lookup"><span data-stu-id="16bf7-143">If you have a server named FS01 with an share named Public, you can change your location by typing</span></span>

```powershell
Set-Location \\FS01\Public
```

<span data-ttu-id="16bf7-144">vagy a</span><span class="sxs-lookup"><span data-stu-id="16bf7-144">or</span></span>

```powershell
Push-Location \\FS01\Public
```

<span data-ttu-id="16bf7-145">Használhatja a **leküldéses helymeghatározás** és **hely beállítása** módosítsa a helyet bármely elérhető meghajtó-parancsokat.</span><span class="sxs-lookup"><span data-stu-id="16bf7-145">You can use the **Push-Location** and **Set-Location** commands to change the location to any available drive.</span></span> <span data-ttu-id="16bf7-146">Például ha D meghajtóbetűjellel CD-ről adatokat tartalmazó helyi CD-ROM-meghajtóval rendelkezik, módosíthatja a helyet a CD-meghajtó megadásával a **hely beállítása D:** parancsot.</span><span class="sxs-lookup"><span data-stu-id="16bf7-146">For example, if you have a local CD-ROM drive with drive letter D that contains a data CD, you can change the location to the CD drive by entering the **Set-Location D:** command.</span></span>

<span data-ttu-id="16bf7-147">Ha a meghajtó üres, a következő hibaüzenet jelenik meg:</span><span class="sxs-lookup"><span data-stu-id="16bf7-147">If the drive is empty, you will get the following error message:</span></span>

```
PS> Set-Location D:
Set-Location : Cannot find path 'D:\' because it does not exist.
```

<span data-ttu-id="16bf7-148">Ha olyan parancssori felületet használ, akkor sem kényelmes fájlkezelő használata a rendelkezésre álló fizikai meghajtók vizsgálatához.</span><span class="sxs-lookup"><span data-stu-id="16bf7-148">When you are using a command-line interface, it is not convenient to use File Explorer to examine the available physical drives.</span></span> <span data-ttu-id="16bf7-149">Ezenkívül fájlkezelő lenne jeleníti meg az összes, a Windows PowerShell-meghajtók.</span><span class="sxs-lookup"><span data-stu-id="16bf7-149">Also, File Explorer would not show you the all of the Windows PowerShell drives.</span></span> <span data-ttu-id="16bf7-150">Windows PowerShell parancsokat biztosít kezelésére szolgáló Windows PowerShell-meghajtók és az előadás a Tovább gombra.</span><span class="sxs-lookup"><span data-stu-id="16bf7-150">Windows PowerShell provides a set of commands for manipulating Windows PowerShell drives, and we will talk about these next.</span></span>
