---
ms.date: 06/12/2017
contributor: JKeithB, SydneyhSmith
keywords: Galéria, PowerShell, parancsmag, psgallery
description: A közzétevők iránymutatásai
title: PowerShell-galéria közzétételi irányelvek és ajánlott eljárások
ms.openlocfilehash: b470dbd81e79d2a6a228b8c89f85e57c03803ede
ms.sourcegitcommit: 5a004064f33acc0145ccd414535763e95f998c89
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/23/2019
ms.locfileid: "69986505"
---
# <a name="powershellgallery-publishing-guidelines-and-best-practices"></a>Galériabeli közzétételi irányelvek és ajánlott eljárások

Ez a témakör azokat a javasolt lépéseket ismerteti, amelyeket a Microsoft Teams használ a PowerShell-galéria közzétett csomagok széles körben való elfogadására és magas érték biztosítására a felhasználók számára, attól függően, hogy a PowerShell-galéria hogyan kezeli a jegyzékfájlok adatait és a nagyméretű visszajelzéseket. PowerShell-galéria felhasználók száma.
Az ezen irányelvek alapján közzétett csomagok nagyobb valószínűséggel lesznek telepítve, megbízhatóak, és több felhasználót vonzanak.

Az alábbiakban a megfelelő PowerShell-galéria csomagra vonatkozó irányelvek olvashatók, melyek a legfontosabb opcionális jegyzékfájl-beállítások, a kód javítása a kezdeti felülvizsgálók és a PowerShell- [parancsfájl elemzője](https://aka.ms/psscriptanalyzer)által, a modul verziószámozása révén dokumentáció, tesztek & példák a megosztott elemek használatára.
A dokumentáció nagy része a [kiváló minőségű DSC-erőforrás-modulok](https://github.com/PowerShell/DscResources/blob/master/HighQualityModuleGuidelines.md)közzétételének irányelveit követi.

A csomagok a PowerShell-galéria való közzétételének mechanikája: [csomagok létrehozása és közzététele](/powershell/gallery/how-to/publishing-packages/publishing-a-package).

Az irányelvekről szóló visszajelzések üdvözölve vannak. Ha visszajelzést szeretne küldeni, nyissa meg a [GitHub dokumentációs tárházában](https://github.com/powershell/powershell-docs/issues)található problémákat.

## <a name="best-practices-for-publishing-packages"></a>Ajánlott eljárások a csomagok közzétételéhez

A következő ajánlott eljárások azt ismertetik, hogy a PowerShell-galéria elemek felhasználói milyen fontosak, és a névleges prioritási sorrendben vannak felsorolva.
Az ezeket az irányelveket követő csomagokat sokkal nagyobb eséllyel töltik le és fogadják el mások.

- PSScriptAnalyzer használata
- Dokumentációval és példákkal együtt
- Válaszoljon a visszajelzésre
- Parancsfájlok helyett a modulok megadása
- A Project-helyre mutató hivatkozások megadása
- A csomag címkézése a kompatibilis PSEdition (s) és platformokkal
- Tesztek belefoglalása a modulokkal
- Licencfeltételek belefoglalása és/vagy hivatkozása
- A kód aláírása
- [SemVer](http://semver.org/) -irányelvek követése a verziószámozáshoz
- Általános címkék használata a közös PowerShell-galéria címkékben dokumentálva
- Közzététel tesztelése helyi tárház használatával
- Közzététel a PowerShellGet használatával

Ezek mindegyikét röviden az alábbi részekben tárgyaljuk.

## <a name="use-psscriptanalyzer"></a>PSScriptAnalyzer használata

A [PSScriptAnalyzer](https://www.powershellgallery.com/packages/PSScriptAnalyzer) egy ingyenes, statikus kód-elemzési eszköz, amely PowerShell-kódban működik.
A PSScriptAnalyzer azonosítja a PowerShell-kódban leggyakrabban előforduló problémákat, és gyakran a probléma megoldására vonatkozó javaslatot is tartalmaz.
Az eszköz könnyen használható, és kategorizálja a hibákat (súlyos, kezelendő), a figyelmeztetést (& kell vizsgálni), és információt (érdemes megnézni az ajánlott eljárásokat).
A PowerShell-galéria közzétett összes csomagot a rendszer a PSScriptAnalyzer használatával vizsgálja, és az esetleges hibákat visszaküldi a tulajdonosnak, és meg kell oldania.

Az ajánlott eljárás az, hogy `Invoke-ScriptAnalyzer` a `-Recurse` és `-Severity` a figyelmeztetés használatával fusson.

Tekintse át az eredményeket, és ügyeljen rá, hogy:

- Az összes hibát kijavítottuk vagy a dokumentációban tárgyaljuk
- Az összes figyelmeztetést felülvizsgálják, és ahol lehetséges, a rendszer tárgyalja

Azok a felhasználók, akik a PowerShell-galéria csomagokat szerzik be, erősen javasoltak a PSScriptAnalyzer futtatására és az összes hiba és figyelmeztetés kiértékelésére.
A felhasználók nagyon valószínű, hogy felveszik a kapcsolatot a csomag tulajdonosainak, ha úgy látják, hogy a PSScriptAnalyzer által jelentett hiba történt.
Ha a csomagnak olyan meggyőző oka van, hogy a kód megtartja a hibát jelző kódot, adja hozzá ezeket az információkat a dokumentációhoz, hogy ne kelljen ugyanarra a kérdésre többször válaszolnia.

## <a name="include-documentation-and-examples"></a>Dokumentációval és példákkal együtt

A dokumentáció és a példák a legjobb módszer annak biztosítására, hogy a felhasználók kihasználhatják a megosztott kódokat.

A dokumentáció a leghasznosabb dolog a PowerShell-galéria közzétett csomagokba való felvételhez.
A felhasználók általában a dokumentáció nélkül fogják megkerülni a csomagokat, mivel a másik lehetőség a kód beolvasása, hogy megtudja, mi a csomag, és hogyan használható.
Több cikk is rendelkezésre áll, amelyekkel megtudhatja, hogyan biztosíthat dokumentációt PowerShell-csomagokkal, beleértve a következőket:

- Útmutató a Súgó használatához a [parancsmag súgójának írásához](https://go.microsoft.com/fwlink/?LinkID=123415)
- A parancsmag súgójának létrehozása, amely a legjobb módszer a PowerShell-parancsfájlok, a függvények vagy a parancsmagok számára.
  A parancsmag súgójának létrehozásával kapcsolatos további információkért Kezdje a [parancsmagok súgójának írásával](https://go.microsoft.com/fwlink/?LinkID=123415).
  Ha egy parancsfájlon belül szeretne segítséget adni, olvassa el [a megjegyzések alapján kapcsolatos súgót](/powershell/module/microsoft.powershell.core/about/about_comment_based_help).
- Számos modul szöveges formátumban is tartalmaz dokumentációt, például MarkDown-fájlokat.
  Ez különösen hasznos lehet abban az esetben, ha a githubon van egy projekt-hely, ahol a Markdown nagy mértékben használt formátum.
  Az ajánlott eljárás a [GitHub ízű Markdown](https://help.github.com/categories/writing-on-github/) használata

A példák azt mutatják be, hogy a csomag mely felhasználók számára készült.
Számos fejlesztő azt fogja mondani, hogy példákat mutatnak be a dokumentációra, hogy megértsük, hogyan kell használni valamit.
A legjobb példa az alapszintű használatot, valamint egy szimulált reális használati esetet mutat be, és a kód jól kommentálva van.
A PowerShell-galéria közzétett modulokra példákat kell megadni a modul gyökerének egyik példás mappájába.

A példákra jó példa található a [PSDscResource modulban](https://www.powershellgallery.com/packages/PSDscResources) a Examples\RegistryResource mappában.
Négy minta használati eset van az egyes fájlok tetején található rövid leírással, amely a dokumentált dokumentációt mutatja.

## <a name="manage-dependencies"></a>Függőségek kezelése

Fontos megadnia azokat a modulokat, amelyeknek a modulja függ a modul jegyzékfájljában.
Ez lehetővé teszi, hogy a végfelhasználó ne kelljen aggódnia a modulok megfelelő verzióinak telepítésével kapcsolatban.
A függő modulok megadásához használja a modul jegyzékfájljának szükséges modul mezőjét.
Ezzel betölti a felsorolt modulokat a globális környezetbe a modul importálása előtt, kivéve, ha azokat már betöltötték. (Például egyes modulokat már egy másik modul is betölt.)
Egy adott verziót is meg lehet adni a betöltéshez a ModuleVersion mező helyett a RequiredVersion mező használatával. A ModuleVersion használatakor a rendszer az elérhető legújabb verziót fogja betölteni legalább a megadott verzióval.
Ha nem használja a RequiredVersion mezőt egy adott verzió megadásához, fontos a verziófrissítések figyelése a szükséges modulra.
Különösen fontos, hogy tisztában legyenek az összes olyan változással, amely hatással lehet a felhasználói élményre a modulban.

```powershell
Example: RequiredModules = @(@{ModuleName="myDependentModule"; ModuleVersion="2.0"; Guid="cfc45206-1e49-459d-a8ad-5b571ef94857"})

Example: RequiredModules = @(@{ModuleName="myDependentModule"; RequiredVersion="1.5"; Guid="cfc45206-1e49-459d-a8ad-5b571ef94857"})
```

## <a name="respond-to-feedback"></a>Válasz a visszajelzésre

A megfelelő visszajelzésre válaszoló csomagok tulajdonosai a Közösségnek igen értékesek.
Azok a felhasználók, akik konstruktív visszajelzést adnak, fontosak a válaszadásra, hiszen a csomagban elég érdeklik, hogy segítsenek a fejlesztésben.

A PowerShell-galéria két visszajelzési módszer érhető el:

- Kapcsolatfelvétel a tulajdonossal: Ez lehetővé teszi, hogy a felhasználó e-mailt küldjön a csomag tulajdonosa (i) nak. A csomag tulajdonosaként fontos figyelni a PowerShell-galéria-csomagokhoz használt e-mail-címet, és reagálni a felmerült problémákra. Ennek a módszernek a hátránya, hogy csak a felhasználó és a tulajdonos fogja látni a kommunikációt, így a tulajdonosnak többször is meg kell válaszolnia ugyanazt a kérdést.
- Megjegyzések A csomag lap alján egy megjegyzés mező szerepel.
  Ennek a rendszernek az előnye, hogy más felhasználók láthatják a megjegyzéseket és a válaszokat, ami csökkenti az egyetlen kérdésre adandó válaszok számát.
  A csomag tulajdonosaként határozottan javasoljuk, hogy kövesse az egyes csomagokra vonatkozó megjegyzéseket.
Tekintse meg a visszajelzéseket a [közösségi médián keresztül, vagy](../how-to/working-with-packages/social-media-feedback.md) a megjegyzésekkel kapcsolatos információkat.

A Közösség méltányolja a visszajelzésre reagáló tulajdonosokat.
Ha szükséges, a jelentésben szereplő lehetőséggel további információkat kérhet, megadhat egy megkerülő megoldást, vagy azonosíthatja, ha egy frissítés javít egy problémát.

Ha a fenti kommunikációs csatornák valamelyike nem felel meg a megfelelő viselkedésnek, akkor a PowerShell-galéria jelentési visszaélés funkciójával lépjen kapcsolatba a katalógus rendszergazdájával.

## <a name="modules-versus-scripts"></a>Modulok és parancsfájlok

A szkriptek más felhasználókkal való megosztása nagyszerű megoldás, és többek között az esetlegesen felmerülő problémák megoldásához nyújt példákat.
A probléma az, hogy a PowerShell-galéria található parancsfájlok külön dokumentáció, példák és tesztek nélkül önálló fájlok.

A PowerShell-modulok rendelkeznek olyan mappastruktúrát, amely lehetővé teszi több mappa és fájl felvételét a csomagba.
A modul szerkezete lehetővé teszi, hogy a többi csomag az ajánlott eljárásoknak megfelelően legyen felsorolva: parancsmag Súgó, dokumentáció, példák és tesztek.
A legnagyobb hátránya, hogy egy modulon belüli szkriptet ki kell tenni, és függvényként kell használni.
A modulok létrehozásával kapcsolatos információkért lásd: [Windows PowerShell-modul írása](http://go.microsoft.com/fwlink/?LinkId=144916).

Vannak olyan helyzetek, amikor egy parancsfájl jobb felhasználói élményt nyújt a felhasználónak, különösen a DSC-konfigurációk esetében.
A DSC-konfigurációk ajánlott gyakorlata, hogy a konfigurációt a dokumentumokat, példákat és teszteket tartalmazó csatolt modullal ellátott parancsfájlként tegye közzé.
A parancsfájl felsorolja a kapcsolódó modult a RequiredModules = @ (a modul neve) használatával.
Ez a módszer bármilyen parancsfájl használatával használható.

Az egyéb ajánlott eljárásokat követő önálló parancsfájlok valós értéket biztosítanak más felhasználóknak.
A Megjegyzés-alapú dokumentáció és a projekt webhelyére mutató hivatkozás használata kifejezetten ajánlott, ha parancsfájlokat tesz közzé a PowerShell-galéria.

## <a name="provide-a-link-to-a-project-site"></a>A projekt webhelyére mutató hivatkozás megadása

A projekt helye, ahol a közzétevő közvetlenül tud kommunikálni PowerShell-galéria csomagjainak felhasználóival.
A felhasználók inkább az ezt biztosító csomagokat részesítik előnyben, mivel így könnyebben kaphatják meg a csomag információit.
A PowerShell-galéria számos csomagja van kifejlesztve a GitHubban, másokat pedig egy dedikált webes jelenléttel rendelkező szervezetek biztosítanak.
Ezek mindegyike egy projekt helyének tekinthető.

A hivatkozások hozzáadásához a következő módon kell megtenni a ProjectURI, beleértve a PSData szakaszt:

        # A URL to the main website for this project.
        ProjectUri = 'https://github.com/powershell/powershell'

ProjectURI megadása esetén a PowerShell-galéria tartalmazni fog egy hivatkozást a projekt webhelyére a csomag lap bal oldalán.

## <a name="tag-your-package-with-the-compatible-pseditions-and-platforms"></a>A csomag címkézése a kompatibilis PSEdition (s) és platformokkal

A következő címkék segítségével bemutathatja azokat a felhasználókat, akik a csomagok jól fognak működni a környezetében:

- PSEdition_Desktop : A Windows PowerShell szolgáltatással kompatibilis csomagok
- PSEdition_Core : A PowerShell Core-kompatibilis csomagok
- Windows A Windows operációs rendszerrel kompatibilis csomagok
- Linux Linux operációs rendszerekkel kompatibilis csomagok
- MacOS A Mac operációs rendszerrel kompatibilis csomagok

Ha címkézi a csomagot a kompatibilis platform (ok) val, a keresési eredmények bal oldali paneljén a katalógus keresési szűrőinek részét képezi majd. Ha a csomagot a githubon futtatja, akkor a csomag címkézése során kihasználhatja a [PowerShell-Galéria compability Shields](https://img.shields.io/powershellgallery/p/:packageName.svg) 
![kompatibilitási pajzsot](https://img.shields.io/powershellgallery/p/CosmosDB.svg)is.  

## <a name="include-tests"></a>Tesztek belefoglalása

A nyílt forráskódot tartalmazó tesztek fontosak a felhasználók számára, mivel biztosítanak garanciát az érvényesítéséhez, és információt nyújt a kód működéséről. Azt is lehetővé teszi a felhasználóknak, hogy ne szakítsák meg az eredeti funkciót, ha a programkódot úgy módosítják, hogy illeszkedjenek a környezetéhez.

Erősen ajánlott a tesztek megírása, hogy kihasználja a kifejezetten a PowerShell-hez készült, a "a"-re vonatkozó tesztelési keretrendszert.
A Pest a [GitHub](https://github.com/Pester/Pester), a [PowerShell-Galéria](https://www.powershellgallery.com/packages/Pester/)és a Windows 10, a Windows Server 2016, a WMF 5,0 és a WMF 5,1 hajókon érhető el.

A [githubon található pesting Project-webhely](https://github.com/Pester/Pester) jó dokumentációt tartalmaz a Pest-tesztek megírásához, az első lépésektől kezdve az ajánlott eljárásig.

A tesztelési lefedettség célját a [magas színvonalú erőforrás-modul dokumentációja](https://github.com/PowerShell/DscResources/blob/master/HighQualityModuleGuidelines.md)hívja meg, a 70%-os tesztelési kód lefedettsége ajánlott.

## <a name="include-andor-link-to-license-terms"></a>Licencfeltételek belefoglalása és/vagy hivatkozása

A PowerShell-galéria közzétett összes csomagnak meg kell határoznia a licencfeltételeket, vagy a használati [feltételekben](https://www.powershellgallery.com/policies/Terms) foglalt licenchez kötve kell lennie.
Egy másik licenc megadásának legjobb módszere, ha a PSData-ben lévő LicenseURI használatával a licencre mutató hivatkozást ad meg.
A következő témakörben talál példát:.

```powershell
PrivateData = @{
    PSData = @{

        # Tags applied to this module. These help with module discovery in online galleries.
        Tags = @('.net','acl','active-directory')

        # A URL to the license for this module.
        LicenseUri = 'http://www.apache.org/licenses/LICENSE-2.0'
```

## <a name="sign-your-code"></a>A kód aláírása

A kód aláírása biztosítja a legmagasabb szintű garanciát a csomag közzétételére, valamint arról, hogy a beszerzett kód másolata pontosan mit jelent a közzétevő számára.
A kódok aláírásával kapcsolatos további tudnivalókért tekintse meg a [kód aláírásának bemutatása](http://go.microsoft.com/fwlink/?LinkId=106296)című témakört.
A PowerShell két elsődleges megközelítéssel támogatja a kódok aláírásának érvényesítését:

- Parancsfájl-fájlok aláírása
- Modul aláírása

A PowerShell-fájlok aláírása jól bevált megközelítés annak biztosítására, hogy a végrehajtott programkódot megbízható forrás hozta létre, és nem módosították.
A PowerShell-parancsfájlok aláírásáról a [tudnivalók](/powershell/module/microsoft.powershell.core/about/about_signing) az aláírásról című témakörben olvashat bővebben.
Az áttekintésben bármelyikhez hozzáadhat egy aláírást. PS1-fájl, amelyet a PowerShell érvényesít a parancsfájl betöltésekor.
A PowerShell a [végrehajtási házirend](/powershell/module/microsoft.powershell.core/about/about_execution_policies) -parancsmagok használatával korlátozható az aláírt parancsfájlok használatának biztosítása érdekében.

A katalógus-aláíró modulok a 5,1-es verzióban a PowerShellhez hozzáadott funkciók.
A modul aláírása a [katalógus](/powershell/wmf/5.1/catalog-cmdlets) -parancsmagok című témakörben található.
Az áttekintésben a katalógus-aláírást egy katalógusfájl létrehozásával végezheti el, amely a modul összes fájljának kivonatoló értékét tartalmazza, majd aláírja a fájlt.
A PowerShellGet Publishing-Module, a install-Module, a Save-Module és az Update-Module parancsmagok ellenőrizhetik az aláírást, hogy érvényesek legyenek, majd győződjön meg róla, hogy az egyes csomagok kivonatoló értéke megegyezik a katalógusban szereplővel.
Ha a modul egy korábbi verziója telepítve van a rendszeren, akkor a install-Module megerősíti, hogy az új verzióhoz tartozó aláíró hatóság megfelel a korábban telepítettnek.
A katalógus-aláírás együttműködik a szolgáltatással, de nem váltja fel az aláíró parancsfájlok fájljait. A PowerShell nem ellenőrzi a katalógus-aláírásokat a modul betöltési idején.

## <a name="follow-semver-guidelines-for-versioning"></a>SemVer-irányelvek követése a verziószámozáshoz

A [SemVer](http://semver.org/) egy nyilvános egyezmény, amely leírja, hogyan lehet egy verziót strukturálni és módosítani a változások egyszerű értelmezése érdekében.
A csomag verziójának szerepelnie kell a jegyzékfájl adatai között.

- A verziónak 3, ponttal elválasztott numerikus blokknak kell lennie, például 0.1.1 vagy 4.11.192
- A "0" kezdetű verziók azt jelzik, hogy a csomag még nem áll készen a gyártásra, és az első szám csak akkor kezdődhet a "0" értékkel, ha ez az egyetlen használatban lévő szám.
- Az első szám változásai (1.9.9999 – 2.0.0) a verziók közötti jelentős és megszakított változásokat jelzik
- A második szám módosításai (1,1 – 1,2) a szolgáltatás szintű módosításokat jeleznek, például új parancsmagok hozzáadása egy modulhoz
- A harmadik szám módosításai a nem törhető módosításokat jelzik, például az új paramétereket, a frissített mintákat vagy az új teszteket.
- A verziók listázásakor a PowerShell karakterláncként rendezi a verziókat, így a 1.01.0 a 1.001.0-nál nagyobb mértékben lesz kezelve.

A PowerShell a SemVer közzététele előtt lett létrehozva, így a SemVer a legtöbb, de nem az összes elemének támogatását biztosítja, pontosabban:

- A verziószámokban nem támogatja az előzetes kiadású karakterláncokat. Ez akkor hasznos, ha a kiadó egy új főverzió előzetes kiadását szeretné kézbesíteni a 1.0.0 verziójának megadása után. Ez a PowerShell-galéria és a PowerShellGet-parancsmagok jövőbeli kiadásában lesz támogatott.
- A PowerShell és a PowerShell-galéria lehetővé teszik az 1, 2 és 4 szegmensek verziószámát. Számos korai modul nem követte az irányelveket, és a Microsoft termék-kiadásainak negyedik blokkja (például 5.1.14393.1066) alapján kell felépíteni az adatokat. A verziószámozás szempontjából ezeket a különbségeket a rendszer figyelmen kívül hagyja.

## <a name="test-using-a-local-repository"></a>Tesztelés helyi tárház használatával

A PowerShell-galéria nem a közzétételi folyamat tesztelésére szolgáló cél.
A legjobb módszer, ha tesztelni szeretné a PowerShell-galéria közzétételének végpontok közötti folyamatát, és saját helyi tárházat kell beállítania és használnia.
Ez többféleképpen is elvégezhető, többek között:

- Hozzon létre egy helyi PowerShell-galéria példányt a githubon a [PS Private Gallery-projekt](https://github.com/PowerShell/PSPrivateGallery) használatával. Ez az előzetes verziójú projekt segítséget nyújt azon PowerShell-galéria példányának beállításához, amelyekkel szabályozható és használható a tesztek.
- Hozzon létre egy [belső Nuget](https://blogs.msdn.microsoft.com/powershell/2014/05/20/setting-up-an-internal-powershellget-repository/)-tárházat. Ehhez több munkát kell beállítania a beállításhoz, de az előnye, hogy több követelményt is érvényesít, például az API-kulcs használatának érvényességét, valamint azt, hogy a cél a közzétételkor megjelenjen-e a függőségek között.
- Hozzon létre egy fájlmegosztást "adattár" tesztként. Ez egyszerűen beállítható, de mivel ez egy fájlmegosztás, a fentiekben ismertetett érvényesítések nem lesznek érvényben. Ebben az esetben az egyik lehetséges előnye, hogy a fájlmegosztás nem vizsgálja meg a (kötelező) API-kulcsot, így ugyanazt a kulcsot használhatja, amelyet közzé szeretne tenni a PowerShell-galéria.

Bármelyik megoldás esetében a Register-PSRepository használatával Definiáljon egy új "tárházat", amelyet a közzétételi modul adattár tulajdonságában használhat.

Egy további pont a tesztek közzétételével kapcsolatban: a PowerShell-galéria közzétett bármely csomag nem törölhető az operatív csapat segítsége nélkül, aki megerősíti, hogy semmi nem függ a közzétenni kívánt csomagtól.
Ezért nem támogatjuk a PowerShell-galéria tesztelési célként, és felvesszük Önnel a kapcsolatot.

## <a name="use-powershellget-to-publish"></a>Közzététel a PowerShellGet használatával

Erősen ajánlott, hogy a közzétevők a közzétételi modult és a publish-script parancsmagokat használják a PowerShell-galéria használatakor.
A PowerShellGet azért jött létre, hogy elkerülje a PowerShell-galéria telepítésének és közzétételének fontos részleteit.
Alkalmanként a kiadók úgy döntöttek, hogy kihagyják a PowerShellGet, és az NuGet-ügyfelet, vagy a PackageManagement-parancsmagokat használják a közzétételi modul helyett.
A könnyen kihagyható részletek számos különböző támogatási kérést eredményeznek.

Ha valamilyen okból kifolyólag nem használhatja a közzétételi modult vagy a publish-scriptet, kérjük, tudassa velünk.
Fájl a PowerShellGet GitHub-tárházban, és adja meg a NuGet vagy a PackageManagement kiválasztását kiváltó adatokat.

## <a name="recommended-workflow"></a>Javasolt munkafolyamat

A PowerShell-galéria közzétett csomagok legsikeresebb megközelítése a következő:

- A kezdeti fejlesztést egy nyílt forráskódú projektbeli helyen végezze el. A PowerShell-csapat a Githubot használja.
- Visszajelzés küldése a felülvizsgálók és a [PowerShell-parancsfájl-elemző](https://aka.ms/psscriptanalyzer) számára a kód stabil állapotba való beolvasásához
- Dokumentáció belefoglalása, hogy mások is tudják, hogyan használják a munkájukat
- Próbálja ki a közzétételi műveletet egy helyi tárház használatával.
- Tegyen közzé egy stabil vagy alfa-kiadást a PowerShell-galériaon, és ügyeljen rá, hogy tartalmazza a dokumentációt és a projekt webhelyére mutató hivatkozást.
- Gyűjtsön visszajelzést, és ismételje meg a kódot a projekt webhelyén, majd tegye közzé a stabil frissítéseket a PowerShell-galéria
- Példák és a felzaklató tesztek hozzáadása a projektben és a modulban
- Döntse el, hogy szeretné-e aláírni a csomagot
- Ha úgy érzi, hogy a projekt készen áll az éles környezetben való használatra, tegye közzé a 1.0.0-verziót a PowerShell-galéria
- Folytassa a visszajelzések összegyűjtését, és ismételje meg a kódot a felhasználói bevitel alapján
