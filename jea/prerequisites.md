---
ms.date: 2017-06-12
author: rpsqrd
ms.topic: conceptual
keywords: "jea, a powershell, a biztonsági"
title: "JEA Előfeltételek"
ms.openlocfilehash: e6ee16e34eb9f1f0b2f3601c1aa9e90ab4f785f1
ms.sourcegitcommit: 99227f62dcf827354770eb2c3e95c5cf6a3118b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/15/2018
---
# <a name="prerequisites"></a><span data-ttu-id="03366-103">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="03366-103">Prerequisites</span></span>

> <span data-ttu-id="03366-104">A következőkre vonatkozik: a Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="03366-104">Applies to: Windows PowerShell 5.0</span></span>

<span data-ttu-id="03366-105">Csak elég felügyeleti lehetővé teszi a Windows PowerShell 5.0-s és újabb rendszer.</span><span class="sxs-lookup"><span data-stu-id="03366-105">Just Enough Administration is a feature included with Windows PowerShell 5.0 and higher.</span></span>
<span data-ttu-id="03366-106">Ez a témakör ismerteti az előfeltételeket, amelyeket meg kell felelniük ahhoz, hogy a JEA használatának megkezdéséhez.</span><span class="sxs-lookup"><span data-stu-id="03366-106">This topic describes the prerequisites that must be satisfied in order to start using JEA.</span></span>

## <a name="install-jea"></a><span data-ttu-id="03366-107">JEA telepítése</span><span class="sxs-lookup"><span data-stu-id="03366-107">Install JEA</span></span>

<span data-ttu-id="03366-108">JEA elérhető Windows PowerShell 5.0-s és újabb, de az összes funkció javasoljuk, hogy telepítse a PowerShell elérhető legújabb verzióját a rendszer.</span><span class="sxs-lookup"><span data-stu-id="03366-108">JEA is available with Windows PowerShell 5.0 and higher, but for full functionality it is recommended that you install the latest version of PowerShell available for your system.</span></span>
<span data-ttu-id="03366-109">Az alábbi táblázat a Windows Server JEA tartozó rendelkezésre állási ismerteti:</span><span class="sxs-lookup"><span data-stu-id="03366-109">The following table describes JEA's availability on Windows Server:</span></span>

<span data-ttu-id="03366-110">Kiszolgálói operációs rendszer</span><span class="sxs-lookup"><span data-stu-id="03366-110">Server Operating System</span></span>   | <span data-ttu-id="03366-111">JEA rendelkezésre állása</span><span class="sxs-lookup"><span data-stu-id="03366-111">JEA Availability</span></span>
--------------------------|--------------------------------
<span data-ttu-id="03366-112">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="03366-112">Windows Server 2016</span></span>       | <span data-ttu-id="03366-113">Előre telepítve</span><span class="sxs-lookup"><span data-stu-id="03366-113">Preinstalled</span></span>
<span data-ttu-id="03366-114">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="03366-114">Windows Server 2012 R2</span></span>    | <span data-ttu-id="03366-115">A WMF 5.1 összes funkcióját</span><span class="sxs-lookup"><span data-stu-id="03366-115">Full functionality with WMF 5.1</span></span>
<span data-ttu-id="03366-116">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="03366-116">Windows Server 2012</span></span>       | <span data-ttu-id="03366-117">A WMF 5.1 összes funkcióját</span><span class="sxs-lookup"><span data-stu-id="03366-117">Full functionality with WMF 5.1</span></span>
<span data-ttu-id="03366-118">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="03366-118">Windows Server 2008 R2</span></span>    | <span data-ttu-id="03366-119">Csökkentett funkció<sup>1</sup> a WMF 5.1</span><span class="sxs-lookup"><span data-stu-id="03366-119">Reduced functionality<sup>1</sup> with WMF 5.1</span></span>

<span data-ttu-id="03366-120">Otthoni vagy munkahelyi számítógépen JEA használhatja:</span><span class="sxs-lookup"><span data-stu-id="03366-120">You can also use JEA on your home or work computer:</span></span>

