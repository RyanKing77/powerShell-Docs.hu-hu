---
ms.date: 07/10/2019
keywords: a jea, powershell, biztonsági
title: A JEA-Előfeltételek
ms.openlocfilehash: 8fca5c068412e86acfdb8bed400699f721b76191
ms.sourcegitcommit: 46bebe692689ebedfe65ff2c828fe666b443198d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/10/2019
ms.locfileid: "67734291"
---
# <a name="prerequisites"></a><span data-ttu-id="396fd-103">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="396fd-103">Prerequisites</span></span>

<span data-ttu-id="396fd-104">Just Enough Administration lehetővé teszi a PowerShell 5.0-s vagy újabb.</span><span class="sxs-lookup"><span data-stu-id="396fd-104">Just Enough Administration is a feature included in PowerShell 5.0 and higher.</span></span> <span data-ttu-id="396fd-105">Ez a cikk ismerteti az előfeltételeket kell biztosítani a JEA használatának megkezdéséhez.</span><span class="sxs-lookup"><span data-stu-id="396fd-105">This article describes the prerequisites that must be satisfied to start using JEA.</span></span>


## <a name="check-which-version-of-powershell-is-installed"></a><span data-ttu-id="396fd-106">Ellenőrizze, hogy telepítve van a PowerShell-verzió</span><span class="sxs-lookup"><span data-stu-id="396fd-106">Check which version of PowerShell is installed</span></span>

<span data-ttu-id="396fd-107">Ellenőrizze a PowerShell-verzió van telepítve a rendszeren, ellenőrizze a `$PSVersionTable` változót egy Windows PowerShell-parancssort.</span><span class="sxs-lookup"><span data-stu-id="396fd-107">To check which version of PowerShell is installed on your system, check the `$PSVersionTable` variable in a Windows PowerShell prompt.</span></span>

```powershell
$PSVersionTable.PSVersion
```

```Output
Major  Minor  Build  Revision
-----  -----  -----  --------
5      1      14393  1000
```

<span data-ttu-id="396fd-108">A JEA, a PowerShell 5.0-s vagy újabb.</span><span class="sxs-lookup"><span data-stu-id="396fd-108">JEA is available with PowerShell 5.0 and higher.</span></span> <span data-ttu-id="396fd-109">Az összes funkció ajánlott elérhető PowerShell legújabb verzióját telepíti a rendszer.</span><span class="sxs-lookup"><span data-stu-id="396fd-109">For full functionality, it's recommended that you install the latest version of PowerShell available for your system.</span></span> <span data-ttu-id="396fd-110">A következő táblázat ismerteti a JEA a rendelkezésre állás Windows-kiszolgálón:</span><span class="sxs-lookup"><span data-stu-id="396fd-110">The following table describes JEA's availability on Windows Server:</span></span>

| <span data-ttu-id="396fd-111">Kiszolgálóoldali operációs rendszer</span><span class="sxs-lookup"><span data-stu-id="396fd-111">Server Operating System</span></span> |                <span data-ttu-id="396fd-112">A JEA rendelkezésre állása</span><span class="sxs-lookup"><span data-stu-id="396fd-112">JEA Availability</span></span>                |
| ----------------------- | ---------------------------------------------- |
| <span data-ttu-id="396fd-113">Windows Server 2016+</span><span class="sxs-lookup"><span data-stu-id="396fd-113">Windows Server 2016+</span></span>    | <span data-ttu-id="396fd-114">Előtelepített</span><span class="sxs-lookup"><span data-stu-id="396fd-114">Preinstalled</span></span>                                   |
| <span data-ttu-id="396fd-115">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="396fd-115">Windows Server 2012 R2</span></span>  | <span data-ttu-id="396fd-116">A WMF 5.1 összes funkciójának</span><span class="sxs-lookup"><span data-stu-id="396fd-116">Full functionality with WMF 5.1</span></span>                |
| <span data-ttu-id="396fd-117">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="396fd-117">Windows Server 2012</span></span>     | <span data-ttu-id="396fd-118">A WMF 5.1 összes funkciójának</span><span class="sxs-lookup"><span data-stu-id="396fd-118">Full functionality with WMF 5.1</span></span>                |
| <span data-ttu-id="396fd-119">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="396fd-119">Windows Server 2008 R2</span></span>  | <span data-ttu-id="396fd-120">Csökkentett funkciók<sup>1</sup> a WMF 5.1</span><span class="sxs-lookup"><span data-stu-id="396fd-120">Reduced functionality<sup>1</sup> with WMF 5.1</span></span> |

<span data-ttu-id="396fd-121">A JEA a otthoni vagy munkahelyi számítógépen is használhatja:</span><span class="sxs-lookup"><span data-stu-id="396fd-121">You can also use JEA on your home or work computer:</span></span>

