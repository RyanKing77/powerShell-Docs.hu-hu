---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "WMF, a powershell, a beállítása"
ms.openlocfilehash: f39328b240a36deb40d484c4aedb889cee91dc8d
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2017
---
# <a name="desired-state-configuration-dsc-known-issues-and-limitations"></a><span data-ttu-id="1f4e5-102">Célállapot-konfiguráció (DSC) ismert problémák és korlátozások</span><span class="sxs-lookup"><span data-stu-id="1f4e5-102">Desired State Configuration (DSC) Known Issues and Limitations</span></span>

<a name="breaking-change-certificates-used-to-encryptdecrypt-passwords-in-dsc-configurations-may-not-work-after-installing-wmf-50-rtm"></a><span data-ttu-id="1f4e5-103">Megtörje módosítása: A DSC-konfigurációk jelszavak titkosításához/visszafejtéséhez használt tanúsítványok nem feltétlenül WMF 5.0 RTM telepítése után</span><span class="sxs-lookup"><span data-stu-id="1f4e5-103">Breaking Change: Certificates used to encrypt/decrypt passwords in DSC configurations may not work after installing WMF 5.0 RTM</span></span>
--------------------------------------------------------------------------------------------------------------------------------

<span data-ttu-id="1f4e5-104">A WMF 4.0-s és a WMF 5.0 Preview kiadásokban DSC nem teszik lehetővé a jelszavak a konfigurációban kell lennie a length több mint 121 karaktereket.</span><span class="sxs-lookup"><span data-stu-id="1f4e5-104">In WMF 4.0 and WMF 5.0 Preview releases, DSC would not allow passwords in the configuration to be of length more than 121 characters.</span></span> <span data-ttu-id="1f4e5-105">A DSC rövid jelszavak használatát, akkor is, ha a hosszú és erős jelszót volt szükség volt kényszerítése.</span><span class="sxs-lookup"><span data-stu-id="1f4e5-105">DSC was forcing to use short passwords even if lengthy and strong password was desired.</span></span> <span data-ttu-id="1f4e5-106">A legfrissebb módosítás lehetővé teszi, hogy a DSC-konfiguráció tetszőleges hosszúságú jelszót.</span><span class="sxs-lookup"><span data-stu-id="1f4e5-106">This breaking change allows passwords to be of arbitrary length in the DSC configuration.</span></span>

<span data-ttu-id="1f4e5-107">**Megoldás:** hozza létre újból a tanúsítványt, amelynek adattitkosítás vagy kulcs rejtjelezése kulcs használatát, és a dokumentum titkosítási kibővített kulcshasználat (1.3.6.1.4.1.311.80.1).</span><span class="sxs-lookup"><span data-stu-id="1f4e5-107">**Resolution:** Re-create the certificate with Data Encipherment or Key Encipherment Key usage, and Document Encryption Enhanced Key usage (1.3.6.1.4.1.311.80.1).</span></span> <span data-ttu-id="1f4e5-108">A TechNet cikknek <https://technet.microsoft.com/en-us/library/dn807171.aspx> további részleteket tartalmaz.</span><span class="sxs-lookup"><span data-stu-id="1f4e5-108">Technet article <https://technet.microsoft.com/en-us/library/dn807171.aspx> has more information.</span></span>


<a name="dsc-cmdlets-may-fail-after-installing-wmf-50-rtm"></a><span data-ttu-id="1f4e5-109">A DSC-parancsmagok sikertelenek lehetnek a WMF 5.0 RTM telepítése után</span><span class="sxs-lookup"><span data-stu-id="1f4e5-109">DSC cmdlets may fail after installing WMF 5.0 RTM</span></span>
------------------------------------------------------------------------------------
<span data-ttu-id="1f4e5-110">Start-DscConfiguration és egyéb DSC-parancsmagokkal meghiúsulhat, miután telepítette a WMF 5.0 RTM-re a következő hiba miatt:</span><span class="sxs-lookup"><span data-stu-id="1f4e5-110">Start-DscConfiguration and other DSC cmdlets may fail after installing WMF 5.0 RTM with the following error:</span></span>
```powershell
    LCM failed to retrieve the property PendingJobStep from the object of class dscInternalCache .
    + CategoryInfo : ObjectNotFound: (root/Microsoft/...gurationManager:String) [], CimException
    + FullyQualifiedErrorId : MI RESULT 6
    + PSComputerName : localhost
```

