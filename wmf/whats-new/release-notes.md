---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: WMF, powershell, beállítás
title: A WMF 5.x kibocsátási megjegyzései
ms.openlocfilehash: 8bdc423234cf0b104b72b1bee1de35e50783d8a4
ms.sourcegitcommit: 01b81317029b28dd9b61d167045fd31f1ec7bc06
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/17/2019
ms.locfileid: "65856398"
---
# <a name="windows-management-framework-wmf-5x-release-notes"></a><span data-ttu-id="5b99a-103">Windows Management Framework (WMF) 5.x kiadási megjegyzései</span><span class="sxs-lookup"><span data-stu-id="5b99a-103">Windows Management Framework (WMF) 5.x Release Notes</span></span>

## <a name="wmf-50-changes"></a><span data-ttu-id="5b99a-104">A WMF 5.0 változik</span><span class="sxs-lookup"><span data-stu-id="5b99a-104">WMF 5.0 Changes</span></span>

- <span data-ttu-id="5b99a-105">PowerShell 5.0 hozzáad egy új strukturált **információk** stream</span><span class="sxs-lookup"><span data-stu-id="5b99a-105">PowerShell 5.0 adds a new structured **Information** stream</span></span>
- <span data-ttu-id="5b99a-106">DSC, beleértve a négy új DSC-erőforrások fejlesztései:</span><span class="sxs-lookup"><span data-stu-id="5b99a-106">Improvements to DSC including four new DSC resources:</span></span>
  - <span data-ttu-id="5b99a-107">WindowsFeatureSet</span><span class="sxs-lookup"><span data-stu-id="5b99a-107">WindowsFeatureSet</span></span>
  - <span data-ttu-id="5b99a-108">WindowsOptionalFeatureSet</span><span class="sxs-lookup"><span data-stu-id="5b99a-108">WindowsOptionalFeatureSet</span></span>
  - <span data-ttu-id="5b99a-109">ServiceSet</span><span class="sxs-lookup"><span data-stu-id="5b99a-109">ServiceSet</span></span>
  - <span data-ttu-id="5b99a-110">ProcessSet</span><span class="sxs-lookup"><span data-stu-id="5b99a-110">ProcessSet</span></span>
- <span data-ttu-id="5b99a-111">A hozzáadott Just Enough Administration – PowerShell-távelérés szerepkör alapú felügyelet engedélyezése</span><span class="sxs-lookup"><span data-stu-id="5b99a-111">Added Just Enough Administration to enable role-based administration through PowerShell remoting</span></span>
- <span data-ttu-id="5b99a-112">PowerShell 5.0 terjeszti ki a nyelvet, a felhasználó által definiált osztályok és enumerálásokat tartalmaznak</span><span class="sxs-lookup"><span data-stu-id="5b99a-112">PowerShell 5.0 extends the language to include user-defined classes and enumerations</span></span>
- <span data-ttu-id="5b99a-113">Továbbfejlesztett hibakeresés a PowerShell ISE-ben és az új távoli hibakeresési funkciók</span><span class="sxs-lookup"><span data-stu-id="5b99a-113">Improved debugging features in PowerShell ISE and added remote debugging</span></span>
- <span data-ttu-id="5b99a-114">A PowerShellGet és a PackageManagement-modulok hozzáadása</span><span class="sxs-lookup"><span data-stu-id="5b99a-114">Added the PowerShellGet and PackageManagement modules</span></span>
- <span data-ttu-id="5b99a-115">PowerShell-parancsfájl a továbbfejlesztett naplózás és szövegekben</span><span class="sxs-lookup"><span data-stu-id="5b99a-115">Enhanced PowerShell script logging and transcripts</span></span>
- <span data-ttu-id="5b99a-116">Titkosítási Message Syntax-parancsmagok hozzáadása</span><span class="sxs-lookup"><span data-stu-id="5b99a-116">Add Cryptographic Message Syntax cmdlets</span></span>
- <span data-ttu-id="5b99a-117">A WMF 5.0 a NetworkSwitchManager modult tartalmaz a Windows</span><span class="sxs-lookup"><span data-stu-id="5b99a-117">WMF 5.0 includes the NetworkSwitchManager module for Windows</span></span>
- <span data-ttu-id="5b99a-118">A Microsoft.PowerShell.ODataUtils modul hozzáadása</span><span class="sxs-lookup"><span data-stu-id="5b99a-118">Added the Microsoft.PowerShell.ODataUtils module</span></span>
- <span data-ttu-id="5b99a-119">Támogatás hozzáadva a szoftverleltár-naplózási (SIL)</span><span class="sxs-lookup"><span data-stu-id="5b99a-119">Added support for Software Inventory Logging (SIL)</span></span>
- <span data-ttu-id="5b99a-120">Új-kiszolgálóhoz, vagy felhasználói kérésre és problémára válaszul parancsmagok frissítése</span><span class="sxs-lookup"><span data-stu-id="5b99a-120">Sever new or update cmdlets in response to user requests and issues</span></span>

