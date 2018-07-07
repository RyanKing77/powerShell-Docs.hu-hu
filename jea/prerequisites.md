---
ms.date: 06/12/2017
keywords: a jea, powershell, biztonsági
title: A JEA-Előfeltételek
ms.openlocfilehash: acc16c0c7eec357b621c0706a66b8752ae5578cd
ms.sourcegitcommit: 8b076ebde7ef971d7465bab834a3c2a32471ef6f
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/06/2018
ms.locfileid: "37893035"
---
# <a name="prerequisites"></a><span data-ttu-id="8d5be-103">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="8d5be-103">Prerequisites</span></span>

> <span data-ttu-id="8d5be-104">A következőkre vonatkozik: Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="8d5be-104">Applies to: Windows PowerShell 5.0</span></span>

<span data-ttu-id="8d5be-105">Just Enough Administration lehetővé teszi a Windows PowerShell 5.0-s vagy újabb.</span><span class="sxs-lookup"><span data-stu-id="8d5be-105">Just Enough Administration is a feature included with Windows PowerShell 5.0 and higher.</span></span>
<span data-ttu-id="8d5be-106">Ez a témakör ismerteti az előfeltételeket kell biztosítani a JEA használatának elkezdéséhez.</span><span class="sxs-lookup"><span data-stu-id="8d5be-106">This topic describes the prerequisites that must be satisfied in order to start using JEA.</span></span>

## <a name="install-jea"></a><span data-ttu-id="8d5be-107">A JEA telepítése</span><span class="sxs-lookup"><span data-stu-id="8d5be-107">Install JEA</span></span>

<span data-ttu-id="8d5be-108">A JEA elérhető Windows PowerShell 5.0-s vagy újabb, de a teljes funkció ajánlott elérhető PowerShell legújabb verzióját telepíti a rendszer.</span><span class="sxs-lookup"><span data-stu-id="8d5be-108">JEA is available with Windows PowerShell 5.0 and higher, but for full functionality it is recommended that you install the latest version of PowerShell available for your system.</span></span>
<span data-ttu-id="8d5be-109">A következő táblázat ismerteti a JEA a rendelkezésre állás Windows-kiszolgálón:</span><span class="sxs-lookup"><span data-stu-id="8d5be-109">The following table describes JEA's availability on Windows Server:</span></span>

<span data-ttu-id="8d5be-110">Kiszolgálóoldali operációs rendszer</span><span class="sxs-lookup"><span data-stu-id="8d5be-110">Server Operating System</span></span>   | <span data-ttu-id="8d5be-111">A JEA rendelkezésre állása</span><span class="sxs-lookup"><span data-stu-id="8d5be-111">JEA Availability</span></span>
--------------------------|--------------------------------
<span data-ttu-id="8d5be-112">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="8d5be-112">Windows Server 2016</span></span>       | <span data-ttu-id="8d5be-113">Előtelepített</span><span class="sxs-lookup"><span data-stu-id="8d5be-113">Preinstalled</span></span>
<span data-ttu-id="8d5be-114">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="8d5be-114">Windows Server 2012 R2</span></span>    | <span data-ttu-id="8d5be-115">A WMF 5.1 összes funkciójának</span><span class="sxs-lookup"><span data-stu-id="8d5be-115">Full functionality with WMF 5.1</span></span>
<span data-ttu-id="8d5be-116">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="8d5be-116">Windows Server 2012</span></span>       | <span data-ttu-id="8d5be-117">A WMF 5.1 összes funkciójának</span><span class="sxs-lookup"><span data-stu-id="8d5be-117">Full functionality with WMF 5.1</span></span>
<span data-ttu-id="8d5be-118">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="8d5be-118">Windows Server 2008 R2</span></span>    | <span data-ttu-id="8d5be-119">Csökkentett funkciók<sup>1</sup> a WMF 5.1</span><span class="sxs-lookup"><span data-stu-id="8d5be-119">Reduced functionality<sup>1</sup> with WMF 5.1</span></span>

