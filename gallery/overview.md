---
ms.date: 06/12/2017
contributor: JKeithB
keywords: katalógus, powershell, a parancsmag, psgallery, psget
title: A PowerShell-galéria
ms.openlocfilehash: d3e3b9d8bb3d6cefd3a3bfe79b012bb1dc1d8a2d
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55685458"
---
# <a name="the-powershell-gallery"></a><span data-ttu-id="f485a-103">A PowerShell-galéria</span><span class="sxs-lookup"><span data-stu-id="f485a-103">The PowerShell Gallery</span></span>

<span data-ttu-id="f485a-104">A PowerShell-galériából a PowerShell-tartalmak központi adattára.</span><span class="sxs-lookup"><span data-stu-id="f485a-104">The PowerShell Gallery is the central repository for PowerShell content.</span></span> <span data-ttu-id="f485a-105">A PowerShell-parancsok és a Desired State Configuration (DSC) erőforrásokat tartalmazó hasznos PowerShell-modulok is megtalálhatja.</span><span class="sxs-lookup"><span data-stu-id="f485a-105">In it, you can find useful PowerShell modules containing PowerShell commands and Desired State Configuration (DSC) resources.</span></span>
<span data-ttu-id="f485a-106">PowerShell-parancsfájlok, amelyek előfordulhat, hogy tartalmazza a PowerShell-munkafolyamatokkal, és amely szerkezeti feladatokhoz, és adja meg ezeket a feladatokat az alkalmazás-előkészítés is megtalálhatja.</span><span class="sxs-lookup"><span data-stu-id="f485a-106">You can also find PowerShell scripts, some of which may contain PowerShell workflows, and which outline a set of tasks and provide sequencing for those tasks.</span></span> <span data-ttu-id="f485a-107">Néhány ezeket a csomagokat a Microsoft által lett létrehozva, és mások vannak a PowerShell-Közösség által készített.</span><span class="sxs-lookup"><span data-stu-id="f485a-107">Some of these packages are authored by Microsoft, and others are authored by the PowerShell community.</span></span>

## <a name="powershellget-overview"></a><span data-ttu-id="f485a-108">A PowerShellGet áttekintése</span><span class="sxs-lookup"><span data-stu-id="f485a-108">PowerShellGet Overview</span></span>

