---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: 883f80a5c8c99f2ab9886558a7aebfe1204f3be6
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62085160"
---
# <a name="desired-state-configuration-dsc-known-issues-and-limitations"></a><span data-ttu-id="915b2-102">Desired State Configuration (DSC) ismert problémák és korlátozások</span><span class="sxs-lookup"><span data-stu-id="915b2-102">Desired State Configuration (DSC) Known Issues and Limitations</span></span>

## <a name="breaking-change-certificates-used-to-encryptdecrypt-passwords-in-dsc-configurations-may-not-work-after-installing-wmf-50-rtm"></a><span data-ttu-id="915b2-103">Kompatibilitástörő változás: A DSC-konfigurációk jelszavak titkosítási/visszafejtési tanúsítványokat nem működnek a WMF 5.0 RTM-re telepítése után</span><span class="sxs-lookup"><span data-stu-id="915b2-103">Breaking Change: Certificates used to encrypt/decrypt passwords in DSC configurations may not work after installing WMF 5.0 RTM</span></span>

<span data-ttu-id="915b2-104">A WMF 4.0-s és WMF 5.0-s előzetes kiadások DSC nem teszik lehetővé a jelszavak hosszát, a konfiguráció a több mint 121 karakter.</span><span class="sxs-lookup"><span data-stu-id="915b2-104">In WMF 4.0 and WMF 5.0 Preview releases, DSC would not allow passwords in the configuration to be of length more than 121 characters.</span></span> <span data-ttu-id="915b2-105">DSC rövid jelszavak használatát, akkor is, ha a hosszú és erős jelszót volt szükség volt kényszerítése.</span><span class="sxs-lookup"><span data-stu-id="915b2-105">DSC was forcing to use short passwords even if lengthy and strong password was desired.</span></span> <span data-ttu-id="915b2-106">Ez használhatatlanná tévő változás lehetővé teszi, hogy a jelszavakat a DSC-konfiguráció tetszőleges hosszúságú lehet.</span><span class="sxs-lookup"><span data-stu-id="915b2-106">This breaking change allows passwords to be of arbitrary length in the DSC configuration.</span></span>

<span data-ttu-id="915b2-107">**Megoldás:** Hozza létre újra a tanúsítványt, az adattitkosítás vagy a fő titkosítási kulcs használati és dokumentum titkosítási kibővített kulcshasználat (1.3.6.1.4.1.311.80.1).</span><span class="sxs-lookup"><span data-stu-id="915b2-107">**Resolution:** Re-create the certificate with Data Encipherment or Key Encipherment Key usage, and Document Encryption Enhanced Key usage (1.3.6.1.4.1.311.80.1).</span></span> <span data-ttu-id="915b2-108">TechNet-cikk <https://technet.microsoft.com/library/dn807171.aspx> tartalmaz további információkat.</span><span class="sxs-lookup"><span data-stu-id="915b2-108">Technet article <https://technet.microsoft.com/library/dn807171.aspx> has more information.</span></span>

## <a name="dsc-cmdlets-may-fail-after-installing-wmf-50-rtm"></a><span data-ttu-id="915b2-109">A WMF 5.0 RTM-re telepítése után sikertelen lehet a DSC-parancsmagok</span><span class="sxs-lookup"><span data-stu-id="915b2-109">DSC cmdlets may fail after installing WMF 5.0 RTM</span></span>

<span data-ttu-id="915b2-110">Start-DscConfiguration és egyéb DSC-parancsmagok után telepíti a WMF 5.0 RTM-re a következő hibaüzenettel meghiúsulhat:</span><span class="sxs-lookup"><span data-stu-id="915b2-110">Start-DscConfiguration and other DSC cmdlets may fail after installing WMF 5.0 RTM with the following error:</span></span>
```powershell
    LCM failed to retrieve the property PendingJobStep from the object of class dscInternalCache .
    + CategoryInfo : ObjectNotFound: (root/Microsoft/...gurationManager:String) [], CimException
    + FullyQualifiedErrorId : MI RESULT 6
    + PSComputerName : localhost
```