<span data-ttu-id="03366-121">Ügyfél típusú operációs rendszer</span><span class="sxs-lookup"><span data-stu-id="03366-121">Client Operating System</span></span>   | <span data-ttu-id="03366-122">JEA rendelkezésre állása</span><span class="sxs-lookup"><span data-stu-id="03366-122">JEA Availability</span></span>
--------------------------|-----------------------------------------------------
<span data-ttu-id="03366-123">Windows 10 1607+</span><span class="sxs-lookup"><span data-stu-id="03366-123">Windows 10 1607+</span></span>          | <span data-ttu-id="03366-124">Előre telepítve</span><span class="sxs-lookup"><span data-stu-id="03366-124">Preinstalled</span></span>
<span data-ttu-id="03366-125">Windows 10 1603, 1511</span><span class="sxs-lookup"><span data-stu-id="03366-125">Windows 10 1603, 1511</span></span>     | <span data-ttu-id="03366-126">Előtelepített, csökken funkció<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="03366-126">Preinstalled, with reduced functionality<sup>2</sup></span></span>
<span data-ttu-id="03366-127">Windows 10 1507</span><span class="sxs-lookup"><span data-stu-id="03366-127">Windows 10 1507</span></span>           | <span data-ttu-id="03366-128">Nem elérhető el</span><span class="sxs-lookup"><span data-stu-id="03366-128">Not available</span></span>
<span data-ttu-id="03366-129">Windows 8, 8.1</span><span class="sxs-lookup"><span data-stu-id="03366-129">Windows 8, 8.1</span></span>            | <span data-ttu-id="03366-130">A WMF 5.1 összes funkcióját</span><span class="sxs-lookup"><span data-stu-id="03366-130">Full functionality with WMF 5.1</span></span>
<span data-ttu-id="03366-131">Windows 7</span><span class="sxs-lookup"><span data-stu-id="03366-131">Windows 7</span></span>                 | <span data-ttu-id="03366-132">Csökkentett funkció<sup>1</sup> a WMF 5.1</span><span class="sxs-lookup"><span data-stu-id="03366-132">Reduced functionality<sup>1</sup> with WMF 5.1</span></span>

<span data-ttu-id="03366-133"><sup>1</sup> JEA csoportosan felügyelt szolgáltatásfiókok használatához Windows Server 2008 R2 vagy Windows 7 nem konfigurálható.</span><span class="sxs-lookup"><span data-stu-id="03366-133"><sup>1</sup> JEA cannot be configured to use group managed service accounts on Windows Server 2008 R2 or Windows 7.</span></span>
<span data-ttu-id="03366-134">Virtuális fiókok és egyéb JEA szolgáltatások *vannak* támogatott.</span><span class="sxs-lookup"><span data-stu-id="03366-134">Virtual accounts and other JEA features *are* supported.</span></span>

<span data-ttu-id="03366-135"><sup>2</sup> 1511-es és a 1603-as Windows 10-verziók nem támogatják a következő JEA: egy olyan csoport által felügyelt szolgáltatásfiókot, a munkamenet-konfigurációk feltételes hozzáférési szabályai, a felhasználó és helyi felhasználói fiókokhoz történő hozzáférés futtatnia.</span><span class="sxs-lookup"><span data-stu-id="03366-135"><sup>2</sup> Windows 10 versions 1511 and 1603 do not support the following JEA features: running as a group managed service account, conditional access rules in session configurations, the user drive, and granting access to local user accounts.</span></span>
<span data-ttu-id="03366-136">Segítségre van szüksége a következő szolgáltatások, a Windows frissítése verzióra 1607 (évforduló frissítése) vagy újabb verzióját.</span><span class="sxs-lookup"><span data-stu-id="03366-136">To get support for these features, update Windows to version 1607 (Anniversary Update) or higher.</span></span>

### <a name="check-which-version-of-powershell-is-installed"></a><span data-ttu-id="03366-137">Ellenőrizze, hogy mely PowerShell verziója telepítve van</span><span class="sxs-lookup"><span data-stu-id="03366-137">Check which version of PowerShell is installed</span></span>

<span data-ttu-id="03366-138">Annak ellenőrzése, PowerShell verziójának telepítve van a rendszeren, ellenőrizze, hogy a `$PSVersionTable` változó a Windows PowerShell-parancssorban.</span><span class="sxs-lookup"><span data-stu-id="03366-138">To check which version of PowerShell is installed on your system, check the `$PSVersionTable` variable in a Windows PowerShell prompt.</span></span>

```powershell
PS C:\> $PSVersionTable.PSVersion

Major  Minor  Build  Revision
-----  -----  -----  --------
5      1      14393  1000
```

<span data-ttu-id="03366-139">A JEA használatára, ha készen áll a *fő* verziószáma kisebb mint **5**.</span><span class="sxs-lookup"><span data-stu-id="03366-139">You are ready to use JEA if the *Major* version is equal to or greater than **5**.</span></span>
<span data-ttu-id="03366-140">A legjobb élményt, és a legújabb szolgáltatásokhoz való hozzáférést, javasoljuk, hogy PowerShell verzióra frissít **5.1** amikor lehetséges.</span><span class="sxs-lookup"><span data-stu-id="03366-140">For the best experience, and to have access to all the latest features, it is recommended that you upgrade to PowerShell version **5.1** when possible.</span></span>

### <a name="install-windows-management-framework"></a><span data-ttu-id="03366-141">A Windows Management Framework telepítése</span><span class="sxs-lookup"><span data-stu-id="03366-141">Install Windows Management Framework</span></span>