<span data-ttu-id="f485a-109">A PowerShellGet modul felderítése, telepítése, frissítése és PowerShell csomagok, amely tartalmazza azokat az összetevőket, például a modulok, a DSC-erőforrások, a szerepköri funkciók és a parancsfájlok közzétételéhez szükséges parancsmagokat tartalmazza a [PowerShell-galériából](https://www.PowerShellGallery.com)és más privát tárházakban.</span><span class="sxs-lookup"><span data-stu-id="f485a-109">The PowerShellGet module contains cmdlets for discovering, installing, updating and publishing PowerShell packages which contain artifacts such as Modules, DSC Resources, Role Capabilities and Scripts from the [PowerShell Gallery](https://www.PowerShellGallery.com) and other private repositories.</span></span>

## <a name="getting-started-with-the-gallery"></a><span data-ttu-id="f485a-110">A katalógus – első lépések</span><span class="sxs-lookup"><span data-stu-id="f485a-110">Getting Started with the Gallery</span></span>

<span data-ttu-id="f485a-111">A PowerShellGet-modul legújabb verzióját a katalógusból csomagok telepítése szükséges.</span><span class="sxs-lookup"><span data-stu-id="f485a-111">Installing packages from the Gallery requires the latest version of the PowerShellGet module.</span></span>
<span data-ttu-id="f485a-112">Lásd: [PowerShellGet telepítése](installing-psget.md) részletes utasításokért.</span><span class="sxs-lookup"><span data-stu-id="f485a-112">See [Installing PowerShellGet](installing-psget.md) for complete instructions.</span></span>

<span data-ttu-id="f485a-113">Tekintse meg a [bevezetés](getting-started.md) további tudnivalókat a PowerShellGet-parancsok használata a katalógusban.</span><span class="sxs-lookup"><span data-stu-id="f485a-113">Check out the [Getting Started](getting-started.md) page for more information on how to use PowerShellGet commands with the Gallery.</span></span> <span data-ttu-id="f485a-114">Futtathat *Update-Help-Module PowerShellGet* ezekkel a parancsokkal a helyi súgó telepítése.</span><span class="sxs-lookup"><span data-stu-id="f485a-114">You can also run *Update-Help -Module PowerShellGet* to install local help for these commands.</span></span>

## <a name="supported-operating-systems"></a><span data-ttu-id="f485a-115">A támogatott operációs rendszerek</span><span class="sxs-lookup"><span data-stu-id="f485a-115">Supported Operating Systems</span></span>

<span data-ttu-id="f485a-116">A **PowerShellGet** modulhoz szükséges **Windows PowerShell 3.0-s vagy újabb**, vagy **a PowerShell Core 6.0-s vagy újabb**.</span><span class="sxs-lookup"><span data-stu-id="f485a-116">The **PowerShellGet** module requires **Windows PowerShell 3.0 or newer**, or **PowerShell Core 6.0 or newer**.</span></span>

<span data-ttu-id="f485a-117">Egy megfelelő verziója **Windows PowerShell** ezen operációs rendszerekhez érhető el:</span><span class="sxs-lookup"><span data-stu-id="f485a-117">A suitable version of **Windows PowerShell** is available for these operating systems:</span></span>

- <span data-ttu-id="f485a-118">Windows 10</span><span class="sxs-lookup"><span data-stu-id="f485a-118">Windows 10</span></span>
- <span data-ttu-id="f485a-119">Windows 8.1 Pro</span><span class="sxs-lookup"><span data-stu-id="f485a-119">Windows 8.1 Pro</span></span>
- <span data-ttu-id="f485a-120">Windows 8.1 Enterprise</span><span class="sxs-lookup"><span data-stu-id="f485a-120">Windows 8.1 Enterprise</span></span>
- <span data-ttu-id="f485a-121">Windows 7 SP1</span><span class="sxs-lookup"><span data-stu-id="f485a-121">Windows 7 SP1</span></span>
- <span data-ttu-id="f485a-122">Windows Server 2019</span><span class="sxs-lookup"><span data-stu-id="f485a-122">Windows Server 2019</span></span>
- <span data-ttu-id="f485a-123">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="f485a-123">Windows Server 2016</span></span>
- <span data-ttu-id="f485a-124">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="f485a-124">Windows Server 2012 R2</span></span>
- <span data-ttu-id="f485a-125">Windows Server 2008 R2 SP1</span><span class="sxs-lookup"><span data-stu-id="f485a-125">Windows Server 2008 R2 SP1</span></span>

<span data-ttu-id="f485a-126">**A PowerShellGet** szükséges a .NET-keretrendszer 4.5 vagy újabb.</span><span class="sxs-lookup"><span data-stu-id="f485a-126">**PowerShellGet** requires .NET Framework 4.5 or above.</span></span> <span data-ttu-id="f485a-127">Telepítheti a .NET-keretrendszer 4.5 vagy újabb a [Itt](https://msdn.microsoft.com/library/5a4x27ek.aspx).</span><span class="sxs-lookup"><span data-stu-id="f485a-127">You can install .NET Framework 4.5 or above from [here](https://msdn.microsoft.com/library/5a4x27ek.aspx).</span></span>

<span data-ttu-id="f485a-128">Mivel **a PowerShell Core** platformfüggetlen és, hogy azt jelenti, hogy a Windows, Linux és MacOS rendszeren működik, amely is lehetővé teszi, **PowerShellGet** ezeket rendszereken érhető el.</span><span class="sxs-lookup"><span data-stu-id="f485a-128">Since **PowerShell Core** is cross-platform and that means it works on Windows, Linux and MacOS, that also makes **PowerShellGet** available on those systems.</span></span> <span data-ttu-id="f485a-129">Által támogatott rendszerek teljes listáját **a PowerShell Core** lásd [PowerShell telepítése](/powershell/scripting/setup/installing-powershell).</span><span class="sxs-lookup"><span data-stu-id="f485a-129">For a full list of systems supported by **PowerShell Core** see [Installing PowerShell](/powershell/scripting/setup/installing-powershell).</span></span>

<span data-ttu-id="f485a-130">A tárban lévő üzemeltetett számos modulok támogatják a különböző OSE-kre, és a további követelményeket támasztanak.</span><span class="sxs-lookup"><span data-stu-id="f485a-130">Many modules hosted in the gallery will support different OSes and have additional requirements.</span></span> <span data-ttu-id="f485a-131">Tekintse meg a modulok további információt a dokumentációban.</span><span class="sxs-lookup"><span data-stu-id="f485a-131">Please refer to the documentation for the modules for more information.</span></span>

## <a name="got-a-question-have-feedback"></a><span data-ttu-id="f485a-132">Kérdése van?</span><span class="sxs-lookup"><span data-stu-id="f485a-132">Got a question?</span></span> <span data-ttu-id="f485a-133">Visszajelzés küldene?</span><span class="sxs-lookup"><span data-stu-id="f485a-133">Have feedback?</span></span>

<span data-ttu-id="f485a-134">További információ a PowerShell-galéria és a PowerShellGet megtalálható a [bevezetés](getting-started.md) lap.</span><span class="sxs-lookup"><span data-stu-id="f485a-134">More information about the PowerShell Gallery and PowerShellGet can be found in the [Getting Started](getting-started.md) page.</span></span> <span data-ttu-id="f485a-135">Adja meg a visszajelzések és a jelentés kapcsolatos problémákat [UserVoice](http://windowsserver.uservoice.com/forums/301869-powershell).</span><span class="sxs-lookup"><span data-stu-id="f485a-135">Please provide feedback and report issues using [UserVoice](http://windowsserver.uservoice.com/forums/301869-powershell).</span></span>
