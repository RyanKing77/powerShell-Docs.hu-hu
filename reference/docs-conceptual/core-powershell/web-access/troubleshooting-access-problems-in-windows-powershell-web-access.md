---
ms.date: 08/23/2017
keywords: PowerShell parancsmag
title: a windows powershell web access hozzáférési problémák elhárítása
ms.openlocfilehash: ef476d8e386e5380cb2c9dda69180dfce8748bf4
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="troubleshooting-access-problems-in-windows-powershell-web-access"></a><span data-ttu-id="11a2c-103">Hozzáférési problémák hibaelhárítása a Webes Windows PowerShell-elérésben</span><span class="sxs-lookup"><span data-stu-id="11a2c-103">Troubleshooting Access Problems in Windows PowerShell Web Access</span></span>

<span data-ttu-id="11a2c-104">Frissítés: Június 24, 2013 (módosított 2017. augusztus 23.)</span><span class="sxs-lookup"><span data-stu-id="11a2c-104">Updated: June 24, 2013 (revised August 23, 2017)</span></span>

<span data-ttu-id="11a2c-105">Vonatkozik: Windows Server 2012 R2, Windows Server 2012-ben</span><span class="sxs-lookup"><span data-stu-id="11a2c-105">Applies To: Windows Server 2012 R2, Windows Server 2012</span></span>

<span data-ttu-id="11a2c-106">A következő szakaszok olyan gyakori problémákat azonosítása, a Windows PowerShell Web Access használatával kapcsolódik egy távoli számítógépen, és javaslatokat is kínál a problémák.</span><span class="sxs-lookup"><span data-stu-id="11a2c-106">The following sections identify some common problems when attempting to connect to a remote computer by using Windows PowerShell Web Access, and includes suggestions for resolving the problems.</span></span>

## <a name="sign-in-failure"></a><span data-ttu-id="11a2c-107">Bejelentkezési hiba</span><span class="sxs-lookup"><span data-stu-id="11a2c-107">Sign-in failure</span></span>

<span data-ttu-id="11a2c-108">A hiba oka a következők bármelyike lehet.</span><span class="sxs-lookup"><span data-stu-id="11a2c-108">Failure could occur because of any of the following.</span></span>

- <span data-ttu-id="11a2c-109">Hiányzik egy olyan engedélyezési szabály, amely lehetővé tenné a felhasználónak a számítógép hozzáférését vagy hiányzik egy adott munkamenet-konfiguráció a távoli számítógépen.</span><span class="sxs-lookup"><span data-stu-id="11a2c-109">An authorization rule that allows the user access to the computer, or a specific session configuration on the remote computer, does not exist.</span></span>

  <span data-ttu-id="11a2c-110">A Windows PowerShell Web Access biztonsági érték korlátozó; felhasználókhoz kifejezett hozzáférést távoli számítógépekhez engedélyezési szabályok segítségével kell kell rendelni.</span><span class="sxs-lookup"><span data-stu-id="11a2c-110">Windows PowerShell Web Access security is restrictive; users must be granted explicit access to remote computers by using authorization rules.</span></span>

  <span data-ttu-id="11a2c-111">Az engedélyezési szabályok létrehozásával kapcsolatos további információkért lásd: [engedélyezési szabályai és biztonsági szolgáltatások a Windows PowerShell Web Access](authorization-rules-and-security-features-of-windows-powershell-web-access.md).</span><span class="sxs-lookup"><span data-stu-id="11a2c-111">For more information about creating authorization rules, see [Authorization Rules and Security Features of Windows PowerShell Web Access](authorization-rules-and-security-features-of-windows-powershell-web-access.md).</span></span>

