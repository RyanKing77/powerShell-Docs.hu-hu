---
ms.date: 2017-08-09
keywords: "PowerShell, a parancsmag, letöltése, telepítése, beállításához, windows 10, windows 8.1, windows 8.0-s, windows 7"
title: "Windows PowerShell telepítése"
ms.openlocfilehash: 781bf50b6ac649e72bcdbb708555275fb7422d94
ms.sourcegitcommit: 3720ce4efb6735694cfb53a1b793d949af5d1bc5
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/29/2017
---
# <a name="installing-windows-powershell"></a><span data-ttu-id="e5a42-103">Windows PowerShell telepítése</span><span class="sxs-lookup"><span data-stu-id="e5a42-103">Installing Windows PowerShell</span></span>

<span data-ttu-id="e5a42-104">PowerShell előre telepített alapértelmezés szerint a minden Windows, Windows 7 SP1 és Windows Server 2008 R2 SP1 kezdve.</span><span class="sxs-lookup"><span data-stu-id="e5a42-104">PowerShell comes installed by default in every Windows, starting with Windows 7 SP1 and Windows Server 2008 R2 SP1.</span></span>

<span data-ttu-id="e5a42-105">Szeretné telepíteni a Windows, Linux és macOS felhasználók **PowerShell 6** (béta), a számítógépükre, szükséges, hogy:</span><span class="sxs-lookup"><span data-stu-id="e5a42-105">Linux, macOS, and Windows users that would like to install **PowerShell 6** (beta), in their machines, need to:</span></span>