<span data-ttu-id="8d5be-120">A JEA a otthoni vagy munkahelyi számítógépen is használhatja:</span><span class="sxs-lookup"><span data-stu-id="8d5be-120">You can also use JEA on your home or work computer:</span></span>

<span data-ttu-id="8d5be-121">Ügyfél típusú operációs rendszer</span><span class="sxs-lookup"><span data-stu-id="8d5be-121">Client Operating System</span></span>   | <span data-ttu-id="8d5be-122">A JEA rendelkezésre állása</span><span class="sxs-lookup"><span data-stu-id="8d5be-122">JEA Availability</span></span>
--------------------------|-----------------------------------------------------
<span data-ttu-id="8d5be-123">Windows 10 1607+</span><span class="sxs-lookup"><span data-stu-id="8d5be-123">Windows 10 1607+</span></span>          | <span data-ttu-id="8d5be-124">Előtelepített</span><span class="sxs-lookup"><span data-stu-id="8d5be-124">Preinstalled</span></span>
<span data-ttu-id="8d5be-125">Windows 10 1603, 1511</span><span class="sxs-lookup"><span data-stu-id="8d5be-125">Windows 10 1603, 1511</span></span>     | <span data-ttu-id="8d5be-126">Előre telepítve, a csökkentett funkciók<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="8d5be-126">Preinstalled, with reduced functionality<sup>2</sup></span></span>
<span data-ttu-id="8d5be-127">A Windows 10 1507-es</span><span class="sxs-lookup"><span data-stu-id="8d5be-127">Windows 10 1507</span></span>           | <span data-ttu-id="8d5be-128">Nem elérhető el</span><span class="sxs-lookup"><span data-stu-id="8d5be-128">Not available</span></span>
<span data-ttu-id="8d5be-129">A Windows 8, 8.1</span><span class="sxs-lookup"><span data-stu-id="8d5be-129">Windows 8, 8.1</span></span>            | <span data-ttu-id="8d5be-130">A WMF 5.1 összes funkciójának</span><span class="sxs-lookup"><span data-stu-id="8d5be-130">Full functionality with WMF 5.1</span></span>
<span data-ttu-id="8d5be-131">Windows 7</span><span class="sxs-lookup"><span data-stu-id="8d5be-131">Windows 7</span></span>                 | <span data-ttu-id="8d5be-132">Csökkentett funkciók<sup>1</sup> a WMF 5.1</span><span class="sxs-lookup"><span data-stu-id="8d5be-132">Reduced functionality<sup>1</sup> with WMF 5.1</span></span>

<span data-ttu-id="8d5be-133"><sup>1</sup> JEA csoportosan felügyelt szolgáltatásfiókok használatához a Windows Server 2008 R2 vagy Windows 7-es nem konfigurálható.</span><span class="sxs-lookup"><span data-stu-id="8d5be-133"><sup>1</sup> JEA cannot be configured to use group managed service accounts on Windows Server 2008 R2 or Windows 7.</span></span>
<span data-ttu-id="8d5be-134">A virtuális fiókok és egyéb JEA funkciók *vannak* támogatott.</span><span class="sxs-lookup"><span data-stu-id="8d5be-134">Virtual accounts and other JEA features *are* supported.</span></span>

<span data-ttu-id="8d5be-135"><sup>2</sup> 1511-es és a 1603-as Windows 10-verziók nem támogatják az alábbi JEA szolgáltatások: fut, a csoportosan felügyelt szolgáltatásfiók, a feltételes hozzáférési szabályok a munkamenet-konfigurációk, a felhasználó meghajtó és a helyi felhasználói fiókokhoz való hozzáférést.</span><span class="sxs-lookup"><span data-stu-id="8d5be-135"><sup>2</sup> Windows 10 versions 1511 and 1603 do not support the following JEA features: running as a group managed service account, conditional access rules in session configurations, the user drive, and granting access to local user accounts.</span></span>
<span data-ttu-id="8d5be-136">Segítségre van szüksége a következő szolgáltatások, 1607-es (Évfordulós frissítés) verzió Windows update vagy újabb verziója.</span><span class="sxs-lookup"><span data-stu-id="8d5be-136">To get support for these features, update Windows to version 1607 (Anniversary Update) or higher.</span></span>