- <span data-ttu-id="11a2c-112">A felhasználó rendelkezik engedélyezett hozzáféréssel a célszámítógéphez.</span><span class="sxs-lookup"><span data-stu-id="11a2c-112">The user does not have authorized access to the destination computer.</span></span> <span data-ttu-id="11a2c-113">A hozzáférést a hozzáférés-vezérlési listák (access control list, ACL) határozzák meg.</span><span class="sxs-lookup"><span data-stu-id="11a2c-113">This is determined by access control lists (ACLs).</span></span>

  <span data-ttu-id="11a2c-114">További információkért lásd: [bejelentkezés a Windows PowerShell Web Access](use-the-web-based-windows-powershell-console.md#signing-in-to-windows-powershell-web-access), vagy a Windows PowerShell csapatának blogját.</span><span class="sxs-lookup"><span data-stu-id="11a2c-114">For more information, see [Signing in to Windows PowerShell Web Access](use-the-web-based-windows-powershell-console.md#signing-in-to-windows-powershell-web-access), or the Windows PowerShell Team Blog.</span></span>

- <span data-ttu-id="11a2c-115">Előfordulhat, hogy a célszámítógépen nincs engedélyezve távoli felügyelet a Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="11a2c-115">Windows PowerShell remote management might not be enabled on the destination computer.</span></span>

  <span data-ttu-id="11a2c-116">Ellenőrizze a távoli felügyelet engedélyezve van a számítógépen, amelyre a felhasználó csatlakozni próbál.</span><span class="sxs-lookup"><span data-stu-id="11a2c-116">Verify remote management is enabled on the computer to which the user is trying to connect.</span></span>

  <span data-ttu-id="11a2c-117">További információkért lásd: [hogyan konfigurálhatja a számítógép a távoli eljáráshívás](https://docs.microsoft.com/powershell/module/microsoft.powershell.core/about/about_remote_requirements#how-to-configure-your-computer-for-remoting).</span><span class="sxs-lookup"><span data-stu-id="11a2c-117">For more information, see [How to Configure Your Computer for Remoting](https://docs.microsoft.com/powershell/module/microsoft.powershell.core/about/about_remote_requirements#how-to-configure-your-computer-for-remoting).</span></span>

## <a name="internal-server-error"></a><span data-ttu-id="11a2c-118">Belső kiszolgálóhiba.</span><span class="sxs-lookup"><span data-stu-id="11a2c-118">Internal Server Error</span></span>

<span data-ttu-id="11a2c-119">Amikor a felhasználó próbál bejelentkezni a Windows PowerShell Web Access egy Internet Explorer-ablakban, megtekinthető egy **belső kiszolgálóhiba** lapon vagy *Internet Explorer* nem válaszol.</span><span class="sxs-lookup"><span data-stu-id="11a2c-119">When users try to sign in to Windows PowerShell Web Access in an Internet Explorer window, they are shown an **Internal Server Error** page, or *Internet Explorer* stops responding.</span></span>

<span data-ttu-id="11a2c-120">Ez a hiba csak az Internet Explorerben fordul elő.</span><span class="sxs-lookup"><span data-stu-id="11a2c-120">This issue is specific to Internet Explorer.</span></span>

### <a name="possible-cause"></a><span data-ttu-id="11a2c-121">Lehetséges ok</span><span class="sxs-lookup"><span data-stu-id="11a2c-121">Possible cause</span></span>

<span data-ttu-id="11a2c-122">Olyan felhasználóknál jelentkezhet, akik kínai karaktereket használó tartománynévvel jelentkeztek be, vagy akiknél az átjárókiszolgáló neve kínai karaktereket tartalmaz.</span><span class="sxs-lookup"><span data-stu-id="11a2c-122">This can occur for users who have signed in with a domain name that contains Chinese characters, or if one or more Chinese characters are part of the gateway server name.</span></span>

#### <a name="workaround"></a><span data-ttu-id="11a2c-123">Megkerülő megoldás</span><span class="sxs-lookup"><span data-stu-id="11a2c-123">Workaround</span></span>

1. [<span data-ttu-id="11a2c-124">Telepítheti és futtathatja az Internet Explorer 10</span><span class="sxs-lookup"><span data-stu-id="11a2c-124">Install and run Internet Explorer 10</span></span>](http://ie.microsoft.com/testdrive/info/downloads/Default.html)
1. <span data-ttu-id="11a2c-125">Módosítsa az Internet Explorer **dokumentum-üzemmód** beállítást *IE10* szabványoknak.</span><span class="sxs-lookup"><span data-stu-id="11a2c-125">Change Internet Explorer **Document Mode** setting to *IE10* standards.</span></span>
   1. <span data-ttu-id="11a2c-126">Nyomja le az **F12** a fejlesztői eszközök konzol megnyitása</span><span class="sxs-lookup"><span data-stu-id="11a2c-126">Press **F12** to open the Developer Tools console</span></span>
   1. <span data-ttu-id="11a2c-127">Kattintson az Internet Explorer 10 **böngésző üzemmódja**, majd válassza ki *Internet Explorer 10*.</span><span class="sxs-lookup"><span data-stu-id="11a2c-127">In Internet Explorer 10, click **Browser Mode**, and then select *Internet Explorer 10*.</span></span>
   1. <span data-ttu-id="11a2c-128">Kattintson a **dokumentum-üzemmód**, és kattintson a *IE10* szabványoknak.</span><span class="sxs-lookup"><span data-stu-id="11a2c-128">Click **Document Mode**, and then click *IE10* standards.</span></span>
   1. <span data-ttu-id="11a2c-129">Nyomja le az **F12** a fejlesztői eszközök konzol bezárásához.</span><span class="sxs-lookup"><span data-stu-id="11a2c-129">Press **F12** again to close the Developer Tools console.</span></span>
1. <span data-ttu-id="11a2c-130">Tiltsa le az Internet Explorer 10 automatikus proxybeállítást.</span><span class="sxs-lookup"><span data-stu-id="11a2c-130">Disable automatic proxy configuration in Internet Explorer 10.</span></span>
   1. <span data-ttu-id="11a2c-131">Kattintson a **eszközök**, és kattintson a **Internetbeállítások**.</span><span class="sxs-lookup"><span data-stu-id="11a2c-131">Click **Tools**, and then click **Internet Options**.</span></span>
   1. <span data-ttu-id="11a2c-132">Az a **Internetbeállítások** párbeszédpanel a **kapcsolatok** lapra, majd **LAN-beállítások**.</span><span class="sxs-lookup"><span data-stu-id="11a2c-132">In the **Internet Options** dialog box, on the **Connections** tab, click **LAN settings**.</span></span>
   1. <span data-ttu-id="11a2c-133">Törölje a jelet a **beállítások automatikus észlelése** jelölőnégyzetet.</span><span class="sxs-lookup"><span data-stu-id="11a2c-133">Clear the **Automatically detect settings** check box.</span></span> <span data-ttu-id="11a2c-134">Kattintson a **OK**, és kattintson a **OK** bezárásához a *Internetbeállítások* párbeszédpanel megnyitásához.</span><span class="sxs-lookup"><span data-stu-id="11a2c-134">Click **OK**, and then click **OK** again to close the *Internet Options* dialog box.</span></span>

## <a name="cannot-connect-to-a-remote-workgroup-computer"></a><span data-ttu-id="11a2c-135">Nem lehet csatlakozni egy távoli munkacsoport-számítógéphez</span><span class="sxs-lookup"><span data-stu-id="11a2c-135">Cannot connect to a remote workgroup computer</span></span>

<span data-ttu-id="11a2c-136">Ha a célszámítógép egy munkacsoport tagja, használja a következő szintaxist a felhasználónév megadásához és a számítógépre történő bejelentkezéshez: `<workgroup_name>\<user_name>`</span><span class="sxs-lookup"><span data-stu-id="11a2c-136">If the destination computer is a member of a workgroup, use the following syntax to provide your user name and sign in to the computer: `<workgroup_name>\<user_name>`</span></span>

## <a name="cannot-find-web-server-iis-management-tools-even-though-the-role-was-installed"></a><span data-ttu-id="11a2c-137">A rendszer nem találja a webkiszolgáló (IIS) felügyeleti eszközöket, pedig a szerepkör telepítve van</span><span class="sxs-lookup"><span data-stu-id="11a2c-137">Cannot find Web Server (IIS) management tools, even though the role was installed</span></span>

<span data-ttu-id="11a2c-138">Ha a Windows PowerShell Web Access segítségével telepítette a `Install-WindowsFeature` parancsmag, felügyeleti eszközei nincsenek telepítve, kivéve, ha a `-IncludeManagementTools` paraméter hozzáadódik a parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="11a2c-138">If you installed Windows PowerShell Web Access by using the `Install-WindowsFeature` cmdlet, management tools are not installed unless the `-IncludeManagementTools` parameter is added to the cmdlet.</span></span>

<span data-ttu-id="11a2c-139">Egy vonatkozó példáért lásd: [Windows PowerShell Web Access telepítése a Windows PowerShell-parancsmagok használatával](install-and-use-windows-powershell-web-access.md#to-install-windows-powershell-web-access-by-using-windows-powershell-cmdlets).</span><span class="sxs-lookup"><span data-stu-id="11a2c-139">For an example, see [To install Windows PowerShell Web Access by using Windows PowerShell cmdlets](install-and-use-windows-powershell-web-access.md#to-install-windows-powershell-web-access-by-using-windows-powershell-cmdlets).</span></span>

<span data-ttu-id="11a2c-140">Az IIS-kezelő konzolon is hozzáadhat, és egyéb IIS felügyeleti eszközöket, hogy van szüksége, ha kiválasztja a egy **hozzáadása szerepkörök és szolgáltatások varázsló** az átjárókiszolgálót célzó munkamenet.</span><span class="sxs-lookup"><span data-stu-id="11a2c-140">You can add the IIS Manager console, and other IIS management tools that you need, by selecting the tools in an **Add Roles and Features Wizard** session that is targeted at the gateway server.</span></span>
<span data-ttu-id="11a2c-141">A szerepkörök hozzáadása és szolgáltatások varázsló megnyitása a Kiszolgálókezelőben</span><span class="sxs-lookup"><span data-stu-id="11a2c-141">The Add Roles and Features Wizard is opened from within Server Manager.</span></span>

## <a name="windows-powershell-web-access-website-is-not-accessible"></a><span data-ttu-id="11a2c-142">A Windows PowerShell Web Access webhely nem érhető el.</span><span class="sxs-lookup"><span data-stu-id="11a2c-142">Windows PowerShell Web Access website is not accessible</span></span>

<span data-ttu-id="11a2c-143">Ha fokozott biztonsági beállítások engedélyezve van az Internet Explorerben (IE ESC), a Windows PowerShell Web Access webhely is hozzáadhat a megbízható helyek listájához.</span><span class="sxs-lookup"><span data-stu-id="11a2c-143">If Enhanced Security Configuration is enabled in Internet Explorer (IE ESC), you can add the Windows PowerShell Web Access website to the list of trusted sites.</span></span>

<span data-ttu-id="11a2c-144">A kisebb ajánlott megközelítést, biztonsági kockázatok miatt is letilthatja az IE ESC-t.</span><span class="sxs-lookup"><span data-stu-id="11a2c-144">A less recommended approach, due to security risks, is to disable IE ESC.</span></span>
<span data-ttu-id="11a2c-145">Letilthatja az IE ESC-t a helyi kiszolgáló oldalán a Kiszolgálókezelőben a Tulajdonságok csempén.</span><span class="sxs-lookup"><span data-stu-id="11a2c-145">You can disable IE ESC in the Properties tile on the Local Server page in Server Manager.</span></span>

## <a name="an-authorization-failure-occurred-verify-that-you-are-authorized-to-connect-to-the-destination-computer"></a><span data-ttu-id="11a2c-146">Engedélyezési hiba történt.</span><span class="sxs-lookup"><span data-stu-id="11a2c-146">An authorization failure occurred.</span></span> <span data-ttu-id="11a2c-147">Győződjön meg arról, hogy jogosult a célszámítógéphez kapcsolódni.</span><span class="sxs-lookup"><span data-stu-id="11a2c-147">Verify that you are authorized to connect to the destination computer.</span></span>

<span data-ttu-id="11a2c-148">A fenti hibaüzenet jelenik meg, amikor az átjárókiszolgáló a célszámítógép, és egyben egy munkacsoporthoz csatlakozás közben.</span><span class="sxs-lookup"><span data-stu-id="11a2c-148">The above error message is displayed while trying to connect when the gateway server is the destination computer, and is also in a workgroup.</span></span>

<span data-ttu-id="11a2c-149">Amikor az átjárókiszolgáló is a célkiszolgálón, és egy munkacsoporthoz, adja meg a felhasználónevet, a számítógépnév és a felhasználó csoportnevét.</span><span class="sxs-lookup"><span data-stu-id="11a2c-149">When the gateway server is also the destination server, and it is in a workgroup, specify the user name, computer name, and user group name.</span></span>
<span data-ttu-id="11a2c-150">A számítógép nevét képviselő ne használjon önmagában egy pontot (.) önmagában.</span><span class="sxs-lookup"><span data-stu-id="11a2c-150">Do not use a dot (.) by itself to represent the computer name.</span></span>

### <a name="scenarios-and-proper-values"></a><span data-ttu-id="11a2c-151">Forgatókönyvek és a megfelelő értékek</span><span class="sxs-lookup"><span data-stu-id="11a2c-151">Scenarios and proper values</span></span>

#### <a name="all-cases"></a><span data-ttu-id="11a2c-152">Minden esetben</span><span class="sxs-lookup"><span data-stu-id="11a2c-152">All cases</span></span>

<span data-ttu-id="11a2c-153">Paraméter</span><span class="sxs-lookup"><span data-stu-id="11a2c-153">Parameter</span></span> | <span data-ttu-id="11a2c-154">Érték</span><span class="sxs-lookup"><span data-stu-id="11a2c-154">Value</span></span>
-- | --
<span data-ttu-id="11a2c-155">UserName</span><span class="sxs-lookup"><span data-stu-id="11a2c-155">UserName</span></span> | <span data-ttu-id="11a2c-156">Server\_name\\user\_name</span><span class="sxs-lookup"><span data-stu-id="11a2c-156">Server\_name\\user\_name</span></span><br/><span data-ttu-id="11a2c-157">Localhost\\user\_name</span><span class="sxs-lookup"><span data-stu-id="11a2c-157">Localhost\\user\_name</span></span><br/><span data-ttu-id="11a2c-158">.\\user\_name</span><span class="sxs-lookup"><span data-stu-id="11a2c-158">.\\user\_name</span></span>
<span data-ttu-id="11a2c-159">Felhasználói csoport</span><span class="sxs-lookup"><span data-stu-id="11a2c-159">UserGroup</span></span> | <span data-ttu-id="11a2c-160">Kiszolgáló\_neve\\felhasználói\_csoport</span><span class="sxs-lookup"><span data-stu-id="11a2c-160">Server\_name\\user\_group</span></span><br/><span data-ttu-id="11a2c-161">Localhost\\user\_group</span><span class="sxs-lookup"><span data-stu-id="11a2c-161">Localhost\\user\_group</span></span><br/><span data-ttu-id="11a2c-162">. \\felhasználói\_csoport</span><span class="sxs-lookup"><span data-stu-id="11a2c-162">.\\user\_group</span></span>
<span data-ttu-id="11a2c-163">ComputerGroup</span><span class="sxs-lookup"><span data-stu-id="11a2c-163">ComputerGroup</span></span> | <span data-ttu-id="11a2c-164">Kiszolgáló\_neve\\számítógép\_csoport</span><span class="sxs-lookup"><span data-stu-id="11a2c-164">Server\_name\\computer\_group</span></span><br/><span data-ttu-id="11a2c-165">Localhost\\számítógép\_csoport</span><span class="sxs-lookup"><span data-stu-id="11a2c-165">Localhost\\computer\_group</span></span><br/><span data-ttu-id="11a2c-166">. \\számítógép\_csoport</span><span class="sxs-lookup"><span data-stu-id="11a2c-166">.\\computer\_group</span></span>

#### <a name="gateway-server-is-in-a-domain"></a><span data-ttu-id="11a2c-167">Az átjárókiszolgáló egy tartományhoz tartozik</span><span class="sxs-lookup"><span data-stu-id="11a2c-167">Gateway server is in a domain</span></span>

<span data-ttu-id="11a2c-168">Paraméter</span><span class="sxs-lookup"><span data-stu-id="11a2c-168">Parameter</span></span> | <span data-ttu-id="11a2c-169">Érték</span><span class="sxs-lookup"><span data-stu-id="11a2c-169">Value</span></span>
-- | --
<span data-ttu-id="11a2c-170">ComputerName</span><span class="sxs-lookup"><span data-stu-id="11a2c-170">ComputerName</span></span> | <span data-ttu-id="11a2c-171">Az átjárókiszolgáló teljes neve vagy Localhost</span><span class="sxs-lookup"><span data-stu-id="11a2c-171">Fully qualified name of gateway server, or Localhost</span></span>

#### <a name="gateway-server-is-in-a-workgroup"></a><span data-ttu-id="11a2c-172">Az átjárókiszolgáló egy munkacsoporthoz tartozik</span><span class="sxs-lookup"><span data-stu-id="11a2c-172">Gateway server is in a workgroup</span></span>

<span data-ttu-id="11a2c-173">Paraméter</span><span class="sxs-lookup"><span data-stu-id="11a2c-173">Parameter</span></span> | <span data-ttu-id="11a2c-174">Érték</span><span class="sxs-lookup"><span data-stu-id="11a2c-174">Value</span></span>
-- | --
<span data-ttu-id="11a2c-175">ComputerName</span><span class="sxs-lookup"><span data-stu-id="11a2c-175">ComputerName</span></span> | <span data-ttu-id="11a2c-176">Kiszolgálónév</span><span class="sxs-lookup"><span data-stu-id="11a2c-176">Server name</span></span>

### <a name="gateway-credentials"></a><span data-ttu-id="11a2c-177">Átjáró hitelesítő adatok</span><span class="sxs-lookup"><span data-stu-id="11a2c-177">Gateway credentials</span></span>

<span data-ttu-id="11a2c-178">Jelentkezzen be a célkiszolgálóként működő átjárókiszolgálóra a következők valamelyike szerint formázott hitelesítő adatokkal.</span><span class="sxs-lookup"><span data-stu-id="11a2c-178">Sign in to a gateway server as target computer by using credentials formatted as one of the following.</span></span>

- <span data-ttu-id="11a2c-179">Server\_name\\user\_name</span><span class="sxs-lookup"><span data-stu-id="11a2c-179">Server\_name\\user\_name</span></span>
- <span data-ttu-id="11a2c-180">Localhost\\user\_name</span><span class="sxs-lookup"><span data-stu-id="11a2c-180">Localhost\\user\_name</span></span>
- <span data-ttu-id="11a2c-181">.\\user\_name</span><span class="sxs-lookup"><span data-stu-id="11a2c-181">.\\user\_name</span></span>

## <a name="a-security-identifier-sid-is-displayed-in-an-authorization-rule"></a><span data-ttu-id="11a2c-182">Egy biztonsági azonosítóval (SID) jelenik meg egy engedélyezési szabályban</span><span class="sxs-lookup"><span data-stu-id="11a2c-182">A security identifier (SID) is displayed in an authorization rule</span></span>

<span data-ttu-id="11a2c-183">Egy biztonsági azonosítóval (SID) jelenik meg egy engedélyezési szabályt, a szintaxis felhasználó helyett\_neve/számítógép\_nevét.</span><span class="sxs-lookup"><span data-stu-id="11a2c-183">A security identifier (SID) is displayed in an authorization rule instead of the syntax user\_name/computer\_name.</span></span>

<span data-ttu-id="11a2c-184">Ennek az lehet az oka, hogy a szabály már nem érvényes, vagy az Active Directory tartományi szolgáltatások lekérdezése meghiúsult.</span><span class="sxs-lookup"><span data-stu-id="11a2c-184">Either the rule is no longer valid, or the Active Directory Domain Services query failed.</span></span>
<span data-ttu-id="11a2c-185">Az engedélyezési szabály érvénytelen általában helyzetekben, amikor az átjárókiszolgáló korábban egy munkacsoporthoz tartozott, de aztán egy tartományhoz csatlakoztatták</span><span class="sxs-lookup"><span data-stu-id="11a2c-185">An authorization rule is usually not valid in scenarios where the gateway server was at one time in a workgroup, but was later joined to a domain</span></span>

## <a name="cannot-sign-in-with-rule-as-an-ipv6-address-with-a-domain"></a><span data-ttu-id="11a2c-186">Tartománnyal rendelkező IPv6-címként nem tud bejelentkezni a szabály</span><span class="sxs-lookup"><span data-stu-id="11a2c-186">Cannot sign in with rule as an IPv6 address with a domain</span></span>

<span data-ttu-id="11a2c-187">Nem lehet bejelentkezni egy olyan célszámítógépre, ami az engedélyezési szabályokban tartománnyal rendelkező IPv6-címként lett meghatározva.</span><span class="sxs-lookup"><span data-stu-id="11a2c-187">Cannot sign in to a target computer that has been specified in authorization rules as an IPv6 address with a domain.</span></span>

<span data-ttu-id="11a2c-188">Az engedélyezési szabályok nem támogatják az IPv6-címek használatát a tartománynevekben.</span><span class="sxs-lookup"><span data-stu-id="11a2c-188">Authorization rules do not support an IPv6 address in form of a domain name.</span></span>

<span data-ttu-id="11a2c-189">Ha IPv6-cím használatával szeretne megadni egy célszámítógépet, használja az eredeti (kettőspontokat tartalmazó) IPv6-címet az engedélyezési szabályban.</span><span class="sxs-lookup"><span data-stu-id="11a2c-189">To specify a destination computer by using an IPv6 address, use the original IPv6 address (that contains colons) in the authorization rule.</span></span>
<span data-ttu-id="11a2c-190">A tartomány és a numerikus (kettőspontokat tartalmazó) IPv6-címeket a célszámítógép nevének a Windows PowerShell Web Access bejelentkezési oldal, de az engedélyezési szabályok nem támogatottak.</span><span class="sxs-lookup"><span data-stu-id="11a2c-190">Both domain and numerical (with colons) IPv6 addresses are supported as the target computer name on the Windows PowerShell Web Access sign-in page, but not in authorization rules.</span></span>

<span data-ttu-id="11a2c-191">IPv6-címekre vonatkozó további információkért lásd: [IPv6 működése](https://technet.microsoft.com/library/cc781672(v=ws.10).aspx).</span><span class="sxs-lookup"><span data-stu-id="11a2c-191">For more information about IPv6 addresses, see [How IPv6 Works](https://technet.microsoft.com/library/cc781672(v=ws.10).aspx).</span></span>

## <a name="see-also"></a><span data-ttu-id="11a2c-192">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="11a2c-192">See Also</span></span>

- <span data-ttu-id="11a2c-193">[Az engedélyezési szabályok és a Windows PowerShell Web Access biztonsági funkciói](https://technet.microsoft.com/en-us/library/dn282394(v=ws.11).aspx)</span><span class="sxs-lookup"><span data-stu-id="11a2c-193">[Authorization Rules and Security Features of Windows PowerShell Web Access](https://technet.microsoft.com/en-us/library/dn282394(v=ws.11).aspx)</span></span>
- <span data-ttu-id="11a2c-194">[A webes Windows PowerShell konzol használata](https://technet.microsoft.com/en-us/library/hh831417(v=ws.11).aspx)</span><span class="sxs-lookup"><span data-stu-id="11a2c-194">[Use the Web-based Windows PowerShell Console](https://technet.microsoft.com/en-us/library/hh831417(v=ws.11).aspx)</span></span>
- [<span data-ttu-id="11a2c-195">about_Remote_Requirements</span><span class="sxs-lookup"><span data-stu-id="11a2c-195">about_Remote_Requirements</span></span>](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_remote_requirements)