---
ms.date: 10/17/2017
contributor: keithb
ms.topic: reference
keywords: gyűjtemény, a powershell, a parancsmag, a psget
title: PrereleaseScript
ms.openlocfilehash: 575babd6bc373e99a4e924fafef6e9edeec972d4
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="prerelease-versions-of-scripts"></a>Parancsfájlok előzetes verziói

1.6.0 verziójától kezdve, PowerShellGet és a PowerShell-galériában támogatást nyújt a címkézés nagyobb, mint egy előzetes verzióját, 1.0.0 verziók. Ez a szolgáltatás előtt előzetes elemek volt, hogy egy 0 verzió kezdetű korlátozott. Ezeket a szolgáltatásokat az a célja, hogy a szélesebb körű támogatást nyújtanak [SemVer v1.0.0](http://semver.org/spec/v1.0.0.html) versioning egyezmény visszamenőleges verzióival való kompatibilitás PowerShell verziók 3 és újabb, vagy meglévő PowerShellGet megszakítása nélkül.
Ez a témakör a parancsfájl-specifikus szolgáltatásokra összpontosít. A modulok egyenértékű szolgáltatások szerepelnek a [előzetes verziója](../module/PrereleaseModule.md) témakör. Használja ezeket a funkciókat, közzétevők is azonosíthatja verzió 2.5.0-alpha egy parancsfájlt, és később kiadásból egy éles használatra kész 2.5.0, amely felülírja az előzetes verziót.

Magas szinten a kiadás előtti parancsprogrammal kapcsolatos funkciói a következők:

* Egy PrereleaseString utótagot ad hozzá a parancsfájl jegyzékfájl verzió-karakterlánca.
Amikor a parancsfájlok közzé van téve a PowerShell-galériában, ezeket az adatokat a jegyzék kinyert, és előzetes elemek azonosítására szolgál.
* -AllowPrerelease jelző ad hozzá a PowerShellGet parancsok keresése-parancsfájl, Install-parancsfájl, előzetes elemek beszerzése szükséges frissítés-parancsfájl, és a Mentés-parancsfájl.
Ha a jelző nincs megadva, az előzetes elemek nem jelenik meg.
* A PrereleaseString 2.5.0-alpha hasonlóan jelenik meg a keresés-parancsfájl, a Get-InstalledScript, és a PowerShell-galériában parancsfájl verziók jelenik.

A szolgáltatások részleteit az alábbiakban találhatók.


## <a name="identifying-a-script-version-as-a-prerelease"></a>A parancsfájl verziója egy előzetes verzióját azonosítása

Előzetes verziói PowerShellGet támogatása még parancsfájlok könnyebb modulok.
Parancsfájl versioning csak akkor támogatott PowerShellGet, ezért jelenleg nincs kompatibilitási probléma hozzáadása az előzetes karakterlánc miatt.
Egy megfelelően formázott verzió-karakterláncot a parancsprogram-metaadatait az előzetes utótag hozzáadása a egy előzetes verzióját, a PowerShell-galériában parancsfájl azonosításához.

Egy példa a szakasz egy parancsfájl jegyzékfájl előzetes verziójának a következőhöz hasonló a következő:
```powershell
<#PSScriptInfo

.VERSION 3.2.1-alpha12

.GUID

...

#>

```

Előzetes utótagot használja, a verzió-karakterláncnak a következő követelményeknek kell megfelelnie:

* Előzetes utótag csak akkor adható meg, ha a verzió a Major.Minor.Build 3 szegmensek. Ez SemVer v1.0.0 igazodik
* Az előzetes utótag egy karakterlánc, amely kötőjellel kezdődik, és tartalmazhat ASCII számok és betűk [0-9A-Za - z-]
* Csak SemVer v1.0.0 előzetes karakterláncok használata támogatott jelenleg, ezért az előzetes utótag __nem kell__ vagy időszak tartalmaz vagy + [. +], amelyek használata engedélyezett SemVer 2.0
* Támogatott PrereleaseString egységmeghatározást:-alpha, - α1,-BETA, - update20171020

__Előzetes versioning hatása a rendezési sorrend és a telepítési mappa__

Rendezési sorrend megváltozik, ha előzetes verzióját, akkor fontos, amikor a PowerShell-galériában közzététele, amely használja PowerShellGet parancsokkal parancsfájlok telepítésekor.
Ha két a parancsfájlok a verziószámú verzió található, a rendezési sorrend alapján a következő a kötőjel karakterláncra vonatkozó részében. Igen verziója 2.5.0-alpha nem éri el 2.5.0-beta, ez pedig kisebb, mint 2.5.0-gamma.
Ha két parancsfájlok azonos verziószámát, és csak egy PrereleaseString, a parancsfájl nincs __nélkül__ az előzetes utótag feltételezett, hogy az éles használatra kész verzió, és nagyobb, mint előzetes verzióként rendezése történik verzió.
Tegyük fel, amikor 2.5.0 és 2.5.0-beta, a 2.5.0 összehasonlításával kiadott verzióját akkor veszi figyelembe a két nagyobb.

A PowerShell-galériában való közzétételkor alapértelmezés szerint a közzétett parancsfájl verziója kell lennie a nagyobb, mint a korábban közzétett verziót a PowerShell-galériában.
A közzétevő módosíthatjuk verzió 2.5.0-alpha 2.5.0-beta vagy 2.5.0 (utótaggal nincs előzetes).

## <a name="finding-and-acquiring-prerelease-items-using-powershellget-commands"></a>Keresés és PowerShellGet parancsokkal előzetes elemek beszerzése

Előzetes elemek PowerShellGet keresés-parancsfájlból Install-, frissítés-parancsfájl használatával foglalkozó és mentés-parancsprogram-utasítások szükséges a - AllowPrerelease jelző hozzáadása.
Ha - AllowPrerelease meg van adva, előzetes elemek is fog szerepelni, ha ilyenek.
Ha - AllowPrerelease jelző nincs megadva, az előzetes elemek nem jelenik meg.

Az egyetlen kivétel ez alól a PowerShellGet parancsprogram-utasítások a a következők: Get-InstalledScript és bizonyos esetekben az Uninstall-parancsfájl.

* Get-InstalledScript mindig automatikusan információk jelennek meg az előzetes verzió-karakterlánca a ha telepítve.
* Távolítsa el parancsfájl alapértelmezés szerint eltávolítja a legfrissebb egy parancsfájlt, ha __megszűnik__ van megadva. Ezt a viselkedést nem változott. Azonban ha - RequiredVersion, adott előzetes verziójának - AllowPrerelease lesz szükség.

## <a name="examples"></a>Példák
```powershell
# Assume the PowerShell Gallery has TestPackage versions 1.8.0 and 1.9.0-alpha. If -AllowPrerelease is not specified, only version 1.8.0 will be returned.
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

Eltávolítása parancsfájl eltávolítja a jelenlegi verziója egy parancsfájlt, amikor - RequiredVersion nem.
Ha - RequiredVersion van megadva, és egy előzetes verzióját, a parancs - AllowPrerelease kell adni.

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



## <a name="more-details"></a>További részletekért
### <a name="prerelease-module-versionsmoduleprereleasemodulemd"></a>[Előzetes verziója](../module/PrereleaseModule.md)
### <a name="find-scriptpsgetfind-scriptmd"></a>[Keresés – parancsprogram](./psget_find-script.md)
### <a name="install-scriptpsgetinstall-scriptmd"></a>[Install-script](./psget_install-script.md)
### <a name="save-scriptpsgetsave-scriptmd"></a>[Save-script](./psget_save-script.md)
### <a name="update-scriptpsgetupdate-scriptmd"></a>[Frissítés-parancsfájl](./psget_update-script.md)
### <a name="get-installedscriptpsgetget-installedscriptmd"></a>[Get-Installedscript](./psget_get-installedscript.md)
### <a name="uninstall-scriptpsgetuninstall-scriptmd"></a>[UnInstall-script](./psget_uninstall-script.md)