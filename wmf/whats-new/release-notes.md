---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: WMF, powershell, beállítás
title: A WMF 5.x kiadási megjegyzései
ms.openlocfilehash: 8924240a4bbedcd34bc68b7cacdd23189a3716d6
ms.sourcegitcommit: 00083f07b13c73b86936e7d7307397df27c63c04
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/10/2019
ms.locfileid: "70848156"
---
# <a name="windows-management-framework-wmf-5x-release-notes"></a><span data-ttu-id="fc6f1-103">Windows Management Framework (WMF) 5. x kibocsátási megjegyzések</span><span class="sxs-lookup"><span data-stu-id="fc6f1-103">Windows Management Framework (WMF) 5.x Release Notes</span></span>

## <a name="wmf-50-changes"></a><span data-ttu-id="fc6f1-104">WMF 5,0-változások</span><span class="sxs-lookup"><span data-stu-id="fc6f1-104">WMF 5.0 Changes</span></span>

- <span data-ttu-id="fc6f1-105">A PowerShell 5,0 új strukturált **információs** streamet hoz létre</span><span class="sxs-lookup"><span data-stu-id="fc6f1-105">PowerShell 5.0 adds a new structured **Information** stream</span></span>
- <span data-ttu-id="fc6f1-106">A DSC fejlesztése, beleértve a négy új DSC-erőforrást:</span><span class="sxs-lookup"><span data-stu-id="fc6f1-106">Improvements to DSC including four new DSC resources:</span></span>
  - <span data-ttu-id="fc6f1-107">WindowsFeatureSet</span><span class="sxs-lookup"><span data-stu-id="fc6f1-107">WindowsFeatureSet</span></span>
  - <span data-ttu-id="fc6f1-108">WindowsOptionalFeatureSet</span><span class="sxs-lookup"><span data-stu-id="fc6f1-108">WindowsOptionalFeatureSet</span></span>
  - <span data-ttu-id="fc6f1-109">ServiceSet</span><span class="sxs-lookup"><span data-stu-id="fc6f1-109">ServiceSet</span></span>
  - <span data-ttu-id="fc6f1-110">ProcessSet</span><span class="sxs-lookup"><span data-stu-id="fc6f1-110">ProcessSet</span></span>
- <span data-ttu-id="fc6f1-111">Elég felügyeletet adott hozzá a Szerepköralapú felügyelet engedélyezéséhez a PowerShell távelérés használatával</span><span class="sxs-lookup"><span data-stu-id="fc6f1-111">Added Just Enough Administration to enable role-based administration through PowerShell remoting</span></span>
- <span data-ttu-id="fc6f1-112">A PowerShell 5,0 kiterjeszti a nyelvet a felhasználó által definiált osztályok és enumerálások belefoglalására.</span><span class="sxs-lookup"><span data-stu-id="fc6f1-112">PowerShell 5.0 extends the language to include user-defined classes and enumerations</span></span>
- <span data-ttu-id="fc6f1-113">Továbbfejlesztett hibakeresési funkciók a PowerShell ISE-ben és távoli hibakeresés hozzáadva</span><span class="sxs-lookup"><span data-stu-id="fc6f1-113">Improved debugging features in PowerShell ISE and added remote debugging</span></span>
- <span data-ttu-id="fc6f1-114">A PowerShellGet és a PackageManagement modulok hozzáadása</span><span class="sxs-lookup"><span data-stu-id="fc6f1-114">Added the PowerShellGet and PackageManagement modules</span></span>
- <span data-ttu-id="fc6f1-115">Továbbfejlesztett PowerShell-parancsfájlok naplózása és átiratai</span><span class="sxs-lookup"><span data-stu-id="fc6f1-115">Enhanced PowerShell script logging and transcripts</span></span>
- <span data-ttu-id="fc6f1-116">Titkosítási üzenet Szintaxisi parancsmagjainek hozzáadása</span><span class="sxs-lookup"><span data-stu-id="fc6f1-116">Add Cryptographic Message Syntax cmdlets</span></span>
- <span data-ttu-id="fc6f1-117">A WMF 5,0 tartalmazza a Windows NetworkSwitchManager modulját</span><span class="sxs-lookup"><span data-stu-id="fc6f1-117">WMF 5.0 includes the NetworkSwitchManager module for Windows</span></span>
- <span data-ttu-id="fc6f1-118">A Microsoft. PowerShell. ODataUtils modul hozzáadva</span><span class="sxs-lookup"><span data-stu-id="fc6f1-118">Added the Microsoft.PowerShell.ODataUtils module</span></span>
- <span data-ttu-id="fc6f1-119">A szoftveres leltár naplózásának (SIL) támogatása</span><span class="sxs-lookup"><span data-stu-id="fc6f1-119">Added support for Software Inventory Logging (SIL)</span></span>
- <span data-ttu-id="fc6f1-120">Új vagy frissítési parancsmagok replikálása a felhasználói kérésekre és problémákra válaszul</span><span class="sxs-lookup"><span data-stu-id="fc6f1-120">Sever new or update cmdlets in response to user requests and issues</span></span>

