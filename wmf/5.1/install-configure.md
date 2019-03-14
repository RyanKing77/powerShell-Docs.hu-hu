---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: WMF, powershell, beállítás
contributor: keithb
title: Telepítse és konfigurálja a WMF 5.1
ms.openlocfilehash: e5590d48d467506270ccef4089513e1afade07be
ms.sourcegitcommit: 5990f04b8042ef2d8e571bec6d5b051e64c9921c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/12/2019
ms.locfileid: "57795572"
---
# <a name="install-and-configure-wmf-51"></a><span data-ttu-id="5f2c3-103">Telepítse és konfigurálja a WMF 5.1</span><span class="sxs-lookup"><span data-stu-id="5f2c3-103">Install and Configure WMF 5.1</span></span>

## <a name="download-and-install-the-wmf-51-package"></a><span data-ttu-id="5f2c3-104">Töltse le és telepítse a WMF 5.1-csomagot</span><span class="sxs-lookup"><span data-stu-id="5f2c3-104">Download and install the WMF 5.1 package</span></span>

<span data-ttu-id="5f2c3-105">Töltse le a WMF 5.1 csomagot a telepíteni kívánt operációs rendszer és architektúra:</span><span class="sxs-lookup"><span data-stu-id="5f2c3-105">Download the WMF 5.1 package for the operating system and architecture you wish to install it on:</span></span>

| <span data-ttu-id="5f2c3-106">Operációs rendszer</span><span class="sxs-lookup"><span data-stu-id="5f2c3-106">Operating System</span></span>       | <span data-ttu-id="5f2c3-107">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="5f2c3-107">Prerequisites</span></span>           | <span data-ttu-id="5f2c3-108">Csomag hivatkozások</span><span class="sxs-lookup"><span data-stu-id="5f2c3-108">Package Links</span></span>                          |
|------------------------|-------------------------|----------------------------------------|
| <span data-ttu-id="5f2c3-109">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="5f2c3-109">Windows Server 2012 R2</span></span> |                         | <span data-ttu-id="5f2c3-110">[Win8.1AndW2K12R2-KB3191564-x64.msu][]</span><span class="sxs-lookup"><span data-stu-id="5f2c3-110">[Win8.1AndW2K12R2-KB3191564-x64.msu][]</span></span> |
| <span data-ttu-id="5f2c3-111">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="5f2c3-111">Windows Server 2012</span></span>    |                         | <span data-ttu-id="5f2c3-112">[W2K12-KB3191565-x64.msu][]</span><span class="sxs-lookup"><span data-stu-id="5f2c3-112">[W2K12-KB3191565-x64.msu][]</span></span>            |
| <span data-ttu-id="5f2c3-113">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="5f2c3-113">Windows Server 2008 R2</span></span> | <span data-ttu-id="5f2c3-114">[.NET-keretrendszer 4.5.2-es verziója][]</span><span class="sxs-lookup"><span data-stu-id="5f2c3-114">[.NET Framework 4.5.2][]</span></span>| <span data-ttu-id="5f2c3-115">[Win7AndW2K8R2-KB3191566-x64.ZIP][]</span><span class="sxs-lookup"><span data-stu-id="5f2c3-115">[Win7AndW2K8R2-KB3191566-x64.ZIP][]</span></span>    |
| <span data-ttu-id="5f2c3-116">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="5f2c3-116">Windows 8.1</span></span>            |                         | <span data-ttu-id="5f2c3-117">**x64:** [Win8.1AndW2K12R2-KB3191564-x64.msu][]</span><span class="sxs-lookup"><span data-stu-id="5f2c3-117">**x64:** [Win8.1AndW2K12R2-KB3191564-x64.msu][]</span></span></br><span data-ttu-id="5f2c3-118">**x86:** [Win8.1-KB3191564-x86.msu][]</span><span class="sxs-lookup"><span data-stu-id="5f2c3-118">**x86:** [Win8.1-KB3191564-x86.msu][]</span></span> |
| <span data-ttu-id="5f2c3-119">Windows 7 SP1</span><span class="sxs-lookup"><span data-stu-id="5f2c3-119">Windows 7 SP1</span></span>          | <span data-ttu-id="5f2c3-120">[.NET-keretrendszer 4.5.2-es verziója][]</span><span class="sxs-lookup"><span data-stu-id="5f2c3-120">[.NET Framework 4.5.2][]</span></span>| <span data-ttu-id="5f2c3-121">**x64:** [Win7AndW2K8R2-KB3191566-x64.ZIP][]</span><span class="sxs-lookup"><span data-stu-id="5f2c3-121">**x64:** [Win7AndW2K8R2-KB3191566-x64.ZIP][]</span></span></br><span data-ttu-id="5f2c3-122">**x86:** [Win7-KB3191566-x86.ZIP][]</span><span class="sxs-lookup"><span data-stu-id="5f2c3-122">**x86:** [Win7-KB3191566-x86.ZIP][]</span></span> |

