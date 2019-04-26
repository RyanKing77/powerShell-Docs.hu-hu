---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: WMF, powershell, beállítás
title: Új forgatókönyvek és funkciók a WMF 5.1
ms.openlocfilehash: b00069aad7422f86d1462a62a6c4bc8a91e46705
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62085454"
---
# <a name="new-scenarios-and-features-in-wmf-51"></a><span data-ttu-id="3ba8c-103">Új forgatókönyvek és funkciók a WMF 5.1</span><span class="sxs-lookup"><span data-stu-id="3ba8c-103">New Scenarios and Features in WMF 5.1</span></span>

> <span data-ttu-id="3ba8c-104">Megjegyzés: Ezek az információk előzetesek, és változhat a tartalmuk.</span><span class="sxs-lookup"><span data-stu-id="3ba8c-104">Note: This information is preliminary and subject to change.</span></span>

## <a name="powershell-editions"></a><span data-ttu-id="3ba8c-105">PowerShell-kiadások</span><span class="sxs-lookup"><span data-stu-id="3ba8c-105">PowerShell Editions</span></span>

<span data-ttu-id="3ba8c-106">Az 5.1-es verziótól kezdődően a PowerShell különböző kiadásokban érhető el, amelyek különböző szolgáltatáskészleteket és platformkompatibilitást kínálnak.</span><span class="sxs-lookup"><span data-stu-id="3ba8c-106">Starting with version 5.1, PowerShell is available in different editions which denote varying feature sets and platform compatibility.</span></span>

- <span data-ttu-id="3ba8c-107">**Desktop kiadás:** .NET-keretrendszer épül, és kompatibilis a Windows például a Server Core és a Windows asztal teljes erőforrás-igényű kiadásain fut PowerShell-verziókat célzó szkriptekhez és modulokhoz biztosít.</span><span class="sxs-lookup"><span data-stu-id="3ba8c-107">**Desktop Edition:** Built on .NET Framework and provides compatibility with scripts and modules targeting versions of PowerShell running on full footprint editions of Windows such as Server Core and Windows Desktop.</span></span>
- <span data-ttu-id="3ba8c-108">**Core kiadás:** .NET Core épül, és kompatibilis csökkentett erőforrás-igényű kiadása esetén például a Nano Server Windows és Windows IoT kiadásokon futtatott PowerShell-verziókat célzó szkriptekhez és modulokhoz biztosít.</span><span class="sxs-lookup"><span data-stu-id="3ba8c-108">**Core Edition:** Built on .NET Core and provides compatibility with scripts and modules targeting versions of PowerShell running on reduced footprint editions of Windows such as Nano Server and Windows IoT.</span></span>

<span data-ttu-id="3ba8c-109">**További tudnivalók a PowerShell-kiadások használatával**</span><span class="sxs-lookup"><span data-stu-id="3ba8c-109">**Learn more about using PowerShell Editions**</span></span>

