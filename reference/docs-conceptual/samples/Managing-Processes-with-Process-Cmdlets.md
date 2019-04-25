---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: Folyamatok kezelése folyamatparancsmagokkal
ms.assetid: 5038f612-d149-4698-8bbb-999986959e31
ms.openlocfilehash: 741a3464bce6284c4933384398c4e9ddcca2572c
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62058709"
---
# <a name="managing-processes-with-process-cmdlets"></a><span data-ttu-id="6ac4e-103">Folyamatok kezelése folyamatparancsmagokkal</span><span class="sxs-lookup"><span data-stu-id="6ac4e-103">Managing Processes with Process Cmdlets</span></span>

<span data-ttu-id="6ac4e-104">A folyamat parancsmagok a Windows PowerShell segítségével a Windows PowerShellben a helyi és távoli folyamatok kezeléséhez.</span><span class="sxs-lookup"><span data-stu-id="6ac4e-104">You can use the Process cmdlets in Windows PowerShell to manage local and remote processes in Windows PowerShell.</span></span>

## <a name="getting-processes-get-process"></a><span data-ttu-id="6ac4e-105">Folyamatok lekérdezése (Get-Process)</span><span class="sxs-lookup"><span data-stu-id="6ac4e-105">Getting Processes (Get-Process)</span></span>

<span data-ttu-id="6ac4e-106">A helyi számítógépen futó folyamatok lekéréséhez futtassa a **Get-Process** nélkül.</span><span class="sxs-lookup"><span data-stu-id="6ac4e-106">To get the processes running on the local computer, run a **Get-Process** with no parameters.</span></span>

<span data-ttu-id="6ac4e-107">Bizonyos folyamatok kaphat a folyamat nevét vagy a folyamat azonosítók megadásával.</span><span class="sxs-lookup"><span data-stu-id="6ac4e-107">You can get particular processes by specifying their process names or process IDs.</span></span> <span data-ttu-id="6ac4e-108">Az alábbi parancs lekéri az üresjárati folyamat:</span><span class="sxs-lookup"><span data-stu-id="6ac4e-108">The following command gets the Idle process:</span></span>

```
PS> Get-Process -id 0

Handles  NPM(K)    PM(K)      WS(K) VM(M)   CPU(s)     Id ProcessName
-------  ------    -----      ----- -----   ------     -- -----------
      0       0        0         16     0               0 Idle
```

<span data-ttu-id="6ac4e-109">Bár előfordulhat, hogy parancsmagokat nem adnak vissza adatokat bizonyos helyzetekben, amikor megad egy folyamat, a folyamatazonosító **Get-Process** hibát generál, ha úgy találja, hogy nincs egyezés, mert szokásos célja beolvasni egy ismert futó folyamat.</span><span class="sxs-lookup"><span data-stu-id="6ac4e-109">Although it is normal for cmdlets to return no data in some situations, when you specify a process by its ProcessId, **Get-Process** generates an error if it finds no matches, because the usual intent is to retrieve a known running process.</span></span> <span data-ttu-id="6ac4e-110">Ha van ilyen azonosítójú folyamatot sem, akkor valószínű, hogy az azonosító helytelen, vagy a folyamat a lényeges már kilépett:</span><span class="sxs-lookup"><span data-stu-id="6ac4e-110">If there is no process with that Id, it is likely that the Id is incorrect or that the process of interest has already exited:</span></span>

```
PS> Get-Process -Id 99

Get-Process : No process with process ID 99 was found.
At line:1 char:12
+ Get-Process  <<<< -Id 99
```

<span data-ttu-id="6ac4e-111">A Name paraméter, a Get-Process-parancsmag segítségével adja meg a folyamat neve alapján a folyamat egy részét.</span><span class="sxs-lookup"><span data-stu-id="6ac4e-111">You can use the Name parameter of the Get-Process cmdlet to specify a subset of processes based on the process name.</span></span> <span data-ttu-id="6ac4e-112">A Name paraméter is igénybe vehet a neveket vesszővel elválasztott listáját, és támogatja a helyettesítő karakterekkel, így beírhatja a név minták.</span><span class="sxs-lookup"><span data-stu-id="6ac4e-112">The Name parameter can take multiple names in a comma-separated list and it supports the use of wildcards, so you can type name patterns.</span></span>

<span data-ttu-id="6ac4e-113">Például az alábbi parancs lekéri a "például" kezdődő folyamat</span><span class="sxs-lookup"><span data-stu-id="6ac4e-113">For example, the following command gets process whose names begin with "ex."</span></span>

