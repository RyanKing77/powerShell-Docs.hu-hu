---
ms.date: 10/17/2017
contributor: keithb
keywords: gyűjtemény, a powershell, a parancsmag, a psget
title: Parancsfájlok előzetes verziói
ms.openlocfilehash: 5b93da418b836d537491d3f1e4e29fa2e61f2f77
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/16/2018
---
# <a name="prerelease-versions-of-scripts"></a><span data-ttu-id="b1403-103">Parancsfájlok előzetes verziói</span><span class="sxs-lookup"><span data-stu-id="b1403-103">Prerelease versions of scripts</span></span>

<span data-ttu-id="b1403-104">1.6.0 verziójától kezdve, PowerShellGet és a PowerShell-galériában támogatást nyújt a címkézés nagyobb, mint egy előzetes verzióját, 1.0.0 verziók.</span><span class="sxs-lookup"><span data-stu-id="b1403-104">Starting with version 1.6.0, PowerShellGet and the PowerShell Gallery provide support for tagging versions greater than 1.0.0 as a prerelease.</span></span> <span data-ttu-id="b1403-105">Ez a szolgáltatás előtt előzetes elemek volt, hogy egy 0 verzió kezdetű korlátozott.</span><span class="sxs-lookup"><span data-stu-id="b1403-105">Prior to this feature, prerelease items were limited to having a version beginning with 0.</span></span> <span data-ttu-id="b1403-106">Ezeket a szolgáltatásokat az a célja, hogy a szélesebb körű támogatást nyújtanak [SemVer v1.0.0](http://semver.org/spec/v1.0.0.html) versioning egyezmény visszamenőleges verzióival való kompatibilitás PowerShell verziók 3 és újabb, vagy meglévő PowerShellGet megszakítása nélkül.</span><span class="sxs-lookup"><span data-stu-id="b1403-106">The goal of these features is to provide greater support for [SemVer v1.0.0](http://semver.org/spec/v1.0.0.html) versioning convention without breaking backwards compatibility with PowerShell versions 3 and above, or existing versions of PowerShellGet.</span></span> <span data-ttu-id="b1403-107">Ez a témakör a parancsfájl-specifikus szolgáltatásokra összpontosít.</span><span class="sxs-lookup"><span data-stu-id="b1403-107">This topic focuses on the script-specific features.</span></span> <span data-ttu-id="b1403-108">A modulok egyenértékű szolgáltatások szerepelnek a [előzetes verziója](module-prerelease-support.md) témakör.</span><span class="sxs-lookup"><span data-stu-id="b1403-108">The equivalent features for modules are in the [Prerelease Module Versions](module-prerelease-support.md) topic.</span></span> <span data-ttu-id="b1403-109">Használja ezeket a funkciókat, közzétevők is azonosíthatja verzió 2.5.0-alpha egy parancsfájlt, és később kiadásból egy éles használatra kész 2.5.0, amely felülírja az előzetes verziót.</span><span class="sxs-lookup"><span data-stu-id="b1403-109">Using these features, publishers can identify a script as version 2.5.0-alpha, and later release a production-ready version 2.5.0 that supersedes the prerelease version.</span></span>

<span data-ttu-id="b1403-110">Magas szinten a kiadás előtti parancsprogrammal kapcsolatos funkciói a következők:</span><span class="sxs-lookup"><span data-stu-id="b1403-110">At a high level, the prerelease script features include:</span></span>

- <span data-ttu-id="b1403-111">Egy PrereleaseString utótagot ad hozzá a parancsfájl jegyzékfájl verzió-karakterlánca.</span><span class="sxs-lookup"><span data-stu-id="b1403-111">Adding a PrereleaseString suffix to the version string in the script manifest.</span></span> <span data-ttu-id="b1403-112">Amikor a parancsfájlok közzé van téve a PowerShell-galériában, ezeket az adatokat a jegyzék kinyert, és előzetes elemek azonosítására szolgál.</span><span class="sxs-lookup"><span data-stu-id="b1403-112">When the scripts is published to the PowerShell Gallery, this data is extracted from the manifest, and used to identify prerelease items.</span></span>
- <span data-ttu-id="b1403-113">-AllowPrerelease jelző ad hozzá a PowerShellGet parancsok keresése-parancsfájl, Install-parancsfájl, előzetes elemek beszerzése szükséges frissítés-parancsfájl, és a Mentés-parancsfájl.</span><span class="sxs-lookup"><span data-stu-id="b1403-113">Acquiring prerelease items requires adding -AllowPrerelease flag to the PowerShellGet commands Find-Script, Install-Script, Update-Script, and Save-Script.</span></span> <span data-ttu-id="b1403-114">Ha a jelző nincs megadva, az előzetes elemek nem jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="b1403-114">If the flag is not specified, prerelease items will not be shown.</span></span>
- <span data-ttu-id="b1403-115">A PrereleaseString 2.5.0-alpha hasonlóan jelenik meg a keresés-parancsfájl, a Get-InstalledScript, és a PowerShell-galériában parancsfájl verziók jelenik.</span><span class="sxs-lookup"><span data-stu-id="b1403-115">Script versions displayed by Find-Script, Get-InstalledScript, and in the PowerShell Gallery will be displayed with the PrereleaseString, as in 2.5.0-alpha.</span></span>

<span data-ttu-id="b1403-116">A szolgáltatások részleteit az alábbiakban találhatók.</span><span class="sxs-lookup"><span data-stu-id="b1403-116">Details for the features are included below.</span></span>

## <a name="identifying-a-script-version-as-a-prerelease"></a><span data-ttu-id="b1403-117">A parancsfájl verziója egy előzetes verzióját azonosítása</span><span class="sxs-lookup"><span data-stu-id="b1403-117">Identifying a script version as a prerelease</span></span>

<span data-ttu-id="b1403-118">Előzetes verziói PowerShellGet támogatása még parancsfájlok könnyebb modulok.</span><span class="sxs-lookup"><span data-stu-id="b1403-118">PowerShellGet support for prerelease versions is easier for scripts than modules.</span></span> <span data-ttu-id="b1403-119">Parancsfájl versioning csak akkor támogatott PowerShellGet, ezért jelenleg nincs kompatibilitási probléma hozzáadása az előzetes karakterlánc miatt.</span><span class="sxs-lookup"><span data-stu-id="b1403-119">Script versioning is only supported by PowerShellGet, so there are no compatibility issues caused by adding the prerelease string.</span></span> <span data-ttu-id="b1403-120">Egy megfelelően formázott verzió-karakterláncot a parancsprogram-metaadatait az előzetes utótag hozzáadása a egy előzetes verzióját, a PowerShell-galériában parancsfájl azonosításához.</span><span class="sxs-lookup"><span data-stu-id="b1403-120">To identify a script in the PowerShell Gallery as a prerelease, add a prerelease suffix to a properly-formatted version string in the script metadata.</span></span>

<span data-ttu-id="b1403-121">Egy példa a szakasz egy parancsfájl jegyzékfájl előzetes verziójának a következőhöz hasonló a következő:</span><span class="sxs-lookup"><span data-stu-id="b1403-121">An example section of a script manifest with a prerelease version would look like the following:</span></span>

```powershell
<#PSScriptInfo

.VERSION 3.2.1-alpha12

.GUID

...

#>

```

<span data-ttu-id="b1403-122">Előzetes utótagot használja, a verzió-karakterláncnak a következő követelményeknek kell megfelelnie:</span><span class="sxs-lookup"><span data-stu-id="b1403-122">To use a prerelease suffix, the version string must meet the following requirements:</span></span>

- <span data-ttu-id="b1403-123">Előzetes utótag csak akkor adható meg, ha a verzió a Major.Minor.Build 3 szegmensek.</span><span class="sxs-lookup"><span data-stu-id="b1403-123">A prerelease suffix may only be specified when the Version is 3 segments for Major.Minor.Build.</span></span>
  <span data-ttu-id="b1403-124">Ez SemVer v1.0.0 igazodik</span><span class="sxs-lookup"><span data-stu-id="b1403-124">This aligns with SemVer v1.0.0</span></span>
- <span data-ttu-id="b1403-125">Az előzetes utótag egy karakterlánc, amely kötőjellel kezdődik, és tartalmazhat ASCII számok és betűk [0-9A-Za - z-]</span><span class="sxs-lookup"><span data-stu-id="b1403-125">The prerelease suffix is a string which begins with a hyphen, and may contain ASCII alphanumerics [0-9A-Za-z-]</span></span>
- <span data-ttu-id="b1403-126">Csak SemVer v1.0.0 előzetes karakterláncok használata támogatott jelenleg, ezért az előzetes utótag __nem kell__ vagy időszak tartalmaz vagy + [. +], amelyek használata engedélyezett SemVer 2.0</span><span class="sxs-lookup"><span data-stu-id="b1403-126">Only SemVer v1.0.0 prerelease strings are supported at this time, so the prerelease suffix __must not__ contain either period or + [.+], which are allowed in SemVer 2.0</span></span>
- <span data-ttu-id="b1403-127">Támogatott PrereleaseString egységmeghatározást:-alpha, - α1,-BETA, - update20171020</span><span class="sxs-lookup"><span data-stu-id="b1403-127">Examples of supported PrereleaseString strings are: -alpha, -alpha1, -BETA, -update20171020</span></span>

<span data-ttu-id="b1403-128">__Előzetes versioning hatása a rendezési sorrend és a telepítési mappa__</span><span class="sxs-lookup"><span data-stu-id="b1403-128">__Prerelease versioning impact on sort order and installation folders__</span></span>

<span data-ttu-id="b1403-129">Rendezési sorrend megváltozik, ha előzetes verzióját, akkor fontos, amikor a PowerShell-galériában közzététele, amely használja PowerShellGet parancsokkal parancsfájlok telepítésekor.</span><span class="sxs-lookup"><span data-stu-id="b1403-129">Sort order changes when using a prerelease version, which is important when publishing to the PowerShell Gallery, and when installing scripts using PowerShellGet commands.</span></span> <span data-ttu-id="b1403-130">Ha két a parancsfájlok a verziószámú verzió található, a rendezési sorrend alapján a következő a kötőjel karakterláncra vonatkozó részében.</span><span class="sxs-lookup"><span data-stu-id="b1403-130">If two scripts versions with the version number exist, the sort order is based on the string portion following the hyphen.</span></span> <span data-ttu-id="b1403-131">Igen verziója 2.5.0-alpha nem éri el 2.5.0-beta, ez pedig kisebb, mint 2.5.0-gamma.</span><span class="sxs-lookup"><span data-stu-id="b1403-131">So, version 2.5.0-alpha is less than 2.5.0-beta, which is less than 2.5.0-gamma.</span></span> <span data-ttu-id="b1403-132">Ha két parancsfájlok azonos verziószámát, és csak egy PrereleaseString, a parancsfájl nincs __nélkül__ az előzetes utótag feltételezett, hogy az éles használatra kész verzió, és nagyobb, mint előzetes verzióként rendezése történik verzió.</span><span class="sxs-lookup"><span data-stu-id="b1403-132">If two scripts have the same version number, and only one has a PrereleaseString, the script __without__ the prerelease suffix is assumed to be the production-ready version and will be sorted as a greater version than the prerelease version.</span></span> <span data-ttu-id="b1403-133">Tegyük fel, amikor 2.5.0 és 2.5.0-beta, a 2.5.0 összehasonlításával kiadott verzióját akkor veszi figyelembe a két nagyobb.</span><span class="sxs-lookup"><span data-stu-id="b1403-133">As an example, when comparing releases 2.5.0 and 2.5.0-beta, the 2.5.0 version will be considered the greater of the two.</span></span>

<span data-ttu-id="b1403-134">A PowerShell-galériában való közzétételkor alapértelmezés szerint a közzétett parancsfájl verziója kell lennie a nagyobb, mint a korábban közzétett verziót a PowerShell-galériában.</span><span class="sxs-lookup"><span data-stu-id="b1403-134">When publishing to the PowerShell Gallery, by default the version of the script being published must have a greater version than any previously-published version that is in the PowerShell Gallery.</span></span> <span data-ttu-id="b1403-135">A közzétevő módosíthatjuk verzió 2.5.0-alpha 2.5.0-beta vagy 2.5.0 (utótaggal nincs előzetes).</span><span class="sxs-lookup"><span data-stu-id="b1403-135">A publisher may update version 2.5.0-alpha with 2.5.0-beta, or with 2.5.0 (with no prerelease suffix).</span></span>

## <a name="finding-and-acquiring-prerelease-items-using-powershellget-commands"></a><span data-ttu-id="b1403-136">Keresés és PowerShellGet parancsokkal előzetes elemek beszerzése</span><span class="sxs-lookup"><span data-stu-id="b1403-136">Finding and acquiring prerelease items using PowerShellGet commands</span></span>

<span data-ttu-id="b1403-137">Előzetes elemek PowerShellGet keresés-parancsfájlból Install-, frissítés-parancsfájl használatával foglalkozó és mentés-parancsprogram-utasítások szükséges a - AllowPrerelease jelző hozzáadása.</span><span class="sxs-lookup"><span data-stu-id="b1403-137">Dealing with prerelease items using PowerShellGet Find-Script, Install-Script, Update-Script, and Save-Script commands requires adding the -AllowPrerelease flag.</span></span> <span data-ttu-id="b1403-138">Ha - AllowPrerelease meg van adva, előzetes elemek is fog szerepelni, ha ilyenek.</span><span class="sxs-lookup"><span data-stu-id="b1403-138">If -AllowPrerelease is specified, prerelease items will be included if they are present.</span></span> <span data-ttu-id="b1403-139">Ha - AllowPrerelease jelző nincs megadva, az előzetes elemek nem jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="b1403-139">If -AllowPrerelease flag is not specified, prerelease items will not be shown.</span></span>

<span data-ttu-id="b1403-140">Az egyetlen kivétel ez alól a PowerShellGet parancsprogram-utasítások a a következők: Get-InstalledScript és bizonyos esetekben az Uninstall-parancsfájl.</span><span class="sxs-lookup"><span data-stu-id="b1403-140">The only exceptions to this in the PowerShellGet script commands are Get-InstalledScript, and some cases with Uninstall-Script.</span></span>

- <span data-ttu-id="b1403-141">Get-InstalledScript mindig automatikusan információk jelennek meg az előzetes verzió-karakterlánca a ha telepítve.</span><span class="sxs-lookup"><span data-stu-id="b1403-141">Get-InstalledScript always will automatically show the prerelease information in the version string if it is present.</span></span>
- <span data-ttu-id="b1403-142">Távolítsa el parancsfájl alapértelmezés szerint eltávolítja a legfrissebb egy parancsfájlt, ha __megszűnik__ van megadva.</span><span class="sxs-lookup"><span data-stu-id="b1403-142">Uninstall-Script will by default uninstall the most recent version of a script, if __no version__ is specified.</span></span> <span data-ttu-id="b1403-143">Ezt a viselkedést nem változott.</span><span class="sxs-lookup"><span data-stu-id="b1403-143">That behavior has not changed.</span></span> <span data-ttu-id="b1403-144">Azonban ha - RequiredVersion, adott előzetes verziójának - AllowPrerelease lesz szükség.</span><span class="sxs-lookup"><span data-stu-id="b1403-144">However, if a prerelease version is specified using -RequiredVersion, -AllowPrerelease will be required.</span></span>

## <a name="examples"></a><span data-ttu-id="b1403-145">Példák</span><span class="sxs-lookup"><span data-stu-id="b1403-145">Examples</span></span>

```powershell
# Assume the PowerShell Gallery has TestPackage versions 1.8.0 and 1.9.0-alpha.
# If -AllowPrerelease is not specified, only version 1.8.0 will be returned.
C:\windows\system32> Find-Script TestPackage

Version        Name                                Repository           Description
-------        ----                                ----------           -----------
1.8.0          TestPackage                         PSGallery            Package used to validate changes to the PowerShe...

C:\windows\system32> Find-Script TestPackage -AllowPrerelease

Version        Name                                Repository           Description
-------        ----                                ----------           -----------
1.9.0-alpha    TestPackage                         PSGallery            Package used to validate changes to PowerShe...

# To install a prerelease, you must specify -AllowPrerelease. Specifying a prerelease version string is not sufficient.

C:\windows\system32> Install-Script TestPackage -RequiredVersion 1.9.0-alpha
PackageManagement\Find-Package : No match was found for the specified search criteria and script name 'TestPackage'.
Try Get-PSRepository to see all available registered script repositories.
At C:\Program Files\WindowsPowerShell\Modules\PowerShellGet\1.6.0\PSModule.psm1:1455 char:3
+         PackageManagement\Find-Package @PSBoundParameters | Microsoft ...
+         ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : ObjectNotFound: (Microsoft.Power...ets.FindPackage:FindPackage) [Find-Package], Exceptio
   n
    + FullyQualifiedErrorId : NoMatchFoundForCriteria,Microsoft.PowerShell.PackageManagement.Cmdlets.FindPackage

# The previous command failed because -AllowPrerelease was not specified.
# Adding -AllowPrerelease will result in success.

C:\windows\system32> Install-Script TestPackage -RequiredVersion 1.9.0-alpha -AllowPrerelease
C:\windows\system32> Get-InstalledScript TestPackage

Version         Name                                Repository           Description
-------         ----                                ----------           -----------
1.9.0-alpha     TestPackage                         PSGallery            Package used to validate changes to PowerShe...

# Note that Get-InstalledScript shows the prerelease version.
# If -RequiredVersion is not specified, all installed scripts will be displayed by Get-InstalledScript
```

<span data-ttu-id="b1403-146">Eltávolítása parancsfájl eltávolítja a jelenlegi verziója egy parancsfájlt, amikor - RequiredVersion nem.</span><span class="sxs-lookup"><span data-stu-id="b1403-146">Uninstall-Script will remove the current version of a script when -RequiredVersion is not supplied.</span></span>
<span data-ttu-id="b1403-147">Ha - RequiredVersion van megadva, és egy előzetes verzióját, a parancs - AllowPrerelease kell adni.</span><span class="sxs-lookup"><span data-stu-id="b1403-147">If -RequiredVersion is specified, and is a prerelease, -AllowPrerelease must be added to the command.</span></span>

``` powershell
C:\windows\system32> Get-InstalledScript TestPackage

Version         Name                                Repository           Description
-------         ----                                ----------           -----------
1.9.0-alpha     TestPackage                         PSGallery            Package used to validate changes to PowerShe...

C:\windows\system32> Uninstall-Script TestPackage -RequiredVersion 1.9.0-alpha
Uninstall-Script: The '-AllowPrerelease' parameter must be specified when using the Prerelease string in
MinimumVersion, MaximumVersion, or RequiredVersion.
At line:1 char:1
+ Unnstall-Script TestPackage -RequiredVersion 1.9.0-beta
+ ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : InvalidArgument: (:) [Uninstall-Script], ArgumentException
    + FullyQualifiedErrorId : AllowPrereleaseRequiredToUsePrereleaseStringInVersion,Uninnstall-script


C:\windows\system32> Uninstall-Script TestPackage -RequiredVersion 1.9.0-alpha -AllowPrerelease
# Since script versions are not installed side-by-side, the above could be simply "Uninstall-Script TestPackage"

C:\windows\system32> Get-Installedscript TestPackage
PackageManagement\Get-Package : No match was found for the specified search criteria and script names 'testpackage'.
At C:\Program Files\WindowsPowerShell\Modules\PowerShellGet\1.5.0.0\PSModule.psm1:4088 char:9
+         PackageManagement\Get-Package @PSBoundParameters | Microsoft. ...
+         ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : ObjectNotFound: (Microsoft.Power...lets.GetPackage:GetPackage) [Get-Package], Exception
    + FullyQualifiedErrorId : NoMatchFound,Microsoft.PowerShell.PackageManagement.Cmdlets.GetPackage
```

## <a name="more-details"></a><span data-ttu-id="b1403-148">További részletekért</span><span class="sxs-lookup"><span data-stu-id="b1403-148">More details</span></span>

- [<span data-ttu-id="b1403-149">Előzetes verziója</span><span class="sxs-lookup"><span data-stu-id="b1403-149">Prerelease Module Versions</span></span>](module-prerelease-support.md)
- [<span data-ttu-id="b1403-150">Keresés – parancsprogram</span><span class="sxs-lookup"><span data-stu-id="b1403-150">Find-script</span></span>](/powershell/module/powershellget/find-script)
- [<span data-ttu-id="b1403-151">Install-parancsfájl</span><span class="sxs-lookup"><span data-stu-id="b1403-151">Install-script</span></span>](/powershell/module/powershellget/install-script)
- [<span data-ttu-id="b1403-152">Mentés-parancsfájl</span><span class="sxs-lookup"><span data-stu-id="b1403-152">Save-script</span></span>](/powershell/module/powershellget/save-script)
- [<span data-ttu-id="b1403-153">Frissítés-parancsfájl</span><span class="sxs-lookup"><span data-stu-id="b1403-153">Update-script</span></span>](/powershell/module/powershellget/update-script)
- [<span data-ttu-id="b1403-154">Get-Installedscript</span><span class="sxs-lookup"><span data-stu-id="b1403-154">Get-Installedscript</span></span>](/powershell/module/powershellget/get-installedscript)
- [<span data-ttu-id="b1403-155">Távolítsa el parancsfájl</span><span class="sxs-lookup"><span data-stu-id="b1403-155">UnInstall-script</span></span>](/powershell/module/powershellget/uninstall-script)