<span data-ttu-id="03366-142">Ha PowerShell régebbi verzióját futtatja, akkor frissítse rendszerét a Windows Management Framework (WMF) legfrissebb.</span><span class="sxs-lookup"><span data-stu-id="03366-142">If you are running an older version of PowerShell, you will need to update your system with the latest Windows Management Framework (WMF) update.</span></span>
<span data-ttu-id="03366-143">Frissítési csomagok és egy hivatkozást a WMF legújabb kibocsátási megjegyzésekben érhetők el a [letöltőközpontból](https://aka.ms/WMF5).</span><span class="sxs-lookup"><span data-stu-id="03366-143">Update packages and a link to the latest WMF release notes are available in the [Download Center](https://aka.ms/WMF5).</span></span>

<span data-ttu-id="03366-144">A számítási kompatibilitást WMF tesztelni az összes kiszolgáló frissítése előtt erősen ajánlott.</span><span class="sxs-lookup"><span data-stu-id="03366-144">It is strongly recommended that you test your workload's compatibility with WMF before upgrading all of your servers.</span></span>

<span data-ttu-id="03366-145">Windows 10 kell telepíteni a legújabb szolgáltatás-frissítéseket a Windows PowerShell aktuális verzióját.</span><span class="sxs-lookup"><span data-stu-id="03366-145">Windows 10 users should install the latest feature updates to obtain the current version of Windows PowerShell.</span></span>

## <a name="enable-powershell-remoting"></a><span data-ttu-id="03366-146">PowerShell-távelérés engedélyezése</span><span class="sxs-lookup"><span data-stu-id="03366-146">Enable PowerShell Remoting</span></span>

<span data-ttu-id="03366-147">PowerShell-távelérést az alapokat amelyen JEA épül.</span><span class="sxs-lookup"><span data-stu-id="03366-147">PowerShell Remoting provides the foundation on which JEA is built.</span></span>
<span data-ttu-id="03366-148">Ezért elengedhetetlen, hogy engedélyezve van a PowerShell távelérése és [megfelelően védett](https://msdn.microsoft.com/powershell/scripting/setup/winrmsecurity) JEA használata előtt a rendszeren.</span><span class="sxs-lookup"><span data-stu-id="03366-148">It is therefore necessary to ensure PowerShell Remoting is enabled and [properly secured](https://msdn.microsoft.com/powershell/scripting/setup/winrmsecurity) on your system before you can use JEA.</span></span>

<span data-ttu-id="03366-149">A Windows Server 2012, 2012 R2 és 2016 alapértelmezés szerint engedélyezve van a PowerShell távvezérlését.</span><span class="sxs-lookup"><span data-stu-id="03366-149">PowerShell Remoting is enabled by default on Windows Server 2012, 2012 R2, and 2016.</span></span>
<span data-ttu-id="03366-150">PowerShell távoli eljáráshívás engedélyezéséhez futtassa a következő parancsot egy emelt szintű PowerShell-ablakban.</span><span class="sxs-lookup"><span data-stu-id="03366-150">You can enable PowerShell Remoting by running the following command in an elevated PowerShell window.</span></span>

```powershell
Enable-PSRemoting
```

## <a name="enable-powershell-module-and-script-block-logging-optional"></a><span data-ttu-id="03366-151">Engedélyezze a PowerShell-modul és a parancsfájl blokk naplózása (nem kötelező)</span><span class="sxs-lookup"><span data-stu-id="03366-151">Enable PowerShell module and script block logging (optional)</span></span>

<span data-ttu-id="03366-152">Az alábbi lépéseket az összes PowerShell műveleteket a rendszer a naplózás engedélyezése.</span><span class="sxs-lookup"><span data-stu-id="03366-152">The following steps enable logging for all PowerShell actions on your system.</span></span>
<span data-ttu-id="03366-153">PowerShell modul naplózás nincs szükség JEA, azonban erősen ajánlott bekapcsolni, annak érdekében, hogy a parancsok felhasználók futtatni egy központi helyen vannak bejelentkezve.</span><span class="sxs-lookup"><span data-stu-id="03366-153">PowerShell Module Logging is not required for JEA, however it is strongly recommended that you turn it on to ensure the commands users run are logged in a central location.</span></span>

<span data-ttu-id="03366-154">A PowerShell modul naplózási házirend csoportházirend használatával konfigurálható.</span><span class="sxs-lookup"><span data-stu-id="03366-154">You can configure the PowerShell Module Logging policy using Group Policy.</span></span>

1. <span data-ttu-id="03366-155">Nyissa meg a Helyicsoportházirend-szerkesztő munkaállomáson vagy csoportházirend-objektumra a Csoportházirend kezelése konzol egy Active Directory tartományvezérlőn</span><span class="sxs-lookup"><span data-stu-id="03366-155">Open the Local Group Policy Editor on a workstation or a Group Policy Object in the Group Policy Management Console on an Active Directory Domain Controller</span></span>
2. <span data-ttu-id="03366-156">Navigáljon a **számítógép konfigurációja\\felügyeleti sablonok\\Windows-összetevők\\Windows PowerShell**</span><span class="sxs-lookup"><span data-stu-id="03366-156">Navigate to **Computer Configuration\\Administrative Templates\\Windows Components\\Windows PowerShell**</span></span>
3. <span data-ttu-id="03366-157">Kattintson duplán a **kapcsolja be a modul naplózás**</span><span class="sxs-lookup"><span data-stu-id="03366-157">Double click on **Turn on Module Logging**</span></span>
4. <span data-ttu-id="03366-158">Kattintson a **engedélyezve**</span><span class="sxs-lookup"><span data-stu-id="03366-158">Click **Enabled**</span></span>
5. <span data-ttu-id="03366-159">A beállítások területen kattintson a **megjelenítése** modul neve mellett</span><span class="sxs-lookup"><span data-stu-id="03366-159">In the Options section, click on **Show** next to Module Names</span></span>
6. <span data-ttu-id="03366-160">Típusa "**\***" az előugró ablakban.</span><span class="sxs-lookup"><span data-stu-id="03366-160">Type "**\***" in the pop up window.</span></span> <span data-ttu-id="03366-161">Ez arra utasítja a PowerShell-parancsok naplózásra kerül minden modul.</span><span class="sxs-lookup"><span data-stu-id="03366-161">This instructs PowerShell to log commands from all modules.</span></span>
7. <span data-ttu-id="03366-162">Kattintson a **OK** házirend beállítása</span><span class="sxs-lookup"><span data-stu-id="03366-162">Click **OK** to set the policy</span></span>
8. <span data-ttu-id="03366-163">Kattintson duplán a **PowerShell parancsfájl-blokk naplózás bekapcsolása**</span><span class="sxs-lookup"><span data-stu-id="03366-163">Double click on **Turn on PowerShell Script Block Logging**</span></span>
9. <span data-ttu-id="03366-164">Kattintson a **engedélyezve**</span><span class="sxs-lookup"><span data-stu-id="03366-164">Click **Enabled**</span></span>
10. <span data-ttu-id="03366-165">Kattintson a **OK** házirend beállítása</span><span class="sxs-lookup"><span data-stu-id="03366-165">Click **OK** to set the policy</span></span>
11. <span data-ttu-id="03366-166">(A tartományhoz csatlakoztatott számítógépeken csak) Futtatás **gpupdate** vagy várja meg, a frissített házirendet, és alkalmazza a beállításokat a csoportházirend</span><span class="sxs-lookup"><span data-stu-id="03366-166">(On domain-joined machines only) Run **gpupdate** or wait for Group Policy to process the updated policy and apply the settings</span></span>

<span data-ttu-id="03366-167">Rendszerszintű PowerShell írjanak elő csoportházirenden keresztül is engedélyezheti.</span><span class="sxs-lookup"><span data-stu-id="03366-167">You can also enable system-wide PowerShell transcription through Group Policy.</span></span>

## <a name="next-steps"></a><span data-ttu-id="03366-168">További lépések</span><span class="sxs-lookup"><span data-stu-id="03366-168">Next steps</span></span>

- [<span data-ttu-id="03366-169">Egy szerepkör funkció fájl létrehozása</span><span class="sxs-lookup"><span data-stu-id="03366-169">Create a role capability file</span></span>](role-capabilities.md)
- [<span data-ttu-id="03366-170">Egy munkamenet-konfigurációs fájl létrehozása</span><span class="sxs-lookup"><span data-stu-id="03366-170">Create a session configuration file</span></span>](session-configurations.md)

## <a name="see-also"></a><span data-ttu-id="03366-171">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="03366-171">See also</span></span>

- [<span data-ttu-id="03366-172">PowerShell távvezérlése és a Rendszerfelügyeleti webszolgáltatások biztonsággal kapcsolatos további információk</span><span class="sxs-lookup"><span data-stu-id="03366-172">Additional information about PowerShell Remoting and WinRM security</span></span>](https://msdn.microsoft.com/powershell/scripting/setup/winrmsecurity)
- [<span data-ttu-id="03366-173">*PowerShell ♥ a kék Team* a biztonsági által írt blogbejegyzés</span><span class="sxs-lookup"><span data-stu-id="03366-173">*PowerShell ♥ the Blue Team* blog post on security</span></span>](https://blogs.msdn.microsoft.com/powershell/2015/06/09/powershell-the-blue-team/)

