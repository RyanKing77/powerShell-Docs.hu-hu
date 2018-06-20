---
ms.date: 06/05/2017
keywords: PowerShell parancsmag
title: Folyamatok kezelése folyamatparancsmagokkal
ms.assetid: 5038f612-d149-4698-8bbb-999986959e31
ms.openlocfilehash: d6d7daa810dce2d476566e4d30f03cc95bf730e6
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
ms.locfileid: "30952494"
---
# <a name="managing-processes-with-process-cmdlets"></a><span data-ttu-id="17bd9-103">Folyamatok kezelése folyamatparancsmagokkal</span><span class="sxs-lookup"><span data-stu-id="17bd9-103">Managing Processes with Process Cmdlets</span></span>

<span data-ttu-id="17bd9-104">A folyamat parancsmagok a Windows PowerShell segítségével kezelheti a Windows PowerShell helyi és távoli folyamatokhoz.</span><span class="sxs-lookup"><span data-stu-id="17bd9-104">You can use the Process cmdlets in Windows PowerShell to manage local and remote processes in Windows PowerShell.</span></span>

## <a name="getting-processes-get-process"></a><span data-ttu-id="17bd9-105">Folyamatok lekérdezése (Get-Process)</span><span class="sxs-lookup"><span data-stu-id="17bd9-105">Getting Processes (Get-Process)</span></span>

<span data-ttu-id="17bd9-106">Ahhoz, hogy a helyi számítógépen futó folyamatok, futtassa a **Get-Process** paraméter nélkül.</span><span class="sxs-lookup"><span data-stu-id="17bd9-106">To get the processes running on the local computer, run a **Get-Process** with no parameters.</span></span>

<span data-ttu-id="17bd9-107">Adja meg a folyamat neve vagy a folyamat azonosítók kaphat olyan folyamatokat.</span><span class="sxs-lookup"><span data-stu-id="17bd9-107">You can get particular processes by specifying their process names or process IDs.</span></span> <span data-ttu-id="17bd9-108">A következő parancs beolvassa az üresjárati folyamat:</span><span class="sxs-lookup"><span data-stu-id="17bd9-108">The following command gets the Idle process:</span></span>

```
PS> Get-Process -id 0

Handles  NPM(K)    PM(K)      WS(K) VM(M)   CPU(s)     Id ProcessName
-------  ------    -----      ----- -----   ------     -- -----------
      0       0        0         16     0               0 Idle
```

<span data-ttu-id="17bd9-109">Bár ez normális vissza adatot nem bizonyos esetekben, amikor megad egy folyamat. a folyamatazonosító parancsmagok **Get-Process** hibát generál, ha nincs találat megtalálja, mert a szokásos szándéka az, hogy beolvasni egy ismert futó folyamat.</span><span class="sxs-lookup"><span data-stu-id="17bd9-109">Although it is normal for cmdlets to return no data in some situations, when you specify a process by its ProcessId, **Get-Process** generates an error if it finds no matches, because the usual intent is to retrieve a known running process.</span></span> <span data-ttu-id="17bd9-110">Egyetlen folyamat sem ezzel az azonosítóval van, akkor valószínű, hogy az azonosító érvénytelen, vagy az, hogy már kilépett a folyamat egyik fontos:</span><span class="sxs-lookup"><span data-stu-id="17bd9-110">If there is no process with that Id, it is likely that the Id is incorrect or that the process of interest has already exited:</span></span>

```
PS> Get-Process -Id 99

Get-Process : No process with process ID 99 was found.
At line:1 char:12
+ Get-Process  <<<< -Id 99
```

<span data-ttu-id="17bd9-111">A Name paraméter, a Get-Process parancsmag segítségével adja meg a folyamat neve alapján folyamatok egy részét.</span><span class="sxs-lookup"><span data-stu-id="17bd9-111">You can use the Name parameter of the Get-Process cmdlet to specify a subset of processes based on the process name.</span></span> <span data-ttu-id="17bd9-112">A Name paraméter hajthatja végre több név a vesszővel tagolt listáját, és helyettesítő karakterekkel, támogatja, megadhatja a mintában.</span><span class="sxs-lookup"><span data-stu-id="17bd9-112">The Name parameter can take multiple names in a comma-separated list and it supports the use of wildcards, so you can type name patterns.</span></span>

