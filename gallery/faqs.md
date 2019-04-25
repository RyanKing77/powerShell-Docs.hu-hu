---
ms.date: 06/12/2017
contributor: JKeithB
keywords: katalógus, a powershell, a parancsmag, a psgallery
title: PowerShell-galériából – gyakori kérdések
ms.openlocfilehash: bcbb36a9ec60d88d1ef56fd270f0ae1862d5ca6b
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62084628"
---
# <a name="frequently-asked-questions"></a>Gyakori kérdések

## <a name="what-is-a-powershell-module"></a>Mi az a PowerShell-modult?

Egy PowerShell-modul az egyes PowerShell-funkciókat tartalmazó újrafelhasználható csomag. A PowerShell (funkciók, változókat, DSC-erőforrások, stb.) minden csomagolható modulok. Modulok általában az adott típusú egy adott elérési úton tárolt fájlokat tartalmazó mappákat. PowerShell-modulok is elérhető néhány különböző típusai vannak.

## <a name="what-is-a-powershell-script"></a>Mi az, egy PowerShell-parancsfájlt?

Egy PowerShell-parancsprogram egy .ps1 kiterjesztésű fájlba újbóli használata és megosztása engedélyezéséhez tárolt parancsokat. PowerShell-munkafolyamatok is rendelkezésre állnak PowerShell-parancsfájlok, amelyek szerkezeti feladatokhoz, és adja meg ezeket a feladatokat az alkalmazás-előkészítés. További információkért látogasson el [– első lépések PowerShell-munkafolyamat](https://technet.microsoft.com/library/jj134242.aspx).

## <a name="how-are-powershell-scripts-different-from-powershell-modules"></a>Miben különböznek PowerShell-szkripteket a PowerShell-modulok?

Modulok általában jobb megosztási, de azt engedélyezi a parancsfájl megkönnyítheti a munkafolyamatok és a parancsfájlok járulnak hozzá a Közösség megosztását. További információkért tekintse meg a következő angol nyelvű blogokban:

- [Ne írjon a parancsfájlok, PowerShell-modul írása](https://blogs.technet.microsoft.com/heyscriptingguy/2011/06/27/dont-write-scripts-write-powershell-modules/)
- [PowerShell-modulok megismerése](https://blogs.technet.microsoft.com/heyscriptingguy/2015/07/10/understanding-powershell-modules/)

## <a name="how-can-i-publish-to-the-powershell-gallery"></a>Hogyan teheti közzé a PowerShell-galériában?

Regisztrálnia kell egy fiókot a PowerShell-galériából a csomagok a katalógusban való közzététel előtt. Ez azért van így, mert csomagok közzététele megköveteli egy NuGetApiKey, amelyről az regisztráláskor. Regisztrálni, használja a személyes, munkahelyi vagy iskolai fiókjával jelentkezzen be a PowerShell-galériából. Egyszeri regisztrációs folyamatot kötelező, amikor először jelentkezik be. Ezt követően a NuGetApiKey a profil lapon érhető el.

Ha már regisztrálta a katalógusban, használja a [Publish-Module][] vagy [Publish-Script][] parancsmagjait a csomag közzététele a katalógusban.
Ezek a parancsmagok futtatásával kapcsolatos további részletekért látogasson el a Közzététel lapot, vagy olvassa el a [Publish-Module][] és [Publish-Script][] dokumentációját.

**Nem kell regisztrálni, vagy jelentkezzen be a katalógus telepítéséhez vagy csomagok mentése.**

## <a name="i-received-failed-to-process-request-the-specified-api-key-is-invalid-or-does-not-have-permission-to-access-the-specified-package-the-remote-server-returned-an-error-403-forbidden-error-when-i-tried-to-publish-a-package-to-the-powershell-gallery-what-does-that-mean"></a>Kapott "nem sikerült feldolgozni a kérelmet. "A megadott API-kulcs érvénytelen, vagy nem rendelkezik hozzáféréssel a megadott csomaghoz.". A távoli kiszolgáló hibát adott vissza: (403) tiltott." Hiba történt a PowerShell-galériában egy csomag közzététele során. az mit jelent?

Ez a hiba a következő okok miatt fordulhat elő:

- **A megadott API-kulcs érvénytelen.**
     Győződjön meg arról, hogy megadott érvényes API-kulcsot a fiókból. Az API-kulcs beszerzéséhez profiloldalán megtekintheti.
- **A megadott csomag neve nem Ön tulajdonában van.**
     Ha meggyőződött róla, hogy az API-kulcs helyes, majd előfordulhat, hogy már léteznek a neve megegyezik egy használni kívánt csomagot. A csomag Előfordulhat, hogy importálta a tulajdonos által fel nem sorolt, ebben az esetben az nem fog megjelenni minden olyan keresési eredmények között. Annak megállapításához, hogy egy azonos nevű csomag már létezik-e, nyisson meg egy böngészőt, és a csomag részleteit megjelenítő oldalra léphet: `https://www.powershellgallery.com/packages/<packageName>`. Például közvetlenül a Navigálás `https://www.powershellgallery.com/packages/pester` vesz igénybe, a Pester modul részleteit megjelenítő oldalra, hogy fel nem sorolt-e. Ha egy ütköző nevű csomag már létezik, és fel nem sorolt, végezheti el:
    - Válassza ki a csomag egy másik nevet.
    - Lépjen kapcsolatba a következő létező csomagba.

## <a name="why-cant-i-sign-in-with-my-personal-account-but-i-could-sign-in-yesterday"></a>Miért nem sikerül bejelentkezni a személyes fiókkal jelentkezik be, de szeretnék sikerült tegnap bejelentkezni?

Vegye figyelembe, hogy a katalógus-fiók nem alkalmazzák a módosításokat az elsődleges e-mail-címre. További információkért lásd: [Microsoft E-mail aliasok](https://windows.microsoft.com/windows/outlook/add-alias-account).

## <a name="why-dont-i-see-all-the-gallery-packages-when-i-select-all-the-category-checkboxes-on-the-packages-tab"></a>Miért nem látom az összes katalóguscsomagok csomagok lapján az összes kategória jelölőnégyzetek kiválasztásakor?

Egy kategória jelölőnégyzet kiválasztásával, vannak megjelölve "Szeretnék kapni, tekintse meg a kategória összes csomagot." Csak a kiválasztott kategóriákba tartozó csomag jelenik meg. Tehát ehhez hasonlóan a kategória összes jelölőnégyzetek bejelölésével, akkor is figyelmezteti a "Szeretnék kapni, tekintse meg az összes csomag bármelyik kategóriában." De az egyes csomagok a katalógusban nem tartozik kategóriákra szerepel a listában, így azok nem jelennek az eredményeket. Tekintse meg a katalógusban található összes csomagot, törölje az összes kategóriát, vagy válassza ki újra a csomagok lapot.

## <a name="what-are-the-requirements-to-publish-a-module-to-the-powershell-gallery"></a>Mik a modul közzétételére a PowerShell-galériából?

PowerShell-modul (parancsfájl-modulokba, bináris modulok vagy jegyzékfájl modulok) bármilyen típusú tehetők közzé a katalógusban.
A közzétételhez egy modul PowerShellGet tudnia kell, néhány dolgot kapcsolatos – a verzió, leírás, Szerző és hogyan licencelve van.
Ez az információ olvasható, a közzétételi folyamat részeként a *moduljegyzék* (.psd1) fájl, vagy az értékét a [Publish-Module][] parancsmag **LicenseUri** a paraméter.
A galériában közzétett modulok modul jegyzékfájlokká kell rendelkeznie.
A katalógus teheti közzé minden olyan modul, amely a következő információkat tartalmazza a jegyzékfájlban:

- Verzió
- Leírás
- Szerző
- A licencfeltételeket, a modul részét képező vagy egy URI-t a **PrivateData** a jegyzékfájl, vagy a szakasz a **LicenseUri** paraméterében a [Publish-Module][] parancsmag.

## <a name="how-do-i-create-a-correctly-formatted-module-manifest"></a>Hogyan hozhatok létre egy megfelelően formázott moduljegyzék?

Hozzon létre egy moduljegyzék legegyszerűbb módja az, hogy futtassa a [New-ModuleManifest][] parancsmagot. PowerShell 5.0-s vagy újabb, a New-ModuleManifest hoz létre egy megfelelően formázott moduljegyzék hasznos metaadatokat, például az üres mezők **ProjectUri**, **LicenseUri**, és **címkék**. Egyszerűen adja meg a megszámlálandó üres értékeket, vagy a létrehozott jegyzékre használja példaként megfelelő formázását.

Győződjön meg arról, hogy minden szükséges metaadatokat tartalmazó mezőket megfelelően ki van töltve, használja a [Test-ModuleManifest][] parancsmagot.

A modul jegyzékfájl mezők frissítéséhez használja a [Update-ModuleManifest][] parancsmagot.

## <a name="what-are-the-requirements-to-publish-a-script-to-the-gallery"></a>Mik a parancsfájl közzététele a katalógusban?

PowerShell-parancsprogram (parancsfájlok és munkafolyamatok) bármilyen típusú teheti közzé a katalógusban.
Parancsfájl közzétételét, a PowerShellGet tudnia kell, néhány dolgot kapcsolatos – a verzió, leírás, Szerző és hogyan licencelve van.
Ez az információ olvasható, a parancsfájl a közzétételi folyamat részeként *PSScriptInfo* szakaszban vagy értékét a [Publish-Script][] parancsmag **LicenseUri**paraméter.
A katalógusban közzétett összes parancsfájl metaadat-információkat kell rendelkeznie.
A katalógus teheti közzé minden olyan parancsfájl, amely a PSScriptInfo szakaszban a következő információkat tartalmazza:

- Verzió
- Leírás
- Szerző
- Egy URI-t a licencfeltételeket, a parancsfájl, vagy részeként a **PSScriptInfo** a parancsfájl vagy a szakasz a **LicenseUri** paraméterében a [Publish-Script][] parancsmag.

## <a name="how-do-i-search"></a>Hogyan kereshetek?

Írja be, amit Ön keres a szövegmezőben. Például ha szeretné az Azure SQL kapcsolódó keresőmodul, csak írja be "az azure sql". A keresőmotor megkeresi ezeket a kulcsszavakat, az összes közzétett csomagok, például a címét, leírását és a metaadatok között. Ezután egy súlyozott minőségi pontszám alapján, jelenik meg a leginkább megfelel. Mezőben használja adott mező szerint is kereshet: "érték" a következő mezőket a keresési lekérdezés szintaxist:

- Címkék
- Funkciók
- Parancsmagok
- DscResources
- PowerShellVersion

Igen, például, ha a keresés PowerShellVersion: (a parancsfájl modul jegyzékfájl alapján) PowerShellVersion 2.0-val kompatibilis "2.0" csak eredmények jelennek meg.

## <a name="how-do-i-create-a-correctly-formatted-script-file"></a>Hogyan hozhatok létre egy megfelelően formázott parancsfájlt?

Parancsfájl megfelelően formázott legegyszerűbb módja az, hogy futtassa a [New-ScriptFileInfo][] parancsmagot. PowerShell 5.0-, a New-ScriptFileInfo hoz létre egy megfelelően formázott parancsfájl üres mezők hasznos metaadatokat, például a **ProjectUri**, **LicenseUri**, és **címkék** . Egyszerűen adja meg a megszámlálandó üres értékeket, vagy a megfelelő formázását, például a létrehozott parancsfájl használatával.

Győződjön meg arról, hogy minden szükséges metaadatokat tartalmazó mezőket megfelelően ki van töltve, használja a [Test-ScriptFileInfo][] parancsmagot.

A parancsfájl metaadatmezőket frissítéséhez használja a [Update-ScriptFileInfo][] parancsmagot.

## <a name="what-other-types-of-powershell-modules-exist"></a>Milyen más PowerShell-modul létezik?

Az előfizetési időszak PowerShell-modul is a fájlok tényleges funkciókat megvalósító utal. A modul parancsfájlok (.psm1) PowerShell-kódot tartalmaz. A modul bináris fájlok (.dll) lefordított kódot tartalmaznak.

Gondolja át, hogy egyik módja: a mappát, amely magában foglalja a modul az a modul mappa. A modul mappáját egy modul jegyzékfájlt (.psd1), amely leírja a mappa tartalmát is tartalmazhat. Valójában hogyan használják a munkahelyi fájlok a parancsfájl modul (.psm1) és a modul bináris fájlokat (.dll). DSC-erőforrások egy adott alfeladat mappában található, és a parancsfájl modul vagy a modul bináris fájlokat vannak implementálva.

A katalógusban található összes modul jegyzékek tartalmazhat, és ezeket a modulokat a legtöbb parancsfájl modul vagy a modul bináris fájlokat tartalmaz. A kifejezés modul miatt ezek különböző jelentéssel zavaró lehet. Kivéve, ha explicit módon meghatározva, a word modul ezen az oldalon összes felhasználását tekintse meg a modul mappát, amely tartalmazza ezeket a fájlokat.

## <a name="how-does-packagemanagement-relate-to-powershellget-high-level-answer"></a>Hogyan kapcsolódnak a PackageManagement PowerShellGet? (Magas szintű válasz)

A PackageManagement egy közös felület bármilyen Csomagkezelő való munkához. Végül PowerShell-modulok, a MSIs, a Ruby gems, a NuGet-csomagok vagy a Perl-modulok még foglalkozik, hogy meg kell tudni (Find-Package és Install-Package) keresse meg és telepítheti a PackageManagement a parancsok használata. A PackageManagement egyes Csomagkezelő, amely rendkívüli PackageManagement csomag szolgáltatót sablonkonfigurációkat azért teszi ezt. Szolgáltatók tegye meg a tényleges munka; tartalmat beolvasni a változásokat, és a tartalom helyi telepítése. Csomag szolgáltatók gyakran egyszerűen burkolása körül a meglévő csomag manager eszközök egy adott csomag-típus.

A PowerShellGet a Csomagkezelő PowerShell csomagok.
Nincs egy PSModule csomag szolgáltató, amely elérhetővé teszi a PackageManagement PowerShellGet funkciót.
Ez az oka, vagy futtassa is [Install-Module][] vagy az Install-Package-szolgáltató PSModule modul telepítésére a PowerShell-galériából.
Bizonyos PowerShellGet funkciókat, beleértve a [Update-Module][] és [Publish-Module][], nem érhető el a PackageManagement-parancsok segítségével.

Összefoglalva a PowerShellGet kizárólag összpontosít egy prémium szintű csomag megoldást PowerShell tartalom kellene. A PackageManagement összpontosít adatokhoz hozzáférést biztosító eszközök egy általános rekordkészletből minden csomag felügyeleti funkciókat. Unsatisfying találja meg a választ, van-e ez a dokumentum alján egy hosszú válasz a a **hogyan PackageManagement ténylegesen kapcsolódik a PowerShellGet?** szakaszban.

További információkért látogasson el a [PackageManagement projektoldalon](https://oneget.org/).

## <a name="how-does-nuget-relate-to-powershellget"></a>Hogyan kapcsolódnak NuGet PowerShellGet?

A PowerShell-galériából egy módosított verziója, a [NuGet-katalógusban](https://www.nuget.org/). A PowerShellGet NuGet-szolgáltató például a PowerShell-galériából NuGet-alapú tárházak dolgozhat használ.

A PowerShellGet is használhatja bármilyen érvényes NuGet tárházban vagy a fájlmegosztásnak ellen. Egyszerűen csak hozzá kell a tárház futtatásával a [Register-PSRepository][] parancsmagot.

## <a name="does-that-mean-i-can-use-nugetexe-to-work-with-the-gallery"></a>Jelent NuGet.exe használható dolgozhat a katalógusban?

Igen.

## <a name="how-does-packagemanagement-actually-relate-to-powershellget-technical-details"></a>Hogyan PackageManagement ténylegesen kapcsolódik a PowerShellGet? (Technikai részletek)

Technikai részletek a PowerShellGet erősen PackageManagement infrastruktúrát használja.

A PowerShell-parancsmag rétegben [Install-Module][] ténylegesen vékony burkolója Install-Package-szolgáltató PSModule.

A PackageManagement csomag szolgáltató rétegben az PSModule csomag szolgáltató ténylegesen hívások egyéb PackageManagement csomag szolgáltatók. Például ha katalógusok NuGet-alapú (például a PowerShell-galériából) dolgozik, a PSModule csomag szolgáltató használ a NuGet-csomag szolgáltató dolgozhat a tárházban.

![A PowerShellGet-architektúra](Images/powershellgetArchitecture.png)

1. ábra: A PowerShellGet-architektúra

## <a name="what-is-required-to-run-powershellget"></a>Mi szükséges a PowerShellGet futtatásához?

Általában javasoljuk, hogy kiválasztotta a PowerShellGet modul (vegye figyelembe, hogy .NET 4.5-ös igényel) legújabb verzióját.

A **PowerShellGet** modulhoz szükséges **PowerShell 3.0-s vagy újabb**.

Ezért **PowerShellGet** a következő operációs rendszerek egyike szükséges:

- Windows 10
- Windows 8.1 Pro
- Windows 8.1 Enterprise
- Windows 7 SP1
- Windows Server 2016
- Windows Server 2012 R2
- Windows Server 2008 R2 SP1

**A PowerShellGet** is szükséges a .NET-keretrendszer 4.5 vagy újabb. Telepítheti a .NET-keretrendszer 4.5 vagy újabb a [Itt](https://msdn.microsoft.com/library/5a4x27ek.aspx).

## <a name="is-it-possible-to-reserve-names-for-packages-that-will-be-published-in-future"></a>Ennyi az egész lehet foglalni a jövőben tesznek közzé csomagok nevei?

Nem alkalmas guggolós csomag nevét. Ha úgy érzi, hogy egy meglévő csomaghoz vette a nevét, amely megfelel a csomag több, próbálja meg [forduljon a tulajdonoshoz csomag](./how-to/working-with-packages/contacting-package-owners.md). Ha nem kap választ belül egy pár hétig, forduljon az ügyfélszolgálathoz, és a PowerShell-galériából csapat azt jeleníti meg.

## <a name="how-do-i-claim-ownership-for-packages"></a>Hogyan vehetem tulajdonjog-csomagok?

Tekintse meg [csomag tulajdonosainak kezelése a PowerShellGallery.com](./how-to/publishing-packages/managing-package-owners.md) részleteiről.

## <a name="how-do-i-deal-with-a-package-owner-who-is-violating-my-package-license"></a>Hogyan egy csomag tulajdonost, aki a csomag licenc van megsértése foglalkoznak?

Azt javasoljuk, hogy a PowerShell-Közösség működhet együtt, oldja meg a csomag tulajdonosai és más csomagokat, a tulajdonosok között felmerülő viták.  Azt a célra egy [névfeloldási folyamat vitát](./how-to/getting-support/dispute-resolution.md) , megkérjük, hogy a rendszergazdák PowerShellGallery.com intercede előtt hajtsa végre.

[New-ModuleManifest]: /powershell/module/Microsoft.PowerShell.Core/New-ModuleManifest
[Test-ModuleManifest]: /powershell/module/Microsoft.PowerShell.Core/Test-ModuleManifest
[Update-ModuleManifest]: /powershell/module/Microsoft.PowerShell.Core/Update-ModuleManifest

[Install-Module]: /powershell/module/PowershellGet/Install-Module
[New-ScriptFileInfo]: /powershell/module/PowershellGet/New-ScriptFileInfo
[Publish-Module]: /powershell/module/PowershellGet/Publish-Module
[Publish-Script]: /powershell/module/PowershellGet/Publish-Script
[Register-PSRepository]: /powershell/module/PowershellGet/Register-PSRepository
[Test-ScriptFileInfo]: /powershell/module/PowershellGet/Test-ScriptFileInfo
[Update-Module]: /powershell/module/PowershellGet/Update-Module
[Update-ScriptFileInfo]: /powershell/module/PowershellGet/Update-ScriptFileInfo