[.NET-keretrendszer 4.5.2-es verziója]: https://www.microsoft.com/download/details.aspx?id=42642
[.NET Framework 4.5.2]: https://www.microsoft.com/download/details.aspx?id=42642
[W2K12-KB3191565-x64.msu]: https://go.microsoft.com/fwlink/?linkid=839513
[Win7-KB3191566-x86.ZIP]: https://go.microsoft.com/fwlink/?linkid=839522
[Win7AndW2K8R2-KB3191566-x64.ZIP]: https://go.microsoft.com/fwlink/?linkid=839523
[Win8.1-KB3191564-x86.msu]: https://go.microsoft.com/fwlink/?linkid=839521
[Win8.1AndW2K12R2-KB3191564-x64.msu]: https://go.microsoft.com/fwlink/?linkid=839516

## <a name="install-wmf-51-for-windows-server-2008-r2-and-windows-7"></a><span data-ttu-id="5f2c3-129">Telepítse a WMF 5.1 Windows Server 2008 R2 és Windows 7</span><span class="sxs-lookup"><span data-stu-id="5f2c3-129">Install WMF 5.1 for Windows Server 2008 R2 and Windows 7</span></span>

> <span data-ttu-id="5f2c3-130">**Megjegyzés:** Telepítési utasítások Windows 7 és Windows Server 2008 R2 változtak, és eltér a többi csomagot vonatkozó utasításokat.</span><span class="sxs-lookup"><span data-stu-id="5f2c3-130">**Note:** Installation instructions for Windows Server 2008 R2 and Windows 7 have changed, and differ from the instructions for the other packages.</span></span> <span data-ttu-id="5f2c3-131">Az alábbiakban a Windows Server 2012 R2, Windows Server 2012 és Windows 8.1 telepítési utasításokat.</span><span class="sxs-lookup"><span data-stu-id="5f2c3-131">Installation instructions for Windows Server 2012 R2, Windows Server 2012, and Windows 8.1 are below.</span></span>

<span data-ttu-id="5f2c3-132">**A WMF 5.1 Windows Server 2008 R2 és Windows 7 telepítése**</span><span class="sxs-lookup"><span data-stu-id="5f2c3-132">**Installing WMF 5.1 on Windows Server 2008 R2 and Windows 7**</span></span>

1. <span data-ttu-id="5f2c3-133">Keresse meg a mappát, amelybe a letöltött ZIP-fájl.</span><span class="sxs-lookup"><span data-stu-id="5f2c3-133">Navigate to the folder into which you downloaded the ZIP file.</span></span>

2. <span data-ttu-id="5f2c3-134">Kattintson a jobb gombbal a ZIP-fájlt, és válassza a "Bontsa ki az összes...".</span><span class="sxs-lookup"><span data-stu-id="5f2c3-134">Right-click on the ZIP file, and select "Extract All...".</span></span> <span data-ttu-id="5f2c3-135">A zip-fájl 2 fájlokat tartalmazza: az MSU és az Install-WMF5.1.PS1-parancsfájl tárolásához.</span><span class="sxs-lookup"><span data-stu-id="5f2c3-135">The Zip contains 2 files: an MSU and the Install-WMF5.1.PS1 script file.</span></span>
<span data-ttu-id="5f2c3-136">Miután a ZIP-fájl kicsomagolása, másolja bele a bármely Windows 7 vagy Windows Server 2008 R2 rendszerű géphez.</span><span class="sxs-lookup"><span data-stu-id="5f2c3-136">Once you have unpacked the ZIP file, you can copy the contents to any machine running Windows 7 or Windows Server 2008 R2.</span></span>

