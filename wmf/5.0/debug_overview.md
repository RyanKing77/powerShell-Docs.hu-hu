---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: 22a027ebc97e15075980bc77ce272d8ecdae0b5f
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62058661"
---
# <a name="improvements-in-powershell-script-debugging"></a><span data-ttu-id="f1c7a-102">A PowerShell parancsfájlokban végzett hibakeresésének javításai</span><span class="sxs-lookup"><span data-stu-id="f1c7a-102">Improvements in PowerShell Script Debugging</span></span>

<span data-ttu-id="f1c7a-103">Számos fejlesztéssel történtek a PowerShell 5.0 a hibakeresési élmény:</span><span class="sxs-lookup"><span data-stu-id="f1c7a-103">A number of improvements were made in PowerShell 5.0 to enhance the debugging experience:</span></span>

## <a name="break-all"></a><span data-ttu-id="f1c7a-104">Törés az összes</span><span class="sxs-lookup"><span data-stu-id="f1c7a-104">Break All</span></span>

<span data-ttu-id="f1c7a-105">A PowerShell-konzolt és a Windows PowerShell ISE-ben mostantól lehetővé teszi, hogy megszakítással belépjen a hibakeresőbe parancsfájlok futtatásához.</span><span class="sxs-lookup"><span data-stu-id="f1c7a-105">The PowerShell console and Windows PowerShell ISE now allow you to break into the debugger for running scripts.</span></span> <span data-ttu-id="f1c7a-106">Ez a módszer a helyi és távoli munkamenetek során.</span><span class="sxs-lookup"><span data-stu-id="f1c7a-106">This works in both local and remote sessions.</span></span>

<span data-ttu-id="f1c7a-107">Nyomja meg a konzolon **Ctrl + Break**.</span><span class="sxs-lookup"><span data-stu-id="f1c7a-107">In the console, press **Ctrl+Break**.</span></span>

<span data-ttu-id="f1c7a-108">A ISE-ben, nyomja le az ENTER **Ctrl + B**, vagy használja a **hibakeresése -> minden felosztása** parancs.</span><span class="sxs-lookup"><span data-stu-id="f1c7a-108">In ISE, press **Ctrl+B**, or use the **Debug -> Break All** menu command.</span></span>

## <a name="remote-debugging-and-remote-file-editing-in-windows-powershell-ise"></a><span data-ttu-id="f1c7a-109">Távoli hibakeresés és a távoli fájl szerkesztése a Windows PowerShell ISE-ben</span><span class="sxs-lookup"><span data-stu-id="f1c7a-109">Remote debugging and remote file editing in Windows PowerShell ISE</span></span>

<span data-ttu-id="f1c7a-110">Windows PowerShell ISE-ben mostantól lehetővé teszi megnyithatja és szerkesztheti a fájlokat a távoli kapcsolat a PSEdit parancsnak futtatásával.</span><span class="sxs-lookup"><span data-stu-id="f1c7a-110">Windows PowerShell ISE now lets you open and edit files in a remote session by running the PSEdit command.</span></span>
<span data-ttu-id="f1c7a-111">Például nyithatja meg egy fájlt szerkesztésre a parancssorból egy távoli munkamenetet a következőképpen:</span><span class="sxs-lookup"><span data-stu-id="f1c7a-111">For example, you can open a file for editing from the command line in a remote session as follows:</span></span>

```powershell
[RemoteComputer1]: PS C:\> PSEdit C:\DebugDemoScripts\Test-GetMutex.ps1
```

<span data-ttu-id="f1c7a-112">Emellett most már szerkesztheti és menti a változásokat egy távoli fájlt, amely automatikusan megnyílik a Windows PowerShell ISE-ben a töréspont elérésekor.</span><span class="sxs-lookup"><span data-stu-id="f1c7a-112">In addition, you can now edit and save changes in a remote file that is automatically opened in Windows PowerShell ISE when you hit a breakpoint.</span></span>
<span data-ttu-id="f1c7a-113">Most hibakeresése egy parancsfájlt, amely egy távoli számítógépen fut, javítsa ki a hibát, és futtassa újból a módosított szkriptet a fájl szerkesztésével.</span><span class="sxs-lookup"><span data-stu-id="f1c7a-113">Now, you can debug a script file that is running on a remote computer, edit the file to fix an error, and then rerun the modified script.</span></span>

