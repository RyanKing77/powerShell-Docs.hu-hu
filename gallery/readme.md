---
ms.date: 06/12/2017
contributor: JKeithB
ms.topic: conceptual
keywords: gyűjtemény, powershell, a parancsmag, psgallery, psget
title: A PowerShell-galériában
ms.openlocfilehash: 9519b8bcca9f43419a33db380c3b852e9bb354ac
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="the-powershell-gallery"></a><span data-ttu-id="73dbb-103">A PowerShell-galériában</span><span class="sxs-lookup"><span data-stu-id="73dbb-103">The PowerShell Gallery</span></span>

<span data-ttu-id="73dbb-104">A PowerShell-galériában PowerShell tartalom központi tárháza.</span><span class="sxs-lookup"><span data-stu-id="73dbb-104">The PowerShell Gallery is the central repository for PowerShell content.</span></span> <span data-ttu-id="73dbb-105">Új PowerShell-parancsok vagy a kívánt állapot konfigurációs szolgáltatása (DSC) erőforrások a gyűjteményben található.</span><span class="sxs-lookup"><span data-stu-id="73dbb-105">You can find new PowerShell commands or Desired State Configuration (DSC) resources in the Gallery.</span></span>

## <a name="powershellget-overview"></a><span data-ttu-id="73dbb-106">PowerShellGet áttekintése</span><span class="sxs-lookup"><span data-stu-id="73dbb-106">PowerShellGet Overview</span></span>