```
PS> Get-Process -Name ex*

Handles  NPM(K)    PM(K)      WS(K) VM(M)   CPU(s)     Id ProcessName
-------  ------    -----      ----- -----   ------     -- -----------
    234       7     5572      12484   134     2.98   1684 EXCEL
    555      15    34500      12384   134   105.25    728 explorer
```

<span data-ttu-id="6ac4e-114">Mivel a Windows PowerShell-folyamatok alapját, a .NET System.Diagnostics.Process osztály követi a egyezmények System.Diagnostics.Process által használt néhány.</span><span class="sxs-lookup"><span data-stu-id="6ac4e-114">Because the .NET System.Diagnostics.Process class is the foundation for Windows PowerShell processes, it follows some of the conventions used by System.Diagnostics.Process.</span></span> <span data-ttu-id="6ac4e-115">Ezen egyezmények egyike, hogy a folyamat nevét, egy végrehajtható fájl soha nem tartalmazza a ".exe" végén található a végrehajtható fájl nevét.</span><span class="sxs-lookup"><span data-stu-id="6ac4e-115">One of those conventions is that the process name for an executable never includes the ".exe" at the end of the executable name.</span></span>

<span data-ttu-id="6ac4e-116">**Get-Process** a Name paraméter több értéket is fogad.</span><span class="sxs-lookup"><span data-stu-id="6ac4e-116">**Get-Process** also accepts multiple values for the Name parameter.</span></span>

```
PS> Get-Process -Name exp*,power*

Handles  NPM(K)    PM(K)      WS(K) VM(M)   CPU(s)     Id ProcessName
-------  ------    -----      ----- -----   ------     -- -----------
    540      15    35172      48148   141    88.44    408 explorer
    605       9    30668      29800   155     7.11   3052 powershell
```

<span data-ttu-id="6ac4e-117">A Get-Process-ComputerName paraméter használatával a távoli számítógépeken lévő folyamatok beolvasása.</span><span class="sxs-lookup"><span data-stu-id="6ac4e-117">You can use the ComputerName parameter of Get-Process to get processes on remote computers.</span></span> <span data-ttu-id="6ac4e-118">Például a következő parancs lekérdezi a helyi számítógépen (a "localhost" által jelölt) a PowerShell-folyamatokat, és két távoli számítógépen.</span><span class="sxs-lookup"><span data-stu-id="6ac4e-118">For example, the following command gets the PowerShell processes on the local computer (represented by "localhost") and on two remote computers.</span></span>

```
PS> Get-Process -Name PowerShell -ComputerName localhost, Server01, Server02

Handles  NPM(K)    PM(K)      WS(K) VM(M)   CPU(s)     Id ProcessName
-------  ------    -----      ----- -----   ------     -- -----------
    258       8    29772      38636   130            3700 powershell
    398      24    75988      76800   572            5816 powershell
    605       9    30668      29800   155     7.11   3052 powershell
```

<span data-ttu-id="6ac4e-119">A számítógép nevében a rendszer nem egyértelmű, a kijelzett, de a számítógépnév tulajdonság, amely visszaadja a Get-Process folyamat objektumot tárolódnak.</span><span class="sxs-lookup"><span data-stu-id="6ac4e-119">The computer names are not evident in this display, but they are stored in the MachineName property of the process objects that Get-Process returns.</span></span> <span data-ttu-id="6ac4e-120">A következő parancsot a Format-Table-parancsmag használatával jeleníti meg, a Folyamatazonosítója, ProcessName és MachineName (ComputerName) a folyamat objektumok tulajdonságait.</span><span class="sxs-lookup"><span data-stu-id="6ac4e-120">The following command uses the Format-Table cmdlet to display the process ID, ProcessName and MachineName (ComputerName) properties of the process objects.</span></span>

```
PS> Get-Process -Name PowerShell -ComputerName localhost, Server01, Server01 | Format-Table -Property ID, ProcessName, MachineName

  Id ProcessName MachineName
  -- ----------- -----------
3700 powershell  Server01
3052 powershell  Server02
5816 powershell  localhost
```

<span data-ttu-id="6ac4e-121">Összetettebb hozzáadja a számítógépnév tulajdonság a standard szintű Get-Process megjelenítése.</span><span class="sxs-lookup"><span data-stu-id="6ac4e-121">This more complex command adds the MachineName property to the standard Get-Process display.</span></span>

