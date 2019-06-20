---
title: A Visual Studio Code használata távoli szerkesztéshez és hibakereséshez
description: A Visual Studio Code használata távoli szerkesztéshez és hibakereséshez
ms.date: 06/13/2019
ms.openlocfilehash: ae3b7a3709498fcd547a48d0849b0dc880217225
ms.sourcegitcommit: 13f24786ed39ca1c07eff2b73a1974c366e31cb8
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/19/2019
ms.locfileid: "67264016"
---
# <a name="using-visual-studio-code-for-remote-editing-and-debugging"></a><span data-ttu-id="48bb4-103">A Visual Studio Code használata távoli szerkesztéshez és hibakereséshez</span><span class="sxs-lookup"><span data-stu-id="48bb4-103">Using Visual Studio Code for remote editing and debugging</span></span>

<span data-ttu-id="48bb4-104">Azok számára, az, hogy ismeri az ISE-ben, előfordulhat, hogy már ismert, hogy futtatja sikerült `psedit file.ps1` az integrált konzol – helyi vagy távoli - fájlok megnyitásához a jobb gombbal az ISE-ben.</span><span class="sxs-lookup"><span data-stu-id="48bb4-104">For those of you that are familiar with the ISE, you may recall that you could run `psedit file.ps1` from the integrated console to open files - local or remote - right in the ISE.</span></span>

<span data-ttu-id="48bb4-105">Ez a funkció a VSCode-PowerShell-bővítményének is érhető el.</span><span class="sxs-lookup"><span data-stu-id="48bb4-105">This feature is also available in the PowerShell extension for VSCode.</span></span> <span data-ttu-id="48bb4-106">Ez az útmutató bemutatja, hogyan teheti meg.</span><span class="sxs-lookup"><span data-stu-id="48bb4-106">This guide shows you how to do it.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="48bb4-107">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="48bb4-107">Prerequisites</span></span>

<span data-ttu-id="48bb4-108">Ez az útmutató feltételezi, hogy:</span><span class="sxs-lookup"><span data-stu-id="48bb4-108">This guide assumes that you have:</span></span>

- <span data-ttu-id="48bb4-109">a távoli erőforrás (például: virtuális gép, egy tárolót), hogy rendelkezik-e a hozzáférést</span><span class="sxs-lookup"><span data-stu-id="48bb4-109">A remote resource (ex: a VM, a container) that you have access to</span></span>
- <span data-ttu-id="48bb4-110">A PowerShell, és a gazdagépen futó</span><span class="sxs-lookup"><span data-stu-id="48bb4-110">PowerShell running on it and the host machine</span></span>
- <span data-ttu-id="48bb4-111">VSCode és a PowerShell-bővítmény VSCode-</span><span class="sxs-lookup"><span data-stu-id="48bb4-111">VSCode and the PowerShell extension for VSCode</span></span>

<span data-ttu-id="48bb4-112">Ez a funkció a Windows PowerShell és a PowerShell Core működik.</span><span class="sxs-lookup"><span data-stu-id="48bb4-112">This feature works on Windows PowerShell and PowerShell Core.</span></span>