## <a name="wmf-51-changes"></a><span data-ttu-id="fc6f1-121">WMF 5,1-változások</span><span class="sxs-lookup"><span data-stu-id="fc6f1-121">WMF 5.1 Changes</span></span>

<span data-ttu-id="fc6f1-122">A WMF 5,1 magában foglalja a Windows Server 2016-ben kiadott PowerShell-, WMI-, WinRM-és szoftveres leltár-naplózási (SIL) összetevőket.</span><span class="sxs-lookup"><span data-stu-id="fc6f1-122">WMF 5.1 includes the PowerShell, WMI, WinRM, and Software Inventory Logging (SIL) components that were released with Windows Server 2016.</span></span> <span data-ttu-id="fc6f1-123">A WMF 5,1 a Windows 7, a Windows 8,1, a Windows Server 2008 R2, az 2012 és az 2012 R2 rendszerre telepíthető, és számos javítást biztosít a WMF 5,0-hez, beleértve a következőket:</span><span class="sxs-lookup"><span data-stu-id="fc6f1-123">WMF 5.1 can be installed on Windows 7, Windows 8.1, Windows Server 2008 R2, 2012, and 2012 R2, and provides several improvements over WMF 5.0 including:</span></span>

- <span data-ttu-id="fc6f1-124">Új parancsmagok</span><span class="sxs-lookup"><span data-stu-id="fc6f1-124">New cmdlets</span></span>
- <span data-ttu-id="fc6f1-125">A PowerShellGet javításai, többek között az aláírt modulok használatának kényszerítése és a JEA-modulok telepítése</span><span class="sxs-lookup"><span data-stu-id="fc6f1-125">PowerShellGet improvements include enforcing signed modules, and installing JEA modules</span></span>
- <span data-ttu-id="fc6f1-126">A PackageManagement mostantól támogatja a Containers szolgáltatást, a CBS-beállítást, az EXE-alapú beállítást és a CAB-csomagokat</span><span class="sxs-lookup"><span data-stu-id="fc6f1-126">PackageManagement added support for Containers, CBS Setup, EXE-based setup, CAB packages</span></span>
- <span data-ttu-id="fc6f1-127">DSC- és PowerShell-osztályok hibakeresési javításai</span><span class="sxs-lookup"><span data-stu-id="fc6f1-127">Debugging improvements for DSC and PowerShell classes</span></span>
- <span data-ttu-id="fc6f1-128">Biztonsági fejlesztések: katalógus által aláírt modulok használatának kényszerítése a lekérési kiszolgálóról érkező modulok, illetve PowerShellGet-parancsmagok használata esetén</span><span class="sxs-lookup"><span data-stu-id="fc6f1-128">Security enhancements including enforcement of catalog-signed modules coming from the Pull Server and when using PowerShellGet cmdlets</span></span>
- <span data-ttu-id="fc6f1-129">Válaszok néhány felhasználói kérésre és problémára</span><span class="sxs-lookup"><span data-stu-id="fc6f1-129">Responses to a number of user requests and issues</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fc6f1-130">Mielőtt telepítené a WMF 5,1-et a Windows Server 2008 vagy a Windows 7 rendszerre, győződjön meg róla, hogy a WMF 3,0 nincs telepítve.</span><span class="sxs-lookup"><span data-stu-id="fc6f1-130">Before you install WMF 5.1 on Windows Server 2008 or Windows 7, confirm that WMF 3.0 isn't installed.</span></span> <span data-ttu-id="fc6f1-131">További információ: [a Windows Server 2008 R2 SP1 és a Windows 7 SP1 rendszerhez készült WMF 5,1 előfeltételei](../setup/install-configure.md#wmf-51-prerequisites-for-windows-server-2008-r2-sp1-and-windows-7-sp1).</span><span class="sxs-lookup"><span data-stu-id="fc6f1-131">For more information, see [WMF 5.1 Prerequisites for Windows Server 2008 R2 SP1 and Windows 7 SP1](../setup/install-configure.md#wmf-51-prerequisites-for-windows-server-2008-r2-sp1-and-windows-7-sp1).</span></span>

