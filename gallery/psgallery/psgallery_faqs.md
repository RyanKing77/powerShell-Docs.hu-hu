---
ms.date: 2017-06-12
contributor: JKeithB
ms.topic: conceptual
keywords: "gyűjtemény, a powershell, a parancsmag, a psgallery"
title: psgallery_faqs
ms.openlocfilehash: b856c44f3733d4a7c236d901edb391091d9d546e
ms.sourcegitcommit: 99227f62dcf827354770eb2c3e95c5cf6a3118b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/15/2018
---
# <a name="frequently-asked-questions"></a>Gyakori kérdések

## <a name="what-is-a-powershell-module"></a>Mi az a PowerShell-modult?

Egy PowerShell-modul csomag egy újrafelhasználható tartalmazó néhány PowerShell szolgáltatást. A PowerShell (funkciók, változókat, DSC erőforrások stb.) tartalmát csomagolható modulok. Modulok általában egy adott elérési úton tárolt fájlok adott típusú tartalmazó mappákat. Nincsenek ott a PowerShell-modulok néhány különböző típusú.

## <a name="what-is-a-powershell-script"></a>Mi az a PowerShell-parancsfájlt?

Egy PowerShell-parancsprogram egy .ps1 fájl újbóli használata és megosztása engedélyezése tárolt parancsokat. PowerShell-munkafolyamatok is PowerShell-parancsfájlok, amelyek felsorolják feladatokhoz, és adja meg ezeket a feladatokat az alkalmazás-előkészítés. További információkért látogasson el a [PowerShell munkafolyamat-első lépések](https://technet.microsoft.com/library/jj134242.aspx).

## <a name="how-are-powershell-scripts-different-from-powershell-modules"></a>Hogyan eltérnek PowerShell-parancsfájlok PowerShell-modulok?

Modulok általában jobb megosztható, de azt engedélyezi a parancsfájl használatával könnyebben a munkafolyamatok és a parancsfájlok hozzájárulnak a közösségi megosztás. További információkért tekintse meg a következő angol nyelvű blogokban:

- [Nem parancsfájlokat, írási PowerShell-modulok](https://blogs.technet.microsoft.com/heyscriptingguy/2011/06/27/dont-write-scripts-write-powershell-modules/)
- [PowerShell-modulok ismertetése](https://blogs.technet.microsoft.com/heyscriptingguy/2015/07/10/understanding-powershell-modules/)

## <a name="how-can-i-publish-to-the-powershell-gallery"></a>Hogyan is közzéteheti a PowerShell-galériában?

Regisztrálnia kell egy fiókot a PowerShell-galériában elem a gyűjteményben való közzététele előtt. Ennek az az oka elem közzététele egy NuGetApiKey, amelyről az regisztráláskor igényel. Regisztrálni, használja a személyes, munkahelyi vagy iskolai fiókkal bejelentkezni a PowerShell-galériában. Egyszeri regisztrációt, ha az első alkalommal bejelentkezik. Ezután a NuGetApiKey érhető el a profil lapon.

Miután regisztrálta a katalógusban, a [Publish-modul](https://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409) vagy [Publish-parancsfájl](https://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409) parancsmagok közzétenni a elem a gyűjteményben. Ezen parancsmagok futtatásához kapcsolatos további részletekért látogasson el a közzététel fülre, vagy olvassa el a [Publish-modul](https://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409) és [Publish-parancsfájl](https://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409) dokumentációját.

**Nem kell regisztrálni, vagy jelentkezzen be a gyűjtemény telepítéséhez vagy elemek mentése.**

## <a name="i-received-failed-to-process-request-the-specified-api-key-is-invalid-or-does-not-have-permission-to-access-the-specified-package-the-remote-server-returned-an-error-403-forbidden-error-when-i-tried-to-publish-an-item-to-the-powershell-gallery-what-does-that-mean"></a>Kaptam "kérelem feldolgozása sikertelen. "A megadott API-kulcs érvénytelen, vagy nem rendelkezik hozzáféréssel a megadott csomaghoz.". A távoli kiszolgáló hibát adott vissza: (403-as) tiltott. " a cikk közzétételéhez a PowerShell-galériában közben hiba történt. az mit jelent?

Ez a hiba akkor fordulhat elő, a következő okok miatt:

- **A megadott API-kulcs érvénytelen.**
     Győződjön meg arról, hogy megadta a fiókhoz tartozó érvényes API-kulcsot. Ahhoz, hogy az API-kulcsot, a profil a lapnak a megtekintésére.
- **A megadott elem neve nem Ön tulajdonában van.**
     Ha meggyőződött róla, hogy az API-kulcs megfelelő, akkor előfordulhat, hogy már vannak ilyen nevű megegyezik a használni kívánt elem. A cikk a tulajdonos által fel nem sorolt lehetett, ebben az esetben az nem fog megjelenni a keresési eredmények között. Annak megállapításához, hogy egy elemet ugyanazzal a névvel már létezik-e, nyisson meg egy böngészőt, és az elem részleteit megjelenítő oldalra léphet: `https://www.powershellgallery.com/packages/<itemName>`. Például Navigálás közvetlenül `https://www.powershellgallery.com/packages/pester` elindítjuk ezt a Pester modul részleteit megjelenítő oldalra, hogy-e fel nem sorolt, vagy nem. Ha egy ütköző nevű elem már létezik, és fel nem sorolt, akkor a következőket teheti:
    - Válassza ki a cikk egy másik nevet.
    - Lépjen kapcsolatba a meglévő elemet.

## <a name="why-cant-i-sign-in-with-my-personal-account-but-i-could-sign-in-yesterday"></a>Miért nem tudom jelentkezzen be a személyes fiókkal, de sikertelen bejelentkezés tegnap?

Felhívjuk a figyelmét arra, hogy gyűjtemény fiókját nem alkalmazzák a módosításokat az elsődleges e-mail aliasát. További információkért lásd: [Microsoft E-mail aliasok](https://windows.microsoft.com/windows/outlook/add-alias-account).

## <a name="why-dont-i-see-all-the-gallery-items-when-i-select-all-the-category-checkboxes-on-the-items-tab"></a>Miért nem látom az összes gyűjteményelemet a kategória jelölőnégyzetek az elemek lapon kiválasztott?

A kategória jelölőnégyzet bejelölésével akkor van feltüntetve "Szeretném ebbe a kategóriába tartozó összes elemeket." Csak a kiválasztott kategóriákra elemeinek jelenik meg. Ezért hasonlóan kijelölésével a kategória négyzet jelölését, meg vannak megjelölve "Szeretnék egyetlen kategória összes problémát talál." Azonban minden elem a gyűjteményben nem tartoznak sem kategóriáinak, így azok nem jelennek meg az eredményeket. A gyűjtemény minden elemén, törölje az összes kategória, vagy válassza ismét a elemek lap.

## <a name="what-are-the-requirements-to-publish-a-module-to-the-powershell-gallery"></a>Mik a követelmények, a modul közzétételéhez a PowerShell-galériában?

PowerShell modul (parancsfájl-modulokba, a bináris modulok vagy jegyzék modulok) bármilyen teheti közzé a katalógusban. Modul közzétételéhez PowerShellGet információk – a verzió, néhány dolgot tudnia kell leírása, Szerző és hogyan licencelése. Ezek az információk olvasható a közzétételi folyamat részeként a *moduljegyzék* (.psd1) fájl, vagy az értéke a [ **Publish-modul** ](https://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409) parancsmag **LicenseUri** paraméter. A katalógusban közzétett összes modul modul jegyzékfájlokban kell rendelkeznie. Bármely modul, amely a következő információkat tartalmazza a jegyzékben teheti közzé a gyűjteményben:

- Verzió
- Leírás
- Szerző
- A licencfeltételeket, a modul, vagy részeként mutató URI-t a **PrivateData** a jegyzék, vagy a szakasz a **LicenseUri** paramétere a [ **Publish-modul** ](https://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409) parancsmag.

## <a name="how-do-i-create-a-correctly-formatted-module-manifest"></a>Hogyan hozható létre egy megfelelően formázott moduljegyzék?

Egy moduljegyzék létrehozásához legegyszerűbb módja a futtassa a [ **New-ModuleManifest** ](https://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409) parancsmag. PowerShell 5.0-s vagy újabb, a New-ModuleManifest hoz létre egy megfelelően formázott moduljegyzék például hasznos metaadatok üres mezők **ProjectUri**, **LicenseUri**, és **címkék**. Egyszerűen csak töltse ki a üres értékeket, vagy használja a létrehozott jegyzékre megfelelő formázását példát.

Győződjön meg arról, hogy minden szükséges metaadatok mezők megfelelően ki van töltve, használja a [ **teszt-ModuleManifest** ](https://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409) parancsmag.

A modul jegyzékfájl mezők frissítéséhez használja a [ **frissítés-ModuleManifest** ](https://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409) parancsmag.

## <a name="what-are-the-requirements-to-publish-a-script-to-the-gallery"></a>Mik a követelmények, a parancsfájl közzétételéhez a katalógusban?

PowerShell parancsfájl (parancsfájlok és munkafolyamatok) bármilyen teheti közzé a katalógusban. Parancsfájl közzétételét, PowerShellGet információk – a verzió, néhány dolgot tudnia kell leírása, Szerző és hogyan licencelése. Ezt az információt a parancsfájl-fájlból a közzétételi folyamat részeként olvasható *PSScriptInfo* szakaszban, vagy az értéke a [ **Publish-parancsfájl** ](https://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409) parancsmag  **LicenseUri** paraméter. A katalógusban közzétett összes parancsfájl metaadat-információt kell rendelkeznie. Bármely parancsfájl, amely tartalmazza a következő információkat PSScriptInfo szakaszban található a gyűjteményelem közzé kell tenni:

- Verzió
- Leírás
- Szerző
- A licencfeltételeket, a parancsfájl, részeként mutató URI-t a **PSScriptInfo** a parancsfájl vagy a szakasz a **LicenseUri** paramétere a [ **Publish-parancsfájl** ](https://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409) parancsmag.

## <a name="how-do-i-search"></a>Hogyan kereshető?

Adja meg, mi keres a szövegmezőben. Például ha azt szeretné, a kapcsolódó Azure SQL modulok keresése zajlik, csak gépelje "azure sql". A keresőmotor azokat az összes közzétett elemek, többek között a címét, leírását és metaadatok között kulcsszavak keresi. Ezt követően a súlyozott minőségi pontszám alapján, jelenik meg a leginkább megfelel. Egyedi mező mező szerint is kereshet: "érték" szintaxist a keresési lekérdezés az alábbi mezők:

- Címkék
- Funkciók
- Parancsmagok
- DscResources
- PowerShellVersion

Igen, például ha PowerShellVersion keres: "2.0" csak eredmények, amelyek kompatibilisek-e (a modul, a parancsfájl jegyzékfájl alapján) PowerShellVersion 2.0 fog megjelenni.

## <a name="how-do-i-create-a-correctly-formatted-script-file"></a>Hogyan hozható létre egy megfelelően formázott parancsfájlt?

Hozzon létre egy megfelelően formázott parancsfájlt a legegyszerűbb módja futtatásához a [ **New-ScriptFileInfo** ](https://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409) parancsmag. PowerShell 5.0-s, új-ScriptFileInfo hoz létre egy megfelelően formázott parancsfájl üres mezők például hasznos metaadatok **ProjectUri**, **LicenseUri**, és **címkék** . Egyszerűen adja meg az üres, vagy használjon a létrehozott parancsfájlt példa bemutatja, hogy megfelelő formázását.

Győződjön meg arról, hogy minden szükséges metaadatok mezők megfelelően ki van töltve, használja a [ **teszt-ScriptFileInfo** ](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409) parancsmag.

A parancsfájl metaadatmezőket frissítéséhez használja a [ **frissítés-ScriptFileInfo** ](https://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409) parancsmag.

## <a name="what-other-types-of-powershell-modules-exist"></a>Milyen más PowerShell-modulok létezik?

A kifejezés PowerShell-modul a fájlok tényleges funkcióit megvalósító is hivatkozik. Parancsfájl modul fájlok (.psm1) PowerShell-kódot tartalmaznak. A modul bináris fájlok (.dll) lefordított kódot tartalmaznak.

Gondolja át az egyik módja: a mappa, amely magában foglalja a modul az a modul mappa. A modul mappát egy moduljegyzék (.psd1), amely leírja a mappa tartalmát is tartalmazhat. A fájl ténylegesen a munkájuk, a parancsfájl modul (.psm1) és a modul bináris fájlokat (.dll). DSC erőforrások egy meghatározott almappára találhatók, és parancsfájl modul vagy bináris modul fájlokat megvalósítása.

A modulok a gyűjtemény összes modul jegyzékfájlokban, valamint ezek a modulok többsége tartalmazhatja parancsfájl modul vagy modul bináris fájlokat. A kifejezés modul zavaró lehet a különböző jelentésekkel miatt. Explicit módon másként nincs feltüntetve, minden használ, a word modul ezen a lapon tekintse át a modul mappát, amely tartalmazza ezeket a fájlokat.

## <a name="how-does-packagemanagement-relate-to-powershellget-high-level-answer"></a>Hogyan kapcsolódnak PackageManagement PowerShellGet? (Magas szintű válasz)

PackageManagement bármilyen Csomagkezelő való munkához egy közös felületet. Végül PowerShell-modulok, a MSIs, a Ruby gems, a NuGet-csomagok vagy a Perl-modulok által foglalkozik, hogy meg kell tudni parancsokkal PackageManagement meg (Keresés – csomag és Install-Package) található, és telepítheti. PackageManagement ezt végzi, azzal, hogy minden egyes Csomagkezelő PackageManagement keresztül csatlakozó csomag szolgáltatót. Szolgáltatók tegye meg a tényleges munkát; tartalom beolvasása a tárházak találhatók, és a tartalomhoz helyileg telepíteni. Gyakran csomag szolgáltatók egyszerűen elemlista a meglévő csomag kezelőeszközei egy adott csomag típusa.

PowerShellGet, a package manager PowerShell elemekhez. Nincs olyan PowerShellGet funkciókkal rendelkezik PackageManagement keresztül PSModule csomag szolgáltató. Ebből kifolyólag is fut [Install-modul](https://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409) vagy az Install-Package-szolgáltató PSModule modul telepítésére a PowerShell-galériából. Bizonyos PowerShellGet funkciót, beleértve a [frissítés-modul](https://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409) és [Publish-modul](https://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409), PackageManagement parancsok nem érhető el.

Az összegzés PowerShellGet kizárólag arra irányul, amely a prémium csomag felügyeleti tartalom-közzétételi környezetet PowerShell. PackageManagement arra irányul, hogy az ilyen eszközök egy általános készlete keresztül minden csomag felügyeleti feladatait. Unsatisfying találja a választ, ha van egy hosszú válasz, ez a dokumentum alján a **hogyan PackageManagement ténylegesen kapcsolódik PowerShellGet?** szakasz.

További információkért tekintse meg a [PackageManagement projekt lap](https://oneget.org/).

## <a name="how-does-nuget-relate-to-powershellget"></a>Hogyan kapcsolódnak NuGet PowerShellGet?

A PowerShell-galériában egy módosított verziója telepítve a [NuGet gyűjtemény](https://www.nuget.org/). PowerShellGet NuGet-szolgáltatóját használja a NuGet-alapú tárházak találhatók, mint például a PowerShell-galériában együttműködni.

Bármilyen érvényes NuGet tárház vagy a fájlmegosztásnak elleni PowerShellGet is használhatja. Egyszerűen hozzá kell adnia a tárház futtatásával a [ **Register-PSRepository** ](https://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409) parancsmag.

## <a name="does-that-mean-i-can-use-nugetexe-to-work-with-the-gallery"></a>Amely azt jelenti a gyűjtemény használható NuGet.exe használata?

Igen.

## <a name="how-does-packagemanagement-actually-relate-to-powershellget-technical-details"></a>Hogyan PackageManagement ténylegesen kapcsolódik PowerShellGet? (Technikai részleteket)

A technikai részletek alatt PowerShellGet fokozottan PackageManagement infrastruktúráját használja.

A PowerShell-parancsmag rétegben [Install-modul](https://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409) van ténylegesen vékony csomagolásának Install-Package-szolgáltató PSModule.

Az PackageManagement csomag szolgáltató rétegben a PSModule csomag szolgáltató ténylegesen hívja be más PackageManagement csomag szolgáltatók. Például ha (például a PowerShell-galériában) NuGet-alapú gyűjtemények dolgozik, a PSModule csomag szolgáltató használ a NuGet csomag szolgáltató működéséhez a tárházban.

![PowerShellGet architektúra](Images/powershellgetArchitecture.png)

1. ábra: PowerShellGet architektúrája

## <a name="what-is-required-to-run-powershellget"></a>Mi az PowerShellGet futtatásához szükséges?

Általánosságban ajánlott kiadási PowerShellGet modul (vegye figyelembe, hogy szükséges-e a .NET 4.5) legújabb verzióját.

A **PowerShellGet** module használatához **PowerShell 3.0-s vagy újabb**.

Ezért **PowerShellGet** a következő operációs rendszerek egyike szükséges:

- Windows-10
- Windows 8.1 Pro
- Windows 8.1 Enterprise
- Windows 7 SP1
- Windows Server 2016
- Windows Server 2012 R2
- Windows Server 2008 R2 SP1

**PowerShellGet** is szükséges a .NET-keretrendszer 4.5 vagy újabb. Telepítheti a .NET-keretrendszer 4.5 vagy újabb a [Itt](https://msdn.microsoft.com/library/5a4x27ek.aspx).

## <a name="is-it-possible-to-reserve-names-for-items-that-will-be-published-in-future"></a>Az elemek, a jövőben tesznek közzé nevek lefoglalhat?

Nincs lehetőség a guggolós elemek nevei. Ha úgy véli, hogy egy meglévő elem tartott a neve, amely megfelel a cikk több, próbálja meg [való kapcsolódás a tulajdonos elem](psgallery_contacting_item_owners.md). Ha néhány hétre belül nem kap választ, meg, forduljon a támogatási szolgálathoz, és a PowerShell-galériában csapat azt jeleníti meg.

## <a name="how-do-i-claim-ownership-for-items-"></a>Milyen jogcímek a cikkek tulajdonosa?

Tekintse meg [elem tulajdonosainak kezelése a PowerShellGallery.com](Managing-Item-Owners.md) részleteiről.

## <a name="how-do-i-deal-with-an-item-owner-who-is-violating-my-item-license"></a>Hogyan egy elem tulajdonost, aki a cikk licencet van megsértése foglalkozik?

A PowerShell közösségi működjön együtt a cikk tulajdonosok és más elemek tulajdonosai között esetleg felmerülő jogviták javasoljuk.  Azt a célra egy [névfeloldási folyamat vitát](psgallery_dispute_resolution.md) , kérjük, hogy PowerShellGallery.com rendszergazdák intercede előtt hajtsa végre.