### <a name="check-which-version-of-powershell-is-installed"></a><span data-ttu-id="8d5be-137">Ellenőrizze, hogy telepítve van a PowerShell-verzió</span><span class="sxs-lookup"><span data-stu-id="8d5be-137">Check which version of PowerShell is installed</span></span>

<span data-ttu-id="8d5be-138">Ellenőrizze a PowerShell-verzió van telepítve a rendszeren, ellenőrizze a `$PSVersionTable` változót egy Windows PowerShell-parancssort.</span><span class="sxs-lookup"><span data-stu-id="8d5be-138">To check which version of PowerShell is installed on your system, check the `$PSVersionTable` variable in a Windows PowerShell prompt.</span></span>

```powershell
$PSVersionTable.PSVersion
```

```output
Major  Minor  Build  Revision
-----  -----  -----  --------
5      1      14393  1000
```

<span data-ttu-id="8d5be-139">A JEA használata, ha készen áll a *fő* verziószáma nagyobb vagy azzal egyenlőnek **5**.</span><span class="sxs-lookup"><span data-stu-id="8d5be-139">You are ready to use JEA if the *Major* version is equal to or greater than **5**.</span></span>
<span data-ttu-id="8d5be-140">A legjobb élményt, és a legújabb funkciók eléréséhez, frissítése a PowerShell-verzió ajánlott **5.1** amikor csak lehetséges.</span><span class="sxs-lookup"><span data-stu-id="8d5be-140">For the best experience, and to have access to all the latest features, it is recommended that you upgrade to PowerShell version **5.1** when possible.</span></span>

### <a name="install-windows-management-framework"></a><span data-ttu-id="8d5be-141">Telepítse a Windows Management Framework</span><span class="sxs-lookup"><span data-stu-id="8d5be-141">Install Windows Management Framework</span></span>

