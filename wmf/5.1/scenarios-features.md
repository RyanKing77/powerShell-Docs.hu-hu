---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: WMF, powershell, beállítás
title: Új forgatókönyvek és funkciók a WMF 5.1
ms.openlocfilehash: 77b439e61c5802f8ddbc4a0f39923cc8c0c36fe9
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/16/2018
ms.locfileid: "34190315"
---
# <a name="new-scenarios-and-features-in-wmf-51"></a><span data-ttu-id="21d39-103">Új forgatókönyvek és funkciók a WMF 5.1</span><span class="sxs-lookup"><span data-stu-id="21d39-103">New Scenarios and Features in WMF 5.1</span></span>

> <span data-ttu-id="21d39-104">Megjegyzés: A rendszer előzetes és bármikor megváltozhat.</span><span class="sxs-lookup"><span data-stu-id="21d39-104">Note: This information is preliminary and subject to change.</span></span>

## <a name="powershell-editions"></a><span data-ttu-id="21d39-105">PowerShell-kiadások</span><span class="sxs-lookup"><span data-stu-id="21d39-105">PowerShell Editions</span></span>

<span data-ttu-id="21d39-106">Az 5.1-es verziótól kezdődően a PowerShell különböző kiadásokban érhető el, amelyek különböző szolgáltatáskészleteket és platformkompatibilitást kínálnak.</span><span class="sxs-lookup"><span data-stu-id="21d39-106">Starting with version 5.1, PowerShell is available in different editions which denote varying feature sets and platform compatibility.</span></span>

- <span data-ttu-id="21d39-107">**Desktop kiadás:** A .NET-keretrendszeren alapul, és a Windows teljes erőforrás-igényű kiadásain, például a Server Core és a Windows asztali kiadásain futtatott PowerShell-verziókat célzó szkriptekhez és modulokhoz biztosít kompatibilitást.</span><span class="sxs-lookup"><span data-stu-id="21d39-107">**Desktop Edition:** Built on .NET Framework and provides compatibility with scripts and modules targeting versions of PowerShell running on full footprint editions of Windows such as Server Core and Windows Desktop.</span></span>
- <span data-ttu-id="21d39-108">**Core kiadás:** .NET Core-on alapul, és a Windows csökkentett erőforrás-igényű kiadásain, például a Nano Serveren és a Windows IoT kiadásokon futtatott PowerShell-verziókat célzó szkriptekhez és modulokhoz biztosít kompatibilitást.</span><span class="sxs-lookup"><span data-stu-id="21d39-108">**Core Edition:** Built on .NET Core and provides compatibility with scripts and modules targeting versions of PowerShell running on reduced footprint editions of Windows such as Nano Server and Windows IoT.</span></span>

<span data-ttu-id="21d39-109">**További tudnivalók a PowerShell verziójával**</span><span class="sxs-lookup"><span data-stu-id="21d39-109">**Learn more about using PowerShell Editions**</span></span>