<span data-ttu-id="17bd9-113">Például a következő paranccsal lekérdezi a "ex." kezdődő folyamat</span><span class="sxs-lookup"><span data-stu-id="17bd9-113">For example, the following command gets process whose names begin with "ex."</span></span>

```
PS> Get-Process -Name ex*

Handles  NPM(K)    PM(K)      WS(K) VM(M)   CPU(s)     Id ProcessName
-------  ------    -----      ----- -----   ------     -- -----------
    234       7     5572      12484   134     2.98   1684 EXCEL
    555      15    34500      12384   134   105.25    728 explorer
```

<span data-ttu-id="17bd9-114">Mivel a .NET System.Diagnostics.Process osztály a Windows PowerShell folyamatok alapját, követi a egyezmények System.Diagnostics.Process által használt néhány.</span><span class="sxs-lookup"><span data-stu-id="17bd9-114">Because the .NET System.Diagnostics.Process class is the foundation for Windows PowerShell processes, it follows some of the conventions used by System.Diagnostics.Process.</span></span> <span data-ttu-id="17bd9-115">Ezen egyezmények egyike, hogy a folyamat végrehajtható fájl nevét soha nem tartalmazza a ".exe" végén található a végrehajtható fájl nevét.</span><span class="sxs-lookup"><span data-stu-id="17bd9-115">One of those conventions is that the process name for an executable never includes the ".exe" at the end of the executable name.</span></span>

<span data-ttu-id="17bd9-116">**Get-Process** a Name paraméter több értéket is fogad.</span><span class="sxs-lookup"><span data-stu-id="17bd9-116">**Get-Process** also accepts multiple values for the Name parameter.</span></span>

```
PS> Get-Process -Name exp*,power*

Handles  NPM(K)    PM(K)      WS(K) VM(M)   CPU(s)     Id ProcessName
-------  ------    -----      ----- -----   ------     -- -----------
    540      15    35172      48148   141    88.44    408 explorer
    605       9    30668      29800   155     7.11   3052 powershell
```

<span data-ttu-id="17bd9-117">A ComputerName paraméterre, a Get-Process folyamatok lekérni a távoli számítógépeken használható.</span><span class="sxs-lookup"><span data-stu-id="17bd9-117">You can use the ComputerName parameter of Get-Process to get processes on remote computers.</span></span> <span data-ttu-id="17bd9-118">A következő parancs például a PowerShell folyamatok lekérdezi a helyi számítógépen (a "localhost" képviseli) és két távoli számítógépen.</span><span class="sxs-lookup"><span data-stu-id="17bd9-118">For example, the following command gets the PowerShell processes on the local computer (represented by "localhost") and on two remote computers.</span></span>

```
PS> Get-Process -Name PowerShell -ComputerName localhost, Server01, Server02

Handles  NPM(K)    PM(K)      WS(K) VM(M)   CPU(s)     Id ProcessName
-------  ------    -----      ----- -----   ------     -- -----------
    258       8    29772      38636   130            3700 powershell
    398      24    75988      76800   572            5816 powershell
    605       9    30668      29800   155     7.11   3052 powershell
```

<span data-ttu-id="17bd9-119">A számítógép nevében a rendszer nem egyértelmű a kijelzett, de a számítógépnév tulajdonság Get-Process visszaadó folyamat objektum tárolódnak.</span><span class="sxs-lookup"><span data-stu-id="17bd9-119">The computer names are not evident in this display, but they are stored in the MachineName property of the process objects that Get-Process returns.</span></span> <span data-ttu-id="17bd9-120">A következő parancsot a Format-Table parancsmag segítségével jeleníti meg, a folyamat azonosítója, a folyamatnév és a számítógépnév (számítógépnév) a folyamat objektumok tulajdonságai.</span><span class="sxs-lookup"><span data-stu-id="17bd9-120">The following command uses the Format-Table cmdlet to display the process ID, ProcessName and MachineName (ComputerName) properties of the process objects.</span></span>

```
PS> Get-Process -Name PowerShell -ComputerName localhost, Server01, Server01 | Format-Table -Property ID, ProcessName, MachineName

  Id ProcessName MachineName
  -- ----------- -----------
3700 powershell  Server01
3052 powershell  Server02
5816 powershell  localhost
```

