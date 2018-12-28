---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: A DSC használata a Nano Serveren
ms.openlocfilehash: fd81fe56d16100f45d9ee2dfd8fdc303c2a6c17a
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/14/2018
ms.locfileid: "53404237"
---
# <a name="using-dsc-on-nano-server"></a><span data-ttu-id="658ae-103">A DSC használata a Nano Serveren</span><span class="sxs-lookup"><span data-stu-id="658ae-103">Using DSC on Nano Server</span></span>

> <span data-ttu-id="658ae-104">Érvényes: Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="658ae-104">Applies To: Windows PowerShell 5.0</span></span>

<span data-ttu-id="658ae-105">**A Nano Serveren DSC** a választható csomag létezik a `NanoServer\Packages` mappájában, a Windows Server 2016 adathordozójáról.</span><span class="sxs-lookup"><span data-stu-id="658ae-105">**DSC on Nano Server** is an optional package in the `NanoServer\Packages` folder of the Windows Server 2016 media.</span></span> <span data-ttu-id="658ae-106">A csomag létrehozásakor egy virtuális Merevlemezt a Nano Server megadásával telepíthető **Microsoft-NanoServer-DSC-Package** értékeként a **csomagok** paraméterében a **New-NanoServerImage**  függvény.</span><span class="sxs-lookup"><span data-stu-id="658ae-106">The package can be installed when you create a VHD for a Nano Server by specifying **Microsoft-NanoServer-DSC-Package** as the value of the **Packages** parameter of the **New-NanoServerImage** function.</span></span> <span data-ttu-id="658ae-107">Ha például egy virtuális Merevlemezt a virtuális gép létrehozásakor, a parancs lenne a következőhöz hasonló:</span><span class="sxs-lookup"><span data-stu-id="658ae-107">For example, if you are creating a VHD for a virtual machine, the command would look like the following:</span></span>

```powershell
New-NanoServerImage -Edition Standard -DeploymentType Guest -MediaPath f:\ -BasePath .\Base -TargetPath .\Nano1\Nano.vhd -ComputerName Nano1 -Packages Microsoft-NanoServer-DSC-Package
```

<span data-ttu-id="658ae-108">További információ a telepítése és használata a Nano Serveren, valamint a PowerShell-táveléréssel a Nano Server kezelése: [Ismerkedés a Nano Serverrel](/windows-server/get-started/getting-started-with-nano-server).</span><span class="sxs-lookup"><span data-stu-id="658ae-108">For information about installing and using Nano Server, as well as how to manage Nano Server with PowerShell Remoting, see [Getting Started with Nano Server](/windows-server/get-started/getting-started-with-nano-server).</span></span>

## <a name="dsc-features-available-on-nano-server"></a><span data-ttu-id="658ae-109">DSC-funkciók érhető el a Nano Serveren</span><span class="sxs-lookup"><span data-stu-id="658ae-109">DSC features available on Nano Server</span></span>

<span data-ttu-id="658ae-110">Mivel a Nano Server támogatja a Windows Server teljes verzióját képest API-k csak korlátozott számú, DSC, a Nano Serveren nem rendelkezik teljes funkciói egyenértékűek teljes Termékváltozatai jelenleg futó DSC.</span><span class="sxs-lookup"><span data-stu-id="658ae-110">Because Nano Server supports only a limited set of APIs compared to a full version of Windows Server, DSC on Nano Server does not have full functional parity with DSC running on full SKUs for the time being.</span></span> <span data-ttu-id="658ae-111">A Nano Serveren a DSC szolgáltatás aktív fejlesztés alatt áll, és még nem teljes funkció.</span><span class="sxs-lookup"><span data-stu-id="658ae-111">DSC on Nano Server is in active development and is not yet feature complete.</span></span>

<span data-ttu-id="658ae-112">A következő DSC-funkciók érhetők el jelenleg a Nano Serveren:</span><span class="sxs-lookup"><span data-stu-id="658ae-112">The following DSC features are currently available on Nano Server:</span></span>

<span data-ttu-id="658ae-113">Leküldéses és lekéréses módok</span><span class="sxs-lookup"><span data-stu-id="658ae-113">Both push and pull modes</span></span>

