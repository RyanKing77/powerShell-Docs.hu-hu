---
ms.date: 07/10/2019
keywords: jea, PowerShell, biztonság
title: A JEA előfeltételei
ms.openlocfilehash: 8fca5c068412e86acfdb8bed400699f721b76191
ms.sourcegitcommit: e894ed833cef57967cdaf002f8c883f66864e836
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/25/2019
ms.locfileid: "70017936"
---
# <a name="prerequisites"></a><span data-ttu-id="a6d23-103">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="a6d23-103">Prerequisites</span></span>

<span data-ttu-id="a6d23-104">Elég adminisztráció a PowerShell 5,0-es és újabb verziója.</span><span class="sxs-lookup"><span data-stu-id="a6d23-104">Just Enough Administration is a feature included in PowerShell 5.0 and higher.</span></span> <span data-ttu-id="a6d23-105">Ez a cikk azokat az előfeltételeket ismerteti, amelyeknek teljesülniük kell a JEA használatának megkezdéséhez.</span><span class="sxs-lookup"><span data-stu-id="a6d23-105">This article describes the prerequisites that must be satisfied to start using JEA.</span></span>


## <a name="check-which-version-of-powershell-is-installed"></a><span data-ttu-id="a6d23-106">A PowerShell telepített verziójának megkeresése</span><span class="sxs-lookup"><span data-stu-id="a6d23-106">Check which version of PowerShell is installed</span></span>

<span data-ttu-id="a6d23-107">Ha szeretné megnézni, hogy a PowerShell melyik verziója van telepítve a rendszeren `$PSVersionTable` , akkor a változót egy Windows PowerShell-parancssorban jelenítheti meg.</span><span class="sxs-lookup"><span data-stu-id="a6d23-107">To check which version of PowerShell is installed on your system, check the `$PSVersionTable` variable in a Windows PowerShell prompt.</span></span>

```powershell
$PSVersionTable.PSVersion
```

```Output
Major  Minor  Build  Revision
-----  -----  -----  --------
5      1      14393  1000
```

<span data-ttu-id="a6d23-108">A JEA a PowerShell 5,0-es vagy újabb verziójával érhető el.</span><span class="sxs-lookup"><span data-stu-id="a6d23-108">JEA is available with PowerShell 5.0 and higher.</span></span> <span data-ttu-id="a6d23-109">A teljes funkcionalitás érdekében javasoljuk, hogy telepítse a PowerShell legújabb verzióját a rendszer számára.</span><span class="sxs-lookup"><span data-stu-id="a6d23-109">For full functionality, it's recommended that you install the latest version of PowerShell available for your system.</span></span> <span data-ttu-id="a6d23-110">A következő táblázat ismerteti a JEA rendelkezésre állását a Windows Serveren:</span><span class="sxs-lookup"><span data-stu-id="a6d23-110">The following table describes JEA's availability on Windows Server:</span></span>

| <span data-ttu-id="a6d23-111">Kiszolgálói operációs rendszer</span><span class="sxs-lookup"><span data-stu-id="a6d23-111">Server Operating System</span></span> |                <span data-ttu-id="a6d23-112">JEA rendelkezésre állása</span><span class="sxs-lookup"><span data-stu-id="a6d23-112">JEA Availability</span></span>                |
| ----------------------- | ---------------------------------------------- |
| <span data-ttu-id="a6d23-113">Windows Server 2016 +</span><span class="sxs-lookup"><span data-stu-id="a6d23-113">Windows Server 2016+</span></span>    | <span data-ttu-id="a6d23-114">Előtelepített</span><span class="sxs-lookup"><span data-stu-id="a6d23-114">Preinstalled</span></span>                                   |
| <span data-ttu-id="a6d23-115">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="a6d23-115">Windows Server 2012 R2</span></span>  | <span data-ttu-id="a6d23-116">Teljes funkcionalitás a WMF 5,1-vel</span><span class="sxs-lookup"><span data-stu-id="a6d23-116">Full functionality with WMF 5.1</span></span>                |
| <span data-ttu-id="a6d23-117">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="a6d23-117">Windows Server 2012</span></span>     | <span data-ttu-id="a6d23-118">Teljes funkcionalitás a WMF 5,1-vel</span><span class="sxs-lookup"><span data-stu-id="a6d23-118">Full functionality with WMF 5.1</span></span>                |
| <span data-ttu-id="a6d23-119">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="a6d23-119">Windows Server 2008 R2</span></span>  | <span data-ttu-id="a6d23-120">Kevesebb funkció<sup>1</sup> a WMF 5,1-vel</span><span class="sxs-lookup"><span data-stu-id="a6d23-120">Reduced functionality<sup>1</sup> with WMF 5.1</span></span> |