<span data-ttu-id="17bd9-121">Összetettebb hozzáadja a számítógépnév tulajdonság Get-Process szabványos megjelenítéséhez.</span><span class="sxs-lookup"><span data-stu-id="17bd9-121">This more complex command adds the MachineName property to the standard Get-Process display.</span></span>

```
PS> Get-Process powershell -ComputerName localhost, Server01, Server02 |
    Format-Table -Property Handles,
        @{Label="NPM(K)";Expression={[int]($_.NPM/1024)}},
        @{Label="PM(K)";Expression={[int]($_.PM/1024)}},
        @{Label="WS(K)";Expression={[int]($_.WS/1024)}},
        @{Label="VM(M)";Expression={[int]($_.VM/1MB)}},
        @{Label="CPU(s)";Expression={if ($_.CPU -ne $() {$_.CPU.ToString("N")}}},
        Id, ProcessName, MachineName -auto

Handles  NPM(K)  PM(K) WS(K) VM(M) CPU(s)  Id ProcessName  MachineName
-------  ------  ----- ----- ----- ------  -- -----------  -----------
    258       8  29772 38636   130         3700 powershell Server01
    398      24  75988 76800   572         5816 powershell localhost
    605       9  30668 29800   155 7.11    3052 powershell Server02
```

## <a name="stopping-processes-stop-process"></a><span data-ttu-id="17bd9-122">Folyamatok (Stop-Process) leállítása</span><span class="sxs-lookup"><span data-stu-id="17bd9-122">Stopping Processes (Stop-Process)</span></span>

<span data-ttu-id="17bd9-123">A Windows PowerShell folyamatok listázása, de mi a helyzet a folyamat leállítása rugalmasságot biztosít?</span><span class="sxs-lookup"><span data-stu-id="17bd9-123">Windows PowerShell gives you flexibility for listing processes, but what about stopping a process?</span></span>

<span data-ttu-id="17bd9-124">A **Stop-Process** parancsmag időt vesz igénybe, egy nevű vagy azonosítójú adhatja meg a folyamat le kívánja állítani.</span><span class="sxs-lookup"><span data-stu-id="17bd9-124">The **Stop-Process** cmdlet takes a Name or Id to specify a process you want to stop.</span></span> <span data-ttu-id="17bd9-125">A folyamat leállítása függ az engedélyeket.</span><span class="sxs-lookup"><span data-stu-id="17bd9-125">Your ability to stop processes depends on your permissions.</span></span> <span data-ttu-id="17bd9-126">Egyes folyamatok nem lehet leállítani.</span><span class="sxs-lookup"><span data-stu-id="17bd9-126">Some processes cannot be stopped.</span></span> <span data-ttu-id="17bd9-127">Például ha megpróbálja leállítani az üresjárati folyamat, hibaüzenetet kap:</span><span class="sxs-lookup"><span data-stu-id="17bd9-127">For example, if you try to stop the idle process, you get an error:</span></span>

```
PS> Stop-Process -Name Idle
Stop-Process : Process 'Idle (0)' cannot be stopped due to the following error:
 Access is denied
At line:1 char:13
+ Stop-Process  <<<< -Name Idle
```

<span data-ttu-id="17bd9-128">A kérdés is kényszeríthető a **megerősítése** paraméter.</span><span class="sxs-lookup"><span data-stu-id="17bd9-128">You can also force prompting with the **Confirm** parameter.</span></span> <span data-ttu-id="17bd9-129">Ez a paraméter különösen hasznos, ha egy helyettesítő karakter adható meg a folyamat neve, mert előfordulhat, hogy véletlenül felel meg valamelyik folyamat nem szeretné leállítani:</span><span class="sxs-lookup"><span data-stu-id="17bd9-129">This parameter is particularly useful if you use a wildcard when specifying the process name, because you may accidentally match some processes you do not want to stop:</span></span>

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

<span data-ttu-id="17bd9-130">Összetett folyamat adatkezelési esetében néhány, a parancsmagok szűrés objektum használatával.</span><span class="sxs-lookup"><span data-stu-id="17bd9-130">Complex process manipulation is possible by using some of the object filtering cmdlets.</span></span> <span data-ttu-id="17bd9-131">Egy folyamat objektumot válaszoló tulajdonsága igaz, ha már nem válaszol, mivel le lehet állítani az összes nem válaszoló alkalmazásokat a következő paranccsal:</span><span class="sxs-lookup"><span data-stu-id="17bd9-131">Because a Process object has a Responding property that is true when it is no longer responding, you can stop all nonresponsive applications with the following command:</span></span>

