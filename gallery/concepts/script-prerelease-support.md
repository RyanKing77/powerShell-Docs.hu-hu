---
ms.date: 10/17/2017
contributor: keithb
keywords: katalógus, powershell, a parancsmag, psget
title: A parancsfájlok előzetes verziók
ms.openlocfilehash: 4e7eab682008ed57163c51fe3a61a744b347bef2
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55683981"
---
# <a name="prerelease-versions-of-scripts"></a><span data-ttu-id="7cde6-103">A parancsfájlok előzetes verziók</span><span class="sxs-lookup"><span data-stu-id="7cde6-103">Prerelease versions of scripts</span></span>

<span data-ttu-id="7cde6-104">1.6.0-s verziójának verziótól kezdődően a PowerShellGet és a PowerShell-galériából támogatást nyújt a címkézési egy előzetes verzióját, 1.0.0-esnél újabb verzióiban.</span><span class="sxs-lookup"><span data-stu-id="7cde6-104">Starting with version 1.6.0, PowerShellGet and the PowerShell Gallery provide support for tagging versions greater than 1.0.0 as a prerelease.</span></span> <span data-ttu-id="7cde6-105">Ez a funkció előtt előzetes csomagokat a rendszer 0-verzió kezdő járulnia korlátozott.</span><span class="sxs-lookup"><span data-stu-id="7cde6-105">Prior to this feature, prerelease packages were limited to having a version beginning with 0.</span></span> <span data-ttu-id="7cde6-106">Ezeket a funkciókat az a célja, hogy a szélesebb körű támogatást biztosít [SemVer v1.0.0](http://semver.org/spec/v1.0.0.html) versioning egyezmény visszamenőleges PowerShell verziók 3 és újabb, vagy meglévő a PowerShellGet verzióival való kompatibilitás megszakítása nélkül.</span><span class="sxs-lookup"><span data-stu-id="7cde6-106">The goal of these features is to provide greater support for [SemVer v1.0.0](http://semver.org/spec/v1.0.0.html) versioning convention without breaking backwards compatibility with PowerShell versions 3 and above, or existing versions of PowerShellGet.</span></span> <span data-ttu-id="7cde6-107">Ez a témakör a parancsfájl-specifikus szolgáltatásokra összpontosít.</span><span class="sxs-lookup"><span data-stu-id="7cde6-107">This topic focuses on the script-specific features.</span></span> <span data-ttu-id="7cde6-108">A modulok egyenértékű funkciókra a [Prerelease modulverziók](module-prerelease-support.md) témakör.</span><span class="sxs-lookup"><span data-stu-id="7cde6-108">The equivalent features for modules are in the [Prerelease Module Versions](module-prerelease-support.md) topic.</span></span> <span data-ttu-id="7cde6-109">Használja ezeket a funkciókat, a kiadók is verzió 2.5.0-alpha, a szkriptet azonosító, és később kiadásból egy éles használatra kész 2.5.0, amely felülírja az előzetes verziót.</span><span class="sxs-lookup"><span data-stu-id="7cde6-109">Using these features, publishers can identify a script as version 2.5.0-alpha, and later release a production-ready version 2.5.0 that supersedes the prerelease version.</span></span>

<span data-ttu-id="7cde6-110">Magas szinten a kiadás előtti parancsfájl szolgáltatásai többek között:</span><span class="sxs-lookup"><span data-stu-id="7cde6-110">At a high level, the prerelease script features include:</span></span>

- <span data-ttu-id="7cde6-111">A verzió-karakterlánc, a parancsfájl-jegyzékfájlban PrereleaseString utótag hozzáadása.</span><span class="sxs-lookup"><span data-stu-id="7cde6-111">Adding a PrereleaseString suffix to the version string in the script manifest.</span></span> <span data-ttu-id="7cde6-112">A PowerShell-galériából való közzétételekor a parancsfájlok, ezeket az adatokat a jegyzékfájl kinyert, és előzetes csomagok azonosítására szolgál.</span><span class="sxs-lookup"><span data-stu-id="7cde6-112">When the scripts is published to the PowerShell Gallery, this data is extracted from the manifest, and used to identify prerelease packages.</span></span>
- <span data-ttu-id="7cde6-113">-AllowPrerelease jelző hozzáadja a PowerShellGet parancsok Find-Script Install-Script előzetes csomagok beszerzése szükséges frissítés-parancsfájl, és a Save-Script.</span><span class="sxs-lookup"><span data-stu-id="7cde6-113">Acquiring prerelease packages requires adding -AllowPrerelease flag to the PowerShellGet commands Find-Script, Install-Script, Update-Script, and Save-Script.</span></span> <span data-ttu-id="7cde6-114">Ha nincs megadva a jelzőt, végleges csomagok nem jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="7cde6-114">If the flag is not specified, prerelease packages will not be shown.</span></span>
- <span data-ttu-id="7cde6-115">A PrereleaseString 2.5.0-alpha hasonlóan a parancsfájl verziója jelenik meg a Find-Script, Get-InstalledScript, és a PowerShell-galériából a fog megjelenni.</span><span class="sxs-lookup"><span data-stu-id="7cde6-115">Script versions displayed by Find-Script, Get-InstalledScript, and in the PowerShell Gallery will be displayed with the PrereleaseString, as in 2.5.0-alpha.</span></span>

<span data-ttu-id="7cde6-116">Szolgáltatások részletei az alábbiakban találhatók.</span><span class="sxs-lookup"><span data-stu-id="7cde6-116">Details for the features are included below.</span></span>

## <a name="identifying-a-script-version-as-a-prerelease"></a><span data-ttu-id="7cde6-117">A szkript verziója azonosítása egy előzetes verzióját</span><span class="sxs-lookup"><span data-stu-id="7cde6-117">Identifying a script version as a prerelease</span></span>

<span data-ttu-id="7cde6-118">A PowerShellGet-támogatás előzetes verzióihoz, mint a modulok parancsfájlok könnyebbé válik.</span><span class="sxs-lookup"><span data-stu-id="7cde6-118">PowerShellGet support for prerelease versions is easier for scripts than modules.</span></span> <span data-ttu-id="7cde6-119">Szkriptet verziószámozása csak támogatja a PowerShellGet, így nincsenek kompatibilitási problémák okozta a megjelenés előtti karakterlánc hozzáadása.</span><span class="sxs-lookup"><span data-stu-id="7cde6-119">Script versioning is only supported by PowerShellGet, so there are no compatibility issues caused by adding the prerelease string.</span></span> <span data-ttu-id="7cde6-120">Egy szkriptet a PowerShell-galériából, mint egy előzetes verzióját az azonosító, a parancsprogram-metaadatait egy megfelelően formázott verzió-karakterlánca előzetes utótagot hozzá.</span><span class="sxs-lookup"><span data-stu-id="7cde6-120">To identify a script in the PowerShell Gallery as a prerelease, add a prerelease suffix to a properly-formatted version string in the script metadata.</span></span>

<span data-ttu-id="7cde6-121">Egy példa a szakasz egy parancsfájl jegyzékfájl az előzetes verzióval a következőhöz hasonlóan néz ki:</span><span class="sxs-lookup"><span data-stu-id="7cde6-121">An example section of a script manifest with a prerelease version would look like the following:</span></span>

```powershell
<#PSScriptInfo

.VERSION 3.2.1-alpha12

.GUID

...

#>
```

<span data-ttu-id="7cde6-122">Előzetes utótag használata, a verzió-karakterlánc az alábbi követelményeknek kell megfelelnie:</span><span class="sxs-lookup"><span data-stu-id="7cde6-122">To use a prerelease suffix, the version string must meet the following requirements:</span></span>

- <span data-ttu-id="7cde6-123">A kiadás előtti utótag csak akkor adható meg, ha a verzió a főverzió.alverzió.build formában 3 szegmenssel.</span><span class="sxs-lookup"><span data-stu-id="7cde6-123">A prerelease suffix may only be specified when the Version is 3 segments for Major.Minor.Build.</span></span>
  <span data-ttu-id="7cde6-124">Ez a SemVer v1.0.0 igazítása</span><span class="sxs-lookup"><span data-stu-id="7cde6-124">This aligns with SemVer v1.0.0</span></span>
- <span data-ttu-id="7cde6-125">Az előzetes utótag egy karakterlánc, amely kötőjellel kezdődik, és előfordulhat, hogy a ASCII és számokat tartalmazhat [0-pedig a 9A-Za - z-]</span><span class="sxs-lookup"><span data-stu-id="7cde6-125">The prerelease suffix is a string which begins with a hyphen, and may contain ASCII alphanumerics [0-9A-Za-z-]</span></span>
- <span data-ttu-id="7cde6-126">Csak SemVer v1.0.0 előzetes karakterláncok támogatott szerepkörönként, ezért az előzetes utótag **nem kell** vagy időszak tartalmazhat vagy + [. +], SemVer 2.0 engedélyezettek, amelyek</span><span class="sxs-lookup"><span data-stu-id="7cde6-126">Only SemVer v1.0.0 prerelease strings are supported at this time, so the prerelease suffix **must not** contain either period or + [.+], which are allowed in SemVer 2.0</span></span>
- <span data-ttu-id="7cde6-127">Néhány példa a támogatott PrereleaseString karakterláncok:-alpha, - α1, – BÉTAVERZIÓ, - update20171020</span><span class="sxs-lookup"><span data-stu-id="7cde6-127">Examples of supported PrereleaseString strings are: -alpha, -alpha1, -BETA, -update20171020</span></span>

### <a name="prerelease-versioning-impact-on-sort-order-and-installation-folders"></a><span data-ttu-id="7cde6-128">Előzetes versioning hatása a rendezési sorrend és a telepítési mappa</span><span class="sxs-lookup"><span data-stu-id="7cde6-128">Prerelease versioning impact on sort order and installation folders</span></span>

<span data-ttu-id="7cde6-129">Rendezési sorrend módosítja, ami fontos a PowerShell-galériából való közzétételkor, előzetes verziójának használata esetén, és a PowerShellGet-parancsokkal parancsfájlok telepítésekor.</span><span class="sxs-lookup"><span data-stu-id="7cde6-129">Sort order changes when using a prerelease version, which is important when publishing to the PowerShell Gallery, and when installing scripts using PowerShellGet commands.</span></span> <span data-ttu-id="7cde6-130">Ha két, parancsfájlok, a verziószámot a verziók találhatók, a rendezési sorrend alapján a kötőjelet a következő karakterlánc része.</span><span class="sxs-lookup"><span data-stu-id="7cde6-130">If two scripts versions with the version number exist, the sort order is based on the string portion following the hyphen.</span></span> <span data-ttu-id="7cde6-131">Tehát verzió 2.5.0-alpha kisebb, mint 2.5.0-beta, amely kisebb, mint 2.5.0-gamma.</span><span class="sxs-lookup"><span data-stu-id="7cde6-131">So, version 2.5.0-alpha is less than 2.5.0-beta, which is less than 2.5.0-gamma.</span></span> <span data-ttu-id="7cde6-132">Ha két parancsfájlt kell ugyanazon a verziószámot, és csak az egyiket egy PrereleaseString, a parancsfájl **nélkül** az előzetes utótag adatforrásmérete az éles használatra kész verziót, és nagyobb, mint az előzetes verzióként rendezése verzió.</span><span class="sxs-lookup"><span data-stu-id="7cde6-132">If two scripts have the same version number, and only one has a PrereleaseString, the script **without** the prerelease suffix is assumed to be the production-ready version and will be sorted as a greater version than the prerelease version.</span></span> <span data-ttu-id="7cde6-133">Tegyük fel, amikor 2.5.0 és 2.5.0-beta, a 2.5.0 összehasonlítása kiadások nagyobb, mint a két verzió akkor minősül.</span><span class="sxs-lookup"><span data-stu-id="7cde6-133">As an example, when comparing releases 2.5.0 and 2.5.0-beta, the 2.5.0 version will be considered the greater of the two.</span></span>

<span data-ttu-id="7cde6-134">A PowerShell-galériából való közzétételkor alapértelmezés szerint a parancsfájl közzétett verzióját kell lennie a nagyobb, mint a korábban közzétett verzió, a PowerShell-galériában található.</span><span class="sxs-lookup"><span data-stu-id="7cde6-134">When publishing to the PowerShell Gallery, by default the version of the script being published must have a greater version than any previously-published version that is in the PowerShell Gallery.</span></span> <span data-ttu-id="7cde6-135">A kiadó. Előfordulhat, hogy frissítéssel verzió 2.5.0-alpha 2.5.0-beta vagy 2.5.0 (az előzetes utótag nélkül).</span><span class="sxs-lookup"><span data-stu-id="7cde6-135">A publisher may update version 2.5.0-alpha with 2.5.0-beta, or with 2.5.0 (with no prerelease suffix).</span></span>

## <a name="finding-and-acquiring-prerelease-packages-using-powershellget-commands"></a><span data-ttu-id="7cde6-136">Keresés és a PowerShellGet-parancsokkal előzetes csomagok beszerzése</span><span class="sxs-lookup"><span data-stu-id="7cde6-136">Finding and acquiring prerelease packages using PowerShellGet commands</span></span>

<span data-ttu-id="7cde6-137">A PowerShellGet Find-Script, Install-Script, frissítési-parancsfájlt, előzetes csomagokat foglalkozó és a Save-Script parancsokat igényel, a - AllowPrerelease jelző hozzáadása.</span><span class="sxs-lookup"><span data-stu-id="7cde6-137">Dealing with prerelease packages using PowerShellGet Find-Script, Install-Script, Update-Script, and Save-Script commands requires adding the -AllowPrerelease flag.</span></span> <span data-ttu-id="7cde6-138">Ha meg van adva a - AllowPrerelease, előzetes csomagokat helyőrzője, ha ilyenek.</span><span class="sxs-lookup"><span data-stu-id="7cde6-138">If -AllowPrerelease is specified, prerelease packages will be included if they are present.</span></span> <span data-ttu-id="7cde6-139">Ha nincs megadva - AllowPrerelease jelző, előzetes csomagokat nem jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="7cde6-139">If -AllowPrerelease flag is not specified, prerelease packages will not be shown.</span></span>

<span data-ttu-id="7cde6-140">Alól kivételt csak a PowerShellGet parancsprogram-utasítások a a következők: Get-InstalledScript és bizonyos esetekben az eltávolítási-szkriptet.</span><span class="sxs-lookup"><span data-stu-id="7cde6-140">The only exceptions to this in the PowerShellGet script commands are Get-InstalledScript, and some cases with Uninstall-Script.</span></span>

- <span data-ttu-id="7cde6-141">Get-InstalledScript mindig automatikusan információk jelennek meg a kiadás előtti verzió-karakterlánca a telepítve, ha.</span><span class="sxs-lookup"><span data-stu-id="7cde6-141">Get-InstalledScript always will automatically show the prerelease information in the version string if it is present.</span></span>
- <span data-ttu-id="7cde6-142">Eltávolítási Parancsprogramja lesz alapértelmezés szerint távolítsa el a legújabb verziót az adott parancsprogramot, ha **nincs verzió** van megadva.</span><span class="sxs-lookup"><span data-stu-id="7cde6-142">Uninstall-Script will by default uninstall the most recent version of a script, if **no version** is specified.</span></span> <span data-ttu-id="7cde6-143">Ezt a viselkedést nem változott.</span><span class="sxs-lookup"><span data-stu-id="7cde6-143">That behavior has not changed.</span></span> <span data-ttu-id="7cde6-144">Azonban ha előzetes verziójának használatával van megadva `-RequiredVersion`, `-AllowPrerelease` lesz szükség.</span><span class="sxs-lookup"><span data-stu-id="7cde6-144">However, if a prerelease version is specified using `-RequiredVersion`, `-AllowPrerelease` will be required.</span></span>

## <a name="examples"></a><span data-ttu-id="7cde6-145">Példák</span><span class="sxs-lookup"><span data-stu-id="7cde6-145">Examples</span></span>

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
    + CategoryInfo          : ObjectNotFound: (Microsoft.Power...ets.FindPackage:FindPackage)[Find-Package], Exception
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

<span data-ttu-id="7cde6-146">Eltávolítási Parancsprogramja parancsfájl jelenlegi verziója eltávolítja, ha a - RequiredVersion nem áll rendelkezésre.</span><span class="sxs-lookup"><span data-stu-id="7cde6-146">Uninstall-Script will remove the current version of a script when -RequiredVersion is not supplied.</span></span>
<span data-ttu-id="7cde6-147">Ha a - RequiredVersion van megadva, és egy előzetes verzióját, - AllowPrerelease hozzá kell adni a parancshoz.</span><span class="sxs-lookup"><span data-stu-id="7cde6-147">If -RequiredVersion is specified, and is a prerelease, -AllowPrerelease must be added to the command.</span></span>

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

## <a name="more-details"></a><span data-ttu-id="7cde6-148">További részletek</span><span class="sxs-lookup"><span data-stu-id="7cde6-148">More details</span></span>

- [<span data-ttu-id="7cde6-149">Előzetes verziója</span><span class="sxs-lookup"><span data-stu-id="7cde6-149">Prerelease Module Versions</span></span>](module-prerelease-support.md)
- [<span data-ttu-id="7cde6-150">Find-script</span><span class="sxs-lookup"><span data-stu-id="7cde6-150">Find-script</span></span>](/powershell/module/powershellget/find-script)
- [<span data-ttu-id="7cde6-151">Install-script</span><span class="sxs-lookup"><span data-stu-id="7cde6-151">Install-script</span></span>](/powershell/module/powershellget/install-script)
- [<span data-ttu-id="7cde6-152">Save-script</span><span class="sxs-lookup"><span data-stu-id="7cde6-152">Save-script</span></span>](/powershell/module/powershellget/save-script)
- [<span data-ttu-id="7cde6-153">Update-script</span><span class="sxs-lookup"><span data-stu-id="7cde6-153">Update-script</span></span>](/powershell/module/powershellget/update-script)
- [<span data-ttu-id="7cde6-154">Get-Installedscript</span><span class="sxs-lookup"><span data-stu-id="7cde6-154">Get-Installedscript</span></span>](/powershell/module/powershellget/get-installedscript)
- [<span data-ttu-id="7cde6-155">UnInstall-script</span><span class="sxs-lookup"><span data-stu-id="7cde6-155">UnInstall-script</span></span>](/powershell/module/powershellget/uninstall-script)
