---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: A második Ugrás létrehozása a PowerShell távoli eljáráshívás
ms.openlocfilehash: 06ca43e3e0524d89ec6f66f6553c4c75072beaf3
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/14/2018
ms.locfileid: "53404245"
---
# <a name="making-the-second-hop-in-powershell-remoting"></a><span data-ttu-id="47dfa-103">A második Ugrás létrehozása a PowerShell távoli eljáráshívás</span><span class="sxs-lookup"><span data-stu-id="47dfa-103">Making the second hop in PowerShell Remoting</span></span>

<span data-ttu-id="47dfa-104">A "második Ugrás probléma" hivatkozik olyan helyzet, a következőhöz hasonló:</span><span class="sxs-lookup"><span data-stu-id="47dfa-104">The "second hop problem" refers to a situation like the following:</span></span>

1. <span data-ttu-id="47dfa-105">A bejelentkezett _ServerA_.</span><span class="sxs-lookup"><span data-stu-id="47dfa-105">You are logged in to _ServerA_.</span></span>
2. <span data-ttu-id="47dfa-106">A _ServerA_, szeretne csatlakozni egy távoli PowerShell-munkamenetben megkezdése _ServerB_.</span><span class="sxs-lookup"><span data-stu-id="47dfa-106">From _ServerA_, you start a remote PowerShell session to connect to _ServerB_.</span></span>
3. <span data-ttu-id="47dfa-107">A következő parancsot kell futtatnia a _ServerB_ keresztül a PowerShell távoli eljáráshívás munkamenet próbál elérni egy erőforrást _ServerC_.</span><span class="sxs-lookup"><span data-stu-id="47dfa-107">A command you run on _ServerB_ via your PowerShell Remoting session attempts to access a resource on _ServerC_.</span></span>
4. <span data-ttu-id="47dfa-108">Az erőforráshoz való hozzáférés a _ServerC_ megtagadva, mert a hitelesítő adatokat, a PowerShell-táveléréssel munkamenet létrehozásához használt nem továbbítódnak a _ServerB_ való _ServerC_.</span><span class="sxs-lookup"><span data-stu-id="47dfa-108">Access to the resource on _ServerC_ is denied, because the credentials you used to create the PowerShell Remoting session are not passed from _ServerB_ to _ServerC_.</span></span>

<span data-ttu-id="47dfa-109">Számos módon oldja meg a problémát.</span><span class="sxs-lookup"><span data-stu-id="47dfa-109">There are several ways to address this problem.</span></span> <span data-ttu-id="47dfa-110">Ebben a témakörben áttekintjük számos, a második Ugrás a probléma a legnépszerűbb megoldásokat.</span><span class="sxs-lookup"><span data-stu-id="47dfa-110">In this topic, we'll look at several of the most popular solutions to the second hop problem.</span></span>

## <a name="credssp"></a><span data-ttu-id="47dfa-111">CredSSP</span><span class="sxs-lookup"><span data-stu-id="47dfa-111">CredSSP</span></span>