- <span data-ttu-id="658ae-114">Minden DSC-parancsmagok a teljes verzióját a Windows Server, beleértve a következőket:</span><span class="sxs-lookup"><span data-stu-id="658ae-114">All DSC cmdlets that exist on a full version of Windows Server, including the following:</span></span>
- [<span data-ttu-id="658ae-115">Get-DscLocalConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="658ae-115">Get-DscLocalConfigurationManager</span></span>](/powershell/module/PSDesiredStateConfiguration/Get-DscLocalConfigurationManager)
- [<span data-ttu-id="658ae-116">Set-DscLocalConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="658ae-116">Set-DscLocalConfigurationManager</span></span>](/powershell/module/PSDesiredStateConfiguration/Set-DscLocalConfigurationManager)
- [<span data-ttu-id="658ae-117">Enable-DscDebug</span><span class="sxs-lookup"><span data-stu-id="658ae-117">Enable-DscDebug</span></span>](/powershell/module/PSDesiredStateConfiguration/Enable-DscDebug)
- [<span data-ttu-id="658ae-118">Disable-DscDebug</span><span class="sxs-lookup"><span data-stu-id="658ae-118">Disable-DscDebug</span></span>](/powershell/module/PSDesiredStateConfiguration/Disable-DscDebug)
- [<span data-ttu-id="658ae-119">Start-DscConfiguration</span><span class="sxs-lookup"><span data-stu-id="658ae-119">Start-DscConfiguration</span></span>](/powershell/module/psdesiredstateconfiguration/start-dscconfiguration)
- [<span data-ttu-id="658ae-120">Stop-DscConfiguration</span><span class="sxs-lookup"><span data-stu-id="658ae-120">Stop-DscConfiguration</span></span>](/powershell/module/PSDesiredStateConfiguration/Stop-DscConfiguration)
- [<span data-ttu-id="658ae-121">Get-DscConfiguration</span><span class="sxs-lookup"><span data-stu-id="658ae-121">Get-DscConfiguration</span></span>](/powershell/module/PSDesiredStateConfiguration/Get-DscConfiguration)
- [<span data-ttu-id="658ae-122">Test-DscConfiguration</span><span class="sxs-lookup"><span data-stu-id="658ae-122">Test-DscConfiguration</span></span>](/powershell/module/psdesiredstateconfiguration/Test-DSCConfiguration)
- [<span data-ttu-id="658ae-123">Publish-DscConfiguraiton</span><span class="sxs-lookup"><span data-stu-id="658ae-123">Publish-DscConfiguraiton</span></span>](/powershell/module/PSDesiredStateConfiguration/Publish-DscConfiguration)
- [<span data-ttu-id="658ae-124">Update-DscConfiguration</span><span class="sxs-lookup"><span data-stu-id="658ae-124">Update-DscConfiguration</span></span>](/powershell/module/PSDesiredStateConfiguration/Update-DscConfiguration)
- [<span data-ttu-id="658ae-125">Restore-DscConfiguration</span><span class="sxs-lookup"><span data-stu-id="658ae-125">Restore-DscConfiguration</span></span>](/powershell/module/PSDesiredStateConfiguration/Restore-DscConfiguration)
- [<span data-ttu-id="658ae-126">Remove-DscConfigurationDocument</span><span class="sxs-lookup"><span data-stu-id="658ae-126">Remove-DscConfigurationDocument</span></span>](/powershell/module/PSDesiredStateConfiguration/Remove-DscConfigurationDocument)
- [<span data-ttu-id="658ae-127">Get-DscConfigurationStatus</span><span class="sxs-lookup"><span data-stu-id="658ae-127">Get-DscConfigurationStatus</span></span>](/powershell/module/PSDesiredStateConfiguration/Get-DscConfigurationStatus)
- [<span data-ttu-id="658ae-128">Invoke-DscResource</span><span class="sxs-lookup"><span data-stu-id="658ae-128">Invoke-DscResource</span></span>](/powershell/module/PSDesiredStateConfiguration/Invoke-DscResource)
- [<span data-ttu-id="658ae-129">Find-DscResource</span><span class="sxs-lookup"><span data-stu-id="658ae-129">Find-DscResource</span></span>](https://technet.microsoft.com/en-us/library/mt517874.aspx)
- [<span data-ttu-id="658ae-130">Get-DscResource</span><span class="sxs-lookup"><span data-stu-id="658ae-130">Get-DscResource</span></span>](/powershell/module/PSDesiredStateConfiguration/Get-DscResource)
- [<span data-ttu-id="658ae-131">Új DscChecksum</span><span class="sxs-lookup"><span data-stu-id="658ae-131">New-DscChecksum</span></span>](/powershell/module/PSDesiredStateConfiguration/New-DSCCheckSum)

- <span data-ttu-id="658ae-132">Konfiguráció fordítása (lásd: [DSC-konfigurációk](../configurations/configurations.md))</span><span class="sxs-lookup"><span data-stu-id="658ae-132">Compiling configurations (see [DSC configurations](../configurations/configurations.md))</span></span>

  <span data-ttu-id="658ae-133">**A probléma leírása:** Jelszó titkosítása (lásd: [a MOF-fájl biztonságossá tétele](../pull-server/secureMOF.md)) konfigurálása során összeállítása nem működik.</span><span class="sxs-lookup"><span data-stu-id="658ae-133">**Issue:** Password encryption (see [Securing the MOF File](../pull-server/secureMOF.md)) during configuration compilation doesn't work.</span></span>

- <span data-ttu-id="658ae-134">Metaconfigurations összeállítása (lásd: [a Local Configuration Manager](../managing-nodes/metaConfig.md))</span><span class="sxs-lookup"><span data-stu-id="658ae-134">Compiling metaconfigurations (see [Configuring the Local Configuration Manager](../managing-nodes/metaConfig.md))</span></span>

- <span data-ttu-id="658ae-135">Egy erőforrás felhasználó környezetében fut (lásd: [DSC futtatása felhasználói hitelesítő adatokkal (RunAs)](../configurations/runAsUser.md))</span><span class="sxs-lookup"><span data-stu-id="658ae-135">Running a resource under user context (see [Running DSC with user credentials (RunAs)](../configurations/runAsUser.md))</span></span>

- <span data-ttu-id="658ae-136">Osztályalapú erőforrások (lásd: [PowerShell-osztályokkal egyéni DSC-erőforrás írása](../resources/authoringResourceClass.md))</span><span class="sxs-lookup"><span data-stu-id="658ae-136">Class-based resources (see [Writing a custom DSC resource with PowerShell classes](../resources/authoringResourceClass.md))</span></span>

- <span data-ttu-id="658ae-137">DSC-erőforrások hibakeresés (lásd: [hibakeresés DSC-erőforrások](../troubleshooting/debugResource.md))</span><span class="sxs-lookup"><span data-stu-id="658ae-137">Debugging of DSC resources (see [Debugging DSC resources](../troubleshooting/debugResource.md))</span></span>

  <span data-ttu-id="658ae-138">**A probléma leírása:** Nem működik, ha egy erőforrás PsDscRunAsCredential használ (lásd: [DSC futtatása felhasználói hitelesítő adatokkal](../configurations/runAsUser.md))</span><span class="sxs-lookup"><span data-stu-id="658ae-138">**Issue:** Doesn't work if a resource is using PsDscRunAsCredential (see [Running DSC with user credentials](../configurations/runAsUser.md))</span></span>

- [<span data-ttu-id="658ae-139">Csomópontok közötti függőségek megadása</span><span class="sxs-lookup"><span data-stu-id="658ae-139">Specifying cross-node dependencies</span></span>](../configurations/crossNodeDependencies.md)

- [<span data-ttu-id="658ae-140">Erőforrás-verziókezelés</span><span class="sxs-lookup"><span data-stu-id="658ae-140">Resource versioning</span></span>](../configurations/sxsResource.md)

- <span data-ttu-id="658ae-141">Lekérési ügyfél (konfigurációk és erőforrások) (lásd: [konfigurációs nevek lekérési ügyfél beállítása](../pull-server/pullClientConfigNames.md))</span><span class="sxs-lookup"><span data-stu-id="658ae-141">Pull client (configurations & resources) (see [Setting up a pull client using configuration names](../pull-server/pullClientConfigNames.md))</span></span>

- [<span data-ttu-id="658ae-142">Részleges konfigurációk (lekéréses & leküldéses)</span><span class="sxs-lookup"><span data-stu-id="658ae-142">Partial configurations (pull & push)</span></span>](../pull-server/partialConfigs.md)

- [<span data-ttu-id="658ae-143">A jelentéskészítés lekéréses kiszolgálón</span><span class="sxs-lookup"><span data-stu-id="658ae-143">Reporting to pull server</span></span>](../pull-server/reportServer.md)

- <span data-ttu-id="658ae-144">MOF-titkosítás</span><span class="sxs-lookup"><span data-stu-id="658ae-144">MOF encryption</span></span>

- <span data-ttu-id="658ae-145">Eseménynaplózás</span><span class="sxs-lookup"><span data-stu-id="658ae-145">Event logging</span></span>

- <span data-ttu-id="658ae-146">Az Azure Automation DSC jelentési</span><span class="sxs-lookup"><span data-stu-id="658ae-146">Azure Automation DSC reporting</span></span>

- <span data-ttu-id="658ae-147">Erőforrások, amelyek teljes körűen használható</span><span class="sxs-lookup"><span data-stu-id="658ae-147">Resources that are fully functional</span></span>

- <span data-ttu-id="658ae-148">**Archívum**</span><span class="sxs-lookup"><span data-stu-id="658ae-148">**Archive**</span></span>
- <span data-ttu-id="658ae-149">**Környezet**</span><span class="sxs-lookup"><span data-stu-id="658ae-149">**Environment**</span></span>
- <span data-ttu-id="658ae-150">**Fájl**</span><span class="sxs-lookup"><span data-stu-id="658ae-150">**File**</span></span>
- <span data-ttu-id="658ae-151">**Log**</span><span class="sxs-lookup"><span data-stu-id="658ae-151">**Log**</span></span>
- <span data-ttu-id="658ae-152">**ProcessSet**</span><span class="sxs-lookup"><span data-stu-id="658ae-152">**ProcessSet**</span></span>
- <span data-ttu-id="658ae-153">**Registry**</span><span class="sxs-lookup"><span data-stu-id="658ae-153">**Registry**</span></span>
- <span data-ttu-id="658ae-154">**Parancsfájl**</span><span class="sxs-lookup"><span data-stu-id="658ae-154">**Script**</span></span>
- <span data-ttu-id="658ae-155">**WindowsPackageCab**</span><span class="sxs-lookup"><span data-stu-id="658ae-155">**WindowsPackageCab**</span></span>
- <span data-ttu-id="658ae-156">**WindowsProcess**</span><span class="sxs-lookup"><span data-stu-id="658ae-156">**WindowsProcess**</span></span>
- <span data-ttu-id="658ae-157">**WaitForAll** (lásd: [csomópontok közötti függőségek megadása](../configurations/crossNodeDependencies.md))</span><span class="sxs-lookup"><span data-stu-id="658ae-157">**WaitForAll** (see [Specifying cross-node dependencies](../configurations/crossNodeDependencies.md))</span></span>
- <span data-ttu-id="658ae-158">**WaitForAny** (lásd: [csomópontok közötti függőségek megadása](../configurations/crossNodeDependencies.md))</span><span class="sxs-lookup"><span data-stu-id="658ae-158">**WaitForAny** (see [Specifying cross-node dependencies](../configurations/crossNodeDependencies.md))</span></span>
- <span data-ttu-id="658ae-159">**WaitForSome** (lásd: [csomópontok közötti függőségek megadása](../configurations/crossNodeDependencies.md))</span><span class="sxs-lookup"><span data-stu-id="658ae-159">**WaitForSome** (see [Specifying cross-node dependencies](../configurations/crossNodeDependencies.md))</span></span>

- <span data-ttu-id="658ae-160">Erőforrások, amelyek részben működési</span><span class="sxs-lookup"><span data-stu-id="658ae-160">Resources that are partially functional</span></span>
- <span data-ttu-id="658ae-161">**Csoport**</span><span class="sxs-lookup"><span data-stu-id="658ae-161">**Group**</span></span>
- <span data-ttu-id="658ae-162">**GroupSet**</span><span class="sxs-lookup"><span data-stu-id="658ae-162">**GroupSet**</span></span>

  <span data-ttu-id="658ae-163">**A probléma leírása:** Erőforrások felett sikertelen, ha az adott példány volat dvakrát (ugyanaz a konfiguráció kétszer fut)</span><span class="sxs-lookup"><span data-stu-id="658ae-163">**Issue:** Above resources fail if specific instance is called twice (running the same configuration twice)</span></span>

- <span data-ttu-id="658ae-164">**Service**</span><span class="sxs-lookup"><span data-stu-id="658ae-164">**Service**</span></span>
- <span data-ttu-id="658ae-165">**ServiceSet**</span><span class="sxs-lookup"><span data-stu-id="658ae-165">**ServiceSet**</span></span>

  <span data-ttu-id="658ae-166">**A probléma leírása:** Csak akkor működik, a (állapot) szolgáltatás indítása/leállítása.</span><span class="sxs-lookup"><span data-stu-id="658ae-166">**Issue:** Only works for starting/stopping (status) service.</span></span> <span data-ttu-id="658ae-167">Nem sikerül, ha az egyik megpróbálja módosítani a más szolgáltatás-attribútumok indítási típusa, a hitelesítő adatokat, a leírás stb...</span><span class="sxs-lookup"><span data-stu-id="658ae-167">Fails, if one tries to change other service attributes like startuptype, credentials, description etc..</span></span> <span data-ttu-id="658ae-168">A hiba lépett fel hasonlít:</span><span class="sxs-lookup"><span data-stu-id="658ae-168">The error thrown is similar to:</span></span>

  <span data-ttu-id="658ae-169">*[Management.managementobject] típus nem található: Győződjön meg arról, hogy ez a típus tartalmazó szerelvény be töltve.*</span><span class="sxs-lookup"><span data-stu-id="658ae-169">*Cannot find type [management.managementobject]: verify that the assembly containing this type is loaded.*</span></span>

- <span data-ttu-id="658ae-170">Erőforrások, amelyek nem működik</span><span class="sxs-lookup"><span data-stu-id="658ae-170">Resources that are not functional</span></span>
- <span data-ttu-id="658ae-171">**Felhasználó**</span><span class="sxs-lookup"><span data-stu-id="658ae-171">**User**</span></span>

## <a name="dsc-features-not-available-on-nano-server"></a><span data-ttu-id="658ae-172">DSC-funkciók nem érhető el a Nano Serveren</span><span class="sxs-lookup"><span data-stu-id="658ae-172">DSC features not available on Nano Server</span></span>

<span data-ttu-id="658ae-173">A következő DSC-funkciók nem érhetők el jelenleg a Nano Serveren:</span><span class="sxs-lookup"><span data-stu-id="658ae-173">The following DSC features are not currently available on Nano Server:</span></span>

- <span data-ttu-id="658ae-174">Egy titkosított MOF dokumentum visszafejtése</span><span class="sxs-lookup"><span data-stu-id="658ae-174">Decrypting MOF document with encrypted password(s)</span></span>
- <span data-ttu-id="658ae-175">Lekérési kiszolgáló –, jelenleg nem állíthat egy lekéréses kiszolgálót a Nano Serveren</span><span class="sxs-lookup"><span data-stu-id="658ae-175">Pull Server--you cannot currently set up a pull server on Nano Server</span></span>
- <span data-ttu-id="658ae-176">Bármi, amely nem szerepel a listában, a szolgáltatás működése</span><span class="sxs-lookup"><span data-stu-id="658ae-176">Anything that is not in the list of feature works</span></span>

## <a name="using-custom-dsc-resources-on-nano-server"></a><span data-ttu-id="658ae-177">Egyéni DSC-erőforrások használata a Nano Serveren</span><span class="sxs-lookup"><span data-stu-id="658ae-177">Using custom DSC resources on Nano Server</span></span>

<span data-ttu-id="658ae-178">Korlátozott csoportok Windows API-k és a CLR-beli kódtárak érhető el a Nano Serveren, mert DSC-erőforrások, amelyek működnek a Windows teljes CLR verziója nem feltétlenül működik a Nano Serveren.</span><span class="sxs-lookup"><span data-stu-id="658ae-178">Due to a limited sets of Windows APIs and CLR libraries available on Nano Server, DSC resources that work on the full CLR version of Windows do not necessarily work on Nano Server.</span></span>
<span data-ttu-id="658ae-179">Fejezze be a teljes körű tesztelés éles környezetben olyan egyéni DSC-erőforrások üzembe helyezése előtt.</span><span class="sxs-lookup"><span data-stu-id="658ae-179">Complete end-to-end testing before deploying any DSC custom resources to a production environment.</span></span>

## <a name="see-also"></a><span data-ttu-id="658ae-180">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="658ae-180">See Also</span></span>

- [<span data-ttu-id="658ae-181">Ismerkedés a Nano Serverrel</span><span class="sxs-lookup"><span data-stu-id="658ae-181">Getting Started with Nano Server</span></span>](/windows-server/get-started/getting-started-with-nano-server)
