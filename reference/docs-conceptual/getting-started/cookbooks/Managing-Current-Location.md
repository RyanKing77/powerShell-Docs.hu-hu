---
ms.date: 06/05/2017
keywords: PowerShell parancsmag
title: Aktuális hely kezelése
ms.assetid: a9f9e7a7-3ea8-47d3-bbb4-6e437f6d4a4a
ms.openlocfilehash: 8d529bf4a85553b95a9cab2739016859662486f2
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
ms.locfileid: "30952222"
---
# <a name="managing-current-location"></a><span data-ttu-id="8a3a4-103">Aktuális hely kezelése</span><span class="sxs-lookup"><span data-stu-id="8a3a4-103">Managing Current Location</span></span>

<span data-ttu-id="8a3a4-104">A Fájlkezelőben mappa rendszerek navigáláskor általában rendelkeznek egy adott működő hely -, az aktuális mappa megnyitása.</span><span class="sxs-lookup"><span data-stu-id="8a3a4-104">When navigating folder systems in File Explorer, you usually have a specific working location - namely, the current open folder.</span></span> <span data-ttu-id="8a3a4-105">Az aktuális mappában elemek kattintással könnyedén kezelhetők.</span><span class="sxs-lookup"><span data-stu-id="8a3a4-105">Items in the current folder can be manipulated easily by clicking them.</span></span> <span data-ttu-id="8a3a4-106">A parancssori felületen például a Cmd.exe amikor egy adott fájl ugyanabban a mappában van-e hozzáférése által viszonylag rövid nevének megadása helyett adja meg a fájl teljes elérési útja kell.</span><span class="sxs-lookup"><span data-stu-id="8a3a4-106">For command-line interfaces such as Cmd.exe, when you are in the same folder as a particular file, you can access it by specifying a relatively short name, rather than needing to specify the entire path to the file.</span></span> <span data-ttu-id="8a3a4-107">Az aktuális könyvtár neve a munkakönyvtárat.</span><span class="sxs-lookup"><span data-stu-id="8a3a4-107">The current directory is called the working directory.</span></span>

<span data-ttu-id="8a3a4-108">A Windows PowerShell használja a főnév **hely** lehet hivatkozni a munkakönyvtár családba tartozó-parancsmagok segítségével vizsgálja meg és kezelheti a felhasználó tartózkodási helyét, és.</span><span class="sxs-lookup"><span data-stu-id="8a3a4-108">Windows PowerShell uses the noun **Location** to refer to the working directory, and implements a family of cmdlets to examine and manipulate your location.</span></span>

### <a name="getting-your-current-location-get-location"></a><span data-ttu-id="8a3a4-109">A jelenlegi hely (Get-hely) beolvasása</span><span class="sxs-lookup"><span data-stu-id="8a3a4-109">Getting Your Current Location (Get-Location)</span></span>

<span data-ttu-id="8a3a4-110">Határozza meg az elérési útját az aktuális könyvtár helyét, írja be a következőt a **Get-hely** parancs:</span><span class="sxs-lookup"><span data-stu-id="8a3a4-110">To determine the path of your current directory location, enter the **Get-Location** command:</span></span>

```
PS> Get-Location
Path
----
C:\Documents and Settings\PowerUser
```

> [!NOTE]
> <span data-ttu-id="8a3a4-111">A Get-hely parancsmag hasonlít a **pwd** a rendszerhéjakba parancsot.</span><span class="sxs-lookup"><span data-stu-id="8a3a4-111">The Get-Location cmdlet is similar to the **pwd** command in the BASH shell.</span></span> <span data-ttu-id="8a3a4-112">A hely beállítása parancsmag hasonlít a **cd** Cmd.exe parancsot.</span><span class="sxs-lookup"><span data-stu-id="8a3a4-112">The Set-Location cmdlet is similar to the **cd** command in Cmd.exe.</span></span>

### <a name="setting-your-current-location-set-location"></a><span data-ttu-id="8a3a4-113">A jelenlegi hely (Set-helyének) beállítása</span><span class="sxs-lookup"><span data-stu-id="8a3a4-113">Setting Your Current Location (Set-Location)</span></span>

<span data-ttu-id="8a3a4-114">A **Get-hely** parancs használatos a **hely beállítása** parancsot.</span><span class="sxs-lookup"><span data-stu-id="8a3a4-114">The **Get-Location** command is used with the **Set-Location** command.</span></span> <span data-ttu-id="8a3a4-115">A **hely beállítása** parancs lehetővé teszi, hogy adja meg az aktuális könyvtár helyet.</span><span class="sxs-lookup"><span data-stu-id="8a3a4-115">The **Set-Location** command allows you to specify your current directory location.</span></span>

