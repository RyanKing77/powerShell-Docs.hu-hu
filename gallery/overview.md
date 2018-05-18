---
ms.date: 06/12/2017
contributor: JKeithB
keywords: gyűjtemény, powershell, a parancsmag, psgallery, psget
title: A PowerShell-galériában
ms.openlocfilehash: 65e0c427310ac20621109a6620e926a7894cf8f8
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/16/2018
---
# <a name="the-powershell-gallery"></a><span data-ttu-id="4fb25-103">A PowerShell-galériában</span><span class="sxs-lookup"><span data-stu-id="4fb25-103">The PowerShell Gallery</span></span>

<span data-ttu-id="4fb25-104">A PowerShell-galériában PowerShell tartalom központi tárháza.</span><span class="sxs-lookup"><span data-stu-id="4fb25-104">The PowerShell Gallery is the central repository for PowerShell content.</span></span> <span data-ttu-id="4fb25-105">Az oktatóanyagban található PowerShell-parancsokat és a kívánt állapot konfigurációs szolgáltatása (DSC) erőforrásokat tartalmazó hasznos PowerShell-modulok.</span><span class="sxs-lookup"><span data-stu-id="4fb25-105">In it, you can find useful PowerShell modules containing PowerShell commands and Desired State Configuration (DSC) resources.</span></span>
<span data-ttu-id="4fb25-106">PowerShell-parancsfájlok, amelyek PowerShell-munkafolyamatok, és amely szerkezeti feladatokhoz és tartalmazhat adja meg a műveleti sorrend a ezeket a feladatokat is tájékozódhat.</span><span class="sxs-lookup"><span data-stu-id="4fb25-106">You can also find PowerShell scripts, some of which may contain PowerShell workflows, and which outline a set of tasks and provide sequencing for those tasks.</span></span> <span data-ttu-id="4fb25-107">Ezek az elemek egy része felhasználók a Microsoft által készített, és más felhasználók által a PowerShell közösségi készített.</span><span class="sxs-lookup"><span data-stu-id="4fb25-107">Some of these items are authored by Microsoft, and others are authored by the PowerShell community.</span></span>

## <a name="powershellget-overview"></a><span data-ttu-id="4fb25-108">PowerShellGet áttekintése</span><span class="sxs-lookup"><span data-stu-id="4fb25-108">PowerShellGet Overview</span></span>