```powershell
Get-Process | Where-Object -FilterScript {$_.Responding -eq $false} | Stop-Process
```

<span data-ttu-id="17bd9-132">Más helyzetekben használhatja ugyanezt a megközelítést.</span><span class="sxs-lookup"><span data-stu-id="17bd9-132">You can use the same approach in other situations.</span></span> <span data-ttu-id="17bd9-133">Tegyük fel például, hogy egy másodlagos értesítési terület alkalmazás automatikusan fut, amikor a felhasználók egy másik alkalmazás indításához.</span><span class="sxs-lookup"><span data-stu-id="17bd9-133">For example, suppose a secondary notification area application automatically runs when users start another application.</span></span> <span data-ttu-id="17bd9-134">Előfordulhat, hogy ez nem működik megfelelően a Terminálszolgáltatások-munkamenetekben, de továbbra is szeretné tartani a fizikai számítógép konzol futó munkameneteket.</span><span class="sxs-lookup"><span data-stu-id="17bd9-134">You may find that this does not work correctly in Terminal Services sessions, but you still want to keep it in sessions that run on the physical computer console.</span></span> <span data-ttu-id="17bd9-135">Mindig kapcsolódik a fizikai számítógép asztali munkamenetek rendelkezik egy munkamenet-Azonosítót, 0, így a folyamat összes példánya esetén más munkamenetekben használatával történő leállíthatja **Where-Object** és a folyamat **SessionId** :</span><span class="sxs-lookup"><span data-stu-id="17bd9-135">Sessions connected to the physical computer desktop always have a session ID of 0, so you can stop all instances of the process that are in other sessions by using **Where-Object** and the process, **SessionId**:</span></span>

```powershell
Get-Process -Name BadApp | Where-Object -FilterScript {$_.SessionId -neq 0} | Stop-Process
```

<span data-ttu-id="17bd9-136">A Stop-Process parancsmaghoz nem tartozik a ComputerName paraméterre.</span><span class="sxs-lookup"><span data-stu-id="17bd9-136">The Stop-Process cmdlet does not have a ComputerName parameter.</span></span> <span data-ttu-id="17bd9-137">Ezért a stop-process parancs futtatása távoli számítógépen, akkor kell az Invoke-Command parancsmaggal.</span><span class="sxs-lookup"><span data-stu-id="17bd9-137">Therefore, to run a stop process command on a remote computer, you need to use the Invoke-Command cmdlet.</span></span> <span data-ttu-id="17bd9-138">Például a kiszolgalo01 távoli számítógépen a PowerShell folyamat leállításához írja be:</span><span class="sxs-lookup"><span data-stu-id="17bd9-138">For example, to stop the PowerShell process on the Server01 remote computer, type:</span></span>

```powershell
Invoke-Command -ComputerName Server01 {Stop-Process Powershell}
```

## <a name="stopping-all-other-windows-powershell-sessions"></a><span data-ttu-id="17bd9-139">Minden más Windows PowerShell-munkamenetekben leállítása</span><span class="sxs-lookup"><span data-stu-id="17bd9-139">Stopping All Other Windows PowerShell Sessions</span></span>

<span data-ttu-id="17bd9-140">Alkalmanként lehet hasznos, ha szeretné tudni állítsa le az összes futó Windows PowerShell-munkamenetekben eltérő az aktuális munkamenet.</span><span class="sxs-lookup"><span data-stu-id="17bd9-140">It may occasionally be useful to be able to stop all running Windows PowerShell sessions other than the current session.</span></span> <span data-ttu-id="17bd9-141">Ha a munkamenet túl sok erőforrást használ, vagy nem érhető el (Ez futtathatnak távolról, vagy egy másik asztal munkamenetben), nem lehet közvetlenül állítsa le.</span><span class="sxs-lookup"><span data-stu-id="17bd9-141">If a session is using too many resources or is inaccessible (it may be running remotely or in another desktop session), you may not be able to directly stop it.</span></span> <span data-ttu-id="17bd9-142">Ha megpróbálja leállítani az összes futó munkameneteket, azonban az aktuális munkamenet megszüntethető helyette.</span><span class="sxs-lookup"><span data-stu-id="17bd9-142">If you try to stop all running sessions, however, the current session may be terminated instead.</span></span>