<span data-ttu-id="915b2-111">**Megoldás:** DSCEngineCache.mof törölje a következő parancs futtatásával egy rendszergazda jogú PowerShell-munkamenetben (Futtatás rendszergazdaként):</span><span class="sxs-lookup"><span data-stu-id="915b2-111">**Resolution:** Delete DSCEngineCache.mof by running the following command in an elevated PowerShell session (Run as Administrator):</span></span>

```powershell
Remove-Item -Path $env:SystemRoot\system32\Configuration\DSCEngineCache.mof
```

## <a name="dsc-cmdlets-may-not-work-if-wmf-50-rtm-is-installed-on-top-of-wmf-50-production-preview"></a><span data-ttu-id="915b2-112">DSC-parancsmagok előfordulhat, hogy nem működik, ha a WMF 5.0 RTM-re épülő WMF 5.0 éles előzetes verzió van telepítve</span><span class="sxs-lookup"><span data-stu-id="915b2-112">DSC cmdlets may not work if WMF 5.0 RTM is installed on top of WMF 5.0 Production Preview</span></span>

<span data-ttu-id="915b2-113">**Megoldás:** Futtassa a következő parancsot egy rendszergazda jogú PowerShell-munkamenetben (Futtatás rendszergazdaként):</span><span class="sxs-lookup"><span data-stu-id="915b2-113">**Resolution:** Run the following command in an elevated PowerShell session (run as administrator):</span></span>
```powershell
    mofcomp $env:windir\system32\wbem\DscCoreConfProv.mof
```

## <a name="lcm-can-go-into-an-unstable-state-while-using-get-dscconfiguration-in-debugmode"></a><span data-ttu-id="915b2-114">Az LCM lépjen nem stabil állapotba kerülnek DebugMode Get-DscConfiguration használatával</span><span class="sxs-lookup"><span data-stu-id="915b2-114">LCM can go into an unstable state while using Get-DscConfiguration in DebugMode</span></span>

<span data-ttu-id="915b2-115">Ha LCM DebugMode, nyomja le a CTRL + C billentyűkombinációval állítsa le a Get-DscConfiguration feldolgozása okozhat a go LCM nem stabil állapotba kerülnek az ilyen a DSC-parancsmagok többsége nem fog működni.</span><span class="sxs-lookup"><span data-stu-id="915b2-115">If LCM is in DebugMode, pressing CTRL+C to stop the processing of Get-DscConfiguration can cause LCM to go into an unstable state such that majority of DSC cmdlets won’t work.</span></span>

<span data-ttu-id="915b2-116">**Megoldás:** Ne nyomja le a CTRL + C Get-DscConfiguration parancsmag hibakeresése során.</span><span class="sxs-lookup"><span data-stu-id="915b2-116">**Resolution:** Don’t press CTRL+C while debugging Get-DscConfiguration cmdlet.</span></span>

## <a name="stop-dscconfiguration-may-not-respond-in-debugmode"></a><span data-ttu-id="915b2-117">STOP-DscConfiguration nem válaszol a DebugMode</span><span class="sxs-lookup"><span data-stu-id="915b2-117">Stop-DscConfiguration may not respond in DebugMode</span></span>

<span data-ttu-id="915b2-118">Ha LCM DebugMode, Stop-DscConfiguration nem válaszol, Get-DscConfiguration által indított művelet megszakítására tett kísérlet során</span><span class="sxs-lookup"><span data-stu-id="915b2-118">If LCM is in DebugMode, Stop-DscConfiguration may not respond while trying to stop an operation started by Get-DscConfiguration</span></span>