<span data-ttu-id="4fb25-109">A PowerShellGet modul tartalmaz parancsmagokat a felderítése, telepítése, frissítése és PowerShell összetevők, például a modulok, a DSC-erőforrások, a szerepkör képességek és a parancsfájlokat a közzététel a [PowerShell-galériában](https://www.PowerShellGallery.com) és egyéb magánhálózatokon tárházak találhatók.</span><span class="sxs-lookup"><span data-stu-id="4fb25-109">The PowerShellGet module contains cmdlets for discovering, installing, updating and publishing PowerShell artifacts such as Modules, DSC Resources, Role Capabilities and Scripts from the [PowerShell Gallery](https://www.PowerShellGallery.com) and other private repositories.</span></span>

## <a name="getting-started-with-the-gallery"></a><span data-ttu-id="4fb25-110">A gyűjtemény első lépések</span><span class="sxs-lookup"><span data-stu-id="4fb25-110">Getting Started with the Gallery</span></span>

<span data-ttu-id="4fb25-111">Elemet a gyűjteményből telepítéséhez a PowerShellGet modul legújabb verzióját.</span><span class="sxs-lookup"><span data-stu-id="4fb25-111">Installing items from the Gallery requires the latest version of the PowerShellGet module.</span></span>
<span data-ttu-id="4fb25-112">Lásd: [telepítése PowerShellGet](installing-psget.md) részletes utasításokért.</span><span class="sxs-lookup"><span data-stu-id="4fb25-112">See [Installing PowerShellGet](installing-psget.md) for complete instructions.</span></span>

<span data-ttu-id="4fb25-113">Tekintse meg a [bevezetés](getting-started.md) oldalon olvashat PowerShellGet parancsok használata a gyűjteményben.</span><span class="sxs-lookup"><span data-stu-id="4fb25-113">Check out the [Getting Started](getting-started.md) page for more information on how to use PowerShellGet commands with the Gallery.</span></span> <span data-ttu-id="4fb25-114">Is futtathatja *Update-Help-modul PowerShellGet* parancsok helyi súgó telepítése.</span><span class="sxs-lookup"><span data-stu-id="4fb25-114">You can also run *Update-Help -Module PowerShellGet* to install local help for these commands.</span></span>

## <a name="supported-operating-systems"></a><span data-ttu-id="4fb25-115">Támogatott operációs rendszerek</span><span class="sxs-lookup"><span data-stu-id="4fb25-115">Supported Operating Systems</span></span>

<span data-ttu-id="4fb25-116">A **PowerShellGet** module használatához **PowerShell 3.0-s vagy újabb**.</span><span class="sxs-lookup"><span data-stu-id="4fb25-116">The **PowerShellGet** module requires **PowerShell 3.0 or newer**.</span></span>

<span data-ttu-id="4fb25-117">Ezért **PowerShellGet** a következő operációs rendszerek egyike szükséges:</span><span class="sxs-lookup"><span data-stu-id="4fb25-117">Therefore, **PowerShellGet** requires one of the following operating systems:</span></span>

- <span data-ttu-id="4fb25-118">Windows-10</span><span class="sxs-lookup"><span data-stu-id="4fb25-118">Windows 10</span></span>
- <span data-ttu-id="4fb25-119">Windows 8.1 Pro</span><span class="sxs-lookup"><span data-stu-id="4fb25-119">Windows 8.1 Pro</span></span>
- <span data-ttu-id="4fb25-120">Windows 8.1 Enterprise</span><span class="sxs-lookup"><span data-stu-id="4fb25-120">Windows 8.1 Enterprise</span></span>
- <span data-ttu-id="4fb25-121">Windows 7 SP1</span><span class="sxs-lookup"><span data-stu-id="4fb25-121">Windows 7 SP1</span></span>
- <span data-ttu-id="4fb25-122">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="4fb25-122">Windows Server 2016</span></span>
- <span data-ttu-id="4fb25-123">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="4fb25-123">Windows Server 2012 R2</span></span>
- <span data-ttu-id="4fb25-124">Windows Server 2008 R2 SP1</span><span class="sxs-lookup"><span data-stu-id="4fb25-124">Windows Server 2008 R2 SP1</span></span>

<span data-ttu-id="4fb25-125">**PowerShellGet** is szükséges a .NET-keretrendszer 4.5 vagy újabb.</span><span class="sxs-lookup"><span data-stu-id="4fb25-125">**PowerShellGet** also requires .NET Framework 4.5 or above.</span></span> <span data-ttu-id="4fb25-126">Telepítheti a .NET-keretrendszer 4.5 vagy újabb a [Itt](https://msdn.microsoft.com/library/5a4x27ek.aspx).</span><span class="sxs-lookup"><span data-stu-id="4fb25-126">You can install .NET Framework 4.5 or above from [here](https://msdn.microsoft.com/library/5a4x27ek.aspx).</span></span>

## <a name="got-a-question-have-feedback"></a><span data-ttu-id="4fb25-127">A kapott a következő kérdést?</span><span class="sxs-lookup"><span data-stu-id="4fb25-127">Got a question?</span></span> <span data-ttu-id="4fb25-128">Van?</span><span class="sxs-lookup"><span data-stu-id="4fb25-128">Have feedback?</span></span>

<span data-ttu-id="4fb25-129">További információ a PowerShell-galériában és PowerShellGet megtalálhatók a [bevezetés](getting-started.md) lap.</span><span class="sxs-lookup"><span data-stu-id="4fb25-129">More information about the PowerShell Gallery and PowerShellGet can be found in the [Getting Started](getting-started.md) page.</span></span> <span data-ttu-id="4fb25-130">Adja meg a visszajelzések és a jelentés kapcsolatos problémákat [UserVoice](http://windowsserver.uservoice.com/forums/301869-powershell).</span><span class="sxs-lookup"><span data-stu-id="4fb25-130">Please provide feedback and report issues using [UserVoice](http://windowsserver.uservoice.com/forums/301869-powershell).</span></span>