<span data-ttu-id="73dbb-107">A PowerShellGet modul tartalmaz parancsmagokat a felderítése, telepítése, frissítése és PowerShell összetevők, például a modulok, a DSC-erőforrások, a szerepkör képességek és a parancsfájlokat a közzététel a [PowerShell-galériában](https://www.PowerShellGallery.com) és egyéb magánhálózatokon tárházak találhatók.</span><span class="sxs-lookup"><span data-stu-id="73dbb-107">The PowerShellGet module contains cmdlets for discovering, installing, updating and publishing PowerShell artifacts such as Modules, DSC Resources, Role Capabilities and Scripts from the [PowerShell Gallery](https://www.PowerShellGallery.com) and other private repositories.</span></span>

## <a name="getting-started-with-the-gallery"></a><span data-ttu-id="73dbb-108">A gyűjtemény első lépések</span><span class="sxs-lookup"><span data-stu-id="73dbb-108">Getting Started with the Gallery</span></span>

<span data-ttu-id="73dbb-109">Elemet a gyűjteményből telepítéséhez a PowerShellGet modul, amely megtalálható a Windows 10, Windows Management Framework (WMF) 5.0 vagy az MSI-alapú telepítő (a PowerShell 3. és 4) a legújabb verzióra.</span><span class="sxs-lookup"><span data-stu-id="73dbb-109">Installing items from the Gallery requires the latest version of the PowerShellGet module, which is available in Windows 10, in Windows Management Framework (WMF) 5.0, or in the MSI-based installer (for PowerShell 3 and 4).</span></span>

- <span data-ttu-id="73dbb-110">[**Windows 10 beolvasása**](http://go.microsoft.com/fwlink/?LinkID=624830&clcid=0x409),</span><span class="sxs-lookup"><span data-stu-id="73dbb-110">[**Get Windows 10**](http://go.microsoft.com/fwlink/?LinkID=624830&clcid=0x409),</span></span>
- <span data-ttu-id="73dbb-111">[**WMF 5.0 beolvasása**](http://go.microsoft.com/fwlink/?LinkId=398175), vagy</span><span class="sxs-lookup"><span data-stu-id="73dbb-111">[**Get WMF 5.0**](http://go.microsoft.com/fwlink/?LinkId=398175), or</span></span>
- [<span data-ttu-id="73dbb-112">**Az MSI telepítő beolvasása**</span><span class="sxs-lookup"><span data-stu-id="73dbb-112">**Get MSI Installer**</span></span>](http://go.microsoft.com/fwlink/?LinkID=746217&clcid=0x409)

<span data-ttu-id="73dbb-113">A legújabb [PowerShellGet](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409) modulban is:</span><span class="sxs-lookup"><span data-stu-id="73dbb-113">With the latest [PowerShellGet](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409) module, you can:</span></span>

-   <span data-ttu-id="73dbb-114">A gyűjtemény elemeinek keresztül keresési [keresés-modul](https://go.microsoft.com/fwlink/?LinkId=821658) és [keresés-parancsfájl](https://go.microsoft.com/fwlink/?LinkId=822322)</span><span class="sxs-lookup"><span data-stu-id="73dbb-114">Search through items in the Gallery with [Find-Module](https://go.microsoft.com/fwlink/?LinkId=821658) and [Find-Script](https://go.microsoft.com/fwlink/?LinkId=822322)</span></span>
-   <span data-ttu-id="73dbb-115">A rendszer a gyűjteményből elemek mentése [mentés-modul](https://go.microsoft.com/fwlink/?LinkId=821669) és [mentés-parancsfájl](https://go.microsoft.com/fwlink/?LinkId=822334)</span><span class="sxs-lookup"><span data-stu-id="73dbb-115">Save items to your system from the Gallery with [Save-Module](https://go.microsoft.com/fwlink/?LinkId=821669) and [Save-Script](https://go.microsoft.com/fwlink/?LinkId=822334)</span></span>
-   <span data-ttu-id="73dbb-116">A gyűjtemény elemeinek telepítéséhez [Install-modul](https://go.microsoft.com/fwlink/?LinkId=821663) és [telepítési-parancsfájl](https://go.microsoft.com/fwlink/?LinkId=822327)</span><span class="sxs-lookup"><span data-stu-id="73dbb-116">Install items from the Gallery with [Install-Module](https://go.microsoft.com/fwlink/?LinkId=821663) and [Install-Script](https://go.microsoft.com/fwlink/?LinkId=822327)</span></span>
-   <span data-ttu-id="73dbb-117">Elemek feltöltése a gyűjteményébe [Publish-modul](https://go.microsoft.com/fwlink/?LinkId=821666) és [Publish-parancsfájl](https://go.microsoft.com/fwlink/?LinkId=822331)</span><span class="sxs-lookup"><span data-stu-id="73dbb-117">Upload items to the Gallery with [Publish-Module](https://go.microsoft.com/fwlink/?LinkId=821666) and [Publish-Script](https://go.microsoft.com/fwlink/?LinkId=822331)</span></span>
-   <span data-ttu-id="73dbb-118">Adja hozzá a saját egyéni tárház [Register-PSRepository](https://go.microsoft.com/fwlink/?LinkId=821668)</span><span class="sxs-lookup"><span data-stu-id="73dbb-118">Add your own custom repository with [Register-PSRepository](https://go.microsoft.com/fwlink/?LinkId=821668)</span></span>

<span data-ttu-id="73dbb-119">Tekintse meg a [bevezetés](psgallery/psgallery_gettingstarted.md) oldalon olvashat PowerShellGet parancsok használata a gyűjteményben.</span><span class="sxs-lookup"><span data-stu-id="73dbb-119">Check out the [Getting Started](psgallery/psgallery_gettingstarted.md) page for more information on how to use PowerShellGet commands with the Gallery.</span></span> <span data-ttu-id="73dbb-120">Is futtathatja *Update-Help-modul PowerShellGet* parancsok helyi súgó telepítése.</span><span class="sxs-lookup"><span data-stu-id="73dbb-120">You can also run *Update-Help -Module PowerShellGet* to install local help for these commands.</span></span>

## <a name="supported-operating-systems"></a><span data-ttu-id="73dbb-121">Támogatott operációs rendszerek</span><span class="sxs-lookup"><span data-stu-id="73dbb-121">Supported Operating Systems</span></span>

<span data-ttu-id="73dbb-122">A **PowerShellGet** module használatához **PowerShell 3.0-s vagy újabb**.</span><span class="sxs-lookup"><span data-stu-id="73dbb-122">The **PowerShellGet** module requires **PowerShell 3.0 or newer**.</span></span>

<span data-ttu-id="73dbb-123">Ezért **PowerShellGet** a következő operációs rendszerek egyike szükséges:</span><span class="sxs-lookup"><span data-stu-id="73dbb-123">Therefore, **PowerShellGet** requires one of the following operating systems:</span></span>

- <span data-ttu-id="73dbb-124">Windows-10</span><span class="sxs-lookup"><span data-stu-id="73dbb-124">Windows 10</span></span>
- <span data-ttu-id="73dbb-125">Windows 8.1 Pro</span><span class="sxs-lookup"><span data-stu-id="73dbb-125">Windows 8.1 Pro</span></span>
- <span data-ttu-id="73dbb-126">Windows 8.1 Enterprise</span><span class="sxs-lookup"><span data-stu-id="73dbb-126">Windows 8.1 Enterprise</span></span>
- <span data-ttu-id="73dbb-127">Windows 7 SP1</span><span class="sxs-lookup"><span data-stu-id="73dbb-127">Windows 7 SP1</span></span>
- <span data-ttu-id="73dbb-128">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="73dbb-128">Windows Server 2016</span></span>
- <span data-ttu-id="73dbb-129">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="73dbb-129">Windows Server 2012 R2</span></span>
- <span data-ttu-id="73dbb-130">Windows Server 2008 R2 SP1</span><span class="sxs-lookup"><span data-stu-id="73dbb-130">Windows Server 2008 R2 SP1</span></span>

<span data-ttu-id="73dbb-131">**PowerShellGet** is szükséges a .NET-keretrendszer 4.5 vagy újabb.</span><span class="sxs-lookup"><span data-stu-id="73dbb-131">**PowerShellGet** also  requires .NET Framework 4.5 or above.</span></span> <span data-ttu-id="73dbb-132">Telepítheti a .NET-keretrendszer 4.5 vagy újabb a [Itt](https://msdn.microsoft.com/library/5a4x27ek.aspx).</span><span class="sxs-lookup"><span data-stu-id="73dbb-132">You can install .NET Framework 4.5 or above from [here](https://msdn.microsoft.com/library/5a4x27ek.aspx).</span></span>


## <a name="got-a-question-have-feedback"></a><span data-ttu-id="73dbb-133">A kapott a következő kérdést?</span><span class="sxs-lookup"><span data-stu-id="73dbb-133">Got a question?</span></span> <span data-ttu-id="73dbb-134">Van?</span><span class="sxs-lookup"><span data-stu-id="73dbb-134">Have feedback?</span></span>

<span data-ttu-id="73dbb-135">További információ a PowerShell-galériában és PowerShellGet megtalálhatók a [bevezetés](psgallery/psgallery_gettingstarted.md) lap.</span><span class="sxs-lookup"><span data-stu-id="73dbb-135">More information about the PowerShell Gallery and PowerShellGet can be found in the [Getting Started](psgallery/psgallery_gettingstarted.md) page.</span></span> <span data-ttu-id="73dbb-136">Adja meg a visszajelzések és a jelentés kapcsolatos problémákat [UserVoice](http://windowsserver.uservoice.com/forums/301869-powershell).</span><span class="sxs-lookup"><span data-stu-id="73dbb-136">Please provide feedback and report issues using [UserVoice](http://windowsserver.uservoice.com/forums/301869-powershell).</span></span>