- [<span data-ttu-id="21d39-110">Határozza meg a PowerShell használatával $PSVersionTable futó kiadása</span><span class="sxs-lookup"><span data-stu-id="21d39-110">Determine running edition of PowerShell using $PSVersionTable</span></span>](/powershell/module/microsoft.powershell.core/about/about_automatic_variables)
- [<span data-ttu-id="21d39-111">Get-Module eredmény által PSEdition paraméter használatával CompatiblePSEditions szűrése</span><span class="sxs-lookup"><span data-stu-id="21d39-111">Filter Get-Module results by CompatiblePSEditions using PSEdition parameter</span></span>](/powershell/module/microsoft.powershell.core/get-module)
- [<span data-ttu-id="21d39-112">Megakadályozza a parancsfájl végrehajtása, kivéve, ha egy kompatibilis PowerShell kiadásán futtatása</span><span class="sxs-lookup"><span data-stu-id="21d39-112">Prevent script execution unless run on a compatible edition of PowerShell</span></span>](/powershell/gallery/psget/script/scriptwithpseditionsupport)
- [<span data-ttu-id="21d39-113">A modul kompatibilitási adott PowerShell verziókra deklarálható</span><span class="sxs-lookup"><span data-stu-id="21d39-113">Declare a module's compatibility to specific PowerShell versions</span></span>](/powershell/gallery/psget/module/modulewithpseditionsupport)

## <a name="catalog-cmdlets"></a><span data-ttu-id="21d39-114">Katalógus-parancsmagok</span><span class="sxs-lookup"><span data-stu-id="21d39-114">Catalog Cmdlets</span></span>

<span data-ttu-id="21d39-115">Két új parancsmagokkal bővült a a [Microsoft.PowerShell.Security](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.security) modul; ezek létrehozása és a Windows katalógusban fájlok érvényesítése.</span><span class="sxs-lookup"><span data-stu-id="21d39-115">Two new cmdlets have been added in the [Microsoft.PowerShell.Security](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.security) module; these generate and validate Windows catalog files.</span></span>

### <a name="new-filecatalog"></a><span data-ttu-id="21d39-116">New-FileCatalog</span><span class="sxs-lookup"><span data-stu-id="21d39-116">New-FileCatalog</span></span>
--------------------------------

<span data-ttu-id="21d39-117">Új FileCatalog fájlt hoz létre a Windows katalógusban mappák és fájlok.</span><span class="sxs-lookup"><span data-stu-id="21d39-117">New-FileCatalog creates a Windows catalog file for set of folders and files.</span></span>
<span data-ttu-id="21d39-118">Ez a katalógus fájl tartalmazza az összes fájl megadott elérési utak a kivonatok.</span><span class="sxs-lookup"><span data-stu-id="21d39-118">This catalog file contains hashes for all files in specified paths.</span></span>
<span data-ttu-id="21d39-119">Az ezeken a mappákon jelölő megfelelő katalógusfájlt együtt mappák készletét terjeszthetnek.</span><span class="sxs-lookup"><span data-stu-id="21d39-119">Users can distribute the set of folders along with corresponding catalog file representing those folders.</span></span>
<span data-ttu-id="21d39-120">Ez az információ akkor hasznos, ellenőrzése, hogy bármely módosult a mappák katalógus létrehozása óta.</span><span class="sxs-lookup"><span data-stu-id="21d39-120">This information is useful to validate whether any changes have been made to the folders since catalog creation time.</span></span>

```powershell
New-FileCatalog [-CatalogFilePath] <string> [[-Path] <string[]>] [-CatalogVersion <int>] [-WhatIf] [-Confirm] [<CommonParameters>]
```

<span data-ttu-id="21d39-121">1. és 2-katalógus verziókat támogatja.</span><span class="sxs-lookup"><span data-stu-id="21d39-121">Catalog versions 1 and 2 are supported.</span></span>
<span data-ttu-id="21d39-122">1-es verziójú az SHA1 kivonatoló algoritmus segítségével hozza létre a fájlkivonat; 2-es verzióját használja az SHA-256.</span><span class="sxs-lookup"><span data-stu-id="21d39-122">Version 1 uses the SHA1 hashing algorithm to create file hashes; version 2 uses SHA256.</span></span>
<span data-ttu-id="21d39-123">Katalógus 2-es verzió nem támogatott a *Windows Server 2008 R2* vagy *Windows 7*.</span><span class="sxs-lookup"><span data-stu-id="21d39-123">Catalog version 2 is not supported on *Windows Server 2008 R2* or *Windows 7*.</span></span>
<span data-ttu-id="21d39-124">A katalógus 2-es verzióját kell használnia *Windows 8*, *Windows Server 2012*, és annál újabb operációs rendszereken.</span><span class="sxs-lookup"><span data-stu-id="21d39-124">You should use catalog version 2 on *Windows 8*, *Windows Server 2012*, and later operating systems.</span></span>

![](../images/NewFileCatalog.jpg)

<span data-ttu-id="21d39-125">Ez a katalógus fájlt hoz létre.</span><span class="sxs-lookup"><span data-stu-id="21d39-125">This creates the catalog file.</span></span>

![](../images/CatalogFile1.jpg)

![](../images/CatalogFile2.jpg)

<span data-ttu-id="21d39-126">Katalógusfájlt (Pester.cat a fenti példában) sértetlenségének ellenőrzéséhez használatával írja alá [Set-AuthenticodeSignature](https://technet.microsoft.com/library/hh849819.aspx) parancsmag.</span><span class="sxs-lookup"><span data-stu-id="21d39-126">To verify the integrity of catalog file (Pester.cat in above example), sign it using [Set-AuthenticodeSignature](https://technet.microsoft.com/library/hh849819.aspx) cmdlet.</span></span>

### <a name="test-filecatalog"></a><span data-ttu-id="21d39-127">Test-FileCatalog</span><span class="sxs-lookup"><span data-stu-id="21d39-127">Test-FileCatalog</span></span>
--------------------------------

<span data-ttu-id="21d39-128">Teszt-FileCatalog érvényesíti a katalógus képviselő mappákat.</span><span class="sxs-lookup"><span data-stu-id="21d39-128">Test-FileCatalog validates the catalog representing a set of folders.</span></span>

```powershell
Test-FileCatalog [-CatalogFilePath] <string> [[-Path] <string[]>] [-Detailed] [-FilesToSkip <string[]>] [-WhatIf] [-Confirm] [<CommonParameters>]
```

![](../images/TestFileCatalog.jpg)

<span data-ttu-id="21d39-129">Ez a parancsmag összehasonlítja a fájlok kivonatok és azok relatív elérési utak található *katalógus* az azokat a *lemez*.</span><span class="sxs-lookup"><span data-stu-id="21d39-129">This cmdlet compares all the files hashes and their relative paths found in *catalog* with ones on *disk*.</span></span>
<span data-ttu-id="21d39-130">Ha a fájlkivonat és elérési utak bármely eltérést észlel a állapotának adja vissza *ValidationFailed*.</span><span class="sxs-lookup"><span data-stu-id="21d39-130">If it detects any mismatch between file hashes and paths it returns the status as *ValidationFailed*.</span></span>
<span data-ttu-id="21d39-131">Felhasználók használatával kérheti le ezt az információt a *-részletes* paraméter.</span><span class="sxs-lookup"><span data-stu-id="21d39-131">Users can retrieve all this information by using the *-Detailed* parameter.</span></span>
<span data-ttu-id="21d39-132">Azt is állapotát jeleníti meg az aláíró katalógust a *aláírás* tulajdonság, amely egyenértékű hívása [Get-AuthenticodeSignature](https://technet.microsoft.com/library/hh849805.aspx) parancsmag a katalógus fájlra.</span><span class="sxs-lookup"><span data-stu-id="21d39-132">It also displays signing status of catalog in *Signature* property which is equivalent to calling [Get-AuthenticodeSignature](https://technet.microsoft.com/library/hh849805.aspx) cmdlet on the catalog file.</span></span>
<span data-ttu-id="21d39-133">Felhasználók is hagyhatja a fájl ellenőrzésekor használatával a *- FilesToSkip* paraméter.</span><span class="sxs-lookup"><span data-stu-id="21d39-133">Users can also skip any file during validation by using the *-FilesToSkip* parameter.</span></span>

## <a name="module-analysis-cache"></a><span data-ttu-id="21d39-134">A modul elemzés gyorsítótár</span><span class="sxs-lookup"><span data-stu-id="21d39-134">Module Analysis Cache</span></span>

<span data-ttu-id="21d39-135">WMF 5.1 verziótól kezdődően PowerShell segítségével szabályozhatja, a fájl, amellyel egy modul, mint például a parancsok kivitt gyorsítótár adatait.</span><span class="sxs-lookup"><span data-stu-id="21d39-135">Starting with WMF 5.1, PowerShell provides control over the file that is used to cache data about a module, such as the commands it exports.</span></span>

<span data-ttu-id="21d39-136">Alapértelmezés szerint ez a gyorsítótár a fájlban tárolt `${env:LOCALAPPDATA}\Microsoft\Windows\PowerShell\ModuleAnalysisCache`.</span><span class="sxs-lookup"><span data-stu-id="21d39-136">By default, this cache is stored in the file `${env:LOCALAPPDATA}\Microsoft\Windows\PowerShell\ModuleAnalysisCache`.</span></span>
<span data-ttu-id="21d39-137">A gyorsítótár indításkor parancs keresése során általában olvasható nevével, és a háttérszálon az némi várakozás után egy modul importálása.</span><span class="sxs-lookup"><span data-stu-id="21d39-137">The cache is typically read at startup while searching for a command and is written on a background thread sometime after a module is imported.</span></span>

<span data-ttu-id="21d39-138">A gyorsítótár alapértelmezett helyének módosításához állítsa a `$env:PSModuleAnalysisCachePath` környezeti változó PowerShell indítása előtt.</span><span class="sxs-lookup"><span data-stu-id="21d39-138">To change the default location of the cache, set the `$env:PSModuleAnalysisCachePath` environment variable before starting PowerShell.</span></span>
<span data-ttu-id="21d39-139">A környezeti változó módosítása csak hatással gyermekei folyamat.</span><span class="sxs-lookup"><span data-stu-id="21d39-139">Changes to this environment variable will only affect children processes.</span></span>
<span data-ttu-id="21d39-140">Az érték egy teljes elérési útja (többek között a következőket fájlnév), amely PowerShell jogosult létrehozásához és írásához fájlok nevet.</span><span class="sxs-lookup"><span data-stu-id="21d39-140">The value should name a full path (including filename) that PowerShell has permission to create and write files.</span></span>
<span data-ttu-id="21d39-141">Tiltsa le a gyorsítótárban, állítsa be az érték érvénytelen helyre, például:</span><span class="sxs-lookup"><span data-stu-id="21d39-141">To disable the file cache, set this value to an invalid location, for example:</span></span>

```powershell
$env:PSModuleAnalysisCachePath = 'nul'
```

<span data-ttu-id="21d39-142">Ez beállítja az elérési út érvénytelen eszközök számára.</span><span class="sxs-lookup"><span data-stu-id="21d39-142">This sets the path to an invalid device.</span></span>
<span data-ttu-id="21d39-143">PowerShell az elérési út nem lehet írni, ha nincs hibát ad vissza, de egy követő használatával hibajelentési láthatja:</span><span class="sxs-lookup"><span data-stu-id="21d39-143">If PowerShell can't write to the path, no error is returned, but you can see error reporting by using a tracer:</span></span>

```powershell
Trace-Command -PSHost -Name Modules -Expression { Import-Module Microsoft.PowerShell.Management -Force }
```

<span data-ttu-id="21d39-144">A gyorsítótár írása, PowerShell ellenőrzi a modulok, amely egy feleslegesen gyorsítótár elkerülése érdekében a továbbiakban nem létezik.</span><span class="sxs-lookup"><span data-stu-id="21d39-144">When writing out the cache, PowerShell will check for modules that no longer exist to avoid an unnecessarily large cache.</span></span>
<span data-ttu-id="21d39-145">Az ellenőrzések sokszor nem kívánatos, ebben az esetben kikapcsolható őket úgy, hogy:</span><span class="sxs-lookup"><span data-stu-id="21d39-145">Sometimes these checks are not desirable, in which case you can turn them off by setting:</span></span>

```powershell
$env:PSDisableModuleAnalysisCacheCleanup = 1
```

<span data-ttu-id="21d39-146">A környezeti változó beállítása azonnali hatállyal érvénybe a jelenlegi folyamatban.</span><span class="sxs-lookup"><span data-stu-id="21d39-146">Setting this environment variable will take effect immediately in the current process.</span></span>

## <a name="specifying-module-version"></a><span data-ttu-id="21d39-147">Modul verzió megadása</span><span class="sxs-lookup"><span data-stu-id="21d39-147">Specifying module version</span></span>

<span data-ttu-id="21d39-148">A WMF 5.1 `using module` ugyanúgy, mint más a PowerShell modul kapcsolatos építmények viselkedik.</span><span class="sxs-lookup"><span data-stu-id="21d39-148">In WMF 5.1, `using module` behaves the same way as other module-related constructions in PowerShell.</span></span>
<span data-ttu-id="21d39-149">Adjon meg egy adott modulban verziót; semmilyen módon nem volt korábban Ha több verziója található, akkor ez hibát eredményezett.</span><span class="sxs-lookup"><span data-stu-id="21d39-149">Previously, you had no way to specify a particular module version; if there were multiple versions present, this resulted in an error.</span></span>

<span data-ttu-id="21d39-150">A WMF 5.1:</span><span class="sxs-lookup"><span data-stu-id="21d39-150">In WMF 5.1:</span></span>

- <span data-ttu-id="21d39-151">Használhat [ModuleSpecification konstruktor (hibás)](https://msdn.microsoft.com/library/jj136290).</span><span class="sxs-lookup"><span data-stu-id="21d39-151">You can use [ModuleSpecification Constructor (Hashtable)](https://msdn.microsoft.com/library/jj136290).</span></span>
<span data-ttu-id="21d39-152">A kivonattábla formátuma, `Get-Module -FullyQualifiedName`.</span><span class="sxs-lookup"><span data-stu-id="21d39-152">This hash table has the same format as `Get-Module -FullyQualifiedName`.</span></span>

<span data-ttu-id="21d39-153">**Példa:** `using module @{ModuleName = 'PSReadLine'; RequiredVersion = '1.1'}`</span><span class="sxs-lookup"><span data-stu-id="21d39-153">**Example:** `using module @{ModuleName = 'PSReadLine'; RequiredVersion = '1.1'}`</span></span>

- <span data-ttu-id="21d39-154">Ha a modul több verziója is van, a PowerShell használja a **logikák feloldási** , `Import-Module` nem ad visszatérési hiba – a kívánt viselkedést eredményező beállítást, és `Import-Module` és `Import-DscResource`.</span><span class="sxs-lookup"><span data-stu-id="21d39-154">If there are multiple versions of the module, PowerShell uses the **same resolution logic** as `Import-Module` and doesn't return an error--the same behavior as `Import-Module` and `Import-DscResource`.</span></span>

## <a name="improvements-to-pester"></a><span data-ttu-id="21d39-155">Pester fejlesztései</span><span class="sxs-lookup"><span data-stu-id="21d39-155">Improvements to Pester</span></span>

<span data-ttu-id="21d39-156">WMF 5.1, a PowerShell-lel részét képező Pester verziója 3.4.0 véglegesítés azonban kiegészül a 3.3.5 megújult https://github.com/pester/Pester/pull/484/commits/3854ae8a1f215b39697ac6c2607baf42257b102e, amely lehetővé teszi, hogy jobb viselkedését a Nano Server Pester a.</span><span class="sxs-lookup"><span data-stu-id="21d39-156">In WMF 5.1, the version of Pester that ships with PowerShell has been updated from 3.3.5 to 3.4.0, with the addition of commit https://github.com/pester/Pester/pull/484/commits/3854ae8a1f215b39697ac6c2607baf42257b102e, which enables better behavior for Pester on Nano Server.</span></span>

<span data-ttu-id="21d39-157">Ellenőrizze a ChangeLog.md fájlban a következő verziók 3.3.5 való 3.4.0 változásai tekinthetők át: https://github.com/pester/Pester/blob/master/CHANGELOG.md</span><span class="sxs-lookup"><span data-stu-id="21d39-157">You can review the changes in versions 3.3.5 to 3.4.0 by inspecting the ChangeLog.md file at: https://github.com/pester/Pester/blob/master/CHANGELOG.md</span></span>