1. <span data-ttu-id="e5a42-106">PowerShell lekérése az adott operációs rendszer és verzió, a [GitHub](https://github.com/powershell/powershell#get-powershell)</span><span class="sxs-lookup"><span data-stu-id="e5a42-106">Get PowerShell for the specific OS and version, from [GitHub](https://github.com/powershell/powershell#get-powershell)</span></span>
1. <span data-ttu-id="e5a42-107">Kövesse a telepítési utasításokat</span><span class="sxs-lookup"><span data-stu-id="e5a42-107">Follow the installation instructions</span></span>
  - [<span data-ttu-id="e5a42-108">Linux</span><span class="sxs-lookup"><span data-stu-id="e5a42-108">Linux</span></span>](https://github.com/PowerShell/PowerShell/blob/master/docs/installation/linux.md)
  - [<span data-ttu-id="e5a42-109">macOS</span><span class="sxs-lookup"><span data-stu-id="e5a42-109">macOS</span></span>](https://github.com/PowerShell/PowerShell/blob/master/docs/installation/linux.md#macos-1012)
  - [<span data-ttu-id="e5a42-110">Windows</span><span class="sxs-lookup"><span data-stu-id="e5a42-110">Windows</span></span>](https://github.com/PowerShell/PowerShell/blob/master/docs/installation/windows.md#msi)

<span data-ttu-id="e5a42-111">PowerShell 6 is rendelkezésre áll, a Docker; Lásd: [Docker telepítési](https://github.com/PowerShell/PowerShell/tree/master/docker) utasításokat.</span><span class="sxs-lookup"><span data-stu-id="e5a42-111">PowerShell 6 is also available for Docker; see [Docker installation](https://github.com/PowerShell/PowerShell/tree/master/docker) instructions.</span></span>

## <a name="finding-powershell-in-windows-10-81-80-and-7"></a><span data-ttu-id="e5a42-112">A Windows 10, 8.1, 8.0 és 7 PowerShell keresése</span><span class="sxs-lookup"><span data-stu-id="e5a42-112">Finding PowerShell in Windows 10, 8.1, 8.0, and 7</span></span>

<span data-ttu-id="e5a42-113">Néha a PowerShell keresése konzol vagy a ISE (integrált parancsfájlkezelési környezet) a Windows nehézségekbe ütközhet, helyének áthelyezése egyik verzióról a Windows a következő módon.</span><span class="sxs-lookup"><span data-stu-id="e5a42-113">Sometimes locating PowerShell console or ISE (Integrated Scripting Environment) in Windows can be difficult, as it's location moves from one version of Windows to the next.</span></span>

<span data-ttu-id="e5a42-114">Az alábbi táblázatok segítséget PowerShell található a Windows-verzió.</span><span class="sxs-lookup"><span data-stu-id="e5a42-114">The following tables should help you find PowerShell in your Windows version.</span></span>
<span data-ttu-id="e5a42-115">Az itt felsorolt összes verzió az eredeti verzió, amelyeket szabaddá, nincsenek frissítések.</span><span class="sxs-lookup"><span data-stu-id="e5a42-115">All versions listed here are the original version, as released, with no updates.</span></span>

### <a name="for-console"></a><span data-ttu-id="e5a42-116">A konzol</span><span class="sxs-lookup"><span data-stu-id="e5a42-116">For Console</span></span>

<span data-ttu-id="e5a42-117">Verzió</span><span class="sxs-lookup"><span data-stu-id="e5a42-117">Version</span></span> | <span data-ttu-id="e5a42-118">Hely</span><span class="sxs-lookup"><span data-stu-id="e5a42-118">Location</span></span>
-- | --
<span data-ttu-id="e5a42-119">Windows-10</span><span class="sxs-lookup"><span data-stu-id="e5a42-119">Windows 10</span></span> | <span data-ttu-id="e5a42-120">Kattintson a bal alsó sarokban Windows ikon, kezdje el begépelni PowerShell</span><span class="sxs-lookup"><span data-stu-id="e5a42-120">Click left lower corner Windows icon, start typing PowerShell</span></span>
<span data-ttu-id="e5a42-121">Windows 8.1, 8.0</span><span class="sxs-lookup"><span data-stu-id="e5a42-121">Windows 8.1, 8.0</span></span> | <span data-ttu-id="e5a42-122">Indítsa el a kezdőképernyőn írja be a PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e5a42-122">On the start screen, start typing PowerShell.</span></span><br/><span data-ttu-id="e5a42-123">Ha a számítógépen, kattintson a bal alsó sarokban Windows ikon kezdje el beírni PowerShell</span><span class="sxs-lookup"><span data-stu-id="e5a42-123">If on desktop, click left lower corner Windows icon, start typing PowerShell</span></span>
<span data-ttu-id="e5a42-124">Windows 7 SP1</span><span class="sxs-lookup"><span data-stu-id="e5a42-124">Windows 7 SP1</span></span> | <span data-ttu-id="e5a42-125">Kattintson a bal alsó sarokban Windows ikonra, a keresési mezőbe írja be a PowerShell elindítása</span><span class="sxs-lookup"><span data-stu-id="e5a42-125">Click left lower corner Windows icon, on the search box start typing PowerShell</span></span>

### <a name="for-ise"></a><span data-ttu-id="e5a42-126">Az ISE</span><span class="sxs-lookup"><span data-stu-id="e5a42-126">For ISE</span></span>

<span data-ttu-id="e5a42-127">Verzió</span><span class="sxs-lookup"><span data-stu-id="e5a42-127">Version</span></span> | <span data-ttu-id="e5a42-128">Hely</span><span class="sxs-lookup"><span data-stu-id="e5a42-128">Location</span></span>
-- | --
<span data-ttu-id="e5a42-129">Windows-10</span><span class="sxs-lookup"><span data-stu-id="e5a42-129">Windows 10</span></span> | <span data-ttu-id="e5a42-130">Kattintson a bal alsó sarokban Windows ikon, kezdje el begépelni az ISE</span><span class="sxs-lookup"><span data-stu-id="e5a42-130">Click left lower corner Windows icon, start typing ISE</span></span>
<span data-ttu-id="e5a42-131">Windows 8.1, 8.0</span><span class="sxs-lookup"><span data-stu-id="e5a42-131">Windows 8.1, 8.0</span></span> | <span data-ttu-id="e5a42-132">A kezdőképernyőn írja be a **PowerShell ISE**.</span><span class="sxs-lookup"><span data-stu-id="e5a42-132">On the start screen, type **PowerShell ISE**.</span></span><br/><span data-ttu-id="e5a42-133">Ha az asztalon kattintson bal alsó sarokban Windows ikonra, írja be a **PowerShell ISE**</span><span class="sxs-lookup"><span data-stu-id="e5a42-133">If on desktop, click left lower corner Windows icon, type **PowerShell ISE**</span></span>
<span data-ttu-id="e5a42-134">Windows 7 SP1</span><span class="sxs-lookup"><span data-stu-id="e5a42-134">Windows 7 SP1</span></span> | <span data-ttu-id="e5a42-135">Kattintson a bal alsó sarokban Windows ikonra, a keresési mezőbe írja be a PowerShell elindítása</span><span class="sxs-lookup"><span data-stu-id="e5a42-135">Click left lower corner Windows icon, on the search box start typing PowerShell</span></span>

## <a name="finding-powershell-in-windows-server-versions"></a><span data-ttu-id="e5a42-136">Windows Server-verziók PowerShell keresése</span><span class="sxs-lookup"><span data-stu-id="e5a42-136">Finding PowerShell in Windows Server versions</span></span>

<span data-ttu-id="e5a42-137">Windows Server 2008 R2 verziótól kezdődően a Windows operációs rendszer nélkül is telepíthetők a grafikus felhasználói felületen (GUI).</span><span class="sxs-lookup"><span data-stu-id="e5a42-137">Starting with Windows Server 2008 R2, Windows operating system can be installed without the graphical user interface (GUI).</span></span>
<span data-ttu-id="e5a42-138">Windows Server a grafikus felhasználói felület nélkül kiadásai megnevezett **Core** és a grafikus felhasználói Felülettel rendelkező kiadásához nevű **asztali**.</span><span class="sxs-lookup"><span data-stu-id="e5a42-138">Editions of Windows Server without GUI are named **Core** editions, and editions with the GUI are named **Desktop**.</span></span>

### <a name="windows-server-core-editions"></a><span data-ttu-id="e5a42-139">Windows Server Core kiadásokban</span><span class="sxs-lookup"><span data-stu-id="e5a42-139">Windows Server Core editions</span></span>

<span data-ttu-id="e5a42-140">Az összes mag kiadásai amikor bejelentkezik a kiszolgáló kap egy Windows parancssori ablakban.</span><span class="sxs-lookup"><span data-stu-id="e5a42-140">In all Core editions, when you log to the server you get a Windows command prompt window.</span></span>

<span data-ttu-id="e5a42-141">Típus `powershell` nyomja le az ENTER **ENTER** PowerShell elindítása belül a parancssor-szakaszt.</span><span class="sxs-lookup"><span data-stu-id="e5a42-141">Type `powershell` and press **ENTER** to start PowerShell inside the command prompt session.</span></span> <span data-ttu-id="e5a42-142">Típus `exit` állítsa le a PowerShell-parancssorba, majd a parancssorba való visszatéréshez.</span><span class="sxs-lookup"><span data-stu-id="e5a42-142">Type `exit` to terminate the PowerShell session and return to command prompt.</span></span>

### <a name="windows-server-desktop-editions"></a><span data-ttu-id="e5a42-143">Windows Server asztali verziója esetén</span><span class="sxs-lookup"><span data-stu-id="e5a42-143">Windows Server Desktop editions</span></span>

<span data-ttu-id="e5a42-144">Összes asztali kiadása kattintson a bal alsó sarokban Windows ikonra kezdje el beírni PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e5a42-144">In all desktop editions, click the left lower corner Windows icon, start typing PowerShell.</span></span>
<span data-ttu-id="e5a42-145">Mind a konzolon, és az ISE-beállítások kapják meg.</span><span class="sxs-lookup"><span data-stu-id="e5a42-145">You get both console and ISE options.</span></span>

<span data-ttu-id="e5a42-146">Az egyetlen kivétel a fenti szabály, a Windows Server 2008 R2 SP1; ISE Ebben az esetben kattintson a bal alsó sarokban Windows ikonra, írja be a PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="e5a42-146">The only exception to the above rule is the ISE in Windows Server 2008 R2 SP1; in this case, click the left lower corner Windows icon, type PowerShell ISE.</span></span>

## <a name="how-to-check-the-version-of-powershell"></a><span data-ttu-id="e5a42-147">Hogyan PowerShell verziójának ellenőrzése</span><span class="sxs-lookup"><span data-stu-id="e5a42-147">How to check the version of PowerShell</span></span>

<span data-ttu-id="e5a42-148">Található PowerShell verziójának telepítését, indítsa el a PowerShell-konzolban (vagy az ISE) és típus `$PSVersionTable` nyomja le az ENTER **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="e5a42-148">To find which version of PowerShell you have installed, start a PowerShell console (or the ISE) and type `$PSVersionTable` and press **ENTER**.</span></span>

## <a name="upgrading-existing-windows-powershell"></a><span data-ttu-id="e5a42-149">Meglévő Windows PowerShell frissítése</span><span class="sxs-lookup"><span data-stu-id="e5a42-149">Upgrading existing Windows PowerShell</span></span>

<span data-ttu-id="e5a42-150">A telepítőcsomag PowerShell belül egy WMF telepítő származnak.</span><span class="sxs-lookup"><span data-stu-id="e5a42-150">The installation package for PowerShell comes inside a WMF installer.</span></span>
<span data-ttu-id="e5a42-151">A WMF installer verziójának ugyanolyan verziójúak, mint a PowerShell; nem önálló telepítő Windows PowerShell van.</span><span class="sxs-lookup"><span data-stu-id="e5a42-151">The version of the WMF installer matches the version of PowerShell; there's no stand alone installer for Windows PowerShell.</span></span>

<span data-ttu-id="e5a42-152">Ha frissítenie kell a meglévő PowerShell, a Windows rendszerben segítségével az alábbi táblázatban keresse meg a telepítő frissíti a PowerShell-verziójának.</span><span class="sxs-lookup"><span data-stu-id="e5a42-152">If you need to update your existing version of PowerShell, in Windows, use the following table to locate the installer for the version of PowerShell you want to update to.</span></span>

<span data-ttu-id="e5a42-153">Windows</span><span class="sxs-lookup"><span data-stu-id="e5a42-153">Windows</span></span> | <span data-ttu-id="e5a42-154">POWERSHELL 3.0</span><span class="sxs-lookup"><span data-stu-id="e5a42-154">PS 3.0</span></span> | <span data-ttu-id="e5a42-155">PS 4.0</span><span class="sxs-lookup"><span data-stu-id="e5a42-155">PS 4.0</span></span> | <span data-ttu-id="e5a42-156">PS 5.0</span><span class="sxs-lookup"><span data-stu-id="e5a42-156">PS 5.0</span></span> | <span data-ttu-id="e5a42-157">PS 5.1</span><span class="sxs-lookup"><span data-stu-id="e5a42-157">PS 5.1</span></span> |
--|--|--|--|--|
<span data-ttu-id="e5a42-158">Windows 10 (lásd a Note1)</span><span class="sxs-lookup"><span data-stu-id="e5a42-158">Windows 10 (see Note1)</span></span><br/><span data-ttu-id="e5a42-159">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="e5a42-159">Windows Server 2016</span></span> | - | - | - | <span data-ttu-id="e5a42-160">telepítve</span><span class="sxs-lookup"><span data-stu-id="e5a42-160">installed</span></span>
<span data-ttu-id="e5a42-161">A Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="e5a42-161">Windows 8.1</span></span><br/><span data-ttu-id="e5a42-162">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="e5a42-162">Windows Server 2012 R2</span></span> | - | <span data-ttu-id="e5a42-163">telepítve</span><span class="sxs-lookup"><span data-stu-id="e5a42-163">installed</span></span> | [<span data-ttu-id="e5a42-164">WMF 5.0</span><span class="sxs-lookup"><span data-stu-id="e5a42-164">WMF 5.0</span></span>](https://www.microsoft.com/en-us/download/details.aspx?id=50395) | [<span data-ttu-id="e5a42-165">WMF 5.1</span><span class="sxs-lookup"><span data-stu-id="e5a42-165">WMF 5.1</span></span>](https://www.microsoft.com/en-us/download/details.aspx?id=54616)
<span data-ttu-id="e5a42-166">Windows 8</span><span class="sxs-lookup"><span data-stu-id="e5a42-166">Windows 8</span></span><br/><span data-ttu-id="e5a42-167">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="e5a42-167">Windows Server 2012</span></span> | <span data-ttu-id="e5a42-168">telepítve</span><span class="sxs-lookup"><span data-stu-id="e5a42-168">installed</span></span> | [<span data-ttu-id="e5a42-169">WMF 4.0</span><span class="sxs-lookup"><span data-stu-id="e5a42-169">WMF 4.0</span></span>](https://www.microsoft.com/en-us/download/details.aspx?id=40855) | [<span data-ttu-id="e5a42-170">WMF 5.0</span><span class="sxs-lookup"><span data-stu-id="e5a42-170">WMF 5.0</span></span>](https://www.microsoft.com/en-us/download/details.aspx?id=50395) | [<span data-ttu-id="e5a42-171">WMF 5.1</span><span class="sxs-lookup"><span data-stu-id="e5a42-171">WMF 5.1</span></span>](https://www.microsoft.com/en-us/download/details.aspx?id=54616)
<span data-ttu-id="e5a42-172">Windows 7 SP1</span><span class="sxs-lookup"><span data-stu-id="e5a42-172">Windows 7 SP1</span></span><br/><span data-ttu-id="e5a42-173">Windows Server 2008 R2 SP1</span><span class="sxs-lookup"><span data-stu-id="e5a42-173">Windows Server 2008 R2 SP1</span></span> | [<span data-ttu-id="e5a42-174">A WMF 3.0</span><span class="sxs-lookup"><span data-stu-id="e5a42-174">WMF 3.0</span></span>](https://www.microsoft.com/en-us/download/details.aspx?id=34595) | [<span data-ttu-id="e5a42-175">WMF 4.0</span><span class="sxs-lookup"><span data-stu-id="e5a42-175">WMF 4.0</span></span>](https://www.microsoft.com/en-us/download/details.aspx?id=40855) | [<span data-ttu-id="e5a42-176">WMF 5.0</span><span class="sxs-lookup"><span data-stu-id="e5a42-176">WMF 5.0</span></span>](https://www.microsoft.com/en-us/download/details.aspx?id=50395) | [<span data-ttu-id="e5a42-177">WMF 5.1</span><span class="sxs-lookup"><span data-stu-id="e5a42-177">WMF 5.1</span></span>](https://www.microsoft.com/en-us/download/details.aspx?id=54616)

> <span data-ttu-id="e5a42-178">**Megjegyzés: 1**:</span><span class="sxs-lookup"><span data-stu-id="e5a42-178">**Note 1**:</span></span>
  >>
  >> <span data-ttu-id="e5a42-179">PowerShell engedélyezve van, az automatikus frissítések szolgáltatással a Windows 10, a kezdeti verzióját a 5.1 5.0-s verziójáról frissíti az lekérdezi.</span><span class="sxs-lookup"><span data-stu-id="e5a42-179">On the initial release of Windows 10, with automatic updates enabled, PowerShell gets updated from version 5.0 to 5.1.</span></span>
  >>
  >> <span data-ttu-id="e5a42-180">Ha a Windows 10 eredeti verzióját nem frissül a Windows-frissítések, a PowerShell verziója 5.0.</span><span class="sxs-lookup"><span data-stu-id="e5a42-180">If the original version of Windows 10 is not updated through Windows Updates, the version of PowerShell is 5.0.</span></span>

## <a name="need-azure-powershell"></a><span data-ttu-id="e5a42-181">Az Azure PowerShell kell</span><span class="sxs-lookup"><span data-stu-id="e5a42-181">Need Azure PowerShell</span></span>

<span data-ttu-id="e5a42-182">Ha a keresett **Azure PowerShell**, sikerült a kiindulási pont [áttekintés az Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure).</span><span class="sxs-lookup"><span data-stu-id="e5a42-182">If you're looking for **Azure PowerShell**, you could start with [Overview of Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure).</span></span>

<span data-ttu-id="e5a42-183">Ellenkező esetben előfordulhat, hogy teendők van [telepítése és konfigurálása az Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps)</span><span class="sxs-lookup"><span data-stu-id="e5a42-183">Otherwise, what you might need is [Install and configure Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps)</span></span>

## <a name="see-also"></a><span data-ttu-id="e5a42-184">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="e5a42-184">See Also</span></span>

- [<span data-ttu-id="e5a42-185">Windows PowerShell rendszerkövetelményei</span><span class="sxs-lookup"><span data-stu-id="e5a42-185">Windows PowerShell System Requirements</span></span>](Windows-PowerShell-System-Requirements.md)
- [<span data-ttu-id="e5a42-186">A Windows PowerShell indítása</span><span class="sxs-lookup"><span data-stu-id="e5a42-186">Starting Windows PowerShell</span></span>](Starting-Windows-PowerShell.md)