<span data-ttu-id="17bd9-143">Minden Windows PowerShell-munkamenetet egy környezeti változó, amely tartalmazza a Windows PowerShell-folyamat azonosítója azonosítója (PID) rendelkezik.</span><span class="sxs-lookup"><span data-stu-id="17bd9-143">Each Windows PowerShell session has an environment variable PID that contains the Id of the Windows PowerShell process.</span></span> <span data-ttu-id="17bd9-144">Ellenőrizze a $PID minden munkamenet azonosítója alapján, és állítsa le a csak a Windows PowerShell-munkamenetekben, amelyek egy másik azonosítót. A következő adatcsatorna parancs ezt, és leállított munkamenetek listáját adja vissza (használata miatt a **PassThru** paraméter):</span><span class="sxs-lookup"><span data-stu-id="17bd9-144">You can check the $PID against the Id of each session and terminate only Windows PowerShell sessions that have a different Id. The following pipeline command does this and returns the list of terminated sessions (because of the use of the **PassThru** parameter):</span></span>

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

## <a name="starting-debugging-and-waiting-for-processes"></a><span data-ttu-id="17bd9-145">Indítása, a Hibakeresés és a folyamatok vár</span><span class="sxs-lookup"><span data-stu-id="17bd9-145">Starting, Debugging, and Waiting for Processes</span></span>

<span data-ttu-id="17bd9-146">Windows PowerShell is tartalmaz parancsmagokat indítása (vagy újraindítása), hibakeresési egy folyamatot, és várja meg a folyamat befejezéséhez a parancs futtatása előtt.</span><span class="sxs-lookup"><span data-stu-id="17bd9-146">Windows PowerShell also comes with cmdlets to start (or restart), debug a process, and wait for a process to complete before running a command.</span></span> <span data-ttu-id="17bd9-147">Ezekkel a parancsmagokkal kapcsolatos információkért lásd a parancsmag súgó-témakörének parancsmagok.</span><span class="sxs-lookup"><span data-stu-id="17bd9-147">For information about these cmdlets, see the cmdlet help topic for each cmdlet.</span></span>

## <a name="see-also"></a><span data-ttu-id="17bd9-148">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="17bd9-148">See Also</span></span>

- <span data-ttu-id="17bd9-149">[Get-Process [m2]](https://technet.microsoft.com/en-us/library/27a05dbd-4b69-48a3-8d55-b295f6225f15)</span><span class="sxs-lookup"><span data-stu-id="17bd9-149">[Get-Process [m2]](https://technet.microsoft.com/en-us/library/27a05dbd-4b69-48a3-8d55-b295f6225f15)</span></span>
- <span data-ttu-id="17bd9-150">[Stop-Process [m2]](https://technet.microsoft.com/en-us/library/12454238-9881-457a-bde4-fb6cd124deec)</span><span class="sxs-lookup"><span data-stu-id="17bd9-150">[Stop-Process [m2]](https://technet.microsoft.com/en-us/library/12454238-9881-457a-bde4-fb6cd124deec)</span></span>
- [<span data-ttu-id="17bd9-151">Start-Process</span><span class="sxs-lookup"><span data-stu-id="17bd9-151">Start-Process</span></span>](https://technet.microsoft.com/en-us/library/41a7e43c-9bb3-4dc2-8b0c-f6c32962e72c)
- [<span data-ttu-id="17bd9-152">Wait-Process</span><span class="sxs-lookup"><span data-stu-id="17bd9-152">Wait-Process</span></span>](https://technet.microsoft.com/en-us/library/9222af7a-789d-4a09-aa90-09d7c256c799)
- [<span data-ttu-id="17bd9-153">Debug-Process</span><span class="sxs-lookup"><span data-stu-id="17bd9-153">Debug-Process</span></span>](https://technet.microsoft.com/en-us/library/eea1dace-3913-4dbd-b659-5a94a610eee1)
- [<span data-ttu-id="17bd9-154">Invoke-Command parancsot</span><span class="sxs-lookup"><span data-stu-id="17bd9-154">Invoke-Command</span></span>](https://technet.microsoft.com/en-us/library/22fd98ba-1874-492e-95a5-c069467b8462)