## <a name="powershell-editions"></a><span data-ttu-id="fc6f1-132">PowerShell-kiadások</span><span class="sxs-lookup"><span data-stu-id="fc6f1-132">PowerShell Editions</span></span>

<span data-ttu-id="fc6f1-133">A 5,1-es verziótól kezdődően a PowerShell különböző kiadásokban érhető el, amelyek különböző szolgáltatáskészleteket és platform-kompatibilitást jeleznek.</span><span class="sxs-lookup"><span data-stu-id="fc6f1-133">Starting with version 5.1, PowerShell is available in different editions that denote varying feature sets and platform compatibility.</span></span>

- <span data-ttu-id="fc6f1-134">**Asztali kiadás:** A .NET-keretrendszerre épülő, valamint a Windows teljes helyigényű, például a Server Core és a Windows Desktop szolgáltatásban futó PowerShell-verzióit célzó parancsfájlok és modulok kompatibilitását teszi lehetővé.</span><span class="sxs-lookup"><span data-stu-id="fc6f1-134">**Desktop Edition:** Built on .NET Framework and provides compatibility with scripts and modules targeting versions of PowerShell running on full footprint editions of Windows such as Server Core and Windows Desktop.</span></span>
- <span data-ttu-id="fc6f1-135">**Core kiadás:** A .NET Core-ra épülő, valamint a Windows csökkentett lábnyomú kiadásain futó PowerShell-verziókkal való kompatibilitást biztosító parancsfájlokkal és modulokkal kompatibilis, például a nano Server és a Windows IoT.</span><span class="sxs-lookup"><span data-stu-id="fc6f1-135">**Core Edition:** Built on .NET Core and provides compatibility with scripts and modules targeting versions of PowerShell running on reduced footprint editions of Windows such as Nano Server and Windows IoT.</span></span>

### <a name="learn-more-about-using-powershell-editions"></a><span data-ttu-id="fc6f1-136">További információ a PowerShell-kiadások használatáról</span><span class="sxs-lookup"><span data-stu-id="fc6f1-136">Learn more about using PowerShell Editions</span></span>