<span data-ttu-id="8d5be-142">Ha a PowerShell egy régebbi verzióját futtatja, a rendszer frissítése a legújabb Windows Management Framework (WMF) frissítéssel kell.</span><span class="sxs-lookup"><span data-stu-id="8d5be-142">If you are running an older version of PowerShell, you will need to update your system with the latest Windows Management Framework (WMF) update.</span></span>
<span data-ttu-id="8d5be-143">Csomagok és a egy hivatkozást a WMF legújabb kibocsátási megjegyzéseinek érhető el a [letöltőközpontból](https://blogs.msdn.microsoft.com/powershell/2016/02/24/windows-management-framework-wmf-5-0-rtm-packages-has-been-republished/).</span><span class="sxs-lookup"><span data-stu-id="8d5be-143">Update packages and a link to the latest WMF release notes are available in the [Download Center](https://blogs.msdn.microsoft.com/powershell/2016/02/24/windows-management-framework-wmf-5-0-rtm-packages-has-been-republished/).</span></span>

<span data-ttu-id="8d5be-144">Erősen ajánlott, a WMF kompatibilitást a számítási feladat összes kiszolgáló frissítése előtt tesztelje.</span><span class="sxs-lookup"><span data-stu-id="8d5be-144">It is strongly recommended that you test your workload's compatibility with WMF before upgrading all of your servers.</span></span>

<span data-ttu-id="8d5be-145">Windows 10-es Windows PowerShell aktuális verzióját a legújabb funkciófrissítések kell telepítenie.</span><span class="sxs-lookup"><span data-stu-id="8d5be-145">Windows 10 users should install the latest feature updates to obtain the current version of Windows PowerShell.</span></span>

## <a name="enable-powershell-remoting"></a><span data-ttu-id="8d5be-146">PowerShell-távelérés engedélyezése</span><span class="sxs-lookup"><span data-stu-id="8d5be-146">Enable PowerShell Remoting</span></span>

<span data-ttu-id="8d5be-147">PowerShell-táveléréssel az alapokat, amelyen a JEA épül.</span><span class="sxs-lookup"><span data-stu-id="8d5be-147">PowerShell Remoting provides the foundation on which JEA is built.</span></span>
<span data-ttu-id="8d5be-148">Ezért elengedhetetlen, annak érdekében, hogy engedélyezve van a PowerShell-táveléréssel, és [megfelelően védett](/powershell/scripting/setup/winrmsecurity) JEA használata előtt a rendszer.</span><span class="sxs-lookup"><span data-stu-id="8d5be-148">It is therefore necessary to ensure PowerShell Remoting is enabled and [properly secured](/powershell/scripting/setup/winrmsecurity) on your system before you can use JEA.</span></span>

<span data-ttu-id="8d5be-149">A Windows Server 2012, 2012 R2 és 2016 alapértelmezés szerint engedélyezve van a PowerShell távoli eljáráshívás.</span><span class="sxs-lookup"><span data-stu-id="8d5be-149">PowerShell Remoting is enabled by default on Windows Server 2012, 2012 R2, and 2016.</span></span>
<span data-ttu-id="8d5be-150">PowerShell távoli eljáráshívás engedélyezéséhez futtassa a következő parancsot egy emelt szintű PowerShell-ablakban.</span><span class="sxs-lookup"><span data-stu-id="8d5be-150">You can enable PowerShell Remoting by running the following command in an elevated PowerShell window.</span></span>

```powershell
Enable-PSRemoting
```

## <a name="enable-powershell-module-and-script-block-logging-optional"></a><span data-ttu-id="8d5be-151">Engedélyezze a PowerShell-modul és a parancsfájl blokk naplózása (nem kötelező)</span><span class="sxs-lookup"><span data-stu-id="8d5be-151">Enable PowerShell module and script block logging (optional)</span></span>

<span data-ttu-id="8d5be-152">Az alábbi lépésekkel engedélyezheti a rendszer minden PowerShell-műveletek naplózása.</span><span class="sxs-lookup"><span data-stu-id="8d5be-152">The following steps enable logging for all PowerShell actions on your system.</span></span>
<span data-ttu-id="8d5be-153">PowerShell-modul naplózás nem szükséges a jea-t, azonban erősen ajánlott bekapcsolni, annak érdekében, hogy a parancsok felhasználók futtatnak egy központi helyen van bejelentkezve.</span><span class="sxs-lookup"><span data-stu-id="8d5be-153">PowerShell Module Logging is not required for JEA, however it is strongly recommended that you turn it on to ensure the commands users run are logged in a central location.</span></span>

<span data-ttu-id="8d5be-154">A PowerShell-modul naplózási házirend csoportházirend használatával konfigurálható.</span><span class="sxs-lookup"><span data-stu-id="8d5be-154">You can configure the PowerShell Module Logging policy using Group Policy.</span></span>

1. <span data-ttu-id="8d5be-155">Nyissa meg a Helyicsoportházirend-szerkesztő a munkaállomásokon vagy csoportházirend-objektum az Active Directory-tartományvezérlő a Csoportházirend kezelése konzolt</span><span class="sxs-lookup"><span data-stu-id="8d5be-155">Open the Local Group Policy Editor on a workstation or a Group Policy Object in the Group Policy Management Console on an Active Directory Domain Controller</span></span>
2. <span data-ttu-id="8d5be-156">Navigáljon a **számítógép konfigurációja\\felügyeleti sablonok\\Windows-összetevők\\Windows PowerShell**</span><span class="sxs-lookup"><span data-stu-id="8d5be-156">Navigate to **Computer Configuration\\Administrative Templates\\Windows Components\\Windows PowerShell**</span></span>
3. <span data-ttu-id="8d5be-157">Kattintson duplán a **modul naplózás bekapcsolása**</span><span class="sxs-lookup"><span data-stu-id="8d5be-157">Double click on **Turn on Module Logging**</span></span>
4. <span data-ttu-id="8d5be-158">Kattintson a **engedélyezve**</span><span class="sxs-lookup"><span data-stu-id="8d5be-158">Click **Enabled**</span></span>
5. <span data-ttu-id="8d5be-159">Ebben a szakaszban, kattintson a **megjelenítése** Modulneveket mellett</span><span class="sxs-lookup"><span data-stu-id="8d5be-159">In the Options section, click on **Show** next to Module Names</span></span>
6. <span data-ttu-id="8d5be-160">Típus `\*` az előugró ablakban.</span><span class="sxs-lookup"><span data-stu-id="8d5be-160">Type `\*` in the pop up window.</span></span> <span data-ttu-id="8d5be-161">Ezzel arra utasítja a PowerShell-parancsokat az összes modulok bejelentkezni.</span><span class="sxs-lookup"><span data-stu-id="8d5be-161">This instructs PowerShell to log commands from all modules.</span></span>
7. <span data-ttu-id="8d5be-162">Kattintson a **OK** házirend beállítása</span><span class="sxs-lookup"><span data-stu-id="8d5be-162">Click **OK** to set the policy</span></span>
8. <span data-ttu-id="8d5be-163">Kattintson duplán a **PowerShell parancsfájl-blokk naplózás bekapcsolása**</span><span class="sxs-lookup"><span data-stu-id="8d5be-163">Double click on **Turn on PowerShell Script Block Logging**</span></span>
9. <span data-ttu-id="8d5be-164">Kattintson a **engedélyezve**</span><span class="sxs-lookup"><span data-stu-id="8d5be-164">Click **Enabled**</span></span>
10. <span data-ttu-id="8d5be-165">Kattintson a **OK** házirend beállítása</span><span class="sxs-lookup"><span data-stu-id="8d5be-165">Click **OK** to set the policy</span></span>
11. <span data-ttu-id="8d5be-166">(A tartományhoz csatlakoztatott gépeket csak) Futtatás `gpupdate` vagy várjon, amíg a csoportházirend segítségével dolgozza fel a frissített szabályzatot, és a alkalmazni a beállításokat</span><span class="sxs-lookup"><span data-stu-id="8d5be-166">(On domain-joined machines only) Run `gpupdate` or wait for Group Policy to process the updated policy and apply the settings</span></span>

<span data-ttu-id="8d5be-167">Rendszerszintű PowerShell beszédátírási csoportházirenden keresztül is engedélyezheti.</span><span class="sxs-lookup"><span data-stu-id="8d5be-167">You can also enable system-wide PowerShell transcription through Group Policy.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8d5be-168">További lépések</span><span class="sxs-lookup"><span data-stu-id="8d5be-168">Next steps</span></span>

[<span data-ttu-id="8d5be-169">Hozzon létre egy szerepkört képesség fájlt</span><span class="sxs-lookup"><span data-stu-id="8d5be-169">Create a role capability file</span></span>](role-capabilities.md)

[<span data-ttu-id="8d5be-170">Egy munkamenet-konfigurációs fájl létrehozása</span><span class="sxs-lookup"><span data-stu-id="8d5be-170">Create a session configuration file</span></span>](session-configurations.md)

## <a name="see-also"></a><span data-ttu-id="8d5be-171">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="8d5be-171">See also</span></span>

[<span data-ttu-id="8d5be-172">További információt a PowerShell-táveléréssel, és a Rendszerfelügyeleti webszolgáltatások biztonsági</span><span class="sxs-lookup"><span data-stu-id="8d5be-172">Additional information about PowerShell Remoting and WinRM security</span></span>](/powershell/scripting/setup/winrmsecurity)

[<span data-ttu-id="8d5be-173">*PowerShell a kék csapat ♥* biztonsági blogbejegyzés</span><span class="sxs-lookup"><span data-stu-id="8d5be-173">*PowerShell ♥ the Blue Team* blog post on security</span></span>](https://blogs.msdn.microsoft.com/powershell/2015/06/09/powershell-the-blue-team/)