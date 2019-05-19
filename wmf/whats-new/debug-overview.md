---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
title: A PowerShell parancsfájlokban végzett hibakeresésének javításai
ms.openlocfilehash: f1771a451ba671da2371fcfc95374e6131573ddc
ms.sourcegitcommit: 01b81317029b28dd9b61d167045fd31f1ec7bc06
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/17/2019
ms.locfileid: "65856174"
---
# <a name="improvements-in-powershell-script-debugging"></a><span data-ttu-id="0da26-103">A PowerShell parancsfájlokban végzett hibakeresésének javításai</span><span class="sxs-lookup"><span data-stu-id="0da26-103">Improvements in PowerShell Script Debugging</span></span>

<span data-ttu-id="0da26-104">PowerShell 5.0, amelyek javítják a hibakeresési folyamatot számos fejlesztést tartalmaz.</span><span class="sxs-lookup"><span data-stu-id="0da26-104">PowerShell 5.0 includes several improvements that enhance the debugging experience.</span></span>

## <a name="break-all"></a><span data-ttu-id="0da26-105">Törés az összes</span><span class="sxs-lookup"><span data-stu-id="0da26-105">Break All</span></span>

<span data-ttu-id="0da26-106">A PowerShell-konzolt és a PowerShell ISE-ben mostantól lehetővé teszi, hogy megszakítással belépjen a hibakeresőbe parancsfájlok futtatásához.</span><span class="sxs-lookup"><span data-stu-id="0da26-106">The PowerShell console and PowerShell ISE now allow you to break into the debugger for running scripts.</span></span> <span data-ttu-id="0da26-107">Ez a módszer a helyi és távoli munkamenetek során.</span><span class="sxs-lookup"><span data-stu-id="0da26-107">This works in both local and remote sessions.</span></span>

<span data-ttu-id="0da26-108">Nyomja meg a konzolon <kbd>Ctrl</kbd>+<kbd>felosztása</kbd>.</span><span class="sxs-lookup"><span data-stu-id="0da26-108">In the console, press <kbd>Ctrl</kbd>+<kbd>Break</kbd>.</span></span>

<span data-ttu-id="0da26-109">A ISE-ben, nyomja le az ENTER <kbd>Ctrl</kbd>+<kbd>B</kbd>, vagy használja a **hibakeresése -> minden felosztása** parancs.</span><span class="sxs-lookup"><span data-stu-id="0da26-109">In ISE, press <kbd>Ctrl</kbd>+<kbd>B</kbd>, or use the **Debug -> Break All** menu command.</span></span>

## <a name="remote-debugging-and-remote-file-editing-in-powershell-ise"></a><span data-ttu-id="0da26-110">Távoli hibakeresés és a távoli fájl szerkesztése a PowerShell ISE-ben</span><span class="sxs-lookup"><span data-stu-id="0da26-110">Remote debugging and remote file editing in PowerShell ISE</span></span>

<span data-ttu-id="0da26-111">PowerShell ISE-ben mostantól lehetővé teszi megnyithatja és szerkesztheti a fájlokat a távoli kapcsolat a PSEdit parancsnak futtatásával.</span><span class="sxs-lookup"><span data-stu-id="0da26-111">PowerShell ISE now lets you open and edit files in a remote session by running the PSEdit command.</span></span>
<span data-ttu-id="0da26-112">Például nyithatja meg egy fájlt szerkesztésre a parancssorból egy távoli munkamenetet a következőképpen:</span><span class="sxs-lookup"><span data-stu-id="0da26-112">For example, you can open a file for editing from the command line in a remote session as follows:</span></span>

```powershell
[RemoteComputer1]: PS C:\> PSEdit C:\DebugDemoScripts\Test-GetMutex.ps1
```

<span data-ttu-id="0da26-113">Emellett most már szerkesztheti és menti a változásokat egy távoli fájlt, amely automatikusan megnyílik a PowerShell ISE-ben a töréspont elérésekor.</span><span class="sxs-lookup"><span data-stu-id="0da26-113">In addition, you can now edit and save changes in a remote file that is automatically opened in PowerShell ISE when you hit a breakpoint.</span></span> <span data-ttu-id="0da26-114">Most hibakeresése egy parancsfájlt, amely egy távoli számítógépen fut, javítsa ki a hibát, és futtassa újból a módosított szkriptet a fájl szerkesztésével.</span><span class="sxs-lookup"><span data-stu-id="0da26-114">Now, you can debug a script file that is running on a remote computer, edit the file to fix an error, and then rerun the modified script.</span></span>

