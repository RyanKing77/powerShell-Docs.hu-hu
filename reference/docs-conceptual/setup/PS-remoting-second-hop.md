---
ms.date: 2017-06-05
keywords: PowerShell parancsmag
title: "A kétugrásos létrehozása a PowerShell-távelérés"
ms.openlocfilehash: 2518409369a75a49b975b9b944320c1878819421
ms.sourcegitcommit: 1a0a0928c1e3cae4e8df8d79b0737bd7ed6b4e47
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/21/2017
---
# <a name="making-the-second-hop-in-powershell-remoting"></a><span data-ttu-id="63cf3-103">A kétugrásos létrehozása a PowerShell-távelérés</span><span class="sxs-lookup"><span data-stu-id="63cf3-103">Making the second hop in PowerShell Remoting</span></span>

<span data-ttu-id="63cf3-104">A "második Ugrás probléma" hivatkozik a helyzet, a következőhöz hasonló:</span><span class="sxs-lookup"><span data-stu-id="63cf3-104">The "second hop problem" refers to a situation like the following:</span></span>

1. <span data-ttu-id="63cf3-105">A bejelentkezett _ServerA_.</span><span class="sxs-lookup"><span data-stu-id="63cf3-105">You are logged in to _ServerA_.</span></span>
2. <span data-ttu-id="63cf3-106">A _ServerA_, a távoli PowerShell-munkamenethez való csatlakozáshoz megkezdése _ServerB_.</span><span class="sxs-lookup"><span data-stu-id="63cf3-106">From _ServerA_, you start a remote PowerShell session to connect to _ServerB_.</span></span>
3. <span data-ttu-id="63cf3-107">A parancs futtatása _ServerB_ keresztül a PowerShell távelérése munkamenet megpróbál hozzáférni egy erőforrást a _ServerC_.</span><span class="sxs-lookup"><span data-stu-id="63cf3-107">A command you run on _ServerB_ via your PowerShell Remoting session attempts to access a resource on _ServerC_.</span></span>
4. <span data-ttu-id="63cf3-108">Az erőforrás elérését a _ServerC_ megtagadva, mert a PowerShell távelérése a munkamenet létrehozásához használt hitelesítő adatok nem adta át az _ServerB_ való _ServerC_.</span><span class="sxs-lookup"><span data-stu-id="63cf3-108">Access to the resource on _ServerC_ is denied, because the credentials you used to create the PowerShell Remoting session are not passed from _ServerB_ to _ServerC_.</span></span>

<span data-ttu-id="63cf3-109">Többféleképpen is a probléma megoldása.</span><span class="sxs-lookup"><span data-stu-id="63cf3-109">There are several ways to address this problem.</span></span> <span data-ttu-id="63cf3-110">Ebben a témakörben megnézzük, a második Ugrás probléma a legnépszerűbb megoldásai számos.</span><span class="sxs-lookup"><span data-stu-id="63cf3-110">In this topic, we'll look at several of the most popular solutions to the second hop problem.</span></span>

## <a name="credssp"></a><span data-ttu-id="63cf3-111">CredSSP</span><span class="sxs-lookup"><span data-stu-id="63cf3-111">CredSSP</span></span>