## <a name="wmf-51-changes"></a><span data-ttu-id="5b99a-121">A WMF 5.1 változik</span><span class="sxs-lookup"><span data-stu-id="5b99a-121">WMF 5.1 Changes</span></span>

<span data-ttu-id="5b99a-122">A WMF 5.1 összetevői a PowerShell, a WMI, a Rendszerfelügyeleti webszolgáltatások és a szoftverleltár-naplózási (SIL) kiadott – Windows Server 2016-ban.</span><span class="sxs-lookup"><span data-stu-id="5b99a-122">WMF 5.1 includes the PowerShell, WMI, WinRM, and Software Inventory Logging (SIL) components that were released with Windows Server 2016.</span></span> <span data-ttu-id="5b99a-123">A WMF 5.1 Windows 7, Windows 8.1, Windows Server 2008 R2, 2012 és 2012 R2 telepíthető, és felett, beleértve a WMF 5.0 számos fejlesztést tartalmaz:</span><span class="sxs-lookup"><span data-stu-id="5b99a-123">WMF 5.1 can be installed on Windows 7, Windows 8.1, Windows Server 2008 R2, 2012, and 2012 R2, and provides several improvements over WMF 5.0 including:</span></span>

- <span data-ttu-id="5b99a-124">Új parancsmagok</span><span class="sxs-lookup"><span data-stu-id="5b99a-124">New cmdlets</span></span>
- <span data-ttu-id="5b99a-125">A PowerShellGet javításai, többek között az aláírt modulok használatának kényszerítése és a JEA-modulok telepítése</span><span class="sxs-lookup"><span data-stu-id="5b99a-125">PowerShellGet improvements include enforcing signed modules, and installing JEA modules</span></span>
- <span data-ttu-id="5b99a-126">A PackageManagement mostantól támogatja a Containers szolgáltatást, a CBS-beállítást, az EXE-alapú beállítást és a CAB-csomagokat</span><span class="sxs-lookup"><span data-stu-id="5b99a-126">PackageManagement added support for Containers, CBS Setup, EXE-based setup, CAB packages</span></span>
- <span data-ttu-id="5b99a-127">DSC- és PowerShell-osztályok hibakeresési javításai</span><span class="sxs-lookup"><span data-stu-id="5b99a-127">Debugging improvements for DSC and PowerShell classes</span></span>
- <span data-ttu-id="5b99a-128">Biztonsági fejlesztések: katalógus által aláírt modulok használatának kényszerítése a lekérési kiszolgálóról érkező modulok, illetve PowerShellGet-parancsmagok használata esetén</span><span class="sxs-lookup"><span data-stu-id="5b99a-128">Security enhancements including enforcement of catalog-signed modules coming from the Pull Server and when using PowerShellGet cmdlets</span></span>
- <span data-ttu-id="5b99a-129">Válaszok néhány felhasználói kérésre és problémára</span><span class="sxs-lookup"><span data-stu-id="5b99a-129">Responses to a number of user requests and issues</span></span>

## <a name="powershell-editions"></a><span data-ttu-id="5b99a-130">PowerShell-kiadások</span><span class="sxs-lookup"><span data-stu-id="5b99a-130">PowerShell Editions</span></span>