<span data-ttu-id="1f4e5-111">**Megoldás:** DSCEngineCache.mof törlése a következő parancs futtatásával egy rendszergazda jogú PowerShell-munkamenetben (Futtatás rendszergazdaként):</span><span class="sxs-lookup"><span data-stu-id="1f4e5-111">**Resolution:** Delete DSCEngineCache.mof by running the following command in an elevated PowerShell session (Run as Administrator):</span></span>
    
```powershell
Remove-Item -Path $env:SystemRoot\system32\Configuration\DSCEngineCache.mof
```


<a name="dsc-cmdlets-may-not-work-if-wmf-50-rtm-is-installed-on-top-of-wmf-50-production-preview"></a><span data-ttu-id="1f4e5-112">A DSC-parancsmagok előfordulhat, hogy nem működik, ha a WMF 5.0 RTM WMF 5.0 éles előzetes funkciók mellett kártevőészlelést telepítve van</span><span class="sxs-lookup"><span data-stu-id="1f4e5-112">DSC cmdlets may not work if WMF 5.0 RTM is installed on top of WMF 5.0 Production Preview</span></span>
------------------------------------------------------
<span data-ttu-id="1f4e5-113">**Megoldás:** a következő parancsot egy rendszergazda jogú PowerShell-munkamenetben (Futtatás rendszergazdaként):</span><span class="sxs-lookup"><span data-stu-id="1f4e5-113">**Resolution:** Run the following command in an elevated PowerShell session (run as administrator):</span></span>
```powershell
    mofcomp $env:windir\system32\wbem\DscCoreConfProv.mof
```


<a name="lcm-can-go-into-an-unstable-state-while-using-get-dscconfiguration-in-debugmode"></a><span data-ttu-id="1f4e5-114">LCM is kísérhet instabil állapotban DebugMode a Get-DscConfiguration használata során</span><span class="sxs-lookup"><span data-stu-id="1f4e5-114">LCM can go into an unstable state while using Get-DscConfiguration in DebugMode</span></span>
-------------------------------------------------------------------------------

<span data-ttu-id="1f4e5-115">Ha LCM DebugMode, állítsa le a Get-DscConfiguration feldolgozását a CTRL + C billentyűkombináció lenyomásával okozhat a go LCM instabil állapotban ilyen be, hogy a DSC-parancsmagok többsége nem fognak működni.</span><span class="sxs-lookup"><span data-stu-id="1f4e5-115">If LCM is in DebugMode, pressing CTRL+C to stop the processing of Get-DscConfiguration can cause LCM to go into an unstable state such that majority of DSC cmdlets won’t work.</span></span>

<span data-ttu-id="1f4e5-116">**Megoldás:** nem CTRL + C billentyűkombináció Get-DscConfiguration parancsmag hibakeresés során.</span><span class="sxs-lookup"><span data-stu-id="1f4e5-116">**Resolution:** Don’t press CTRL+C while debugging Get-DscConfiguration cmdlet.</span></span>


<a name="stop-dscconfiguration-may-hang-in-debugmode"></a><span data-ttu-id="1f4e5-117">A DebugMode STOP-DscConfiguration lefagyhat</span><span class="sxs-lookup"><span data-stu-id="1f4e5-117">Stop-DscConfiguration may hang in DebugMode</span></span>
------------------------------------------------------------------------------------------------------------------------
<span data-ttu-id="1f4e5-118">Ha LCM DebugMode, Stop-DscConfiguration leállhat a Get-DscConfiguration által elindított egy műveletet leállítására tett kísérlet közben</span><span class="sxs-lookup"><span data-stu-id="1f4e5-118">If LCM is in DebugMode, Stop-DscConfiguration may hang while trying to stop an operation started by Get-DscConfiguration</span></span>

