---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "A DSC használata a Nano Server"
ms.openlocfilehash: c8f3669ee9c2ed6107c14ba9f4460d82276e1932
ms.sourcegitcommit: 99227f62dcf827354770eb2c3e95c5cf6a3118b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/15/2018
---
# <a name="using-dsc-on-nano-server"></a><span data-ttu-id="666dd-103">A DSC használata a Nano Server</span><span class="sxs-lookup"><span data-stu-id="666dd-103">Using DSC on Nano Server</span></span>

> <span data-ttu-id="666dd-104">Vonatkozik: A Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="666dd-104">Applies To: Windows PowerShell 5.0</span></span>

<span data-ttu-id="666dd-105">**A Nano Server DSC** egy választható csomag van a `NanoServer\Packages` a Windows Server 2016 adathordozó mappájában.</span><span class="sxs-lookup"><span data-stu-id="666dd-105">**DSC on Nano Server** is an optional package in the `NanoServer\Packages` folder of the Windows Server 2016 media.</span></span> <span data-ttu-id="666dd-106">A csomag létrehozásakor a virtuális merevlemez a Nano Server megadásával telepítésének **Microsoft-NanoServer-DSC-csomag** értékeként a **csomagok** paramétere a **új-NanoServerImage**  függvény.</span><span class="sxs-lookup"><span data-stu-id="666dd-106">The package can be installed when you create a VHD for a Nano Server by specifying **Microsoft-NanoServer-DSC-Package** as the value of the **Packages** parameter of the **New-NanoServerImage** function.</span></span> <span data-ttu-id="666dd-107">Például ha egy virtuális gép virtuális hoz létre, a parancs volna a következőhöz hasonló:</span><span class="sxs-lookup"><span data-stu-id="666dd-107">For example, if you are creating a VHD for a virtual machine, the command would look like the following:</span></span>

```powershell
New-NanoServerImage -Edition Standard -DeploymentType Guest -MediaPath f:\ -BasePath .\Base -TargetPath .\Nano1\Nano.vhd -ComputerName Nano1 -Packages Microsoft-NanoServer-DSC-Package
```