<span data-ttu-id="47dfa-112">Használhatja a [Credential biztonságitámogatás-szolgáltató (CredSSP)](https://msdn.microsoft.com/library/windows/desktop/bb931352.aspx) a hitelesítéshez.</span><span class="sxs-lookup"><span data-stu-id="47dfa-112">You can use the [Credential Security Support Provider (CredSSP)](https://msdn.microsoft.com/library/windows/desktop/bb931352.aspx) for authentication.</span></span> <span data-ttu-id="47dfa-113">CredSSP gyorsítótárazza a hitelesítő adatokat a távoli kiszolgálón (_ServerB_), így az azt használó megnyílik, akár hitelesítő adatok ellopására irányuló támadásokkal.</span><span class="sxs-lookup"><span data-stu-id="47dfa-113">CredSSP caches credentials on the remote server (_ServerB_), so using it opens you up to credential theft attacks.</span></span> <span data-ttu-id="47dfa-114">Ha a távoli számítógép biztonsága sérül, a támadó rendelkezik a felhasználói hitelesítő adatokkal.</span><span class="sxs-lookup"><span data-stu-id="47dfa-114">If the remote computer is compromised, the attacker has access to the user's credentials.</span></span> <span data-ttu-id="47dfa-115">CredSSP ügyfél és a kiszolgáló számítógépeken alapértelmezés szerint le van tiltva.</span><span class="sxs-lookup"><span data-stu-id="47dfa-115">CredSSP is disabled by default on both client and server computers.</span></span> <span data-ttu-id="47dfa-116">Csak a legmegbízhatóbb környezetben engedélyeznie kell a CredSSP-alapú hitelesítésre.</span><span class="sxs-lookup"><span data-stu-id="47dfa-116">You should enable CredSSP only in the most trusted environments.</span></span> <span data-ttu-id="47dfa-117">Ha például egy tartományi rendszergazda csatlakozik egy tartományvezérlő, mivel a tartományvezérlő nem megbízható.</span><span class="sxs-lookup"><span data-stu-id="47dfa-117">For example, a domain administrator connecting to a domain controller because the domain controller is highly trusted.</span></span>

<span data-ttu-id="47dfa-118">Biztonsági kérdések CredSSP használata esetén a PowerShell-táveléréssel kapcsolatos további információkért lásd: [véletlen megtámadása: Ügyeljen arra, hogy a CredSSP](https://www.powershellmagazine.com/2014/03/06/accidental-sabotage-beware-of-credssp).</span><span class="sxs-lookup"><span data-stu-id="47dfa-118">For more information about security concerns when using CredSSP for PowerShell Remoting, see [Accidental Sabotage: Beware of CredSSP](https://www.powershellmagazine.com/2014/03/06/accidental-sabotage-beware-of-credssp).</span></span>

<span data-ttu-id="47dfa-119">Hitelesítő adatok ellopására irányuló támadásokkal kapcsolatos további információkért lásd: [Mitigating Pass-the-Hash (PtH) támadások és más hitelesítő adatokkal való visszaéléseket](https://www.microsoft.com/en-us/download/details.aspx?id=36036).</span><span class="sxs-lookup"><span data-stu-id="47dfa-119">For more information about credential theft attacks, see [Mitigating Pass-the-Hash (PtH) Attacks and Other Credential Theft](https://www.microsoft.com/en-us/download/details.aspx?id=36036).</span></span>

<span data-ttu-id="47dfa-120">Példa bemutatja, hogyan engedélyezheti és CredSSP használata PowerShell-táveléréssel,: [CredSSP használatával a second-hop probléma megoldására](https://blogs.technet.microsoft.com/heyscriptingguy/2012/11/14/enable-powershell-second-hop-functionality-with-credssp/).</span><span class="sxs-lookup"><span data-stu-id="47dfa-120">For an example of how to enable and use CredSSP for PowerShell remoting, see [Using CredSSP to solve the second-hop problem](https://blogs.technet.microsoft.com/heyscriptingguy/2012/11/14/enable-powershell-second-hop-functionality-with-credssp/).</span></span>

### <a name="pros"></a><span data-ttu-id="47dfa-121">Előnyök</span><span class="sxs-lookup"><span data-stu-id="47dfa-121">Pros</span></span>

- <span data-ttu-id="47dfa-122">Az összes kiszolgálón a Windows Server 2008 vagy újabb működik.</span><span class="sxs-lookup"><span data-stu-id="47dfa-122">It works for all servers with Windows Server 2008 or later.</span></span>

### <a name="cons"></a><span data-ttu-id="47dfa-123">Hátrányok</span><span class="sxs-lookup"><span data-stu-id="47dfa-123">Cons</span></span>

- <span data-ttu-id="47dfa-124">Biztonsági rések rendelkezik.</span><span class="sxs-lookup"><span data-stu-id="47dfa-124">Has security vulnerabilities.</span></span>
- <span data-ttu-id="47dfa-125">Ügyfél- és kiszolgálói szerepkörök konfigurálást igényel.</span><span class="sxs-lookup"><span data-stu-id="47dfa-125">Requires configuration of both client and server roles.</span></span>

## <a name="kerberos-delegation-unconstrained"></a><span data-ttu-id="47dfa-126">A Kerberos-delegálás (nem korlátozott)</span><span class="sxs-lookup"><span data-stu-id="47dfa-126">Kerberos delegation (unconstrained)</span></span>

<span data-ttu-id="47dfa-127">Győződjön meg arról, a második Ugrás végrehajtása a nem korlátozott Kerberos-delegálás is használható.</span><span class="sxs-lookup"><span data-stu-id="47dfa-127">You can also used Kerberos unconstrained delegation to make the second hop.</span></span> <span data-ttu-id="47dfa-128">Ezt a módszert azonban nem szabályozza, ahol szolgálnak a delegált hitelesítő adatokat biztosít.</span><span class="sxs-lookup"><span data-stu-id="47dfa-128">However, this method provides no control of where delegated credentials are used.</span></span>

><span data-ttu-id="47dfa-129">**Megjegyzés:** Active Directory-fiókok, amelyek rendelkeznek a **fiók bizalmas és nem delegálható** tulajdonság beállítása nem delegálható.</span><span class="sxs-lookup"><span data-stu-id="47dfa-129">**Note:** Active Directory accounts that have the **Account is sensitive and cannot be delegated** property set cannot be delegated.</span></span> <span data-ttu-id="47dfa-130">További információkért lásd: [biztonsági fókusz: "Fiók-és nagybetűket, és nem delegálható" elemzése a kiemelt jogosultságokkal rendelkező fiókok](https://blogs.technet.microsoft.com/poshchap/2015/05/01/security-focus-analysing-account-is-sensitive-and-cannot-be-delegated-for-privileged-accounts/) és [Kerberos hitelesítési eszközök és beállítások](https://technet.microsoft.com/library/cc738673(v=ws.10).aspx)</span><span class="sxs-lookup"><span data-stu-id="47dfa-130">For more information, see [Security Focus: Analysing 'Account is sensitive and cannot be delegated' for Privileged Accounts](https://blogs.technet.microsoft.com/poshchap/2015/05/01/security-focus-analysing-account-is-sensitive-and-cannot-be-delegated-for-privileged-accounts/) and [Kerberos Authentication Tools and Settings](https://technet.microsoft.com/library/cc738673(v=ws.10).aspx)</span></span>

### <a name="pros"></a><span data-ttu-id="47dfa-131">Előnyök</span><span class="sxs-lookup"><span data-stu-id="47dfa-131">Pros</span></span>

- <span data-ttu-id="47dfa-132">Szükséges, nincs külön kódolásra.</span><span class="sxs-lookup"><span data-stu-id="47dfa-132">Requires no special coding.</span></span>

### <a name="cons"></a><span data-ttu-id="47dfa-133">Hátrányok</span><span class="sxs-lookup"><span data-stu-id="47dfa-133">Cons</span></span>

- <span data-ttu-id="47dfa-134">A második Ugrás végrehajtása támogatja a winrm.</span><span class="sxs-lookup"><span data-stu-id="47dfa-134">Does not support the second hop for WinRM.</span></span>
- <span data-ttu-id="47dfa-135">Itt nem szabályozza, ahol a hitelesítő adatokat használják, a biztonsági rés létrehozása.</span><span class="sxs-lookup"><span data-stu-id="47dfa-135">Provides no control over where credentials are used, creating a security vulnerability.</span></span>

## <a name="kerberos-constrained-delegation"></a><span data-ttu-id="47dfa-136">Kerberos által korlátozott delegálás</span><span class="sxs-lookup"><span data-stu-id="47dfa-136">Kerberos constrained delegation</span></span>

<span data-ttu-id="47dfa-137">(Nem erőforrás-alapú) régebbi a korlátozott delegálás segítségével győződjön meg arról, a második Ugrás végrehajtása.</span><span class="sxs-lookup"><span data-stu-id="47dfa-137">You can use legacy constrained delegation (not resource-based) to make the second hop.</span></span>

><span data-ttu-id="47dfa-138">**Megjegyzés:** Active Directory-fiókok, amelyek rendelkeznek a **fiók bizalmas és nem delegálható** tulajdonság beállítása nem delegálható.</span><span class="sxs-lookup"><span data-stu-id="47dfa-138">**Note:** Active Directory accounts that have the **Account is sensitive and cannot be delegated** property set cannot be delegated.</span></span> <span data-ttu-id="47dfa-139">További információkért lásd: [biztonsági fókusz: "Fiók-és nagybetűket, és nem delegálható" elemzése a kiemelt jogosultságokkal rendelkező fiókok](https://blogs.technet.microsoft.com/poshchap/2015/05/01/security-focus-analysing-account-is-sensitive-and-cannot-be-delegated-for-privileged-accounts/) és [Kerberos hitelesítési eszközök és beállítások](https://technet.microsoft.com/library/cc738673(v=ws.10).aspx)</span><span class="sxs-lookup"><span data-stu-id="47dfa-139">For more information, see [Security Focus: Analysing 'Account is sensitive and cannot be delegated' for Privileged Accounts](https://blogs.technet.microsoft.com/poshchap/2015/05/01/security-focus-analysing-account-is-sensitive-and-cannot-be-delegated-for-privileged-accounts/) and [Kerberos Authentication Tools and Settings](https://technet.microsoft.com/library/cc738673(v=ws.10).aspx)</span></span>

### <a name="pros"></a><span data-ttu-id="47dfa-140">Előnyök</span><span class="sxs-lookup"><span data-stu-id="47dfa-140">Pros</span></span>

- <span data-ttu-id="47dfa-141">Nincsenek speciális kódolási igényel</span><span class="sxs-lookup"><span data-stu-id="47dfa-141">Requires no special coding</span></span>

### <a name="cons"></a><span data-ttu-id="47dfa-142">Hátrányok</span><span class="sxs-lookup"><span data-stu-id="47dfa-142">Cons</span></span>

- <span data-ttu-id="47dfa-143">A második Ugrás végrehajtása támogatja a winrm.</span><span class="sxs-lookup"><span data-stu-id="47dfa-143">Does not support the second hop for WinRM.</span></span>
- <span data-ttu-id="47dfa-144">Az Active Directory-objektum a távoli kiszolgáló kell konfigurálni (_ServerB_).</span><span class="sxs-lookup"><span data-stu-id="47dfa-144">Must be configured on the Active Directory object of the remote server (_ServerB_).</span></span>
- <span data-ttu-id="47dfa-145">Legfeljebb egyetlen tartományhoz.</span><span class="sxs-lookup"><span data-stu-id="47dfa-145">Limited to one domain.</span></span> <span data-ttu-id="47dfa-146">Nem lehet eltérő tartományok és erdők közötti.</span><span class="sxs-lookup"><span data-stu-id="47dfa-146">Cannot cross domains or forests.</span></span>
- <span data-ttu-id="47dfa-147">A szükséges jogosultsággal az objektumok és az egyszerű szolgáltatásnevek (SPN) frissítéséhez.</span><span class="sxs-lookup"><span data-stu-id="47dfa-147">Requires rights to update objects and Service Principal Names (SPNs).</span></span>

## <a name="resource-based-kerberos-constrained-delegation"></a><span data-ttu-id="47dfa-148">Erőforrás-alapú Kerberos általi korlátozott delegálás</span><span class="sxs-lookup"><span data-stu-id="47dfa-148">Resource-based Kerberos constrained delegation</span></span>

<span data-ttu-id="47dfa-149">Erőforrás-alapú Kerberos használatával által korlátozott delegálás (Windows Server 2012-ben jelent meg), a kiszolgáló objektum erőforrás-ket a hitelesítő adatok delegálása konfigurálja.</span><span class="sxs-lookup"><span data-stu-id="47dfa-149">Using resource-based Kerberos constrained delegation (introduced in Windows Server 2012), you configure credential delegation on the server object where resources reside.</span></span>
<span data-ttu-id="47dfa-150">A második Ugrás a forgatókönyvben a fent leírt konfigurálása _ServerC_ megadható, hogy elfogadja delegált hitelesítő adatokat.</span><span class="sxs-lookup"><span data-stu-id="47dfa-150">In the second hop scenario described above, you configure _ServerC_ to specify from where it will accept delegated credentials.</span></span>

><span data-ttu-id="47dfa-151">**Megjegyzés:** Active Directory-fiókok, amelyek rendelkeznek a **fiók bizalmas és nem delegálható** tulajdonság beállítása nem delegálható.</span><span class="sxs-lookup"><span data-stu-id="47dfa-151">**Note:** Active Directory accounts that have the **Account is sensitive and cannot be delegated** property set cannot be delegated.</span></span> <span data-ttu-id="47dfa-152">További információkért lásd: [biztonsági fókusz: "Fiók-és nagybetűket, és nem delegálható" elemzése a kiemelt jogosultságokkal rendelkező fiókok](https://blogs.technet.microsoft.com/poshchap/2015/05/01/security-focus-analysing-account-is-sensitive-and-cannot-be-delegated-for-privileged-accounts/) és [Kerberos hitelesítési eszközök és beállítások](https://technet.microsoft.com/library/cc738673(v=ws.10).aspx)</span><span class="sxs-lookup"><span data-stu-id="47dfa-152">For more information, see [Security Focus: Analysing 'Account is sensitive and cannot be delegated' for Privileged Accounts](https://blogs.technet.microsoft.com/poshchap/2015/05/01/security-focus-analysing-account-is-sensitive-and-cannot-be-delegated-for-privileged-accounts/) and [Kerberos Authentication Tools and Settings](https://technet.microsoft.com/library/cc738673(v=ws.10).aspx)</span></span>

### <a name="pros"></a><span data-ttu-id="47dfa-153">Előnyök</span><span class="sxs-lookup"><span data-stu-id="47dfa-153">Pros</span></span>

- <span data-ttu-id="47dfa-154">Hitelesítő adatok nem kerülnek.</span><span class="sxs-lookup"><span data-stu-id="47dfa-154">Credentials are not stored.</span></span>
- <span data-ttu-id="47dfa-155">Viszonylag könnyen konfigurálható a PowerShell-parancsmagok – speciális kódírás nélkül.</span><span class="sxs-lookup"><span data-stu-id="47dfa-155">Relatively easy to configure by using PowerShell cmdlets--no special coding required.</span></span>
- <span data-ttu-id="47dfa-156">Nincsenek speciális tartomány hozzáférésre szükség.</span><span class="sxs-lookup"><span data-stu-id="47dfa-156">No special domain access is required.</span></span>
- <span data-ttu-id="47dfa-157">Tartományok és erdők között működik.</span><span class="sxs-lookup"><span data-stu-id="47dfa-157">Works across domains and forests.</span></span>
- <span data-ttu-id="47dfa-158">PowerShell-kódot.</span><span class="sxs-lookup"><span data-stu-id="47dfa-158">PowerShell code.</span></span>

### <a name="cons"></a><span data-ttu-id="47dfa-159">Hátrányok</span><span class="sxs-lookup"><span data-stu-id="47dfa-159">Cons</span></span>

- <span data-ttu-id="47dfa-160">Windows Server 2012 vagy újabb verziója szükséges.</span><span class="sxs-lookup"><span data-stu-id="47dfa-160">Requires Windows Server 2012 or later.</span></span>
- <span data-ttu-id="47dfa-161">A második Ugrás végrehajtása támogatja a winrm.</span><span class="sxs-lookup"><span data-stu-id="47dfa-161">Does not support the second hop for WinRM.</span></span>
- <span data-ttu-id="47dfa-162">A szükséges jogosultsággal az objektumok és az egyszerű szolgáltatásnevek (SPN) frissítéséhez.</span><span class="sxs-lookup"><span data-stu-id="47dfa-162">Requires rights to update objects and Service Principal Names (SPNs).</span></span>

### <a name="example"></a><span data-ttu-id="47dfa-163">Példa</span><span class="sxs-lookup"><span data-stu-id="47dfa-163">Example</span></span>

<span data-ttu-id="47dfa-164">Vegyünk egy példát, amely erőforrás konfigurálja a korlátozott delegálás alapján PowerShell _ServerC_ , hogy a delegált hitelesítő adatokat egy _ServerB_.</span><span class="sxs-lookup"><span data-stu-id="47dfa-164">Let's look at a PowerShell example that configures resource based constrained delegation on _ServerC_ to allow delegated credentials from a _ServerB_.</span></span>
<span data-ttu-id="47dfa-165">Ez a példa feltételezi, hogy az összes kiszolgálón fut a Windows Server 2012 vagy újabb, és legyen legalább egy Windows Server 2012 tartományvezérlőn, mely a kiszolgálók egyikén sincs minden egyes tartományhoz tartozik.</span><span class="sxs-lookup"><span data-stu-id="47dfa-165">This example assumes that all servers are running Windows Server 2012 or later, and that there is at least one Windows Server 2012 domain controller each domain to which any of the servers belong.</span></span>

<span data-ttu-id="47dfa-166">A korlátozott delegálás konfigurálása előtt hozzá kell adnia a `RSAT-AD-PowerShell` funkciót az Active Directory PowerShell-modul telepítéséhez, és importálja a modult a munkamenetbe:</span><span class="sxs-lookup"><span data-stu-id="47dfa-166">Before you can configure constrained delegation, you must add the `RSAT-AD-PowerShell` feature to install the Active Directory PowerShell module, and then import that module into your session:</span></span>

```powershell
PS C:\> Add-WindowsFeature RSAT-AD-PowerShell

PS C:\> Import-Module ActiveDirectory
```
<span data-ttu-id="47dfa-167">Számos elérhető parancsmagjainak most már rendelkezik egy **PrincipalsAllowedToDelegateToAccount** paramétert:</span><span class="sxs-lookup"><span data-stu-id="47dfa-167">Several available cmdlets now have a **PrincipalsAllowedToDelegateToAccount** parameter:</span></span>

```powershell
PS C:\> Get-Command -ParameterName PrincipalsAllowedToDelegateToAccount

CommandType Name                 ModuleName
----------- ----                 ----------
Cmdlet      New-ADComputer       ActiveDirectory
Cmdlet      New-ADServiceAccount ActiveDirectory
Cmdlet      New-ADUser           ActiveDirectory
Cmdlet      Set-ADComputer       ActiveDirectory
Cmdlet      Set-ADServiceAccount ActiveDirectory
Cmdlet      Set-ADUser           ActiveDirectory
```

<span data-ttu-id="47dfa-168">A **PrincipalsAllowedToDelegateToAccount** paraméter állítja be az Active Directory-objektumattribútum **msDS-AllowedToActOnBehalfOfOtherIdentity**, amely tartalmazza a hozzáférés-vezérlési lista (ACL), amely Itt adhatja meg, hogy mely fiókok hitelesítő adatait, a hozzá tartozó fiókot meghatalmazásához engedélyekkel rendelkezik (a példánkban a tartozó számítógépfiók lesz _kiszolgáló_).</span><span class="sxs-lookup"><span data-stu-id="47dfa-168">The **PrincipalsAllowedToDelegateToAccount** parameter sets the Active Directory object attribute **msDS-AllowedToActOnBehalfOfOtherIdentity**, which contains an access control list (ACL) that specifies which accounts have permission to delegate credentials to the associated account (in our example, it will be the machine account for _Server_).</span></span>

<span data-ttu-id="47dfa-169">Most állítsa be a változókat, amelyek a kiszolgálók fogjuk használni:</span><span class="sxs-lookup"><span data-stu-id="47dfa-169">Now let's set up the variables we'll use to represent the servers:</span></span>

```powershell
# Set up variables for reuse
$ServerA = $env:COMPUTERNAME
$ServerB = Get-ADComputer -Identity ServerB
$ServerC = Get-ADComputer -Identity ServerC
```

<span data-ttu-id="47dfa-170">A Rendszerfelügyeleti webszolgáltatások (és így a PowerShell-táveléréssel) fut, a számítógép fiók alapértelmezés szerint.</span><span class="sxs-lookup"><span data-stu-id="47dfa-170">WinRM (and therefore PowerShell remoting) runs as the computer account by default.</span></span> <span data-ttu-id="47dfa-171">Ez naplófájlbejegyzéseket átnézve láthatja a **StartName** tulajdonságát a `winrm` szolgáltatás:</span><span class="sxs-lookup"><span data-stu-id="47dfa-171">You can see this by looking at the **StartName** property of the `winrm` service:</span></span>

```powershell
PS C:\> Get-WmiObject win32_service -filter 'name="winrm"' | Format-List StartName

StartName : NT AUTHORITY\NetworkService
```

<span data-ttu-id="47dfa-172">A _ServerC_ engedélyezni a PowerShell távoli eljáráshívás munkamenetből a _ServerB_, beállításával hozzáférést a Microsoft biztosít a **PrincipalsAllowedToDelegateToAccount** a paraméter _ServerC_ a számítógép-objektumhoz _ServerB_:</span><span class="sxs-lookup"><span data-stu-id="47dfa-172">For _ServerC_ to allow delegation from a PowerShell remoting session on _ServerB_, we will grant access by setting the **PrincipalsAllowedToDelegateToAccount** parameter on _ServerC_ to the computer object of _ServerB_:</span></span>

```powershell
# Grant resource-based Kerberos constrained delegation
Set-ADComputer -Identity $ServerC -PrincipalsAllowedToDelegateToAccount $ServerB

# Check the value of the attribute directly
$x = Get-ADComputer -Identity $ServerC -Properties msDS-AllowedToActOnBehalfOfOtherIdentity
$x.'msDS-AllowedToActOnBehalfOfOtherIdentity'.Access

# Check the value of the attribute indirectly
Get-ADComputer -Identity $ServerC -Properties PrincipalsAllowedToDelegateToAccount
```

<span data-ttu-id="47dfa-173">A Kerberos [kulcsszolgáltató (KDC)](https://msdn.microsoft.com/library/windows/desktop/aa378170(v=vs.85).aspx) gyorsítótárak megtagadva hozzáférési kísérleteket (negatív gyorsítótár) 15 percig.</span><span class="sxs-lookup"><span data-stu-id="47dfa-173">The Kerberos [Key Distribution Center (KDC)](https://msdn.microsoft.com/library/windows/desktop/aa378170(v=vs.85).aspx) caches denied access attempts (negative cache) for 15 minutes.</span></span> <span data-ttu-id="47dfa-174">Ha _ServerB_ korábban megkísérelte elérni _ServerC_, a gyorsítótár ürítése a kell _ServerB_ meghívásával az alábbi parancsot:</span><span class="sxs-lookup"><span data-stu-id="47dfa-174">If _ServerB_ has previously attempted to access _ServerC_, you will need to clear the cache on _ServerB_ by invoking the following command:</span></span>

```powershell
Invoke-Command -ComputerName $ServerB.Name -Credential $cred -ScriptBlock {
    klist purge -li 0x3e7
}
```

<span data-ttu-id="47dfa-175">Ön sikerült is indítsa újra a számítógépet, vagy várjon legalább 15 percet, a gyorsítótár kiürítése.</span><span class="sxs-lookup"><span data-stu-id="47dfa-175">You could also restart the computer, or wait at least 15 minutes to clear the cache.</span></span>

<span data-ttu-id="47dfa-176">A gyorsítótár kiürítése után sikeresen futtathatja a kódot _ServerA_ keresztül _ServerB_ való _ServerC_:</span><span class="sxs-lookup"><span data-stu-id="47dfa-176">After clearing the cache, you can successfully run code from _ServerA_ through _ServerB_ to _ServerC_:</span></span>

```powershell
# Capture a credential
$cred = Get-Credential Contoso\Alice

# Test kerberos double hop
Invoke-Command -ComputerName $ServerB.Name -Credential $cred -ScriptBlock {
    Test-Path \\$($using:ServerC.Name)\C$
    Get-Process lsass -ComputerName $($using:ServerC.Name)
    Get-EventLog -LogName System -Newest 3 -ComputerName $($using:ServerC.Name)
}
```

<span data-ttu-id="47dfa-177">Ebben a példában a `$using` változójával győződjön meg arról, hogy a `$ServerC` változó számára látható _ServerB_.</span><span class="sxs-lookup"><span data-stu-id="47dfa-177">In this example, the `$using` variable is used to make the `$ServerC` variable visible to _ServerB_.</span></span> <span data-ttu-id="47dfa-178">További információ a `$using` változó, lásd: [about_Remote_Variables](https://technet.microsoft.com/library/jj149005.aspx).</span><span class="sxs-lookup"><span data-stu-id="47dfa-178">For more information about the `$using` variable, see [about_Remote_Variables](https://technet.microsoft.com/library/jj149005.aspx).</span></span>

<span data-ttu-id="47dfa-179">A több kiszolgálót a hitelesítő adatok delegálásának engedélyezése _ServerC_, az értékét állítsa be a **PrincipalsAllowedToDelegateToAccount** paraméterrel _ServerC_ egy tömbre:</span><span class="sxs-lookup"><span data-stu-id="47dfa-179">To allow multiple servers to delegate credentials to _ServerC_, set the value of the **PrincipalsAllowedToDelegateToAccount** parameter on _ServerC_ to an array:</span></span>

```powershell
# Set up variables for each server
$ServerB1 = Get-ADComputer -Identity ServerB1
$ServerB2 = Get-ADComputer -Identity ServerB2
$ServerB3 = Get-ADComputer -Identity ServerB3
$ServerC  = Get-ADComputer -Identity ServerC

# Grant resource-based Kerberos constrained delegation
Set-ADComputer -Identity $ServerC `
    -PrincipalsAllowedToDelegateToAccount @($ServerB1,$ServerB2,$ServerB3)
```

<span data-ttu-id="47dfa-180">Ha azt szeretné, hogy a második Ugrás végrehajtása a tartományok között, adjon hozzá teljes tartománynév (FQDN) a tartományvezérlő a tartomány, amelyhez _ServerB_ tartozik:</span><span class="sxs-lookup"><span data-stu-id="47dfa-180">If you want to make the second hop across domains, add fully-qualified domain name (FQDN) of the domain controller of the domain to which _ServerB_ belongs:</span></span>

```powershell
# For ServerC in Contoso domain and ServerB in other domain
$ServerB = Get-ADComputer -Identity ServerB -Server dc1.alpineskihouse.com
$ServerC = Get-ADComputer -Identity ServerC
Set-ADComputer -Identity $ServerC -PrincipalsAllowedToDelegateToAccount $ServerB
```

<span data-ttu-id="47dfa-181">Lehetővé teszi a ServerC hitelesítő adatok delegálása eltávolításához állítsa az értékét a **PrincipalsAllowedToDelegateToAccount** paraméterrel _ServerC_ való `$null`:</span><span class="sxs-lookup"><span data-stu-id="47dfa-181">To remove the ability to delegate credentials to ServerC, set the value of the **PrincipalsAllowedToDelegateToAccount** parameter on _ServerC_ to `$null`:</span></span>

```powershell
Set-ADComputer -Identity $ServerC -PrincipalsAllowedToDelegateToAccount $null
```

### <a name="information-on-resource-based-kerberos-constrained-delegation"></a><span data-ttu-id="47dfa-182">Információk az erőforrás-alapú Kerberos általi korlátozott delegálás</span><span class="sxs-lookup"><span data-stu-id="47dfa-182">Information on resource-based Kerberos constrained delegation</span></span>

- [<span data-ttu-id="47dfa-183">Újdonságok a Kerberos-hitelesítés</span><span class="sxs-lookup"><span data-stu-id="47dfa-183">What's New in Kerberos Authentication</span></span>](https://technet.microsoft.com/library/hh831747.aspx)
- [<span data-ttu-id="47dfa-184">Hogyan Windows Server 2012 használatának egyszerűbbé tétele a problémás Kerberos által korlátozott delegálást, 1. rész</span><span class="sxs-lookup"><span data-stu-id="47dfa-184">How Windows Server 2012 Eases the Pain of Kerberos Constrained Delegation, Part 1</span></span>](https://windowsitpro.com/security/how-windows-server-2012-eases-pain-kerberos-constrained-delegation-part-1)
- [<span data-ttu-id="47dfa-185">Hogyan Windows Server 2012 használatának egyszerűbbé tétele a problémás Kerberos által korlátozott delegálást, 2. rész</span><span class="sxs-lookup"><span data-stu-id="47dfa-185">How Windows Server 2012 Eases the Pain of Kerberos Constrained Delegation, Part 2</span></span>](https://windowsitpro.com/security/how-windows-server-2012-eases-pain-kerberos-constrained-delegation-part-2)
- [<span data-ttu-id="47dfa-186">Understanding Kerberos általi korlátozott delegálás az Azure Active Directory Application Proxy központi telepítéseknél integrált Windows-hitelesítés</span><span class="sxs-lookup"><span data-stu-id="47dfa-186">Understanding Kerberos Constrained Delegation for Azure Active Directory Application Proxy Deployments with Integrated Windows Authentication</span></span>](https://aka.ms/kcdpaper)
- <span data-ttu-id="47dfa-187">[[MS-ADA2]: Az Active Directory séma attribútumok M2.210 attribútum msDS-AllowedToActOnBehalfOfOtherIdentity](https://msdn.microsoft.com/library/hh554126.aspx)</span><span class="sxs-lookup"><span data-stu-id="47dfa-187">[[MS-ADA2]: Active Directory Schema Attributes M2.210 Attribute msDS-AllowedToActOnBehalfOfOtherIdentity](https://msdn.microsoft.com/library/hh554126.aspx)</span></span>
- <span data-ttu-id="47dfa-188">[[MS-SFU]: Kerberos-protokoll kiterjesztései: Felhasználó és a korlátozott delegálás protokoll 1.3.2 S4U2proxy szolgáltatás](https://msdn.microsoft.com/library/cc246079.aspx)</span><span class="sxs-lookup"><span data-stu-id="47dfa-188">[[MS-SFU]: Kerberos Protocol Extensions: Service for User and Constrained Delegation Protocol 1.3.2 S4U2proxy](https://msdn.microsoft.com/library/cc246079.aspx)</span></span>
- [<span data-ttu-id="47dfa-189">Erőforrás-alapú Kerberos által korlátozott delegálás</span><span class="sxs-lookup"><span data-stu-id="47dfa-189">Resource Based Kerberos Constrained Delegation</span></span>](https://blog.kloud.com.au/2013/07/11/kerberos-constrained-delegation/)
- [<span data-ttu-id="47dfa-190">Távoli felügyelet nélkül PrincipalsAllowedToDelegateToAccount használatával korlátozott delegálás</span><span class="sxs-lookup"><span data-stu-id="47dfa-190">Remote Administration Without Constrained Delegation Using PrincipalsAllowedToDelegateToAccount</span></span>](https://blogs.msdn.microsoft.com/taylorb/2012/11/06/remote-administration-without-constrained-delegation-using-principalsallowedtodelegatetoaccount/)

## <a name="pssessionconfiguration-using-runas"></a><span data-ttu-id="47dfa-191">PSSessionConfiguration RunAs használatával</span><span class="sxs-lookup"><span data-stu-id="47dfa-191">PSSessionConfiguration using RunAs</span></span>

<span data-ttu-id="47dfa-192">Létrehozhat egy munkamenet-konfiguráció _ServerB_ , és állítsa annak **RunAsCredential** paraméter.</span><span class="sxs-lookup"><span data-stu-id="47dfa-192">You can create a session configuration on _ServerB_ and set its **RunAsCredential** parameter.</span></span>

<span data-ttu-id="47dfa-193">A második Ugrás a probléma megoldásához PSSessionConfiguration és futtató használatával kapcsolatos információkért lásd: [Többugrásos PowerShell távoli eljáráshívás egy másik megoldás](https://blogs.msdn.microsoft.com/sergey_babkins_blog/2015/03/18/another-solution-to-multi-hop-powershell-remoting/).</span><span class="sxs-lookup"><span data-stu-id="47dfa-193">For information about using PSSessionConfiguration and RunAs to solve the second hop problem, see [Another solution to multi-hop PowerShell remoting](https://blogs.msdn.microsoft.com/sergey_babkins_blog/2015/03/18/another-solution-to-multi-hop-powershell-remoting/).</span></span>

### <a name="pros"></a><span data-ttu-id="47dfa-194">Előnyök</span><span class="sxs-lookup"><span data-stu-id="47dfa-194">Pros</span></span>

- <span data-ttu-id="47dfa-195">Minden olyan kiszolgáló, a WMF 3.0-s vagy újabb együttműködik.</span><span class="sxs-lookup"><span data-stu-id="47dfa-195">Works with any server with WMF 3.0 or later.</span></span>

### <a name="cons"></a><span data-ttu-id="47dfa-196">Hátrányok</span><span class="sxs-lookup"><span data-stu-id="47dfa-196">Cons</span></span>

- <span data-ttu-id="47dfa-197">A konfigurálást igényel **PSSessionConfiguration** és **RunAs** az összes köztes kiszolgálón (_ServerB_).</span><span class="sxs-lookup"><span data-stu-id="47dfa-197">Requires configuration of **PSSessionConfiguration** and **RunAs** on every intermediate server (_ServerB_).</span></span>
- <span data-ttu-id="47dfa-198">Tartomány használata esetén van szükség a jelszó karbantartási **RunAs** fiók</span><span class="sxs-lookup"><span data-stu-id="47dfa-198">Requires password maintenance when using a domain **RunAs** account</span></span>

## <a name="just-enough-administration-jea"></a><span data-ttu-id="47dfa-199">Just Enough Administration (JEA)</span><span class="sxs-lookup"><span data-stu-id="47dfa-199">Just Enough Administration (JEA)</span></span>

<span data-ttu-id="47dfa-200">A JEA lehetővé teszi, hogy milyen parancsokat rendszergazdaként egy PowerShell-munkamenetben futtathatja korlátozása.</span><span class="sxs-lookup"><span data-stu-id="47dfa-200">JEA allows you to restrict what commands an administrator can run during a PowerShell session.</span></span> <span data-ttu-id="47dfa-201">A második Ugrás a probléma megoldásához használható.</span><span class="sxs-lookup"><span data-stu-id="47dfa-201">It can be used to solve the second hop problem.</span></span>

<span data-ttu-id="47dfa-202">A JEA kapcsolatos információkért lásd: [Just Enough Administration](https://docs.microsoft.com/powershell/jea/overview).</span><span class="sxs-lookup"><span data-stu-id="47dfa-202">For information about JEA, see [Just Enough Administration](https://docs.microsoft.com/powershell/jea/overview).</span></span>

### <a name="pros"></a><span data-ttu-id="47dfa-203">Előnyök</span><span class="sxs-lookup"><span data-stu-id="47dfa-203">Pros</span></span>

- <span data-ttu-id="47dfa-204">Jelszó karbantartás virtuális fiók használata esetén.</span><span class="sxs-lookup"><span data-stu-id="47dfa-204">No password maintenance when using a virtual account.</span></span>

### <a name="cons"></a><span data-ttu-id="47dfa-205">Hátrányok</span><span class="sxs-lookup"><span data-stu-id="47dfa-205">Cons</span></span>

- <span data-ttu-id="47dfa-206">A WMF 5.0 vagy újabb verzió szükséges.</span><span class="sxs-lookup"><span data-stu-id="47dfa-206">Requires WMF 5.0 or later.</span></span>
- <span data-ttu-id="47dfa-207">Az összes köztes kiszolgálón konfigurációt igényel (_ServerB_).</span><span class="sxs-lookup"><span data-stu-id="47dfa-207">Requires configuration on every intermediate server (_ServerB_).</span></span>

## <a name="pass-credentials-inside-an-invoke-command-script-block"></a><span data-ttu-id="47dfa-208">Az Invoke-Command parancsfájl-blokkon belül hitelesítő adatokat küldenie</span><span class="sxs-lookup"><span data-stu-id="47dfa-208">Pass credentials inside an Invoke-Command script block</span></span>

<span data-ttu-id="47dfa-209">Hitelesítő adatok belül átadható a **ScriptBlock** paraméter hívása a [Invoke-Command](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/invoke-command) parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="47dfa-209">You can pass credentials inside the **ScriptBlock** parameter of a call to the [Invoke-Command](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/invoke-command) cmdlet.</span></span>

### <a name="pros"></a><span data-ttu-id="47dfa-210">Előnyök</span><span class="sxs-lookup"><span data-stu-id="47dfa-210">Pros</span></span>

- <span data-ttu-id="47dfa-211">Nem igényel különleges kiszolgáló konfigurációját.</span><span class="sxs-lookup"><span data-stu-id="47dfa-211">Does not require special server configuration.</span></span>
- <span data-ttu-id="47dfa-212">A WMF használó 2.0-s vagy újabb működik.</span><span class="sxs-lookup"><span data-stu-id="47dfa-212">Works on any server running WMF 2.0 or later.</span></span>

### <a name="cons"></a><span data-ttu-id="47dfa-213">Hátrányok</span><span class="sxs-lookup"><span data-stu-id="47dfa-213">Cons</span></span>

- <span data-ttu-id="47dfa-214">Egy helyen levő kód módszert igényel.</span><span class="sxs-lookup"><span data-stu-id="47dfa-214">Requires an awkward code technique.</span></span>
- <span data-ttu-id="47dfa-215">A WMF 2.0 fut, ha szükséges különböző szintaktikai argumentumoknak a távoli munkamenetet.</span><span class="sxs-lookup"><span data-stu-id="47dfa-215">If running WMF 2.0, requires different syntax for passing arguments to a remote session.</span></span>

### <a name="example"></a><span data-ttu-id="47dfa-216">Példa</span><span class="sxs-lookup"><span data-stu-id="47dfa-216">Example</span></span>

<span data-ttu-id="47dfa-217">Az alábbi példa bemutatja, hogyan adhatók át a hitelesítő adatokat egy **Invoke-Command** parancsprogram-blokkot:</span><span class="sxs-lookup"><span data-stu-id="47dfa-217">The following example shows how to pass credentials in an **Invoke-Command** script block:</span></span>

```powershell
# This works without delegation, passing fresh creds
# Note $Using:Cred in nested request
$cred = Get-Credential Contoso\Administrator
Invoke-Command -ComputerName ServerB -Credential $cred -ScriptBlock {
    hostname
    Invoke-Command -ComputerName ServerC -Credential $Using:cred -ScriptBlock {hostname}
}
```

## <a name="see-also"></a><span data-ttu-id="47dfa-218">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="47dfa-218">See also</span></span>

[<span data-ttu-id="47dfa-219">PowerShell távoli eljáráshívásainak biztonsági megfontolásai</span><span class="sxs-lookup"><span data-stu-id="47dfa-219">PowerShell Remoting Security Considerations</span></span>](WinRMSecurity.md)