<span data-ttu-id="a6d23-121">Használhatja a JEA a saját otthoni vagy munkahelyi számítógépén is:</span><span class="sxs-lookup"><span data-stu-id="a6d23-121">You can also use JEA on your home or work computer:</span></span>

| <span data-ttu-id="a6d23-122">Ügyféloldali operációs rendszer</span><span class="sxs-lookup"><span data-stu-id="a6d23-122">Client Operating System</span></span> |                   <span data-ttu-id="a6d23-123">JEA rendelkezésre állása</span><span class="sxs-lookup"><span data-stu-id="a6d23-123">JEA Availability</span></span>                   |
| ----------------------- | ---------------------------------------------------- |
| <span data-ttu-id="a6d23-124">Windows 10 1607+</span><span class="sxs-lookup"><span data-stu-id="a6d23-124">Windows 10 1607+</span></span>        | <span data-ttu-id="a6d23-125">Előtelepített</span><span class="sxs-lookup"><span data-stu-id="a6d23-125">Preinstalled</span></span>                                         |
| <span data-ttu-id="a6d23-126">Windows 10 1603, 1511</span><span class="sxs-lookup"><span data-stu-id="a6d23-126">Windows 10 1603, 1511</span></span>   | <span data-ttu-id="a6d23-127">Előre telepítve, a csökkentett funkciókkal<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="a6d23-127">Preinstalled, with reduced functionality<sup>2</sup></span></span> |
| <span data-ttu-id="a6d23-128">Windows 10 1507</span><span class="sxs-lookup"><span data-stu-id="a6d23-128">Windows 10 1507</span></span>         | <span data-ttu-id="a6d23-129">Nem elérhető el</span><span class="sxs-lookup"><span data-stu-id="a6d23-129">Not available</span></span>                                        |
| <span data-ttu-id="a6d23-130">Windows 8, 8,1</span><span class="sxs-lookup"><span data-stu-id="a6d23-130">Windows 8, 8.1</span></span>          | <span data-ttu-id="a6d23-131">Teljes funkcionalitás a WMF 5,1-vel</span><span class="sxs-lookup"><span data-stu-id="a6d23-131">Full functionality with WMF 5.1</span></span>                      |
| <span data-ttu-id="a6d23-132">Windows 7</span><span class="sxs-lookup"><span data-stu-id="a6d23-132">Windows 7</span></span>               | <span data-ttu-id="a6d23-133">Kevesebb funkció<sup>1</sup> a WMF 5,1-vel</span><span class="sxs-lookup"><span data-stu-id="a6d23-133">Reduced functionality<sup>1</sup> with WMF 5.1</span></span>       |

- <span data-ttu-id="a6d23-134"><sup>1</sup> a JEA nem konfigurálhatók csoportosan felügyelt szolgáltatásfiókok használatára windows Server 2008 R2 vagy Windows 7 rendszeren.</span><span class="sxs-lookup"><span data-stu-id="a6d23-134"><sup>1</sup> JEA can't be configured to use group-managed service accounts on Windows Server 2008 R2 or Windows 7.</span></span> <span data-ttu-id="a6d23-135">*A* virtuális fiókok és egyéb JEA-funkciók támogatottak.</span><span class="sxs-lookup"><span data-stu-id="a6d23-135">Virtual accounts and other JEA features *are* supported.</span></span>