<span data-ttu-id="5b99a-131">5.1-es verziótól kezdődően PowerShell érhető el a különböző kiadásait, amelyek különböző szolgáltatáskészleteket és a platformkompatibilitásra jelöl.</span><span class="sxs-lookup"><span data-stu-id="5b99a-131">Starting with version 5.1, PowerShell is available in different editions that denote varying feature sets and platform compatibility.</span></span>

- <span data-ttu-id="5b99a-132">**Desktop kiadás:** .NET-keretrendszer épül, és kompatibilis a Windows például a Server Core és a Windows asztal teljes erőforrás-igényű kiadásain fut PowerShell-verziókat célzó szkriptekhez és modulokhoz biztosít.</span><span class="sxs-lookup"><span data-stu-id="5b99a-132">**Desktop Edition:** Built on .NET Framework and provides compatibility with scripts and modules targeting versions of PowerShell running on full footprint editions of Windows such as Server Core and Windows Desktop.</span></span>
- <span data-ttu-id="5b99a-133">**Core kiadás:** .NET Core épül, és kompatibilis csökkentett erőforrás-igényű kiadása esetén például a Nano Server Windows és Windows IoT kiadásokon futtatott PowerShell-verziókat célzó szkriptekhez és modulokhoz biztosít.</span><span class="sxs-lookup"><span data-stu-id="5b99a-133">**Core Edition:** Built on .NET Core and provides compatibility with scripts and modules targeting versions of PowerShell running on reduced footprint editions of Windows such as Nano Server and Windows IoT.</span></span>

### <a name="learn-more-about-using-powershell-editions"></a><span data-ttu-id="5b99a-134">További tudnivalók a PowerShell-kiadások használatával</span><span class="sxs-lookup"><span data-stu-id="5b99a-134">Learn more about using PowerShell Editions</span></span>