- [<span data-ttu-id="fc6f1-137">A PowerShell futtatási kiadásának meghatározása $PSVersionTable használatával</span><span class="sxs-lookup"><span data-stu-id="fc6f1-137">Determine running edition of PowerShell using $PSVersionTable</span></span>](/powershell/module/microsoft.powershell.core/about/about_automatic_variables)
- [<span data-ttu-id="fc6f1-138">A Get-Module eredményeinek szűrése CompatiblePSEditions alapján a PSEdition paraméter használatával</span><span class="sxs-lookup"><span data-stu-id="fc6f1-138">Filter Get-Module results by CompatiblePSEditions using PSEdition parameter</span></span>](/powershell/module/microsoft.powershell.core/get-module)
- [<span data-ttu-id="fc6f1-139">Parancsfájlok végrehajtásának megakadályozása, ha a PowerShell kompatibilis változatán fut</span><span class="sxs-lookup"><span data-stu-id="fc6f1-139">Prevent script execution unless run on a compatible edition of PowerShell</span></span>](/powershell/gallery/concepts/script-psedition-support)
- [<span data-ttu-id="fc6f1-140">Modul kompatibilitásának deklarálása adott PowerShell-verziókhoz</span><span class="sxs-lookup"><span data-stu-id="fc6f1-140">Declare a module's compatibility to specific PowerShell versions</span></span>](/powershell/gallery/concepts/module-psedition-support)

## <a name="module-analysis-cache"></a><span data-ttu-id="fc6f1-141">Modul elemzési gyorsítótára</span><span class="sxs-lookup"><span data-stu-id="fc6f1-141">Module Analysis Cache</span></span>

<span data-ttu-id="fc6f1-142">A WMF 5,1-től kezdve a PowerShell szabályozza a modul adatainak gyorsítótárazásához használt fájlt, például az általa exportált parancsokat.</span><span class="sxs-lookup"><span data-stu-id="fc6f1-142">Starting with WMF 5.1, PowerShell provides control over the file that is used to cache data about a module, such as the commands it exports.</span></span>

<span data-ttu-id="fc6f1-143">Alapértelmezés szerint a fájl `${env:LOCALAPPDATA}\Microsoft\Windows\PowerShell\ModuleAnalysisCache`tárolja a gyorsítótárat.</span><span class="sxs-lookup"><span data-stu-id="fc6f1-143">By default, this cache is stored in the file `${env:LOCALAPPDATA}\Microsoft\Windows\PowerShell\ModuleAnalysisCache`.</span></span> <span data-ttu-id="fc6f1-144">A gyorsítótár általában indításkor a parancs keresésekor történik, és egy modul importálása után egy háttérbeli szálon van írva.</span><span class="sxs-lookup"><span data-stu-id="fc6f1-144">The cache is typically read at startup while searching for a command and is written on a background thread sometime after a module is imported.</span></span>

<span data-ttu-id="fc6f1-145">A gyorsítótár alapértelmezett helyének módosításához állítsa a `$env:PSModuleAnalysisCachePath` környezeti változót a PowerShell elindítása előtt.</span><span class="sxs-lookup"><span data-stu-id="fc6f1-145">To change the default location of the cache, set the `$env:PSModuleAnalysisCachePath` environment variable before starting PowerShell.</span></span> <span data-ttu-id="fc6f1-146">A környezeti változó módosításai csak a gyermekeket érintő folyamatokat érintik.</span><span class="sxs-lookup"><span data-stu-id="fc6f1-146">Changes to this environment variable will only affect children processes.</span></span> <span data-ttu-id="fc6f1-147">Az értéknek egy teljes elérési utat (a fájlnevet is beleértve) kell megjelennie, amelyet a PowerShell jogosult fájlok létrehozására és írására.</span><span class="sxs-lookup"><span data-stu-id="fc6f1-147">The value should name a full path (including filename) that PowerShell has permission to create and write files.</span></span> <span data-ttu-id="fc6f1-148">A fájl gyorsítótárának letiltásához állítsa ezt az értéket érvénytelen helyre, például:</span><span class="sxs-lookup"><span data-stu-id="fc6f1-148">To disable the file cache, set this value to an invalid location, for example:</span></span>

```powershell
$env:PSModuleAnalysisCachePath = 'nul'
```

<span data-ttu-id="fc6f1-149">Ez egy érvénytelen eszköz elérési útját állítja be.</span><span class="sxs-lookup"><span data-stu-id="fc6f1-149">This sets the path to an invalid device.</span></span> <span data-ttu-id="fc6f1-150">Ha a PowerShell nem tud írni az elérési útra, a rendszer nem ad vissza hibát, de a következőt láthatja: nyomjelző használatával.</span><span class="sxs-lookup"><span data-stu-id="fc6f1-150">If PowerShell can't write to the path, no error is returned, but you can see error reporting by using a tracer:</span></span>

```powershell
Trace-Command -PSHost -Name Modules -Expression { Import-Module Microsoft.PowerShell.Management -Force }
```

<span data-ttu-id="fc6f1-151">A gyorsítótár kiírásakor a PowerShell megkeresi azokat a modulokat, amelyek már nem léteznek a szükségtelenül nagy gyorsítótár elkerüléséhez.</span><span class="sxs-lookup"><span data-stu-id="fc6f1-151">When writing out the cache, PowerShell will check for modules that no longer exist to avoid an unnecessarily large cache.</span></span> <span data-ttu-id="fc6f1-152">Előfordulhat, hogy ezek az ellenőrzések nem kívánatosak, ebben az esetben a következő beállítással lehet kikapcsolni:</span><span class="sxs-lookup"><span data-stu-id="fc6f1-152">Sometimes these checks are not desirable, in which case you can turn them off by setting:</span></span>

```powershell
$env:PSDisableModuleAnalysisCacheCleanup = 1
```

<span data-ttu-id="fc6f1-153">A környezeti változó beállítása azonnal érvénybe lép az aktuális folyamatban.</span><span class="sxs-lookup"><span data-stu-id="fc6f1-153">Setting this environment variable will take effect immediately in the current process.</span></span>

## <a name="specifying-module-version"></a><span data-ttu-id="fc6f1-154">Modul verziószámának meghatározása</span><span class="sxs-lookup"><span data-stu-id="fc6f1-154">Specifying module version</span></span>

<span data-ttu-id="fc6f1-155">A WMF 5,1- `using module` ben ugyanúgy viselkedik, mint az egyéb modulokkal kapcsolatos szerkezetek a PowerShellben.</span><span class="sxs-lookup"><span data-stu-id="fc6f1-155">In WMF 5.1, `using module` behaves the same way as other module-related constructions in PowerShell.</span></span>
<span data-ttu-id="fc6f1-156">Korábban nem volt lehetőség egy adott modul verziójának megadására; Ha több verzió is létezik, ez hibát eredményezett.</span><span class="sxs-lookup"><span data-stu-id="fc6f1-156">Previously, you had no way to specify a particular module version; if there were multiple versions present, this resulted in an error.</span></span>

<span data-ttu-id="fc6f1-157">WMF 5,1 esetén:</span><span class="sxs-lookup"><span data-stu-id="fc6f1-157">In WMF 5.1:</span></span>

- <span data-ttu-id="fc6f1-158">Használhatja a [ModuleSpecification konstruktort (szórótábla)](/dotnet/api/microsoft.powershell.commands.modulespecification.-ctor?view=powershellsdk-1.1.0#Microsoft_PowerShell_Commands_ModuleSpecification__ctor_System_Collections_Hashtable_).</span><span class="sxs-lookup"><span data-stu-id="fc6f1-158">You can use [ModuleSpecification Constructor (Hashtable)](/dotnet/api/microsoft.powershell.commands.modulespecification.-ctor?view=powershellsdk-1.1.0#Microsoft_PowerShell_Commands_ModuleSpecification__ctor_System_Collections_Hashtable_).</span></span>

  <span data-ttu-id="fc6f1-159">Ez a kivonatoló tábla formátuma `Get-Module -FullyQualifiedName`megegyezik a következővel:.</span><span class="sxs-lookup"><span data-stu-id="fc6f1-159">This hash table has the same format as `Get-Module -FullyQualifiedName`.</span></span>

  <span data-ttu-id="fc6f1-160">**Példa:** `using module @{ModuleName = 'PSReadLine'; RequiredVersion = '1.1'}`</span><span class="sxs-lookup"><span data-stu-id="fc6f1-160">**Example:** `using module @{ModuleName = 'PSReadLine'; RequiredVersion = '1.1'}`</span></span>

- <span data-ttu-id="fc6f1-161">Ha a modul több verziója is létezik, a PowerShell ugyanazt a **feloldási logikát** használja, mint `Import-Module` a, és nem ad vissza hibát – ugyanaz `Import-DscResource`a viselkedés, mint `Import-Module` a és a.</span><span class="sxs-lookup"><span data-stu-id="fc6f1-161">If there are multiple versions of the module, PowerShell uses the **same resolution logic** as `Import-Module` and doesn't return an error--the same behavior as `Import-Module` and `Import-DscResource`.</span></span>

## <a name="improvements-to-pester"></a><span data-ttu-id="fc6f1-162">A Pest fejlesztése</span><span class="sxs-lookup"><span data-stu-id="fc6f1-162">Improvements to Pester</span></span>

<span data-ttu-id="fc6f1-163">A WMF 5,1-ben a PowerShell-lel rendelkező, a 3.3.5-ről a 3.4.0-re irányuló zaklató verziója frissült.</span><span class="sxs-lookup"><span data-stu-id="fc6f1-163">In WMF 5.1, the version of Pester that ships with PowerShell has been updated from 3.3.5 to 3.4.0.</span></span>
<span data-ttu-id="fc6f1-164">Ez a frissítés lehetővé teszi, hogy a nano Serveren a zaklatás jobb viselkedést biztosítson.</span><span class="sxs-lookup"><span data-stu-id="fc6f1-164">This update enables better behavior for Pester on Nano Server.</span></span>

<span data-ttu-id="fc6f1-165">A kártevők változásait a GitHub-tárházban található [changelog](https://github.com/pester/Pester/blob/master/CHANGELOG.md) ellenőrizheti.</span><span class="sxs-lookup"><span data-stu-id="fc6f1-165">You can review the changes in Pest by inspecting the [ChangeLog](https://github.com/pester/Pester/blob/master/CHANGELOG.md) in the GitHub repository.</span></span>