- <span data-ttu-id="a6d23-136"><sup>2</sup> a következő JEA funkciók nem támogatottak a Windows 10 1511-es és 1603-es verziójában:</span><span class="sxs-lookup"><span data-stu-id="a6d23-136"><sup>2</sup> The following JEA features aren't supported on Windows 10 versions 1511 and 1603:</span></span>

  - <span data-ttu-id="a6d23-137">Futtatás csoportosan felügyelt szolgáltatásfiókként</span><span class="sxs-lookup"><span data-stu-id="a6d23-137">Running as a group-managed service account</span></span>
  - <span data-ttu-id="a6d23-138">Feltételes hozzáférési szabályok a munkamenet-konfigurációkban</span><span class="sxs-lookup"><span data-stu-id="a6d23-138">Conditional access rules in session configurations</span></span>
  - <span data-ttu-id="a6d23-139">A felhasználói meghajtó</span><span class="sxs-lookup"><span data-stu-id="a6d23-139">The user drive</span></span>
  - <span data-ttu-id="a6d23-140">Hozzáférés biztosítása a helyi felhasználói fiókokhoz</span><span class="sxs-lookup"><span data-stu-id="a6d23-140">Granting access to local user accounts</span></span>

  <span data-ttu-id="a6d23-141">Ezeknek a funkcióknak a támogatásához frissítse a Windowst az 1607-es (évfordulós frissítés) vagy újabb verzióra.</span><span class="sxs-lookup"><span data-stu-id="a6d23-141">To get support for these features, update Windows to version 1607 (Anniversary Update) or higher.</span></span>

### <a name="install-windows-management-framework"></a><span data-ttu-id="a6d23-142">A Windows Management Framework telepítése</span><span class="sxs-lookup"><span data-stu-id="a6d23-142">Install Windows Management Framework</span></span>

<span data-ttu-id="a6d23-143">Ha a PowerShell egy régebbi verzióját futtatja, előfordulhat, hogy frissítenie kell a rendszert a legújabb Windows Management Framework (WMF) frissítéssel.</span><span class="sxs-lookup"><span data-stu-id="a6d23-143">If you're running an older version of PowerShell, you may need to update your system with the latest Windows Management Framework (WMF) update.</span></span> <span data-ttu-id="a6d23-144">További információt a [WMF dokumentációjában](/powershell/wmf/overview)talál.</span><span class="sxs-lookup"><span data-stu-id="a6d23-144">For more information, see the [WMF documentation](/powershell/wmf/overview).</span></span>

<span data-ttu-id="a6d23-145">Javasoljuk, hogy az összes kiszolgáló frissítése előtt tesztelje a munkaterhelést a WMF-kompatibilitással.</span><span class="sxs-lookup"><span data-stu-id="a6d23-145">It's recommended that you test your workload's compatibility with WMF before upgrading all of your servers.</span></span>

<span data-ttu-id="a6d23-146">A Windows 10 rendszerű felhasználóknak telepíteniük kell a legújabb szolgáltatás-frissítéseket a Windows PowerShell aktuális verziójának beszerzéséhez.</span><span class="sxs-lookup"><span data-stu-id="a6d23-146">Windows 10 users should install the latest feature updates to obtain the current version of Windows PowerShell.</span></span>

## <a name="enable-powershell-remoting"></a><span data-ttu-id="a6d23-147">A PowerShell távelérésének engedélyezése</span><span class="sxs-lookup"><span data-stu-id="a6d23-147">Enable PowerShell Remoting</span></span>

