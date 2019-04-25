---
ms.date: 08/09/2017
keywords: PowerShell, parancsmag, letöltése, telepítése, a telepítő, windows 10, windows 8.1, windows 8.0-s, windows 7
title: A Windows PowerShell telepítése
ms.openlocfilehash: 345cde8012bece730e7217ed16be6175ad26bb28
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62086476"
---
# <a name="installing-windows-powershell"></a><span data-ttu-id="43a9d-103">A Windows PowerShell telepítése</span><span class="sxs-lookup"><span data-stu-id="43a9d-103">Installing Windows PowerShell</span></span>

<span data-ttu-id="43a9d-104">Windows PowerShell előre telepített alapértelmezés szerint a minden Windows, Windows 7 SP1 és a Windows Server 2008 R2 SP1-től.</span><span class="sxs-lookup"><span data-stu-id="43a9d-104">Windows PowerShell comes installed by default in every Windows, starting with Windows 7 SP1 and Windows Server 2008 R2 SP1.</span></span>

<span data-ttu-id="43a9d-105">Ha érdekli a PowerShell 6-os vagy újabb, a PowerShell Core helyett a Windows PowerShell telepíteni szeretné.</span><span class="sxs-lookup"><span data-stu-id="43a9d-105">If you are interested in PowerShell 6 and later, you need to install PowerShell Core instead of Windows PowerShell.</span></span> <span data-ttu-id="43a9d-106">Ehhez lásd [Windows-alapú PowerShell Core telepítése](Installing-PowerShell-Core-on-Windows.md).</span><span class="sxs-lookup"><span data-stu-id="43a9d-106">For that, see [Installing PowerShell Core on Windows](Installing-PowerShell-Core-on-Windows.md).</span></span>

## <a name="finding-powershell-in-windows-10-81-80-and-7"></a><span data-ttu-id="43a9d-107">A Windows 10-es, 8.1, 8.0-s és 7 PowerShell keresése</span><span class="sxs-lookup"><span data-stu-id="43a9d-107">Finding PowerShell in Windows 10, 8.1, 8.0, and 7</span></span>

<span data-ttu-id="43a9d-108">Néha keresése a PowerShell konzolt vagy az ISE-ben (integrált parancsfájl-kezelési környezet) a Windows nehézkes lehet, mint a Windows egyik verziójának a helyét helyez át a következő.</span><span class="sxs-lookup"><span data-stu-id="43a9d-108">Sometimes locating PowerShell console or ISE (Integrated Scripting Environment) in Windows can be difficult, as its location moves from one version of Windows to the next.</span></span>

<span data-ttu-id="43a9d-109">Az alábbi táblázatok segítséget PowerShell található Windows-verzióhoz.</span><span class="sxs-lookup"><span data-stu-id="43a9d-109">The following tables should help you find PowerShell in your Windows version.</span></span>
<span data-ttu-id="43a9d-110">Az itt felsorolt összes verzió az eredeti verzió, mert a kiadott, sem a frissítés.</span><span class="sxs-lookup"><span data-stu-id="43a9d-110">All versions listed here are the original version, as released, with no updates.</span></span>

### <a name="for-console"></a><span data-ttu-id="43a9d-111">-Konzol</span><span class="sxs-lookup"><span data-stu-id="43a9d-111">For Console</span></span>

