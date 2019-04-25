---
title: A Visual Studio Code használata távoli szerkesztéshez és hibakereséshez
description: A Visual Studio Code használata távoli szerkesztéshez és hibakereséshez
ms.date: 08/06/2018
ms.openlocfilehash: fbc1ee3556e822b4afb2b37111d0688dc89fdab3
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62086671"
---
# <a name="using-visual-studio-code-for-remote-editing-and-debugging"></a><span data-ttu-id="27da7-103">A Visual Studio Code használata távoli szerkesztéshez és hibakereséshez</span><span class="sxs-lookup"><span data-stu-id="27da7-103">Using Visual Studio Code for remote editing and debugging</span></span>

<span data-ttu-id="27da7-104">Azoknak, azokat az ISE ismernie, előfordulhat, hogy már ismert, hogy futtatja sikerült `psedit file.ps1` az integrált konzol – helyi vagy távoli - fájlok megnyitásához a jobb gombbal az ISE-ben.</span><span class="sxs-lookup"><span data-stu-id="27da7-104">For those of you that were familiar with the ISE, you may recall that you could run `psedit file.ps1` from the integrated console to open files - local or remote - right in the ISE.</span></span>

<span data-ttu-id="27da7-105">Azt tapasztaltuk, ez a funkció érhető el a PowerShell-VSCode-bővítményben.</span><span class="sxs-lookup"><span data-stu-id="27da7-105">As it turns out, this feature is also available in the PowerShell extension for VSCode.</span></span> <span data-ttu-id="27da7-106">Ez az útmutató bemutatja, hogyan kell tenni.</span><span class="sxs-lookup"><span data-stu-id="27da7-106">This guide will show you how to do it.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="27da7-107">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="27da7-107">Prerequisites</span></span>

<span data-ttu-id="27da7-108">Ez az útmutató feltételezi, hogy:</span><span class="sxs-lookup"><span data-stu-id="27da7-108">This guide assumes that you have:</span></span>

- <span data-ttu-id="27da7-109">a távoli erőforrás (például: virtuális gép, egy tárolót), hogy rendelkezik-e a hozzáférést</span><span class="sxs-lookup"><span data-stu-id="27da7-109">a remote resource (ex: a VM, a container) that you have access to</span></span>
- <span data-ttu-id="27da7-110">A PowerShell, és a gazdagépen futó</span><span class="sxs-lookup"><span data-stu-id="27da7-110">PowerShell running on it and the host machine</span></span>
- <span data-ttu-id="27da7-111">VSCode és a PowerShell-bővítmény VSCode-</span><span class="sxs-lookup"><span data-stu-id="27da7-111">VSCode and the PowerShell extension for VSCode</span></span>

<span data-ttu-id="27da7-112">Ez a funkció a Windows PowerShell és a PowerShell Core működik.</span><span class="sxs-lookup"><span data-stu-id="27da7-112">This feature works on Windows PowerShell and PowerShell Core.</span></span>

