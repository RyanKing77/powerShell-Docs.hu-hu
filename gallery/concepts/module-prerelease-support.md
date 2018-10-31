---
ms.date: 09/26/2017
contributor: keithb
keywords: katalógus, powershell, a parancsmag, psget
title: Előzetes verziója
ms.openlocfilehash: f58b5adfeba7ed06d231c76accbd52508c7d67d6
ms.sourcegitcommit: 98b7cfd8ad5718efa8e320526ca76c3cc4141d78
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/25/2018
ms.locfileid: "50002769"
---
# <a name="prerelease-module-versions"></a><span data-ttu-id="98a60-103">Előzetes verziója</span><span class="sxs-lookup"><span data-stu-id="98a60-103">Prerelease Module Versions</span></span>

<span data-ttu-id="98a60-104">1.6.0-s verziójának verziótól kezdődően a PowerShellGet és a PowerShell-galériából támogatást nyújt a címkézési egy előzetes verzióját, 1.0.0-esnél újabb verzióiban.</span><span class="sxs-lookup"><span data-stu-id="98a60-104">Starting with version 1.6.0, PowerShellGet and the PowerShell Gallery provide support for tagging versions greater than 1.0.0 as a prerelease.</span></span> <span data-ttu-id="98a60-105">Ez a funkció előtt előzetes csomagokat a rendszer 0-verzió kezdő járulnia korlátozott.</span><span class="sxs-lookup"><span data-stu-id="98a60-105">Prior to this feature, prerelease packages were limited to having a version beginning with 0.</span></span> <span data-ttu-id="98a60-106">Ezeket a funkciókat az a célja, hogy a szélesebb körű támogatást biztosít [SemVer v1.0.0](http://semver.org/spec/v1.0.0.html) versioning egyezmény visszamenőleges PowerShell verziók 3 és újabb, vagy meglévő a PowerShellGet verzióival való kompatibilitás megszakítása nélkül.</span><span class="sxs-lookup"><span data-stu-id="98a60-106">The goal of these features is to provide greater support for [SemVer v1.0.0](http://semver.org/spec/v1.0.0.html) versioning convention without breaking backwards compatibility with PowerShell versions 3 and above, or existing versions of PowerShellGet.</span></span> <span data-ttu-id="98a60-107">Ez a témakör a modul-specifikus szolgáltatásokra összpontosít.</span><span class="sxs-lookup"><span data-stu-id="98a60-107">This topic focuses on the module-specific features.</span></span> <span data-ttu-id="98a60-108">A parancsfájlok egyenértékű funkciókra a [parancsfájlok előzetes verziók](script-prerelease-support.md) témakör.</span><span class="sxs-lookup"><span data-stu-id="98a60-108">The equivalent features for scripts are in the [Prerelease Versions of Scripts](script-prerelease-support.md) topic.</span></span> <span data-ttu-id="98a60-109">Használja ezeket a funkciókat, a kiadók is modul vagy verzió 2.5.0-alpha-parancsprogramot, és később kiadásból egy éles használatra kész 2.5.0, amely felülírja az előzetes verziót.</span><span class="sxs-lookup"><span data-stu-id="98a60-109">Using these features, publishers can identify a module or script as version 2.5.0-alpha, and later release a production-ready version 2.5.0 that supersedes the prerelease version.</span></span>

<span data-ttu-id="98a60-110">Magas szinten a modul előzetes funkciók a következők:</span><span class="sxs-lookup"><span data-stu-id="98a60-110">At a high level, the prerelease module features include:</span></span>

- <span data-ttu-id="98a60-111">A modul előzetes karakterláncot ad hozzá a moduljegyzékben PSData szakaszában azonosítja az előzetes verzióként.</span><span class="sxs-lookup"><span data-stu-id="98a60-111">Adding a Prerelease string to the PSData section of the module manifest identifies the module as a prerelease version.</span></span> <span data-ttu-id="98a60-112">Ha a modul a PowerShell-galériából tesznek közzé, ezeket az adatokat a jegyzékfájl kinyert, és előzetes csomagok azonosítására szolgál.</span><span class="sxs-lookup"><span data-stu-id="98a60-112">When the module is published to the PowerShell Gallery, this data is extracted from the manifest, and used to identify prerelease packages.</span></span>
- <span data-ttu-id="98a60-113">Előzetes csomagokat beszerzéséhez szükséges hozzáadása `-AllowPrerelease` jelzőt a PowerShellGet-parancsokkal `Find-Module`, `Install-Module`, `Update-Module`, és `Save-Module`.</span><span class="sxs-lookup"><span data-stu-id="98a60-113">Acquiring prerelease packages requires adding `-AllowPrerelease` flag to the PowerShellGet commands `Find-Module`, `Install-Module`, `Update-Module`, and `Save-Module`.</span></span> <span data-ttu-id="98a60-114">Ha nincs megadva a jelzőt, végleges csomagok nem jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="98a60-114">If the flag is not specified, prerelease packages will not be shown.</span></span>
- <span data-ttu-id="98a60-115">Modulverziók által megjelenített `Find-Module`, `Get-InstalledModule`, és a PowerShell-galériából a jelenik meg egyetlen utótaggal, mint 2.5.0-alpha előzetes karakterláncot karakterláncként.</span><span class="sxs-lookup"><span data-stu-id="98a60-115">Module versions displayed by `Find-Module`, `Get-InstalledModule`, and in the PowerShell Gallery will be displayed as a single string with the Prerelease string appended, as in 2.5.0-alpha.</span></span>

<span data-ttu-id="98a60-116">Szolgáltatások részletei az alábbiakban találhatók.</span><span class="sxs-lookup"><span data-stu-id="98a60-116">Details for the features are included below.</span></span>

<span data-ttu-id="98a60-117">Ezek a változások nem befolyásolják a PowerShell beépített modul verzió támogatása, és kompatibilis a PowerShell 3.0-s, 4.0 és 5.</span><span class="sxs-lookup"><span data-stu-id="98a60-117">These changes do not affect the module version support that is built into PowerShell, and are compatible with PowerShell 3.0, 4.0, and 5.</span></span>

## <a name="identifying-a-module-version-as-a-prerelease"></a><span data-ttu-id="98a60-118">Egy modul verzió azonosítása egy előzetes verzióját</span><span class="sxs-lookup"><span data-stu-id="98a60-118">Identifying a module version as a prerelease</span></span>

<span data-ttu-id="98a60-119">A PowerShellGet-támogatás előzetes verzióihoz két mezőt a modul Manifest használatát igényli:</span><span class="sxs-lookup"><span data-stu-id="98a60-119">PowerShellGet support for prerelease versions requires the use of two fields within the Module Manifest:</span></span>

- <span data-ttu-id="98a60-120">A foglalt a moduljegyzékben ModuleVersion egy 3 részben verziójúnak kell lennie, ha előzetes verziójának szolgál, és meg kell felelniük a meglévő PowerShell verziószámozás.</span><span class="sxs-lookup"><span data-stu-id="98a60-120">The ModuleVersion included in the module manifest must be a 3-part version if a prerelease version is used, and must comply with existing PowerShell versioning.</span></span> <span data-ttu-id="98a60-121">A verziójának formátumát A.B.C, ahol A, B és C az összes egész szám lehet.</span><span class="sxs-lookup"><span data-stu-id="98a60-121">The version format would be A.B.C, where A, B, and C are all integers.</span></span>
- <span data-ttu-id="98a60-122">A kiadás előtti karakterlánc van megadva a moduljegyzékben PrivateData PSData szakaszában.</span><span class="sxs-lookup"><span data-stu-id="98a60-122">The Prerelease string is specified in the module manifest, in the PSData section of PrivateData.</span></span>

<span data-ttu-id="98a60-123">Az alábbiakban a megjelenés előtti karakterlánc részletes követelményeket.</span><span class="sxs-lookup"><span data-stu-id="98a60-123">Detailed requirements on the Prerelease string are below.</span></span>

<span data-ttu-id="98a60-124">Egy példa szakaszában egy moduljegyzék, amely meghatározza egy modul egy előzetes verzióját, az alábbi módon jelenik meg:</span><span class="sxs-lookup"><span data-stu-id="98a60-124">An example section of a module manifest that defines a module as a prerelease would look like the following:</span></span>

```powershell
@{
    ModuleVersion = '2.5.0'
    #---
    PrivateData = @{
        PSData = @{
            Prerelease = 'alpha'
        }
    }
}
```

<span data-ttu-id="98a60-125">A kiadás előtti karakterlánc részletes követelményei a következők:</span><span class="sxs-lookup"><span data-stu-id="98a60-125">The detailed requirements for Prerelease string are:</span></span>

- <span data-ttu-id="98a60-126">Előzetes karakterlánc csak akkor adható meg, ha a ModuleVersion 3 szegmenssel főverzió.alverzió.build formában az.</span><span class="sxs-lookup"><span data-stu-id="98a60-126">Prerelease string may only be specified when the ModuleVersion is 3 segments for Major.Minor.Build.</span></span> <span data-ttu-id="98a60-127">Ez SemVer v1.0.0 illeszkedik.</span><span class="sxs-lookup"><span data-stu-id="98a60-127">This aligns with SemVer v1.0.0.</span></span>
- <span data-ttu-id="98a60-128">Egy kötőjel a kivonni kívánt a buildszám és a megjelenés előtti karakterlánc között.</span><span class="sxs-lookup"><span data-stu-id="98a60-128">A hyphen is the delimiter between the Build number and the Prerelease string.</span></span> <span data-ttu-id="98a60-129">Egy kötőjel mint az első karakter, csak a kiadás előtti karakterlánc kell venni.</span><span class="sxs-lookup"><span data-stu-id="98a60-129">A hyphen may be included in the Prerelease string as the first character, only.</span></span>
- <span data-ttu-id="98a60-130">A kiadás előtti karakterlánc csak alfanumerikus ASCII-karaktereket tartalmazhat [0-pedig a 9A-Za - z-].</span><span class="sxs-lookup"><span data-stu-id="98a60-130">The Prerelease string may contain only ASCII alphanumerics [0-9A-Za-z-].</span></span> <span data-ttu-id="98a60-131">Ajánlott eljárás a Prerelease megkezdéséhez karakterlánc egy alfanumerikus karakter, könnyebben azonosíthatja, hogy ez a kiadás előtti verzióját, csomagok listájának beolvasásakor.</span><span class="sxs-lookup"><span data-stu-id="98a60-131">It is a best practice to begin the Prerelease string with an alpha character, as it will be easier to identify that this is a prerelease version when scanning a list of packages.</span></span>
- <span data-ttu-id="98a60-132">Jelenleg csak SemVer v1.0.0 előzetes karakterláncok támogatott.</span><span class="sxs-lookup"><span data-stu-id="98a60-132">Only SemVer v1.0.0 prerelease strings are supported at this time.</span></span> <span data-ttu-id="98a60-133">Előzetes karakterlánc **nem kell** vagy időszak tartalmazhat vagy + [. +], amely SemVer 2.0 használata engedélyezett.</span><span class="sxs-lookup"><span data-stu-id="98a60-133">Prerelease string **must not** contain either period or + [.+], which are allowed in SemVer 2.0.</span></span>
- <span data-ttu-id="98a60-134">Néhány példa a támogatott előzetes karakterlánc:-alpha, - α1, – BÉTAVERZIÓ, - update20171020</span><span class="sxs-lookup"><span data-stu-id="98a60-134">Examples of supported Prerelease string are: -alpha, -alpha1, -BETA, -update20171020</span></span>

### <a name="prerelease-versioning-impact-on-sort-order-and-installation-folders"></a><span data-ttu-id="98a60-135">Előzetes versioning hatása a rendezési sorrend és a telepítési mappa</span><span class="sxs-lookup"><span data-stu-id="98a60-135">Prerelease versioning impact on sort order and installation folders</span></span>

<span data-ttu-id="98a60-136">Rendezési sorrend módosítja, ami fontos a PowerShell-galériából való közzétételkor, előzetes verziójának használata esetén, és ha a PowerShellGet-parancsokkal modulok telepítése.</span><span class="sxs-lookup"><span data-stu-id="98a60-136">Sort order changes when using a prerelease version, which is important when publishing to the PowerShell Gallery, and when installing modules using PowerShellGet commands.</span></span> <span data-ttu-id="98a60-137">Ha az kiadás előtti karakterlánc két modul van megadva, a rendezési sorrendet a karakterlánc része a kötőjelet tartalmazhatja a következő alapul.</span><span class="sxs-lookup"><span data-stu-id="98a60-137">If the Prerelease string is specified for two modules, the sort order is based on the string portion following the hyphen.</span></span> <span data-ttu-id="98a60-138">Tehát verzió 2.5.0-alpha kisebb, mint 2.5.0-beta, amely kisebb, mint 2.5.0-gamma.</span><span class="sxs-lookup"><span data-stu-id="98a60-138">So, version 2.5.0-alpha is less than 2.5.0-beta, which is less than 2.5.0-gamma.</span></span> <span data-ttu-id="98a60-139">Ha két modult az azonos ModuleVersion, és csak egy előzetes karakterlánccal rendelkezik, a kiadás előtti karakterlánc nélkül a modul adatforrásmérete az éles használatra kész verziót, és nagyobb, mint az előzetes verziót (amely tartalmazza az előzetes verzióként rendezése (karakterlánc).</span><span class="sxs-lookup"><span data-stu-id="98a60-139">If two modules have the same ModuleVersion, and only one has a Prerelease string, the module without the Prerelease string is assumed to be the production-ready version and will be sorted as a greater version than the prerelease version (which includes the Prerelease string).</span></span> <span data-ttu-id="98a60-140">Tegyük fel, amikor 2.5.0 és 2.5.0-beta, a 2.5.0 összehasonlítása kiadások nagyobb, mint a két verzió akkor minősül.</span><span class="sxs-lookup"><span data-stu-id="98a60-140">As an example, when comparing releases 2.5.0 and 2.5.0-beta, the 2.5.0 version will be considered the greater of the two.</span></span>

<span data-ttu-id="98a60-141">A PowerShell-galériából való közzétételkor alapértelmezés szerint a közzétett modul verzióját kell lennie a nagyobb, mint a korábban közzétett verzió, a PowerShell-galériában található.</span><span class="sxs-lookup"><span data-stu-id="98a60-141">When publishing to the PowerShell Gallery, by default the version of the module being published must have a greater version than any previously-published version that is in the PowerShell Gallery.</span></span>

## <a name="finding-and-acquiring-prerelease-packages-using-powershellget-commands"></a><span data-ttu-id="98a60-142">Keresés és a PowerShellGet-parancsokkal előzetes csomagok beszerzése</span><span class="sxs-lookup"><span data-stu-id="98a60-142">Finding and acquiring prerelease packages using PowerShellGet commands</span></span>

<span data-ttu-id="98a60-143">Előzetes csomagokat-Module PowerShellGet Find-Module, Install-Module, frissítés, kezelése és a Save-Module parancsokat igényel, a - AllowPrerelease jelző hozzáadása.</span><span class="sxs-lookup"><span data-stu-id="98a60-143">Dealing with prerelease packages using PowerShellGet Find-Module, Install-Module, Update-Module, and Save-Module commands requires adding the -AllowPrerelease flag.</span></span> <span data-ttu-id="98a60-144">Ha meg van adva a - AllowPrerelease, előzetes csomagokat helyőrzője, ha ilyenek.</span><span class="sxs-lookup"><span data-stu-id="98a60-144">If -AllowPrerelease is specified, prerelease packages will be included if they are present.</span></span> <span data-ttu-id="98a60-145">Ha nincs megadva - AllowPrerelease jelző, előzetes csomagokat nem jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="98a60-145">If -AllowPrerelease flag is not specified, prerelease packages will not be shown.</span></span>

<span data-ttu-id="98a60-146">Alól kivételt csak ehhez a PowerShellGet modul parancsok a következők: Get-InstalledModule és bizonyos esetekben az Uninstall-modul.</span><span class="sxs-lookup"><span data-stu-id="98a60-146">The only exceptions to this in the PowerShellGet module commands are Get-InstalledModule, and some cases with Uninstall-Module.</span></span>

- <span data-ttu-id="98a60-147">Get-InstalledModule mindig automatikusan információk jelennek meg az előzetes modulok verzió karakterláncában.</span><span class="sxs-lookup"><span data-stu-id="98a60-147">Get-InstalledModule always will automatically show the prerelease information in the version string for modules.</span></span>
- <span data-ttu-id="98a60-148">Távolítsa el modul alapértelmezés szerint eltávolítja egy modul legújabb verzióját Ha __nincs verzió__ van megadva.</span><span class="sxs-lookup"><span data-stu-id="98a60-148">Uninstall-Module will by default uninstall the most recent version of a module, if __no version__ is specified.</span></span> <span data-ttu-id="98a60-149">Ezt a viselkedést nem változott.</span><span class="sxs-lookup"><span data-stu-id="98a60-149">That behavior has not changed.</span></span> <span data-ttu-id="98a60-150">Azonban ha előzetes verziójának meg van adva, használja a - RequiredVersion, - AllowPrerelease lesz szükség.</span><span class="sxs-lookup"><span data-stu-id="98a60-150">However, if a prerelease version is specified using -RequiredVersion, -AllowPrerelease will be required.</span></span>

## <a name="examples"></a><span data-ttu-id="98a60-151">Példák</span><span class="sxs-lookup"><span data-stu-id="98a60-151">Examples</span></span>

<span data-ttu-id="98a60-152">Tegyük fel, a PowerShell-galériából TestPackage modulverziók 1.8.0-as és 1.9.0-alpha rendelkezik.</span><span class="sxs-lookup"><span data-stu-id="98a60-152">Assume the PowerShell Gallery has TestPackage module versions 1.8.0 and 1.9.0-alpha.</span></span> <span data-ttu-id="98a60-153">Ha `-AllowPrerelease` van nincs megadva, csak 1.8.0-as verziót adja vissza.</span><span class="sxs-lookup"><span data-stu-id="98a60-153">If `-AllowPrerelease` is not specified, only version 1.8.0 will be returned.</span></span>

```powershell
find-module TestPackage
```

```output
Version        Name           Repository  Description
-------        ----           ----------  -----------
1.8.0          TestPackage    PSGallery   Package used to validate changes to the PowerShe...
```

```powershell
find-module TestPackage -AllowPrerelease
```

```output
Version        Name           Repository  Description
-------        ----           ----------  -----------
1.9.0-alpha    TestPackage    PSGallery   Package used to validate changes to the PowerShe...
```

<span data-ttu-id="98a60-154">Mindig adja meg a - AllowPrerelease egy előzetes verzióját kell telepíteni.</span><span class="sxs-lookup"><span data-stu-id="98a60-154">To install a prerelease, always specify -AllowPrerelease.</span></span> <span data-ttu-id="98a60-155">Egy kiadás előtti verzió-karakterlánccal való megadása nem elegendő.</span><span class="sxs-lookup"><span data-stu-id="98a60-155">Specifying a prerelease version string is not sufficient.</span></span>

```powershell
Install-module TestPackage -RequiredVersion 1.9.0-alpha
```

```output
PackageManagement\Find-Package : No match was found for the specified search criteria and module name 'TestPackage'.
Try Get-PSRepository to see all available registered module repositories.
At C:\Program Files\WindowsPowerShell\Modules\PowerShellGet\1.6.0\PSModule.psm1:1455 char:3
+         PackageManagement\Find-Package @PSBoundParameters | Microsoft ...
+         ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : ObjectNotFound: (Microsoft.Power...ets.FindPackage:FindPackage) [Find-Package], Exception
    + FullyQualifiedErrorId : NoMatchFoundForCriteria,Microsoft.PowerShell.PackageManagement.Cmdlets.FindPackage
```

<span data-ttu-id="98a60-156">Az előző parancs meghiúsult, mert a - AllowPrerelease nincs megadva.</span><span class="sxs-lookup"><span data-stu-id="98a60-156">The previous command failed because -AllowPrerelease was not specified.</span></span> <span data-ttu-id="98a60-157">Hozzáadás `-AllowPrerelease` sikeres eredményez.</span><span class="sxs-lookup"><span data-stu-id="98a60-157">Adding `-AllowPrerelease` will result in success.</span></span>

```powershell
Install-module TestPackage -RequiredVersion 1.9.0-alpha -AllowPrerelease
Get-InstalledModule TestPackage
```

```output
Version         Name          Repository  Description
-------         ----          ----------  -----------
1.9.0-alpha     TestPackage   PSGallery   Package used to validate changes to the PowerShe...
```

<span data-ttu-id="98a60-158">Egymás melletti telepítés, amelyet csak a megadott prerelease miatt eltérő verziójú modulok nem támogatott.</span><span class="sxs-lookup"><span data-stu-id="98a60-158">Side-by-side installation of versions of a module that differ only due to the prerelease specified is not supported.</span></span> <span data-ttu-id="98a60-159">A PowerShellGet-modul telepítésekor ugyanazon modul különböző verzióinak egymás melletti telepített hoz létre a mappa nevét, a ModuleVersion használatával.</span><span class="sxs-lookup"><span data-stu-id="98a60-159">When installing a module using PowerShellGet, different versions of the same module are installed side-by-side by creating a folder name using the ModuleVersion.</span></span> <span data-ttu-id="98a60-160">A mappa nevét a ModuleVersion, a kiadás előtti karakterlánc nélkül használható.</span><span class="sxs-lookup"><span data-stu-id="98a60-160">The ModuleVersion, without the prerelease string, is used for the folder name.</span></span> <span data-ttu-id="98a60-161">Ha egy felhasználó MyModule verzió 2.5.0-alpha telepíti, akkor fog települni a `MyModule\2.5.0` mappát.</span><span class="sxs-lookup"><span data-stu-id="98a60-161">If a user installs MyModule version 2.5.0-alpha, it will be installed to the `MyModule\2.5.0` folder.</span></span> <span data-ttu-id="98a60-162">Ha a felhasználó ezután 2.5.0-beta telepíti, a 2.5.0-beta verziót fog **felülírása** a mappa tartalmának `MyModule\2.5.0`.</span><span class="sxs-lookup"><span data-stu-id="98a60-162">If the user then installs 2.5.0-beta, the 2.5.0-beta version will **overwrite** the contents of the folder `MyModule\2.5.0`.</span></span> <span data-ttu-id="98a60-163">Egyik előnye az, hogy ez a módszer, hogy nincs szükség az eltávolítási az előzetes verziót az éles használatra kész verzió telepítése után.</span><span class="sxs-lookup"><span data-stu-id="98a60-163">One advantage to this approach is that there is no need to un-install the prerelease version after installing the production-ready version.</span></span> <span data-ttu-id="98a60-164">Az alábbi példa bemutatja, mi várható:</span><span class="sxs-lookup"><span data-stu-id="98a60-164">The example below shows what to expect:</span></span>

``` powershell
C:\windows\system32> Get-InstalledModule TestPackage -AllVersions

Version         Name           Repository  Description
-------         ----           ----------  -----------
1.9.0-alpha     TestPackage    PSGallery   Package used to validate changes to the PowerShe...
1.8.0           TestPackage    PSGallery   Package used to validate changes to the PowerShe...
1.1.3.2         TestPackage    PSGallery   Package used to validate changes to the PowerShe...

C:\windows\system32> find-module TestPackage -AllowPrerelease

Version        Name            Repository  Description
-------        ----            ----------  -----------
1.9.0-beta     TestPackage     PSGallery   Package used to validate changes to the PowerShe...

C:\windows\system32> Update-Module TestPackage -AllowPrerelease
C:\windows\system32> Get-InstalledModule TestPackage -AllVersions

Version         Name           Repository  Description
-------         ----           ----------  -----------
1.9.0-beta      TestPackage    PSGallery   Package used to validate changes to the PowerShe...
1.8.0           TestPackage    PSGallery   Package used to validate changes to the PowerShe...
1.1.3.2         TestPackage    PSGallery   Package used to validate changes to the PowerShe...

```

<span data-ttu-id="98a60-165">Modul eltávolítása eltávolítja a modulok a legújabb verzióra, amikor a - RequiredVersion nem tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="98a60-165">Uninstall-Module will remove the latest version of a module when -RequiredVersion is not supplied.</span></span>
<span data-ttu-id="98a60-166">Ha a - RequiredVersion van megadva, és egy előzetes verzióját, - AllowPrerelease hozzá kell adni a parancshoz.</span><span class="sxs-lookup"><span data-stu-id="98a60-166">If -RequiredVersion is specified, and is a prerelease, -AllowPrerelease must be added to the command.</span></span>

``` powershell
C:\windows\system32> Get-InstalledModule TestPackage -AllVersions

Version         Name           Repository  Description
-------         ----           ----------  -----------
2.0.0-alpha1    TestPackage    PSGallery   Package used to validate changes to the PowerShe...
1.9.0-beta      TestPackage    PSGallery   Package used to validate changes to the PowerShe...
1.8.0           TestPackage    PSGallery   Package used to validate changes to the PowerShe...
1.1.3.2         TestPackage    PSGallery   Package used to validate changes to the PowerShe...

C:\windows\system32> Uninstall-Module TestPackage -RequiredVersion 1.9.0-beta

Uninstall-Module : The '-AllowPrerelease' parameter must be specified when using the Prerelease string in
MinimumVersion, MaximumVersion, or RequiredVersion.
At line:1 char:1
+ Unnstall-Module TestPackage -RequiredVersion 1.9.0-beta
+ ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : InvalidArgument: (:) [Uninstall-Module], ArgumentException
    + FullyQualifiedErrorId : AllowPrereleaseRequiredToUsePrereleaseStringInVersion,Uninnstall-Module

C:\windows\system32> Uninstall-Module TestPackage -RequiredVersion 1.9.0-beta -AllowPrerelease
C:\windows\system32> Get-InstalledModule TestPackage -AllVersions

Version         Name          Repository   Description
-------         ----          ----------   -----------
2.0.0-alpha1    TestPackage   PSGallery    Package used to validate changes to the PowerShe...
1.8.0           TestPackage   PSGallery    Package used to validate changes to the PowerShe...
1.1.3.2         TestPackage   PSGallery    Package used to validate changes to the PowerShe...

C:\windows\system32> Uninstall-Module TestPackage
C:\windows\system32> Get-InstalledModule TestPackage -AllVersions

Version         Name          Repository   Description
-------         ----          ----------   -----------
1.8.0           TestPackage   PSGallery    Package used to validate changes to the PowerShe...
1.1.3.2         TestPackage   PSGallery    Package used to validate changes to the PowerShe...
```

## <a name="more-details"></a><span data-ttu-id="98a60-167">További részletek</span><span class="sxs-lookup"><span data-stu-id="98a60-167">More details</span></span>

- [<span data-ttu-id="98a60-168">Parancsfájl előzetes verziók</span><span class="sxs-lookup"><span data-stu-id="98a60-168">Prerelease Script Versions</span></span>](script-prerelease-support.md)
- [<span data-ttu-id="98a60-169">Find-Module</span><span class="sxs-lookup"><span data-stu-id="98a60-169">Find-Module</span></span>](/powershell/module/powershellget/find-module)
- [<span data-ttu-id="98a60-170">Install-Module</span><span class="sxs-lookup"><span data-stu-id="98a60-170">Install-Module</span></span>](/powershell/module/powershellget/install-module)
- [<span data-ttu-id="98a60-171">Save-Module</span><span class="sxs-lookup"><span data-stu-id="98a60-171">Save-Module</span></span>](/powershell/module/powershellget/save-module)
- [<span data-ttu-id="98a60-172">Frissítés-modul</span><span class="sxs-lookup"><span data-stu-id="98a60-172">Update-Module</span></span>](/powershell/module/powershellget/Update-Module)
- [<span data-ttu-id="98a60-173">Get-InstalledModule</span><span class="sxs-lookup"><span data-stu-id="98a60-173">Get-InstalledModule</span></span>](/powershell/module/powershellget/get-installedmodule)
- [<span data-ttu-id="98a60-174">Távolítsa el modul</span><span class="sxs-lookup"><span data-stu-id="98a60-174">UnInstall-Module</span></span>](/powershell/module/powershellget/uninstall-module)