<span data-ttu-id="63cf3-112">Használhatja a [hitelesítőadat-szolgáltató (CredSSP)](https://msdn.microsoft.com/en-us/library/windows/desktop/bb931352.aspx) hitelesítéshez.</span><span class="sxs-lookup"><span data-stu-id="63cf3-112">You can use the [Credential Security Support Provider (CredSSP)](https://msdn.microsoft.com/en-us/library/windows/desktop/bb931352.aspx) for authentication.</span></span> <span data-ttu-id="63cf3-113">A CredSSP gyorsítótárazza a hitelesítő adatok a távoli kiszolgálón (_ServerB_), így használja megnyílik, akár hitelesítő adatokkal való visszaéléseket támadások.</span><span class="sxs-lookup"><span data-stu-id="63cf3-113">CredSSP caches credentials on the remote server (_ServerB_), so using it opens you up to credential theft attacks.</span></span> <span data-ttu-id="63cf3-114">A távoli számítógép sérült is, ha a támadó megszerezte a felhasználó hitelesítő adatait.</span><span class="sxs-lookup"><span data-stu-id="63cf3-114">If the remote computer is compromised, the attacker has access to the user's credentials.</span></span> <span data-ttu-id="63cf3-115">CredSSP-alapú ügyfél és kiszolgáló egyaránt számítógépeken alapértelmezés szerint le van tiltva.</span><span class="sxs-lookup"><span data-stu-id="63cf3-115">CredSSP is disabled by default on both client and server computers.</span></span> <span data-ttu-id="63cf3-116">Csak a legmegbízhatóbb környezetben engedélyeznie kell a CredSSP-alapú.</span><span class="sxs-lookup"><span data-stu-id="63cf3-116">You should enable CredSSP only in the most trusted environments.</span></span> <span data-ttu-id="63cf3-117">Például a tartományi rendszergazda tartományvezérlő csatlakozik, mert a tartományvezérlő nagymértékben megbízható.</span><span class="sxs-lookup"><span data-stu-id="63cf3-117">For example, a domain administrator connecting to a domain controller because the domain controller is highly trusted.</span></span>

<span data-ttu-id="63cf3-118">További információ a biztonsági szempontok a PowerShell távelérése a CredSSP protokoll használatakor: [véletlen megtámadása: Ne feledje, a CredSSP](http://www.powershellmagazine.com/2014/03/06/accidental-sabotage-beware-of-credssp).</span><span class="sxs-lookup"><span data-stu-id="63cf3-118">For more information about security concerns when using CredSSP for PowerShell Remoting, see [Accidental Sabotage: Beware of CredSSP](http://www.powershellmagazine.com/2014/03/06/accidental-sabotage-beware-of-credssp).</span></span>

<span data-ttu-id="63cf3-119">További információ a hitelesítő adatokkal való visszaéléseket támadások: [letölthető Pass-the-Hash (PtH) támadások és más hitelesítő adatokkal való visszaéléseket](https://www.microsoft.com/en-us/download/details.aspx?id=36036).</span><span class="sxs-lookup"><span data-stu-id="63cf3-119">For more information about credential theft attacks, see [Mitigating Pass-the-Hash (PtH) Attacks and Other Credential Theft](https://www.microsoft.com/en-us/download/details.aspx?id=36036).</span></span>

<span data-ttu-id="63cf3-120">Példa bemutatja, hogyan engedélyezése és használata a CredSSP-alapú a PowerShell távelérése, lásd: [CredSSP használatával a second-hop probléma megoldására](https://blogs.technet.microsoft.com/heyscriptingguy/2012/11/14/enable-powershell-second-hop-functionality-with-credssp/).</span><span class="sxs-lookup"><span data-stu-id="63cf3-120">For an example of how to enable and use CredSSP for PowerShell remoting, see [Using CredSSP to solve the second-hop problem](https://blogs.technet.microsoft.com/heyscriptingguy/2012/11/14/enable-powershell-second-hop-functionality-with-credssp/).</span></span>

### <a name="pros"></a><span data-ttu-id="63cf3-121">Előnyök</span><span class="sxs-lookup"><span data-stu-id="63cf3-121">Pros</span></span>

- <span data-ttu-id="63cf3-122">Az összes Windows Server 2008 vagy újabb működik.</span><span class="sxs-lookup"><span data-stu-id="63cf3-122">It works for all servers with Windows Server 2008 or later.</span></span>

### <a name="cons"></a><span data-ttu-id="63cf3-123">Hátrányok</span><span class="sxs-lookup"><span data-stu-id="63cf3-123">Cons</span></span>

- <span data-ttu-id="63cf3-124">Biztonsági rések rendelkezik.</span><span class="sxs-lookup"><span data-stu-id="63cf3-124">Has security vulnerabilities.</span></span>
- <span data-ttu-id="63cf3-125">Ügyfél- és szerepkör-konfigurációt igényli.</span><span class="sxs-lookup"><span data-stu-id="63cf3-125">Requires configuration of both client and server roles.</span></span>

## <a name="kerberos-delegation-unconstrained"></a><span data-ttu-id="63cf3-126">A Kerberos-delegálás (nem korlátozott)</span><span class="sxs-lookup"><span data-stu-id="63cf3-126">Kerberos delegation (unconstrained)</span></span>

<span data-ttu-id="63cf3-127">Nem korlátozott Kerberos-delegálás a kétugrásos végrehajtásához is használt.</span><span class="sxs-lookup"><span data-stu-id="63cf3-127">You can also used Kerberos unconstrained delegation to make the second hop.</span></span> <span data-ttu-id="63cf3-128">Ez a módszer azonban nem szabályozza, ahol delegált hitelesítő adatokat használja a biztosít.</span><span class="sxs-lookup"><span data-stu-id="63cf3-128">However, this method provides no control of where delegated credentials are used.</span></span>

><span data-ttu-id="63cf3-129">**Megjegyzés:** Active Directory-fiókokat, amelyek rendelkeznek a **fiók bizalmas és nem delegálható** tulajdonságkészlet nem delegálható.</span><span class="sxs-lookup"><span data-stu-id="63cf3-129">**Note:** Active Directory accounts that have the **Account is sensitive and cannot be delegated** property set cannot be delegated.</span></span> <span data-ttu-id="63cf3-130">További információkért lásd: [biztonsági fókusz: "Fiók bizalmas és nem delegálható" kiemelt jogosultságokkal rendelkező fiókok elemzése](https://blogs.technet.microsoft.com/poshchap/2015/05/01/security-focus-analysing-account-is-sensitive-and-cannot-be-delegated-for-privileged-accounts/) és [Kerberos hitelesítési eszközök és beállítások](https://technet.microsoft.com/library/cc738673(v=ws.10).aspx)</span><span class="sxs-lookup"><span data-stu-id="63cf3-130">For more information, see [Security Focus: Analysing 'Account is sensitive and cannot be delegated' for Privileged Accounts](https://blogs.technet.microsoft.com/poshchap/2015/05/01/security-focus-analysing-account-is-sensitive-and-cannot-be-delegated-for-privileged-accounts/) and [Kerberos Authentication Tools and Settings](https://technet.microsoft.com/library/cc738673(v=ws.10).aspx)</span></span>

### <a name="pros"></a><span data-ttu-id="63cf3-131">Előnyök</span><span class="sxs-lookup"><span data-stu-id="63cf3-131">Pros</span></span>

- <span data-ttu-id="63cf3-132">Igényel semmilyen különleges kódolása.</span><span class="sxs-lookup"><span data-stu-id="63cf3-132">Requires no special coding.</span></span>

### <a name="cons"></a><span data-ttu-id="63cf3-133">Hátrányok</span><span class="sxs-lookup"><span data-stu-id="63cf3-133">Cons</span></span>

- <span data-ttu-id="63cf3-134">A WinRM nem támogatja a második Ugrás.</span><span class="sxs-lookup"><span data-stu-id="63cf3-134">Does not support the second hop for WinRM.</span></span>
- <span data-ttu-id="63cf3-135">Nem szabályozhatják, hogy hol használják a hitelesítő adatokat biztosít, a biztonsági rés létrehozása.</span><span class="sxs-lookup"><span data-stu-id="63cf3-135">Provides no control over where credentials are used, creating a security vulnerability.</span></span>

## <a name="kerberos-constrained-delegation"></a><span data-ttu-id="63cf3-136">Kerberos által korlátozott delegálás</span><span class="sxs-lookup"><span data-stu-id="63cf3-136">Kerberos constrained delegation</span></span>

<span data-ttu-id="63cf3-137">(Nem erőforrás-alapú) régebbi a korlátozott delegálás segítségével ellenőrizze a kétugrásos.</span><span class="sxs-lookup"><span data-stu-id="63cf3-137">You can use legacy constrained delegation (not resource-based) to make the second hop.</span></span> 

><span data-ttu-id="63cf3-138">**Megjegyzés:** Active Directory-fiókokat, amelyek rendelkeznek a **fiók bizalmas és nem delegálható** tulajdonságkészlet nem delegálható.</span><span class="sxs-lookup"><span data-stu-id="63cf3-138">**Note:** Active Directory accounts that have the **Account is sensitive and cannot be delegated** property set cannot be delegated.</span></span> <span data-ttu-id="63cf3-139">További információkért lásd: [biztonsági fókusz: "Fiók bizalmas és nem delegálható" kiemelt jogosultságokkal rendelkező fiókok elemzése](https://blogs.technet.microsoft.com/poshchap/2015/05/01/security-focus-analysing-account-is-sensitive-and-cannot-be-delegated-for-privileged-accounts/) és [Kerberos hitelesítési eszközök és beállítások](https://technet.microsoft.com/library/cc738673(v=ws.10).aspx)</span><span class="sxs-lookup"><span data-stu-id="63cf3-139">For more information, see [Security Focus: Analysing 'Account is sensitive and cannot be delegated' for Privileged Accounts](https://blogs.technet.microsoft.com/poshchap/2015/05/01/security-focus-analysing-account-is-sensitive-and-cannot-be-delegated-for-privileged-accounts/) and [Kerberos Authentication Tools and Settings](https://technet.microsoft.com/library/cc738673(v=ws.10).aspx)</span></span>

### <a name="pros"></a><span data-ttu-id="63cf3-140">Előnyök</span><span class="sxs-lookup"><span data-stu-id="63cf3-140">Pros</span></span>

- <span data-ttu-id="63cf3-141">Nincsenek speciális kódolási igényel</span><span class="sxs-lookup"><span data-stu-id="63cf3-141">Requires no special coding</span></span>

### <a name="cons"></a><span data-ttu-id="63cf3-142">Hátrányok</span><span class="sxs-lookup"><span data-stu-id="63cf3-142">Cons</span></span>

- <span data-ttu-id="63cf3-143">A WinRM nem támogatja a második Ugrás.</span><span class="sxs-lookup"><span data-stu-id="63cf3-143">Does not support the second hop for WinRM.</span></span>
- <span data-ttu-id="63cf3-144">Az Active Directory-objektum a távoli kiszolgáló kell konfigurálni (_ServerB_).</span><span class="sxs-lookup"><span data-stu-id="63cf3-144">Must be configured on the Active Directory object of the remote server (_ServerB_).</span></span>
- <span data-ttu-id="63cf3-145">Legfeljebb egyetlen tartományhoz.</span><span class="sxs-lookup"><span data-stu-id="63cf3-145">Limited to one domain.</span></span> <span data-ttu-id="63cf3-146">Nem lehet kereszt-tartományok és erdők.</span><span class="sxs-lookup"><span data-stu-id="63cf3-146">Cannot cross domains or forests.</span></span>
- <span data-ttu-id="63cf3-147">Objektumok és az egyszerű szolgáltatásnevek (SPN) frissítése jogosultságra van szükség.</span><span class="sxs-lookup"><span data-stu-id="63cf3-147">Requires rights to update objects and Service Principal Names (SPNs).</span></span>

## <a name="resource-based-kerberos-constrained-delegation"></a><span data-ttu-id="63cf3-148">Erőforrás-alapú Kerberos által korlátozott delegálás</span><span class="sxs-lookup"><span data-stu-id="63cf3-148">Resource-based Kerberos constrained delegation</span></span>

<span data-ttu-id="63cf3-149">Erőforrás-alapú Kerberos használatával által korlátozott delegálás (a Windows Server 2012-ben bevezetett), a server objektum, amelyen erőforrások találhatók a hitelesítő adatok delegálása tudja konfigurálni.</span><span class="sxs-lookup"><span data-stu-id="63cf3-149">Using resource-based Kerberos constrained delegation (introduced in Windows Server 2012), you configure credential delegation on the server object where resources reside.</span></span>
<span data-ttu-id="63cf3-150">A második ugrásos forgatókönyvet a fent leírt konfigurálja _ServerC_ megadható ahol elfogadja delegált hitelesítő adatokat.</span><span class="sxs-lookup"><span data-stu-id="63cf3-150">In the second hop scenario described above, you configure _ServerC_ to specify from where it will accept delegated credentials.</span></span>

><span data-ttu-id="63cf3-151">**Megjegyzés:** Active Directory-fiókokat, amelyek rendelkeznek a **fiók bizalmas és nem delegálható** tulajdonságkészlet nem delegálható.</span><span class="sxs-lookup"><span data-stu-id="63cf3-151">**Note:** Active Directory accounts that have the **Account is sensitive and cannot be delegated** property set cannot be delegated.</span></span> <span data-ttu-id="63cf3-152">További információkért lásd: [biztonsági fókusz: "Fiók bizalmas és nem delegálható" kiemelt jogosultságokkal rendelkező fiókok elemzése](https://blogs.technet.microsoft.com/poshchap/2015/05/01/security-focus-analysing-account-is-sensitive-and-cannot-be-delegated-for-privileged-accounts/) és [Kerberos hitelesítési eszközök és beállítások](https://technet.microsoft.com/library/cc738673(v=ws.10).aspx)</span><span class="sxs-lookup"><span data-stu-id="63cf3-152">For more information, see [Security Focus: Analysing 'Account is sensitive and cannot be delegated' for Privileged Accounts](https://blogs.technet.microsoft.com/poshchap/2015/05/01/security-focus-analysing-account-is-sensitive-and-cannot-be-delegated-for-privileged-accounts/) and [Kerberos Authentication Tools and Settings](https://technet.microsoft.com/library/cc738673(v=ws.10).aspx)</span></span>

### <a name="pros"></a><span data-ttu-id="63cf3-153">Előnyök</span><span class="sxs-lookup"><span data-stu-id="63cf3-153">Pros</span></span>

- <span data-ttu-id="63cf3-154">Hitelesítő adatok nem kerülnek.</span><span class="sxs-lookup"><span data-stu-id="63cf3-154">Credentials are not stored.</span></span>
- <span data-ttu-id="63cf3-155">Viszonylag könnyen konfigurálható semmilyen különleges kódolás szükséges – PowerShell-parancsmagok használatával.</span><span class="sxs-lookup"><span data-stu-id="63cf3-155">Relatively easy to configure by using PowerShell cmdlets--no special coding required.</span></span>
- <span data-ttu-id="63cf3-156">Nincsenek speciális tartomány-hozzáférés megadása kötelező.</span><span class="sxs-lookup"><span data-stu-id="63cf3-156">No special domain access is required.</span></span>
- <span data-ttu-id="63cf3-157">Tartományok és erdők között működik.</span><span class="sxs-lookup"><span data-stu-id="63cf3-157">Works across domains and forests.</span></span>
- <span data-ttu-id="63cf3-158">PowerShell-kódot.</span><span class="sxs-lookup"><span data-stu-id="63cf3-158">PowerShell code.</span></span>

### <a name="cons"></a><span data-ttu-id="63cf3-159">Hátrányok</span><span class="sxs-lookup"><span data-stu-id="63cf3-159">Cons</span></span>

- <span data-ttu-id="63cf3-160">Windows Server 2012 vagy újabb szükséges.</span><span class="sxs-lookup"><span data-stu-id="63cf3-160">Requires Windows Server 2012 or later.</span></span>
- <span data-ttu-id="63cf3-161">A WinRM nem támogatja a második Ugrás.</span><span class="sxs-lookup"><span data-stu-id="63cf3-161">Does not support the second hop for WinRM.</span></span>
- <span data-ttu-id="63cf3-162">Objektumok és az egyszerű szolgáltatásnevek (SPN) frissítése jogosultságra van szükség.</span><span class="sxs-lookup"><span data-stu-id="63cf3-162">Requires rights to update objects and Service Principal Names (SPNs).</span></span> 

### <a name="example"></a><span data-ttu-id="63cf3-163">Példa</span><span class="sxs-lookup"><span data-stu-id="63cf3-163">Example</span></span>

<span data-ttu-id="63cf3-164">Egy példa, amely erőforrás konfigurálja a korlátozott delegálás alapján PowerShell nézzük _ServerC_ delegált hitelesítő adataival engedélyezi egy _ServerB_.</span><span class="sxs-lookup"><span data-stu-id="63cf3-164">Let's look at a PowerShell example that configures resource based constrained delegation on _ServerC_ to allow delegated credentials from a _ServerB_.</span></span>
<span data-ttu-id="63cf3-165">Ebben a példában feltételezzük, hogy minden kiszolgáló Windows Server 2012 vagy újabb verzióját, és hogy van legalább egy Windows Server 2012 rendszerű tartományvezérlőre mely bármelyik kiszolgálójáról minden tartomány tartozik.</span><span class="sxs-lookup"><span data-stu-id="63cf3-165">This example assumes that all servers are running Windows Server 2012 or later, and that there is at least one Windows Server 2012 domain controller each domain to which any of the servers belong.</span></span>

<span data-ttu-id="63cf3-166">A korlátozott delegálás konfigurálása előtt hozzá kell adnia a `RSAT-AD-PowerShell` funkciót az Active Directory PowerShell-modul telepítéséhez, és importálja a modult abba a munkamenetbe:</span><span class="sxs-lookup"><span data-stu-id="63cf3-166">Before you can configure constrained delegation, you must add the `RSAT-AD-PowerShell` feature to install the Active Directory PowerShell module, and then import that module into your session:</span></span>

```powershell
PS C:\> Add-WindowsFeature RSAT-AD-PowerShell

PS C:\> Import-Module ActiveDirector
```
<span data-ttu-id="63cf3-167">Számos elérhető parancsmagok most már rendelkezik egy **PrincipalsAllowedToDelegateToAccount** paraméter:</span><span class="sxs-lookup"><span data-stu-id="63cf3-167">Several available cmdlets now have a **PrincipalsAllowedToDelegateToAccount** parameter:</span></span>

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

<span data-ttu-id="63cf3-168">A **PrincipalsAllowedToDelegateToAccount** paraméter állandóként állítja be az Active Directory-objektum attribútum **msDS-AllowedToActOnBehalfOfOtherIdentity**, amely tartalmazza a hozzáférés-vezérlési listaként (ACL), Meghatározza, hogy mely fiókok jogosultsága a kapcsolódó fiók a hitelesítő adatok delegálása (a példánkban a számítógépfiókját lesz _Server_).</span><span class="sxs-lookup"><span data-stu-id="63cf3-168">The **PrincipalsAllowedToDelegateToAccount** parameter sets the Active Directory object attribute **msDS-AllowedToActOnBehalfOfOtherIdentity**, which contains an access control list (ACL) that specifies which accounts have permission to delegate credentials to the associated account (in our example, it will be the machine account for _Server_).</span></span>

<span data-ttu-id="63cf3-169">Most már a kiszolgálókat képviselő fogjuk használni a változók beállítása:</span><span class="sxs-lookup"><span data-stu-id="63cf3-169">Now let's set up the variables we'll use to represent the servers:</span></span>

```powershell
# Set up variables for reuse            
$ServerA = $env:COMPUTERNAME            
$ServerB = Get-ADComputer -Identity ServerB            
$ServerC = Get-ADComputer -Identity ServerC            
```

<span data-ttu-id="63cf3-170">A Rendszerfelügyeleti webszolgáltatások (és ezért a PowerShell-távelérést) fiókként fut, a számítógép alapértelmezés szerint.</span><span class="sxs-lookup"><span data-stu-id="63cf3-170">WinRM (and therefore PowerShell remoting) runs as the computer account by default.</span></span> <span data-ttu-id="63cf3-171">Ez bármikor megtekintheti a **StartName** tulajdonsága a `winrm` szolgáltatás:</span><span class="sxs-lookup"><span data-stu-id="63cf3-171">You can see this by looking at the **StartName** property of the `winrm` service:</span></span>

```powershell
PS C:\> Get-WmiObject win32_service -filter 'name="winrm"' | Format-List StartName

StartName : NT AUTHORITY\NetworkService
```

<span data-ttu-id="63cf3-172">A _ServerC_ engedélyezni a PowerShell távelérése munkamenetből a _ServerB_, azt fogja hozzáférést úgy, hogy a **PrincipalsAllowedToDelegateToAccount** a paraméter _ServerC_ a számítógép-objektuma _ServerB_:</span><span class="sxs-lookup"><span data-stu-id="63cf3-172">For _ServerC_ to allow delegation from a PowerShell remoting session on _ServerB_, we will grant access by setting the **PrincipalsAllowedToDelegateToAccount** parameter on _ServerC_ to the computer object of _ServerB_:</span></span>

```powershell
# Grant resource-based Kerberos constrained delegation            
Set-ADComputer -Identity $ServerC -PrincipalsAllowedToDelegateToAccount $ServerB            
            
# Check the value of the attribute directly            
$x = Get-ADComputer -Identity $ServerC -Properties msDS-AllowedToActOnBehalfOfOtherIdentity            
$x.'msDS-AllowedToActOnBehalfOfOtherIdentity'.Access            
            
# Check the value of the attribute indirectly            
Get-ADComputer -Identity $ServerC -Properties PrincipalsAllowedToDelegateToAccount
```

<span data-ttu-id="63cf3-173">A Kerberos [kulcsszolgáltató (KDC)](https://msdn.microsoft.com/library/windows/desktop/aa378170(v=vs.85).aspx) gyorsítótárak megtagadta a hozzáférést kísérletek (negatív gyorsítótárral) 15 percig.</span><span class="sxs-lookup"><span data-stu-id="63cf3-173">The Kerberos [Key Distribution Center (KDC)](https://msdn.microsoft.com/library/windows/desktop/aa378170(v=vs.85).aspx) caches denied access attempts (negative cache) for 15 minutes.</span></span> <span data-ttu-id="63cf3-174">Ha _ServerB_ korábban kísérelt meg hozzáférni _ServerC_, szüksége lesz a gyorsítótárat kiürítheti a _ServerB_ figyelőn a következő parancsot:</span><span class="sxs-lookup"><span data-stu-id="63cf3-174">If _ServerB_ has previously attempted to access _ServerC_, you will need to clear the cache on _ServerB_ by invoking the following command:</span></span>

```powershell
Invoke-Command -ComputerName $ServerB.Name -Credential $cred -ScriptBlock {            
    klist purge -li 0x3e7            
}
```

<span data-ttu-id="63cf3-175">Sikerült továbbá indítsa újra a számítógépet, vagy várjon, amíg a gyorsítótár legalább 15 perc.</span><span class="sxs-lookup"><span data-stu-id="63cf3-175">You could also restart the computer, or wait at least 15 minutes to clear the cache.</span></span>

<span data-ttu-id="63cf3-176">A gyorsítótár kiürítése, miután sikeresen futtathatja kódot _ServerA_ keresztül _ServerB_ való _ServerC_:</span><span class="sxs-lookup"><span data-stu-id="63cf3-176">After clearing the cache, you can successfully run code from _ServerA_ through _ServerB_ to _ServerC_:</span></span>

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

<span data-ttu-id="63cf3-177">Ebben a példában a `$using` változó segítségével ellenőrizze a `$ServerC` változó számára látható _ServerB_.</span><span class="sxs-lookup"><span data-stu-id="63cf3-177">In this example, the `$using` variable is used to make the `$ServerC` variable visible to _ServerB_.</span></span> <span data-ttu-id="63cf3-178">További információ a `$using` változó, lásd: [about_Remote_Variables](https://technet.microsoft.com/en-us/library/jj149005.aspx).</span><span class="sxs-lookup"><span data-stu-id="63cf3-178">For more information about the `$using` variable, see [about_Remote_Variables](https://technet.microsoft.com/en-us/library/jj149005.aspx).</span></span>

<span data-ttu-id="63cf3-179">A több kiszolgálót hitelesítő adatok delegálásának engedélyezése _ServerC_, állítsa be a a **PrincipalsAllowedToDelegateToAccount** paraméter _ServerC_ tömbhöz:</span><span class="sxs-lookup"><span data-stu-id="63cf3-179">To allow multiple servers to delegate credentials to _ServerC_, set the value of the **PrincipalsAllowedToDelegateToAccount** parameter on _ServerC_ to an array:</span></span>

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

<span data-ttu-id="63cf3-180">Ha engedélyezni szeretné a kétugrásos tartományokban, vegye fel teljesen minősített tartománynevét (FQDN) a tartományvezérlő a tartomány, amelyhez _ServerB_ tartozik:</span><span class="sxs-lookup"><span data-stu-id="63cf3-180">If you want to make the second hop across domains, add fully-qualified domain name (FQDN) of the domain controller of the domain to which _ServerB_ belongs:</span></span>

```powershell
# For ServerC in Contoso domain and ServerB in other domain            
$ServerB = Get-ADComputer -Identity ServerB -Server dc1.alpineskihouse.com            
$ServerC = Get-ADComputer -Identity ServerC            
Set-ADComputer -Identity $ServerC -PrincipalsAllowedToDelegateToAccount $ServerB
```

<span data-ttu-id="63cf3-181">ServerC hitelesítő adatok delegálása képes eltávolításához állítsa az értékét a **PrincipalsAllowedToDelegateToAccount** paraméter _ServerC_ való `$null`:</span><span class="sxs-lookup"><span data-stu-id="63cf3-181">To remove the ability to delegate credentials to ServerC, set the value of the **PrincipalsAllowedToDelegateToAccount** parameter on _ServerC_ to `$null`:</span></span>

```powershell
Set-ADComputer -Identity $ServerC -PrincipalsAllowedToDelegateToAccount $null
```

### <a name="information-on-resource-based-kerberos-constrained-delegation"></a><span data-ttu-id="63cf3-182">Információ az erőforrás-alapú Kerberos által korlátozott delegálás</span><span class="sxs-lookup"><span data-stu-id="63cf3-182">Information on resource-based Kerberos constrained delegation</span></span>

- [<span data-ttu-id="63cf3-183">Újdonságok a Kerberos-hitelesítés</span><span class="sxs-lookup"><span data-stu-id="63cf3-183">What's New in Kerberos Authentication</span></span>](https://technet.microsoft.com/library/hh831747.aspx)
- [<span data-ttu-id="63cf3-184">Hogyan Windows Server 2012 használatának egyszerűbbé tétele a problémás a Kerberos által korlátozott delegálást, 1. rész</span><span class="sxs-lookup"><span data-stu-id="63cf3-184">How Windows Server 2012 Eases the Pain of Kerberos Constrained Delegation, Part 1</span></span>](http://windowsitpro.com/security/how-windows-server-2012-eases-pain-kerberos-constrained-delegation-part-1)
- [<span data-ttu-id="63cf3-185">Hogyan Windows Server 2012 használatának egyszerűbbé tétele a problémás a Kerberos által korlátozott delegálást, 2. rész</span><span class="sxs-lookup"><span data-stu-id="63cf3-185">How Windows Server 2012 Eases the Pain of Kerberos Constrained Delegation, Part 2</span></span>](http://windowsitpro.com/security/how-windows-server-2012-eases-pain-kerberos-constrained-delegation-part-2)
- [<span data-ttu-id="63cf3-186">Understanding Kerberos által korlátozott delegálás Proxy alkalmazástelepítésekhez az Azure Active Directory integrált Windows-hitelesítés</span><span class="sxs-lookup"><span data-stu-id="63cf3-186">Understanding Kerberos Constrained Delegation for Azure Active Directory Application Proxy Deployments with Integrated Windows Authentication</span></span>](http://aka.ms/kcdpaper)
- <span data-ttu-id="63cf3-187">[[MS-ADA2]: az Active Directory séma attribútumok M2.210 attribútum az msDS-AllowedToActOnBehalfOfOtherIdentity](https://msdn.microsoft.com/en-us/library/hh554126.aspx)</span><span class="sxs-lookup"><span data-stu-id="63cf3-187">[[MS-ADA2]: Active Directory Schema Attributes M2.210 Attribute msDS-AllowedToActOnBehalfOfOtherIdentity](https://msdn.microsoft.com/en-us/library/hh554126.aspx)</span></span>
- <span data-ttu-id="63cf3-188">[[MS-SFU]: Kerberos Protocol Extensions: Service, a felhasználó- és a korlátozott delegálás protokoll 1.3.2 S4U2proxy](https://msdn.microsoft.com/en-us/library/cc246079.aspx)</span><span class="sxs-lookup"><span data-stu-id="63cf3-188">[[MS-SFU]: Kerberos Protocol Extensions: Service for User and Constrained Delegation Protocol 1.3.2 S4U2proxy](https://msdn.microsoft.com/en-us/library/cc246079.aspx)</span></span>
- [<span data-ttu-id="63cf3-189">Erőforrás-alapú Kerberos által korlátozott delegálás</span><span class="sxs-lookup"><span data-stu-id="63cf3-189">Resource Based Kerberos Constrained Delegation</span></span>](https://blog.kloud.com.au/2013/07/11/kerberos-constrained-delegation/)
- [<span data-ttu-id="63cf3-190">Távoli felügyelet nélkül PrincipalsAllowedToDelegateToAccount használatával korlátozott delegálás</span><span class="sxs-lookup"><span data-stu-id="63cf3-190">Remote Administration Without Constrained Delegation Using PrincipalsAllowedToDelegateToAccount</span></span>](https://blogs.msdn.microsoft.com/taylorb/2012/11/06/remote-administration-without-constrained-delegation-using-principalsallowedtodelegatetoaccount/)

## <a name="pssessionconfiguration-using-runas"></a><span data-ttu-id="63cf3-191">PSSessionConfiguration RunAs használatával</span><span class="sxs-lookup"><span data-stu-id="63cf3-191">PSSessionConfiguration using RunAs</span></span>

<span data-ttu-id="63cf3-192">Létrehozhat egy munkamenet-konfiguráció _ServerB_ és állítsa be a **RunAsCredential** paraméter.</span><span class="sxs-lookup"><span data-stu-id="63cf3-192">You can create a session configuration on _ServerB_ and set its **RunAsCredential** parameter.</span></span>

<span data-ttu-id="63cf3-193">A második Ugrás probléma megoldására PSSessionConfiguration és RunAs használatával kapcsolatos információkért lásd: [Többugrásos PowerShell-távelérést egy másik megoldás](https://blogs.msdn.microsoft.com/sergey_babkins_blog/2015/03/18/another-solution-to-multi-hop-powershell-remoting/).</span><span class="sxs-lookup"><span data-stu-id="63cf3-193">For information about using PSSessionConfiguration and RunAs to solve the second hop problem, see [Another solution to multi-hop PowerShell remoting](https://blogs.msdn.microsoft.com/sergey_babkins_blog/2015/03/18/another-solution-to-multi-hop-powershell-remoting/).</span></span>

### <a name="pros"></a><span data-ttu-id="63cf3-194">Előnyök</span><span class="sxs-lookup"><span data-stu-id="63cf3-194">Pros</span></span>

- <span data-ttu-id="63cf3-195">Bármely kiszolgáló WMF 3.0-s vagy újabb együttműködik.</span><span class="sxs-lookup"><span data-stu-id="63cf3-195">Works with any server with WMF 3.0 or later.</span></span>

### <a name="cons"></a><span data-ttu-id="63cf3-196">Hátrányok</span><span class="sxs-lookup"><span data-stu-id="63cf3-196">Cons</span></span>

- <span data-ttu-id="63cf3-197">A konfigurációt igényel **PSSessionConfiguration** és **RunAs** az összes köztes kiszolgálón (_ServerB_).</span><span class="sxs-lookup"><span data-stu-id="63cf3-197">Requires configuration of **PSSessionConfiguration** and **RunAs** on every intermediate server (_ServerB_).</span></span>
- <span data-ttu-id="63cf3-198">Tartomány használata esetén van szükség a jelszó karbantartási **RunAs** fiók</span><span class="sxs-lookup"><span data-stu-id="63cf3-198">Requires password maintenance when using a domain **RunAs** account</span></span>

## <a name="just-enough-administration-jea"></a><span data-ttu-id="63cf3-199">Éppen elég felügyelettel (JEA)</span><span class="sxs-lookup"><span data-stu-id="63cf3-199">Just Enough Administration (JEA)</span></span>

<span data-ttu-id="63cf3-200">JEA lehetővé teszi, hogy milyen parancsokat rendszergazdaként futtathatja egy PowerShell-munkamenetben korlátozhatja.</span><span class="sxs-lookup"><span data-stu-id="63cf3-200">JEA allows you to restrict what commands an administrator can run during a PowerShell session.</span></span> <span data-ttu-id="63cf3-201">A második Ugrás probléma megoldásához használható.</span><span class="sxs-lookup"><span data-stu-id="63cf3-201">It can be used to solve the second hop problem.</span></span>

<span data-ttu-id="63cf3-202">A JEA kapcsolatos információkért lásd: [csak elég felügyeleti](https://docs.microsoft.com/en-us/powershell/jea/overview).</span><span class="sxs-lookup"><span data-stu-id="63cf3-202">For information about JEA, see [Just Enough Administration](https://docs.microsoft.com/en-us/powershell/jea/overview).</span></span>

### <a name="pros"></a><span data-ttu-id="63cf3-203">Előnyök</span><span class="sxs-lookup"><span data-stu-id="63cf3-203">Pros</span></span>

- <span data-ttu-id="63cf3-204">A virtuális fiók használata esetén nincs jelszó karbantartás.</span><span class="sxs-lookup"><span data-stu-id="63cf3-204">No password maintenance when using a virtual account.</span></span>

### <a name="cons"></a><span data-ttu-id="63cf3-205">Hátrányok</span><span class="sxs-lookup"><span data-stu-id="63cf3-205">Cons</span></span>

- <span data-ttu-id="63cf3-206">WMF 5.0-s vagy újabb szükséges.</span><span class="sxs-lookup"><span data-stu-id="63cf3-206">Requires WMF 5.0 or later.</span></span>
- <span data-ttu-id="63cf3-207">Az összes köztes kiszolgálón konfigurációt igényel (_ServerB_).</span><span class="sxs-lookup"><span data-stu-id="63cf3-207">Requires configuration on every intermediate server (_ServerB_).</span></span>

## <a name="pass-credentials-inside-an-invoke-command-script-block"></a><span data-ttu-id="63cf3-208">Az Invoke-Command parancsprogramblokkba berakni hitelesítő adatok továbbítása</span><span class="sxs-lookup"><span data-stu-id="63cf3-208">Pass credentials inside an Invoke-Command script block</span></span>

<span data-ttu-id="63cf3-209">Hitelesítő adatok belül átadhatók a **ScriptBlock** hívásakor paramétere a [Invoke-Command](https://msdn.microsoft.com/en-us/powershell/reference/5.1/microsoft.powershell.core/invoke-command) parancsmag.</span><span class="sxs-lookup"><span data-stu-id="63cf3-209">You can pass credentials inside the **ScriptBlock** parameter of a call to the [Invoke-Command](https://msdn.microsoft.com/en-us/powershell/reference/5.1/microsoft.powershell.core/invoke-command) cmdlet.</span></span>

### <a name="pros"></a><span data-ttu-id="63cf3-210">Előnyök</span><span class="sxs-lookup"><span data-stu-id="63cf3-210">Pros</span></span>

- <span data-ttu-id="63cf3-211">Nem igényel különleges kiszolgálói beállítást.</span><span class="sxs-lookup"><span data-stu-id="63cf3-211">Does not require special server configuration.</span></span>
- <span data-ttu-id="63cf3-212">2.0-s vagy újabb verziót futtató a WMF egyetlen kiszolgálón működik.</span><span class="sxs-lookup"><span data-stu-id="63cf3-212">Works on any server running WMF 2.0 or later.</span></span>

### <a name="cons"></a><span data-ttu-id="63cf3-213">Hátrányok</span><span class="sxs-lookup"><span data-stu-id="63cf3-213">Cons</span></span>

- <span data-ttu-id="63cf3-214">Egy helyen levő kód eljárást igényel.</span><span class="sxs-lookup"><span data-stu-id="63cf3-214">Requires an awkward code technique.</span></span>
- <span data-ttu-id="63cf3-215">WMF 2.0 fut, ha átadja egy távoli munkamenet argumentumokat igényel különböző szintaxis.</span><span class="sxs-lookup"><span data-stu-id="63cf3-215">If running WMF 2.0, requires different syntax for passing arguments to a remote session.</span></span>

### <a name="example"></a><span data-ttu-id="63cf3-216">Példa</span><span class="sxs-lookup"><span data-stu-id="63cf3-216">Example</span></span>

<span data-ttu-id="63cf3-217">A következő példa bemutatja, hogyan a hitelesítő adatok továbbítása egy **Invoke-Command** parancsfájlblokk:</span><span class="sxs-lookup"><span data-stu-id="63cf3-217">The following example shows how to pass credentials in an **Invoke-Command** script block:</span></span>

```powershell
# This works without delegation, passing fresh creds            
# Note $Using:Cred in nested request            
$cred = Get-Credential Contoso\Administrator            
Invoke-Command -ComputerName ServerB -Credential $cred -ScriptBlock {            
    hostname            
    Invoke-Command -ComputerName ServerC -Credential $Using:cred -ScriptBlock {hostname}            
}
```

## <a name="see-also"></a><span data-ttu-id="63cf3-218">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="63cf3-218">See also</span></span>

[<span data-ttu-id="63cf3-219">PowerShell távoli eljáráshívásainak biztonsági megfontolásai</span><span class="sxs-lookup"><span data-stu-id="63cf3-219">PowerShell Remoting Security Considerations</span></span>](WinRMSecurity.md)








 