| <span data-ttu-id="396fd-122">Ügyfél típusú operációs rendszer</span><span class="sxs-lookup"><span data-stu-id="396fd-122">Client Operating System</span></span> |                   <span data-ttu-id="396fd-123">A JEA rendelkezésre állása</span><span class="sxs-lookup"><span data-stu-id="396fd-123">JEA Availability</span></span>                   |
| ----------------------- | ---------------------------------------------------- |
| <span data-ttu-id="396fd-124">Windows 10 1607+</span><span class="sxs-lookup"><span data-stu-id="396fd-124">Windows 10 1607+</span></span>        | <span data-ttu-id="396fd-125">Előtelepített</span><span class="sxs-lookup"><span data-stu-id="396fd-125">Preinstalled</span></span>                                         |
| <span data-ttu-id="396fd-126">Windows 10 1603, 1511</span><span class="sxs-lookup"><span data-stu-id="396fd-126">Windows 10 1603, 1511</span></span>   | <span data-ttu-id="396fd-127">Előre telepítve, a csökkentett funkciók<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="396fd-127">Preinstalled, with reduced functionality<sup>2</sup></span></span> |
| <span data-ttu-id="396fd-128">Windows 10 1507</span><span class="sxs-lookup"><span data-stu-id="396fd-128">Windows 10 1507</span></span>         | <span data-ttu-id="396fd-129">Nem elérhető el</span><span class="sxs-lookup"><span data-stu-id="396fd-129">Not available</span></span>                                        |
| <span data-ttu-id="396fd-130">A Windows 8, 8.1</span><span class="sxs-lookup"><span data-stu-id="396fd-130">Windows 8, 8.1</span></span>          | <span data-ttu-id="396fd-131">A WMF 5.1 összes funkciójának</span><span class="sxs-lookup"><span data-stu-id="396fd-131">Full functionality with WMF 5.1</span></span>                      |
| <span data-ttu-id="396fd-132">Windows 7</span><span class="sxs-lookup"><span data-stu-id="396fd-132">Windows 7</span></span>               | <span data-ttu-id="396fd-133">Csökkentett funkciók<sup>1</sup> a WMF 5.1</span><span class="sxs-lookup"><span data-stu-id="396fd-133">Reduced functionality<sup>1</sup> with WMF 5.1</span></span>       |

- <span data-ttu-id="396fd-134"><sup>1</sup> JEA csoportosan felügyelt szolgáltatásfiókok használatához a Windows Server 2008 R2 vagy Windows 7-es nem konfigurálható.</span><span class="sxs-lookup"><span data-stu-id="396fd-134"><sup>1</sup> JEA can't be configured to use group-managed service accounts on Windows Server 2008 R2 or Windows 7.</span></span> <span data-ttu-id="396fd-135">A virtuális fiókok és egyéb JEA funkciók *vannak* támogatott.</span><span class="sxs-lookup"><span data-stu-id="396fd-135">Virtual accounts and other JEA features *are* supported.</span></span>

- <span data-ttu-id="396fd-136"><sup>2</sup> a következő JEA-funkciók nem támogatottak a Windows 10-verziók 1511-es és a 1603-as:</span><span class="sxs-lookup"><span data-stu-id="396fd-136"><sup>2</sup> The following JEA features aren't supported on Windows 10 versions 1511 and 1603:</span></span>

  - <span data-ttu-id="396fd-137">A csoportosan felügyelt szolgáltatásfiókként fut</span><span class="sxs-lookup"><span data-stu-id="396fd-137">Running as a group-managed service account</span></span>
  - <span data-ttu-id="396fd-138">Feltételes hozzáférési szabályok a munkamenet-konfigurációk</span><span class="sxs-lookup"><span data-stu-id="396fd-138">Conditional access rules in session configurations</span></span>
  - <span data-ttu-id="396fd-139">A felhasználó meghajtó</span><span class="sxs-lookup"><span data-stu-id="396fd-139">The user drive</span></span>
  - <span data-ttu-id="396fd-140">Helyi felhasználói fiókokhoz való hozzáférést</span><span class="sxs-lookup"><span data-stu-id="396fd-140">Granting access to local user accounts</span></span>

  <span data-ttu-id="396fd-141">Segítségre van szüksége a következő szolgáltatások, 1607-es (Évfordulós frissítés) verzió Windows update vagy újabb verziója.</span><span class="sxs-lookup"><span data-stu-id="396fd-141">To get support for these features, update Windows to version 1607 (Anniversary Update) or higher.</span></span>