<span data-ttu-id="43a9d-112">Verzió</span><span class="sxs-lookup"><span data-stu-id="43a9d-112">Version</span></span> | <span data-ttu-id="43a9d-113">Hely</span><span class="sxs-lookup"><span data-stu-id="43a9d-113">Location</span></span>
-- | --
<span data-ttu-id="43a9d-114">Windows 10</span><span class="sxs-lookup"><span data-stu-id="43a9d-114">Windows 10</span></span> | <span data-ttu-id="43a9d-115">Kattintson a bal alsó sarokban Windows ikonjára, és kezdje el begépelni a PowerShell</span><span class="sxs-lookup"><span data-stu-id="43a9d-115">Click left lower corner Windows icon, start typing PowerShell</span></span>
<span data-ttu-id="43a9d-116">Windows 8.1, 8.0</span><span class="sxs-lookup"><span data-stu-id="43a9d-116">Windows 8.1, 8.0</span></span> | <span data-ttu-id="43a9d-117">A kezdőképernyőn írja be a PowerShell indítása.</span><span class="sxs-lookup"><span data-stu-id="43a9d-117">On the start screen, start typing PowerShell.</span></span><br/><span data-ttu-id="43a9d-118">Ha a számítógépen, kattintson a bal alsó sarokban Windows ikonjára, kezdje el begépelni a PowerShell</span><span class="sxs-lookup"><span data-stu-id="43a9d-118">If on desktop, click left lower corner Windows icon, start typing PowerShell</span></span>
<span data-ttu-id="43a9d-119">Windows 7 SP1</span><span class="sxs-lookup"><span data-stu-id="43a9d-119">Windows 7 SP1</span></span> | <span data-ttu-id="43a9d-120">Kattintson a bal alsó sarokban található Windows ikont, a Keresés mezőbe írja be a PowerShell start</span><span class="sxs-lookup"><span data-stu-id="43a9d-120">Click left lower corner Windows icon, on the search box start typing PowerShell</span></span>

### <a name="for-ise"></a><span data-ttu-id="43a9d-121">Az ISE-ben</span><span class="sxs-lookup"><span data-stu-id="43a9d-121">For ISE</span></span>

<span data-ttu-id="43a9d-122">Verzió</span><span class="sxs-lookup"><span data-stu-id="43a9d-122">Version</span></span> | <span data-ttu-id="43a9d-123">Hely</span><span class="sxs-lookup"><span data-stu-id="43a9d-123">Location</span></span>
-- | --
<span data-ttu-id="43a9d-124">Windows 10</span><span class="sxs-lookup"><span data-stu-id="43a9d-124">Windows 10</span></span> | <span data-ttu-id="43a9d-125">Kattintson a bal alsó sarokban Windows ikonjára, és kezdje el begépelni az ISE-ben</span><span class="sxs-lookup"><span data-stu-id="43a9d-125">Click left lower corner Windows icon, start typing ISE</span></span>
<span data-ttu-id="43a9d-126">Windows 8.1, 8.0</span><span class="sxs-lookup"><span data-stu-id="43a9d-126">Windows 8.1, 8.0</span></span> | <span data-ttu-id="43a9d-127">A kezdőképernyőn írja be a **PowerShell ISE-ben**.</span><span class="sxs-lookup"><span data-stu-id="43a9d-127">On the start screen, type **PowerShell ISE**.</span></span><br/><span data-ttu-id="43a9d-128">Ha az asztalon kattintson bal alsó sarokban található Windows ikonra, írja be a **PowerShell ISE-ben**</span><span class="sxs-lookup"><span data-stu-id="43a9d-128">If on desktop, click left lower corner Windows icon, type **PowerShell ISE**</span></span>
<span data-ttu-id="43a9d-129">Windows 7 SP1</span><span class="sxs-lookup"><span data-stu-id="43a9d-129">Windows 7 SP1</span></span> | <span data-ttu-id="43a9d-130">Kattintson a bal alsó sarokban található Windows ikont, a Keresés mezőbe írja be a PowerShell start</span><span class="sxs-lookup"><span data-stu-id="43a9d-130">Click left lower corner Windows icon, on the search box start typing PowerShell</span></span>

## <a name="finding-powershell-in-windows-server-versions"></a><span data-ttu-id="43a9d-131">Keresés a PowerShell a Windows Server-verziók</span><span class="sxs-lookup"><span data-stu-id="43a9d-131">Finding PowerShell in Windows Server versions</span></span>