## <a name="advanced-script-debugging"></a><span data-ttu-id="0da26-115">Speciális Erőforrásparancsfájlokban végzett hibakeresés</span><span class="sxs-lookup"><span data-stu-id="0da26-115">Advanced Script Debugging</span></span>

<span data-ttu-id="0da26-116">Nincsenek új, fejlett hibakeresési funkciók, amelyekkel bármely helyi számítógép folyamatot, amely be van töltve a PowerShell csatolja, és a hibakeresés tetszőleges futási terek, az adott folyamatban.</span><span class="sxs-lookup"><span data-stu-id="0da26-116">There are new, advanced debugging features that let you attach to any local computer process that has loaded PowerShell, and debug arbitrary runspaces in that process.</span></span>

### <a name="runspace-debugging"></a><span data-ttu-id="0da26-117">Futási térben hibakeresés</span><span class="sxs-lookup"><span data-stu-id="0da26-117">Runspace Debugging</span></span>

<span data-ttu-id="0da26-118">Új parancsmagok, amelyekkel egy folyamat az aktuális futási terek listában, és a PowerShell-konzol vagy a PowerShell ISE-ben Hibakereső csatlakoztatása a parancsprogram-hibakeresés futási térben lettek hozzáadva:</span><span class="sxs-lookup"><span data-stu-id="0da26-118">New cmdlets have been added that let you list current runspaces in a process, and attach the PowerShell console or PowerShell ISE debugger to that runspace for script debugging:</span></span>

- <span data-ttu-id="0da26-119">Get-Runspace</span><span class="sxs-lookup"><span data-stu-id="0da26-119">Get-Runspace</span></span>
- <span data-ttu-id="0da26-120">Debug-Runspace</span><span class="sxs-lookup"><span data-stu-id="0da26-120">Debug-Runspace</span></span>
- <span data-ttu-id="0da26-121">Enable-RunspaceDebug</span><span class="sxs-lookup"><span data-stu-id="0da26-121">Enable-RunspaceDebug</span></span>
- <span data-ttu-id="0da26-122">Disable-RunspaceDebug</span><span class="sxs-lookup"><span data-stu-id="0da26-122">Disable-RunspaceDebug</span></span>
- <span data-ttu-id="0da26-123">Get-RunspaceDebug</span><span class="sxs-lookup"><span data-stu-id="0da26-123">Get-RunspaceDebug</span></span>

### <a name="attach-to-process-hosting-powershell"></a><span data-ttu-id="0da26-124">PowerShell tartalmazó folyamat csatolása</span><span class="sxs-lookup"><span data-stu-id="0da26-124">Attach to Process hosting PowerShell</span></span>

<span data-ttu-id="0da26-125">Most már minden olyan számítógép folyamata, amely rendelkezik betöltött PowerShell csatlakoztathat.</span><span class="sxs-lookup"><span data-stu-id="0da26-125">You can now attach to any computer process that has PowerShell loaded.</span></span> <span data-ttu-id="0da26-126">Ehhez be a gazdagép-folyamat az az interaktív munkamenet megadásával.</span><span class="sxs-lookup"><span data-stu-id="0da26-126">You do this by entering into an interactive session with the host process.</span></span> <span data-ttu-id="0da26-127">További információ:</span><span class="sxs-lookup"><span data-stu-id="0da26-127">For more information, see:</span></span>

- [<span data-ttu-id="0da26-128">Enter-PSHostProcess</span><span class="sxs-lookup"><span data-stu-id="0da26-128">Enter-PSHostProcess</span></span>](/powershell/module/Microsoft.PowerShell.Core/Enter-PSHostProcess)
- [<span data-ttu-id="0da26-129">Exit-PSHostProcess</span><span class="sxs-lookup"><span data-stu-id="0da26-129">Exit-PSHostProcess</span></span>](/powershell/module/Microsoft.PowerShell.Core/Exit-PSHostProcess)
