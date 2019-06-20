---
title: Windows PowerShell fogalmak |} A Microsoft Docs
ms.custom: ''
ms.date: 6/12/2019
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 3dd5608e-50b6-4c6a-aee3-dde0e86032bc
caps.latest.revision: 7
ms.openlocfilehash: 4410b1f9c80afefd5479fa68154f9947b805edcf
ms.sourcegitcommit: 13f24786ed39ca1c07eff2b73a1974c366e31cb8
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/19/2019
ms.locfileid: "67263859"
---
# <a name="windows-powershell-concepts"></a><span data-ttu-id="992e5-102">Windows PowerShell – Fogalmak</span><span class="sxs-lookup"><span data-stu-id="992e5-102">Windows PowerShell Concepts</span></span>

<span data-ttu-id="992e5-103">Ez a szakasz tartalmazza, amely segít megérteni a PowerShell egy fejlesztői szempontból elméleti információk.</span><span class="sxs-lookup"><span data-stu-id="992e5-103">This section contains conceptual information that will help you understand PowerShell from a developer's viewpoint.</span></span>

|<span data-ttu-id="992e5-104">Témakör neve</span><span class="sxs-lookup"><span data-stu-id="992e5-104">Topic Name</span></span>|<span data-ttu-id="992e5-105">Leírás</span><span class="sxs-lookup"><span data-stu-id="992e5-105">Description</span></span>|
|----------------|-----------------|
|[<span data-ttu-id="992e5-106">about_Objects</span><span class="sxs-lookup"><span data-stu-id="992e5-106">about_Objects</span></span>](/powershell/module/microsoft.powershell.core/about/about_objects)|<span data-ttu-id="992e5-107">PowerShell-objektumok leírása.</span><span class="sxs-lookup"><span data-stu-id="992e5-107">Description of PowerShell objects.</span></span> <span data-ttu-id="992e5-108">További információkért lásd: [objektum létrehozása](/powershell/module/microsoft.powershell.core/about/about_object_creation)</span><span class="sxs-lookup"><span data-stu-id="992e5-108">For more information, see [About Object Creation](/powershell/module/microsoft.powershell.core/about/about_object_creation)</span></span>|
|[<span data-ttu-id="992e5-109">Futási terek létrehozása</span><span class="sxs-lookup"><span data-stu-id="992e5-109">Creating Runspaces</span></span>](../hosting/creating-runspaces.md)|<span data-ttu-id="992e5-110">A működési környezetek, ahol parancsok feldolgozása.</span><span class="sxs-lookup"><span data-stu-id="992e5-110">The operating environments where commands are processed.</span></span> <span data-ttu-id="992e5-111">További információkért lásd: [futási térben osztály](/dotnet/api/system.management.automation.runspaces.runspace).</span><span class="sxs-lookup"><span data-stu-id="992e5-111">For more information, see [Runspace Class](/dotnet/api/system.management.automation.runspaces.runspace).</span></span>|
|[<span data-ttu-id="992e5-112">Kimeneti objektumok kiterjesztése</span><span class="sxs-lookup"><span data-stu-id="992e5-112">Extending Output Objects</span></span>](../cmdlet/extending-output-objects.md)|<span data-ttu-id="992e5-113">Hogyan bővítheti a PowerShell-objektumok.</span><span class="sxs-lookup"><span data-stu-id="992e5-113">How to extend PowerShell objects.</span></span> <span data-ttu-id="992e5-114">További információkért lásd: [kapcsolatos Types.ps1xml](/powershell/module/microsoft.powershell.core/about/about_types.ps1xml)</span><span class="sxs-lookup"><span data-stu-id="992e5-114">For more information, see [About Types.ps1xml](/powershell/module/microsoft.powershell.core/about/about_types.ps1xml)</span></span>|
|[<span data-ttu-id="992e5-115">Parancsmagok regisztrálása</span><span class="sxs-lookup"><span data-stu-id="992e5-115">Registering Cmdlets</span></span>](../cmdlet/registering-cmdlets.md)|<span data-ttu-id="992e5-116">Hogyan modul és beépülő modulokat a PowerShell elérhetővé tenni.</span><span class="sxs-lookup"><span data-stu-id="992e5-116">How to make modules and snap-ins available in PowerShell.</span></span> <span data-ttu-id="992e5-117">További információkért lásd: [modul és beépülő modulok](../cmdlet/modules-and-snap-ins.md).</span><span class="sxs-lookup"><span data-stu-id="992e5-117">For more information, see [Modules and Snap-ins](../cmdlet/modules-and-snap-ins.md).</span></span>|
|[<span data-ttu-id="992e5-118">Jóváhagyás kérése a parancsmagok</span><span class="sxs-lookup"><span data-stu-id="992e5-118">Requesting Confirmation from Cmdlets</span></span>](../cmdlet/requesting-confirmation-from-cmdlets.md)|<span data-ttu-id="992e5-119">Hogyan parancsmagok és szolgáltatók visszajelzés kérése a felhasználótól, mielőtt egy műveletet.</span><span class="sxs-lookup"><span data-stu-id="992e5-119">How cmdlets and providers request feedback from the user before an action is taken.</span></span>|
|[<span data-ttu-id="992e5-120">RuntimeDefinedParameter osztályban</span><span class="sxs-lookup"><span data-stu-id="992e5-120">RuntimeDefinedParameter Class</span></span>](/dotnet/api/system.management.automation.runtimedefinedparameter)|<span data-ttu-id="992e5-121">Futásidejű paraméterdeklaráció.</span><span class="sxs-lookup"><span data-stu-id="992e5-121">Runtime parameter declarations.</span></span>|
|[<span data-ttu-id="992e5-122">System.Management.Automation Namespace</span><span class="sxs-lookup"><span data-stu-id="992e5-122">System.Management.Automation Namespace</span></span>](/dotnet/api/System.Management.Automation)|<span data-ttu-id="992e5-123">PowerShell API-névtérre áttekintése.</span><span class="sxs-lookup"><span data-stu-id="992e5-123">Overview of PowerShell API namespaces.</span></span>|
|[<span data-ttu-id="992e5-124">Windows PowerShell-szolgáltató áttekintése</span><span class="sxs-lookup"><span data-stu-id="992e5-124">Windows PowerShell Provider Overview</span></span>](../provider/windows-powershell-provider-overview.md)|<span data-ttu-id="992e5-125">Tárolja az adatok elérésére használt PowerShell-szolgáltatók áttekintése.</span><span class="sxs-lookup"><span data-stu-id="992e5-125">Overview about PowerShell providers that are used to access data stores.</span></span>|
|[<span data-ttu-id="992e5-126">PowerShell-parancsmagok súgójának írása</span><span class="sxs-lookup"><span data-stu-id="992e5-126">Writing Help for PowerShell Cmdlets</span></span>](../help/writing-help-for-windows-powershell-cmdlets.md)|<span data-ttu-id="992e5-127">Hogyan írhat a PowerShell-parancsmag súgójában.</span><span class="sxs-lookup"><span data-stu-id="992e5-127">How to write PowerShell cmdlet Help.</span></span>|