<span data-ttu-id="43a9d-132">A Windows Server 2008 R2 verziótól kezdődően Windows operációs rendszer nélkül is telepíthetők a grafikus felhasználói felületen (GUI).</span><span class="sxs-lookup"><span data-stu-id="43a9d-132">Starting with Windows Server 2008 R2, Windows operating system can be installed without the graphical user interface (GUI).</span></span>
<span data-ttu-id="43a9d-133">Windows Server a grafikus felhasználói felület nélkül kiadásai nevesített **Core** és kiadása a grafikus felhasználói Felülettel rendelkező nevű **asztali**.</span><span class="sxs-lookup"><span data-stu-id="43a9d-133">Editions of Windows Server without GUI are named **Core** editions, and editions with the GUI are named **Desktop**.</span></span>

### <a name="windows-server-core-editions"></a><span data-ttu-id="43a9d-134">A Windows Server Core kiadásokban</span><span class="sxs-lookup"><span data-stu-id="43a9d-134">Windows Server Core editions</span></span>

<span data-ttu-id="43a9d-135">A Core kiadásokban az összes a kiszolgálón való bejelentkezéskor kap egy Windows parancssori ablakban.</span><span class="sxs-lookup"><span data-stu-id="43a9d-135">In all Core editions, when you log to the server you get a Windows command prompt window.</span></span>

<span data-ttu-id="43a9d-136">Típus `powershell` nyomja le az ENTER **ENTER** PowerShell elindítása belül a parancssori munkamenetben.</span><span class="sxs-lookup"><span data-stu-id="43a9d-136">Type `powershell` and press **ENTER** to start PowerShell inside the command prompt session.</span></span>
<span data-ttu-id="43a9d-137">Típus `exit` leállítása a PowerShell-munkamenetet, és visszatérhet a parancssor használatával.</span><span class="sxs-lookup"><span data-stu-id="43a9d-137">Type `exit` to terminate the PowerShell session and return to command prompt.</span></span>

### <a name="windows-server-desktop-editions"></a><span data-ttu-id="43a9d-138">A Windows Server asztali verziója esetén</span><span class="sxs-lookup"><span data-stu-id="43a9d-138">Windows Server Desktop editions</span></span>

<span data-ttu-id="43a9d-139">Az összes asztali verzió kattintson a bal alsó sarokban található Windows ikonra, kezdje el begépelni a PowerShell.</span><span class="sxs-lookup"><span data-stu-id="43a9d-139">In all desktop editions, click the left lower corner Windows icon, start typing PowerShell.</span></span>
<span data-ttu-id="43a9d-140">Konzol és az ISE-beállítások is kap.</span><span class="sxs-lookup"><span data-stu-id="43a9d-140">You get both console and ISE options.</span></span>

<span data-ttu-id="43a9d-141">Az egyetlen kivétel a fenti szabály, a Windows Server 2008 R2 SP1; az ISE-ben Ebben az esetben kattintson a bal alsó sarokban található Windows ikonra, írja be a PowerShell ISE-ben.</span><span class="sxs-lookup"><span data-stu-id="43a9d-141">The only exception to the above rule is the ISE in Windows Server 2008 R2 SP1; in this case, click the left lower corner Windows icon, type PowerShell ISE.</span></span>

## <a name="how-to-check-the-version-of-powershell"></a><span data-ttu-id="43a9d-142">A PowerShell-verzió ellenőrzése</span><span class="sxs-lookup"><span data-stu-id="43a9d-142">How to check the version of PowerShell</span></span>

<span data-ttu-id="43a9d-143">Keresse meg a PowerShell-verzió van telepítve, indítsa el a PowerShell-konzolt (vagy az ISE-ben), és írja be `$PSVersionTable` nyomja le az ENTER **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="43a9d-143">To find which version of PowerShell you have installed, start a PowerShell console (or the ISE) and type `$PSVersionTable` and press **ENTER**.</span></span> <span data-ttu-id="43a9d-144">Keresse meg a `PSVersion` értéket.</span><span class="sxs-lookup"><span data-stu-id="43a9d-144">Look for the `PSVersion` value.</span></span>

## <a name="upgrading-existing-windows-powershell"></a><span data-ttu-id="43a9d-145">Meglévő Windows PowerShell frissítése</span><span class="sxs-lookup"><span data-stu-id="43a9d-145">Upgrading existing Windows PowerShell</span></span>