```
PS> Get-Process powershell -ComputerName localhost, Server01, Server02 |
    Format-Table -Property Handles,
        @{Label="NPM(K)";Expression={[int]($_.NPM/1024)}},
        @{Label="PM(K)";Expression={[int]($_.PM/1024)}},
        @{Label="WS(K)";Expression={[int]($_.WS/1024)}},
        @{Label="VM(M)";Expression={[int]($_.VM/1MB)}},
        @{Label="CPU(s)";Expression={if ($_.CPU -ne $()){$_.CPU.ToString("N")}}},
        Id, ProcessName, MachineName -auto

Handles  NPM(K)  PM(K) WS(K) VM(M) CPU(s)  Id ProcessName  MachineName
-------  ------  ----- ----- ----- ------  -- -----------  -----------
    258       8  29772 38636   130         3700 powershell Server01
    398      24  75988 76800   572         5816 powershell localhost
    605       9  30668 29800   155 7.11    3052 powershell Server02
```

## <a name="stopping-processes-stop-process"></a><span data-ttu-id="6ac4e-122">Folyamatok (Stop-Process) leállítása</span><span class="sxs-lookup"><span data-stu-id="6ac4e-122">Stopping Processes (Stop-Process)</span></span>

<span data-ttu-id="6ac4e-123">Windows PowerShell a folyamatok listázása, de mi a helyzet a folyamat leállítása rugalmasságot biztosít?</span><span class="sxs-lookup"><span data-stu-id="6ac4e-123">Windows PowerShell gives you flexibility for listing processes, but what about stopping a process?</span></span>

<span data-ttu-id="6ac4e-124">A **Stop-Process** parancsmagnál egy név vagy azonosító megadása egy folyamat meg szeretné szüntetni.</span><span class="sxs-lookup"><span data-stu-id="6ac4e-124">The **Stop-Process** cmdlet takes a Name or Id to specify a process you want to stop.</span></span> <span data-ttu-id="6ac4e-125">Állítsa le a folyamat képességét az engedélyektől függ.</span><span class="sxs-lookup"><span data-stu-id="6ac4e-125">Your ability to stop processes depends on your permissions.</span></span> <span data-ttu-id="6ac4e-126">Bizonyos folyamatok nem lehet leállítani.</span><span class="sxs-lookup"><span data-stu-id="6ac4e-126">Some processes cannot be stopped.</span></span> <span data-ttu-id="6ac4e-127">Ha például meg az üresjárati folyamat leállítása, ha hibaüzenetet kap:</span><span class="sxs-lookup"><span data-stu-id="6ac4e-127">For example, if you try to stop the idle process, you get an error:</span></span>

```
PS> Stop-Process -Name Idle
Stop-Process : Process 'Idle (0)' cannot be stopped due to the following error:
 Access is denied
At line:1 char:13
+ Stop-Process  <<<< -Name Idle
```

<span data-ttu-id="6ac4e-128">A kérdés is kényszeríthető a **megerősítése** paraméter.</span><span class="sxs-lookup"><span data-stu-id="6ac4e-128">You can also force prompting with the **Confirm** parameter.</span></span> <span data-ttu-id="6ac4e-129">Ez a paraméter különösen hasznos használatakor egy helyettesítő karaktert tartalmazó megadásakor a folyamat nevét, mert előfordulhat, hogy véletlenül felel meg bizonyos folyamatok nem szeretné, hogy állítsa le:</span><span class="sxs-lookup"><span data-stu-id="6ac4e-129">This parameter is particularly useful if you use a wildcard when specifying the process name, because you may accidentally match some processes you do not want to stop:</span></span>

```
PS> Stop-Process -Name t*,e* -Confirm
Confirm
Are you sure you want to perform this action?
Performing operation "Stop-Process" on Target "explorer (408)".
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help
(default is "Y"):n
Confirm
Are you sure you want to perform this action?
Performing operation "Stop-Process" on Target "taskmgr (4072)".
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help
(default is "Y"):n
```

<span data-ttu-id="6ac4e-130">Összetett folyamat manipuláció lehetőség néhány, a parancsmagok szűrés objektum használatával.</span><span class="sxs-lookup"><span data-stu-id="6ac4e-130">Complex process manipulation is possible by using some of the object filtering cmdlets.</span></span> <span data-ttu-id="6ac4e-131">Egy folyamat objektumot válaszol tulajdonsága igaz, amikor nem válaszol, mivel az összes nem válaszoló alkalmazásokat az alábbi paranccsal állíthatja le:</span><span class="sxs-lookup"><span data-stu-id="6ac4e-131">Because a Process object has a Responding property that is true when it is no longer responding, you can stop all nonresponsive applications with the following command:</span></span>

