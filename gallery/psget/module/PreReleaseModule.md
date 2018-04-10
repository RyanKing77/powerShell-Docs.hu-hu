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
# <a name="prerelease-module-versions"></a>Előzetes verziója
1.6.0 verziójától kezdve, PowerShellGet és a PowerShell-galériában támogatást nyújt a címkézés nagyobb, mint egy előzetes verzióját, 1.0.0 verziók. Ez a szolgáltatás előtt előzetes elemek volt, hogy egy 0 verzió kezdetű korlátozott. Ezeket a szolgáltatásokat az a célja, hogy a szélesebb körű támogatást nyújtanak [SemVer v1.0.0](http://semver.org/spec/v1.0.0.html) versioning egyezmény visszamenőleges verzióival való kompatibilitás PowerShell verziók 3 és újabb, vagy meglévő PowerShellGet megszakítása nélkül. Ez a témakör a modul-specifikus szolgáltatásokra összpontosít. A parancsfájlok egyenértékű funkciók vannak a [parancsfájlok előzetes verziók](../script/PrereleaseScript.md) témakör. Használja ezeket a funkciókat, közzétevők is azonosíthatja a modul vagy a verziójával 2.5.0-alpha-parancsprogramot, és később kiadásból egy éles használatra kész 2.5.0, amely felülírja az előzetes verziót.

Magas szinten a modul előzetes funkciók a következők:

* Előzetes karakterláncnak a moduljegyzékben PSData szakaszába azonosítja a modul előzetes verzióként.
Amikor a modul közzé van téve a PowerShell-galériában, ezeket az adatokat a jegyzék kinyert, és előzetes elemek azonosítására szolgál.
* -AllowPrerelease jelző ad hozzá a PowerShellGet parancsok keresése-modul, Install-modul, előzetes elemek beszerzése szükséges frissítés-, és mentés-modul.
Ha a jelző nincs megadva, az előzetes elemek nem jelenik meg.
* Megjelenik a keresés-modul, a Get-InstalledModule, és a PowerShell-galériában verziója lesz hozzáfűzve, mint 2.5.0-alpha előzetes karakterlánccal egyetlen karakterláncként jelenik meg.

A szolgáltatások részleteit az alábbiakban találhatók.

Ezek a változások nem befolyásolják a PowerShell beépített modul verzióinak támogatása, és kompatibilisek a PowerShell 3.0-s, 4.0 és 5.

## <a name="identifying-a-module-version-as-a-prerelease"></a>A modul verziója egy előzetes verzióját azonosítása

Előzetes verziói PowerShellGet támogatása a modul jegyzékfájlja belül két mező használatát igényli:

* Ha előzetes verzióját használja, és meg kell felelniük a meglévő PowerShell versioning, szerepel a moduljegyzékben ModuleVersion 3 részből verziónak kell lennie. A verzió formátum A.B.C, amelyben A, B és C is minden egész számok lenne.
* Az előzetes karakterlánc van megadva a moduljegyzékben PrivateData PSData szakaszában.
Részletes követelményeket az előzetes karakterlánc alatt van.

Egy példa része egy moduljegyzék, amely meghatározza egy modul, egy előzetes verzióját a következő lenne:
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

A kiadás előtti karakterlánc részletes követelményei a következők:

* Előzetes karakterlánc csak a ModuleVersion Major.Minor.Build 3 szegmensek esetén adható meg. Ez SemVer v1.0.0 igazodik.
* Kötőjel az elválasztó buildszámának és az előzetes karakterlánc között. Kötőjel szerepelni fog az előzetes karakterlánc az első karakter, csak.
* Az előzetes karakterlánc csak ASCII számok és betűk is tartalmazhat [0-9A-Za - z-]. Ajánlott eljárás az előzetes megkezdéséhez alfanumerikus karakter, string, egyszerűbb azonosítani, hogy ez egy előzetes verziójának a elemek listájának beolvasásakor lesz.
* Csak SemVer v1.0.0 előzetes karakterláncok jelenleg támogatottak. Előzetes karakterlánc __nem kell__ vagy időszak tartalmaz vagy + [. +], amely SemVer 2.0 engedélyezettek.
* A támogatott előzetes karakterlánc például a következők:-alpha, - α1,-BETA, - update20171020

__Előzetes versioning hatása a rendezési sorrend és a telepítési mappa__

Rendezési sorrend megváltozik, ha előzetes verzióját, akkor fontos, amikor a PowerShell-galériában közzététele, amely használja PowerShellGet parancsokkal modulok telepítésekor.
Az előzetes karakterlánc két modulok, a rendezési sorrend a következő a kötőjel karakterláncra vonatkozó részében alapul. Igen verziója 2.5.0-alpha nem éri el 2.5.0-beta, ez pedig kisebb, mint 2.5.0-gamma.
Ha két modulok az azonos ModuleVersion, és csak egy előzetes karakterlánccal rendelkezik, a modul nélkül a előzetes karakterlánc feltételezett, hogy az éles használatra kész verzió-e, és nagyobb, mint az előzetes verziót (amelynek része az előzetes verzióként rendezése történik (karakterlánc).
Tegyük fel, amikor 2.5.0 és 2.5.0-beta, a 2.5.0 összehasonlításával kiadott verzióját akkor veszi figyelembe a két nagyobb.

A PowerShell-galériában való közzétételkor alapértelmezés szerint a modul közzétett verziója kell lennie a nagyobb, mint a korábban közzétett verziót a PowerShell-galériában.

## <a name="finding-and-acquiring-prerelease-items-using-powershellget-commands"></a>Keresés és PowerShellGet parancsokkal előzetes elemek beszerzése

PowerShellGet keresés-modul, a telepítés-modul, a frissítés-modul, az előzetes elemekről foglalkozó és mentés-modul parancsokat igényel, a - AllowPrerelease jelző hozzáadása.
Ha - AllowPrerelease meg van adva, előzetes elemek is fog szerepelni, ha ilyenek.
Ha - AllowPrerelease jelző nincs megadva, az előzetes elemek nem jelenik meg.

Az egyetlen kivétel ez alól Ez a PowerShellGet modul parancsok a következők: Get-InstalledModule és bizonyos esetekben az Uninstall-modul.

* Get-InstalledModule mindig automatikusan információk jelennek meg az előzetes verzió-karakterlánca a modulok a.
* Távolítsa el modul alapértelmezés szerint eltávolítja a legfrissebb egy modult, ha __megszűnik__ van megadva. Ezt a viselkedést nem változott. Azonban ha - RequiredVersion, adott előzetes verziójának - AllowPrerelease lesz szükség.

## <a name="examples"></a>Példák
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

A modul csak a megadott előzetes miatt eltérőek-verziók egymás melletti telepítése nem támogatott.
PowerShellGet használatával modul telepítésekor ugyanabban a modulban különböző verzióinak egymás melletti telepített hozzon létre egy mappa nevét a ModuleVersion.
A mappa nevét a ModuleVersion az előzetes karakterlánc nélkül használható.
Ha a felhasználó telepít MyModule verzió 2.5.0-alpha, azt a MyModule\2.5.0 mappába telepíti.
Ha a felhasználó 2.5.0-beta telepíti, a 2.5.0-beta verziót fogja __túlzott írási__ MyModule\2.5.0 mappa tartalmát.
Egy ezt a megközelítést előnye, hogy nincs szükség az eltávolítási az előzetes verziót az éles használatra kész verzió telepítése után.
Az alábbi példa bemutatja, mi történik:


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

Modul eltávolítása eltávolítja a legújabb verzióra a modulok, amikor - RequiredVersion nem.
Ha - RequiredVersion van megadva, és egy előzetes verzióját, a parancs - AllowPrerelease kell adni.

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



## <a name="more-details"></a>További részletekért
### <a name="prerelease-script-versionsscriptprereleasescriptmd"></a>[Kiadás előtti parancsfájl-verziók](../script/PrereleaseScript.md)
### <a name="find-modulepsgetfind-modulemd"></a>[A modul keresése](./psget_find-module.md)
### <a name="install-modulepsgetinstall-modulemd"></a>[Install-modul](./psget_install-module.md)
### <a name="save-modulepsgetsave-modulemd"></a>[Save-Module](./psget_save-module.md)
### <a name="update-modulepsgetupdate-modulemd"></a>[Update-Module](./psget_update-module.md)
### <a name="get-installedmodulepsgetget-installedmodulemd"></a>[Get-InstalledModule](./psget_get-installedmodule.md)
### <a name="uninstall-modulepsgetuninstall-modulemd"></a>[Távolítsa el modul](./psget_uninstall-module.md)