---
ms.date: 10/17/2017
contributor: keithb
keywords: katalógus, powershell, a parancsmag, psget
title: A parancsfájlok előzetes verziók
ms.openlocfilehash: 14ae1968e5ee73260b6eae05b11185069d047e93
ms.sourcegitcommit: c3f1a83b59484651119630f3089aa51b6e7d4c3c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/26/2018
ms.locfileid: "39268466"
---
# <a name="prerelease-versions-of-scripts"></a>A parancsfájlok előzetes verziók

1.6.0-s verziójának verziótól kezdődően a PowerShellGet és a PowerShell-galériából támogatást nyújt a címkézési egy előzetes verzióját, 1.0.0-esnél újabb verzióiban. Ez a funkció előtt előzetes elemeket a rendszer 0-verzió kezdő járulnia korlátozott. Ezeket a funkciókat az a célja, hogy a szélesebb körű támogatást biztosít [SemVer v1.0.0](http://semver.org/spec/v1.0.0.html) versioning egyezmény visszamenőleges PowerShell verziók 3 és újabb, vagy meglévő a PowerShellGet verzióival való kompatibilitás megszakítása nélkül. Ez a témakör a parancsfájl-specifikus szolgáltatásokra összpontosít. A modulok egyenértékű funkciókra a [Prerelease modulverziók](module-prerelease-support.md) témakör. Használja ezeket a funkciókat, a kiadók is verzió 2.5.0-alpha, a szkriptet azonosító, és később kiadásból egy éles használatra kész 2.5.0, amely felülírja az előzetes verziót.

Magas szinten a kiadás előtti parancsfájl szolgáltatásai többek között:

- A verzió-karakterlánc, a parancsfájl-jegyzékfájlban PrereleaseString utótag hozzáadása. Ha a parancsfájlok tesznek közzé a PowerShell-galériából, ezeket az adatokat a jegyzékfájl kinyert, és előzetes elemek azonosításához használt.
- -AllowPrerelease jelző hozzáadja a PowerShellGet parancsok Find-Script Install-Script előzetes elemek beszerzése szükséges frissítés-parancsfájl, és a Save-Script. Ha nincs megadva a jelzőt, végleges elemek nem jelenik meg.
- A PrereleaseString 2.5.0-alpha hasonlóan a parancsfájl verziója jelenik meg a Find-Script, Get-InstalledScript, és a PowerShell-galériából a fog megjelenni.

Szolgáltatások részletei az alábbiakban találhatók.

## <a name="identifying-a-script-version-as-a-prerelease"></a>A szkript verziója azonosítása egy előzetes verzióját

A PowerShellGet-támogatás előzetes verzióihoz, mint a modulok parancsfájlok könnyebbé válik. Szkriptet verziószámozása csak támogatja a PowerShellGet, így nincsenek kompatibilitási problémák okozta a megjelenés előtti karakterlánc hozzáadása. Egy szkriptet a PowerShell-galériából, mint egy előzetes verzióját az azonosító, a parancsprogram-metaadatait egy megfelelően formázott verzió-karakterlánca előzetes utótagot hozzá.

Egy példa a szakasz egy parancsfájl jegyzékfájl az előzetes verzióval a következőhöz hasonlóan néz ki:

```powershell
<#PSScriptInfo

.VERSION 3.2.1-alpha12

.GUID

...

#>
```

Előzetes utótag használata, a verzió-karakterlánc az alábbi követelményeknek kell megfelelnie:

- A kiadás előtti utótag csak akkor adható meg, ha a verzió a főverzió.alverzió.build formában 3 szegmenssel.
  Ez a SemVer v1.0.0 igazítása
- Az előzetes utótag egy karakterlánc, amely kötőjellel kezdődik, és előfordulhat, hogy a ASCII és számokat tartalmazhat [0-pedig a 9A-Za - z-]
- Csak SemVer v1.0.0 előzetes karakterláncok támogatott szerepkörönként, ezért az előzetes utótag **nem kell** vagy időszak tartalmazhat vagy + [. +], SemVer 2.0 engedélyezettek, amelyek
- Néhány példa a támogatott PrereleaseString karakterláncok:-alpha, - α1, – BÉTAVERZIÓ, - update20171020

### <a name="prerelease-versioning-impact-on-sort-order-and-installation-folders"></a>Előzetes versioning hatása a rendezési sorrend és a telepítési mappa

Rendezési sorrend módosítja, ami fontos a PowerShell-galériából való közzétételkor, előzetes verziójának használata esetén, és a PowerShellGet-parancsokkal parancsfájlok telepítésekor. Ha két, parancsfájlok, a verziószámot a verziók találhatók, a rendezési sorrend alapján a kötőjelet a következő karakterlánc része. Tehát verzió 2.5.0-alpha kisebb, mint 2.5.0-beta, amely kisebb, mint 2.5.0-gamma. Ha két parancsfájlt kell ugyanazon a verziószámot, és csak az egyiket egy PrereleaseString, a parancsfájl **nélkül** az előzetes utótag adatforrásmérete az éles használatra kész verziót, és nagyobb, mint az előzetes verzióként rendezése verzió. Tegyük fel, amikor 2.5.0 és 2.5.0-beta, a 2.5.0 összehasonlítása kiadások nagyobb, mint a két verzió akkor minősül.

A PowerShell-galériából való közzétételkor alapértelmezés szerint a parancsfájl közzétett verzióját kell lennie a nagyobb, mint a korábban közzétett verzió, a PowerShell-galériában található. A kiadó. Előfordulhat, hogy frissítéssel verzió 2.5.0-alpha 2.5.0-beta vagy 2.5.0 (az előzetes utótag nélkül).

## <a name="finding-and-acquiring-prerelease-items-using-powershellget-commands"></a>Keresés és a PowerShellGet-parancsokkal előzetes elemek beolvasása

A PowerShellGet Find-Script, Install-Script, frissítési-parancsfájlt, az előzetes elemekről foglalkozó és a Save-Script parancsokat igényel, a - AllowPrerelease jelző hozzáadása. Ha meg van adva a - AllowPrerelease, előzetes elemek helyőrzője, ha ezek meg adva. Ha - AllowPrerelease jelző nincs megadva, kiadás előtti elemek nem fognak megjelenni.

Alól kivételt csak a PowerShellGet parancsprogram-utasítások a a következők: Get-InstalledScript és bizonyos esetekben az eltávolítási-szkriptet.

- Get-InstalledScript mindig automatikusan információk jelennek meg a kiadás előtti verzió-karakterlánca a telepítve, ha.
- Eltávolítási Parancsprogramja lesz alapértelmezés szerint távolítsa el a legújabb verziót az adott parancsprogramot, ha **nincs verzió** van megadva. Ezt a viselkedést nem változott. Azonban ha előzetes verziójának használatával van megadva `-RequiredVersion`, `-AllowPrerelease` lesz szükség.

## <a name="examples"></a>Példák

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

Eltávolítási Parancsprogramja parancsfájl jelenlegi verziója eltávolítja, ha a - RequiredVersion nem áll rendelkezésre.
Ha a - RequiredVersion van megadva, és egy előzetes verzióját, - AllowPrerelease hozzá kell adni a parancshoz.

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

## <a name="more-details"></a>További részletek

- [Előzetes verziója](module-prerelease-support.md)
- [Find-script](/powershell/module/powershellget/find-script)
- [Install-script](/powershell/module/powershellget/install-script)
- [Save-script](/powershell/module/powershellget/save-script)
- [Frissítés-parancsfájl](/powershell/module/powershellget/update-script)
- [Get-Installedscript](/powershell/module/powershellget/get-installedscript)
- [Eltávolítási parancsprogramja](/powershell/module/powershellget/uninstall-script)