- [<span data-ttu-id="5b99a-135">Határozza meg a PowerShell használatával $PSVersionTable futó kiadása</span><span class="sxs-lookup"><span data-stu-id="5b99a-135">Determine running edition of PowerShell using $PSVersionTable</span></span>](/powershell/module/microsoft.powershell.core/about/about_automatic_variables)
- [<span data-ttu-id="5b99a-136">Get-Module eredmények által PSEdition paraméterrel CompatiblePSEditions szűrése</span><span class="sxs-lookup"><span data-stu-id="5b99a-136">Filter Get-Module results by CompatiblePSEditions using PSEdition parameter</span></span>](/powershell/module/microsoft.powershell.core/get-module)
- [<span data-ttu-id="5b99a-137">Parancsfájl végrehajtása megakadályozása, ha a PowerShell kompatibilis kiadásán futtatása</span><span class="sxs-lookup"><span data-stu-id="5b99a-137">Prevent script execution unless run on a compatible edition of PowerShell</span></span>](/powershell/gallery/concepts/script-psedition-support)
- [<span data-ttu-id="5b99a-138">Deklarálja a verziókkal PowerShell-modul kompatibilitás</span><span class="sxs-lookup"><span data-stu-id="5b99a-138">Declare a module's compatibility to specific PowerShell versions</span></span>](/powershell/gallery/concepts/module-psedition-support)

## <a name="module-analysis-cache"></a><span data-ttu-id="5b99a-139">A modul elemzési gyorsítótár</span><span class="sxs-lookup"><span data-stu-id="5b99a-139">Module Analysis Cache</span></span>

<span data-ttu-id="5b99a-140">A WMF 5.1-es verziótól kezdődően PowerShell segítségével szabályozhatja, a fájl, amellyel egy modult, exportálja a parancsok például a gyorsítótár adatait.</span><span class="sxs-lookup"><span data-stu-id="5b99a-140">Starting with WMF 5.1, PowerShell provides control over the file that is used to cache data about a module, such as the commands it exports.</span></span>

<span data-ttu-id="5b99a-141">Alapértelmezés szerint ez a gyorsítótár a fájlban tárolt `${env:LOCALAPPDATA}\Microsoft\Windows\PowerShell\ModuleAnalysisCache`.</span><span class="sxs-lookup"><span data-stu-id="5b99a-141">By default, this cache is stored in the file `${env:LOCALAPPDATA}\Microsoft\Windows\PowerShell\ModuleAnalysisCache`.</span></span> <span data-ttu-id="5b99a-142">A gyorsítótár egy parancs keresése közben általában olvasható indításkor, és íródik a háttérbeli szálon némi várakozás után egy modul importálása kész.</span><span class="sxs-lookup"><span data-stu-id="5b99a-142">The cache is typically read at startup while searching for a command and is written on a background thread sometime after a module is imported.</span></span>

<span data-ttu-id="5b99a-143">Ha módosítani szeretné az alapértelmezett hely a gyorsítótár, állítsa be a `$env:PSModuleAnalysisCachePath` környezeti változót a PowerShell indítása előtt.</span><span class="sxs-lookup"><span data-stu-id="5b99a-143">To change the default location of the cache, set the `$env:PSModuleAnalysisCachePath` environment variable before starting PowerShell.</span></span> <span data-ttu-id="5b99a-144">Ez a környezeti változó módosításai csak hatással lesz a gyermekek folyamatokat.</span><span class="sxs-lookup"><span data-stu-id="5b99a-144">Changes to this environment variable will only affect children processes.</span></span> <span data-ttu-id="5b99a-145">Az érték teljes elérési utat (például fájlnév), amely PowerShell jogosult hozhat létre és írhat fájlokat kell neve.</span><span class="sxs-lookup"><span data-stu-id="5b99a-145">The value should name a full path (including filename) that PowerShell has permission to create and write files.</span></span> <span data-ttu-id="5b99a-146">A fájlgyorsítótárban letiltásához állítsa be ezt az értéket érvénytelen helyre, például:</span><span class="sxs-lookup"><span data-stu-id="5b99a-146">To disable the file cache, set this value to an invalid location, for example:</span></span>

```powershell
$env:PSModuleAnalysisCachePath = 'nul'
```

<span data-ttu-id="5b99a-147">Ez az elérési út érvénytelen eszközön állítja be.</span><span class="sxs-lookup"><span data-stu-id="5b99a-147">This sets the path to an invalid device.</span></span> <span data-ttu-id="5b99a-148">PowerShell az elérési út nem lehet írni, ha nincsenek hibát akkor adja vissza, de láthatja a hibajelentés a nyomkövető használatával:</span><span class="sxs-lookup"><span data-stu-id="5b99a-148">If PowerShell can't write to the path, no error is returned, but you can see error reporting by using a tracer:</span></span>

```powershell
Trace-Command -PSHost -Name Modules -Expression { Import-Module Microsoft.PowerShell.Management -Force }
```

<span data-ttu-id="5b99a-149">Ki a gyorsítótár írásakor PowerShell modulok, amely már nem létezik egy szükségtelenül nagy méretű gyorsítótárak elkerülése érdekében ellenőrzi.</span><span class="sxs-lookup"><span data-stu-id="5b99a-149">When writing out the cache, PowerShell will check for modules that no longer exist to avoid an unnecessarily large cache.</span></span> <span data-ttu-id="5b99a-150">Egyes esetekben az ellenőrzések nem kívánatosak, ebben az esetben kikapcsolhatja azokat beállításával:</span><span class="sxs-lookup"><span data-stu-id="5b99a-150">Sometimes these checks are not desirable, in which case you can turn them off by setting:</span></span>

```powershell
$env:PSDisableModuleAnalysisCacheCleanup = 1
```

<span data-ttu-id="5b99a-151">Ez a környezeti változó beállítása azonnal érvénybe a jelenlegi folyamatban.</span><span class="sxs-lookup"><span data-stu-id="5b99a-151">Setting this environment variable will take effect immediately in the current process.</span></span>

## <a name="specifying-module-version"></a><span data-ttu-id="5b99a-152">A modul verzió megadása</span><span class="sxs-lookup"><span data-stu-id="5b99a-152">Specifying module version</span></span>

<span data-ttu-id="5b99a-153">A WMF 5.1 `using module` ugyanúgy, mint más a PowerShell modul kapcsolatos építmények működését.</span><span class="sxs-lookup"><span data-stu-id="5b99a-153">In WMF 5.1, `using module` behaves the same way as other module-related constructions in PowerShell.</span></span>
<span data-ttu-id="5b99a-154">Korábban a semmilyen módon nem lehet adjon meg egy adott modulban verziót; kellett Ha több verzió található, akkor ez hibát eredményezett.</span><span class="sxs-lookup"><span data-stu-id="5b99a-154">Previously, you had no way to specify a particular module version; if there were multiple versions present, this resulted in an error.</span></span>

<span data-ttu-id="5b99a-155">A WMF 5.1:</span><span class="sxs-lookup"><span data-stu-id="5b99a-155">In WMF 5.1:</span></span>

- <span data-ttu-id="5b99a-156">Használhat [ModuleSpecification konstruktor (szórótábla)](/dotnet/api/microsoft.powershell.commands.modulespecification.-ctor?view=powershellsdk-1.1.0#Microsoft_PowerShell_Commands_ModuleSpecification__ctor_System_Collections_Hashtable_).</span><span class="sxs-lookup"><span data-stu-id="5b99a-156">You can use [ModuleSpecification Constructor (Hashtable)](/dotnet/api/microsoft.powershell.commands.modulespecification.-ctor?view=powershellsdk-1.1.0#Microsoft_PowerShell_Commands_ModuleSpecification__ctor_System_Collections_Hashtable_).</span></span>
  <span data-ttu-id="5b99a-157">A kivonattábla rendelkezik felhasználónévként `Get-Module -FullyQualifiedName`.</span><span class="sxs-lookup"><span data-stu-id="5b99a-157">This hash table has the same format as `Get-Module -FullyQualifiedName`.</span></span>

  <span data-ttu-id="5b99a-158">**Példa:** `using module @{ModuleName = 'PSReadLine'; RequiredVersion = '1.1'}`</span><span class="sxs-lookup"><span data-stu-id="5b99a-158">**Example:** `using module @{ModuleName = 'PSReadLine'; RequiredVersion = '1.1'}`</span></span>

- <span data-ttu-id="5b99a-159">Ha a modul több verziója van, használja a PowerShell a **ugyanez a logika felbontása** , `Import-Module` nem ad vissza hibát--viselkedést, és `Import-Module` és `Import-DscResource`.</span><span class="sxs-lookup"><span data-stu-id="5b99a-159">If there are multiple versions of the module, PowerShell uses the **same resolution logic** as `Import-Module` and doesn't return an error--the same behavior as `Import-Module` and `Import-DscResource`.</span></span>

## <a name="improvements-to-pester"></a><span data-ttu-id="5b99a-160">Pester fejlesztései</span><span class="sxs-lookup"><span data-stu-id="5b99a-160">Improvements to Pester</span></span>

<span data-ttu-id="5b99a-161">A WMF 5.1-es verziója a PowerShell-lel részét képező Pester frissült a 3.3.5 3.4.0.</span><span class="sxs-lookup"><span data-stu-id="5b99a-161">In WMF 5.1, the version of Pester that ships with PowerShell has been updated from 3.3.5 to 3.4.0.</span></span>
<span data-ttu-id="5b99a-162">Ez a frissítés lehetővé teszi, hogy jobb viselkedés a Pester a Nano Serveren.</span><span class="sxs-lookup"><span data-stu-id="5b99a-162">This update enables better behavior for Pester on Nano Server.</span></span>

<span data-ttu-id="5b99a-163">Áttekintheti a módosításokat a kártevők vizsgálatával szerezheti be a [változásnaplójában](https://github.com/pester/Pester/blob/master/CHANGELOG.md) a GitHub-adattárában.</span><span class="sxs-lookup"><span data-stu-id="5b99a-163">You can review the changes in Pest by inspecting the [ChangeLog](https://github.com/pester/Pester/blob/master/CHANGELOG.md) in the GitHub repository.</span></span>
