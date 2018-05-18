---
ms.date: 06/12/2017
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: Erőforrás-készítési ellenőrzőlista
ms.openlocfilehash: 76d9fecca8618fcc178975465f45cda0d0e04064
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/16/2018
---
# <a name="resource-authoring-checklist"></a><span data-ttu-id="84677-103">Erőforrás-készítési ellenőrzőlista</span><span class="sxs-lookup"><span data-stu-id="84677-103">Resource authoring checklist</span></span>
<span data-ttu-id="84677-104">Az alábbi ellenőrzőlista gyakorlati tanácsok listája esetén egy új DSC-erőforrások szerzői.</span><span class="sxs-lookup"><span data-stu-id="84677-104">This checklist is a list of best practices when authoring a new DSC Resource.</span></span>
## <a name="resource-module-contains-psd1-file-and-schemamof-for-every-resource"></a><span data-ttu-id="84677-105">Erőforrás-modul .psd1 fájl és minden erőforráshoz schema.mof tartalmazza</span><span class="sxs-lookup"><span data-stu-id="84677-105">Resource module contains .psd1 file and schema.mof for every resource</span></span>
<span data-ttu-id="84677-106">Ellenőrizze, hogy az erőforrás helyes struktúrával rendelkezik-e, és minden szükséges fájlokat tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="84677-106">Check that your resource has correct structure and contains all required files.</span></span> <span data-ttu-id="84677-107">Minden erőforrás modul tartalmaznia kell egy .psd1 fájlt, és minden nem összetett erőforrás schema.mof fájl kell rendelkeznie.</span><span class="sxs-lookup"><span data-stu-id="84677-107">Every resource module should contain a .psd1 file and every non-composite resource should have schema.mof file.</span></span> <span data-ttu-id="84677-108">Erőforrásokat, amelyek nem tartalmaznak a séma nem jelenik meg által **Get-DscResource** és a felhasználók nem fognak tudni használni az intellisense ilyen modulokhoz kódot ISE írásakor.</span><span class="sxs-lookup"><span data-stu-id="84677-108">Resources that do not contain schema will not be listed by **Get-DscResource** and users will not be able to use the intellisense when writing code against those modules in ISE.</span></span>
<span data-ttu-id="84677-109">A könyvtárstruktúra xRemoteFile-erőforráshoz tartozik, a [xPSDesiredStateConfiguration erőforrásmodul](https://github.com/PowerShell/xPSDesiredStateConfiguration), a következőképpen néz ki:</span><span class="sxs-lookup"><span data-stu-id="84677-109">The directory structure for xRemoteFile resource, which is part of the [xPSDesiredStateConfiguration resource module](https://github.com/PowerShell/xPSDesiredStateConfiguration), looks as follows:</span></span>


```
xPSDesiredStateConfiguration
    DSCResources
        MSFT_xRemoteFile
            MSFT_xRemoteFile.psm1
            MSFT_xRemoteFile.schema.mof
    Examples
        xRemoteFile_DownloadFile.ps1
    ResourceDesignerScripts
        GenerateXRemoteFileSchema.ps1
    Tests
        ResourceDesignerTests.ps1
    xPSDesiredStateConfiguration.psd1
```

## <a name="resource-and-schema-are-correct"></a><span data-ttu-id="84677-110">Erőforrás és a séma helyességéről ##</span><span class="sxs-lookup"><span data-stu-id="84677-110">Resource and schema are correct##</span></span>
<span data-ttu-id="84677-111">Ellenőrizze az erőforrás-séma (\*. schema.mof) fájl.</span><span class="sxs-lookup"><span data-stu-id="84677-111">Verify the resource schema (\*.schema.mof) file.</span></span> <span data-ttu-id="84677-112">Használhatja a [DSC erőforrás Designer](https://www.powershellgallery.com/packages/xDSCResourceDesigner/) fejlesztéséhez és teszteléséhez a séma segítségével.</span><span class="sxs-lookup"><span data-stu-id="84677-112">You can use the [DSC Resource Designer](https://www.powershellgallery.com/packages/xDSCResourceDesigner/) to help develop and test your schema.</span></span>
<span data-ttu-id="84677-113">Győződjön meg arról, hogy:</span><span class="sxs-lookup"><span data-stu-id="84677-113">Make sure that:</span></span>
- <span data-ttu-id="84677-114">Helyesek a Tulajdonságok típusa (pl. nem karakterlánc azokhoz a tulajdonságokhoz, amelyek elfogadják a numerikus érték, kell használni: UInt32 vagy más numerikus helyette)</span><span class="sxs-lookup"><span data-stu-id="84677-114">Property types are correct (e.g. don’t use String for properties which accept numeric values, you should use UInt32 or other numeric types instead)</span></span>
- <span data-ttu-id="84677-115">Tulajdonság attribútumok vannak megadva megfelelően: ([kulcs], [szükséges], [írási], [olvasható])</span><span class="sxs-lookup"><span data-stu-id="84677-115">Property attributes are specified correctly as: ([key], [required], [write], [read])</span></span>
- <span data-ttu-id="84677-116">A séma legalább egy paramétert kell megjelölni a [kulcsként] rendelkezik</span><span class="sxs-lookup"><span data-stu-id="84677-116">At least one parameter in the schema has to be marked as [key]</span></span>
- <span data-ttu-id="84677-117">[olvasható] tulajdonság nem használható együtt: [szükséges], [key], [írási]</span><span class="sxs-lookup"><span data-stu-id="84677-117">[read] property does not coexist together with any of: [required], [key], [write]</span></span>
- <span data-ttu-id="84677-118">Ha több minősítők [olvasható] kivéve van adva, majd [kulcs] elsőbbséget</span><span class="sxs-lookup"><span data-stu-id="84677-118">If multiple qualifiers are specified except [read], then [key] takes precedence</span></span>
- <span data-ttu-id="84677-119">Ha [írási] és [szükséges] van megadva, az elsőbbséget élvez [szükséges]</span><span class="sxs-lookup"><span data-stu-id="84677-119">If [write] and [required] are specified, then [required] takes precedence</span></span>
- <span data-ttu-id="84677-120">ValueMap szükség van megadva.</span><span class="sxs-lookup"><span data-stu-id="84677-120">ValueMap is specified where appropriate</span></span>

<span data-ttu-id="84677-121">Példa:</span><span class="sxs-lookup"><span data-stu-id="84677-121">Example:</span></span>
```
[Read, ValueMap{"Present", "Absent"}, Values{"Present", "Absent"}, Description("Says whether DestinationPath exists on the machine")] String Ensure;
```

- <span data-ttu-id="84677-122">Felhasználóbarát név van megadva, és megerősíti, hogy a DSC-elnevezési konvenciók</span><span class="sxs-lookup"><span data-stu-id="84677-122">Friendly name is specified and confirms to DSC naming conventions</span></span>

<span data-ttu-id="84677-123">Példa: ```[ClassVersion("1.0.0.0"), FriendlyName("xRemoteFile")]```</span><span class="sxs-lookup"><span data-stu-id="84677-123">Example: ```[ClassVersion("1.0.0.0"), FriendlyName("xRemoteFile")]```</span></span>

- <span data-ttu-id="84677-124">Minden mezőnek van beszédes leírást.</span><span class="sxs-lookup"><span data-stu-id="84677-124">Every field has meaningful description.</span></span> <span data-ttu-id="84677-125">A PowerShell GitHub-tárházban rendelkezik jó példa, például a [a. a xRemoteFile schema.mof](https://github.com/PowerShell/xPSDesiredStateConfiguration/blob/dev/DSCResources/MSFT_xRemoteFile/MSFT_xRemoteFile.schema.mof)</span><span class="sxs-lookup"><span data-stu-id="84677-125">The PowerShell GitHub repository has good examples, such as [the .schema.mof for xRemoteFile](https://github.com/PowerShell/xPSDesiredStateConfiguration/blob/dev/DSCResources/MSFT_xRemoteFile/MSFT_xRemoteFile.schema.mof)</span></span>

<span data-ttu-id="84677-126">Ezen felül kell használnia **teszt-xDscResource** és **teszt-xDscSchema** parancsmagjait [DSC erőforrás Designer](https://www.powershellgallery.com/packages/xDSCResourceDesigner/) erőforrás és séma automatikusan ellenőrzéséhez:</span><span class="sxs-lookup"><span data-stu-id="84677-126">Additionally, you should use **Test-xDscResource** and **Test-xDscSchema** cmdlets from [DSC Resource Designer](https://www.powershellgallery.com/packages/xDSCResourceDesigner/) to automatically verify the resource and schema:</span></span>
```
Test-xDscResource <Resource_folder>
Test-xDscSchema <Path_to_resource_schema_file>
```
<span data-ttu-id="84677-127">Például:</span><span class="sxs-lookup"><span data-stu-id="84677-127">For example:</span></span>
```powershell
Test-xDscResource ..\DSCResources\MSFT_xRemoteFile
Test-xDscSchema ..\DSCResources\MSFT_xRemoteFile\MSFT_xRemoteFile.schema.mof
```

## <a name="resource-loads-without-errors"></a><span data-ttu-id="84677-128">Erőforrás-terhelés hibák nélkül</span><span class="sxs-lookup"><span data-stu-id="84677-128">Resource loads without errors</span></span> ##
<span data-ttu-id="84677-129">Ellenőrizze, hogy az erőforrás-modul sikeresen betölthető legyen.</span><span class="sxs-lookup"><span data-stu-id="84677-129">Check whether the resource module can be successfully loaded.</span></span>
<span data-ttu-id="84677-130">Ez elérhető manuálisan, futtatásával `Import-Module <resource_module> -force ` erősítse meg, hogy nincs hiba történt, az írása és tesztelési automation.</span><span class="sxs-lookup"><span data-stu-id="84677-130">This can be achieved manually, by running `Import-Module <resource_module> -force ` and confirming that no errors occurred, or by writing test automation.</span></span> <span data-ttu-id="84677-131">Az utóbbi esetén hajtsa végre ezt a struktúrát a Teszteset a:</span><span class="sxs-lookup"><span data-stu-id="84677-131">In case of the latter, you can follow this structure in your test case:</span></span>
```powershell
$error = $null
Import-Module <resource_module> –force
If ($error.count –ne 0) {
    Throw “Module was not imported correctly. Errors returned: $error”
}
```
## <a name="resource-is-idempotent-in-the-positive-case"></a><span data-ttu-id="84677-132">Erőforrás idempotent pozitív esetben</span><span class="sxs-lookup"><span data-stu-id="84677-132">Resource is idempotent in the positive case</span></span>
<span data-ttu-id="84677-133">A DSC-erőforrások alapvető jellemzői egyik azonosítója lesz.</span><span class="sxs-lookup"><span data-stu-id="84677-133">One of the fundamental characteristics of DSC resources is be idempotence.</span></span> <span data-ttu-id="84677-134">Azt jelenti, hogy egy adott erőforrás többször tartalmazó DSC-konfiguráció alkalmazása mindig érhető el ugyanazt az eredményt.</span><span class="sxs-lookup"><span data-stu-id="84677-134">It means that applying a DSC configuration containing that resource multiple times will always achieve the same result.</span></span> <span data-ttu-id="84677-135">Ha például azt, amely tartalmazza a következő fájl erőforrás-konfiguráció létrehozása:</span><span class="sxs-lookup"><span data-stu-id="84677-135">For example, if we create a configuration which contains the following File resource:</span></span>
```powershell
File file {
    DestinationPath = "C:\test\test.txt"
    Contents = "Sample text"
}
```
<span data-ttu-id="84677-136">Alkalmazás első indításakor, utáni fájl teszt.txt C:\test mappában kell megjelennie.</span><span class="sxs-lookup"><span data-stu-id="84677-136">After applying it for the first time, file test.txt should appear in C:\test folder.</span></span> <span data-ttu-id="84677-137">Azonban későbbi frissítési kísérletei során ugyanaz a konfiguráció nem szükséges módosítani a (pl. nincs másolatot készíteni a teszt.txt fájlról kell létrehozni) a gép állapotát.</span><span class="sxs-lookup"><span data-stu-id="84677-137">However, subsequent runs of the same configuration should not change the state of the machine (e.g. no copies of the test.txt file should be created).</span></span>
<span data-ttu-id="84677-138">Az idempotent ismételten hívása erőforrás biztosításához **Set-TargetResource** az erőforrás ellenőrzése közvetlenül, vagy hívja **Start-DscConfiguration** többször esetén a következőnek teljes körű tesztelés.</span><span class="sxs-lookup"><span data-stu-id="84677-138">To ensure a resource is idempotent you can repeatedly call **Set-TargetResource** when testing the resource directly, or call **Start-DscConfiguration** multiple times when doing end to end testing.</span></span> <span data-ttu-id="84677-139">Az eredmény azonosnak kell lennie minden futtatása után.</span><span class="sxs-lookup"><span data-stu-id="84677-139">The result should be the same after every run.</span></span>


## <a name="test-user-modification-scenario"></a><span data-ttu-id="84677-140">Tesztkörnyezet felhasználó módosítása</span><span class="sxs-lookup"><span data-stu-id="84677-140">Test user modification scenario</span></span> ##
<span data-ttu-id="84677-141">A gép állapotának módosítása, majd ezután futtassa újból a DSC, ellenőrizheti, hogy **Set-TargetResource** és **teszt-TargetResource** működnek majd megfelelően.</span><span class="sxs-lookup"><span data-stu-id="84677-141">By changing the state of the machine and then rerunning DSC, you can verify that **Set-TargetResource** and **Test-TargetResource** function properly.</span></span> <span data-ttu-id="84677-142">Az alábbiakban a lépéseket kell tennie:</span><span class="sxs-lookup"><span data-stu-id="84677-142">Here are steps you should take:</span></span>
1.  <span data-ttu-id="84677-143">Az erőforrás nem a kívánt állapot kezdődik.</span><span class="sxs-lookup"><span data-stu-id="84677-143">Start with the resource not in the desired state.</span></span>
2.  <span data-ttu-id="84677-144">Futtassa az erőforrás-konfiguráció</span><span class="sxs-lookup"><span data-stu-id="84677-144">Run configuration with your resource</span></span>
3.  <span data-ttu-id="84677-145">Győződjön meg arról **teszt-DscConfiguration** igaz értéket ad vissza</span><span class="sxs-lookup"><span data-stu-id="84677-145">Verify **Test-DscConfiguration** returns True</span></span>
4.  <span data-ttu-id="84677-146">A konfigurált elem nem a kívánt állapot módosítása</span><span class="sxs-lookup"><span data-stu-id="84677-146">Modify the configured item to be out of the desired state</span></span>
5.  <span data-ttu-id="84677-147">Győződjön meg arról **teszt-DscConfiguration** adja vissza hamis, a beállításjegyzék használata konkrétabb példa:</span><span class="sxs-lookup"><span data-stu-id="84677-147">Verify **Test-DscConfiguration** returns false Here’s a more concrete example using Registry resource:</span></span>
1.  <span data-ttu-id="84677-148">Indítsa el a beállításkulcs nem található a kívánt állapot</span><span class="sxs-lookup"><span data-stu-id="84677-148">Start with registry key not in the desired state</span></span>
2.  <span data-ttu-id="84677-149">Futtatás **Start-DscConfiguration** elhelyezi a megfelelő állapotban, és győződjön meg arról, hogy a konfiguráció megfelel.</span><span class="sxs-lookup"><span data-stu-id="84677-149">Run **Start-DscConfiguration** with a configuration to put it in the desired state and verify it passes.</span></span>
3.  <span data-ttu-id="84677-150">Futtatás **teszt-DscConfiguration** , és ellenőrizze, hogy igaz értéket ad vissza</span><span class="sxs-lookup"><span data-stu-id="84677-150">Run **Test-DscConfiguration** and verify it returns true</span></span>
4.  <span data-ttu-id="84677-151">A kulcs értékének módosítása, hogy nem a megfelelő állapotban van</span><span class="sxs-lookup"><span data-stu-id="84677-151">Modify the value of the key so that it is not in the desired state</span></span>
5.  <span data-ttu-id="84677-152">Futtatás **teszt-DscConfiguration** , és ellenőrizze a hamis értéket ad vissza</span><span class="sxs-lookup"><span data-stu-id="84677-152">Run **Test-DscConfiguration** and verify it returns false</span></span>
6.  <span data-ttu-id="84677-153">Get-TargetResource funkciókat használja a Get-DscConfiguration ellenőrzés</span><span class="sxs-lookup"><span data-stu-id="84677-153">Get-TargetResource functionality was verified using Get-DscConfiguration</span></span>

<span data-ttu-id="84677-154">Get-TargetResource térjen vissza az erőforrás jelenlegi állapotával részleteit.</span><span class="sxs-lookup"><span data-stu-id="84677-154">Get-TargetResource should return details of the current state of the resource.</span></span> <span data-ttu-id="84677-155">Ügyeljen arra, hogy kipróbálja a Get-DscConfiguration hívása után a konfiguráció alkalmazásához, és ellenőrzi, hogy a kimeneti megfelelően tükrözi a gép aktuális állapotát.</span><span class="sxs-lookup"><span data-stu-id="84677-155">Make sure to test it by calling Get-DscConfiguration after you apply the configuration and verifying that output correctly reflects the current state of the machine.</span></span> <span data-ttu-id="84677-156">Fontos, ha kipróbálja külön-külön, mivel ez a terület esetleg felmerülő problémákat nem jelenik meg, Start-DscConfiguration hívásakor.</span><span class="sxs-lookup"><span data-stu-id="84677-156">It's important to test it separately, since any issues in this area won't appear when calling Start-DscConfiguration.</span></span>

## <a name="call-getsettest-targetresource-functions-directly"></a><span data-ttu-id="84677-157">Hívás **Get vagy Set/Test-TargetResource** közvetlenül működik</span><span class="sxs-lookup"><span data-stu-id="84677-157">Call **Get/Set/Test-TargetResource** functions directly</span></span> ##

<span data-ttu-id="84677-158">Győződjön meg arról, hogy tesztelje a **Get vagy Set/Test-TargetResource** funkciók valósítják meg az erőforrás őket közvetlenül hívó, valamint annak ellenőrzését, vártnak megfelelően működnek.</span><span class="sxs-lookup"><span data-stu-id="84677-158">Make sure you test the **Get/Set/Test-TargetResource** functions implemented in your resource by calling them directly and verifying that they work as expected.</span></span>

## <a name="verify-end-to-end-using-start-dscconfiguration"></a><span data-ttu-id="84677-159">Ellenőrizze a végpontok közötti használatával **Start-DscConfiguration**</span><span class="sxs-lookup"><span data-stu-id="84677-159">Verify End to End using **Start-DscConfiguration**</span></span> ##

<span data-ttu-id="84677-160">Tesztelési **Get vagy Set/Test-TargetResource** azokat közvetlenül meghívásával funkciók azért fontos, de nem minden probléma így fog történni.</span><span class="sxs-lookup"><span data-stu-id="84677-160">Testing **Get/Set/Test-TargetResource** functions by calling them directly is important, but not all issues will be discovered this way.</span></span> <span data-ttu-id="84677-161">A tesztelés használatával jelentős részét irányul **Start-DscConfiguration** vagy a lekérési kiszolgálójával.</span><span class="sxs-lookup"><span data-stu-id="84677-161">You should focus significant part of your testing on using **Start-DscConfiguration** or the pull server.</span></span> <span data-ttu-id="84677-162">Ez valójában a felhasználók hogyan használják az erőforrás, így nem alulbecsülheti vizsgálatok az ilyen típusú jelentőségét.</span><span class="sxs-lookup"><span data-stu-id="84677-162">In fact, this is how users will use the resource, so don’t underestimate the significance of this type of tests.</span></span>
<span data-ttu-id="84677-163">Problémák lehetséges típusait:</span><span class="sxs-lookup"><span data-stu-id="84677-163">Possible types of issues:</span></span>
- <span data-ttu-id="84677-164">Hitelesítő adatok/munkamenet is eltérően viselkednek, mivel szolgáltatásként fut a DSC-ügynök.</span><span class="sxs-lookup"><span data-stu-id="84677-164">Credential/Session may behave differently because the DSC agent runs as a service.</span></span>  <span data-ttu-id="84677-165">Mindenképpen próbálja ki a szolgáltatásokat itt végpont.</span><span class="sxs-lookup"><span data-stu-id="84677-165">Be sure to test any features here end to end.</span></span>
- <span data-ttu-id="84677-166">Hibák kimenetét az **Start-DscConfiguration** jelenik meg, ha hívása házirendektől eltérő lehet a **Set-TargetResource** közvetlenül működik.</span><span class="sxs-lookup"><span data-stu-id="84677-166">Errors output by **Start-DscConfiguration** may be different than those displayed when calling the **Set-TargetResource** function directly.</span></span>

## <a name="test-compatability-on-all-dsc-supported-platforms"></a><span data-ttu-id="84677-167">Teszt kompatibilitási összes DSC a támogatott platformok</span><span class="sxs-lookup"><span data-stu-id="84677-167">Test compatability on all DSC supported platforms</span></span> ##
<span data-ttu-id="84677-168">Erőforrás kell működnie az összes DSC támogatott platformon (Windows Server 2008 R2 és újabb).</span><span class="sxs-lookup"><span data-stu-id="84677-168">Resource should work on all DSC supported platforms (Windows Server 2008 R2 and newer).</span></span> <span data-ttu-id="84677-169">A WMF legújabb Verziójára (a Windows Management Framework) telepítse az operációs rendszer DSC legújabb verziójának.</span><span class="sxs-lookup"><span data-stu-id="84677-169">Install the latest WMF (Windows Management Framework) on your OS to get the latest version of DSC.</span></span> <span data-ttu-id="84677-170">Ha az erőforrás nem működik az egyes ezekről a platformokról úgy lett kialakítva, vissza kell egy specifikus hibaüzenet.</span><span class="sxs-lookup"><span data-stu-id="84677-170">If your resource does not work on some of these platforms by design, a specific error message should be returned.</span></span> <span data-ttu-id="84677-171">Ellenőrizze azt is, az erőforrás ellenőrzi, hogy hívott parancsmagok megtalálható az adott számítógépet.</span><span class="sxs-lookup"><span data-stu-id="84677-171">Also, make sure your resource checks whether cmdlets you are calling are present on particular machine.</span></span> <span data-ttu-id="84677-172">Windows Server 2012 új parancsmagokat, amelyek nem állnak rendelkezésre a Windows Server 2008R2, még akkor is a WMF telepítése számos hozzá.</span><span class="sxs-lookup"><span data-stu-id="84677-172">Windows Server 2012 added a large number of new cmdlets that are not available on Windows Server 2008R2, even with WMF installed.</span></span>

## <a name="verify-on-windows-client-if-applicable"></a><span data-ttu-id="84677-173">Ellenőrizze a Windows-ügyfelén (ha van ilyen)</span><span class="sxs-lookup"><span data-stu-id="84677-173">Verify on Windows Client (if applicable)</span></span> ##
<span data-ttu-id="84677-174">Egy nagyon gyakori teszt résnek ellenőrzi az erőforrás csak a Windows server-verziók.</span><span class="sxs-lookup"><span data-stu-id="84677-174">One very common test gap is verifying the resource only on server versions of Windows.</span></span> <span data-ttu-id="84677-175">Sok erőforrást is tervezték az ügyfél-SKU, így ha, abban az esetben, ha igaz, ne feledje, tesztelje azokat platformokon.</span><span class="sxs-lookup"><span data-stu-id="84677-175">Many resources are also designed to work on Client SKUs, so if that’s true in your case, don’t forget to test it on those platforms as well.</span></span>
## <a name="get-dscresource-lists-the-resource"></a><span data-ttu-id="84677-176">Get-DSCResource sorolja fel az erőforrás</span><span class="sxs-lookup"><span data-stu-id="84677-176">Get-DSCResource lists the resource</span></span> ##
<span data-ttu-id="84677-177">A modul való telepítése után hívja a Get-DscResource szerepelnie kell többek között az erőforrás eredményeképpen.</span><span class="sxs-lookup"><span data-stu-id="84677-177">After deploying the module, calling Get-DscResource should list your resource among others as a result.</span></span> <span data-ttu-id="84677-178">Ha az erőforrás nem található a listában, győződjön meg arról, hogy schema.mof fájl erőforrás létezik.</span><span class="sxs-lookup"><span data-stu-id="84677-178">If you can’t find your resource in the list, make sure that schema.mof file for that resource exists.</span></span>
## <a name="resource-module-contains-examples"></a><span data-ttu-id="84677-179">Erőforrás-modul példákat tartalmaz</span><span class="sxs-lookup"><span data-stu-id="84677-179">Resource module contains examples</span></span> ##
<span data-ttu-id="84677-180">Létrehozása, amely segíteni fog másoknak minőségi példák megtudhatja, hogyan használják.</span><span class="sxs-lookup"><span data-stu-id="84677-180">Creating quality examples which will help others understand how to use it.</span></span> <span data-ttu-id="84677-181">Ez különösen fontos, különösen, mivel számos felhasználó mintakód tekinti dokumentációját.</span><span class="sxs-lookup"><span data-stu-id="84677-181">This is crucial, especially since many users treat sample code as documentation.</span></span>
- <span data-ttu-id="84677-182">Először azt kell meghatározni a példákat is fog szerepelni a modulja – minimum, ki kell terjednie az erőforrás legfontosabb használati esetek:</span><span class="sxs-lookup"><span data-stu-id="84677-182">First, you should determine the examples that will be included with the module – at minimum, you should cover most important use cases for your resource:</span></span>
- <span data-ttu-id="84677-183">Ha a modul több olyan erőforrásokat tartalmaz, működjön együtt egy végpont forgatókönyvhöz szükséges, az alapszintű végpont példa ideális esetben első.</span><span class="sxs-lookup"><span data-stu-id="84677-183">If your module contains several resources that need to work together for an end-to-end scenario, the basic end-to-end example would ideally be first.</span></span>
- <span data-ttu-id="84677-184">A kezdeti példák nagyon egyszerű--kell lennie az erőforrásokhoz (pl. a új virtuális merevlemez létrehozása) kis kezelhető csoportokká az első lépések</span><span class="sxs-lookup"><span data-stu-id="84677-184">The initial examples should be very simple -- how to get started with your resources in small manageable chunks (e.g. creating a new VHD)</span></span>
- <span data-ttu-id="84677-185">További példák kell létrehozása az adott példák (pl. a virtuális gép létrehozása a virtuális Merevlemezek, virtuális gép, módosítja a virtuális gép eltávolításakor) kiszolgálón, és speciális funkciók (például egy virtuális gép létrehozása a dinamikus memória) megjelenítése</span><span class="sxs-lookup"><span data-stu-id="84677-185">Subsequent examples should build on those examples (e.g. creating a VM from a VHD, removing VM, modifying VM), and show advanced functionality (e.g. creating a VM with dynamic memory)</span></span>
- <span data-ttu-id="84677-186">Példa konfigurációk kell paraméteres (összes értéket kell átadni a konfigurációs paraméterek, és nem változtatható értékek lehetnek):</span><span class="sxs-lookup"><span data-stu-id="84677-186">Example configurations should be parameterized (all values should be passed to the configuration as parameters and there should be no hardcoded values):</span></span>
```powershell
configuration Sample_xRemoteFile_DownloadFile
{
    param
    (
        [string[]] $nodeName = 'localhost',

        [parameter(Mandatory = $true)]
        [ValidateNotNullOrEmpty()]
        [String] $destinationPath,

        [parameter(Mandatory = $true)]
        [ValidateNotNullOrEmpty()]
        [String] $uri,

        [String] $userAgent,

        [Hashtable] $headers
    )

    Import-DscResource -Name MSFT_xRemoteFile -ModuleName xPSDesiredStateConfiguration

    Node $nodeName
    {
        xRemoteFile DownloadFile
        {
            DestinationPath = $destinationPath
            Uri = $uri
            UserAgent = $userAgent
            Headers = $headers
        }
    }
}
```
- <span data-ttu-id="84677-187">Ajánlott (megjegyzésként, kimenő), hogyan hívhatja meg a konfigurációs folyamat végén a példaként megadott parancsfájlt a tényleges értékeket tartalmaznak.</span><span class="sxs-lookup"><span data-stu-id="84677-187">It’s a good practice to include (commented out) example of how to call the configuration with the actual values at the end of the example script.</span></span>
<span data-ttu-id="84677-188">Például a fenti konfigurációban nem feltétlenül nyilvánvaló, hogy a legjobb adja meg a felhasználói ügynök módja:</span><span class="sxs-lookup"><span data-stu-id="84677-188">For example, in the configuration above it isn't neccessarily obvious that the best way to specify UserAgent is:</span></span>

<span data-ttu-id="84677-189">`UserAgent = [Microsoft.PowerShell.Commands.PSUserAgent]::InternetExplorer` Ebben az esetben a Megjegyzés szolgálhatnak a konfiguráció kívánt végrehajtása:</span><span class="sxs-lookup"><span data-stu-id="84677-189">`UserAgent = [Microsoft.PowerShell.Commands.PSUserAgent]::InternetExplorer` In which case a comment can clarify the intended execution of the configuration:</span></span>
```
<#
Sample use (parameter values need to be changed according to your scenario):

Sample_xRemoteFile_DownloadFile -destinationPath "$env:SystemDrive\fileName.jpg" -uri "http://www.contoso.com/image.jpg"

Sample_xRemoteFile_DownloadFile -destinationPath "$env:SystemDrive\fileName.jpg" -uri "http://www.contoso.com/image.jpg" `
-userAgent [Microsoft.PowerShell.Commands.PSUserAgent]::InternetExplorer -headers @{"Accept-Language" = "en-US"}
#>
```
- <span data-ttu-id="84677-190">Minden egyes például egy rövid leírást, amelyből megtudhatja, hogyan kezeli, és a paraméterek szerinti írni.</span><span class="sxs-lookup"><span data-stu-id="84677-190">For each example, write a short description which explains what it does, and the meaning of the parameters.</span></span>
- <span data-ttu-id="84677-191">Ellenőrizze, hogy példák az erőforrás legtöbb fontos forgatókönyvekhez, és ha nincs szükség hiányzik, ellenőrizze, hogy az összes hajtható végre, és a gép be a kívánt állapot.</span><span class="sxs-lookup"><span data-stu-id="84677-191">Make sure examples cover most the important scenarios for your resource and if there’s nothing missing, verify that they all execute and put machine in the desired state.</span></span>

## <a name="error-messages-are-easy-to-understand-and-help-users-solve-problems"></a><span data-ttu-id="84677-192">Hibaüzenetek a következők megismeréséhez és problémák megoldására felhasználók könnyen</span><span class="sxs-lookup"><span data-stu-id="84677-192">Error messages are easy to understand and help users solve problems</span></span> ##
<span data-ttu-id="84677-193">Jó hibaüzenetek kell lennie:</span><span class="sxs-lookup"><span data-stu-id="84677-193">Good error messages should be:</span></span>
- <span data-ttu-id="84677-194">: A legnagyobb hibaüzenetek probléma, hogy azok gyakran nem létezik, ezért győződjön meg arról, hogy vannak-e.</span><span class="sxs-lookup"><span data-stu-id="84677-194">There: The biggest problem with error messages is that they often don’t exist, so make sure they are there.</span></span>
- <span data-ttu-id="84677-195">Megértse: emberi olvasható, nem homályos hibakódok</span><span class="sxs-lookup"><span data-stu-id="84677-195">Easy to understand: Human readable, no obscure error codes</span></span>
- <span data-ttu-id="84677-196">Pontos: Mi az, hogy pontosan a hiba leírása</span><span class="sxs-lookup"><span data-stu-id="84677-196">Precise: Describe what’s exactly the problem</span></span>
- <span data-ttu-id="84677-197">Vélelmezett: A Tanácsot a probléma megoldásához</span><span class="sxs-lookup"><span data-stu-id="84677-197">Constructive: Advice how to fix the issue</span></span>
- <span data-ttu-id="84677-198">Udvarias: Nem vétkesség felhasználói vagy azok érzi, hogy rossz gondoskodjon győződjön meg arról, ellenőrizze, hogy teljes körű forgatókönyvekben hibákat (használatával **Start-DscConfiguration**), mert közvetlenül erőforrás funkciók futtatásakor visszaadott azoktól eltérő lehet.</span><span class="sxs-lookup"><span data-stu-id="84677-198">Polite: Don’t blame user or make them feel bad Make sure you verify errors in End to End scenarios (using **Start-DscConfiguration**), because they may differ from those returned when running resource functions directly.</span></span>

## <a name="log-messages-are-easy-to-understand-and-informative-including-verbose-debug-and-etw-logs"></a><span data-ttu-id="84677-199">Naplóüzenetek: megértse és informatív (beleértve – részletes, – hibakeresési és ETW-naplók)</span><span class="sxs-lookup"><span data-stu-id="84677-199">Log messages are easy to understand and informative (including –verbose, –debug and ETW logs)</span></span> ##
<span data-ttu-id="84677-200">Gondoskodjon arról, hogy az erőforrás által outputted naplók könnyen megértéséhez, és adjon meg értéket a felhasználóhoz.</span><span class="sxs-lookup"><span data-stu-id="84677-200">Ensure that logs outputted by the resource are easy to understand and provide value to the user.</span></span> <span data-ttu-id="84677-201">Erőforrások kell kimeneti minden információt, amely a felhasználó számára hasznos lehet, de további naplók nem mindig jobb.</span><span class="sxs-lookup"><span data-stu-id="84677-201">Resources should output all information which might be helpful to the user, but more logs is not always better.</span></span> <span data-ttu-id="84677-202">Inkább elkerülése érdekében a redundancia és szerint kiírta volna az adatokat, amelyek nem további értéket adjon meg – nem jelöl valaki halad át több száz naplóbejegyzések ahhoz, hogy mi keresnek található.</span><span class="sxs-lookup"><span data-stu-id="84677-202">You should avoid redundancy and outputting data which does not provide additional value – don’t make someone go through hundreds of log entries in order to find what they're looking for.</span></span> <span data-ttu-id="84677-203">Természetesen naplókat nincs az elfogadható megoldás a probléma vagy.</span><span class="sxs-lookup"><span data-stu-id="84677-203">Of course, no logs is not an acceptable solution for this problem either.</span></span>

<span data-ttu-id="84677-204">Vizsgálatakor kell is részletes elemzéséhez és hibakeresési naplókat (futtatásával **Start-DscConfiguration** a-verbose és – megfelelően debug kapcsolók), illetve mint ETW-naplók.</span><span class="sxs-lookup"><span data-stu-id="84677-204">When testing, you should also analyze verbose and debug logs (by running **Start-DscConfiguration** with –verbose and –debug switches appropriately), as well as ETW logs.</span></span> <span data-ttu-id="84677-205">DSC ETW naplók megtekintéséhez nyissa meg az eseménynaplót, és nyissa meg a következő mappát: alkalmazások és szolgáltatások - Microsoft - Windows - célállapot-konfiguráció.</span><span class="sxs-lookup"><span data-stu-id="84677-205">To see DSC ETW logs, go to Event Viewer and open the following folder: Applications and Services- Microsoft - Windows - Desired State Configuration.</span></span>  <span data-ttu-id="84677-206">Alapértelmezés szerint nem fog működési csatornát kell, de ellenőrizze, hogy engedélyezi a elemzési és hibakeresési csatornák a konfiguráció futtatása előtt.</span><span class="sxs-lookup"><span data-stu-id="84677-206">By default there will be Operational channel, but make sure you enable Analytic and Debug channels before running the configuration.</span></span>
<span data-ttu-id="84677-207">Ahhoz, hogy az elemző/Debug csatornák, az alábbi parancsfájl hajthat végre:</span><span class="sxs-lookup"><span data-stu-id="84677-207">To enable Analytic/Debug channels, you can execute script below:</span></span>
```powershell
$statusEnabled = $true
# Use "Analytic" to enable Analytic channel
$eventLogFullName = "Microsoft-Windows-Dsc/Debug"
$commandToExecute = "wevtutil set-log $eventLogFullName /e:$statusEnabled /q:$statusEnabled   "
$log = New-Object System.Diagnostics.Eventing.Reader.EventLogConfiguration $eventLogFullName
if($statusEnabled -eq $log.IsEnabled)
{
    Write-Host -Verbose "The channel event log is already enabled"
    return
}
Invoke-Expression $commandToExecute
```
## <a name="resource-implementation-does-not-contain-hardcoded-paths"></a><span data-ttu-id="84677-208">Erőforrás-implementáció nem tartalmaz szoftveresen kötött elérési utak</span><span class="sxs-lookup"><span data-stu-id="84677-208">Resource implementation does not contain hardcoded paths</span></span> ##
<span data-ttu-id="84677-209">Ellenőrizze, hogy nincsenek nincsenek szoftveresen kötött elérési utak erőforrás végrehajtásában, különösen akkor, ha azok feltételezik, hogy nyelvi (en-us), vagy ha az rendszerváltozók használható.</span><span class="sxs-lookup"><span data-stu-id="84677-209">Ensure there are no hardcoded paths in the resource implementation, particularly if they assume language (en-us), or when there are system variables that can be used.</span></span>
<span data-ttu-id="84677-210">Ha az erőforrás kell egyedi elérési utak, a környezeti változók hardcoding helyett a útvonalat használja, mivel más számítógépeken eltérőek lehetnek.</span><span class="sxs-lookup"><span data-stu-id="84677-210">If your resource need to access specific paths, use environment variables instead of hardcoding the path, as it may differ on other machines.</span></span>

<span data-ttu-id="84677-211">Példa:</span><span class="sxs-lookup"><span data-stu-id="84677-211">Example:</span></span>

<span data-ttu-id="84677-212">ahelyett, hogy:</span><span class="sxs-lookup"><span data-stu-id="84677-212">Instead of:</span></span>
```
$tempPath = "C:\Users\kkaczma\AppData\Local\Temp\MyResource"
$programFilesPath = "C:\Program Files (x86)"
 ```
<span data-ttu-id="84677-213">Írhat:</span><span class="sxs-lookup"><span data-stu-id="84677-213">You can write:</span></span>
```
$tempPath = Join-Path $env:temp "MyResource"
$programFilesPath = ${env:ProgramFiles(x86)}
```
## <a name="resource-implementation-does-not-contain-user-information"></a><span data-ttu-id="84677-214">Erőforrás-implementáció nem tartalmaz felhasználói adatokat</span><span class="sxs-lookup"><span data-stu-id="84677-214">Resource implementation does not contain user information</span></span> ##
<span data-ttu-id="84677-215">Győződjön meg arról, hogy nincsenek e-mail nevek, fiók adatait, vagy a kód nevek.</span><span class="sxs-lookup"><span data-stu-id="84677-215">Make sure there are no email names, account information, or names of people in the code.</span></span>
## <a name="resource-was-tested-with-validinvalid-credentials"></a><span data-ttu-id="84677-216">Erőforrás teszteltük, érvényes érvénytelen hitelesítő adatokkal</span><span class="sxs-lookup"><span data-stu-id="84677-216">Resource was tested with valid/invalid credentials</span></span> ##
<span data-ttu-id="84677-217">Ha az erőforrás hitelesítő adatokat fogad paraméterként:</span><span class="sxs-lookup"><span data-stu-id="84677-217">If your resource takes a credential as parameter:</span></span>
- <span data-ttu-id="84677-218">Az erőforrás works ellenőrizze, ha a helyi rendszer (vagy a távoli erőforrásokhoz tartozó számítógépfiók) nem rendelkezik hozzáféréssel.</span><span class="sxs-lookup"><span data-stu-id="84677-218">Verify the resource works when Local System (or the computer account for remote resources) does not have access.</span></span>
- <span data-ttu-id="84677-219">Ellenőrizze az erőforrás működik a megadott hitelesítő adatok beszerzéséhez beállítva, és tesztelése</span><span class="sxs-lookup"><span data-stu-id="84677-219">Verify the resource works with a credential specified for Get, Set and Test</span></span>
- <span data-ttu-id="84677-220">Ha az erőforrás megosztások fér hozzá, tesztelése a támogatandó, például a Variant típusú adatok:</span><span class="sxs-lookup"><span data-stu-id="84677-220">If your resource accesses shares, test all the variants you need to support, such as:</span></span>
  - <span data-ttu-id="84677-221">Szabványos windows-megosztásokat.</span><span class="sxs-lookup"><span data-stu-id="84677-221">Standard windows shares.</span></span>
  - <span data-ttu-id="84677-222">Elosztott fájlrendszer-megosztásokat.</span><span class="sxs-lookup"><span data-stu-id="84677-222">DFS shares.</span></span>
  - <span data-ttu-id="84677-223">SAMBA megosztások (Ha a támogatni kívánt Linux.)</span><span class="sxs-lookup"><span data-stu-id="84677-223">SAMBA shares (if you want to support Linux.)</span></span>

## <a name="resource-does-not-require-interactive-input"></a><span data-ttu-id="84677-224">Az erőforrásnál nincs szükség interaktív bemeneti</span><span class="sxs-lookup"><span data-stu-id="84677-224">Resource does not require interactive input</span></span> ##
<span data-ttu-id="84677-225">**GET vagy Set/Test-TargetResource** funkciók automatikusan hajtható végre, és nem kell várnia, a felhasználó bármely szakaszában végrehajtási bemeneti (pl. ne használjon **Get-Credential** ezeket a funkciókat belül).</span><span class="sxs-lookup"><span data-stu-id="84677-225">**Get/Set/Test-TargetResource** functions should be executed automatically and must not wait for user’s input at any stage of execution (e.g. you should not use **Get-Credential** inside these functions).</span></span> <span data-ttu-id="84677-226">Meg kell adnia a felhasználótól, ha meg kell adja át a konfigurációs paramétere a fordítási fázis során.</span><span class="sxs-lookup"><span data-stu-id="84677-226">If you need to provide user’s input, you should pass it to the configuration as parameter during the compilation phase.</span></span>
## <a name="resource-functionality-was-thoroughly-tested"></a><span data-ttu-id="84677-227">Erőforrás-funkcióit alaposan teszteltük.</span><span class="sxs-lookup"><span data-stu-id="84677-227">Resource functionality was thoroughly tested</span></span> ##
<span data-ttu-id="84677-228">Ezt az ellenőrző listát tartalmaz elemeket, amelyek fontosak, tesztelése és/vagy gyakran nem talált.</span><span class="sxs-lookup"><span data-stu-id="84677-228">This checklist contains items which are important to be tested and/or are often missed.</span></span> <span data-ttu-id="84677-229">Tesztet hajt végre, főleg működési néhányat a meglévők közül ez az éppen tesztel, és itt nem szerepelnek az erőforráshoz adott bunch lesz.</span><span class="sxs-lookup"><span data-stu-id="84677-229">There will be bunch of tests, mainly functional ones which will be specific to the resource you are testing and are not mentioned here.</span></span> <span data-ttu-id="84677-230">Ne feledje kapcsolatos negatív teszteseteket is tartalmaz.</span><span class="sxs-lookup"><span data-stu-id="84677-230">Don’t forget about negative test cases.</span></span>
## <a name="best-practice-resource-module-contains-tests-folder-with-resourcedesignertestsps1-script"></a><span data-ttu-id="84677-231">Az ajánlott eljárás: erőforrásmodul tartalmaz tesztek mappát ResourceDesignerTests.ps1-parancsfájllal</span><span class="sxs-lookup"><span data-stu-id="84677-231">Best practice: Resource module contains Tests folder with ResourceDesignerTests.ps1 script</span></span> ##
<span data-ttu-id="84677-232">Jó gyakorlat mappa "teszt" create erőforrásmodul hozzon létre ResourceDesignerTests.ps1 fájlt, és adja hozzá a teszteket **teszt-xDscResource** és **teszt-xDscSchema** lévő összes erőforrás a megadott a modul.</span><span class="sxs-lookup"><span data-stu-id="84677-232">It’s a good practice to create folder “Tests” inside resource module, create ResourceDesignerTests.ps1 file and add tests using **Test-xDscResource** and **Test-xDscSchema** for all resources in given module.</span></span>
<span data-ttu-id="84677-233">Ezzel a módszerrel gyorsan ellenőrizheti az adott modulok és egy megerősítést a közzététel előtt ellenőrizze az összes erőforrás sémák.</span><span class="sxs-lookup"><span data-stu-id="84677-233">This way you can quickly validate schemas of all resources from the given modules and do a sanity check before publishing.</span></span>
<span data-ttu-id="84677-234">XRemoteFile ResourceTests.ps1 egyszerűen sikerült meg:</span><span class="sxs-lookup"><span data-stu-id="84677-234">For xRemoteFile, ResourceTests.ps1 could look as simple as:</span></span>
```powershell
Test-xDscResource ..\DSCResources\MSFT_xRemoteFile
Test-xDscSchema ..\DSCResources\MSFT_xRemoteFile\MSFT_xRemoteFile.schema.mof
```
##<a name="best-practice-resource-folder-contains-resource-designer-script-for-generating-schema"></a><span data-ttu-id="84677-235">Az ajánlott eljárás: erőforrásmappa tartalmaz erőforrás-tervező parancsfájl létrehozásának séma ##</span><span class="sxs-lookup"><span data-stu-id="84677-235">Best practice: Resource folder contains resource designer script for generating schema##</span></span>
<span data-ttu-id="84677-236">Az egyes erőforrások tartalmaznia kell egy erőforrás tervező parancsfájlt, amely állít elő, az erőforrás mof séma.</span><span class="sxs-lookup"><span data-stu-id="84677-236">Each resource should contain a resource designer script which generates a mof schema of the resource.</span></span> <span data-ttu-id="84677-237">Ezt a fájlt kell helyezni <ResourceName>\ResourceDesignerScripts és Generate neve lehet<ResourceName>xRemoteFile erőforrás Schema.ps1 esetében a fájl volna hívni GenerateXRemoteFileSchema.ps1 és tartalmaz:</span><span class="sxs-lookup"><span data-stu-id="84677-237">This file should be placed in <ResourceName>\ResourceDesignerScripts and be named Generate<ResourceName>Schema.ps1 For xRemoteFile resource this file would be called GenerateXRemoteFileSchema.ps1 and contain:</span></span>
```powershell
$DestinationPath = New-xDscResourceProperty -Name DestinationPath -Type String -Attribute Key -Description 'Path under which downloaded or copied file should be accessible after operation.'
$Uri = New-xDscResourceProperty -Name Uri -Type String -Attribute Required -Description 'Uri of a file which should be copied or downloaded. This parameter supports HTTP and HTTPS values.'
$Headers = New-xDscResourceProperty -Name Headers -Type Hashtable[] -Attribute Write -Description 'Headers of the web request.'
$UserAgent = New-xDscResourceProperty -Name UserAgent -Type String -Attribute Write -Description 'User agent for the web request.'
$Ensure = New-xDscResourceProperty -Name Ensure -Type String -Attribute Read -ValidateSet "Present", "Absent" -Description 'Says whether DestinationPath exists on the machine'
$Credential = New-xDscResourceProperty -Name Credential -Type PSCredential -Attribute Write -Description 'Specifies a user account that has permission to send the request.'
$CertificateThumbprint = New-xDscResourceProperty -Name CertificateThumbprint -Type String -Attribute Write -Description 'Digital public key certificate that is used to send the request.'

New-xDscResource -Name MSFT_xRemoteFile -Property @($DestinationPath, $Uri, $Headers, $UserAgent, $Ensure, $Credential, $CertificateThumbprint) -ModuleName xPSDesiredStateConfiguration2 -FriendlyName xRemoteFile
```
## <a name="best-practice-resource-supports--whatif"></a><span data-ttu-id="84677-238">Az ajánlott eljárás: erőforrás - whatif támogatja</span><span class="sxs-lookup"><span data-stu-id="84677-238">Best practice: Resource supports -whatif</span></span> ##
<span data-ttu-id="84677-239">Az erőforrás "veszélyes" műveleteket hajt végre, ajánlott a - whatif funkcióinak végrehajtásához.</span><span class="sxs-lookup"><span data-stu-id="84677-239">If your resource is performing “dangerous” operations, it’s a good practice to implement -whatif functionality.</span></span> <span data-ttu-id="84677-240">Miután elkészült, győződjön meg arról, hogy whatif kimeneti műveleteket, amelyek történne a parancs végrehajtása történt whatif kapcsoló nélkül helyesen írja le.</span><span class="sxs-lookup"><span data-stu-id="84677-240">After it’s done, make sure that whatif output correctly describes operations which would happen if command was executed without whatif switch.</span></span>
<span data-ttu-id="84677-241">Azt is ellenőrizze, hogy a művelet nem futtatható (nem a csomópont állapota módosul) Ha szerepel – whatif paraméter.</span><span class="sxs-lookup"><span data-stu-id="84677-241">Also, verify that operations does not execute (no changes to the node’s state are made) when –whatif switch is present.</span></span>
<span data-ttu-id="84677-242">Például tételezzük fel, hogy azt fájl erőforrás teszteli.</span><span class="sxs-lookup"><span data-stu-id="84677-242">For example, let’s assume we are testing File resource.</span></span> <span data-ttu-id="84677-243">Alább hoz létre a fájl "teszt.txt" tartalom "teszt" egyszerű konfiguráció van:</span><span class="sxs-lookup"><span data-stu-id="84677-243">Below is simple configuration which creates file “test.txt” with contents “test”:</span></span>
```powershell
configuration config
{
    node localhost
    {
        File file
        {
            Contents="test"
            DestinationPath="C:\test\test.txt"
        }
    }
}
config
```
<span data-ttu-id="84677-244">Ha azt fordítási, majd futtassa a konfiguráció a – whatif kapcsolóval a kimeneti ezzel azt jelzi, pontosan mi történne azt a konfigurációs futtatásakor.</span><span class="sxs-lookup"><span data-stu-id="84677-244">If we compile and then execute the configuration with the –whatif switch, the output is telling us exactly what would happen when we run the configuration.</span></span> <span data-ttu-id="84677-245">Maga a konfiguráció azonban nem történt meg (teszt.txt fájl nem jött létre).</span><span class="sxs-lookup"><span data-stu-id="84677-245">The configuration itself however was not executed (test.txt file was not created).</span></span>
```powershell
Start-DscConfiguration -path .\config -ComputerName localhost -wait -verbose -whatif
VERBOSE: Perform operation 'Invoke CimMethod' with following parameters, ''methodName' =
SendConfigurationApply,'className' = MSFT_DSCLocalConfigurationManager,'namespaceName' =
root/Microsoft/Windows/DesiredStateConfiguration'.
VERBOSE: An LCM method call arrived from computer CHARLESX1 with user sid
S-1-5-21-397955417-626881126-188441444-5179871.
What if: [X]: LCM:  [ Start  Set      ]
What if: [X]: LCM:  [ Start  Resource ]  [[File]file]
What if: [X]: LCM:  [ Start  Test     ]  [[File]file]
What if: [X]:                            [[File]file] The system cannot find the file specified.
What if: [X]:                            [[File]file] The related file/directory is: C:\test\test.txt.
What if: [X]: LCM:  [ End    Test     ]  [[File]file]  in 0.0270 seconds.
What if: [X]: LCM:  [ Start  Set      ]  [[File]file]
What if: [X]:                            [[File]file] The system cannot find the file specified.
What if: [X]:                            [[File]file] The related file/directory is: C:\test\test.txt.
What if: [X]:                            [C:\test\test.txt] Creating and writing contents and setting attributes.
What if: [X]: LCM:  [ End    Set      ]  [[File]file]  in 0.0180 seconds.
What if: [X]: LCM:  [ End    Resource ]  [[File]file]
What if: [X]: LCM:  [ End    Set      ]
VERBOSE: [X]: LCM:  [ End    Set      ]    in  0.1050 seconds.
VERBOSE: Operation 'Invoke CimMethod' complete.
```

<span data-ttu-id="84677-246">A lista nem teljes körű, de számos fontos problémák tervezési, fejlesztés és tesztelés DSC erőforrások is történt, amely magában foglalja.</span><span class="sxs-lookup"><span data-stu-id="84677-246">This list is not exhaustive, but it covers many important issues which can be encountered while designing, developing and testing DSC resources.</span></span>