### <a name="install-windows-management-framework"></a><span data-ttu-id="396fd-142">Telepítse a Windows Management Framework</span><span class="sxs-lookup"><span data-stu-id="396fd-142">Install Windows Management Framework</span></span>

<span data-ttu-id="396fd-143">Ha a PowerShell egy régebbi verzióját futtatja, szükség lehet a rendszer frissítése a legújabb Windows Management Framework (WMF) frissítéssel.</span><span class="sxs-lookup"><span data-stu-id="396fd-143">If you're running an older version of PowerShell, you may need to update your system with the latest Windows Management Framework (WMF) update.</span></span> <span data-ttu-id="396fd-144">További információkért lásd: a [WMF dokumentáció](/powershell/wmf/overview).</span><span class="sxs-lookup"><span data-stu-id="396fd-144">For more information, see the [WMF documentation](/powershell/wmf/overview).</span></span>

<span data-ttu-id="396fd-145">Javasoljuk, a WMF kompatibilitást a számítási feladat összes kiszolgáló frissítése előtt tesztelje.</span><span class="sxs-lookup"><span data-stu-id="396fd-145">It's recommended that you test your workload's compatibility with WMF before upgrading all of your servers.</span></span>

<span data-ttu-id="396fd-146">Windows 10-es Windows PowerShell aktuális verzióját a legújabb funkciófrissítések kell telepítenie.</span><span class="sxs-lookup"><span data-stu-id="396fd-146">Windows 10 users should install the latest feature updates to obtain the current version of Windows PowerShell.</span></span>

## <a name="enable-powershell-remoting"></a><span data-ttu-id="396fd-147">PowerShell-távelérés engedélyezése</span><span class="sxs-lookup"><span data-stu-id="396fd-147">Enable PowerShell Remoting</span></span>

<span data-ttu-id="396fd-148">PowerShell-táveléréssel az alapokat, amelyen a JEA épül.</span><span class="sxs-lookup"><span data-stu-id="396fd-148">PowerShell Remoting provides the foundation on which JEA is built.</span></span> <span data-ttu-id="396fd-149">Fontos biztosítani kell a PowerShell-táveléréssel engedélyezve van, és megfelelően titkosított a JEA használata előtt.</span><span class="sxs-lookup"><span data-stu-id="396fd-149">It's necessary to ensure PowerShell Remoting is enabled and properly secured before you can use JEA.</span></span> <span data-ttu-id="396fd-150">További információkért lásd: [WinRM biztonsági](/powershell/scripting/learn/remoting/winrmsecurity).</span><span class="sxs-lookup"><span data-stu-id="396fd-150">For more information, see [WinRM Security](/powershell/scripting/learn/remoting/winrmsecurity).</span></span>

<span data-ttu-id="396fd-151">A Windows Server 2012, 2012 R2 és 2016 alapértelmezés szerint engedélyezve van a PowerShell távoli eljáráshívás.</span><span class="sxs-lookup"><span data-stu-id="396fd-151">PowerShell Remoting is enabled by default on Windows Server 2012, 2012 R2, and 2016.</span></span> <span data-ttu-id="396fd-152">PowerShell távoli eljáráshívás engedélyezéséhez futtassa a következő parancsot egy emelt szintű PowerShell-ablakban.</span><span class="sxs-lookup"><span data-stu-id="396fd-152">You can enable PowerShell Remoting by running the following command in an elevated PowerShell window.</span></span>

```powershell
Enable-PSRemoting
```

## <a name="enable-powershell-module-and-script-block-logging-optional"></a><span data-ttu-id="396fd-153">Engedélyezze a PowerShell-modul és a parancsfájl blokk naplózása (nem kötelező)</span><span class="sxs-lookup"><span data-stu-id="396fd-153">Enable PowerShell module and script block logging (optional)</span></span>

<span data-ttu-id="396fd-154">Az alábbi lépésekkel engedélyezheti a rendszer minden PowerShell-műveletek naplózása.</span><span class="sxs-lookup"><span data-stu-id="396fd-154">The following steps enable logging for all PowerShell actions on your system.</span></span> <span data-ttu-id="396fd-155">PowerShell-modul naplózás nem szükséges a jea-t, azonban ajánlott bekapcsolja a naplózást, és győződjön meg arról, a parancsok felhasználók futtatnak egy központi helyen van bejelentkezve.</span><span class="sxs-lookup"><span data-stu-id="396fd-155">PowerShell Module Logging isn't required for JEA, however it's recommended you turn on logging to ensure the commands users run are logged in a central location.</span></span>

<span data-ttu-id="396fd-156">A PowerShell-modul naplózási házirend csoportházirend használatával konfigurálható.</span><span class="sxs-lookup"><span data-stu-id="396fd-156">You can configure the PowerShell Module Logging policy using Group Policy.</span></span>