<span data-ttu-id="a6d23-148">A PowerShell-távelérés biztosítja azt az alapot, amely a JEA épül.</span><span class="sxs-lookup"><span data-stu-id="a6d23-148">PowerShell Remoting provides the foundation on which JEA is built.</span></span> <span data-ttu-id="a6d23-149">A JEA használata előtt meg kell győződnie arról, hogy a PowerShell távelérése engedélyezve van és megfelelően védett.</span><span class="sxs-lookup"><span data-stu-id="a6d23-149">It's necessary to ensure PowerShell Remoting is enabled and properly secured before you can use JEA.</span></span> <span data-ttu-id="a6d23-150">További információ: [WinRM Security](/powershell/scripting/learn/remoting/winrmsecurity).</span><span class="sxs-lookup"><span data-stu-id="a6d23-150">For more information, see [WinRM Security](/powershell/scripting/learn/remoting/winrmsecurity).</span></span>

<span data-ttu-id="a6d23-151">A PowerShell-távelérés alapértelmezés szerint engedélyezve van a Windows Server 2012, 2012 R2 és 2016 rendszeren.</span><span class="sxs-lookup"><span data-stu-id="a6d23-151">PowerShell Remoting is enabled by default on Windows Server 2012, 2012 R2, and 2016.</span></span> <span data-ttu-id="a6d23-152">A PowerShell távelérési szolgáltatásának engedélyezéséhez futtassa a következő parancsot egy emelt szintű PowerShell-ablakban.</span><span class="sxs-lookup"><span data-stu-id="a6d23-152">You can enable PowerShell Remoting by running the following command in an elevated PowerShell window.</span></span>

```powershell
Enable-PSRemoting
```

## <a name="enable-powershell-module-and-script-block-logging-optional"></a><span data-ttu-id="a6d23-153">PowerShell-modul és parancsfájl-blokkoló naplózásának engedélyezése (nem kötelező)</span><span class="sxs-lookup"><span data-stu-id="a6d23-153">Enable PowerShell module and script block logging (optional)</span></span>

<span data-ttu-id="a6d23-154">A következő lépésekkel engedélyezheti a naplózást a rendszeren lévő összes PowerShell-művelethez.</span><span class="sxs-lookup"><span data-stu-id="a6d23-154">The following steps enable logging for all PowerShell actions on your system.</span></span> <span data-ttu-id="a6d23-155">A PowerShell-modul naplózása nem szükséges a JEA, azonban javasoljuk, hogy kapcsolja be a naplózást, hogy a felhasználók által futtatott parancsok központi helyen legyenek naplózva.</span><span class="sxs-lookup"><span data-stu-id="a6d23-155">PowerShell Module Logging isn't required for JEA, however it's recommended you turn on logging to ensure the commands users run are logged in a central location.</span></span>

<span data-ttu-id="a6d23-156">A PowerShell-modul naplózási házirendjét Csoportházirend használatával konfigurálhatja.</span><span class="sxs-lookup"><span data-stu-id="a6d23-156">You can configure the PowerShell Module Logging policy using Group Policy.</span></span>