3. <span data-ttu-id="5f2c3-137">Ezt követően a ZIP-fájl tartalmát, nyissa meg a Powershellt rendszergazdaként, majd nyissa meg a mappát, amely tartalmazza a ZIP-fájl tartalmát.</span><span class="sxs-lookup"><span data-stu-id="5f2c3-137">After extracting the ZIP file contents, open PowerShell as administrator, then navigate to the folder containing the contents of the ZIP file.</span></span>

4. <span data-ttu-id="5f2c3-138">A telepítés-Wmf5.1.ps1 parancsprogrammal abban a mappában, és kövesse az utasításokat.</span><span class="sxs-lookup"><span data-stu-id="5f2c3-138">Run the Install-Wmf5.1.ps1 script in that folder, and follow the instructions.</span></span> <span data-ttu-id="5f2c3-139">Ez a szkript ellenőrizze az előfeltételeket a helyi gépen, és telepítse a WMF 5.1, ha az előfeltételek teljesülnek.</span><span class="sxs-lookup"><span data-stu-id="5f2c3-139">This script will check the prerequisites on the local machine, and install WMF 5.1 if the prerequisites have been met.</span></span> <span data-ttu-id="5f2c3-140">Az előfeltételek az alábbiakban láthatók.</span><span class="sxs-lookup"><span data-stu-id="5f2c3-140">The prerequisites are listed below.</span></span>

<span data-ttu-id="5f2c3-141">Install-WMF5.1.ps1 megkönnyítése érdekében automatizálása a Windows 7 és Windows Server 2008 R2 telepítését a következő paramétereket fogadja:</span><span class="sxs-lookup"><span data-stu-id="5f2c3-141">Install-WMF5.1.ps1 takes the following parameters to ease automating the installation on Windows Server 2008 R2 and Windows 7:</span></span>

- <span data-ttu-id="5f2c3-142">AcceptEula: Ha ezt a paramétert tartalmaz, a végfelhasználói licencszerződés automatikusan elfogadja a rendszer, és nem jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="5f2c3-142">AcceptEula: When this parameter is included, the EULA is automatically accepted and will not be displayed.</span></span>
- <span data-ttu-id="5f2c3-143">AllowRestart: Ez a paraméter csak használható, ha AcceptEula van megadva.</span><span class="sxs-lookup"><span data-stu-id="5f2c3-143">AllowRestart: This parameter can only be used if AcceptEula is specified.</span></span> <span data-ttu-id="5f2c3-144">Ha ez a paraméter szerepel, és újraindításra szükség a WMF 5.1 telepítése után, az újraindítás a telepítés befejezése után azonnal rákérdezés nélkül történik meg.</span><span class="sxs-lookup"><span data-stu-id="5f2c3-144">If this parameter is included, and a restart is required after installing WMF 5.1, the restart will happen without prompting immediately after the installation is completed.</span></span>

<span data-ttu-id="5f2c3-145">**A WMF 5.1 Windows Server 2008 R2 SP1, Windows 7 SP1 és előfeltételei**</span><span class="sxs-lookup"><span data-stu-id="5f2c3-145">**WMF 5.1 Prerequisites for Windows Server 2008 R2 SP1 and Windows 7 SP1**</span></span>