1. <span data-ttu-id="396fd-157">Nyissa meg a Helyicsoportházirend-szerkesztő a munkaállomásokon vagy csoportházirend-objektum az Active Directory-tartományvezérlő a Csoportházirend kezelése konzolt</span><span class="sxs-lookup"><span data-stu-id="396fd-157">Open the Local Group Policy Editor on a workstation or a Group Policy Object in the Group Policy Management Console on an Active Directory Domain Controller</span></span>
2. <span data-ttu-id="396fd-158">Navigáljon a **számítógép konfigurációja\\felügyeleti sablonok\\Windows-összetevők\\Windows PowerShell**</span><span class="sxs-lookup"><span data-stu-id="396fd-158">Navigate to **Computer Configuration\\Administrative Templates\\Windows Components\\Windows PowerShell**</span></span>
3. <span data-ttu-id="396fd-159">Kattintson duplán a **modul naplózás bekapcsolása**</span><span class="sxs-lookup"><span data-stu-id="396fd-159">Double-click on **Turn on Module Logging**</span></span>
4. <span data-ttu-id="396fd-160">Kattintson a **engedélyezve**</span><span class="sxs-lookup"><span data-stu-id="396fd-160">Click **Enabled**</span></span>
5. <span data-ttu-id="396fd-161">Ebben a szakaszban, kattintson a **megjelenítése** Modulneveket mellett</span><span class="sxs-lookup"><span data-stu-id="396fd-161">In the Options section, click on **Show** next to Module Names</span></span>
6. <span data-ttu-id="396fd-162">Típus `*` a felugró ablakban parancsokat az összes modulok bejelentkezni.</span><span class="sxs-lookup"><span data-stu-id="396fd-162">Type `*` in the pop-up window to log commands from all modules.</span></span>
7. <span data-ttu-id="396fd-163">Kattintson a **OK** házirend beállítása</span><span class="sxs-lookup"><span data-stu-id="396fd-163">Click **OK** to set the policy</span></span>
8. <span data-ttu-id="396fd-164">Kattintson duplán a **PowerShell parancsprogram-blokkot naplózás bekapcsolása**</span><span class="sxs-lookup"><span data-stu-id="396fd-164">Double-click on **Turn on PowerShell Script Block Logging**</span></span>
9. <span data-ttu-id="396fd-165">Kattintson a **engedélyezve**</span><span class="sxs-lookup"><span data-stu-id="396fd-165">Click **Enabled**</span></span>
10. <span data-ttu-id="396fd-166">Kattintson a **OK** házirend beállítása</span><span class="sxs-lookup"><span data-stu-id="396fd-166">Click **OK** to set the policy</span></span>
11. <span data-ttu-id="396fd-167">(A tartományhoz csatlakoztatott gépeket csak) Futtatás `gpupdate` vagy várjon, amíg a csoportházirend segítségével dolgozza fel a frissített szabályzatot, és a alkalmazni a beállításokat</span><span class="sxs-lookup"><span data-stu-id="396fd-167">(On domain-joined machines only) Run `gpupdate` or wait for Group Policy to process the updated policy and apply the settings</span></span>

<span data-ttu-id="396fd-168">Rendszerszintű PowerShell beszédátírási csoportházirenden keresztül is engedélyezheti.</span><span class="sxs-lookup"><span data-stu-id="396fd-168">You can also enable system-wide PowerShell transcription through Group Policy.</span></span>

## <a name="next-steps"></a><span data-ttu-id="396fd-169">További lépések</span><span class="sxs-lookup"><span data-stu-id="396fd-169">Next steps</span></span>

[<span data-ttu-id="396fd-170">Hozzon létre egy szerepkört képesség fájlt</span><span class="sxs-lookup"><span data-stu-id="396fd-170">Create a role capability file</span></span>](role-capabilities.md)

[<span data-ttu-id="396fd-171">Egy munkamenet-konfigurációs fájl létrehozása</span><span class="sxs-lookup"><span data-stu-id="396fd-171">Create a session configuration file</span></span>](session-configurations.md)

## <a name="see-also"></a><span data-ttu-id="396fd-172">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="396fd-172">See also</span></span>

[<span data-ttu-id="396fd-173">A WinRM-biztonság</span><span class="sxs-lookup"><span data-stu-id="396fd-173">WinRM Security</span></span>](/powershell/scripting/learn/remoting/winrmsecurity)

[<span data-ttu-id="396fd-174">PowerShell ♥ a kék csapat</span><span class="sxs-lookup"><span data-stu-id="396fd-174">PowerShell ♥ the Blue Team</span></span>](https://devblogs.microsoft.com/powershell/powershell-the-blue-team/)