<span data-ttu-id="915b2-119">**Megoldás:** A hibakeresés, a szakaszban ismertetett módon, a Get-DscConfiguration által indított művelet befejezéséhez "[hibakeresés DSC-erőforrások](https://msdn.microsoft.com/powershell/dsc/debugresource)".</span><span class="sxs-lookup"><span data-stu-id="915b2-119">**Resolution:** Finish the debugging of the operation started by Get-DscConfiguration as outlined in section ‘[Debugging DSC resources](https://msdn.microsoft.com/powershell/dsc/debugresource)’.</span></span>

## <a name="no-verbose-error-messages-are-shown-in-debugmode"></a><span data-ttu-id="915b2-120">Részletes hibaüzenetek nem jelennek meg DebugMode</span><span class="sxs-lookup"><span data-stu-id="915b2-120">No Verbose Error Messages are shown in DebugMode</span></span>

<span data-ttu-id="915b2-121">Ha LCM DebugMode, nem a részletes hibaüzenet jelenik meg a DSC-erőforrásokat.</span><span class="sxs-lookup"><span data-stu-id="915b2-121">If LCM is in DebugMode, no verbose error messages are displayed from DSC Resources.</span></span>

<span data-ttu-id="915b2-122">**Megoldás:** Tiltsa le *DebugMode* erőforrásból részletes üzenetek megtekintéséhez</span><span class="sxs-lookup"><span data-stu-id="915b2-122">**Resolution:** Disable *DebugMode* to see verbose messages from the resource</span></span>

## <a name="invoke-dscresource-operations-cannot-be-retrieved-by-get-dscconfigurationstatus-cmdlet"></a><span data-ttu-id="915b2-123">Invoke-DscResource műveletek nem lehet beolvasni a Get-DscConfigurationStatus parancsmag</span><span class="sxs-lookup"><span data-stu-id="915b2-123">Invoke-DscResource operations cannot be retrieved by Get-DscConfigurationStatus cmdlet</span></span>

<span data-ttu-id="915b2-124">Invoke-DscResource parancsmag használatával bármely erőforrás metódusokat hívhat meg közvetlenül, miután a rekordokat az ilyen művelet nem lehet beolvasni Get-DscConfigurationStatus keresztül egy későbbi időpontban.</span><span class="sxs-lookup"><span data-stu-id="915b2-124">After using Invoke-DscResource cmdlet to directly invoke any resource’s methods, the records of such operation cannot be retrieved through Get-DscConfigurationStatus at a later time.</span></span>

<span data-ttu-id="915b2-125">**Megoldás:** Nincs.</span><span class="sxs-lookup"><span data-stu-id="915b2-125">**Resolution:** None.</span></span>

## <a name="get-dscconfigurationstatus-returns-pull-cycle-operations-as-type-consistency"></a><span data-ttu-id="915b2-126">Get-DscConfigurationStatus értéket ad vissza lekéréses ciklus műveletek típusként *konzisztencia*</span><span class="sxs-lookup"><span data-stu-id="915b2-126">Get-DscConfigurationStatus returns pull cycle operations as type *Consistency*</span></span>

<span data-ttu-id="915b2-127">Ha egy csomópont értéke LEKÉRÉSES frissítési mód, minden egyes lekéréses műveletet hajtja végre, a Get-DscConfigurationStatus parancsmag jelentések, a művelet típusa *konzisztencia* helyett *kezdeti*</span><span class="sxs-lookup"><span data-stu-id="915b2-127">When a node is set to PULL refresh mode, for each pull operation performed, Get-DscConfigurationStatus cmdlet reports the operation type as *Consistency* instead of *Initial*</span></span>

<span data-ttu-id="915b2-128">**Megoldás:** Nincs.</span><span class="sxs-lookup"><span data-stu-id="915b2-128">**Resolution:** None.</span></span>

## <a name="invoke-dscresource-cmdlet-does-not-return-message-in-the-order-they-were-produced"></a><span data-ttu-id="915b2-129">Invoke-DscResource parancsmag nem ad vissza üzenet állították sorrendben</span><span class="sxs-lookup"><span data-stu-id="915b2-129">Invoke-DscResource cmdlet does not return message in the order they were produced</span></span>

<span data-ttu-id="915b2-130">Az Invoke-DscResource a parancsmag nem ad részletes, figyelmeztetés, és hibaüzenetek LCM vagy a DSC-erőforrás állították a sorrendben.</span><span class="sxs-lookup"><span data-stu-id="915b2-130">The Invoke-DscResource cmdlet does not return verbose, warning, and error messages in the order they were produced by LCM or the DSC resource.</span></span>

<span data-ttu-id="915b2-131">**Megoldás:** Nincs.</span><span class="sxs-lookup"><span data-stu-id="915b2-131">**Resolution:** None.</span></span>

## <a name="dsc-resources-cannot-be-debugged-easily-when-used-with-invoke-dscresource"></a><span data-ttu-id="915b2-132">DSC-erőforrások hibakeresése nem végezhető el egyszerűen Invoke-DscResource együtt használva</span><span class="sxs-lookup"><span data-stu-id="915b2-132">DSC Resources cannot be debugged easily when used with Invoke-DscResource</span></span>

<span data-ttu-id="915b2-133">Az LCM futtatásakor hibakeresési módban (lásd: [hibakeresés DSC-erőforrások](https://msdn.microsoft.com/powershell/dsc/debugresource) további részletekért), Invoke-DscResource parancsmag nem ad futási térben csatlakozni hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="915b2-133">When LCM is running in debug mode (see [Debugging DSC resources](https://msdn.microsoft.com/powershell/dsc/debugresource) for more details), Invoke-DscResource cmdlet does not give information about runspace to connect to for debugging.</span></span>
<span data-ttu-id="915b2-134">**Megoldás:** Fedezze fel, és csatolja a futási térben parancsmagokkal **Get-PSHostProcessInfo**, **Enter-PSHostProcess** , **Get-futási térben** és **hibakeresési futási térben** hibakeresése a DSC-erőforrás.</span><span class="sxs-lookup"><span data-stu-id="915b2-134">**Resolution:** Discover and attach to the runspace using cmdlets **Get-PSHostProcessInfo**, **Enter-PSHostProcess** , **Get-Runspace** and **Debug-Runspace** to debug the DSC resource.</span></span>

```powershell
# Find all the processes hosting PowerShell
Get-PSHostProcessInfo

ProcessName ProcessId AppDomainName
----------- --------- -------------
powershell 3932 DefaultAppDomain
powershell_ise 2304 DefaultAppDomain
WmiPrvSE 3396 DscPsPluginWkr_AppDomain

# Enter the process that is hosting DSC engine (WMI process with DscPsPluginWkr_Appdomain)
Enter-PSHostProcess -Id 3396 -AppDomainName DscPsPluginWkr_AppDomain

# Find all the available rusnspaces in that process
Get-Runspace

Id Name ComputerName Type State Availability
-- ---- ------------ ---- ----- ------------
2 Runspace2 localhost Local Opened InBreakpoint
5 RemoteHost localhost Local Opened Busy

# Debug the runspace that is in **InBreakpoint** availability state
Debug-Runspace -Id 2
```

## <a name="various-partial-configuration-documents-for-same-node-cannot-have-identical-resource-names"></a><span data-ttu-id="915b2-135">Ugyanazon a csomóponton különböző részleges konfigurációs dokumentumok azonos erőforrás neve nem lehet.</span><span class="sxs-lookup"><span data-stu-id="915b2-135">Various Partial Configuration documents for same node cannot have identical resource names</span></span>

<span data-ttu-id="915b2-136">Azonos nevek erőforrások OK, amely egyetlen csomópont időszakaik legyenek több részleges konfigurációk, futásidejű hiba.</span><span class="sxs-lookup"><span data-stu-id="915b2-136">For several partial configurations that are deployed onto a single node, identical names of resources cause run time error.</span></span>

<span data-ttu-id="915b2-137">**Megoldás:** Akkor is ugyanazokat az erőforrásokat a különböző neveket használ a különböző részleges konfigurációk.</span><span class="sxs-lookup"><span data-stu-id="915b2-137">**Resolution:** Use different names for even same resources in different partial configurations.</span></span>

## <a name="start-dscconfiguration-useexisting-does-not-work-with--credential"></a><span data-ttu-id="915b2-138">Start-DscConfiguration – UseExisting nem működik – a hitelesítő adatok</span><span class="sxs-lookup"><span data-stu-id="915b2-138">Start-DscConfiguration –UseExisting does not work with -Credential</span></span>

<span data-ttu-id="915b2-139">Start-DscConfiguration – UseExisting paraméterrel, használatakor a – Credential paraméter figyelmen kívül hagyja.</span><span class="sxs-lookup"><span data-stu-id="915b2-139">When using Start-DscConfiguration with –UseExisting parameter, the –Credential parameter is ignored.</span></span> <span data-ttu-id="915b2-140">DSC használ alapértelmezett folyamatidentitás folytatja a műveletet.</span><span class="sxs-lookup"><span data-stu-id="915b2-140">DSC uses default process identity to proceed the operation.</span></span> <span data-ttu-id="915b2-141">Ez hibát okoz, ha más hitelesítő adatokat távoli csomóponton folytatja van szükség.</span><span class="sxs-lookup"><span data-stu-id="915b2-141">This causes error when a different credential is needed to proceed on remote node.</span></span>

<span data-ttu-id="915b2-142">**Megoldás:** CIM-munkamenet távoli DSC műveletek:</span><span class="sxs-lookup"><span data-stu-id="915b2-142">**Resolution:** Use CIM session for remote DSC operations:</span></span>
```powershell
$session = New-CimSession -ComputerName $node -Credential $credential
Start-DscConfiguration -UseExisting -CimSession $session
```

## <a name="ipv6-addresses-as-node-names-in-dsc-configurations"></a><span data-ttu-id="915b2-143">A DSC-konfigurációkat csomópont nevét, az IPv6-címek</span><span class="sxs-lookup"><span data-stu-id="915b2-143">IPv6 Addresses as Node Names in DSC configurations</span></span>

<span data-ttu-id="915b2-144">DSC-konfigurációs szkripteket a csomópont nevét, az IPv6-címek nem támogatottak ebben a kiadásban.</span><span class="sxs-lookup"><span data-stu-id="915b2-144">IPv6 addresses as node names in DSC configuration scripts are not supported in this release.</span></span>

<span data-ttu-id="915b2-145">**Megoldás:** Nincs.</span><span class="sxs-lookup"><span data-stu-id="915b2-145">**Resolution:** None.</span></span>

## <a name="debugging-of-class-based-dsc-resources"></a><span data-ttu-id="915b2-146">Osztályalapú DSC-erőforrások hibakeresése</span><span class="sxs-lookup"><span data-stu-id="915b2-146">Debugging of Class-Based DSC Resources</span></span>

<span data-ttu-id="915b2-147">Osztályalapú DSC-erőforrások hibakeresése ebben a kiadásban nem támogatott.</span><span class="sxs-lookup"><span data-stu-id="915b2-147">Debugging of class-based DSC Resources is not supported in this release.</span></span>

<span data-ttu-id="915b2-148">**Megoldás:** Nincs.</span><span class="sxs-lookup"><span data-stu-id="915b2-148">**Resolution:** None.</span></span>

## <a name="variables--functions-defined-in-script-scope-in-dsc-class-based-resource-are-not-preserved-across-multiple-calls-to-a-dsc-resource"></a><span data-ttu-id="915b2-149">Változók és a DSC osztály-alapú erőforrás $script hatókörében meghatározott függvényeket nem maradnak meg több alkalommal hívnia egy DSC-erőforrás között</span><span class="sxs-lookup"><span data-stu-id="915b2-149">Variables & Functions defined in $script scope in DSC Class-Based Resource are not preserved across multiple calls to a DSC Resource</span></span>

<span data-ttu-id="915b2-150">Start-DSCConfiguration több egymást követő hívások sikertelen lesz, ha a konfigurációs van használó osztályalapú erőforrás, amelynek változók vagy $script hatókörében meghatározott függvényeket.</span><span class="sxs-lookup"><span data-stu-id="915b2-150">Multiple consecutive calls to Start-DSCConfiguration will fail if configuration is using any class-based resource which has variables or functions defined in $script scope.</span></span>

<span data-ttu-id="915b2-151">**Megoldás:** Adjon meg a változók és a functions a DSC-erőforrás osztály.</span><span class="sxs-lookup"><span data-stu-id="915b2-151">**Resolution:** Define all variables and functions in DSC Resource class itself.</span></span> <span data-ttu-id="915b2-152">A műveletek/No $script hatókör változókat.</span><span class="sxs-lookup"><span data-stu-id="915b2-152">No $script scope variables/functions.</span></span>

## <a name="dsc-resource-debugging-when-a-resource-is-using-psdscrunascredential"></a><span data-ttu-id="915b2-153">Ha egy erőforrás PSDscRunAsCredential hibakeresés DSC erőforrás</span><span class="sxs-lookup"><span data-stu-id="915b2-153">DSC Resource Debugging when a resource is using PSDscRunAsCredential</span></span>

<span data-ttu-id="915b2-154">DSC-erőforrás hibakeresés erőforrás használatakor a *PSDscRunAsCredential* konfigurációjában tulajdonság nem suported ebben a kiadásban.</span><span class="sxs-lookup"><span data-stu-id="915b2-154">DSC Resource debugging when a resource is using the *PSDscRunAsCredential* property in the configuration is not suported in this release.</span></span>

<span data-ttu-id="915b2-155">**Megoldás:** Nincs.</span><span class="sxs-lookup"><span data-stu-id="915b2-155">**Resolution:** None.</span></span>

## <a name="psdscrunascredential-is-not-supported-for-dsc-composite-resources"></a><span data-ttu-id="915b2-156">PsDscRunAsCredential összetett DSC-erőforrások esetén nem támogatott</span><span class="sxs-lookup"><span data-stu-id="915b2-156">PsDscRunAsCredential is not supported for DSC Composite Resources</span></span>

<span data-ttu-id="915b2-157">**Megoldás:** Hitelesítő adat tulajdonság akkor használható, ha elérhető.</span><span class="sxs-lookup"><span data-stu-id="915b2-157">**Resolution:** Use Credential property if available.</span></span> <span data-ttu-id="915b2-158">Példa ServiceSet és WindowsFeatureSet</span><span class="sxs-lookup"><span data-stu-id="915b2-158">Example ServiceSet and WindowsFeatureSet</span></span>

## <a name="get-dscresource--syntax-does-not-reflect-psdscrunascredential-correctly"></a><span data-ttu-id="915b2-159">*Get-DscResource-szintaxis* nem tükrözi a megfelelő PsDscRunAsCredential</span><span class="sxs-lookup"><span data-stu-id="915b2-159">*Get-DscResource -Syntax* does not reflect PsDscRunAsCredential correctly</span></span>

<span data-ttu-id="915b2-160">Get-DscResource-szintaxist nem tükrözi a PsDscRunAsCredential megfelelően erőforrás jelöli meg, kötelező vagy nem támogatja ezt.</span><span class="sxs-lookup"><span data-stu-id="915b2-160">Get-DscResource -Syntax does not reflect PsDscRunAsCredential correctly when resource marks it as mandatory or does not support it.</span></span>

<span data-ttu-id="915b2-161">**Megoldás:** Nincs.</span><span class="sxs-lookup"><span data-stu-id="915b2-161">**Resolution:** None.</span></span> <span data-ttu-id="915b2-162">Azonban ISE-ben konfigurációs szerzői tükrözi PsDscRunAsCredential tulajdonságra vonatkozó metaadat IntelliSense használatakor.</span><span class="sxs-lookup"><span data-stu-id="915b2-162">However, authoring configuration in ISE reflects correct metadata about PsDscRunAsCredential property when using IntelliSense.</span></span>

## <a name="windowsoptionalfeature-is-not-available-in-windows-7"></a><span data-ttu-id="915b2-163">WindowsOptionalFeature nem érhető el a Windows 7</span><span class="sxs-lookup"><span data-stu-id="915b2-163">WindowsOptionalFeature is not available in Windows 7</span></span>

<span data-ttu-id="915b2-164">A DSC WindowsOptionalFeature erőforrás nem érhető el a Windows 7.</span><span class="sxs-lookup"><span data-stu-id="915b2-164">The WindowsOptionalFeature DSC resource is not available in Windows 7.</span></span> <span data-ttu-id="915b2-165">Ezt az erőforrást igényel a DISM modul, és a DISM-parancsmagok érhetők el a Windows 8 és újabb verzióiban a Windows operációs rendszer indítása.</span><span class="sxs-lookup"><span data-stu-id="915b2-165">This resource requires the DISM module, and DISM cmdlets that are available starting in Windows 8 and newer releases of the Windows operating system.</span></span>

## <a name="for-class-based-dsc-resources-import-dscresource--moduleversion-may-not-work-as-expected"></a><span data-ttu-id="915b2-166">Osztályalapú DSC-erőforrások az Import-DscResource - ModuleVersion esetleg nem működnek megfelelően</span><span class="sxs-lookup"><span data-stu-id="915b2-166">For Class-based DSC resources, Import-DscResource -ModuleVersion may not work as expected</span></span>

<span data-ttu-id="915b2-167">Ha a fordítás csomópont több egy osztályalapú DSC erőforrás-modul verziószámát, `Import-DscResource -ModuleVersion` ne foglalkozzon megadott verzióját és sémafordítási hiba történt a következő eredményez.</span><span class="sxs-lookup"><span data-stu-id="915b2-167">If the compilation node has multiple version of a class-based DSC resource module, `Import-DscResource -ModuleVersion` does not pick the specified version and results in following compilation error.</span></span>

```
ImportClassResourcesFromModule : Exception calling "ImportClassResourcesFromModule" with "3" argument(s): "Keyword 'MyTestResource' already defined in the configuration."
At C:\Windows\system32\WindowsPowerShell\v1.0\Modules\PSDesiredStateConfiguration\PSDesiredStateConfiguration.psm1:2035 char:35
+ ... rcesFound = ImportClassResourcesFromModule -Module $mod -Resources $r ...
+                 ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : NotSpecified: (:) [ImportClassResourcesFromModule], MethodInvocationException
    + FullyQualifiedErrorId : PSInvalidOperationException,ImportClassResourcesFromModule
```

<span data-ttu-id="915b2-168">**Megoldás:** Importálja a szükséges verzióra definiálásával a *ModuleSpecification* az objektum a `-ModuleName` a `RequiredVersion` kulcs van megadva a következőképpen:</span><span class="sxs-lookup"><span data-stu-id="915b2-168">**Resolution:** Import the required version by defining the *ModuleSpecification* object to the `-ModuleName` with `RequiredVersion` key specified as follows:</span></span>

``` PowerShell
Import-DscResource -ModuleName @{ModuleName='MyModuleName';RequiredVersion='1.2'}
```

## <a name="some-dsc-resources-like-registry-resource-may-start-to-take-a-long-time-to-process-the-request"></a><span data-ttu-id="915b2-169">Előfordulhat, hogy egyes DSC-erőforrások, például beállításjegyzék erőforrás időbe telik a kérelem feldolgozása megkezdődött.</span><span class="sxs-lookup"><span data-stu-id="915b2-169">Some DSC resources like registry resource may start to take a long time to process the request.</span></span>

<span data-ttu-id="915b2-170">**Resolution1:** Hozzon létre egy ütemezett feladat, rendszeres időközönként megtisztítja a következő mappát.</span><span class="sxs-lookup"><span data-stu-id="915b2-170">**Resolution1:** Create a schedule task that cleans up the following folder periodically.</span></span>

``` PowerShell
$env:windir\system32\config\systemprofile\AppData\Local\Microsoft\Windows\PowerShell\CommandAnalysis
```

<span data-ttu-id="915b2-171">**Resolution2:** A DSC-konfiguráció karbantartása módosítsa a *CommandAnalysis* végén található a konfigurációs mappát.</span><span class="sxs-lookup"><span data-stu-id="915b2-171">**Resolution2:** Change the DSC configuration to clean up the *CommandAnalysis* folder at the end of the configuration.</span></span>

``` PowerShell
Configuration $configName
{

   # User Data
    Registry SetRegisteredOwner
    {
        Ensure = 'Present'
        Force = $True
        Key = $Node.RegisteredKey
        ValueName = $Node.RegisteredOwnerValue
        ValueType = 'String'
        ValueData = $Node.RegisteredOwnerData
    }
    #
    # Script to delete the config
    #
    script DeleteCommandAnalysisCache
    {
        DependsOn="[Registry]SetRegisteredOwner"
        getscript="@{}"
        testscript = 'Remove-Item -Path $env:windir\system32\config\systemprofile\AppData\Local\Microsoft\Windows\PowerShell\CommandAnalysis -Force -Recurse -ErrorAction SilentlyContinue -ErrorVariable ev | out-null;$true'
        setscript = '$true'
    }
}
```
