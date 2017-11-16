---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "WMF, a powershell, a beállítása"
ms.openlocfilehash: 668a5b20add58ff5e23f35d6cebddc39c64ce926
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2017
---
# <a name="installation-instructions"></a><span data-ttu-id="75595-102">Telepítési utasításokat</span><span class="sxs-lookup"><span data-stu-id="75595-102">Installation Instructions</span></span>

<span data-ttu-id="75595-103">Töltse le az operációs rendszer és az architektúra a megfelelő csomag:</span><span class="sxs-lookup"><span data-stu-id="75595-103">Download the correct package for your operating system and architecture:</span></span>

| <span data-ttu-id="75595-104">Operációs rendszer</span><span class="sxs-lookup"><span data-stu-id="75595-104">Operating System</span></span>       | <span data-ttu-id="75595-105">Architektúra</span><span class="sxs-lookup"><span data-stu-id="75595-105">Architecture</span></span> | <span data-ttu-id="75595-106">Csomag neve</span><span class="sxs-lookup"><span data-stu-id="75595-106">Package Name</span></span>              | 
|------------------------|--------------|---------------------------| 
| <span data-ttu-id="75595-107">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="75595-107">Windows Server 2012 R2</span></span> | <span data-ttu-id="75595-108">x64</span><span class="sxs-lookup"><span data-stu-id="75595-108">x64</span></span>      | [<span data-ttu-id="75595-109">Win8.1AndW2K12R2-KB3134758-x64.msu</span><span class="sxs-lookup"><span data-stu-id="75595-109">Win8.1AndW2K12R2-KB3134758-x64.msu</span></span>](http://go.microsoft.com/fwlink/?LinkId=717507) | 
| <span data-ttu-id="75595-110">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="75595-110">Windows Server 2012</span></span>    | <span data-ttu-id="75595-111">x64</span><span class="sxs-lookup"><span data-stu-id="75595-111">x64</span></span>      | [<span data-ttu-id="75595-112">W2K12-KB3134759-x64.msu</span><span class="sxs-lookup"><span data-stu-id="75595-112">W2K12-KB3134759-x64.msu</span></span>](http://go.microsoft.com/fwlink/?LinkId=717506) | 
| <span data-ttu-id="75595-113">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="75595-113">Windows Server 2008 R2</span></span> | <span data-ttu-id="75595-114">x64</span><span class="sxs-lookup"><span data-stu-id="75595-114">x64</span></span>      | [<span data-ttu-id="75595-115">Win7AndW2K8R2-KB3134760-x64.msu</span><span class="sxs-lookup"><span data-stu-id="75595-115">Win7AndW2K8R2-KB3134760-x64.msu</span></span>](http://go.microsoft.com/fwlink/?LinkId=717504) |
| <span data-ttu-id="75595-116">A Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="75595-116">Windows 8.1</span></span>            | <span data-ttu-id="75595-117">x64</span><span class="sxs-lookup"><span data-stu-id="75595-117">x64</span></span>          | [<span data-ttu-id="75595-118">Win8.1AndW2K12R2-KB3134758-x64.msu</span><span class="sxs-lookup"><span data-stu-id="75595-118">Win8.1AndW2K12R2-KB3134758-x64.msu</span></span>](http://go.microsoft.com/fwlink/?LinkId=717507) |
| <span data-ttu-id="75595-119">A Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="75595-119">Windows 8.1</span></span>            | <span data-ttu-id="75595-120">x86</span><span class="sxs-lookup"><span data-stu-id="75595-120">x86</span></span>          | [<span data-ttu-id="75595-121">Win8.1-KB3134758-x86.msu</span><span class="sxs-lookup"><span data-stu-id="75595-121">Win8.1-KB3134758-x86.msu</span></span>](http://go.microsoft.com/fwlink/?LinkID=717963) |
| <span data-ttu-id="75595-122">Windows 7 SP1</span><span class="sxs-lookup"><span data-stu-id="75595-122">Windows 7 SP1</span></span>          | <span data-ttu-id="75595-123">x64</span><span class="sxs-lookup"><span data-stu-id="75595-123">x64</span></span>          | [<span data-ttu-id="75595-124">Win7AndW2K8R2-KB3134760-x64.msu</span><span class="sxs-lookup"><span data-stu-id="75595-124">Win7AndW2K8R2-KB3134760-x64.msu</span></span>](http://go.microsoft.com/fwlink/?LinkId=717504) |
| <span data-ttu-id="75595-125">Windows 7 SP1</span><span class="sxs-lookup"><span data-stu-id="75595-125">Windows 7 SP1</span></span>          | <span data-ttu-id="75595-126">x86</span><span class="sxs-lookup"><span data-stu-id="75595-126">x86</span></span>          | [<span data-ttu-id="75595-127">Win7-KB3134760-x86.msu</span><span class="sxs-lookup"><span data-stu-id="75595-127">Win7-KB3134760-x86.msu</span></span>](http://go.microsoft.com/fwlink/?LinkID=717962) |


<span data-ttu-id="75595-128">**WMF 5.0 telepítése a Windows Explorer (vagy a Fájlkezelőben a Windows Server 2012 R2 és Windows 8.1):**</span><span class="sxs-lookup"><span data-stu-id="75595-128">**To install WMF 5.0 from Windows Explorer (or File Explorer in Windows Server 2012 R2 and Windows 8.1):**</span></span>

1. <span data-ttu-id="75595-129">Keresse meg a mappát, amelybe letöltötte a MSU fájlt.</span><span class="sxs-lookup"><span data-stu-id="75595-129">Navigate to the folder into which you downloaded the MSU file.</span></span>

2. <span data-ttu-id="75595-130">Kattintson duplán az MSU futtatni.</span><span class="sxs-lookup"><span data-stu-id="75595-130">Double-click the MSU to run it.</span></span>

<span data-ttu-id="75595-131">**WMF 5.0 telepítése a parancssorból:**</span><span class="sxs-lookup"><span data-stu-id="75595-131">**To install WMF 5.0 from Command Prompt:**</span></span> 

1. <span data-ttu-id="75595-132">Az a számítógép architektúrájának megfelelő csomag a letöltés után nyissa meg egy parancssori ablakot emelt szintű felhasználói jogosultságokkal (Futtatás rendszergazdaként).</span><span class="sxs-lookup"><span data-stu-id="75595-132">After downloading the correct package for your computer's architecture, open a Command Prompt window with elevated user rights (Run as Administrator).</span></span> <span data-ttu-id="75595-133">A Server Core telepítési lehetőségekkel, a Windows Server 2012 R2 vagy Windows Server 2012 vagy Windows Server 2008 R2 SP1, a parancssort emelt szintű felhasználói jogosultságokkal alapértelmezés szerint megnyílik.</span><span class="sxs-lookup"><span data-stu-id="75595-133">On the Server Core installation options of Windows Server 2012 R2 or Windows Server 2012 or Windows Server 2008 R2 SP1, Command Prompt opens with elevated user rights by default.</span></span>

2. <span data-ttu-id="75595-134">Váltson át a mappát, amelybe korábban letöltött vagy másolja a WMF 5.0 telepítőcsomagját.</span><span class="sxs-lookup"><span data-stu-id="75595-134">Change directories to the folder into which you have downloaded or copied the WMF 5.0 installation package.</span></span>

3. <span data-ttu-id="75595-135">A következő parancsok egyikét futtatja:</span><span class="sxs-lookup"><span data-stu-id="75595-135">Run one of the following commands:</span></span>
    - <span data-ttu-id="75595-136">Windows Server 2012 R2 vagy Windows 8.1 x64 futtató számítógépén futtassa az **Win8.1AndW2K12R2-KB3134758-x64.msu quiet**.</span><span class="sxs-lookup"><span data-stu-id="75595-136">On computers that are running Windows Server 2012 R2 or Windows 8.1 x64, run **Win8.1AndW2K12R2-KB3134758-x64.msu /quiet**.</span></span>
    - <span data-ttu-id="75595-137">Futtassa a Windows Server 2012 rendszert futtató számítógépeken, **W2K12-KB3134759-x64.msu quiet**.</span><span class="sxs-lookup"><span data-stu-id="75595-137">On computers that are running Windows Server 2012, run **W2K12-KB3134759-x64.msu /quiet**.</span></span>
    - <span data-ttu-id="75595-138">Az x 64 Windows Server 2008 R2 SP1 vagy Windows 7 SP1 futtató számítógépet, futtassa **Win7AndW2K8R2-KB3134760-x64.msu quiet**.</span><span class="sxs-lookup"><span data-stu-id="75595-138">On computers that are running Windows Server 2008 R2 SP1 or Windows 7 SP1 x64, run **Win7AndW2K8R2-KB3134760-x64.msu /quiet**.</span></span>
    - <span data-ttu-id="75595-139">Windows 8.1 x86 futtató számítógépén futtassa az **Win8.1-KB3134758-x86.msu quiet**.</span><span class="sxs-lookup"><span data-stu-id="75595-139">On computers that are running Windows 8.1 x86, run **Win8.1-KB3134758-x86.msu /quiet**.</span></span>
    - <span data-ttu-id="75595-140">X 86 Windows 7 SP1 operációs rendszert futtató számítógépeken futtassa **Win7-KB3134760-x86.msu quiet**.</span><span class="sxs-lookup"><span data-stu-id="75595-140">On computers that are running Windows 7 SP1 x86, run **Win7-KB3134760-x86.msu /quiet**.</span></span>

<span data-ttu-id="75595-141">**További telepítési megjegyzések a Windows Server 2008 SP1 és Windows 7 SP1:**</span><span class="sxs-lookup"><span data-stu-id="75595-141">**Additional Installation Notes for Windows Server 2008 SP1 and Windows 7 SP1:**</span></span>

<span data-ttu-id="75595-142">Győződjön meg arról, hogy teljesülnek a következő előfeltételek teljesülését:</span><span class="sxs-lookup"><span data-stu-id="75595-142">Ensure following prerequisites have been met:</span></span>
- <span data-ttu-id="75595-143">Legfrissebb telepítve van.</span><span class="sxs-lookup"><span data-stu-id="75595-143">Latest service pack is installed.</span></span>
- <span data-ttu-id="75595-144">[WMF 4.0](http://www.microsoft.com/en-us/download/details.aspx?id=40855) telepítve van</span><span class="sxs-lookup"><span data-stu-id="75595-144">[WMF 4.0](http://www.microsoft.com/en-us/download/details.aspx?id=40855) is installed</span></span>

<span data-ttu-id="75595-145">*A Rendszerfelügyeleti webszolgáltatások függőségi:* Windows PowerShell kívánt állapot konfigurációs szolgáltatása (DSC) WinRM függ.</span><span class="sxs-lookup"><span data-stu-id="75595-145">*WinRM Dependency:* Windows PowerShell Desired State Configuration (DSC) depends on WinRM.</span></span> <span data-ttu-id="75595-146">Rendszerfelügyeleti webszolgáltatások a Windows Server 2008 R2 és Windows 7 alapértelmezés szerint nincs engedélyezve.</span><span class="sxs-lookup"><span data-stu-id="75595-146">WinRM is not enabled by default on Windows Server 2008 R2 and Windows 7.</span></span> <span data-ttu-id="75595-147">Ahhoz, hogy a Rendszerfelügyeleti webszolgáltatások, egy Windows PowerShell az emelt szintű munkamenet, futtassa **Set-WSManQuickConfig**.</span><span class="sxs-lookup"><span data-stu-id="75595-147">To enable WinRM, in a Windows PowerShell elevated session, run **Set-WSManQuickConfig**.</span></span>