<span data-ttu-id="1f4e5-119">**Megoldás:** Befejezés szakaszban leírt módon történő Get-DscConfiguration indította a műveletet a hibakeresés "[hibakeresés DSC erőforrások](https://msdn.microsoft.com/powershell/dsc/debugresource)".</span><span class="sxs-lookup"><span data-stu-id="1f4e5-119">**Resolution:** Finish the debugging of the operation started by Get-DscConfiguration as outlined in section ‘[Debugging DSC resources](https://msdn.microsoft.com/powershell/dsc/debugresource)’.</span></span>


<a name="no-verbose-error-messages-are-shown-in-debugmode"></a><span data-ttu-id="1f4e5-120">Részletes hibaüzenetek nem jelennek meg DebugMode</span><span class="sxs-lookup"><span data-stu-id="1f4e5-120">No Verbose Error Messages are shown in DebugMode</span></span>
-----------------------------------------------------------------------------------
<span data-ttu-id="1f4e5-121">Ha LCM DebugMode, a részletes hibaüzeneteket a DSC-források jelennek meg.</span><span class="sxs-lookup"><span data-stu-id="1f4e5-121">If LCM is in DebugMode, no verbose error messages are displayed from DSC Resources.</span></span>

<span data-ttu-id="1f4e5-122">**Megoldás:** letiltása *DebugMode* részletes üzenetek a erőforrás megtekintéséhez</span><span class="sxs-lookup"><span data-stu-id="1f4e5-122">**Resolution:** Disable *DebugMode* to see verbose messages from the resource</span></span>


<a name="invoke-dscresource-operations-cannot-be-retrieved-by-get-dscconfigurationstatus-cmdlet"></a><span data-ttu-id="1f4e5-123">Invoke-DscResource műveletek nem sikerült beolvasni a Get-DscConfigurationStatus parancsmaggal</span><span class="sxs-lookup"><span data-stu-id="1f4e5-123">Invoke-DscResource operations cannot be retrieved by Get-DscConfigurationStatus cmdlet</span></span>
--------------------------------------------------------------------------------------
<span data-ttu-id="1f4e5-124">Után közvetlenül a bármilyen olyan erőforrás módszerek meghívására Invoke-DscResource parancsmag használatával, a rekordok ilyen művelet nem sikerült beolvasni a Get-DscConfigurationStatus egy későbbi időpontban.</span><span class="sxs-lookup"><span data-stu-id="1f4e5-124">After using Invoke-DscResource cmdlet to directly invoke any resource’s methods, the records of such operation cannot be retrieved through Get-DscConfigurationStatus at a later time.</span></span>

<span data-ttu-id="1f4e5-125">**Megoldás:** nincs.</span><span class="sxs-lookup"><span data-stu-id="1f4e5-125">**Resolution:** None.</span></span>


<a name="get-dscconfigurationstatus-returns-pull-cycle-operations-as-type-consistency"></a><span data-ttu-id="1f4e5-126">Get-DscConfigurationStatus értéket ad vissza lekéréses ciklus műveletek típusként *konzisztencia*</span><span class="sxs-lookup"><span data-stu-id="1f4e5-126">Get-DscConfigurationStatus returns pull cycle operations as type *Consistency*</span></span>
---------------------------------------------------------------------------------
<span data-ttu-id="1f4e5-127">Ha egy csomópont értéke LEKÉRÉSES frissítési mód, minden egyes lekéréses műveletet hajtja végre, a Get-DscConfigurationStatus parancsmag jelent-e a művelet típusú, mint *konzisztencia* helyett *kezdeti*</span><span class="sxs-lookup"><span data-stu-id="1f4e5-127">When a node is set to PULL refresh mode, for each pull operation performed, Get-DscConfigurationStatus cmdlet reports the operation type as *Consistency* instead of *Initial*</span></span>

<span data-ttu-id="1f4e5-128">**Megoldás:** nincs.</span><span class="sxs-lookup"><span data-stu-id="1f4e5-128">**Resolution:** None.</span></span>

<a name="invoke-dscresource-cmdlet-does-not-return-message-in-the-order-they-were-produced"></a><span data-ttu-id="1f4e5-129">Invoke-DscResource parancsmag nem ad vissza üzenet állították sorrendben</span><span class="sxs-lookup"><span data-stu-id="1f4e5-129">Invoke-DscResource cmdlet does not return message in the order they were produced</span></span>
---------------------------------------------------------------------------------
<span data-ttu-id="1f4e5-130">Az Invoke-DscResource parancsmag nem ad vissza figyelmeztetést, a részletes és hibaüzeneteket LCM vagy a DSC-erőforrás állították sorrendben.</span><span class="sxs-lookup"><span data-stu-id="1f4e5-130">The Invoke-DscResource cmdlet does not return verbose, warning, and error messages in the order they were produced by LCM or the DSC resource.</span></span>

<span data-ttu-id="1f4e5-131">**Megoldás:** nincs.</span><span class="sxs-lookup"><span data-stu-id="1f4e5-131">**Resolution:** None.</span></span>


<a name="dsc-resources-cannot-be-debugged-easily-when-used-with-invoke-dscresource"></a><span data-ttu-id="1f4e5-132">A DSC-erőforrások nem indítja el egyszerűen Invoke-DscResource használata esetén</span><span class="sxs-lookup"><span data-stu-id="1f4e5-132">DSC Resources cannot be debugged easily when used with Invoke-DscResource</span></span>
-----------------------------------------------------------------------
<span data-ttu-id="1f4e5-133">Ha az LCM hibakeresési módban fut. (lásd: [hibakeresés DSC erőforrások](https://msdn.microsoft.com/powershell/dsc/debugresource) további részletekért), Invoke-DscResource parancsmag nem ad futási térben csatlakoztatni a hibakeresési információ.</span><span class="sxs-lookup"><span data-stu-id="1f4e5-133">When LCM is running in debug mode (see [Debugging DSC resources](https://msdn.microsoft.com/powershell/dsc/debugresource) for more details), Invoke-DscResource cmdlet does not give information about runspace to connect to for debugging.</span></span>
<span data-ttu-id="1f4e5-134">**Megoldás:** felderítése, és csatolja a parancsmagok használatával futási térben **Get-PSHostProcessInfo**, **Enter-PSHostProcess** , **Get-futási térben** és  **Hibakeresési-futási térben** hibakeresése a DSC-erőforrás.</span><span class="sxs-lookup"><span data-stu-id="1f4e5-134">**Resolution:** Discover and attach to the runspace using cmdlets **Get-PSHostProcessInfo**, **Enter-PSHostProcess** , **Get-Runspace** and **Debug-Runspace** to debug the DSC resource.</span></span>

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


<a name="various-partial-configuration-documents-for-same-node-cannot-have-identical-resource-names"></a><span data-ttu-id="1f4e5-135">Azonos csomópont különböző részleges konfigurációs dokumentumok azonos erőforrás neve nem lehet.</span><span class="sxs-lookup"><span data-stu-id="1f4e5-135">Various Partial Configuration documents for same node cannot have identical resource names</span></span>
------------------------------------------------------------------------------------------

<span data-ttu-id="1f4e5-136">Több részleges konfigurációkat egyetlen csomópont vannak telepítve, az erőforrások OK azonos nevű futásidejű hiba.</span><span class="sxs-lookup"><span data-stu-id="1f4e5-136">For several partial configurations that are deployed onto a single node, identical names of resources cause run time error.</span></span>

<span data-ttu-id="1f4e5-137">**Megoldás:** különböző részleges konfigurációk is ugyanazokat az erőforrásokat különböző neveket használja.</span><span class="sxs-lookup"><span data-stu-id="1f4e5-137">**Resolution:** Use different names for even same resources in different partial configurations.</span></span>


<a name="start-dscconfiguration-useexisting-does-not-work-with--credential"></a><span data-ttu-id="1f4e5-138">Start-DscConfiguration – UseExisting nem működik a - Credential</span><span class="sxs-lookup"><span data-stu-id="1f4e5-138">Start-DscConfiguration –UseExisting does not work with -Credential</span></span>
------------------------------------------------------------------

<span data-ttu-id="1f4e5-139">– UseExisting paraméterrel, a Start-DscConfiguration használatakor az-Credential paraméter a rendszer figyelmen kívül hagyja.</span><span class="sxs-lookup"><span data-stu-id="1f4e5-139">When using Start-DscConfiguration with –UseExisting parameter, the –Credential parameter is ignored.</span></span> <span data-ttu-id="1f4e5-140">A DSC alapértelmezett folyamat identitást használja folytatja a műveletet.</span><span class="sxs-lookup"><span data-stu-id="1f4e5-140">DSC uses default process identity to proceed the operation.</span></span> <span data-ttu-id="1f4e5-141">Ez hibát okoz, ha eltérő hitelesítő adatok a távoli csomóponton levő folytatáshoz van szükség.</span><span class="sxs-lookup"><span data-stu-id="1f4e5-141">This causes error when a different credential is needed to proceed on remote node.</span></span>

<span data-ttu-id="1f4e5-142">**Megoldás:** használata CIM munkamenet távoli DSC műveletek:</span><span class="sxs-lookup"><span data-stu-id="1f4e5-142">**Resolution:** Use CIM session for remote DSC operations:</span></span>
```powershell
$session = New-CimSession -ComputerName $node -Credential $credential
Start-DscConfiguration -UseExisting -CimSession $session
```


<a name="ipv6-addresses-as-node-names-in-dsc-configurations"></a><span data-ttu-id="1f4e5-143">IPv6-címek, a csomópont nevének a DSC-konfigurációk</span><span class="sxs-lookup"><span data-stu-id="1f4e5-143">IPv6 Addresses as Node Names in DSC configurations</span></span>
--------------------------------------------------
<span data-ttu-id="1f4e5-144">IPv6-címek, a csomópont nevének a DSC konfigurációs parancsfájlokat ebben a kiadásban nem támogatottak.</span><span class="sxs-lookup"><span data-stu-id="1f4e5-144">IPv6 addresses as node names in DSC configuration scripts are not supported in this release.</span></span>

<span data-ttu-id="1f4e5-145">**Megoldás:** nincs.</span><span class="sxs-lookup"><span data-stu-id="1f4e5-145">**Resolution:** None.</span></span>


<a name="debugging-of-class-based-dsc-resources"></a><span data-ttu-id="1f4e5-146">A DSC osztály-alapú erőforrások hibakeresés</span><span class="sxs-lookup"><span data-stu-id="1f4e5-146">Debugging of Class-Based DSC Resources</span></span>
--------------------------------------
<span data-ttu-id="1f4e5-147">A DSC-erőforrások osztály-alapú hibakeresés nem támogatott ebben a kiadásban.</span><span class="sxs-lookup"><span data-stu-id="1f4e5-147">Debugging of class-based DSC Resources is not supported in this release.</span></span>

<span data-ttu-id="1f4e5-148">**Megoldás:** nincs.</span><span class="sxs-lookup"><span data-stu-id="1f4e5-148">**Resolution:** None.</span></span>


<a name="variables--functions-defined-in-script-scope-in-dsc-class-based-resource-are-not-preserved-across-multiple-calls-to-a-dsc-resource"></a><span data-ttu-id="1f4e5-149">Változók & DSC osztály-alapú erőforrás $script hatókörben megadott függvények nem maradnak meg több hívások DSC-erőforrás között</span><span class="sxs-lookup"><span data-stu-id="1f4e5-149">Variables & Functions defined in $script scope in DSC Class-Based Resource are not preserved across multiple calls to a DSC Resource</span></span> 
-------------------------------------------------------------------------------------------------------------------------------------

<span data-ttu-id="1f4e5-150">Start-DSCConfiguration több egymást követő hívások sikertelen lesz, ha a configuration osztály-alapú erőforrás, változók vagy $script hatókörben megadott funkciók használ.</span><span class="sxs-lookup"><span data-stu-id="1f4e5-150">Multiple consecutive calls to Start-DSCConfiguration will fail if configuration is using any class-based resource which has variables or functions defined in $script scope.</span></span>

<span data-ttu-id="1f4e5-151">**Megoldás:** DSC erőforrásosztály magát a változók és a funkciók meghatározása.</span><span class="sxs-lookup"><span data-stu-id="1f4e5-151">**Resolution:** Define all variables and functions in DSC Resource class itself.</span></span> <span data-ttu-id="1f4e5-152">No $script hatókör változók vagy funkciók.</span><span class="sxs-lookup"><span data-stu-id="1f4e5-152">No $script scope variables/functions.</span></span>


<a name="dsc-resource-debugging-when-a-resource-is-using-psdscrunascredential"></a><span data-ttu-id="1f4e5-153">Ha egy erőforrás PSDscRunAsCredential hibakeresés DSC erőforrás</span><span class="sxs-lookup"><span data-stu-id="1f4e5-153">DSC Resource Debugging when a resource is using PSDscRunAsCredential</span></span>
----------------------------------------------------------------------
<span data-ttu-id="1f4e5-154">A DSC erőforrás hibakeresési erőforrás használatakor a *PSDscRunAsCredential* tulajdonság a konfigurációban nincs suported ebben a kiadásban.</span><span class="sxs-lookup"><span data-stu-id="1f4e5-154">DSC Resource debugging when a resource is using the *PSDscRunAsCredential* property in the configuration is not suported in this release.</span></span>

<span data-ttu-id="1f4e5-155">**Megoldás:** nincs.</span><span class="sxs-lookup"><span data-stu-id="1f4e5-155">**Resolution:** None.</span></span>


<a name="psdscrunascredential-is-not-supported-for-dsc-composite-resources"></a><span data-ttu-id="1f4e5-156">PsDscRunAsCredential DSC összetett erőforrások esetén nem támogatott</span><span class="sxs-lookup"><span data-stu-id="1f4e5-156">PsDscRunAsCredential is not supported for DSC Composite Resources</span></span>
----------------------------------------------------------------

<span data-ttu-id="1f4e5-157">**Megoldás:** használata Credential tulajdonság, ha elérhető.</span><span class="sxs-lookup"><span data-stu-id="1f4e5-157">**Resolution:** Use Credential property if available.</span></span> <span data-ttu-id="1f4e5-158">Példa ServiceSet és WindowsFeatureSet</span><span class="sxs-lookup"><span data-stu-id="1f4e5-158">Example ServiceSet and WindowsFeatureSet</span></span>


<a name="get-dscresource--syntax-does-not-reflect-psdscrunascredential-correctly"></a><span data-ttu-id="1f4e5-159">*Get-DscResource-szintaxis* nem tükrözi a megfelelő PsDscRunAsCredential</span><span class="sxs-lookup"><span data-stu-id="1f4e5-159">*Get-DscResource -Syntax* does not reflect PsDscRunAsCredential correctly</span></span>
-------------------------------------------------------------------------
<span data-ttu-id="1f4e5-160">Get-DscResource-szintaxis nem tükrözi PsDscRunAsCredential megfelelően erőforrás kötelezőként jelöli meg, vagy nem támogatja ezt.</span><span class="sxs-lookup"><span data-stu-id="1f4e5-160">Get-DscResource -Syntax does not reflect PsDscRunAsCredential correctly when resource marks it as mandatory or does not support it.</span></span>

<span data-ttu-id="1f4e5-161">**Megoldás:** nincs.</span><span class="sxs-lookup"><span data-stu-id="1f4e5-161">**Resolution:** None.</span></span> <span data-ttu-id="1f4e5-162">Azonban ISE konfigurációs szerzői tükrözi PsDscRunAsCredential tulajdonságra vonatkozó metaadat IntelliSense használatakor.</span><span class="sxs-lookup"><span data-stu-id="1f4e5-162">However, authoring configuration in ISE reflects correct metadata about PsDscRunAsCredential property when using IntelliSense.</span></span>


<a name="windowsoptionalfeature-is-not-available-in-windows-7"></a><span data-ttu-id="1f4e5-163">WindowsOptionalFeature nem érhető el a Windows 7</span><span class="sxs-lookup"><span data-stu-id="1f4e5-163">WindowsOptionalFeature is not available in Windows 7</span></span>
-----------------------------------------------------

<span data-ttu-id="1f4e5-164">A WindowsOptionalFeature DSC-erőforrás nem érhető el a Windows 7.</span><span class="sxs-lookup"><span data-stu-id="1f4e5-164">The WindowsOptionalFeature DSC resource is not available in Windows 7.</span></span> <span data-ttu-id="1f4e5-165">Ehhez az erőforráshoz van szükség, a DISM-modulját, és a DISM-parancsmagok érhetők el a Windows 8 és újabb verziókban a Windows operációs rendszer elindítása.</span><span class="sxs-lookup"><span data-stu-id="1f4e5-165">This resource requires the DISM module, and DISM cmdlets that are available starting in Windows 8 and newer releases of the Windows operating system.</span></span>

<a name="for-class-based-dsc-resources-import-dscresource--moduleversion-may-not-work-as-expected"></a><span data-ttu-id="1f4e5-166">Osztály-alapú DSC erőforrások importálás-DscResource - ModuleVersion előfordulhat, hogy nem működik megfelelően</span><span class="sxs-lookup"><span data-stu-id="1f4e5-166">For Class-based DSC resources, Import-DscResource -ModuleVersion may not work as expected</span></span>   
------------------------------------------------------------------------------------------
<span data-ttu-id="1f4e5-167">Ha a fordítás fürtcsomópont egy osztály-alapú DSC erőforrásmodul, több verziójának `Import-DscResource -ModuleVersion` nem veszi a megadott verzióját, és annak az eredménye a következő fordítási hiba.</span><span class="sxs-lookup"><span data-stu-id="1f4e5-167">If the compilation node has multiple version of a class-based DSC resource module, `Import-DscResource -ModuleVersion` does not pick the specified version and results in following compilation error.</span></span>

```
ImportClassResourcesFromModule : Exception calling "ImportClassResourcesFromModule" with "3" argument(s): "Keyword 'MyTestResource' already defined in the configuration."
At C:\Windows\system32\WindowsPowerShell\v1.0\Modules\PSDesiredStateConfiguration\PSDesiredStateConfiguration.psm1:2035 char:35
+ ... rcesFound = ImportClassResourcesFromModule -Module $mod -Resources $r ...
+                 ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : NotSpecified: (:) [ImportClassResourcesFromModule], MethodInvocationException
    + FullyQualifiedErrorId : PSInvalidOperationException,ImportClassResourcesFromModule
```

<span data-ttu-id="1f4e5-168">**Megoldás:** importálja a szükséges verziót megadásával a *ModuleSpecification* az objektum a `-ModuleName` a `RequiredVersion` kulcs van megadva az alábbiak szerint:</span><span class="sxs-lookup"><span data-stu-id="1f4e5-168">**Resolution:** Import the required version by defining the *ModuleSpecification* object to the `-ModuleName` with `RequiredVersion` key specified as follows:</span></span>
``` PowerShell  
Import-DscResource -ModuleName @{ModuleName='MyModuleName';RequiredVersion='1.2'}  
```  

<a name="some-dsc-resources-like-registry-resource-may-start-to-take-a-long-time-to-process-the-request"></a><span data-ttu-id="1f4e5-169">Néhány DSC-erőforrásokhoz, mint a beállításjegyzék erőforrás indítsa el a kérelem feldolgozása hosszú ideig tarthat.</span><span class="sxs-lookup"><span data-stu-id="1f4e5-169">Some DSC resources like registry resource may start to take a long time to process the request.</span></span>
--------------------------------------------------------------------------------------------------------------------------------

<span data-ttu-id="1f4e5-170">**Resolution1:** hozzon létre egy ütemezett feladat, amely a szükségtelenné vált a következő mappa rendszeres időközönként.</span><span class="sxs-lookup"><span data-stu-id="1f4e5-170">**Resolution1:** Create a schedule task that cleans up the following folder periodically.</span></span>
``` PowerShell 
$env:windir\system32\config\systemprofile\AppData\Local\Microsoft\Windows\PowerShell\CommandAnalysis 
```

<span data-ttu-id="1f4e5-171">**Resolution2:** karbantartása a DSC-konfiguráció módosítása a *CommandAnalysis* végén található a konfigurációs mappát.</span><span class="sxs-lookup"><span data-stu-id="1f4e5-171">**Resolution2:** Change the DSC configuration to clean up the *CommandAnalysis* folder at the end of the configuration.</span></span>
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