<span data-ttu-id="27da7-113">Ez a funkció is működik, ha egy távoli gépen a Rendszerfelügyeleti webszolgáltatások, a PowerShell Directet vagy az SSH-n keresztül csatlakozik.</span><span class="sxs-lookup"><span data-stu-id="27da7-113">This feature also works when connecting to a remote machine via WinRM, PowerShell Direct, or SSH.</span></span> <span data-ttu-id="27da7-114">Ha az SSH-val szeretne, de Windows használ, tekintse meg a [SSH Win32 verziója](https://github.com/PowerShell/Win32-OpenSSH)!</span><span class="sxs-lookup"><span data-stu-id="27da7-114">If you want to use SSH, but are using Windows, check out the [Win32 version of SSH](https://github.com/PowerShell/Win32-OpenSSH)!</span></span>

## <a name="lets-go"></a><span data-ttu-id="27da7-115">gyerünk</span><span class="sxs-lookup"><span data-stu-id="27da7-115">Let's go</span></span>

<span data-ttu-id="27da7-116">Ebben a szakaszban I fog végig távoli szerkesztése és a hibakeresést a saját MacBook Pro egy Ubuntu virtuális gép futtatása az Azure-ban.</span><span class="sxs-lookup"><span data-stu-id="27da7-116">In this section, I'll walk through remote editing and debugging from my MacBook Pro, to an Ubuntu VM running in Azure.</span></span> <span data-ttu-id="27da7-117">E nem a Windows, de **megegyezik a folyamat**.</span><span class="sxs-lookup"><span data-stu-id="27da7-117">I might not be using Windows, but **the process is identical**.</span></span>

### <a name="local-file-editing-with-open-editorfile"></a><span data-ttu-id="27da7-118">Szerkesztés az Open-EditorFile helyi fájl</span><span class="sxs-lookup"><span data-stu-id="27da7-118">Local file editing with Open-EditorFile</span></span>

<span data-ttu-id="27da7-119">A PowerShell-bővítmény a VSCode elindult, és a PowerShell integrált konzol nyitja meg, hogy írja be `Open-EditorFile foo.ps1` vagy `psedit foo.ps1` megnyitása a helyi foo.ps1 fájlt közvetlenül a szerkesztőben.</span><span class="sxs-lookup"><span data-stu-id="27da7-119">With the PowerShell extension for VSCode started and the PowerShell Integrated Console opened, we can type `Open-EditorFile foo.ps1` or `psedit foo.ps1` to open the local foo.ps1 file right in the editor.</span></span>

![Open-EditorFile foo.ps1 helyileg működik](https://user-images.githubusercontent.com/2644648/34895897-7c2c46ac-f79c-11e7-9410-a252aff52f13.png)

>[!NOTE]
> <span data-ttu-id="27da7-121">foo.ps1 már léteznie kell.</span><span class="sxs-lookup"><span data-stu-id="27da7-121">foo.ps1 must already exist.</span></span>

<span data-ttu-id="27da7-122">Itt is:</span><span class="sxs-lookup"><span data-stu-id="27da7-122">From there, we can:</span></span>

<span data-ttu-id="27da7-123">Töréspont hozzáadása a területbe ![margó a Töréspont hozzáadása](https://user-images.githubusercontent.com/2644648/34895893-7bdc38e2-f79c-11e7-8026-8ad53f9a1bad.png)</span><span class="sxs-lookup"><span data-stu-id="27da7-123">add breakpoints to the gutter ![adding breakpoint to gutter](https://user-images.githubusercontent.com/2644648/34895893-7bdc38e2-f79c-11e7-8026-8ad53f9a1bad.png)</span></span>

<span data-ttu-id="27da7-124">és nyomja le az F5 való hibakeresés a PowerShell-parancsfájlt.</span><span class="sxs-lookup"><span data-stu-id="27da7-124">and hit F5 to debug the PowerShell script.</span></span>
<span data-ttu-id="27da7-125">![a helyi PowerShell-parancsprogram-hibakeresés](https://user-images.githubusercontent.com/2644648/34895894-7bedb874-f79c-11e7-9180-7e0dc2d02af8.png)</span><span class="sxs-lookup"><span data-stu-id="27da7-125">![debugging the PowerShell local script](https://user-images.githubusercontent.com/2644648/34895894-7bedb874-f79c-11e7-9180-7e0dc2d02af8.png)</span></span>

<span data-ttu-id="27da7-126">Hibakeresés közben is együttműködhet a hibakeresési konzolt, tekintse meg a változók a bal oldalon, és hibakeresési eszközök minden más standard hatókörében.</span><span class="sxs-lookup"><span data-stu-id="27da7-126">While debugging, you can interact with the debug console, check out the variables in the scope on the left, and all the other standard debugging tools.</span></span>

### <a name="remote-file-editing-with-open-editorfile"></a><span data-ttu-id="27da7-127">Szerkesztés az Open-EditorFile távoli fájl</span><span class="sxs-lookup"><span data-stu-id="27da7-127">Remote file editing with Open-EditorFile</span></span>

<span data-ttu-id="27da7-128">Most már folytassuk a Szerkesztés és hibakeresés távoli fájlba.</span><span class="sxs-lookup"><span data-stu-id="27da7-128">Now let's get into remote file editing and debugging.</span></span> <span data-ttu-id="27da7-129">A lépések nagyjából azonosak a, igazolnia kell a kezdeti lépések – adja meg a PowerShell-munkamenetet a távoli kiszolgáló csak egy dolog van.</span><span class="sxs-lookup"><span data-stu-id="27da7-129">The steps are nearly the same, there's just one thing we need to do first - enter our PowerShell session to the remote server.</span></span>

<span data-ttu-id="27da7-130">A parancsmag van ehhez.</span><span class="sxs-lookup"><span data-stu-id="27da7-130">There's a cmdlet for to do so.</span></span> <span data-ttu-id="27da7-131">Azt nevezzük `Enter-PSSession`.</span><span class="sxs-lookup"><span data-stu-id="27da7-131">It's called `Enter-PSSession`.</span></span>

<span data-ttu-id="27da7-132">A parancsmag watered le leírását a következő:</span><span class="sxs-lookup"><span data-stu-id="27da7-132">The watered down explanation of the cmdlet is:</span></span>

- <span data-ttu-id="27da7-133">`Enter-PSSession -ComputerName foo` a WinRM-n keresztül munkamenet indítása</span><span class="sxs-lookup"><span data-stu-id="27da7-133">`Enter-PSSession -ComputerName foo` starts a session via WinRM</span></span>
- <span data-ttu-id="27da7-134">`Enter-PSSession -ContainerId foo` és `Enter-PSSession -VmId foo` keresztül a PowerShell Directet munkamenet indítása</span><span class="sxs-lookup"><span data-stu-id="27da7-134">`Enter-PSSession -ContainerId foo` and `Enter-PSSession -VmId foo` start a session via PowerShell Direct</span></span>
- <span data-ttu-id="27da7-135">`Enter-PSSession -HostName foo` SSH-kapcsolaton keresztül egy munkamenet indítása</span><span class="sxs-lookup"><span data-stu-id="27da7-135">`Enter-PSSession -HostName foo` starts a session via SSH</span></span>

<span data-ttu-id="27da7-136">További információ az `Enter-PSSession`, tekintse meg a docs [Itt](https://docs.microsoft.com/powershell/module/microsoft.powershell.core/enter-pssession?view=powershell-6).</span><span class="sxs-lookup"><span data-stu-id="27da7-136">For more info on `Enter-PSSession`, check out the docs [here](https://docs.microsoft.com/powershell/module/microsoft.powershell.core/enter-pssession?view=powershell-6).</span></span>

<span data-ttu-id="27da7-137">E fogja használni az SSH a távelérése óta egy Ubuntu virtuális gép az Azure-ban macOS rendszerről fogom.</span><span class="sxs-lookup"><span data-stu-id="27da7-137">I'll be using SSH for remoting since I'm going from macOS to an Ubuntu VM in Azure.</span></span>

<span data-ttu-id="27da7-138">Először az integrált konzol az Enter-PSSession futtassa.</span><span class="sxs-lookup"><span data-stu-id="27da7-138">First, in the Integrated Console, let's run our Enter-PSSession.</span></span> <span data-ttu-id="27da7-139">Tudni fogja, hogy használja-e a munkamenet mert `[something]` bal oldalán, az üzenet fog megjelenni.</span><span class="sxs-lookup"><span data-stu-id="27da7-139">You'll know that you're in the session because `[something]` will show up to the left of your prompt.</span></span>

![Enter-PSSession-hívás](https://user-images.githubusercontent.com/2644648/34895896-7c18e0bc-f79c-11e7-9b36-6f4bd0e9b0db.png)

<span data-ttu-id="27da7-141">Itt tehetjük a pontos lépések, ha azt egy helyi parancsfájl szerkesztése.</span><span class="sxs-lookup"><span data-stu-id="27da7-141">From there, we can do the exact steps as if we were editing a local script.</span></span>

1. <span data-ttu-id="27da7-142">Futtatás `Open-EditorFile test.ps1` vagy `psedit test.ps1` megnyitása a távoli `test.ps1` fájl ![nyílt-EditorFile test.ps1 fájl](https://user-images.githubusercontent.com/2644648/34895898-7c3e6a12-f79c-11e7-8bdf-549b591ecbcb.png)</span><span class="sxs-lookup"><span data-stu-id="27da7-142">Run `Open-EditorFile test.ps1` or `psedit test.ps1` to open the remote `test.ps1` file ![Open-EditorFile the test.ps1 file](https://user-images.githubusercontent.com/2644648/34895898-7c3e6a12-f79c-11e7-8bdf-549b591ecbcb.png)</span></span>
2. <span data-ttu-id="27da7-143">A fájl/set töréspontok szerkesztése</span><span class="sxs-lookup"><span data-stu-id="27da7-143">Edit the file/set breakpoints</span></span> ![szerkesztheti, és állítson be töréspontokat](https://user-images.githubusercontent.com/2644648/34895892-7bb68246-f79c-11e7-8c0a-c2121773afbb.png)
3. <span data-ttu-id="27da7-145">Hibakeresés (F5), a távoli fájl</span><span class="sxs-lookup"><span data-stu-id="27da7-145">Start debugging (F5) the remote file</span></span>

![a távoli fájl hibakeresés](https://user-images.githubusercontent.com/2644648/34895895-7c040782-f79c-11e7-93ea-47724fa5c10d.png)

<span data-ttu-id="27da7-147">Ez minden van rá!</span><span class="sxs-lookup"><span data-stu-id="27da7-147">That's all there's to it!</span></span> <span data-ttu-id="27da7-148">Reméljük, hogy ez az útmutató segítségével törölje a távoli hibakeresés és a PowerShell használatával a VSCode szerkesztésével kapcsolatos kérdése mentése.</span><span class="sxs-lookup"><span data-stu-id="27da7-148">We hope that this guide helped clear up any questions about remote debugging and editing PowerShell in VSCode.</span></span>

<span data-ttu-id="27da7-149">Ha bármilyen problémába ütközik, nyugodtan megnyithat problémákat [a GitHub-adattárat a](http://github.com/powershell/vscode-powershell).</span><span class="sxs-lookup"><span data-stu-id="27da7-149">If you have any problems, feel free to open issues [on the GitHub repo](http://github.com/powershell/vscode-powershell).</span></span>
