---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "WMF, a powershell, a beállítása"
ms.openlocfilehash: aaf1809277f072c82e5a1a862ea64b75586e32d1
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2017
---
# <a name="improvements-in-powershell-script-debugging"></a><span data-ttu-id="e4b74-102">A PowerShell-parancsprogram-hibakeresés fejlesztései</span><span class="sxs-lookup"><span data-stu-id="e4b74-102">Improvements in PowerShell Script Debugging</span></span>

<span data-ttu-id="e4b74-103">Számos fejlesztéssel PowerShell 5.0 került sor a hibakeresési élmény javítása érdekében:</span><span class="sxs-lookup"><span data-stu-id="e4b74-103">A number of improvements were made in PowerShell 5.0 to enhance the debugging experience:</span></span>

## <a name="break-all"></a><span data-ttu-id="e4b74-104">Törés az összes</span><span class="sxs-lookup"><span data-stu-id="e4b74-104">Break All</span></span>

<span data-ttu-id="e4b74-105">A PowerShell-konzolban és a Windows PowerShell ISE most engedélyezi, hogy megszakítással belépjen a hibakeresőbe parancsfájlok futtatásához.</span><span class="sxs-lookup"><span data-stu-id="e4b74-105">The PowerShell console and Windows PowerShell ISE now allow you to break into the debugger for running scripts.</span></span> <span data-ttu-id="e4b74-106">Ez a helyi és távoli munkamenetek működik.</span><span class="sxs-lookup"><span data-stu-id="e4b74-106">This works in both local and remote sessions.</span></span>

<span data-ttu-id="e4b74-107">A konzolon nyomja le az **Ctrl + Break**.</span><span class="sxs-lookup"><span data-stu-id="e4b74-107">In the console, press **Ctrl+Break**.</span></span>

<span data-ttu-id="e4b74-108">ISE, nyomja le az **Ctrl + B**, vagy használja a **hibakeresési -> minden törés** menüparancshoz.</span><span class="sxs-lookup"><span data-stu-id="e4b74-108">In ISE, press **Ctrl+B**, or use the **Debug -> Break All** menu command.</span></span>

## <a name="remote-debugging-and-remote-file-editing-in-windows-powershell-ise"></a><span data-ttu-id="e4b74-109">Távoli hibakereséssel és a távoli fájl szerkesztése a Windows PowerShell ISE</span><span class="sxs-lookup"><span data-stu-id="e4b74-109">Remote debugging and remote file editing in Windows PowerShell ISE</span></span>

<span data-ttu-id="e4b74-110">A Windows PowerShell ISE lehetővé teszi a megnyitni és módosítani a fájlok a távoli kapcsolat a PSEdit parancs futtatásával.</span><span class="sxs-lookup"><span data-stu-id="e4b74-110">Windows PowerShell ISE now lets you open and edit files in a remote session by running the PSEdit command.</span></span>
<span data-ttu-id="e4b74-111">Például nyithatja meg a fájlt szerkesztésre a parancssorból egy távoli munkamenet az alábbiak szerint:</span><span class="sxs-lookup"><span data-stu-id="e4b74-111">For example, you can open a file for editing from the command line in a remote session as follows:</span></span>

```powershell
[RemoteComputer1]: PS C:\> PSEdit C:\DebugDemoScripts\Test-GetMutex.ps1
```

<span data-ttu-id="e4b74-112">Emellett mostantól szerkeszteni és menteni egy távoli fájlban, amely automatikusan megnyílik a Windows PowerShell ISE, amikor a töréspont kattint.</span><span class="sxs-lookup"><span data-stu-id="e4b74-112">In addition, you can now edit and save changes in a remote file that is automatically opened in Windows PowerShell ISE when you hit a breakpoint.</span></span>
<span data-ttu-id="e4b74-113">Most debug egy parancsfájlt, amely egy távoli számítógépen fut, a hiba javításához, és futtassa újból a módosítási parancsfájl fájl szerkesztésével.</span><span class="sxs-lookup"><span data-stu-id="e4b74-113">Now, you can debug a script file that is running on a remote computer, edit the file to fix an error, and then rerun the modified script.</span></span>