```powershell
Get-Process | Where-Object -FilterScript {$_.Responding -eq $false} | Stop-Process
```

<span data-ttu-id="6ac4e-132">Más helyzetekben használhatja ugyanazt a megközelítést.</span><span class="sxs-lookup"><span data-stu-id="6ac4e-132">You can use the same approach in other situations.</span></span> <span data-ttu-id="6ac4e-133">Tegyük fel például, hogy egy másodlagos értesítési terület alkalmazás automatikusan fut egy másik alkalmazás indításakor.</span><span class="sxs-lookup"><span data-stu-id="6ac4e-133">For example, suppose a secondary notification area application automatically runs when users start another application.</span></span> <span data-ttu-id="6ac4e-134">Előfordulhat, hogy ez nem működik megfelelően a Terminálszolgáltatások munkamenetek során, de továbbra is szeretné a fizikai számítógép-konzolt futtató munkamenetet tárolja.</span><span class="sxs-lookup"><span data-stu-id="6ac4e-134">You may find that this does not work correctly in Terminal Services sessions, but you still want to keep it in sessions that run on the physical computer console.</span></span> <span data-ttu-id="6ac4e-135">Mindig csatlakozik a fizikai számítógép, asztali munkamenetek rendelkezik egy munkamenet-azonosító értéke 0, így a folyamat összes példánya vannak más munkamenetek használatával állítsa le **Where-Object** és a folyamat **SessionId** :</span><span class="sxs-lookup"><span data-stu-id="6ac4e-135">Sessions connected to the physical computer desktop always have a session ID of 0, so you can stop all instances of the process that are in other sessions by using **Where-Object** and the process, **SessionId**:</span></span>

```powershell
Get-Process -Name BadApp | Where-Object -FilterScript {$_.SessionId -neq 0} | Stop-Process
```

<span data-ttu-id="6ac4e-136">A Stop-Process parancsmaghoz nem tartozik a ComputerName paramétert.</span><span class="sxs-lookup"><span data-stu-id="6ac4e-136">The Stop-Process cmdlet does not have a ComputerName parameter.</span></span> <span data-ttu-id="6ac4e-137">Ezért egy leállítási folyamatot parancs futtatása egy távoli számítógépen szeretné használni az Invoke-Command parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="6ac4e-137">Therefore, to run a stop process command on a remote computer, you need to use the Invoke-Command cmdlet.</span></span> <span data-ttu-id="6ac4e-138">Írja be például a kiszolgalo01 távoli számítógépen a PowerShell-folyamat leállításához:</span><span class="sxs-lookup"><span data-stu-id="6ac4e-138">For example, to stop the PowerShell process on the Server01 remote computer, type:</span></span>

```powershell
Invoke-Command -ComputerName Server01 {Stop-Process Powershell}
```

## <a name="stopping-all-other-windows-powershell-sessions"></a><span data-ttu-id="6ac4e-139">Minden más Windows PowerShell-munkamenetekben leállítása</span><span class="sxs-lookup"><span data-stu-id="6ac4e-139">Stopping All Other Windows PowerShell Sessions</span></span>

<span data-ttu-id="6ac4e-140">Időnként hasznos lehet a tudnak állni eltérő az aktuális munkamenet összes futó Windows PowerShell-munkameneteket.</span><span class="sxs-lookup"><span data-stu-id="6ac4e-140">It may occasionally be useful to be able to stop all running Windows PowerShell sessions other than the current session.</span></span> <span data-ttu-id="6ac4e-141">Ha egy munkamenetben túl sok erőforrást használ, vagy nem érhető el (azt is futnia távolról, vagy egy másik asztal munkamenetben), nem lehet közvetlenül állítsa le.</span><span class="sxs-lookup"><span data-stu-id="6ac4e-141">If a session is using too many resources or is inaccessible (it may be running remotely or in another desktop session), you may not be able to directly stop it.</span></span> <span data-ttu-id="6ac4e-142">Ha megpróbálja leállítani az összes futó munkameneteket, azonban a jelenlegi munkamenet megszüntethető helyette.</span><span class="sxs-lookup"><span data-stu-id="6ac4e-142">If you try to stop all running sessions, however, the current session may be terminated instead.</span></span>

