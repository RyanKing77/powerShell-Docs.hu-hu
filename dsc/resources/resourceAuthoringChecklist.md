---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: Erőforrás-készítési ellenőrzőlista
ms.openlocfilehash: 7b1a096bba1b729c096b6689178ee022e12e4634
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/14/2018
ms.locfileid: "53404279"
---
# <a name="resource-authoring-checklist"></a><span data-ttu-id="41c33-103">Erőforrás-készítési ellenőrzőlista</span><span class="sxs-lookup"><span data-stu-id="41c33-103">Resource authoring checklist</span></span>

<span data-ttu-id="41c33-104">Ezzel az ellenőrzőlistával az ajánlott eljárások listája, amikor új DSC-erőforrások szerzői.</span><span class="sxs-lookup"><span data-stu-id="41c33-104">This checklist is a list of best practices when authoring a new DSC Resource.</span></span>

## <a name="resource-module-contains-psd1-file-and-schemamof-for-every-resource"></a><span data-ttu-id="41c33-105">Resource modul .psd1 fájlban, és minden erőforráshoz schema.mof tartalmaz</span><span class="sxs-lookup"><span data-stu-id="41c33-105">Resource module contains .psd1 file and schema.mof for every resource</span></span>

<span data-ttu-id="41c33-106">Ellenőrizze, hogy az erőforrás megfelelő szerkezetéről, és minden szükséges fájlokat tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="41c33-106">Check that your resource has correct structure and contains all required files.</span></span> <span data-ttu-id="41c33-107">Minden erőforrás modul esetleg tartalmaz egy .psd1 fájlban, és minden nem összetett erőforrás schema.mof fájlt kell rendelkeznie.</span><span class="sxs-lookup"><span data-stu-id="41c33-107">Every resource module should contain a .psd1 file and every non-composite resource should have schema.mof file.</span></span> <span data-ttu-id="41c33-108">Erőforrások, amelyek nem rendelkeznek a séma szerint nem lesznek felsorolva `Get-DscResource` és a felhasználók nem fognak tudni használni az intellisense ISE-ben ilyen modulokhoz elleni használt kód írásakor.</span><span class="sxs-lookup"><span data-stu-id="41c33-108">Resources that do not contain schema will not be listed by `Get-DscResource` and users will not be able to use the intellisense when writing code against those modules in ISE.</span></span>
<span data-ttu-id="41c33-109">A könyvtárstruktúra xRemoteFile erőforrás, amely részét képezi, a [xPSDesiredStateConfiguration resource modul](https://github.com/PowerShell/xPSDesiredStateConfiguration), a következőképpen néz ki:</span><span class="sxs-lookup"><span data-stu-id="41c33-109">The directory structure for xRemoteFile resource, which is part of the [xPSDesiredStateConfiguration resource module](https://github.com/PowerShell/xPSDesiredStateConfiguration), looks as follows:</span></span>

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

## <a name="resource-and-schema-are-correct"></a><span data-ttu-id="41c33-110">Erőforrás és a séma helyességét</span><span class="sxs-lookup"><span data-stu-id="41c33-110">Resource and schema are correct</span></span>

<span data-ttu-id="41c33-111">Ellenőrizze az erőforrás-séma (\*. schema.mof) fájlt.</span><span class="sxs-lookup"><span data-stu-id="41c33-111">Verify the resource schema (\*.schema.mof) file.</span></span> <span data-ttu-id="41c33-112">Használhatja a [DSC erőforrás Designer](https://www.powershellgallery.com/packages/xDSCResourceDesigner/1.12.0.0) fejlesztése és tesztelése a séma segítségével.</span><span class="sxs-lookup"><span data-stu-id="41c33-112">You can use the [DSC Resource Designer](https://www.powershellgallery.com/packages/xDSCResourceDesigner/1.12.0.0) to help develop and test your schema.</span></span>
<span data-ttu-id="41c33-113">Győződjön meg arról, hogy:</span><span class="sxs-lookup"><span data-stu-id="41c33-113">Make sure that:</span></span>

- <span data-ttu-id="41c33-114">Tulajdonságtípusok megengedettek helyes-e (pl. ne használjon karakterlánc azokhoz a tulajdonságokhoz, amelyek elfogadják a numerikus értékek, akkor érdemes használni UInt32 más numerikus típusok)</span><span class="sxs-lookup"><span data-stu-id="41c33-114">Property types are correct (e.g. don’t use String for properties which accept numeric values, you should use UInt32 or other numeric types instead)</span></span>
- <span data-ttu-id="41c33-115">Tulajdonság attribútumok helyesen van megadva: ([kulcs], [kötelező], [írási], [olvasási])</span><span class="sxs-lookup"><span data-stu-id="41c33-115">Property attributes are specified correctly as: ([key], [required], [write], [read])</span></span>
- <span data-ttu-id="41c33-116">Legalább egy paramétert a sémában rendelkezik kell megjelölni, [key]</span><span class="sxs-lookup"><span data-stu-id="41c33-116">At least one parameter in the schema has to be marked as [key]</span></span>
- <span data-ttu-id="41c33-117">[olvasható] tulajdonság nem létezhet együtt bármelyik: [kötelező], [key], [írási]</span><span class="sxs-lookup"><span data-stu-id="41c33-117">[read] property does not coexist together with any of: [required], [key], [write]</span></span>
- <span data-ttu-id="41c33-118">Ha több minősítők meg van adva, [olvasási] kivételével, [key] lép érvénybe</span><span class="sxs-lookup"><span data-stu-id="41c33-118">If multiple qualifiers are specified except [read], then [key] takes precedence</span></span>
- <span data-ttu-id="41c33-119">Ha [írási] és [kötelező] van megadva, majd [kötelező] elsőbbséget élvez</span><span class="sxs-lookup"><span data-stu-id="41c33-119">If [write] and [required] are specified, then [required] takes precedence</span></span>
- <span data-ttu-id="41c33-120">ValueMap megadott adott esetben az a példában:</span><span class="sxs-lookup"><span data-stu-id="41c33-120">ValueMap is specified where appropriate Example:</span></span>

  ```
  [Read, ValueMap{"Present", "Absent"}, Values{"Present", "Absent"}, Description("Says whether DestinationPath exists on the machine")] String Ensure;
  ```

- <span data-ttu-id="41c33-121">Felhasználóbarát név van megadva, és megerősíti, hogy elnevezési konvencióinak DSC</span><span class="sxs-lookup"><span data-stu-id="41c33-121">Friendly name is specified and confirms to DSC naming conventions</span></span>

  <span data-ttu-id="41c33-122">Példa: `[ClassVersion("1.0.0.0"), FriendlyName("xRemoteFile")]`</span><span class="sxs-lookup"><span data-stu-id="41c33-122">Example: `[ClassVersion("1.0.0.0"), FriendlyName("xRemoteFile")]`</span></span>

- <span data-ttu-id="41c33-123">Minden mező rendelkezik kifejező leírást.</span><span class="sxs-lookup"><span data-stu-id="41c33-123">Every field has meaningful description.</span></span> <span data-ttu-id="41c33-124">A PowerShell GitHub-adattár tartozik jó példa, például [a. a xRemoteFile schema.mof](https://github.com/PowerShell/xPSDesiredStateConfiguration/blob/dev/DSCResources/MSFT_xRemoteFile/MSFT_xRemoteFile.schema.mof)</span><span class="sxs-lookup"><span data-stu-id="41c33-124">The PowerShell GitHub repository has good examples, such as [the .schema.mof for xRemoteFile](https://github.com/PowerShell/xPSDesiredStateConfiguration/blob/dev/DSCResources/MSFT_xRemoteFile/MSFT_xRemoteFile.schema.mof)</span></span>

<span data-ttu-id="41c33-125">Ezenkívül használjon **Test-xDscResource** és **Test-xDscSchema** parancsmagjait [DSC erőforrás Designer](https://www.powershellgallery.com/packages/xDSCResourceDesigner/1.12.0.0) automatikusan ellenőrizhető, hogy az erőforrások és a séma:</span><span class="sxs-lookup"><span data-stu-id="41c33-125">Additionally, you should use **Test-xDscResource** and **Test-xDscSchema** cmdlets from [DSC Resource Designer](https://www.powershellgallery.com/packages/xDSCResourceDesigner/1.12.0.0) to automatically verify the resource and schema:</span></span>

```
Test-xDscResource <Resource_folder>
Test-xDscSchema <Path_to_resource_schema_file>
```

<span data-ttu-id="41c33-126">Például:</span><span class="sxs-lookup"><span data-stu-id="41c33-126">For example:</span></span>

```powershell
Test-xDscResource ..\DSCResources\MSFT_xRemoteFile
Test-xDscSchema ..\DSCResources\MSFT_xRemoteFile\MSFT_xRemoteFile.schema.mof
```

## <a name="resource-loads-without-errors"></a><span data-ttu-id="41c33-127">Hiba nélkül betölt erőforrás</span><span class="sxs-lookup"><span data-stu-id="41c33-127">Resource loads without errors</span></span>

<span data-ttu-id="41c33-128">Ellenőrizze, hogy az erőforrás-modul sikeresen tölthetők be.</span><span class="sxs-lookup"><span data-stu-id="41c33-128">Check whether the resource module can be successfully loaded.</span></span>
<span data-ttu-id="41c33-129">Ez a érhető el manuálisan a futó `Import-Module <resource_module> -force` , hogy nem lépett megerősíti, a írása és automatizált tesztelést.</span><span class="sxs-lookup"><span data-stu-id="41c33-129">This can be achieved manually, by running `Import-Module <resource_module> -force` and confirming that no errors occurred, or by writing test automation.</span></span> <span data-ttu-id="41c33-130">Az utóbbi esetén ez a struktúra a Teszteset a követheti:</span><span class="sxs-lookup"><span data-stu-id="41c33-130">In case of the latter, you can follow this structure in your test case:</span></span>

```powershell
$error = $null
Import-Module <resource_module> –force
If ($error.count –ne 0) {
    Throw “Module was not imported correctly. Errors returned: $error”
}
```

## <a name="resource-is-idempotent-in-the-positive-case"></a><span data-ttu-id="41c33-131">Erőforrás áll a pozitív esetben idempotens</span><span class="sxs-lookup"><span data-stu-id="41c33-131">Resource is idempotent in the positive case</span></span>

<span data-ttu-id="41c33-132">A DSC-erőforrások alapvető jellemzői egyik idempotencia.</span><span class="sxs-lookup"><span data-stu-id="41c33-132">One of the fundamental characteristics of DSC resources is idempotence.</span></span> <span data-ttu-id="41c33-133">Ez azt jelenti, hogy egy adott erőforrást tartalmazó többször DSC-konfiguráció alkalmazása mindig éri el a ugyanazt az eredményt.</span><span class="sxs-lookup"><span data-stu-id="41c33-133">It means that applying a DSC configuration containing that resource multiple times will always achieve the same result.</span></span> <span data-ttu-id="41c33-134">Például, ha létrehozunk egy konfigurációt, amely tartalmazza a következő fájl erőforrás:</span><span class="sxs-lookup"><span data-stu-id="41c33-134">For example, if we create a configuration which contains the following File resource:</span></span>

```powershell
File file {
    DestinationPath = "C:\test\test.txt"
    Contents = "Sample text"
}
```

<span data-ttu-id="41c33-135">Alkalmazás először, utáni fájl teszt.txt meg kell jelennie `C:\test` mappát.</span><span class="sxs-lookup"><span data-stu-id="41c33-135">After applying it for the first time, file test.txt should appear in `C:\test` folder.</span></span> <span data-ttu-id="41c33-136">Utólagosan ugyanazt a konfigurációt, azonban ne módosítsa a gép állapota (pl. nincs másolatait a `test.txt` fájlt kell létrehozni).</span><span class="sxs-lookup"><span data-stu-id="41c33-136">However, subsequent runs of the same configuration should not change the state of the machine (e.g. no copies of the `test.txt` file should be created).</span></span>
<span data-ttu-id="41c33-137">Annak biztosítása érdekében erőforrás többször is meghívhat idempotens `Set-TargetResource` közvetlenül az erőforrás ellenőrzése, vagy hívja `Start-DscConfiguration` Ha ezt többször is feldolgozza, teljes körű tesztelés.</span><span class="sxs-lookup"><span data-stu-id="41c33-137">To ensure a resource is idempotent you can repeatedly call `Set-TargetResource` when testing the resource directly, or call `Start-DscConfiguration` multiple times when doing end to end testing.</span></span> <span data-ttu-id="41c33-138">Az eredmény azonosnak kell lennie minden futtatása után.</span><span class="sxs-lookup"><span data-stu-id="41c33-138">The result should be the same after every run.</span></span>

## <a name="test-user-modification-scenario"></a><span data-ttu-id="41c33-139">Tesztkörnyezet felhasználói módosítása</span><span class="sxs-lookup"><span data-stu-id="41c33-139">Test user modification scenario</span></span>

<span data-ttu-id="41c33-140">A gép állapotát, és majd újbóli DSC, ellenőrizheti, hogy `Set-TargetResource` és `Test-TargetResource` megfelelő működéséhez.</span><span class="sxs-lookup"><span data-stu-id="41c33-140">By changing the state of the machine and then rerunning DSC, you can verify that `Set-TargetResource` and `Test-TargetResource` function properly.</span></span> <span data-ttu-id="41c33-141">Az alábbiakban a lépéseket kell tennie:</span><span class="sxs-lookup"><span data-stu-id="41c33-141">Here are steps you should take:</span></span>

1. <span data-ttu-id="41c33-142">Indítsa el az erőforrás nem a kívánt állapotban.</span><span class="sxs-lookup"><span data-stu-id="41c33-142">Start with the resource not in the desired state.</span></span>
2. <span data-ttu-id="41c33-143">Futtassa az erőforrás-konfiguráció</span><span class="sxs-lookup"><span data-stu-id="41c33-143">Run configuration with your resource</span></span>
3. <span data-ttu-id="41c33-144">Győződjön meg arról `Test-DscConfiguration` igaz értéket ad vissza</span><span class="sxs-lookup"><span data-stu-id="41c33-144">Verify `Test-DscConfiguration` returns True</span></span>
4. <span data-ttu-id="41c33-145">Módosítsa a kívánt állapotban a konfigurált cikk</span><span class="sxs-lookup"><span data-stu-id="41c33-145">Modify the configured item to be out of the desired state</span></span>
5. <span data-ttu-id="41c33-146">Győződjön meg arról `Test-DscConfiguration` false értéket adja vissza</span><span class="sxs-lookup"><span data-stu-id="41c33-146">Verify `Test-DscConfiguration` returns false</span></span>

<span data-ttu-id="41c33-147">Íme egy beállításjegyzék-erőforrást használ több konkrét példa:</span><span class="sxs-lookup"><span data-stu-id="41c33-147">Here’s a more concrete example using Registry resource:</span></span>

1. <span data-ttu-id="41c33-148">Indítsa el a rendszerleíró kulcsot nem a kívánt állapotban</span><span class="sxs-lookup"><span data-stu-id="41c33-148">Start with registry key not in the desired state</span></span>
2. <span data-ttu-id="41c33-149">Futtatás `Start-DscConfiguration` konfigurációval, a kívánt állapotban és ellenőrzi, hogy adja át.</span><span class="sxs-lookup"><span data-stu-id="41c33-149">Run `Start-DscConfiguration` with a configuration to put it in the desired state and verify it passes.</span></span>
3. <span data-ttu-id="41c33-150">Futtatás `Test-DscConfiguration` , és ellenőrizze, hogy igaz értéket ad vissza</span><span class="sxs-lookup"><span data-stu-id="41c33-150">Run `Test-DscConfiguration` and verify it returns true</span></span>
4. <span data-ttu-id="41c33-151">A kulcsnak az értéke módosíthatja, hogy nem szerepel a kívánt állapot</span><span class="sxs-lookup"><span data-stu-id="41c33-151">Modify the value of the key so that it is not in the desired state</span></span>
5. <span data-ttu-id="41c33-152">Futtatás `Test-DscConfiguration` , és ellenőrizze a hamis értéket ad vissza</span><span class="sxs-lookup"><span data-stu-id="41c33-152">Run `Test-DscConfiguration` and verify it returns false</span></span>
6. <span data-ttu-id="41c33-153">`Get-TargetResource` funkciók a rendszer ellenőrizte használatával `Get-DscConfiguration`</span><span class="sxs-lookup"><span data-stu-id="41c33-153">`Get-TargetResource` functionality was verified using `Get-DscConfiguration`</span></span>

<span data-ttu-id="41c33-154">`Get-TargetResource` az aktuális állapotát az erőforrás részleteit adja vissza.</span><span class="sxs-lookup"><span data-stu-id="41c33-154">`Get-TargetResource` should return details of the current state of the resource.</span></span> <span data-ttu-id="41c33-155">Győződjön meg arról, hogy kipróbáljuk meghívásával `Get-DscConfiguration` a konfiguráció alkalmazásához, és a gép aktuális állapotát tükröző, amely a megfelelő kimeneti ellenőrzése után.</span><span class="sxs-lookup"><span data-stu-id="41c33-155">Make sure to test it by calling `Get-DscConfiguration` after you apply the configuration and verifying that output correctly reflects the current state of the machine.</span></span> <span data-ttu-id="41c33-156">Fontos, hogy külön-külön tesztelni, mivel ez a terület esetleg felmerülő problémákat többé nem jelenik meg, hívásakor `Start-DscConfiguration`.</span><span class="sxs-lookup"><span data-stu-id="41c33-156">It's important to test it separately, since any issues in this area won't appear when calling `Start-DscConfiguration`.</span></span>

## <a name="call-getsettest-targetresource-functions-directly"></a><span data-ttu-id="41c33-157">Hívás **Get/Set/Test-TargetResource** közvetlenül függvények</span><span class="sxs-lookup"><span data-stu-id="41c33-157">Call **Get/Set/Test-TargetResource** functions directly</span></span>

<span data-ttu-id="41c33-158">Ellenőrizze, hogy tesztelje a **Get/Set/Test-TargetResource** közvetlen hívása és annak ellenőrzésére, hogy azok a várt módon működik az erőforrásban implementált függvények.</span><span class="sxs-lookup"><span data-stu-id="41c33-158">Make sure you test the **Get/Set/Test-TargetResource** functions implemented in your resource by calling them directly and verifying that they work as expected.</span></span>

## <a name="verify-end-to-end-using-start-dscconfiguration"></a><span data-ttu-id="41c33-159">Ellenőrizze a teljes körű használatával **Start-DscConfiguration**</span><span class="sxs-lookup"><span data-stu-id="41c33-159">Verify End to End using **Start-DscConfiguration**</span></span>

<span data-ttu-id="41c33-160">Tesztelés **Get/Set/Test-TargetResource** őket közvetlenül meghívásával függvények azért fontos, de ezzel a módszerrel nem minden problémák lesz felderítve.</span><span class="sxs-lookup"><span data-stu-id="41c33-160">Testing **Get/Set/Test-TargetResource** functions by calling them directly is important, but not all issues will be discovered this way.</span></span> <span data-ttu-id="41c33-161">Irányul, hogy a tesztelés használatával jelentős része `Start-DscConfiguration` vagy a lekéréses kiszolgálón.</span><span class="sxs-lookup"><span data-stu-id="41c33-161">You should focus significant part of your testing on using `Start-DscConfiguration` or the pull server.</span></span> <span data-ttu-id="41c33-162">Sőt ez a felhasználók hogyan használja az erőforrást, ezért nem alábecsülni tesztet hajt végre ilyen típusú a jelentősége.</span><span class="sxs-lookup"><span data-stu-id="41c33-162">In fact, this is how users will use the resource, so don’t underestimate the significance of this type of tests.</span></span>
<span data-ttu-id="41c33-163">Problémák lehetséges típusait:</span><span class="sxs-lookup"><span data-stu-id="41c33-163">Possible types of issues:</span></span>

- <span data-ttu-id="41c33-164">Hitelesítő adat/munkamenet előfordulhat, hogy eltérően viselkednek, mivel szolgáltatásként fut a DSC-ügynök.</span><span class="sxs-lookup"><span data-stu-id="41c33-164">Credential/Session may behave differently because the DSC agent runs as a service.</span></span>  <span data-ttu-id="41c33-165">Mindenképp tesztelje a szolgáltatásokat itt teljes körű.</span><span class="sxs-lookup"><span data-stu-id="41c33-165">Be sure to test any features here end to end.</span></span>
- <span data-ttu-id="41c33-166">Hibák kimenetét `Start-DscConfiguration` jelenik meg, ha a hívó eltérő lehet a `Set-TargetResource` függvényt közvetlenül.</span><span class="sxs-lookup"><span data-stu-id="41c33-166">Errors output by `Start-DscConfiguration` may be different than those displayed when calling the `Set-TargetResource` function directly.</span></span>

## <a name="test-compatability-on-all-dsc-supported-platforms"></a><span data-ttu-id="41c33-167">Teszt kompatibilitási minden DSC a támogatott platformok</span><span class="sxs-lookup"><span data-stu-id="41c33-167">Test compatability on all DSC supported platforms</span></span>

<span data-ttu-id="41c33-168">Erőforrás működnie kell az összes DSC támogatott platformon (Windows Server 2008 R2 és újabb).</span><span class="sxs-lookup"><span data-stu-id="41c33-168">Resource should work on all DSC supported platforms (Windows Server 2008 R2 and newer).</span></span> <span data-ttu-id="41c33-169">Telepítse a WMF legújabb Verziójára (a Windows Management Framework) az operációs rendszer DSC legújabb verziójának beszerzéséhez.</span><span class="sxs-lookup"><span data-stu-id="41c33-169">Install the latest WMF (Windows Management Framework) on your OS to get the latest version of DSC.</span></span> <span data-ttu-id="41c33-170">Ha az erőforrás nem működik egyes ezekről a platformokról elvárt, vissza kell egy adott hibaüzenetet.</span><span class="sxs-lookup"><span data-stu-id="41c33-170">If your resource does not work on some of these platforms by design, a specific error message should be returned.</span></span> <span data-ttu-id="41c33-171">Ügyeljen arra, hogy az erőforrás ellenőrzi, hogy az adott gép jelen-e parancsmagok hívja meg.</span><span class="sxs-lookup"><span data-stu-id="41c33-171">Also, make sure your resource checks whether cmdlets you are calling are present on particular machine.</span></span> <span data-ttu-id="41c33-172">A Windows Server 2012 új parancsmagok, amelyek nem érhetők el a Windows Server 2008R2, a WMF telepítése mellett is nagy számú hozzá.</span><span class="sxs-lookup"><span data-stu-id="41c33-172">Windows Server 2012 added a large number of new cmdlets that are not available on Windows Server 2008R2, even with WMF installed.</span></span>

## <a name="verify-on-windows-client-if-applicable"></a><span data-ttu-id="41c33-173">Ellenőrizze a Windows ügyfél (ha van)</span><span class="sxs-lookup"><span data-stu-id="41c33-173">Verify on Windows Client (if applicable)</span></span>

<span data-ttu-id="41c33-174">Egy nagyon gyakori teszt gap ellenőrzi az erőforrás csak a Windows server verzióit.</span><span class="sxs-lookup"><span data-stu-id="41c33-174">One very common test gap is verifying the resource only on server versions of Windows.</span></span> <span data-ttu-id="41c33-175">Sok erőforrást is tervezték, hogy működik az ügyfél SKU-k, ezért ha ez az Ön esetében igaz, ne felejtse el platformokhoz is tesztelni.</span><span class="sxs-lookup"><span data-stu-id="41c33-175">Many resources are also designed to work on Client SKUs, so if that’s true in your case, don’t forget to test it on those platforms as well.</span></span>

## <a name="get-dscresource-lists-the-resource"></a><span data-ttu-id="41c33-176">Get-DSCResource listázza az erőforrás</span><span class="sxs-lookup"><span data-stu-id="41c33-176">Get-DSCResource lists the resource</span></span>

<span data-ttu-id="41c33-177">A modul telepítése után hívása `Get-DscResource` többek között az erőforrás ezért felsorolásban szerepelnie kell.</span><span class="sxs-lookup"><span data-stu-id="41c33-177">After deploying the module, calling `Get-DscResource` should list your resource among others as a result.</span></span> <span data-ttu-id="41c33-178">Ha az erőforrás nem található a listában, ellenőrizze, hogy a schema.mof fájlt a erőforrás létezik.</span><span class="sxs-lookup"><span data-stu-id="41c33-178">If you can’t find your resource in the list, make sure that schema.mof file for that resource exists.</span></span>

## <a name="resource-module-contains-examples"></a><span data-ttu-id="41c33-179">Erőforrás-modul példákat tartalmaz</span><span class="sxs-lookup"><span data-stu-id="41c33-179">Resource module contains examples</span></span>

<span data-ttu-id="41c33-180">Mező segít másoknak létrehozása minőség példákat megtudhatja, hogyan használhatja azt.</span><span class="sxs-lookup"><span data-stu-id="41c33-180">Creating quality examples which will help others understand how to use it.</span></span> <span data-ttu-id="41c33-181">Ez különösen fontos, különösen, mivel sok felhasználó mintakód gyökérkönyvtárral dokumentációját.</span><span class="sxs-lookup"><span data-stu-id="41c33-181">This is crucial, especially since many users treat sample code as documentation.</span></span>

- <span data-ttu-id="41c33-182">Először döntse el, hogy a modul – legalább tartalmazni fogja a bemutatott példákat, ki kell terjednie az erőforrás legfontosabb alkalmazási helyzetek:</span><span class="sxs-lookup"><span data-stu-id="41c33-182">First, you should determine the examples that will be included with the module – at minimum, you should cover most important use cases for your resource:</span></span>
- <span data-ttu-id="41c33-183">Ha a modul számos olyan erőforrásokat tartalmaz, egy végpontok közötti forgatókönyv működjön együtt van szükség, az alapszintű teljes körű ideális esetben lehet például első.</span><span class="sxs-lookup"><span data-stu-id="41c33-183">If your module contains several resources that need to work together for an end-to-end scenario, the basic end-to-end example would ideally be first.</span></span>
- <span data-ttu-id="41c33-184">Lehet, hogy a kezdeti példák nagyon egyszerű – az erőforrások (pl. létrehozásakor egy új virtuális merevlemez) kis méretű kezelhető tömbökben az első lépések</span><span class="sxs-lookup"><span data-stu-id="41c33-184">The initial examples should be very simple -- how to get started with your resources in small manageable chunks (e.g. creating a new VHD)</span></span>
- <span data-ttu-id="41c33-185">További példák kell, ezek példák (például egy virtuális gép létrehozása virtuális merevlemezből, eltávolítja a virtuális gép, virtuális gép módosítása) buildet, és összetettebb funkciók (például egy virtuális gép létrehozása a dinamikus memória) megjelenítése</span><span class="sxs-lookup"><span data-stu-id="41c33-185">Subsequent examples should build on those examples (e.g. creating a VM from a VHD, removing VM, modifying VM), and show advanced functionality (e.g. creating a VM with dynamic memory)</span></span>
- <span data-ttu-id="41c33-186">Érdemes lehet paraméterezni, például konfigurációk (összes értéket kell átadni a konfigurációhoz meg paraméterként, és nincsenek nem változtatható értékek kell lennie):</span><span class="sxs-lookup"><span data-stu-id="41c33-186">Example configurations should be parameterized (all values should be passed to the configuration as parameters and there should be no hardcoded values):</span></span>

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

- <span data-ttu-id="41c33-187">Tanácsos hogyan hívhat meg a konfiguráció a példa parancsfájl végén található tényleges értékkel (megjegyzésekkel ki) példa tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="41c33-187">It’s a good practice to include (commented out) example of how to call the configuration with the actual values at the end of the example script.</span></span>
  <span data-ttu-id="41c33-188">Ha például a fenti konfigurációban nem feltétlenül nyilvánvaló, hogy van-e a legjobb módszer UserAgent adja meg:</span><span class="sxs-lookup"><span data-stu-id="41c33-188">For example, in the configuration above it isn't necessarily obvious that the best way to specify UserAgent is:</span></span>

  <span data-ttu-id="41c33-189">`UserAgent = [Microsoft.PowerShell.Commands.PSUserAgent]::InternetExplorer` Ebben az esetben egy megjegyzést a konfiguráció a tervezett végrehajtási jól átláthatók:</span><span class="sxs-lookup"><span data-stu-id="41c33-189">`UserAgent = [Microsoft.PowerShell.Commands.PSUserAgent]::InternetExplorer` In which case a comment can clarify the intended execution of the configuration:</span></span>

  ```powershell
  <#
  Sample use (parameter values need to be changed according to your scenario):

  Sample_xRemoteFile_DownloadFile -destinationPath "$env:SystemDrive\fileName.jpg" -uri "http://www.contoso.com/image.jpg"

  Sample_xRemoteFile_DownloadFile -destinationPath "$env:SystemDrive\fileName.jpg" -uri "http://www.contoso.com/image.jpg" `
  -userAgent [Microsoft.PowerShell.Commands.PSUserAgent]::InternetExplorer -headers @{"Accept-Language" = "en-US"}
  #>
  ```

- <span data-ttu-id="41c33-190">Minden egyes például írjon egy rövid leírást, amely bemutatja, mire használható, és a paraméterek jelentése.</span><span class="sxs-lookup"><span data-stu-id="41c33-190">For each example, write a short description which explains what it does, and the meaning of the parameters.</span></span>
- <span data-ttu-id="41c33-191">Ellenőrizze, hogy az erőforrás fontos a legtöbb forgatókönyvre példákat, és ha semmit nem hiányzik, ellenőrizze, hogy az összes végrehajtás, és helyezze a gép a kívánt állapotban.</span><span class="sxs-lookup"><span data-stu-id="41c33-191">Make sure examples cover most the important scenarios for your resource and if there’s nothing missing, verify that they all execute and put machine in the desired state.</span></span>

## <a name="error-messages-are-easy-to-understand-and-help-users-solve-problems"></a><span data-ttu-id="41c33-192">Hibaüzenetek a következők így könnyen megismerhető és segítség a felhasználóknak a problémák megoldása</span><span class="sxs-lookup"><span data-stu-id="41c33-192">Error messages are easy to understand and help users solve problems</span></span>

<span data-ttu-id="41c33-193">Lesz helyes hibaüzenetek:</span><span class="sxs-lookup"><span data-stu-id="41c33-193">Good error messages should be:</span></span>

- <span data-ttu-id="41c33-194">Hiba: Hibaüzenetek legnagyobb problémája, hogy azok milyen gyakran nem létezik, ezért ügyeljen arra, hogy vannak-e.</span><span class="sxs-lookup"><span data-stu-id="41c33-194">There: The biggest problem with error messages is that they often don’t exist, so make sure they are there.</span></span>
- <span data-ttu-id="41c33-195">Könnyen áttekinthető: Emberi olvasható, nem homályos hibakódok</span><span class="sxs-lookup"><span data-stu-id="41c33-195">Easy to understand: Human readable, no obscure error codes</span></span>
- <span data-ttu-id="41c33-196">Pontos: Mi az, hogy pontosan a probléma leírása</span><span class="sxs-lookup"><span data-stu-id="41c33-196">Precise: Describe what’s exactly the problem</span></span>
- <span data-ttu-id="41c33-197">Vélelmezett: Tanácsadás a probléma megoldása</span><span class="sxs-lookup"><span data-stu-id="41c33-197">Constructive: Advice how to fix the issue</span></span>
- <span data-ttu-id="41c33-198">Udvarias: Nem felhasználó blame vagy őket úgy hibás</span><span class="sxs-lookup"><span data-stu-id="41c33-198">Polite: Don’t blame user or make them feel bad</span></span>

<span data-ttu-id="41c33-199">Győződjön meg arról, ellenőrizze, hogy a végpontok közötti forgatókönyvek hibákat (használatával `Start-DscConfiguration`), mert előfordulhat, hogy különböznek azoktól, akik közvetlenül erőforrásfüggvények futtatásakor kapott.</span><span class="sxs-lookup"><span data-stu-id="41c33-199">Make sure you verify errors in End to End scenarios (using `Start-DscConfiguration`), because they may differ from those returned when running resource functions directly.</span></span>

## <a name="log-messages-are-easy-to-understand-and-informative-including-verbose-debug-and-etw-logs"></a><span data-ttu-id="41c33-200">Naplóüzenetek, könnyen érthető és informatív (beleértve a – részletes, – hibakeresési és ETW-naplók)</span><span class="sxs-lookup"><span data-stu-id="41c33-200">Log messages are easy to understand and informative (including –verbose, –debug and ETW logs)</span></span>

<span data-ttu-id="41c33-201">Győződjön meg arról, hogy az erőforrás által használt kimeneti adattípus naplók elsajátítása, és adjon meg értéket a felhasználóhoz.</span><span class="sxs-lookup"><span data-stu-id="41c33-201">Ensure that logs outputted by the resource are easy to understand and provide value to the user.</span></span> <span data-ttu-id="41c33-202">Erőforrások jeleníti meg minden olyan információt, amely a felhasználó számára hasznos lehet, de további naplók nem mindig jobb.</span><span class="sxs-lookup"><span data-stu-id="41c33-202">Resources should output all information which might be helpful to the user, but more logs is not always better.</span></span> <span data-ttu-id="41c33-203">Érdemes elkerülése érdekében a redundancia és a ad ki adatokat, amelyek nem adja meg a további értékek – ne valaki naplóbejegyzések több száz hajtania annak érdekében, hogy találja, amit keresnek.</span><span class="sxs-lookup"><span data-stu-id="41c33-203">You should avoid redundancy and outputting data which does not provide additional value – don’t make someone go through hundreds of log entries in order to find what they're looking for.</span></span> <span data-ttu-id="41c33-204">Természetesen nincs napló nem az elfogadható megoldás a probléma vagy.</span><span class="sxs-lookup"><span data-stu-id="41c33-204">Of course, no logs is not an acceptable solution for this problem either.</span></span>

<span data-ttu-id="41c33-205">Tesztelésekor, emellett részletes elemzését és hibakeresési naplók (futtatásával `Start-DscConfiguration` a `–Verbose` és `–Debug` vált megfelelően), illetve ETW-naplók formájában.</span><span class="sxs-lookup"><span data-stu-id="41c33-205">When testing, you should also analyze verbose and debug logs (by running `Start-DscConfiguration` with `–Verbose` and `–Debug` switches appropriately), as well as ETW logs.</span></span> <span data-ttu-id="41c33-206">DSC ETW-naplók megtekintéséhez nyissa meg az eseménynaplót, és nyissa meg a következő mappát: Alkalmazások és szolgáltatások – Microsoft - Windows - Desired State Configuration.</span><span class="sxs-lookup"><span data-stu-id="41c33-206">To see DSC ETW logs, go to Event Viewer and open the following folder: Applications and Services- Microsoft - Windows - Desired State Configuration.</span></span>  <span data-ttu-id="41c33-207">Alapértelmezés szerint nincs fog műveleti csatorna lehet, de ellenőrizze, hogy engedélyezi a elemzési és hibakeresési csatornák a konfiguráció futtatása előtt.</span><span class="sxs-lookup"><span data-stu-id="41c33-207">By default there will be Operational channel, but make sure you enable Analytic and Debug channels before running the configuration.</span></span>
<span data-ttu-id="41c33-208">Engedélyezi az elemzési és hibakeresési csatornák, hajtsa végre az alábbi parancsfájlt:</span><span class="sxs-lookup"><span data-stu-id="41c33-208">To enable Analytic/Debug channels, you can execute script below:</span></span>

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

## <a name="resource-implementation-does-not-contain-hardcoded-paths"></a><span data-ttu-id="41c33-209">Erőforrás-implementáció nem tartalmaz szoftveresen kötött elérési utak</span><span class="sxs-lookup"><span data-stu-id="41c33-209">Resource implementation does not contain hardcoded paths</span></span>

<span data-ttu-id="41c33-210">Győződjön meg, hogy nincsenek szoftveresen kötött elérési utak erőforrás végrehajtásában, különösen akkor, ha a nyelvi azt feltételezik (en-us), vagy ha rendszerváltozók használható.</span><span class="sxs-lookup"><span data-stu-id="41c33-210">Ensure there are no hardcoded paths in the resource implementation, particularly if they assume language (en-us), or when there are system variables that can be used.</span></span>
<span data-ttu-id="41c33-211">Ha az erőforrás eléréséhez egyedi elérési utak, a környezeti változók használata helyett hardcoding kell az elérési út, ahogy más gépeken eltérő lehet.</span><span class="sxs-lookup"><span data-stu-id="41c33-211">If your resource need to access specific paths, use environment variables instead of hardcoding the path, as it may differ on other machines.</span></span>

<span data-ttu-id="41c33-212">Példa:</span><span class="sxs-lookup"><span data-stu-id="41c33-212">Example:</span></span>

<span data-ttu-id="41c33-213">ahelyett, hogy:</span><span class="sxs-lookup"><span data-stu-id="41c33-213">Instead of:</span></span>

```powershell
$tempPath = "C:\Users\kkaczma\AppData\Local\Temp\MyResource"
$programFilesPath = "C:\Program Files (x86)"
```

<span data-ttu-id="41c33-214">Írhat:</span><span class="sxs-lookup"><span data-stu-id="41c33-214">You can write:</span></span>

```powershell
$tempPath = Join-Path $env:temp "MyResource"
$programFilesPath = ${env:ProgramFiles(x86)}
```

## <a name="resource-implementation-does-not-contain-user-information"></a><span data-ttu-id="41c33-215">Erőforrás-implementáció nem tartalmaz felhasználói adatokat</span><span class="sxs-lookup"><span data-stu-id="41c33-215">Resource implementation does not contain user information</span></span>

<span data-ttu-id="41c33-216">Ellenőrizze, hogy nincsenek e-mail neveket, fiók adatait, vagy a kódban személyek nevét.</span><span class="sxs-lookup"><span data-stu-id="41c33-216">Make sure there are no email names, account information, or names of people in the code.</span></span>

## <a name="resource-was-tested-with-validinvalid-credentials"></a><span data-ttu-id="41c33-217">Erőforrás teszteltük érvényes/érvénytelen hitelesítő adatok</span><span class="sxs-lookup"><span data-stu-id="41c33-217">Resource was tested with valid/invalid credentials</span></span>

<span data-ttu-id="41c33-218">Ha az erőforrás paraméterként vesz igénybe egy hitelesítő adatot:</span><span class="sxs-lookup"><span data-stu-id="41c33-218">If your resource takes a credential as parameter:</span></span>

- <span data-ttu-id="41c33-219">Ellenőrizze az erőforrás működését, amikor a helyi rendszer (vagy távoli erőforrásokhoz tartozó számítógépfiók) nem rendelkezik hozzáféréssel.</span><span class="sxs-lookup"><span data-stu-id="41c33-219">Verify the resource works when Local System (or the computer account for remote resources) does not have access.</span></span>
- <span data-ttu-id="41c33-220">Ellenőrizze az erőforrás működik a megadott hitelesítő adatok Get, Set és tesztelése</span><span class="sxs-lookup"><span data-stu-id="41c33-220">Verify the resource works with a credential specified for Get, Set and Test</span></span>
- <span data-ttu-id="41c33-221">Ha az erőforráshoz fér hozzá a megosztásokat, teszteléséhez szüksége támogatásra, mint például variantní hodnoty:</span><span class="sxs-lookup"><span data-stu-id="41c33-221">If your resource accesses shares, test all the variants you need to support, such as:</span></span>
  - <span data-ttu-id="41c33-222">Szabványos windows-megosztásokat.</span><span class="sxs-lookup"><span data-stu-id="41c33-222">Standard windows shares.</span></span>
  - <span data-ttu-id="41c33-223">Elosztott fájlrendszer-megosztásokat.</span><span class="sxs-lookup"><span data-stu-id="41c33-223">DFS shares.</span></span>
  - <span data-ttu-id="41c33-224">SAMBA megosztások (Ha szeretne Linux támogatja.)</span><span class="sxs-lookup"><span data-stu-id="41c33-224">SAMBA shares (if you want to support Linux.)</span></span>

## <a name="resource-does-not-require-interactive-input"></a><span data-ttu-id="41c33-225">Erőforrás nem igényel interaktív bemenet</span><span class="sxs-lookup"><span data-stu-id="41c33-225">Resource does not require interactive input</span></span>

<span data-ttu-id="41c33-226">**Get/Set/Test-TargetResource** függvények automatikusan hajtható végre, és nem kell megvárja, hogy felhasználói bevitel végrehajtási bármely szakaszában (pl. ne használjon `Get-Credential` ezek a függvények belül).</span><span class="sxs-lookup"><span data-stu-id="41c33-226">**Get/Set/Test-TargetResource** functions should be executed automatically and must not wait for user’s input at any stage of execution (e.g. you should not use `Get-Credential` inside these functions).</span></span> <span data-ttu-id="41c33-227">Ha meg kell adnia a felhasználói bevitel, meg kell adja át azt a konfigurációs paraméterként a fordítási fázis során.</span><span class="sxs-lookup"><span data-stu-id="41c33-227">If you need to provide user’s input, you should pass it to the configuration as parameter during the compilation phase.</span></span>

## <a name="resource-functionality-was-thoroughly-tested"></a><span data-ttu-id="41c33-228">Erőforrás-funkciókat alaposan tesztelés</span><span class="sxs-lookup"><span data-stu-id="41c33-228">Resource functionality was thoroughly tested</span></span>

<span data-ttu-id="41c33-229">Ezzel az ellenőrzőlistával elemek, amelyek fontosak, tesztelését és/vagy gyakran vannak-e elmulasztott tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="41c33-229">This checklist contains items which are important to be tested and/or are often missed.</span></span> <span data-ttu-id="41c33-230">Többféle teszteket, elsősorban olyan működési azokat, amely jellemző az erőforrás éppen tesztel, és nem szerepelnek itt lesz.</span><span class="sxs-lookup"><span data-stu-id="41c33-230">There will be bunch of tests, mainly functional ones which will be specific to the resource you are testing and are not mentioned here.</span></span> <span data-ttu-id="41c33-231">Ne felejtse el kapcsolatos negatív vizsgálati eset.</span><span class="sxs-lookup"><span data-stu-id="41c33-231">Don’t forget about negative test cases.</span></span>

## <a name="best-practice-resource-module-contains-tests-folder-with-resourcedesignertestsps1-script"></a><span data-ttu-id="41c33-232">Ajánlott eljárás: Resource modul tesztek mappát ResourceDesignerTests.ps1 szkript tartalmaz</span><span class="sxs-lookup"><span data-stu-id="41c33-232">Best practice: Resource module contains Tests folder with ResourceDesignerTests.ps1 script</span></span>

<span data-ttu-id="41c33-233">A mappa "teszt" resource modul belül létrehozásához hozzon létre egy célszerű `ResourceDesignerTests.ps1` fájlt, és adja hozzá a tesztek segítségével **Test-xDscResource** és **Test-xDscSchema** található összes erőforrást a megadott modul.</span><span class="sxs-lookup"><span data-stu-id="41c33-233">It’s a good practice to create folder “Tests” inside resource module, create `ResourceDesignerTests.ps1` file and add tests using **Test-xDscResource** and **Test-xDscSchema** for all resources in given module.</span></span>
<span data-ttu-id="41c33-234">Így gyorsan ellenőrizheti az adott modulok és a megerősítést a közzététel előtt ellenőrizze az összes erőforrás sémák.</span><span class="sxs-lookup"><span data-stu-id="41c33-234">This way you can quickly validate schemas of all resources from the given modules and do a sanity check before publishing.</span></span>
<span data-ttu-id="41c33-235">A xRemoteFile `ResourceTests.ps1` rákeresve beállítható:</span><span class="sxs-lookup"><span data-stu-id="41c33-235">For xRemoteFile, `ResourceTests.ps1` could look as simple as:</span></span>

```powershell
Test-xDscResource ..\DSCResources\MSFT_xRemoteFile
Test-xDscSchema ..\DSCResources\MSFT_xRemoteFile\MSFT_xRemoteFile.schema.mof
```

## <a name="best-practice-resource-folder-contains-resource-designer-script-for-generating-schema"></a><span data-ttu-id="41c33-236">Ajánlott eljárás: Erőforrás mappa tartalmazza az erőforrás a Tervező parancsfájlját a séma generálásához</span><span class="sxs-lookup"><span data-stu-id="41c33-236">Best practice: Resource folder contains resource designer script for generating schema</span></span>

<span data-ttu-id="41c33-237">Az egyes erőforrások tartalmaznia kell egy erőforrás tervező parancsfájlt, amely az erőforrás mof sémát hoz létre.</span><span class="sxs-lookup"><span data-stu-id="41c33-237">Each resource should contain a resource designer script which generates a mof schema of the resource.</span></span> <span data-ttu-id="41c33-238">Ezt a fájlt kell elhelyezni a `<ResourceName>\ResourceDesignerScripts` Generate neve lehet, és `<ResourceName>Schema.ps1` xRemoteFile erőforrás ezt a fájlt hívható `GenerateXRemoteFileSchema.ps1` és tartalmaznak:</span><span class="sxs-lookup"><span data-stu-id="41c33-238">This file should be placed in `<ResourceName>\ResourceDesignerScripts` and be named Generate `<ResourceName>Schema.ps1` For xRemoteFile resource this file would be called `GenerateXRemoteFileSchema.ps1` and contain:</span></span>

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

## <a name="best-practice-resource-supports--whatif"></a><span data-ttu-id="41c33-239">Ajánlott eljárás: Erőforrás - WhatIf támogatja</span><span class="sxs-lookup"><span data-stu-id="41c33-239">Best practice: Resource supports -WhatIf</span></span>

<span data-ttu-id="41c33-240">Az erőforrás "veszélyes" műveleteket hajt végre, ha tanácsos megvalósítása `-WhatIf` funkciót.</span><span class="sxs-lookup"><span data-stu-id="41c33-240">If your resource is performing “dangerous” operations, it’s a good practice to implement `-WhatIf` functionality.</span></span> <span data-ttu-id="41c33-241">Miután elkészült, győződjön meg arról, hogy `-WhatIf` kimeneti megfelelően leírja a műveleteit, amely történne a parancs végrehajtása történt nélkül `-WhatIf` váltani.</span><span class="sxs-lookup"><span data-stu-id="41c33-241">After it’s done, make sure that `-WhatIf` output correctly describes operations which would happen if command was executed without `-WhatIf` switch.</span></span>
<span data-ttu-id="41c33-242">Azt is ellenőrizze, hogy a művelet nem futtatható (nem az a csomópont állapota módosul) Ha `–WhatIf` kapcsoló használata.</span><span class="sxs-lookup"><span data-stu-id="41c33-242">Also, verify that operations does not execute (no changes to the node’s state are made) when `–WhatIf` switch is present.</span></span>
<span data-ttu-id="41c33-243">Például tegyük fel, File erőforrás azt teszteli.</span><span class="sxs-lookup"><span data-stu-id="41c33-243">For example, let’s assume we are testing File resource.</span></span> <span data-ttu-id="41c33-244">Az alábbi, az egyszerű konfigurációs fájlt hoz létre, amely `test.txt` "test" tartalma:</span><span class="sxs-lookup"><span data-stu-id="41c33-244">Below is simple configuration which creates file `test.txt` with contents “test”:</span></span>

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

<span data-ttu-id="41c33-245">Ha azt fordítsa le és majd futtassa a konfiguráció a `-WhatIf` kapcsoló, a kimeneti eredménytelen pontosan mi lenne fordulhat elő, ha futtatjuk a konfigurációt.</span><span class="sxs-lookup"><span data-stu-id="41c33-245">If we compile and then execute the configuration with the `-WhatIf` switch, the output is telling us exactly what would happen when we run the configuration.</span></span> <span data-ttu-id="41c33-246">Maga a konfiguráció azonban nem lett végrehajtva (`test.txt` fájl nem jött létre).</span><span class="sxs-lookup"><span data-stu-id="41c33-246">The configuration itself however was not executed (`test.txt` file was not created).</span></span>

```powershell
Start-DscConfiguration -Path .\config -ComputerName localhost -Wait -Verbose -WhatIf
```

```output
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

<span data-ttu-id="41c33-247">Ez a lista tehát nem tekinthető teljesnek, de számos fontos problémák megtervezése, fejlesztése és tesztelése a DSC-erőforrások is történt, amely lefedi.</span><span class="sxs-lookup"><span data-stu-id="41c33-247">This list is not exhaustive, but it covers many important issues which can be encountered while designing, developing and testing DSC resources.</span></span>