1. <span data-ttu-id="a6d23-157">A Helyicsoportházirend-szerkesztő megnyitása egy munkaállomáson vagy egy Csoportházirend objektumon a Csoportházirend-kezelő konzol egy Active Directory-tartomány vezérlőn</span><span class="sxs-lookup"><span data-stu-id="a6d23-157">Open the Local Group Policy Editor on a workstation or a Group Policy Object in the Group Policy Management Console on an Active Directory Domain Controller</span></span>
2. <span data-ttu-id="a6d23-158">Navigáljon a **számítógép\\konfigurációja\\felügyeleti sablonok Windows\\-összetevők Windows PowerShell**</span><span class="sxs-lookup"><span data-stu-id="a6d23-158">Navigate to **Computer Configuration\\Administrative Templates\\Windows Components\\Windows PowerShell**</span></span>
3. <span data-ttu-id="a6d23-159">Kattintson duplán a **modul naplózásának** bekapcsolása elemre.</span><span class="sxs-lookup"><span data-stu-id="a6d23-159">Double-click on **Turn on Module Logging**</span></span>
4. <span data-ttu-id="a6d23-160">Kattintson az **engedélyezve** lehetőségre</span><span class="sxs-lookup"><span data-stu-id="a6d23-160">Click **Enabled**</span></span>
5. <span data-ttu-id="a6d23-161">A beállítások szakaszban kattintson a **Megjelenítés** elemre a modulok neve mellett.</span><span class="sxs-lookup"><span data-stu-id="a6d23-161">In the Options section, click on **Show** next to Module Names</span></span>
6. <span data-ttu-id="a6d23-162">Írja `*` be az előugró ablakot a parancsok minden modulból való naplózásához.</span><span class="sxs-lookup"><span data-stu-id="a6d23-162">Type `*` in the pop-up window to log commands from all modules.</span></span>
7. <span data-ttu-id="a6d23-163">A házirend beállításához kattintson **az OK** gombra.</span><span class="sxs-lookup"><span data-stu-id="a6d23-163">Click **OK** to set the policy</span></span>
8. <span data-ttu-id="a6d23-164">Kattintson duplán a **PowerShell parancsfájl** -blokkoló naplózásának bekapcsolása elemre.</span><span class="sxs-lookup"><span data-stu-id="a6d23-164">Double-click on **Turn on PowerShell Script Block Logging**</span></span>
9. <span data-ttu-id="a6d23-165">Kattintson az **engedélyezve** lehetőségre</span><span class="sxs-lookup"><span data-stu-id="a6d23-165">Click **Enabled**</span></span>
10. <span data-ttu-id="a6d23-166">A házirend beállításához kattintson **az OK** gombra.</span><span class="sxs-lookup"><span data-stu-id="a6d23-166">Click **OK** to set the policy</span></span>
11. <span data-ttu-id="a6d23-167">(Csak tartományhoz csatlakoztatott gépeken) Futtassa `gpupdate` vagy várjon csoportházirend a frissített szabályzat feldolgozásához és a beállítások alkalmazásához</span><span class="sxs-lookup"><span data-stu-id="a6d23-167">(On domain-joined machines only) Run `gpupdate` or wait for Group Policy to process the updated policy and apply the settings</span></span>

<span data-ttu-id="a6d23-168">A Csoportházirend használatával is engedélyezheti a rendszerszintű PowerShell-átírást.</span><span class="sxs-lookup"><span data-stu-id="a6d23-168">You can also enable system-wide PowerShell transcription through Group Policy.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a6d23-169">További lépések</span><span class="sxs-lookup"><span data-stu-id="a6d23-169">Next steps</span></span>

[<span data-ttu-id="a6d23-170">Szerepkör-képesség fájl létrehozása</span><span class="sxs-lookup"><span data-stu-id="a6d23-170">Create a role capability file</span></span>](role-capabilities.md)

[<span data-ttu-id="a6d23-171">Munkamenet-konfigurációs fájl létrehozása</span><span class="sxs-lookup"><span data-stu-id="a6d23-171">Create a session configuration file</span></span>](session-configurations.md)

## <a name="see-also"></a><span data-ttu-id="a6d23-172">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="a6d23-172">See also</span></span>

[<span data-ttu-id="a6d23-173">WinRM-biztonság</span><span class="sxs-lookup"><span data-stu-id="a6d23-173">WinRM Security</span></span>](/powershell/scripting/learn/remoting/winrmsecurity)

[<span data-ttu-id="a6d23-174">A PowerShell ♥ a kék csapatot</span><span class="sxs-lookup"><span data-stu-id="a6d23-174">PowerShell ♥ the Blue Team</span></span>](https://devblogs.microsoft.com/powershell/powershell-the-blue-team/)