<span data-ttu-id="5f2c3-146">A Windows Server 2008 R2 SP1 vagy Windows 7 SP1, a WMF 5.1 telepítéséhez a következőket:</span><span class="sxs-lookup"><span data-stu-id="5f2c3-146">Installation of WMF 5.1 on either Windows Server 2008 R2 SP1 or Windows 7 SP1, requires the following:</span></span>
- <span data-ttu-id="5f2c3-147">Legfrissebb szervizcsomag telepítve kell lennie.</span><span class="sxs-lookup"><span data-stu-id="5f2c3-147">Latest service pack must be installed.</span></span>
- <span data-ttu-id="5f2c3-148">WMF 3.0 **nem kell** telepíthető.</span><span class="sxs-lookup"><span data-stu-id="5f2c3-148">WMF 3.0 **must not** be installed.</span></span> <span data-ttu-id="5f2c3-149">A WMF 5.1 telepítése a WMF 3.0 protokollon keresztül a PSModulePath, ami okozhat más alkalmazások sikertelen elvesztését eredményezi.</span><span class="sxs-lookup"><span data-stu-id="5f2c3-149">Installing WMF 5.1 over WMF 3.0 will result in the loss of the PSModulePath, which can cause other applications to fail.</span></span> <span data-ttu-id="5f2c3-150">A WMF 5.1 a telepítés előtt vagy eltávolítási WMF 3.0-s vagy mentse a PSModulePath és kell majd annak visszaállítására manuálisan a WMF 5.1 telepítésének befejezése után.</span><span class="sxs-lookup"><span data-stu-id="5f2c3-150">Before installing WMF 5.1, you must either un-install WMF 3.0, or save the PSModulePath and then restore it manually after WMF 5.1 installation is complete.</span></span>
- <span data-ttu-id="5f2c3-151">A WMF 5.1-es vagy újabb szükséges [.NET-keretrendszer 4.5.2-es](https://www.microsoft.com/en-ca/download/details.aspx?id=42642).</span><span class="sxs-lookup"><span data-stu-id="5f2c3-151">WMF 5.1 requires at least [.NET Framework 4.5.2](https://www.microsoft.com/en-ca/download/details.aspx?id=42642).</span></span>
<span data-ttu-id="5f2c3-152">A letöltési helyen található utasításokat követve telepítheti a Microsoft .NET-keretrendszer 4.5.2-es verzióját.</span><span class="sxs-lookup"><span data-stu-id="5f2c3-152">You can install Microsoft .NET Framework 4.5.2 by following the instructions at the download location.</span></span>

<span data-ttu-id="5f2c3-153">**A WinRM-függőség**</span><span class="sxs-lookup"><span data-stu-id="5f2c3-153">**WinRM Dependency**</span></span>

<span data-ttu-id="5f2c3-154">Windows PowerShell Desired State Configuration (DSC) attól függ, hogy a Rendszerfelügyeleti webszolgáltatások.</span><span class="sxs-lookup"><span data-stu-id="5f2c3-154">Windows PowerShell Desired State Configuration (DSC) depends on WinRM.</span></span>
<span data-ttu-id="5f2c3-155">A Rendszerfelügyeleti webszolgáltatások a Windows Server 2008 R2 és Windows 7 alapértelmezés szerint nincs engedélyezve.</span><span class="sxs-lookup"><span data-stu-id="5f2c3-155">WinRM is not enabled by default on Windows Server 2008 R2 and Windows 7.</span></span>
<span data-ttu-id="5f2c3-156">Futtatás `Set-WSManQuickConfig`, egy Windows PowerShell az emelt szintű ahhoz, hogy a WinRM-munkamenetben.</span><span class="sxs-lookup"><span data-stu-id="5f2c3-156">Run `Set-WSManQuickConfig`, in a Windows PowerShell elevated session, to enable WinRM.</span></span>

## <a name="install-wmf-51-for-windows-server-2012-r2-windows-server-2012-and-windows-81"></a><span data-ttu-id="5f2c3-157">Telepítse a WMF 5.1 Windows Server 2012 R2, Windows Server 2012 és Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="5f2c3-157">Install WMF 5.1 for Windows Server 2012 R2, Windows Server 2012, and Windows 8.1</span></span>

<span data-ttu-id="5f2c3-158">**Telepítse a Windows Explorer (vagy a Fájlkezelővel, a Windows Server 2012 R2 vagy Windows 8.1)**</span><span class="sxs-lookup"><span data-stu-id="5f2c3-158">**Install from Windows Explorer (or File Explorer in Windows Server 2012 R2 or Windows 8.1)**</span></span>

1. <span data-ttu-id="5f2c3-159">Lépjen abba a mappába, amelybe letöltötte a MSU-fájlt.</span><span class="sxs-lookup"><span data-stu-id="5f2c3-159">Navigate to the folder into which you downloaded the MSU file.</span></span>
2. <span data-ttu-id="5f2c3-160">Kattintson duplán az MSU a futtatáshoz.</span><span class="sxs-lookup"><span data-stu-id="5f2c3-160">Double-click the MSU to run it.</span></span>

<span data-ttu-id="5f2c3-161">**Telepítése a parancssorból**</span><span class="sxs-lookup"><span data-stu-id="5f2c3-161">**Installing from the Command Prompt**</span></span>

1. <span data-ttu-id="5f2c3-162">Az a számítógép architektúrájának megfelelő csomagot a letöltés után nyissa meg egy parancssori ablakot emelt szintű felhasználói jogosultságokkal (Futtatás rendszergazdaként).</span><span class="sxs-lookup"><span data-stu-id="5f2c3-162">After downloading the correct package for your computer's architecture, open a Command Prompt window with elevated user rights (Run as Administrator).</span></span> <span data-ttu-id="5f2c3-163">A Server Core telepítési lehetőségekkel, a Windows Server 2012 R2, Windows Server 2012 vagy Windows Server 2008 R2 SP1, a parancssort emelt szintű felhasználói jogosultságokkal alapértelmezés szerint megnyílik.</span><span class="sxs-lookup"><span data-stu-id="5f2c3-163">On the Server Core installation options of Windows Server 2012 R2, Windows Server 2012, or Windows Server 2008 R2 SP1, Command Prompt opens with elevated user rights by default.</span></span>
2. <span data-ttu-id="5f2c3-164">Módosítsa a könyvtárakat a mappát, amelybe korábban letöltött vagy másolja a WMF 5.1-telepítési csomagot.</span><span class="sxs-lookup"><span data-stu-id="5f2c3-164">Change directories to the folder into which you have downloaded or copied the WMF 5.1 installation package.</span></span>
3. <span data-ttu-id="5f2c3-165">Futtassa a következő parancsok egyikét:</span><span class="sxs-lookup"><span data-stu-id="5f2c3-165">Run one of the following commands:</span></span>
   - <span data-ttu-id="5f2c3-166">Windows Server 2012 R2 vagy Windows 8.1 x64 rendszert futtató számítógépeken futtassa `Win8.1AndW2K12R2-KB3191564-x64.msu /quiet`.</span><span class="sxs-lookup"><span data-stu-id="5f2c3-166">On computers that are running Windows Server 2012 R2 or Windows 8.1 x64, run `Win8.1AndW2K12R2-KB3191564-x64.msu /quiet`.</span></span>
   - <span data-ttu-id="5f2c3-167">A Windows Server 2012 rendszert futtató számítógépeken futtassa `W2K12-KB3191565-x64.msu /quiet`.</span><span class="sxs-lookup"><span data-stu-id="5f2c3-167">On computers that are running Windows Server 2012, run `W2K12-KB3191565-x64.msu /quiet`.</span></span>
   - <span data-ttu-id="5f2c3-168">X86 Windows 8.1 rendszert futtató számítógépeken futtassa `Win8.1-KB3191564-x86.msu /quiet`.</span><span class="sxs-lookup"><span data-stu-id="5f2c3-168">On computers that are running Windows 8.1 x86, run `Win8.1-KB3191564-x86.msu /quiet`.</span></span>

> [!NOTE]
> <span data-ttu-id="5f2c3-169">A WMF 5.1 telepítéséhez újraindítás szükséges.</span><span class="sxs-lookup"><span data-stu-id="5f2c3-169">Installing WMF 5.1 requires a reboot.</span></span> <span data-ttu-id="5f2c3-170">Használatával a `/quiet` beállítás újraindul figyelmeztetés nélkül a rendszer.</span><span class="sxs-lookup"><span data-stu-id="5f2c3-170">Using the `/quiet` option will reboot the system without warning.</span></span>
> <span data-ttu-id="5f2c3-171">Használja a `/norestart` azzal elkerülheti a beállítást.</span><span class="sxs-lookup"><span data-stu-id="5f2c3-171">Use the `/norestart` option to avoid rebooting.</span></span> <span data-ttu-id="5f2c3-172">Azonban a WMF 5.1-es nem lesz telepítve csak rendelkezik újraindítása.</span><span class="sxs-lookup"><span data-stu-id="5f2c3-172">However, WMF 5.1 will not be installed until you have rebooted.</span></span>