```powershell
Set-Location -Path C:\Windows
```

<span data-ttu-id="8a3a4-116">Miután megadta a parancs, megfigyelheti, hogy nem jelenik meg a hatását, hogy a parancs minden közvetlen visszajelzést.</span><span class="sxs-lookup"><span data-stu-id="8a3a4-116">After you enter the command, you will notice that you do not receive any direct feedback about the effect of the command.</span></span> <span data-ttu-id="8a3a4-117">Egy műveletet a legtöbb Windows PowerShell-parancsok kevéssé vagy egyáltalán ne kimeneti eredményez, mivel a kimenet nem mindig hasznos.</span><span class="sxs-lookup"><span data-stu-id="8a3a4-117">Most Windows PowerShell commands that perform an action produce little or no output because the output is not always useful.</span></span> <span data-ttu-id="8a3a4-118">Győződjön meg arról, hogy a sikeres könyvtárváltás történt-e, amikor megadja a a **hely beállítása** paranccsal, tartalmazza a **- PassThru** paraméter megadásakor a **Set-hely**parancs:</span><span class="sxs-lookup"><span data-stu-id="8a3a4-118">To verify that a successful directory change has occurred when you enter the **Set-Location** command, include the **-PassThru** parameter when you enter the **Set-Location** command:</span></span>

```
PS> Set-Location -Path C:\Windows -PassThru

Path
----
C:\WINDOWS
```

<span data-ttu-id="8a3a4-119">A **- PassThru** paraméter használható a Windows PowerShell számos Set parancs tevékenység információt nyújt az eredmény abban az esetben, amelyben nincs alapértelmezett kimenet.</span><span class="sxs-lookup"><span data-stu-id="8a3a4-119">The **-PassThru** parameter can be used with many Set commands in Windows PowerShell to return information about the result in cases in which there is no default output.</span></span>

<span data-ttu-id="8a3a4-120">Meg elérési utat is megadhat tartózkodási helyéhez viszonyított azonos módon, akkor volna a UNIX és a Windows legtöbb parancs ismertetése.</span><span class="sxs-lookup"><span data-stu-id="8a3a4-120">You can specify paths relative to your current location in the same way as you would in most UNIX and Windows command shells.</span></span> <span data-ttu-id="8a3a4-121">Standard jelöléssel relatív elérési út esetén időszak (**.**) az aktuális mappát, és egy doubled időszakot jelöli (**...** ) az aktuális hely-jének szülőkönyvtárában jelöli.</span><span class="sxs-lookup"><span data-stu-id="8a3a4-121">In standard notation for relative paths, a period (**.**)represents your current folder, and a doubled period (**..**) represents the parent directory of your current location.</span></span>

<span data-ttu-id="8a3a4-122">Ha például a **C:\\Windows** , az adott időszakban (**.**) jelöli **C:\\Windows** és időszakok duplán (**...** ) képviselő **C:**.</span><span class="sxs-lookup"><span data-stu-id="8a3a4-122">For example, if you are in the **C:\\Windows** folder, a period (**.**)represents **C:\\Windows** and double periods (**..**) represent **C:**.</span></span> <span data-ttu-id="8a3a4-123">Módosíthatja az aktuális helyről a C: meghajtó gyökerébe beírásával:</span><span class="sxs-lookup"><span data-stu-id="8a3a4-123">You can change from your current location to the root of the C: drive by typing:</span></span>

```
PS> Set-Location -Path .. -PassThru

Path
----
C:\
```

<span data-ttu-id="8a3a4-124">Ugyanaz a technika működik, amelyek nincsenek fájl rendszert tartalmazó meghajtókon, például a Windows PowerShell meghajtókon **HKLM:**.</span><span class="sxs-lookup"><span data-stu-id="8a3a4-124">The same technique works on Windows PowerShell drives that are not file system drives, such as **HKLM:**.</span></span> <span data-ttu-id="8a3a4-125">A felhasználó tartózkodási helyét is beállíthatja a HKLM\\szoftverkulcs írja be a beállításjegyzékben:</span><span class="sxs-lookup"><span data-stu-id="8a3a4-125">You can set your location to the HKLM\\Software key in the registry by typing:</span></span>

```
PS> Set-Location -Path HKLM:\SOFTWARE -PassThru

Path
----
HKLM:\SOFTWARE
```

<span data-ttu-id="8a3a4-126">Módosíthatja a könyvtár helyét a szülőkönyvtárat, amely a Windows PowerShell HKLM gyökere: meghajtó relatív elérési úttal:</span><span class="sxs-lookup"><span data-stu-id="8a3a4-126">You can then change the directory location to the parent directory, which is the root of the Windows PowerShell HKLM: drive, by using a relative path:</span></span>

