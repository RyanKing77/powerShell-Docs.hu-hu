---
ms.date: 09/26/2017
contributor: keithb
keywords: katalógus, powershell, a parancsmag, psget
title: Előzetes verziója
ms.openlocfilehash: eced067dd21082de0db653daf3b838217154f1dd
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62084861"
---
# <a name="prerelease-module-versions"></a>Előzetes verziója

1.6.0-s verziójának verziótól kezdődően a PowerShellGet és a PowerShell-galériából támogatást nyújt a címkézési egy előzetes verzióját, 1.0.0-esnél újabb verzióiban. Ez a funkció előtt előzetes csomagokat a rendszer 0-verzió kezdő járulnia korlátozott. Ezeket a funkciókat az a célja, hogy a szélesebb körű támogatást biztosít [SemVer v1.0.0](http://semver.org/spec/v1.0.0.html) versioning egyezmény visszamenőleges PowerShell verziók 3 és újabb, vagy meglévő a PowerShellGet verzióival való kompatibilitás megszakítása nélkül. Ez a témakör a modul-specifikus szolgáltatásokra összpontosít. A parancsfájlok egyenértékű funkciókra a [parancsfájlok előzetes verziók](script-prerelease-support.md) témakör. Használja ezeket a funkciókat, a kiadók is modul vagy verzió 2.5.0-alpha-parancsprogramot, és később kiadásból egy éles használatra kész 2.5.0, amely felülírja az előzetes verziót.

Magas szinten a modul előzetes funkciók a következők:

- A modul előzetes karakterláncot ad hozzá a moduljegyzékben PSData szakaszában azonosítja az előzetes verzióként. Ha a modul a PowerShell-galériából tesznek közzé, ezeket az adatokat a jegyzékfájl kinyert, és előzetes csomagok azonosítására szolgál.
- Előzetes csomagokat beszerzéséhez szükséges hozzáadása `-AllowPrerelease` jelzőt a PowerShellGet-parancsokkal `Find-Module`, `Install-Module`, `Update-Module`, és `Save-Module`. Ha nincs megadva a jelzőt, végleges csomagok nem jelenik meg.
- Modulverziók által megjelenített `Find-Module`, `Get-InstalledModule`, és a PowerShell-galériából a jelenik meg egyetlen utótaggal, mint 2.5.0-alpha előzetes karakterláncot karakterláncként.

Szolgáltatások részletei az alábbiakban találhatók.

Ezek a változások nem befolyásolják a PowerShell beépített modul verzió támogatása, és kompatibilis a PowerShell 3.0-s, 4.0 és 5.

## <a name="identifying-a-module-version-as-a-prerelease"></a>Egy modul verzió azonosítása egy előzetes verzióját

A PowerShellGet-támogatás előzetes verzióihoz két mezőt a modul Manifest használatát igényli:

- A foglalt a moduljegyzékben ModuleVersion egy 3 részben verziójúnak kell lennie, ha előzetes verziójának szolgál, és meg kell felelniük a meglévő PowerShell verziószámozás. A verziójának formátumát A.B.C, ahol A, B és C az összes egész szám lehet.
- A kiadás előtti karakterlánc van megadva a moduljegyzékben PrivateData PSData szakaszában.

Az alábbiakban a megjelenés előtti karakterlánc részletes követelményeket.

Egy példa szakaszában egy moduljegyzék, amely meghatározza egy modul egy előzetes verzióját, az alábbi módon jelenik meg:

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

- Előzetes karakterlánc csak akkor adható meg, ha a ModuleVersion 3 szegmenssel főverzió.alverzió.build formában az. Ez SemVer v1.0.0 illeszkedik.
- Egy kötőjel a kivonni kívánt a buildszám és a megjelenés előtti karakterlánc között. Egy kötőjel mint az első karakter, csak a kiadás előtti karakterlánc kell venni.
- A kiadás előtti karakterlánc csak alfanumerikus ASCII-karaktereket tartalmazhat [0-pedig a 9A-Za - z-]. Ajánlott eljárás a Prerelease megkezdéséhez karakterlánc egy alfanumerikus karakter, könnyebben azonosíthatja, hogy ez a kiadás előtti verzióját, csomagok listájának beolvasásakor.
- Jelenleg csak SemVer v1.0.0 előzetes karakterláncok támogatott. Előzetes karakterlánc **nem kell** vagy időszak tartalmazhat vagy + [. +], amely SemVer 2.0 használata engedélyezett.
- Néhány példa a támogatott előzetes karakterlánc:-alpha, - α1, – BÉTAVERZIÓ, - update20171020

### <a name="prerelease-versioning-impact-on-sort-order-and-installation-folders"></a>Előzetes versioning hatása a rendezési sorrend és a telepítési mappa

Rendezési sorrend módosítja, ami fontos a PowerShell-galériából való közzétételkor, előzetes verziójának használata esetén, és ha a PowerShellGet-parancsokkal modulok telepítése. Ha az kiadás előtti karakterlánc két modul van megadva, a rendezési sorrendet a karakterlánc része a kötőjelet tartalmazhatja a következő alapul. Tehát verzió 2.5.0-alpha kisebb, mint 2.5.0-beta, amely kisebb, mint 2.5.0-gamma. Ha két modult az azonos ModuleVersion, és csak egy előzetes karakterlánccal rendelkezik, a kiadás előtti karakterlánc nélkül a modul adatforrásmérete az éles használatra kész verziót, és nagyobb, mint az előzetes verziót (amely tartalmazza az előzetes verzióként rendezése (karakterlánc). Tegyük fel, amikor 2.5.0 és 2.5.0-beta, a 2.5.0 összehasonlítása kiadások nagyobb, mint a két verzió akkor minősül.

A PowerShell-galériából való közzétételkor alapértelmezés szerint a közzétett modul verzióját kell lennie a nagyobb, mint a korábban közzétett verzió, a PowerShell-galériában található.

## <a name="finding-and-acquiring-prerelease-packages-using-powershellget-commands"></a>Keresés és a PowerShellGet-parancsokkal előzetes csomagok beszerzése

Előzetes csomagokat-Module PowerShellGet Find-Module, Install-Module, frissítés, kezelése és a Save-Module parancsokat igényel, a - AllowPrerelease jelző hozzáadása. Ha meg van adva a - AllowPrerelease, előzetes csomagokat helyőrzője, ha ilyenek. Ha nincs megadva - AllowPrerelease jelző, előzetes csomagokat nem jelenik meg.

Alól kivételt csak ehhez a PowerShellGet modul parancsok a következők: Get-InstalledModule és bizonyos esetekben az Uninstall-modul.

- Get-InstalledModule mindig automatikusan információk jelennek meg az előzetes modulok verzió karakterláncában.
- Távolítsa el modul alapértelmezés szerint eltávolítja egy modul legújabb verzióját Ha __nincs verzió__ van megadva. Ezt a viselkedést nem változott. Azonban ha előzetes verziójának meg van adva, használja a - RequiredVersion, - AllowPrerelease lesz szükség.

## <a name="examples"></a>Példák

Tegyük fel, a PowerShell-galériából TestPackage modulverziók 1.8.0-as és 1.9.0-alpha rendelkezik. Ha `-AllowPrerelease` van nincs megadva, csak 1.8.0-as verziót adja vissza.

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

Mindig adja meg a - AllowPrerelease egy előzetes verzióját kell telepíteni. Egy kiadás előtti verzió-karakterlánccal való megadása nem elegendő.

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

Az előző parancs meghiúsult, mert a - AllowPrerelease nincs megadva. Hozzáadás `-AllowPrerelease` sikeres eredményez.

```powershell
Install-module TestPackage -RequiredVersion 1.9.0-alpha -AllowPrerelease
Get-InstalledModule TestPackage
```

```output
Version         Name          Repository  Description
-------         ----          ----------  -----------
1.9.0-alpha     TestPackage   PSGallery   Package used to validate changes to the PowerShe...
```

Egymás melletti telepítés, amelyet csak a megadott prerelease miatt eltérő verziójú modulok nem támogatott. A PowerShellGet-modul telepítésekor ugyanazon modul különböző verzióinak egymás melletti telepített hoz létre a mappa nevét, a ModuleVersion használatával. A mappa nevét a ModuleVersion, a kiadás előtti karakterlánc nélkül használható. Ha egy felhasználó MyModule verzió 2.5.0-alpha telepíti, akkor fog települni a `MyModule\2.5.0` mappát. Ha a felhasználó ezután 2.5.0-beta telepíti, a 2.5.0-beta verziót fog **felülírása** a mappa tartalmának `MyModule\2.5.0`. Egyik előnye az, hogy ez a módszer, hogy nincs szükség az eltávolítási az előzetes verziót az éles használatra kész verzió telepítése után. Az alábbi példa bemutatja, mi várható:

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

Modul eltávolítása eltávolítja a modulok a legújabb verzióra, amikor a - RequiredVersion nem tartalmazza.
Ha a - RequiredVersion van megadva, és egy előzetes verzióját, - AllowPrerelease hozzá kell adni a parancshoz.

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
+ Uninstall-Module TestPackage -RequiredVersion 1.9.0-beta
+ ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : InvalidArgument: (:) [Uninstall-Module], ArgumentException
    + FullyQualifiedErrorId : AllowPrereleaseRequiredToUsePrereleaseStringInVersion,Uninstall-Module

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

## <a name="more-details"></a>További részletek

- [Parancsfájl előzetes verziók](script-prerelease-support.md)
- [Find-Module](/powershell/module/powershellget/find-module)
- [Install-Module](/powershell/module/powershellget/install-module)
- [Save-Module](/powershell/module/powershellget/save-module)
- [Update-Module](/powershell/module/powershellget/Update-Module)
- [Get-InstalledModule](/powershell/module/powershellget/get-installedmodule)
- [UnInstall-Module](/powershell/module/powershellget/uninstall-module)