<span data-ttu-id="48bb4-113">Ez a funkció is működik, ha egy távoli gépen a Rendszerfelügyeleti webszolgáltatások, a PowerShell Directet vagy az SSH-n keresztül csatlakozik.</span><span class="sxs-lookup"><span data-stu-id="48bb4-113">This feature also works when connecting to a remote machine via WinRM, PowerShell Direct, or SSH.</span></span> <span data-ttu-id="48bb4-114">Ha az SSH-val szeretne, de Windows használ, tekintse meg a [SSH Win32 verziója](https://github.com/PowerShell/Win32-OpenSSH)!</span><span class="sxs-lookup"><span data-stu-id="48bb4-114">If you want to use SSH, but are using Windows, check out the [Win32 version of SSH](https://github.com/PowerShell/Win32-OpenSSH)!</span></span>

> [!IMPORTANT]
> <span data-ttu-id="48bb4-115">A `Open-EditorFile` és `psedit` parancsok csak munkahelyi a **PowerShell integrált konzol** VSCode-a PowerShell-bővítmény által létrehozott.</span><span class="sxs-lookup"><span data-stu-id="48bb4-115">The `Open-EditorFile` and `psedit` commands only work in the **PowerShell Integrated Console** created by the PowerShell extension for VSCode.</span></span>

## <a name="usage-examples"></a><span data-ttu-id="48bb4-116">Használati példák</span><span class="sxs-lookup"><span data-stu-id="48bb4-116">Usage examples</span></span>

<span data-ttu-id="48bb4-117">A példákból látható Szerkesztés és hibakeresés egy MacBook Pro az Ubuntu virtuális géphez távoli Azure-ban.</span><span class="sxs-lookup"><span data-stu-id="48bb4-117">These examples show remote editing and debugging from a MacBook Pro to an Ubuntu VM running in Azure.</span></span> <span data-ttu-id="48bb4-118">A folyamat megegyezik a Windows.</span><span class="sxs-lookup"><span data-stu-id="48bb4-118">The process is identical on Windows.</span></span>

### <a name="local-file-editing-with-open-editorfile"></a><span data-ttu-id="48bb4-119">Szerkesztés az Open-EditorFile helyi fájl</span><span class="sxs-lookup"><span data-stu-id="48bb4-119">Local file editing with Open-EditorFile</span></span>

<span data-ttu-id="48bb4-120">A PowerShell-bővítmény a VSCode elindult, és a PowerShell integrált konzol nyitja meg, hogy írja be `Open-EditorFile foo.ps1` vagy `psedit foo.ps1` megnyitása a helyi foo.ps1 fájlt közvetlenül a szerkesztőben.</span><span class="sxs-lookup"><span data-stu-id="48bb4-120">With the PowerShell extension for VSCode started and the PowerShell Integrated Console opened, we can type `Open-EditorFile foo.ps1` or `psedit foo.ps1` to open the local foo.ps1 file right in the editor.</span></span>

![Open-EditorFile foo.ps1 helyileg működik](images/Using-VSCode-for-Remote-Editing-and-Debugging/1-open-local-file.png)

>[!NOTE]
> <span data-ttu-id="48bb4-122">A fájl `foo.ps1` már léteznie kell.</span><span class="sxs-lookup"><span data-stu-id="48bb4-122">The file `foo.ps1` must already exist.</span></span>

<span data-ttu-id="48bb4-123">Itt is:</span><span class="sxs-lookup"><span data-stu-id="48bb4-123">From there, we can:</span></span>

- <span data-ttu-id="48bb4-124">Töréspont hozzáadása a területbe</span><span class="sxs-lookup"><span data-stu-id="48bb4-124">Add breakpoints to the gutter</span></span>

  ![margó a Töréspont hozzáadása](images/Using-VSCode-for-Remote-Editing-and-Debugging/2-adding-breakpoint-gutter.png)

- <span data-ttu-id="48bb4-126">Nyomja le az F5 való hibakeresés a PowerShell-parancsfájlt.</span><span class="sxs-lookup"><span data-stu-id="48bb4-126">Hit F5 to debug the PowerShell script.</span></span>

  ![a helyi PowerShell-parancsprogram-hibakeresés](images/Using-VSCode-for-Remote-Editing-and-Debugging/3-local-debug.png)

<span data-ttu-id="48bb4-128">Hibakeresés közben is együttműködhet a hibakeresési konzolt, tekintse meg a változók a bal oldalon, és hibakeresési eszközök minden más standard hatókörében.</span><span class="sxs-lookup"><span data-stu-id="48bb4-128">While debugging, you can interact with the debug console, check out the variables in the scope on the left, and all the other standard debugging tools.</span></span>

### <a name="remote-file-editing-with-open-editorfile"></a><span data-ttu-id="48bb4-129">Szerkesztés az Open-EditorFile távoli fájl</span><span class="sxs-lookup"><span data-stu-id="48bb4-129">Remote file editing with Open-EditorFile</span></span>

<span data-ttu-id="48bb4-130">Most már folytassuk a Szerkesztés és hibakeresés távoli fájlba.</span><span class="sxs-lookup"><span data-stu-id="48bb4-130">Now let's get into remote file editing and debugging.</span></span> <span data-ttu-id="48bb4-131">A lépések nagyjából azonosak a, igazolnia kell a kezdeti lépések – adja meg a PowerShell-munkamenetet a távoli kiszolgáló csak egy dolog van.</span><span class="sxs-lookup"><span data-stu-id="48bb4-131">The steps are nearly the same, there's just one thing we need to do first - enter our PowerShell session to the remote server.</span></span>

<span data-ttu-id="48bb4-132">A parancsmag van ehhez.</span><span class="sxs-lookup"><span data-stu-id="48bb4-132">There's a cmdlet for to do so.</span></span> <span data-ttu-id="48bb4-133">Azt nevezzük `Enter-PSSession`.</span><span class="sxs-lookup"><span data-stu-id="48bb4-133">It's called `Enter-PSSession`.</span></span>

<span data-ttu-id="48bb4-134">A parancsmag watered le leírását a következő:</span><span class="sxs-lookup"><span data-stu-id="48bb4-134">The watered down explanation of the cmdlet is:</span></span>

- <span data-ttu-id="48bb4-135">`Enter-PSSession -ComputerName foo` a WinRM-n keresztül munkamenet indítása</span><span class="sxs-lookup"><span data-stu-id="48bb4-135">`Enter-PSSession -ComputerName foo` starts a session via WinRM</span></span>
- <span data-ttu-id="48bb4-136">`Enter-PSSession -ContainerId foo` és `Enter-PSSession -VmId foo` keresztül a PowerShell Directet munkamenet indítása</span><span class="sxs-lookup"><span data-stu-id="48bb4-136">`Enter-PSSession -ContainerId foo` and `Enter-PSSession -VmId foo` start a session via PowerShell Direct</span></span>
- <span data-ttu-id="48bb4-137">`Enter-PSSession -HostName foo` SSH-kapcsolaton keresztül egy munkamenet indítása</span><span class="sxs-lookup"><span data-stu-id="48bb4-137">`Enter-PSSession -HostName foo` starts a session via SSH</span></span>

<span data-ttu-id="48bb4-138">További információkért lásd a dokumentációban [Enter-PSSession](/powershell/module/microsoft.powershell.core/enter-pssession).</span><span class="sxs-lookup"><span data-stu-id="48bb4-138">For more information, see the documentation for [Enter-PSSession](/powershell/module/microsoft.powershell.core/enter-pssession).</span></span>

<span data-ttu-id="48bb4-139">Mivel mi maradunk a macOS egy Ubuntu virtuális gép az Azure-ban, használjuk SSH a távelérése.</span><span class="sxs-lookup"><span data-stu-id="48bb4-139">Since we are going from macOS to an Ubuntu VM in Azure, we are using SSH for remoting.</span></span>

<span data-ttu-id="48bb4-140">Először a integrált konzol futtassa `Enter-PSSession`.</span><span class="sxs-lookup"><span data-stu-id="48bb4-140">First, in the Integrated Console, run `Enter-PSSession`.</span></span> <span data-ttu-id="48bb4-141">Csatlakozik a távoli munkamenet során `[<hostname>]` bal oldalán, az üzenet legfeljebb mutat be.</span><span class="sxs-lookup"><span data-stu-id="48bb4-141">You're connected to the remote session when `[<hostname>]` shows up to the left of your prompt.</span></span>

![Enter-PSSession-hívás](images/Using-VSCode-for-Remote-Editing-and-Debugging/4-enter-pssession.png)

<span data-ttu-id="48bb4-143">Most tehetjük ugyanazokat a lépéseket, ha azt egy helyi parancsfájl szerkesztése.</span><span class="sxs-lookup"><span data-stu-id="48bb4-143">Now, we can do the same steps as if we are editing a local script.</span></span>

1. <span data-ttu-id="48bb4-144">Futtatás `Open-EditorFile test.ps1` vagy `psedit test.ps1` megnyitása a távoli `test.ps1` fájl</span><span class="sxs-lookup"><span data-stu-id="48bb4-144">Run `Open-EditorFile test.ps1` or `psedit test.ps1` to open the remote `test.ps1` file</span></span>

  ![Open-EditorFile test.ps1 fájl](images/Using-VSCode-for-Remote-Editing-and-Debugging/5-open-remote-file.png)

1. <span data-ttu-id="48bb4-146">A fájl/set töréspontok szerkesztése</span><span class="sxs-lookup"><span data-stu-id="48bb4-146">Edit the file/set breakpoints</span></span>

   ![szerkesztheti, és állítson be töréspontokat](images/Using-VSCode-for-Remote-Editing-and-Debugging/6-set-breakpoints.png)

1. <span data-ttu-id="48bb4-148">Hibakeresés (F5), a távoli fájl</span><span class="sxs-lookup"><span data-stu-id="48bb4-148">Start debugging (F5) the remote file</span></span>

   ![a távoli fájl hibakeresés](images/Using-VSCode-for-Remote-Editing-and-Debugging/7-start-debugging.png)

<span data-ttu-id="48bb4-150">Ha bármilyen problémába ütközik, a problémák megnyithatja a [GitHub-adattárat](https://github.com/powershell/vscode-powershell).</span><span class="sxs-lookup"><span data-stu-id="48bb4-150">If you have any problems, you can open issues in the [GitHub repo](https://github.com/powershell/vscode-powershell).</span></span>