<span data-ttu-id="666dd-108">További információ a telepítéséről és használatáról a Nano Server, valamint kezelése a PowerShell távelérése a Nano Server: [Ismerkedés a Nano Server](https://technet.microsoft.com/library/mt126167.aspx).</span><span class="sxs-lookup"><span data-stu-id="666dd-108">For information about installing and using Nano Server, as well as how to manage Nano Server with PowerShell Remoting, see [Getting Started with Nano Server](https://technet.microsoft.com/library/mt126167.aspx).</span></span>


## <a name="dsc-features-available-on-nano-server"></a><span data-ttu-id="666dd-109">A DSC szolgáltatás Nano Server</span><span class="sxs-lookup"><span data-stu-id="666dd-109">DSC features available on Nano Server</span></span>

 <span data-ttu-id="666dd-110">Mivel a Nano Server támogatja a Windows Server teljes verzióját képest API-kat csak korlátozott számú, a Nano Server DSC nem rendelkezik teljes funkciói egyenértékűek teljes termékváltozatok jelenleg futó DSC.</span><span class="sxs-lookup"><span data-stu-id="666dd-110">Because Nano Server supports only a limited set of APIs compared to a full version of Windows Server, DSC on Nano Server does not have full functional parity with DSC running on full SKUs for the time being.</span></span> <span data-ttu-id="666dd-111">A Nano Server DSC aktív fejlesztés, és még nincs kész szolgáltatás.</span><span class="sxs-lookup"><span data-stu-id="666dd-111">DSC on Nano Server is in active development and is not yet feature complete.</span></span>
 
 <span data-ttu-id="666dd-112">A következő DSC-funkciók érhetők el jelenleg a Nano Server:</span><span class="sxs-lookup"><span data-stu-id="666dd-112">The following DSC features are currently available on Nano Server:</span></span> 


* <span data-ttu-id="666dd-113">Mind eseménylekérési és eseményküldési módban</span><span class="sxs-lookup"><span data-stu-id="666dd-113">Both push and pull modes</span></span>

* <span data-ttu-id="666dd-114">Minden DSC-parancsmag a teljes verzióját a Windows Server, beleértve a következőket:</span><span class="sxs-lookup"><span data-stu-id="666dd-114">All DSC cmdlets that exist on a full version of Windows Server, including the following:</span></span> 
  * [<span data-ttu-id="666dd-115">Get-DscLocalConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="666dd-115">Get-DscLocalConfigurationManager</span></span>](https://technet.microsoft.com/library/dn407378.aspx)
  * [<span data-ttu-id="666dd-116">Set-DscLocalConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="666dd-116">Set-DscLocalConfigurationManager</span></span>](https://technet.microsoft.com/library/dn521621.aspx)     
  * [<span data-ttu-id="666dd-117">Enable-DscDebug</span><span class="sxs-lookup"><span data-stu-id="666dd-117">Enable-DscDebug</span></span>](https://technet.microsoft.com/en-us/library/mt517870.aspx)
  * [<span data-ttu-id="666dd-118">Disable-DscDebug</span><span class="sxs-lookup"><span data-stu-id="666dd-118">Disable-DscDebug</span></span>](https://technet.microsoft.com/en-us/library/mt517872.aspx)       
  * [<span data-ttu-id="666dd-119">Start-DscConfiguration</span><span class="sxs-lookup"><span data-stu-id="666dd-119">Start-DscConfiguration</span></span>](https://technet.microsoft.com/en-us/library/dn521623.aspx)
  * [<span data-ttu-id="666dd-120">Stop-DscConfiguration</span><span class="sxs-lookup"><span data-stu-id="666dd-120">Stop-DscConfiguration</span></span>](https://technet.microsoft.com/en-us/library/mt143542.aspx)
  * [<span data-ttu-id="666dd-121">Get-DscConfiguration</span><span class="sxs-lookup"><span data-stu-id="666dd-121">Get-DscConfiguration</span></span>](https://technet.microsoft.com/en-us/library/dn407379.aspx)
  * [<span data-ttu-id="666dd-122">Test-DscConfiguration</span><span class="sxs-lookup"><span data-stu-id="666dd-122">Test-DscConfiguration</span></span>](https://technet.microsoft.com/en-us/library/dn407382.aspx)      
  * [<span data-ttu-id="666dd-123">Publish-DscConfiguraiton</span><span class="sxs-lookup"><span data-stu-id="666dd-123">Publish-DscConfiguraiton</span></span>](https://technet.microsoft.com/en-us/library/mt517875.aspx) 
  * [<span data-ttu-id="666dd-124">Update-DscConfiguration</span><span class="sxs-lookup"><span data-stu-id="666dd-124">Update-DscConfiguration</span></span>](https://technet.microsoft.com/en-us/library/mt143541.aspx)
  * [<span data-ttu-id="666dd-125">Restore-DscConfiguration</span><span class="sxs-lookup"><span data-stu-id="666dd-125">Restore-DscConfiguration</span></span>](https://technet.microsoft.com/en-us/library/dn407383.aspx)
  * [<span data-ttu-id="666dd-126">Remove-DscConfigurationDocument</span><span class="sxs-lookup"><span data-stu-id="666dd-126">Remove-DscConfigurationDocument</span></span>](https://technet.microsoft.com/en-us/library/mt143544.aspx)
  * [<span data-ttu-id="666dd-127">Get-DscConfigurationStatus</span><span class="sxs-lookup"><span data-stu-id="666dd-127">Get-DscConfigurationStatus</span></span>](https://technet.microsoft.com/en-us/library/mt517868.aspx)
  * [<span data-ttu-id="666dd-128">Invoke-DscResource</span><span class="sxs-lookup"><span data-stu-id="666dd-128">Invoke-DscResource</span></span>](https://technet.microsoft.com/en-us/library/mt517869.aspx)
  * [<span data-ttu-id="666dd-129">Keresés – DscResource</span><span class="sxs-lookup"><span data-stu-id="666dd-129">Find-DscResource</span></span>](https://technet.microsoft.com/en-us/library/mt517874.aspx)
  * [<span data-ttu-id="666dd-130">Get-DscResource</span><span class="sxs-lookup"><span data-stu-id="666dd-130">Get-DscResource</span></span>](https://technet.microsoft.com/en-us/library/dn521625.aspx)
  * [<span data-ttu-id="666dd-131">Új DscChecksum</span><span class="sxs-lookup"><span data-stu-id="666dd-131">New-DscChecksum</span></span>](https://technet.microsoft.com/en-us/library/dn521622.aspx)    

* <span data-ttu-id="666dd-132">Konfiguráció fordítása (lásd: [a DSC-konfigurációk](configurations.md))</span><span class="sxs-lookup"><span data-stu-id="666dd-132">Compiling configurations (see [DSC configurations](configurations.md))</span></span>

  <span data-ttu-id="666dd-133">**Probléma:** jelszó-titkosítási (lásd: [biztonságossá tétele a MOF-fájlt](securemof.md)) konfigurálása során fordítás nem működik.</span><span class="sxs-lookup"><span data-stu-id="666dd-133">**Issue:** Password encryption (see [Securing the MOF File](securemof.md)) during configuration compilation doesn't work.</span></span>

* <span data-ttu-id="666dd-134">Metaconfigurations fordítása (lásd: [konfigurálása a helyi Configuration Manager](metaConfig.md))</span><span class="sxs-lookup"><span data-stu-id="666dd-134">Compiling metaconfigurations (see [Configuring the Local Configuration Manager](metaConfig.md))</span></span>

* <span data-ttu-id="666dd-135">Egy erőforrás felhasználó környezetében futó (lásd: [DSC futtató felhasználó hitelesítő adataival (RunAs)](runAsUser.md))</span><span class="sxs-lookup"><span data-stu-id="666dd-135">Running a resource under user context (see [Running DSC with user credentials (RunAs)](runAsUser.md))</span></span>

* <span data-ttu-id="666dd-136">Az osztály-alapú erőforrások (lásd: [PowerShell osztályokra egyéni DSC-erőforrás írása](authoringResourceClass.md))</span><span class="sxs-lookup"><span data-stu-id="666dd-136">Class-based resources (see [Writing a custom DSC resource with PowerShell classes](authoringResourceClass.md))</span></span>

* <span data-ttu-id="666dd-137">A DSC-erőforrások hibakeresés (lásd: [hibakeresés DSC erőforrások](debugresource.md))</span><span class="sxs-lookup"><span data-stu-id="666dd-137">Debugging of DSC resources (see [Debugging DSC resources](debugresource.md))</span></span>
  
  <span data-ttu-id="666dd-138">**Probléma:** nem működik, ha egy erőforrás PsDscRunAsCredential használ (lásd: [felhasználói hitelesítő adatokkal rendelkező futtató DSC](runAsUser.md))</span><span class="sxs-lookup"><span data-stu-id="666dd-138">**Issue:** Doesn't work if a resource is using PsDscRunAsCredential (see [Running DSC with user credentials](runAsUser.md))</span></span>

* [<span data-ttu-id="666dd-139">Csomópontok közötti függőségek megadása</span><span class="sxs-lookup"><span data-stu-id="666dd-139">Specifying cross-node dependencies</span></span>](crossNodeDependencies.md) 

* [<span data-ttu-id="666dd-140">Erőforrás versioning</span><span class="sxs-lookup"><span data-stu-id="666dd-140">Resource versioning</span></span>](sxsResource.md)

* <span data-ttu-id="666dd-141">Lekéréses ügyfél (konfigurációk és erőforrások) (lásd: [ügyféltelepítéshez lekéréses konfigurációs nevek használatával](pullClientConfigNames.md))</span><span class="sxs-lookup"><span data-stu-id="666dd-141">Pull client (configurations & resources) (see [Setting up a pull client using configuration names](pullClientConfigNames.md))</span></span>

* [<span data-ttu-id="666dd-142">Részleges konfigurációk (lekéréses & leküldéses)</span><span class="sxs-lookup"><span data-stu-id="666dd-142">Partial configurations (pull & push)</span></span>](partialConfigs.md)

* [<span data-ttu-id="666dd-143">A lekérési kiszolgálójával Reporting</span><span class="sxs-lookup"><span data-stu-id="666dd-143">Reporting to pull server</span></span>](reportServer.md) 

* <span data-ttu-id="666dd-144">MOF-titkosítás</span><span class="sxs-lookup"><span data-stu-id="666dd-144">MOF encryption</span></span>

* <span data-ttu-id="666dd-145">Események naplózása</span><span class="sxs-lookup"><span data-stu-id="666dd-145">Event logging</span></span>

* <span data-ttu-id="666dd-146">Azure Automation DSC-jelentés</span><span class="sxs-lookup"><span data-stu-id="666dd-146">Azure Automation DSC reporting</span></span>

* <span data-ttu-id="666dd-147">Teljes körűen működőképes erőforrások</span><span class="sxs-lookup"><span data-stu-id="666dd-147">Resources that are fully functional</span></span>
  * [<span data-ttu-id="666dd-148">Archív</span><span class="sxs-lookup"><span data-stu-id="666dd-148">Archive</span></span>](archiveResource.md)
  * [<span data-ttu-id="666dd-149">Környezet</span><span class="sxs-lookup"><span data-stu-id="666dd-149">Environment</span></span>](environmentResource.md)
  * [<span data-ttu-id="666dd-150">File</span><span class="sxs-lookup"><span data-stu-id="666dd-150">File</span></span>](fileResource.md)
  * [<span data-ttu-id="666dd-151">Log</span><span class="sxs-lookup"><span data-stu-id="666dd-151">Log</span></span>](logResource.md)
  * <span data-ttu-id="666dd-152">ProcessSet</span><span class="sxs-lookup"><span data-stu-id="666dd-152">ProcessSet</span></span>
  * [<span data-ttu-id="666dd-153">Registry</span><span class="sxs-lookup"><span data-stu-id="666dd-153">Registry</span></span>](registryResource.md)
  * [<span data-ttu-id="666dd-154">Script</span><span class="sxs-lookup"><span data-stu-id="666dd-154">Script</span></span>](scriptResource.md)
  * <span data-ttu-id="666dd-155">WindowsPackageCab</span><span class="sxs-lookup"><span data-stu-id="666dd-155">WindowsPackageCab</span></span>
  * [<span data-ttu-id="666dd-156">WindowsProcess</span><span class="sxs-lookup"><span data-stu-id="666dd-156">WindowsProcess</span></span>](windowsProcessResource.md)
  * <span data-ttu-id="666dd-157">WaitForAll (lásd: [cross-csomópont függőségek megadását](crossNodeDependencies.md))</span><span class="sxs-lookup"><span data-stu-id="666dd-157">WaitForAll (see [Specifying cross-node dependencies](crossNodeDependencies.md))</span></span>
  * <span data-ttu-id="666dd-158">WaitForAny (lásd: [cross-csomópont függőségek megadását](crossNodeDependencies.md))</span><span class="sxs-lookup"><span data-stu-id="666dd-158">WaitForAny (see [Specifying cross-node dependencies](crossNodeDependencies.md))</span></span>
  * <span data-ttu-id="666dd-159">WaitForSome (lásd: [cross-csomópont függőségek megadását](crossNodeDependencies.md))</span><span class="sxs-lookup"><span data-stu-id="666dd-159">WaitForSome (see [Specifying cross-node dependencies](crossNodeDependencies.md))</span></span>

* <span data-ttu-id="666dd-160">Részlegesen működési erőforrásokhoz</span><span class="sxs-lookup"><span data-stu-id="666dd-160">Resources that are partially functional</span></span>
  * [<span data-ttu-id="666dd-161">Csoport</span><span class="sxs-lookup"><span data-stu-id="666dd-161">Group</span></span>](groupResource.md)
  * <span data-ttu-id="666dd-162">GroupSet</span><span class="sxs-lookup"><span data-stu-id="666dd-162">GroupSet</span></span>
  
  <span data-ttu-id="666dd-163">**Probléma:** felett erőforrást sikertelen, ha a példány neve kétszer (kétszer azonos konfigurációval fut)</span><span class="sxs-lookup"><span data-stu-id="666dd-163">**Issue:** Above resources fail if specific instance is called twice (running the same configuration twice)</span></span>
  
  * [<span data-ttu-id="666dd-164">Service</span><span class="sxs-lookup"><span data-stu-id="666dd-164">Service</span></span>](serviceResource.md)
  * <span data-ttu-id="666dd-165">ServiceSet</span><span class="sxs-lookup"><span data-stu-id="666dd-165">ServiceSet</span></span>
  
  <span data-ttu-id="666dd-166">**Probléma:** csak akkor működik, a (állapot): a szolgáltatás indítása/leállítása.</span><span class="sxs-lookup"><span data-stu-id="666dd-166">**Issue:** Only works for starting/stopping (status) service.</span></span> <span data-ttu-id="666dd-167">Nem sikerül, ha egy próbál módosítani más szolgáltatás tulajdonságai, például a startuptype, a hitelesítő adatokat, a leírás stb...</span><span class="sxs-lookup"><span data-stu-id="666dd-167">Fails, if one tries to change other service attributes like startuptype, credentials, description etc..</span></span> <span data-ttu-id="666dd-168">A hiba lépett fel hasonlít:</span><span class="sxs-lookup"><span data-stu-id="666dd-168">The error thrown is similar to:</span></span>
  
  <span data-ttu-id="666dd-169">*[Management.managementobject] típus nem található: Győződjön meg arról, hogy a típust tartalmazó szerelvény be töltve.*</span><span class="sxs-lookup"><span data-stu-id="666dd-169">*Cannot find type [management.managementobject]: verify that the assembly containing this type is loaded.*</span></span>
  
* <span data-ttu-id="666dd-170">Erőforrások, amelyek nem működik</span><span class="sxs-lookup"><span data-stu-id="666dd-170">Resources that are not functional</span></span>
  * [<span data-ttu-id="666dd-171">Felhasználó</span><span class="sxs-lookup"><span data-stu-id="666dd-171">User</span></span>](userResource.md)
  

## <a name="dsc-features-not-available-on-nano-server"></a><span data-ttu-id="666dd-172">A DSC-szolgáltatások Nano Server rendszeren nem érhető el</span><span class="sxs-lookup"><span data-stu-id="666dd-172">DSC features not available on Nano Server</span></span>

<span data-ttu-id="666dd-173">A következő DSC-szolgáltatások nem érhetők el jelenleg a Nano Server:</span><span class="sxs-lookup"><span data-stu-id="666dd-173">The following DSC features are not currently available on Nano Server:</span></span>

* <span data-ttu-id="666dd-174">MOF dokumentum titkosított egy visszafejtése</span><span class="sxs-lookup"><span data-stu-id="666dd-174">Decrypting MOF document with encrypted password(s)</span></span> 
* <span data-ttu-id="666dd-175">Lekérési kiszolgálójával--nem jelenleg állítható be a lekérési kiszolgálón Nano</span><span class="sxs-lookup"><span data-stu-id="666dd-175">Pull Server--you cannot currently set up a pull server on Nano Server</span></span>
* <span data-ttu-id="666dd-176">Mindent, ami nem funkció akkor működik a listájában</span><span class="sxs-lookup"><span data-stu-id="666dd-176">Anything that is not in the list of feature works</span></span>

## <a name="using-custom-dsc-resources-on-nano-server"></a><span data-ttu-id="666dd-177">Egyéni DSC-erőforrások Nano Server segítségével</span><span class="sxs-lookup"><span data-stu-id="666dd-177">Using custom DSC resources on Nano Server</span></span>
 
<span data-ttu-id="666dd-178">Windows API-k és a CLR-könyvtárak érhető el a Nano Server korlátozott készleteinek miatt a teljes CLR-verzió Windows működő DSC erőforrások feltétlenül működik a Nano Server.</span><span class="sxs-lookup"><span data-stu-id="666dd-178">Due to a limited sets of Windows APIs and CLR libraries available on Nano Server, DSC resources that work on the full CLR version of Windows do not necessarily work on Nano Server.</span></span> <span data-ttu-id="666dd-179">Fejezze be a végpontok közötti tesztelése előtt DSC egyéni erőforrások telepítése éles környezetben.</span><span class="sxs-lookup"><span data-stu-id="666dd-179">Complete end-to-end testing before deploying any DSC custom resources to a production environment.</span></span>

## <a name="see-also"></a><span data-ttu-id="666dd-180">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="666dd-180">See Also</span></span>
- [<span data-ttu-id="666dd-181">Ismerkedés a Nano Server</span><span class="sxs-lookup"><span data-stu-id="666dd-181">Getting Started with Nano Server</span></span>](https://technet.microsoft.com/library/mt126167.aspx)