```
PS> Set-Location -Path .. -PassThru

Path
----
HKLM:\
```

<span data-ttu-id="8a3a4-127">Írja be a hely beállítása, vagy használja a beépített Windows PowerShell-aliasok valamelyikét a Set-helyéhez (cd, chdir, l).</span><span class="sxs-lookup"><span data-stu-id="8a3a4-127">You can type Set-Location or use any of the built-in Windows PowerShell aliases for Set-Location (cd, chdir, sl).</span></span> <span data-ttu-id="8a3a4-128">Például:</span><span class="sxs-lookup"><span data-stu-id="8a3a4-128">For example:</span></span>

```powershell
cd -Path C:\Windows
```

```powershell
chdir -Path .. -PassThru
```

```powershell
sl -Path HKLM:\SOFTWARE -PassThru
```

### <a name="saving-and-recalling-recent-locations-push-location-and-pop-location"></a><span data-ttu-id="8a3a4-129">Mentés és a legutóbbi helyek (leküldéses és Pop-) tárolóról</span><span class="sxs-lookup"><span data-stu-id="8a3a4-129">Saving and Recalling Recent Locations (Push-Location and Pop-Location)</span></span>

<span data-ttu-id="8a3a4-130">Helyek módosítása, esetén hasznos, ha rendelkezik-e nyomon, és térjen vissza az előző helyre tudja.</span><span class="sxs-lookup"><span data-stu-id="8a3a4-130">When changing locations, it is helpful to keep track of where you have been and to be able to return to your previous location.</span></span> <span data-ttu-id="8a3a4-131">A **leküldéses-hely** a Windows PowerShell parancsmag hoz létre a könyvtár elérési utakon található rendelkezik-e, vehetjük vissza elérési útjainak előzményeinek a kiegészítő használatával rendezett előzményeit (a "verem")  **POP-hely** parancsmag.</span><span class="sxs-lookup"><span data-stu-id="8a3a4-131">The **Push-Location** cmdlet in Windows PowerShell creates a ordered history (a "stack") of directory paths where you have been, and you can step back through the history of directory paths by using the complementary **Pop-Location** cmdlet.</span></span>

<span data-ttu-id="8a3a4-132">Például a Windows PowerShell általában indítja el a felhasználó saját könyvtárához.</span><span class="sxs-lookup"><span data-stu-id="8a3a4-132">For example, Windows PowerShell typically starts in the user's home directory.</span></span>

```
PS> Get-Location

Path
----
C:\Documents and Settings\PowerUser
```

> [!NOTE]
> <span data-ttu-id="8a3a4-133">A word *verem* rendelkezik-e speciális jelentéssel számos programozási beállításai, beleértve a .NET-keretrendszer.</span><span class="sxs-lookup"><span data-stu-id="8a3a4-133">The word *stack* has a special meaning in many programming settings, including .NET Framework.</span></span> <span data-ttu-id="8a3a4-134">Fizikai verem elemek, például az utolsó elem a veremben helyezünk elem az első, amely akkor is lehívása a verem.</span><span class="sxs-lookup"><span data-stu-id="8a3a4-134">Like a physical stack of items, the last item you put onto the stack is the first item that you can pull off the stack.</span></span> <span data-ttu-id="8a3a4-135">Egy elem felvétele a verem colloquially nevezik "küldését" a cikk a veremben.</span><span class="sxs-lookup"><span data-stu-id="8a3a4-135">Adding an item to a stack is colloquially known as "pushing" the item onto the stack.</span></span> <span data-ttu-id="8a3a4-136">Húzza ki a verem elem colloquially nevezik "popping" a cikk a verem ki.</span><span class="sxs-lookup"><span data-stu-id="8a3a4-136">Pulling an item off the stack is colloquially known as "popping" the item off the stack.</span></span>

<span data-ttu-id="8a3a4-137">Az aktuális helyen, a veremben leküldéses, és helyezze át a helyi beállításokat mappába, írja be:</span><span class="sxs-lookup"><span data-stu-id="8a3a4-137">To push the current location onto the stack, and then move to the Local Settings folder, type:</span></span>

```powershell
Push-Location -Path "Local Settings"
```

<span data-ttu-id="8a3a4-138">Majd tolható ki a helyi beállításokat helyét a veremben, és írja be az ideiglenes mappa áthelyezése és:</span><span class="sxs-lookup"><span data-stu-id="8a3a4-138">You can then push the Local Settings location onto the stack and and move to the Temp folder by typing:</span></span>

```powershell
Push-Location -Path Temp
```