## <a name="see-also"></a><span data-ttu-id="992e5-128">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="992e5-128">See also</span></span>

[<span data-ttu-id="992e5-129">PowerShell-osztály</span><span class="sxs-lookup"><span data-stu-id="992e5-129">PowerShell Class</span></span>](/dotnet/api/system.management.automation.powershell)

[<span data-ttu-id="992e5-130">PowerShell Core API-referencia</span><span class="sxs-lookup"><span data-stu-id="992e5-130">PowerShell Core API Reference</span></span>](/dotnet/api/?view=pscore-6.2.0)

[<span data-ttu-id="992e5-131">Windows PowerShell programozói útmutató</span><span class="sxs-lookup"><span data-stu-id="992e5-131">Windows PowerShell Programmer's Guide</span></span>](windows-powershell-programmer-s-guide.md)

[<span data-ttu-id="992e5-132">Windows PowerShell-modulok súgó írása</span><span class="sxs-lookup"><span data-stu-id="992e5-132">Writing Help for Windows PowerShell Modules</span></span>](../module/writing-help-for-windows-powershell-modules.md)

[<span data-ttu-id="992e5-133">A Windows Powershell-szolgáltató írása</span><span class="sxs-lookup"><span data-stu-id="992e5-133">Writing a Windows Powershell Provider</span></span>](../provider/writing-a-windows-powershell-provider.md)

[<span data-ttu-id="992e5-134">Windows PowerShell API-referencia</span><span class="sxs-lookup"><span data-stu-id="992e5-134">Windows PowerShell API Reference</span></span>](/dotnet/api/?view=powershellsdk-1.1.0)

[<span data-ttu-id="992e5-135">Windows PowerShell-referencia</span><span class="sxs-lookup"><span data-stu-id="992e5-135">Windows PowerShell Reference</span></span>](../windows-powershell-reference.md)