<span data-ttu-id="6ac4e-143">Minden Windows PowerShell-munkamenetet, egy környezeti változót, amely tartalmazza a Windows PowerShell-folyamat azonosítója PID.</span><span class="sxs-lookup"><span data-stu-id="6ac4e-143">Each Windows PowerShell session has an environment variable PID that contains the Id of the Windows PowerShell process.</span></span> <span data-ttu-id="6ac4e-144">Ellenőrizze a $PID mindegyik munkamenet azonosítója alapján, és csak Windows PowerShell-munkamenetekben, amelyek egy másik azonosítót. megszüntetheti A következő folyamat parancs azért teszi ezt, és elbocsátott munkamenetek listáját adja vissza (a használata miatt a **PassThru** paraméter):</span><span class="sxs-lookup"><span data-stu-id="6ac4e-144">You can check the $PID against the Id of each session and terminate only Windows PowerShell sessions that have a different Id. The following pipeline command does this and returns the list of terminated sessions (because of the use of the **PassThru** parameter):</span></span>

```
PS> Get-Process -Name powershell | Where-Object -FilterScript {$_.Id -ne $PID} | Stop-Process -PassThru

Handles  NPM(K)    PM(K)      WS(K) VM(M)   CPU(s)     Id ProcessName
-------  ------    -----      ----- -----   ------     -- -----------
    334       9    23348      29136   143     1.03    388 powershell
    304       9    23152      29040   143     1.03    632 powershell
    302       9    20916      26804   143     1.03   1116 powershell
    335       9    25656      31412   143     1.09   3452 powershell
    303       9    23156      29044   143     1.05   3608 powershell
    287       9    21044      26928   143     1.02   3672 powershell
```

## <a name="starting-debugging-and-waiting-for-processes"></a><span data-ttu-id="6ac4e-145">Indítása, a Hibakeresés és a folyamatok Várakozás</span><span class="sxs-lookup"><span data-stu-id="6ac4e-145">Starting, Debugging, and Waiting for Processes</span></span>

<span data-ttu-id="6ac4e-146">Windows PowerShell-parancsmagokkal indítása (vagy újraindítása), is tartalmaz, hibakeresési egy folyamatot, és várja meg a folyamat befejeződését, mielőtt a következő parancs futtatásával.</span><span class="sxs-lookup"><span data-stu-id="6ac4e-146">Windows PowerShell also comes with cmdlets to start (or restart), debug a process, and wait for a process to complete before running a command.</span></span> <span data-ttu-id="6ac4e-147">Ezekkel a parancsmagokkal kapcsolatos információkért tekintse meg az egyes parancsmagok parancsmag Súgó-témakör.</span><span class="sxs-lookup"><span data-stu-id="6ac4e-147">For information about these cmdlets, see the cmdlet help topic for each cmdlet.</span></span>

## <a name="see-also"></a><span data-ttu-id="6ac4e-148">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="6ac4e-148">See Also</span></span>

- <span data-ttu-id="6ac4e-149">[Get-Process [m2]](https://technet.microsoft.com/en-us/library/27a05dbd-4b69-48a3-8d55-b295f6225f15)</span><span class="sxs-lookup"><span data-stu-id="6ac4e-149">[Get-Process [m2]](https://technet.microsoft.com/en-us/library/27a05dbd-4b69-48a3-8d55-b295f6225f15)</span></span>
- <span data-ttu-id="6ac4e-150">[Stop-Process [m2]](https://technet.microsoft.com/en-us/library/12454238-9881-457a-bde4-fb6cd124deec)</span><span class="sxs-lookup"><span data-stu-id="6ac4e-150">[Stop-Process [m2]](https://technet.microsoft.com/en-us/library/12454238-9881-457a-bde4-fb6cd124deec)</span></span>
- [<span data-ttu-id="6ac4e-151">Start-Process</span><span class="sxs-lookup"><span data-stu-id="6ac4e-151">Start-Process</span></span>](https://technet.microsoft.com/en-us/library/41a7e43c-9bb3-4dc2-8b0c-f6c32962e72c)
- [<span data-ttu-id="6ac4e-152">Wait-Process</span><span class="sxs-lookup"><span data-stu-id="6ac4e-152">Wait-Process</span></span>](https://technet.microsoft.com/en-us/library/9222af7a-789d-4a09-aa90-09d7c256c799)
- [<span data-ttu-id="6ac4e-153">Debug-Process</span><span class="sxs-lookup"><span data-stu-id="6ac4e-153">Debug-Process</span></span>](https://technet.microsoft.com/en-us/library/eea1dace-3913-4dbd-b659-5a94a610eee1)
- [<span data-ttu-id="6ac4e-154">Invoke-Command</span><span class="sxs-lookup"><span data-stu-id="6ac4e-154">Invoke-Command</span></span>](https://technet.microsoft.com/en-us/library/22fd98ba-1874-492e-95a5-c069467b8462)
