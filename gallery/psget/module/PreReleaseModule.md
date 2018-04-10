---
ms.date: 09/26/2017
contributor: keithb
ms.topic: reference
keywords: gyűjtemény, a powershell, a parancsmag, a psget
title: PrereleaseModule
ms.openlocfilehash: 1fc08cbba90e3eb8ca7d280e4d279af1d8aa279f
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="prerelease-module-versions"></a><span data-ttu-id="beafd-103">Előzetes verziója</span><span class="sxs-lookup"><span data-stu-id="beafd-103">Prerelease Module Versions</span></span>
<span data-ttu-id="beafd-104">1.6.0 verziójától kezdve, PowerShellGet és a PowerShell-galériában támogatást nyújt a címkézés nagyobb, mint egy előzetes verzióját, 1.0.0 verziók.</span><span class="sxs-lookup"><span data-stu-id="beafd-104">Starting with version 1.6.0, PowerShellGet and the PowerShell Gallery provide support for tagging versions greater than 1.0.0 as a prerelease.</span></span> <span data-ttu-id="beafd-105">Ez a szolgáltatás előtt előzetes elemek volt, hogy egy 0 verzió kezdetű korlátozott.</span><span class="sxs-lookup"><span data-stu-id="beafd-105">Prior to this feature, prerelease items were limited to having a version beginning with 0.</span></span> <span data-ttu-id="beafd-106">Ezeket a szolgáltatásokat az a célja, hogy a szélesebb körű támogatást nyújtanak [SemVer v1.0.0](http://semver.org/spec/v1.0.0.html) versioning egyezmény visszamenőleges verzióival való kompatibilitás PowerShell verziók 3 és újabb, vagy meglévő PowerShellGet megszakítása nélkül.</span><span class="sxs-lookup"><span data-stu-id="beafd-106">The goal of these features is to provide greater support for [SemVer v1.0.0](http://semver.org/spec/v1.0.0.html) versioning convention without breaking backwards compatibility with PowerShell versions 3 and above, or existing versions of PowerShellGet.</span></span> <span data-ttu-id="beafd-107">Ez a témakör a modul-specifikus szolgáltatásokra összpontosít.</span><span class="sxs-lookup"><span data-stu-id="beafd-107">This topic focuses on the module-specific features.</span></span> <span data-ttu-id="beafd-108">A parancsfájlok egyenértékű funkciók vannak a [parancsfájlok előzetes verziók](../script/PrereleaseScript.md) témakör.</span><span class="sxs-lookup"><span data-stu-id="beafd-108">The equivalent features for scripts are in the [Prerelease Versions of Scripts](../script/PrereleaseScript.md) topic.</span></span> <span data-ttu-id="beafd-109">Használja ezeket a funkciókat, közzétevők is azonosíthatja a modul vagy a verziójával 2.5.0-alpha-parancsprogramot, és később kiadásból egy éles használatra kész 2.5.0, amely felülírja az előzetes verziót.</span><span class="sxs-lookup"><span data-stu-id="beafd-109">Using these features, publishers can identify a module or script as version 2.5.0-alpha, and later release a production-ready version 2.5.0 that supersedes the prerelease version.</span></span>

<span data-ttu-id="beafd-110">Magas szinten a modul előzetes funkciók a következők:</span><span class="sxs-lookup"><span data-stu-id="beafd-110">At a high level, the prerelease module features include:</span></span>

* <span data-ttu-id="beafd-111">Előzetes karakterláncnak a moduljegyzékben PSData szakaszába azonosítja a modul előzetes verzióként.</span><span class="sxs-lookup"><span data-stu-id="beafd-111">Adding a Prerelease string to the PSData section of the module manifest identifies the module as a prerelease version.</span></span>
<span data-ttu-id="beafd-112">Amikor a modul közzé van téve a PowerShell-galériában, ezeket az adatokat a jegyzék kinyert, és előzetes elemek azonosítására szolgál.</span><span class="sxs-lookup"><span data-stu-id="beafd-112">When the module is published to the PowerShell Gallery, this data is extracted from the manifest, and used to identify prerelease items.</span></span>
* <span data-ttu-id="beafd-113">-AllowPrerelease jelző ad hozzá a PowerShellGet parancsok keresése-modul, Install-modul, előzetes elemek beszerzése szükséges frissítés-, és mentés-modul.</span><span class="sxs-lookup"><span data-stu-id="beafd-113">Acquiring prerelease items requires adding -AllowPrerelease flag to the PowerShellGet commands Find-Module, Install-Module, Update-Module, and Save-Module.</span></span>
<span data-ttu-id="beafd-114">Ha a jelző nincs megadva, az előzetes elemek nem jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="beafd-114">If the flag is not specified, prerelease items will not be shown.</span></span>
* <span data-ttu-id="beafd-115">Megjelenik a keresés-modul, a Get-InstalledModule, és a PowerShell-galériában verziója lesz hozzáfűzve, mint 2.5.0-alpha előzetes karakterlánccal egyetlen karakterláncként jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="beafd-115">Module versions displayed by Find-Module, Get-InstalledModule, and in the PowerShell Gallery will be displayed as a single string with the Prerelease string appended, as in 2.5.0-alpha.</span></span>

<span data-ttu-id="beafd-116">A szolgáltatások részleteit az alábbiakban találhatók.</span><span class="sxs-lookup"><span data-stu-id="beafd-116">Details for the features are included below.</span></span>

<span data-ttu-id="beafd-117">Ezek a változások nem befolyásolják a PowerShell beépített modul verzióinak támogatása, és kompatibilisek a PowerShell 3.0-s, 4.0 és 5.</span><span class="sxs-lookup"><span data-stu-id="beafd-117">These changes do not affect the module version support that is built into PowerShell, and are compatible with PowerShell 3.0, 4.0, and 5.</span></span>

## <a name="identifying-a-module-version-as-a-prerelease"></a><span data-ttu-id="beafd-118">A modul verziója egy előzetes verzióját azonosítása</span><span class="sxs-lookup"><span data-stu-id="beafd-118">Identifying a module version as a prerelease</span></span>

<span data-ttu-id="beafd-119">Előzetes verziói PowerShellGet támogatása a modul jegyzékfájlja belül két mező használatát igényli:</span><span class="sxs-lookup"><span data-stu-id="beafd-119">PowerShellGet support for prerelease versions requires the use of two fields within the Module Manifest:</span></span>

* <span data-ttu-id="beafd-120">Ha előzetes verzióját használja, és meg kell felelniük a meglévő PowerShell versioning, szerepel a moduljegyzékben ModuleVersion 3 részből verziónak kell lennie.</span><span class="sxs-lookup"><span data-stu-id="beafd-120">The ModuleVersion included in the module manifest must be a 3-part version if a prerelease version is used, and must comply with existing PowerShell versioning.</span></span> <span data-ttu-id="beafd-121">A verzió formátum A.B.C, amelyben A, B és C is minden egész számok lenne.</span><span class="sxs-lookup"><span data-stu-id="beafd-121">The version format would be A.B.C, where A, B, and C are all integers.</span></span>
* <span data-ttu-id="beafd-122">Az előzetes karakterlánc van megadva a moduljegyzékben PrivateData PSData szakaszában.</span><span class="sxs-lookup"><span data-stu-id="beafd-122">The Prerelease string is specified in the module manifest, in the PSData section of PrivateData.</span></span>
<span data-ttu-id="beafd-123">Részletes követelményeket az előzetes karakterlánc alatt van.</span><span class="sxs-lookup"><span data-stu-id="beafd-123">Detailed requirements on the Prerelease string are below.</span></span>

<span data-ttu-id="beafd-124">Egy példa része egy moduljegyzék, amely meghatározza egy modul, egy előzetes verzióját a következő lenne:</span><span class="sxs-lookup"><span data-stu-id="beafd-124">An example section of a module manifest that defines a module as a prerelease would look like the following:</span></span>
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

<span data-ttu-id="beafd-125">A kiadás előtti karakterlánc részletes követelményei a következők:</span><span class="sxs-lookup"><span data-stu-id="beafd-125">The detailed requirements for Prerelease string are:</span></span>

* <span data-ttu-id="beafd-126">Előzetes karakterlánc csak a ModuleVersion Major.Minor.Build 3 szegmensek esetén adható meg.</span><span class="sxs-lookup"><span data-stu-id="beafd-126">Prerelease string may only be specified when the ModuleVersion is 3 segments for Major.Minor.Build.</span></span> <span data-ttu-id="beafd-127">Ez SemVer v1.0.0 igazodik.</span><span class="sxs-lookup"><span data-stu-id="beafd-127">This aligns with SemVer v1.0.0.</span></span>
* <span data-ttu-id="beafd-128">Kötőjel az elválasztó buildszámának és az előzetes karakterlánc között.</span><span class="sxs-lookup"><span data-stu-id="beafd-128">A hyphen is the delimiter between the Build number and the Prerelease string.</span></span> <span data-ttu-id="beafd-129">Kötőjel szerepelni fog az előzetes karakterlánc az első karakter, csak.</span><span class="sxs-lookup"><span data-stu-id="beafd-129">A hyphen may be included in the Prerelease string as the first character, only.</span></span>
* <span data-ttu-id="beafd-130">Az előzetes karakterlánc csak ASCII számok és betűk is tartalmazhat [0-9A-Za - z-].</span><span class="sxs-lookup"><span data-stu-id="beafd-130">The Prerelease string may contain only ASCII alphanumerics [0-9A-Za-z-].</span></span> <span data-ttu-id="beafd-131">Ajánlott eljárás az előzetes megkezdéséhez alfanumerikus karakter, string, egyszerűbb azonosítani, hogy ez egy előzetes verziójának a elemek listájának beolvasásakor lesz.</span><span class="sxs-lookup"><span data-stu-id="beafd-131">It is a best practice to begin the Prerelease string with an alpha character, as it will be easier to identify that this is a prerelease version when scanning a list of items.</span></span>
* <span data-ttu-id="beafd-132">Csak SemVer v1.0.0 előzetes karakterláncok jelenleg támogatottak.</span><span class="sxs-lookup"><span data-stu-id="beafd-132">Only SemVer v1.0.0 prerelease strings are supported at this time.</span></span> <span data-ttu-id="beafd-133">Előzetes karakterlánc __nem kell__ vagy időszak tartalmaz vagy + [. +], amely SemVer 2.0 engedélyezettek.</span><span class="sxs-lookup"><span data-stu-id="beafd-133">Prerelease string __must not__ contain either period or + [.+], which are allowed in SemVer 2.0.</span></span>
* <span data-ttu-id="beafd-134">A támogatott előzetes karakterlánc például a következők:-alpha, - α1,-BETA, - update20171020</span><span class="sxs-lookup"><span data-stu-id="beafd-134">Examples of supported Prerelease string are: -alpha, -alpha1, -BETA, -update20171020</span></span>

<span data-ttu-id="beafd-135">__Előzetes versioning hatása a rendezési sorrend és a telepítési mappa__</span><span class="sxs-lookup"><span data-stu-id="beafd-135">__Prerelease versioning impact on sort order and installation folders__</span></span>

<span data-ttu-id="beafd-136">Rendezési sorrend megváltozik, ha előzetes verzióját, akkor fontos, amikor a PowerShell-galériában közzététele, amely használja PowerShellGet parancsokkal modulok telepítésekor.</span><span class="sxs-lookup"><span data-stu-id="beafd-136">Sort order changes when using a prerelease version, which is important when publishing to the PowerShell Gallery, and when installing modules using PowerShellGet commands.</span></span>
<span data-ttu-id="beafd-137">Az előzetes karakterlánc két modulok, a rendezési sorrend a következő a kötőjel karakterláncra vonatkozó részében alapul.</span><span class="sxs-lookup"><span data-stu-id="beafd-137">If the Prerelease string is specified for two modules, the sort order is based on the string portion following the hyphen.</span></span> <span data-ttu-id="beafd-138">Igen verziója 2.5.0-alpha nem éri el 2.5.0-beta, ez pedig kisebb, mint 2.5.0-gamma.</span><span class="sxs-lookup"><span data-stu-id="beafd-138">So, version 2.5.0-alpha is less than 2.5.0-beta, which is less than 2.5.0-gamma.</span></span>
<span data-ttu-id="beafd-139">Ha két modulok az azonos ModuleVersion, és csak egy előzetes karakterlánccal rendelkezik, a modul nélkül a előzetes karakterlánc feltételezett, hogy az éles használatra kész verzió-e, és nagyobb, mint az előzetes verziót (amelynek része az előzetes verzióként rendezése történik (karakterlánc).</span><span class="sxs-lookup"><span data-stu-id="beafd-139">If two modules have the same ModuleVersion, and only one has a Prerelease string, the module without the Prerelease string is assumed to be the production-ready version and will be sorted as a greater version than the prerelease version (which includes the Prerelease string).</span></span>
<span data-ttu-id="beafd-140">Tegyük fel, amikor 2.5.0 és 2.5.0-beta, a 2.5.0 összehasonlításával kiadott verzióját akkor veszi figyelembe a két nagyobb.</span><span class="sxs-lookup"><span data-stu-id="beafd-140">As an example, when comparing releases 2.5.0 and 2.5.0-beta, the 2.5.0 version will be considered the greater of the two.</span></span>

<span data-ttu-id="beafd-141">A PowerShell-galériában való közzétételkor alapértelmezés szerint a modul közzétett verziója kell lennie a nagyobb, mint a korábban közzétett verziót a PowerShell-galériában.</span><span class="sxs-lookup"><span data-stu-id="beafd-141">When publishing to the PowerShell Gallery, by default the version of the module being published must have a greater version than any previously-published version that is in the PowerShell Gallery.</span></span>

## <a name="finding-and-acquiring-prerelease-items-using-powershellget-commands"></a><span data-ttu-id="beafd-142">Keresés és PowerShellGet parancsokkal előzetes elemek beszerzése</span><span class="sxs-lookup"><span data-stu-id="beafd-142">Finding and acquiring prerelease items using PowerShellGet commands</span></span>

<span data-ttu-id="beafd-143">PowerShellGet keresés-modul, a telepítés-modul, a frissítés-modul, az előzetes elemekről foglalkozó és mentés-modul parancsokat igényel, a - AllowPrerelease jelző hozzáadása.</span><span class="sxs-lookup"><span data-stu-id="beafd-143">Dealing with prerelease items using PowerShellGet Find-Module, Install-Module, Update-Module, and Save-Module commands requires adding the -AllowPrerelease flag.</span></span>
<span data-ttu-id="beafd-144">Ha - AllowPrerelease meg van adva, előzetes elemek is fog szerepelni, ha ilyenek.</span><span class="sxs-lookup"><span data-stu-id="beafd-144">If -AllowPrerelease is specified, prerelease items will be included if they are present.</span></span>
<span data-ttu-id="beafd-145">Ha - AllowPrerelease jelző nincs megadva, az előzetes elemek nem jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="beafd-145">If -AllowPrerelease flag is not specified, prerelease items will not be shown.</span></span>

<span data-ttu-id="beafd-146">Az egyetlen kivétel ez alól Ez a PowerShellGet modul parancsok a következők: Get-InstalledModule és bizonyos esetekben az Uninstall-modul.</span><span class="sxs-lookup"><span data-stu-id="beafd-146">The only exceptions to this in the PowerShellGet module commands are Get-InstalledModule, and some cases with Uninstall-Module.</span></span>

* <span data-ttu-id="beafd-147">Get-InstalledModule mindig automatikusan információk jelennek meg az előzetes verzió-karakterlánca a modulok a.</span><span class="sxs-lookup"><span data-stu-id="beafd-147">Get-InstalledModule always will automatically show the prerelease information in the version string for modules.</span></span>
* <span data-ttu-id="beafd-148">Távolítsa el modul alapértelmezés szerint eltávolítja a legfrissebb egy modult, ha __megszűnik__ van megadva.</span><span class="sxs-lookup"><span data-stu-id="beafd-148">Uninstall-Module will by default uninstall the most recent version of a module, if __no version__ is specified.</span></span> <span data-ttu-id="beafd-149">Ezt a viselkedést nem változott.</span><span class="sxs-lookup"><span data-stu-id="beafd-149">That behavior has not changed.</span></span> <span data-ttu-id="beafd-150">Azonban ha - RequiredVersion, adott előzetes verziójának - AllowPrerelease lesz szükség.</span><span class="sxs-lookup"><span data-stu-id="beafd-150">However, if a prerelease version is specified using -RequiredVersion, -AllowPrerelease will be required.</span></span>

## <a name="examples"></a><span data-ttu-id="beafd-151">Példák</span><span class="sxs-lookup"><span data-stu-id="beafd-151">Examples</span></span>
```powershell
# Assume the PowerShell Gallery has TestPackage module versions 1.8.0 and 1.9.0-alpha. If -AllowPrerelease is not specified, only version 1.8.0 will be returned.
C:\windows\system32> find-module TestPackage

Version        Name                                Repository           Description
-------        ----                                ----------           -----------
1.8.0          TestPackage                         PSGallery            Package used to validate changes to the PowerShe...

C:\windows\system32> find-module TestPackage -AllowPrerelease

Version        Name                                Repository           Description
-------        ----                                ----------           -----------
1.9.0-alpha    TestPackage                         PSGallery            Package used to validate changes to the PowerShe...

# To install a prerelease, always specify -AllowPrerelease. Specifying a prerelease version string is not sufficient.

C:\windows\system32> Install-module TestPackage -RequiredVersion 1.9.0-alpha
PackageManagement\Find-Package : No match was found for the specified search criteria and module name 'TestPackage'.
Try Get-PSRepository to see all available registered module repositories.
At C:\Program Files\WindowsPowerShell\Modules\PowerShellGet\1.6.0\PSModule.psm1:1455 char:3
+         PackageManagement\Find-Package @PSBoundParameters | Microsoft ...
+         ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : ObjectNotFound: (Microsoft.Power...ets.FindPackage:FindPackage) [Find-Package], Exceptio
   n
    + FullyQualifiedErrorId : NoMatchFoundForCriteria,Microsoft.PowerShell.PackageManagement.Cmdlets.FindPackage

# The previous command failed because -AllowPrerelease was not specified.
# Adding -AllowPrerelease will result in success.

C:\windows\system32> Install-module TestPackage -RequiredVersion 1.9.0-alpha -AllowPrerelease
C:\windows\system32> Get-InstalledModule TestPackage

Version         Name                                Repository           Description
-------         ----                                ----------           -----------
1.9.0-alpha     TestPackage                         PSGallery            Package used to validate changes to the PowerShe...

```

<span data-ttu-id="beafd-152">A modul csak a megadott előzetes miatt eltérőek-verziók egymás melletti telepítése nem támogatott.</span><span class="sxs-lookup"><span data-stu-id="beafd-152">Side-by-side installation of versions of a module that differ only due to the prerelease specified is not supported.</span></span>
<span data-ttu-id="beafd-153">PowerShellGet használatával modul telepítésekor ugyanabban a modulban különböző verzióinak egymás melletti telepített hozzon létre egy mappa nevét a ModuleVersion.</span><span class="sxs-lookup"><span data-stu-id="beafd-153">When installing a module using PowerShellGet, different versions of the same module are installed side-by-side by creating a folder name using the ModuleVersion.</span></span>
<span data-ttu-id="beafd-154">A mappa nevét a ModuleVersion az előzetes karakterlánc nélkül használható.</span><span class="sxs-lookup"><span data-stu-id="beafd-154">The ModuleVersion, without the prerelease string, is used for the folder name.</span></span>
<span data-ttu-id="beafd-155">Ha a felhasználó telepít MyModule verzió 2.5.0-alpha, azt a MyModule\2.5.0 mappába telepíti.</span><span class="sxs-lookup"><span data-stu-id="beafd-155">If a user installs MyModule version 2.5.0-alpha, it will be installed to the MyModule\2.5.0 folder.</span></span>
<span data-ttu-id="beafd-156">Ha a felhasználó 2.5.0-beta telepíti, a 2.5.0-beta verziót fogja __túlzott írási__ MyModule\2.5.0 mappa tartalmát.</span><span class="sxs-lookup"><span data-stu-id="beafd-156">If the user then installs 2.5.0-beta, the 2.5.0-beta version will __over-write__ the contents of the folder MyModule\2.5.0.</span></span>
<span data-ttu-id="beafd-157">Egy ezt a megközelítést előnye, hogy nincs szükség az eltávolítási az előzetes verziót az éles használatra kész verzió telepítése után.</span><span class="sxs-lookup"><span data-stu-id="beafd-157">One advantage to this approach is that there is no need to un-install the prerelease version after installing the production-ready version.</span></span>
<span data-ttu-id="beafd-158">Az alábbi példa bemutatja, mi történik:</span><span class="sxs-lookup"><span data-stu-id="beafd-158">The example below shows what to expect:</span></span>


``` powershell
C:\windows\system32> Get-InstalledModule TestPackage -AllVersions

Version         Name                                Repository           Description
-------         ----                                ----------           -----------
1.9.0-alpha     TestPackage                         PSGallery            Package used to validate changes to the PowerShe...
1.8.0           TestPackage                         PSGallery            Package used to validate changes to the PowerShe...
1.1.3.2         TestPackage                         PSGallery            Package used to validate changes to the PowerShe...

C:\windows\system32> find-module TestPackage -AllowPrerelease

Version        Name                                Repository           Description
-------        ----                                ----------           -----------
1.9.0-beta     TestPackage                         PSGallery            Package used to validate changes to the PowerShe...

C:\windows\system32> Update-Module TestPackage -AllowPrerelease
C:\windows\system32> Get-InstalledModule TestPackage -AllVersions

Version         Name                                Repository           Description
-------         ----                                ----------           -----------
1.9.0-beta      TestPackage                         PSGallery            Package used to validate changes to the PowerShe...
1.8.0           TestPackage                         PSGallery            Package used to validate changes to the PowerShe...
1.1.3.2         TestPackage                         PSGallery            Package used to validate changes to the PowerShe...

```

<span data-ttu-id="beafd-159">Modul eltávolítása eltávolítja a legújabb verzióra a modulok, amikor - RequiredVersion nem.</span><span class="sxs-lookup"><span data-stu-id="beafd-159">Uninstall-Module will remove the latest version of a module when -RequiredVersion is not supplied.</span></span>
<span data-ttu-id="beafd-160">Ha - RequiredVersion van megadva, és egy előzetes verzióját, a parancs - AllowPrerelease kell adni.</span><span class="sxs-lookup"><span data-stu-id="beafd-160">If -RequiredVersion is specified, and is a prerelease, -AllowPrerelease must be added to the command.</span></span>

``` powershell
C:\windows\system32> Get-InstalledModule TestPackage -AllVersions

Version         Name                                Repository           Description
-------         ----                                ----------           -----------
2.0.0-alpha1    TestPackage                         PSGallery            Package used to validate changes to the PowerShe...
1.9.0-beta      TestPackage                         PSGallery            Package used to validate changes to the PowerShe...
1.8.0           TestPackage                         PSGallery            Package used to validate changes to the PowerShe...
1.1.3.2         TestPackage                         PSGallery            Package used to validate changes to the PowerShe...

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

Version         Name                                Repository           Description
-------         ----                                ----------           -----------
2.0.0-alpha1    TestPackage                         PSGallery            Package used to validate changes to the PowerShe...
1.8.0           TestPackage                         PSGallery            Package used to validate changes to the PowerShe...
1.1.3.2         TestPackage                         PSGallery            Package used to validate changes to the PowerShe...

C:\windows\system32> Uninstall-Module TestPackage
C:\windows\system32> Get-InstalledModule TestPackage -AllVersions

Version         Name                                Repository           Description
-------         ----                                ----------           -----------
1.8.0           TestPackage                         PSGallery            Package used to validate changes to the PowerShe...
1.1.3.2         TestPackage                         PSGallery            Package used to validate changes to the PowerShe...


```



## <a name="more-details"></a><span data-ttu-id="beafd-161">További részletekért</span><span class="sxs-lookup"><span data-stu-id="beafd-161">More details</span></span>
### <a name="prerelease-script-versionsscriptprereleasescriptmd"></a>[<span data-ttu-id="beafd-162">Kiadás előtti parancsfájl-verziók</span><span class="sxs-lookup"><span data-stu-id="beafd-162">Prerelease Script Versions</span></span>](../script/PrereleaseScript.md)
### <a name="find-modulepsgetfind-modulemd"></a>[<span data-ttu-id="beafd-163">A modul keresése</span><span class="sxs-lookup"><span data-stu-id="beafd-163">Find-Module</span></span>](./psget_find-module.md)
### <a name="install-modulepsgetinstall-modulemd"></a>[<span data-ttu-id="beafd-164">Install-modul</span><span class="sxs-lookup"><span data-stu-id="beafd-164">Install-Module</span></span>](./psget_install-module.md)
### <a name="save-modulepsgetsave-modulemd"></a>[<span data-ttu-id="beafd-165">Save-Module</span><span class="sxs-lookup"><span data-stu-id="beafd-165">Save-Module</span></span>](./psget_save-module.md)
### <a name="update-modulepsgetupdate-modulemd"></a>[<span data-ttu-id="beafd-166">Update-Module</span><span class="sxs-lookup"><span data-stu-id="beafd-166">Update-Module</span></span>](./psget_update-module.md)
### <a name="get-installedmodulepsgetget-installedmodulemd"></a>[<span data-ttu-id="beafd-167">Get-InstalledModule</span><span class="sxs-lookup"><span data-stu-id="beafd-167">Get-InstalledModule</span></span>](./psget_get-installedmodule.md)
### <a name="uninstall-modulepsgetuninstall-modulemd"></a>[<span data-ttu-id="beafd-168">Távolítsa el modul</span><span class="sxs-lookup"><span data-stu-id="beafd-168">UnInstall-Module</span></span>](./psget_uninstall-module.md)