## <a name="advanced-script-debugging"></a><span data-ttu-id="f1c7a-114">Speciális Erőforrásparancsfájlokban végzett hibakeresés</span><span class="sxs-lookup"><span data-stu-id="f1c7a-114">Advanced Script Debugging</span></span>

<span data-ttu-id="f1c7a-115">Nincsenek új, fejlett hibakeresési funkciók, amelyekkel bármely helyi számítógép folyamatot, amely be van töltve a Windows PowerShell csatolja, és a hibakeresés tetszőleges futási terek, az adott folyamatban.</span><span class="sxs-lookup"><span data-stu-id="f1c7a-115">There are new, advanced debugging features that let you attach to any local computer process that has loaded Windows PowerShell, and debug arbitrary runspaces in that process.</span></span>

### <a name="runspace-debugging"></a><span data-ttu-id="f1c7a-116">Futási térben hibakeresés</span><span class="sxs-lookup"><span data-stu-id="f1c7a-116">Runspace Debugging</span></span>

<span data-ttu-id="f1c7a-117">Új parancsmagok, amelyekkel egy folyamat az aktuális futási terek listában, és a Windows PowerShell-konzolt vagy az ISE Hibakereső csatlakoztatása a parancsprogram-hibakeresés futási térben lettek hozzáadva:</span><span class="sxs-lookup"><span data-stu-id="f1c7a-117">New cmdlets have been added that let you list current runspaces in a process, and attach the Windows PowerShell console or ISE debugger to that runspace for script debugging:</span></span>

-   <span data-ttu-id="f1c7a-118">Get-Runspace</span><span class="sxs-lookup"><span data-stu-id="f1c7a-118">Get-Runspace</span></span>
-   <span data-ttu-id="f1c7a-119">Debug-Runspace</span><span class="sxs-lookup"><span data-stu-id="f1c7a-119">Debug-Runspace</span></span>
-   <span data-ttu-id="f1c7a-120">Enable-RunspaceDebug</span><span class="sxs-lookup"><span data-stu-id="f1c7a-120">Enable-RunspaceDebug</span></span>
-   <span data-ttu-id="f1c7a-121">Disable-RunspaceDebug</span><span class="sxs-lookup"><span data-stu-id="f1c7a-121">Disable-RunspaceDebug</span></span>
-   <span data-ttu-id="f1c7a-122">Get-RunspaceDebug</span><span class="sxs-lookup"><span data-stu-id="f1c7a-122">Get-RunspaceDebug</span></span>

### <a name="attach-to-process-hosting-powershell"></a><span data-ttu-id="f1c7a-123">PowerShell tartalmazó folyamat csatolása</span><span class="sxs-lookup"><span data-stu-id="f1c7a-123">Attach to Process hosting PowerShell</span></span>

<span data-ttu-id="f1c7a-124">Most már minden olyan számítógép folyamata, amely rendelkezik a Windows PowerShell betöltött csatlakoztathat.</span><span class="sxs-lookup"><span data-stu-id="f1c7a-124">You can now attach to any computer process that has Windows PowerShell loaded.</span></span> <span data-ttu-id="f1c7a-125">Ehhez a folyamathoz hasonló módon, hogy hogyan ad meg egy interaktív távoli munkamenetet a Enter-PSSession parancsmag futtatásával egy interaktív munkamenetbe írja be:</span><span class="sxs-lookup"><span data-stu-id="f1c7a-125">You do this by entering into an interactive session with the process, similarly to how you enter into an interactive remote session by running the Enter-PSSession cmdlet:</span></span>

-   <span data-ttu-id="f1c7a-126">Enter-PSHostProcess</span><span class="sxs-lookup"><span data-stu-id="f1c7a-126">Enter-PSHostProcess</span></span>
-   <span data-ttu-id="f1c7a-127">Exit-PSHostProcess</span><span class="sxs-lookup"><span data-stu-id="f1c7a-127">Exit-PSHostProcess</span></span>