<span data-ttu-id="43a9d-146">A telepítőcsomag PowerShell belül a WMF-telepítési származnak.</span><span class="sxs-lookup"><span data-stu-id="43a9d-146">The installation package for PowerShell comes inside a WMF installer.</span></span>
<span data-ttu-id="43a9d-147">A WMF telepítő verzióegyezéseket PowerShell; verziója Nincs nincs önálló telepítő a Windows PowerShell környezethez.</span><span class="sxs-lookup"><span data-stu-id="43a9d-147">The version of the WMF installer matches the version of PowerShell; there's no stand alone installer for Windows PowerShell.</span></span>

<span data-ttu-id="43a9d-148">Ha a meglévő PowerShell-lel, frissítenie kell a Windows, segítségével az alábbi táblázatban keresse meg a frissíteni kívánt PowerShell verziójának telepítőjét.</span><span class="sxs-lookup"><span data-stu-id="43a9d-148">If you need to update your existing version of PowerShell, in Windows, use the following table to locate the installer for the version of PowerShell you want to update to.</span></span>

<span data-ttu-id="43a9d-149">Windows</span><span class="sxs-lookup"><span data-stu-id="43a9d-149">Windows</span></span> | <span data-ttu-id="43a9d-150">PS 3.0</span><span class="sxs-lookup"><span data-stu-id="43a9d-150">PS 3.0</span></span> | <span data-ttu-id="43a9d-151">PS 4.0</span><span class="sxs-lookup"><span data-stu-id="43a9d-151">PS 4.0</span></span> | <span data-ttu-id="43a9d-152">PS 5.0</span><span class="sxs-lookup"><span data-stu-id="43a9d-152">PS 5.0</span></span> | <span data-ttu-id="43a9d-153">PS 5.1</span><span class="sxs-lookup"><span data-stu-id="43a9d-153">PS 5.1</span></span> |
--|--|--|--|--|
<span data-ttu-id="43a9d-154">A Windows 10-es (lásd a Note1)</span><span class="sxs-lookup"><span data-stu-id="43a9d-154">Windows 10 (see Note1)</span></span><br/><span data-ttu-id="43a9d-155">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="43a9d-155">Windows Server 2016</span></span> | - | - | - | <span data-ttu-id="43a9d-156">Telepítve van</span><span class="sxs-lookup"><span data-stu-id="43a9d-156">installed</span></span>
<span data-ttu-id="43a9d-157">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="43a9d-157">Windows 8.1</span></span><br/><span data-ttu-id="43a9d-158">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="43a9d-158">Windows Server 2012 R2</span></span> | - | <span data-ttu-id="43a9d-159">Telepítve van</span><span class="sxs-lookup"><span data-stu-id="43a9d-159">installed</span></span> | [<span data-ttu-id="43a9d-160">WMF 5.0</span><span class="sxs-lookup"><span data-stu-id="43a9d-160">WMF 5.0</span></span>](https://www.microsoft.com/en-us/download/details.aspx?id=50395) | [<span data-ttu-id="43a9d-161">WMF 5.1</span><span class="sxs-lookup"><span data-stu-id="43a9d-161">WMF 5.1</span></span>](https://www.microsoft.com/en-us/download/details.aspx?id=54616)
<span data-ttu-id="43a9d-162">Windows 8</span><span class="sxs-lookup"><span data-stu-id="43a9d-162">Windows 8</span></span><br/><span data-ttu-id="43a9d-163">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="43a9d-163">Windows Server 2012</span></span> | <span data-ttu-id="43a9d-164">Telepítve van</span><span class="sxs-lookup"><span data-stu-id="43a9d-164">installed</span></span> | [<span data-ttu-id="43a9d-165">WMF 4.0</span><span class="sxs-lookup"><span data-stu-id="43a9d-165">WMF 4.0</span></span>](https://www.microsoft.com/en-us/download/details.aspx?id=40855) | [<span data-ttu-id="43a9d-166">WMF 5.0</span><span class="sxs-lookup"><span data-stu-id="43a9d-166">WMF 5.0</span></span>](https://www.microsoft.com/en-us/download/details.aspx?id=50395) | [<span data-ttu-id="43a9d-167">WMF 5.1</span><span class="sxs-lookup"><span data-stu-id="43a9d-167">WMF 5.1</span></span>](https://www.microsoft.com/en-us/download/details.aspx?id=54616)
<span data-ttu-id="43a9d-168">Windows 7 SP1</span><span class="sxs-lookup"><span data-stu-id="43a9d-168">Windows 7 SP1</span></span><br/><span data-ttu-id="43a9d-169">Windows Server 2008 R2 SP1</span><span class="sxs-lookup"><span data-stu-id="43a9d-169">Windows Server 2008 R2 SP1</span></span> | [<span data-ttu-id="43a9d-170">WMF 3.0</span><span class="sxs-lookup"><span data-stu-id="43a9d-170">WMF 3.0</span></span>](https://www.microsoft.com/en-us/download/details.aspx?id=34595) | [<span data-ttu-id="43a9d-171">WMF 4.0</span><span class="sxs-lookup"><span data-stu-id="43a9d-171">WMF 4.0</span></span>](https://www.microsoft.com/en-us/download/details.aspx?id=40855) | [<span data-ttu-id="43a9d-172">WMF 5.0</span><span class="sxs-lookup"><span data-stu-id="43a9d-172">WMF 5.0</span></span>](https://www.microsoft.com/en-us/download/details.aspx?id=50395) | [<span data-ttu-id="43a9d-173">WMF 5.1</span><span class="sxs-lookup"><span data-stu-id="43a9d-173">WMF 5.1</span></span>](https://www.microsoft.com/en-us/download/details.aspx?id=54616)

> [!NOTE]
>
> <span data-ttu-id="43a9d-174">Az automatikus frissítések szolgáltatás engedélyezve van, a Windows 10, az eredeti kiadásban a PowerShell 5.0, 5.1-es verziójából származó frissül.</span><span class="sxs-lookup"><span data-stu-id="43a9d-174">On the initial release of Windows 10, with automatic updates enabled, PowerShell gets updated from version 5.0 to 5.1.</span></span>
>
> <span data-ttu-id="43a9d-175">Ha az eredeti verzió Windows 10-es nem frissül a Windows-frissítések, a PowerShell verziója 5.0-s.</span><span class="sxs-lookup"><span data-stu-id="43a9d-175">If the original version of Windows 10 is not updated through Windows Updates, the version of PowerShell is 5.0.</span></span>

## <a name="need-azure-powershell"></a><span data-ttu-id="43a9d-176">Az Azure PowerShell szükséges.</span><span class="sxs-lookup"><span data-stu-id="43a9d-176">Need Azure PowerShell</span></span>

<span data-ttu-id="43a9d-177">Ha a keresett **Azure PowerShell-lel**, kezdheti [áttekintése az Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="43a9d-177">If you're looking for **Azure PowerShell**, you could start with [Overview of Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="43a9d-178">Ellenkező esetben van, mit érdemes [telepítése és konfigurálása az Azure PowerShell-lel](/powershell/azure/install-az-ps)</span><span class="sxs-lookup"><span data-stu-id="43a9d-178">Otherwise, what you might need is [Install and configure Azure PowerShell](/powershell/azure/install-az-ps)</span></span>

## <a name="see-also"></a><span data-ttu-id="43a9d-179">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="43a9d-179">See Also</span></span>

[<span data-ttu-id="43a9d-180">Windows PowerShell rendszerkövetelményei</span><span class="sxs-lookup"><span data-stu-id="43a9d-180">Windows PowerShell System Requirements</span></span>](Windows-PowerShell-System-Requirements.md)

[<span data-ttu-id="43a9d-181">Windows PowerShell indítása</span><span class="sxs-lookup"><span data-stu-id="43a9d-181">Starting Windows PowerShell</span></span>](../getting-started/Starting-Windows-PowerShell.md)