<span data-ttu-id="8a3a4-139">Könyvtárak módosította beírásával ellenőrizheti a **Get-hely** parancs:</span><span class="sxs-lookup"><span data-stu-id="8a3a4-139">You can verify that you changed directories by entering the **Get-Location** command:</span></span>

```
PS> Get-Location

Path
----
C:\Documents and Settings\PowerUser\Local Settings\Temp
```

<span data-ttu-id="8a3a4-140">Akkor is majd állítsa vissza a nemrég megtekintett könyvtárba megadásával a **Pop-hely** parancsot, és ellenőrzéséhez írja be a **Get-hely** parancs:</span><span class="sxs-lookup"><span data-stu-id="8a3a4-140">You can then pop back into the most recently visited directory by entering the **Pop-Location** command, and verify the change by entering the **Get-Location** command:</span></span>

```
PS> Pop-Location
PS> Get-Location

Path
----
C:\Documents and Settings\me\Local Settings
```

<span data-ttu-id="8a3a4-141">Együtt, csak a **hely beállítása** parancsmaggal, megadhatja a **- PassThru** paraméter megadásakor a **Pop-hely** parancsmag használatával jelenítse meg a megadott könyvtár:</span><span class="sxs-lookup"><span data-stu-id="8a3a4-141">Just as with the **Set-Location** cmdlet, you can include the **-PassThru** parameter when you enter the **Pop-Location** cmdlet to display the directory that you entered:</span></span>

```
PS> Pop-Location -PassThru

Path
----
C:\Documents and Settings\PowerUser
```

<span data-ttu-id="8a3a4-142">A hálózati elérési út is használhatja a hely parancsmagokat.</span><span class="sxs-lookup"><span data-stu-id="8a3a4-142">You can also use the Location cmdlets with network paths.</span></span> <span data-ttu-id="8a3a4-143">Ha egy kiszolgáló egy nyilvános nevű fájlmegosztás FS01 nevű, módosíthatja írja be a felhasználó tartózkodási helyét</span><span class="sxs-lookup"><span data-stu-id="8a3a4-143">If you have a server named FS01 with an share named Public, you can change your location by typing</span></span>

```powershell
Set-Location \\FS01\Public
```

<span data-ttu-id="8a3a4-144">vagy a</span><span class="sxs-lookup"><span data-stu-id="8a3a4-144">or</span></span>

```powershell
Push-Location \\FS01\Public
```

<span data-ttu-id="8a3a4-145">Használhatja a **leküldéses-hely** és **hely beállítása** parancsok helyének módosításához az összes rendelkezésre álló meghajtóra.</span><span class="sxs-lookup"><span data-stu-id="8a3a4-145">You can use the **Push-Location** and **Set-Location** commands to change the location to any available drive.</span></span> <span data-ttu-id="8a3a4-146">Például ha D meghajtóbetűjellel adatok CD-ről tartalmazó helyi CD-ROM-meghajtóval rendelkezik, módosíthatja a hely a CD-meghajtót írja be a **hely beállítása D:** parancsot.</span><span class="sxs-lookup"><span data-stu-id="8a3a4-146">For example, if you have a local CD-ROM drive with drive letter D that contains a data CD, you can change the location to the CD drive by entering the **Set-Location D:** command.</span></span>

<span data-ttu-id="8a3a4-147">Ha a meghajtó üres, a következő hibaüzenet jelenik meg:</span><span class="sxs-lookup"><span data-stu-id="8a3a4-147">If the drive is empty, you will get the following error message:</span></span>

```
PS> Set-Location D:
Set-Location : Cannot find path 'D:\' because it does not exist.
```

<span data-ttu-id="8a3a4-148">Amikor egy parancssori felületet használ, célszerű nem a Fájlkezelőben a rendelkezésre álló fizikai meghajtók ellenőrzéséhez.</span><span class="sxs-lookup"><span data-stu-id="8a3a4-148">When you are using a command-line interface, it is not convenient to use File Explorer to examine the available physical drives.</span></span> <span data-ttu-id="8a3a4-149">Emellett a Fájlkezelőben volna jeleníti meg az összes, a Windows PowerShell-meghajtó.</span><span class="sxs-lookup"><span data-stu-id="8a3a4-149">Also, File Explorer would not show you the all of the Windows PowerShell drives.</span></span> <span data-ttu-id="8a3a4-150">Windows PowerShell parancsokat biztosít kezelésére szolgáló Windows PowerShell-meghajtókat, valamint az előadás a Tovább gombra.</span><span class="sxs-lookup"><span data-stu-id="8a3a4-150">Windows PowerShell provides a set of commands for manipulating Windows PowerShell drives, and we will talk about these next.</span></span>