- [<span data-ttu-id="3ba8c-110">Határozza meg a PowerShell használatával $PSVersionTable futó kiadása</span><span class="sxs-lookup"><span data-stu-id="3ba8c-110">Determine running edition of PowerShell using $PSVersionTable</span></span>](/powershell/module/microsoft.powershell.core/about/about_automatic_variables)
- [<span data-ttu-id="3ba8c-111">Get-Module eredmények által PSEdition paraméterrel CompatiblePSEditions szűrése</span><span class="sxs-lookup"><span data-stu-id="3ba8c-111">Filter Get-Module results by CompatiblePSEditions using PSEdition parameter</span></span>](/powershell/module/microsoft.powershell.core/get-module)
- [<span data-ttu-id="3ba8c-112">Parancsfájl végrehajtása megakadályozása, ha a PowerShell kompatibilis kiadásán futtatása</span><span class="sxs-lookup"><span data-stu-id="3ba8c-112">Prevent script execution unless run on a compatible edition of PowerShell</span></span>](/powershell/gallery/concepts/script-psedition-support)
- [<span data-ttu-id="3ba8c-113">Deklarálja a verziókkal PowerShell-modul kompatibilitás</span><span class="sxs-lookup"><span data-stu-id="3ba8c-113">Declare a module's compatibility to specific PowerShell versions</span></span>](/powershell/gallery/concepts/module-psedition-support)

## <a name="catalog-cmdlets"></a><span data-ttu-id="3ba8c-114">Katalógusbeli parancsmagok</span><span class="sxs-lookup"><span data-stu-id="3ba8c-114">Catalog Cmdlets</span></span>

<span data-ttu-id="3ba8c-115">Két új parancsmagot a lettek hozzáadva a [Microsoft.PowerShell.Security](/powershell/module/microsoft.powershell.security) modul; ezek létrehozása és a Windows katalógusban fájlok érvényesítése.</span><span class="sxs-lookup"><span data-stu-id="3ba8c-115">Two new cmdlets have been added in the [Microsoft.PowerShell.Security](/powershell/module/microsoft.powershell.security) module; these generate and validate Windows catalog files.</span></span>

### <a name="new-filecatalog"></a><span data-ttu-id="3ba8c-116">New-FileCatalog</span><span class="sxs-lookup"><span data-stu-id="3ba8c-116">New-FileCatalog</span></span>
--------------------------------

<span data-ttu-id="3ba8c-117">Új FileCatalog fájlt hoz létre Windows catalog az tartozó fájlokat és mappákat.</span><span class="sxs-lookup"><span data-stu-id="3ba8c-117">New-FileCatalog creates a Windows catalog file for set of folders and files.</span></span>
<span data-ttu-id="3ba8c-118">A katalógus-fájl tartalmazza az összes fájl megadott elérési utak a kivonatok.</span><span class="sxs-lookup"><span data-stu-id="3ba8c-118">This catalog file contains hashes for all files in specified paths.</span></span>
<span data-ttu-id="3ba8c-119">Jelölő mappákat megfelelő katalógusfájlt együtt mappakészlet terjeszthetnek.</span><span class="sxs-lookup"><span data-stu-id="3ba8c-119">Users can distribute the set of folders along with corresponding catalog file representing those folders.</span></span>
<span data-ttu-id="3ba8c-120">Ez az információ hasznos megállapítani, hogy e bármely módosultak a mappák katalógus létrehozása óta.</span><span class="sxs-lookup"><span data-stu-id="3ba8c-120">This information is useful to validate whether any changes have been made to the folders since catalog creation time.</span></span>

```powershell
New-FileCatalog [-CatalogFilePath] <string> [[-Path] <string[]>] [-CatalogVersion <int>] [-WhatIf] [-Confirm] [<CommonParameters>]
```

<span data-ttu-id="3ba8c-121">1. és 2 katalógus verziók támogatottak.</span><span class="sxs-lookup"><span data-stu-id="3ba8c-121">Catalog versions 1 and 2 are supported.</span></span>
<span data-ttu-id="3ba8c-122">1. verzió az SHA1 kivonatoló algoritmus segítségével hozza létre a fájlkivonat; 2. verzió SHA256 titkosítást használ.</span><span class="sxs-lookup"><span data-stu-id="3ba8c-122">Version 1 uses the SHA1 hashing algorithm to create file hashes; version 2 uses SHA256.</span></span>
<span data-ttu-id="3ba8c-123">Katalógus 2-es verzió nem támogatott az *Windows Server 2008 R2* vagy *Windows 7*.</span><span class="sxs-lookup"><span data-stu-id="3ba8c-123">Catalog version 2 is not supported on *Windows Server 2008 R2* or *Windows 7*.</span></span>
<span data-ttu-id="3ba8c-124">A katalógus 2-es verziójú használjon *Windows 8*, *Windows Server 2012*, és annál újabb operációs rendszereken.</span><span class="sxs-lookup"><span data-stu-id="3ba8c-124">You should use catalog version 2 on *Windows 8*, *Windows Server 2012*, and later operating systems.</span></span>

![](../images/NewFileCatalog.jpg)

<span data-ttu-id="3ba8c-125">Ez a katalógus fájlt hoz létre.</span><span class="sxs-lookup"><span data-stu-id="3ba8c-125">This creates the catalog file.</span></span>

![](../images/CatalogFile1.jpg)

![](../images/CatalogFile2.jpg)

<span data-ttu-id="3ba8c-126">A katalógus fájlt (Pester.cat a fenti példában) sértetlenségének ellenőrzése használatával írja alá [Set-AuthenticodeSignature](/powershell/module/Microsoft.PowerShell.Security/Set-AuthenticodeSignature) parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="3ba8c-126">To verify the integrity of catalog file (Pester.cat in above example), sign it using [Set-AuthenticodeSignature](/powershell/module/Microsoft.PowerShell.Security/Set-AuthenticodeSignature) cmdlet.</span></span>

### <a name="test-filecatalog"></a><span data-ttu-id="3ba8c-127">Test-FileCatalog</span><span class="sxs-lookup"><span data-stu-id="3ba8c-127">Test-FileCatalog</span></span>
--------------------------------

<span data-ttu-id="3ba8c-128">Test-FileCatalog érvényesíti a katalógus jelölő mappákat.</span><span class="sxs-lookup"><span data-stu-id="3ba8c-128">Test-FileCatalog validates the catalog representing a set of folders.</span></span>

```powershell
Test-FileCatalog [-CatalogFilePath] <string> [[-Path] <string[]>] [-Detailed] [-FilesToSkip <string[]>] [-WhatIf] [-Confirm] [<CommonParameters>]
```

![](../images/TestFileCatalog.jpg)

<span data-ttu-id="3ba8c-129">Ez a parancsmag a fájlok-kivonatok hasonlítja össze, és azok relatív elérési utakat található *katalógus* együtt megjelennek a *lemez*.</span><span class="sxs-lookup"><span data-stu-id="3ba8c-129">This cmdlet compares all the files hashes and their relative paths found in *catalog* with ones on *disk*.</span></span>
<span data-ttu-id="3ba8c-130">Ha azt észleli, hogy bármely fájlkivonatokkal és elérési utak nem egyezik, adja vissza, az állapot *ValidationFailed*.</span><span class="sxs-lookup"><span data-stu-id="3ba8c-130">If it detects any mismatch between file hashes and paths it returns the status as *ValidationFailed*.</span></span>
<span data-ttu-id="3ba8c-131">Felhasználók használatával lekérhető ezt az információt a *– részletes* paraméter.</span><span class="sxs-lookup"><span data-stu-id="3ba8c-131">Users can retrieve all this information by using the *-Detailed* parameter.</span></span>
<span data-ttu-id="3ba8c-132">A katalógus aláíró állapotát is megjeleníti *aláírás* tulajdonság, amely egyenértékű hívása [Get-AuthenticodeSignature](/powershell/module/Microsoft.PowerShell.Security/Get-AuthenticodeSignature) katalógusfájl parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="3ba8c-132">It also displays signing status of catalog in *Signature* property which is equivalent to calling [Get-AuthenticodeSignature](/powershell/module/Microsoft.PowerShell.Security/Get-AuthenticodeSignature) cmdlet on the catalog file.</span></span>
<span data-ttu-id="3ba8c-133">Felhasználók ki is hagyhatja bármely fájl ellenőrzésekor használatával a *- FilesToSkip* paraméter.</span><span class="sxs-lookup"><span data-stu-id="3ba8c-133">Users can also skip any file during validation by using the *-FilesToSkip* parameter.</span></span>

## <a name="module-analysis-cache"></a><span data-ttu-id="3ba8c-134">A modul elemzési gyorsítótár</span><span class="sxs-lookup"><span data-stu-id="3ba8c-134">Module Analysis Cache</span></span>

<span data-ttu-id="3ba8c-135">A WMF 5.1-es verziótól kezdődően PowerShell segítségével szabályozhatja, a fájl, amellyel egy modult, exportálja a parancsok például a gyorsítótár adatait.</span><span class="sxs-lookup"><span data-stu-id="3ba8c-135">Starting with WMF 5.1, PowerShell provides control over the file that is used to cache data about a module, such as the commands it exports.</span></span>

<span data-ttu-id="3ba8c-136">Alapértelmezés szerint ez a gyorsítótár a fájlban tárolt `${env:LOCALAPPDATA}\Microsoft\Windows\PowerShell\ModuleAnalysisCache`.</span><span class="sxs-lookup"><span data-stu-id="3ba8c-136">By default, this cache is stored in the file `${env:LOCALAPPDATA}\Microsoft\Windows\PowerShell\ModuleAnalysisCache`.</span></span>
<span data-ttu-id="3ba8c-137">A gyorsítótár egy parancs keresése közben általában olvasható indításkor, és íródik a háttérbeli szálon némi várakozás után egy modul importálása kész.</span><span class="sxs-lookup"><span data-stu-id="3ba8c-137">The cache is typically read at startup while searching for a command and is written on a background thread sometime after a module is imported.</span></span>

<span data-ttu-id="3ba8c-138">Ha módosítani szeretné az alapértelmezett hely a gyorsítótár, állítsa be a `$env:PSModuleAnalysisCachePath` környezeti változót a PowerShell indítása előtt.</span><span class="sxs-lookup"><span data-stu-id="3ba8c-138">To change the default location of the cache, set the `$env:PSModuleAnalysisCachePath` environment variable before starting PowerShell.</span></span>
<span data-ttu-id="3ba8c-139">Ez a környezeti változó módosításai csak hatással lesz a gyermekek folyamatokat.</span><span class="sxs-lookup"><span data-stu-id="3ba8c-139">Changes to this environment variable will only affect children processes.</span></span>
<span data-ttu-id="3ba8c-140">Az érték teljes elérési utat (például fájlnév), amely PowerShell jogosult hozhat létre és írhat fájlokat kell neve.</span><span class="sxs-lookup"><span data-stu-id="3ba8c-140">The value should name a full path (including filename) that PowerShell has permission to create and write files.</span></span>
<span data-ttu-id="3ba8c-141">A fájlgyorsítótárban letiltásához állítsa be ezt az értéket érvénytelen helyre, például:</span><span class="sxs-lookup"><span data-stu-id="3ba8c-141">To disable the file cache, set this value to an invalid location, for example:</span></span>

```powershell
$env:PSModuleAnalysisCachePath = 'nul'
```

<span data-ttu-id="3ba8c-142">Ez az elérési út érvénytelen eszközön állítja be.</span><span class="sxs-lookup"><span data-stu-id="3ba8c-142">This sets the path to an invalid device.</span></span>
<span data-ttu-id="3ba8c-143">PowerShell az elérési út nem lehet írni, ha nincsenek hibát akkor adja vissza, de láthatja a hibajelentés a nyomkövető használatával:</span><span class="sxs-lookup"><span data-stu-id="3ba8c-143">If PowerShell can't write to the path, no error is returned, but you can see error reporting by using a tracer:</span></span>

```powershell
Trace-Command -PSHost -Name Modules -Expression { Import-Module Microsoft.PowerShell.Management -Force }
```

<span data-ttu-id="3ba8c-144">Ki a gyorsítótár írásakor PowerShell modulok, amely már nem létezik egy szükségtelenül nagy méretű gyorsítótárak elkerülése érdekében ellenőrzi.</span><span class="sxs-lookup"><span data-stu-id="3ba8c-144">When writing out the cache, PowerShell will check for modules that no longer exist to avoid an unnecessarily large cache.</span></span>
<span data-ttu-id="3ba8c-145">Egyes esetekben az ellenőrzések nem kívánatosak, ebben az esetben kikapcsolhatja azokat beállításával:</span><span class="sxs-lookup"><span data-stu-id="3ba8c-145">Sometimes these checks are not desirable, in which case you can turn them off by setting:</span></span>

```powershell
$env:PSDisableModuleAnalysisCacheCleanup = 1
```

<span data-ttu-id="3ba8c-146">Ez a környezeti változó beállítása azonnal érvénybe a jelenlegi folyamatban.</span><span class="sxs-lookup"><span data-stu-id="3ba8c-146">Setting this environment variable will take effect immediately in the current process.</span></span>

## <a name="specifying-module-version"></a><span data-ttu-id="3ba8c-147">A modul verzió megadása</span><span class="sxs-lookup"><span data-stu-id="3ba8c-147">Specifying module version</span></span>

<span data-ttu-id="3ba8c-148">A WMF 5.1 `using module` ugyanúgy, mint más a PowerShell modul kapcsolatos építmények működését.</span><span class="sxs-lookup"><span data-stu-id="3ba8c-148">In WMF 5.1, `using module` behaves the same way as other module-related constructions in PowerShell.</span></span>
<span data-ttu-id="3ba8c-149">Korábban a semmilyen módon nem lehet adjon meg egy adott modulban verziót; kellett Ha több verzió található, akkor ez hibát eredményezett.</span><span class="sxs-lookup"><span data-stu-id="3ba8c-149">Previously, you had no way to specify a particular module version; if there were multiple versions present, this resulted in an error.</span></span>

<span data-ttu-id="3ba8c-150">A WMF 5.1:</span><span class="sxs-lookup"><span data-stu-id="3ba8c-150">In WMF 5.1:</span></span>

- <span data-ttu-id="3ba8c-151">Használhat [ModuleSpecification konstruktor (szórótábla)](/dotnet/api/microsoft.powershell.commands.modulespecification.-ctor?view=powershellsdk-1.1.0#Microsoft_PowerShell_Commands_ModuleSpecification__ctor_System_Collections_Hashtable_).</span><span class="sxs-lookup"><span data-stu-id="3ba8c-151">You can use [ModuleSpecification Constructor (Hashtable)](/dotnet/api/microsoft.powershell.commands.modulespecification.-ctor?view=powershellsdk-1.1.0#Microsoft_PowerShell_Commands_ModuleSpecification__ctor_System_Collections_Hashtable_).</span></span>
<span data-ttu-id="3ba8c-152">A kivonattábla rendelkezik felhasználónévként `Get-Module -FullyQualifiedName`.</span><span class="sxs-lookup"><span data-stu-id="3ba8c-152">This hash table has the same format as `Get-Module -FullyQualifiedName`.</span></span>

<span data-ttu-id="3ba8c-153">**Példa:** `using module @{ModuleName = 'PSReadLine'; RequiredVersion = '1.1'}`</span><span class="sxs-lookup"><span data-stu-id="3ba8c-153">**Example:** `using module @{ModuleName = 'PSReadLine'; RequiredVersion = '1.1'}`</span></span>

- <span data-ttu-id="3ba8c-154">Ha a modul több verziója van, használja a PowerShell a **ugyanez a logika felbontása** , `Import-Module` nem ad vissza hibát--viselkedést, és `Import-Module` és `Import-DscResource`.</span><span class="sxs-lookup"><span data-stu-id="3ba8c-154">If there are multiple versions of the module, PowerShell uses the **same resolution logic** as `Import-Module` and doesn't return an error--the same behavior as `Import-Module` and `Import-DscResource`.</span></span>

## <a name="improvements-to-pester"></a><span data-ttu-id="3ba8c-155">Pester fejlesztései</span><span class="sxs-lookup"><span data-stu-id="3ba8c-155">Improvements to Pester</span></span>

<span data-ttu-id="3ba8c-156">A WMF 5.1-es, a PowerShell-lel részét képező Pester verziója 3.4.0 véglegesítési igény szerinti hozzáadásával a 3.3.5 frissült https://github.com/pester/Pester/pull/484/commits/3854ae8a1f215b39697ac6c2607baf42257b102e, amely a Nano Serveren Pester jobb viselkedését.</span><span class="sxs-lookup"><span data-stu-id="3ba8c-156">In WMF 5.1, the version of Pester that ships with PowerShell has been updated from 3.3.5 to 3.4.0, with the addition of commit https://github.com/pester/Pester/pull/484/commits/3854ae8a1f215b39697ac6c2607baf42257b102e, which enables better behavior for Pester on Nano Server.</span></span>

<span data-ttu-id="3ba8c-157">Verziók 3.3.5 való 3.4.0 változásokat áttekintheti vizsgálatával szerezheti be a ChangeLog.md fájlban a következő: https://github.com/pester/Pester/blob/master/CHANGELOG.md</span><span class="sxs-lookup"><span data-stu-id="3ba8c-157">You can review the changes in versions 3.3.5 to 3.4.0 by inspecting the ChangeLog.md file at: https://github.com/pester/Pester/blob/master/CHANGELOG.md</span></span>