## <a name="advanced-script-debugging"></a><span data-ttu-id="e4b74-114">Speciális parancsprogram-hibakeresés engedélyezése</span><span class="sxs-lookup"><span data-stu-id="e4b74-114">Advanced Script Debugging</span></span>

<span data-ttu-id="e4b74-115">Nincsenek új, speciális hibakeresési szolgáltatásokat, amelyek lehetővé teszik a helyi számítógép folyamat, amely be van töltve a Windows PowerShell csatolja, és hibakeresési tetszőleges futási terek a folyamatba.</span><span class="sxs-lookup"><span data-stu-id="e4b74-115">There are new, advanced debugging features that let you attach to any local computer process that has loaded Windows PowerShell, and debug arbitrary runspaces in that process.</span></span>

### <a name="runspace-debugging"></a><span data-ttu-id="e4b74-116">Futási térben hibakeresés</span><span class="sxs-lookup"><span data-stu-id="e4b74-116">Runspace Debugging</span></span>

<span data-ttu-id="e4b74-117">Új parancsmagokkal bővült, amelyek lehetővé teszik, hogy a folyamat az aktuális futási terek listában, és a Windows PowerShell-konzolt vagy az ISE hibakereső csatlakoztatni, hogy futási térben a parancsprogram-hibakeresés engedélyezése:</span><span class="sxs-lookup"><span data-stu-id="e4b74-117">New cmdlets have been added that let you list current runspaces in a process, and attach the Windows PowerShell console or ISE debugger to that runspace for script debugging:</span></span>

-   <span data-ttu-id="e4b74-118">Get-futási térben</span><span class="sxs-lookup"><span data-stu-id="e4b74-118">Get-Runspace</span></span>
-   <span data-ttu-id="e4b74-119">Hibakeresési-futási térben</span><span class="sxs-lookup"><span data-stu-id="e4b74-119">Debug-Runspace</span></span>
-   <span data-ttu-id="e4b74-120">Enable-RunspaceDebug</span><span class="sxs-lookup"><span data-stu-id="e4b74-120">Enable-RunspaceDebug</span></span>
-   <span data-ttu-id="e4b74-121">Disable-RunspaceDebug</span><span class="sxs-lookup"><span data-stu-id="e4b74-121">Disable-RunspaceDebug</span></span>
-   <span data-ttu-id="e4b74-122">Get-RunspaceDebug</span><span class="sxs-lookup"><span data-stu-id="e4b74-122">Get-RunspaceDebug</span></span>

### <a name="attach-to-process-hosting-powershell"></a><span data-ttu-id="e4b74-123">PowerShell tartalmazó folyamat csatolása</span><span class="sxs-lookup"><span data-stu-id="e4b74-123">Attach to Process hosting PowerShell</span></span>

<span data-ttu-id="e4b74-124">E számítógép folyamat, amely rendelkezik a Windows PowerShell betöltött most csatlakoztatni.</span><span class="sxs-lookup"><span data-stu-id="e4b74-124">You can now attach to any computer process that has Windows PowerShell loaded.</span></span> <span data-ttu-id="e4b74-125">Ehhez a folyamathoz hasonló módon, hogy miként meg interaktív távoli munkamenetbe a Enter-PSSession parancsmag futtatásával egy interaktív munkamenet megadva:</span><span class="sxs-lookup"><span data-stu-id="e4b74-125">You do this by entering into an interactive session with the process, similarly to how you enter into an interactive remote session by running the Enter-PSSession cmdlet:</span></span>

-   <span data-ttu-id="e4b74-126">Adja meg PSHostProcess</span><span class="sxs-lookup"><span data-stu-id="e4b74-126">Enter-PSHostProcess</span></span>
-   <span data-ttu-id="e4b74-127">Kilépés-PSHostProcess</span><span class="sxs-lookup"><span data-stu-id="e4b74-127">Exit-PSHostProcess</span></span>

