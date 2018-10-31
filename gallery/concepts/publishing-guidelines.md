---
ms.date: 06/12/2017
contributor: JKeithB
keywords: katalógus, a powershell, a parancsmag, a psgallery
description: A kiadók irányelvek
title: PowerShell-galériából közzétételi irányelvek és bevált gyakorlatok
ms.openlocfilehash: 7e9eca8d3372ddf0b94ab42e125991b857456551
ms.sourcegitcommit: aa1129cc2b0ae6e18918b2b0ea70c74915ed019b
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/30/2018
ms.locfileid: "50235405"
---
# <a name="powershellgallery-publishing-guidelines-and-best-practices"></a>PowerShell-Galériabeli közzétételi irányelvek és bevált gyakorlatok

Ez a témakör ismerteti a csomagok, a PowerShell-galériában közzétett széles körben fogad el, és adja meg a nagy értékű a felhasználók számára, hogyan kezeli az a PowerShell-galériából a jegyzékfájl adatokat és nagy visszajelzései alapján a Microsoft teams által használt javasolt lépések PowerShell-galériából felhasználók számát.
Ezen irányelvek betartása közzétett csomagokat kell telepíteni, nagy valószínűséggel megbízható, és a további felhasználókat szerezzen.

Útmutató a megfelelő PowerShell-galériából csomag, milyen választható jegyzékfájl beállítások legfontosabb, visszajelzést kapjanak az kezdeti teszik a felülvizsgálók a kód javításához teszi az alábbi vannak és [Powershell parancsfájl Analyzer](https://aka.ms/psscriptanalyzer), verziókezelés a modul, a dokumentáció, a tesztek és a példák a mi megosztott használata.
Ez a dokumentáció részét a következő közzétételi irányelvei [magas minőségű DSC erőforrás modulok](https://github.com/PowerShell/DscResources/blob/master/HighQualityModuleGuidelines.md).

A beállítás esetén a csomag közzétételét a PowerShell-galériából, lásd: [létrehozása és közzététele egy csomag](/powershell/gallery/how-to/publishing-packages/publishing-a-package).

Ezeket az irányelveket a visszajelzés üdvözölte van. Ha visszajelzést, nyissa meg a problémákat a [Github dokumentációs tárház](https://github.com/powershell/powershell-docs/issues).

## <a name="best-practices-for-publishing-packages"></a>Ajánlott eljárások a csomagok közzététele

A következő gyakorlati tanácsok Mi a felhasználók PowerShell-galériából elemek tegyük fel, fontos, és névleges prioritási sorrendben vannak felsorolva.
Csomagok, amelyek az alábbiakra sokkal valószínűbb, letöltődnek és mások által elfogadott.

- PSScriptAnalyzer használata
- Dokumentáció és példák
- Legyen elérhető a felhasználói visszajelzések
- Adja meg a szkriptek helyett modulok
- Egy projekt hely mutató hivatkozásokat tartalmaznak
- Tartalmazza a modulok tesztek
- Közé tartozik, és/vagy a szerződés csatolása
- A kód aláírása
- Hajtsa végre a [SemVer](http://semver.org/) irányelvek verziószámozása
- Használjon címkéket, gyakori PowerShell-galériából címkék leírtak szerint
- Közzététel a helyi tárház használatával tesztelése
- A PowerShellGet használatával elvégezhető a közzététel

Minden egyes foglalkozik röviden az alábbi szakaszokban.

## <a name="use-psscriptanalyzer"></a>PSScriptAnalyzer használata

[PSScriptAnalyzer](https://www.powershellgallery.com/packages/PSScriptAnalyzer) egy ingyenes statikus elemző eszköz, a PowerShell-kód működik.
A PowerShell-kódot, és gyakran egy javaslatot a hiba megoldásával leggyakoribb problémáinak PSScriptAnalyzer azonosítja.
Az eszköz egyszerűen használható, és kategorizálja a problémákról, hibák (súlyos, vonhat), Figyelmeztetőre (át kell tekinteni és beavatkozást igényel.), és információkat (érdemes kivétele ajánlott eljárások).
A PowerShell-galériában közzétett összes csomag PSScriptAnalyzer beolvasandó, és az esetleges hibákat jelentést küld a tulajdonos vissza, és vonhat.

Az ajánlott eljárás, hogy futtassa `Invoke-ScriptAnalyzer` a `-Recurse` és `-Severity` figyelmeztetés.

Tekintse át az eredményeket, és ellenőrizze, hogy:

- Minden hibát kijavított vagy ellenáll a dokumentáció a
- Minden figyelmeztetés felül, és adott esetben címzett

Felhasználók, akik a PowerShell-galériából csomagok beszerzése időveszteség PSScriptAnalyzer futtatásához, és az összes hiba és figyelmeztetés kiértékeléséhez.
Nagyon valószínű csomag tulajdonosok kapcsolatba, ha azok jelenik meg, hogy nincs-e PSScriptAnalyzer által jelentett hiba, a felhasználók.
Egy jelentős indok, hogy a kódot, amely meg van jelölve, amely során a csomag esetén adja hozzá ezt az információt a dokumentációban ugyanezt a kérdést megválaszolni sokszor ne kelljen.

## <a name="include-documentation-and-examples"></a>Dokumentáció és példák

Dokumentáció és példákat is az a legjobb módszer annak garantálására, felhasználók kihasználhatják a közös kód.

Dokumentáció az a leginkább hasznos tudnivaló, hogy a PowerShell-galériában közzétett csomagokat felvenni.
Felhasználók általában megkerülik nem dokumentáció, csomagok, a tulajdonos alternatív, hogy olvassa el a kódot, és ismerje meg a csomag t, és hogyan használható a.
Nincsenek elérhető kapcsolatos dokumentáció a PowerShell-csomagok, például a több cikkek:

- Útmutató a Súgó szerepelnek [arról, hogy miként írhat parancsmag](https://go.microsoft.com/fwlink/?LinkID=123415)
- Hozza létre a parancsmag súgóját, akkor a legjobb módszer a PowerShell-parancsfájlt, függvényt vagy parancsmagot.
  Parancsmag súgóját létrehozásával kapcsolatos további információkért kezdődnie [arról, hogy miként írhat parancsmag](https://go.microsoft.com/fwlink/?LinkID=123415).
  Adjon hozzá egy parancsfájlban súgó, lásd: [kapcsolatos megjegyzés-alapú súgó](/powershell/module/microsoft.powershell.core/about/about_comment_based_help).
- Számos modulok is dokumentáció szöveges formátumban, például a MarkDown-fájlok.
  Ez különösen hasznos lehet, ha a Githubon, ahol a Markdown egy olyan kitett formátum egy projekt hely van.
  Az ajánlott eljárás a használandó [Github-stílusú Markdown](https://help.github.com/categories/writing-on-github/)

Példák bemutatják a felhasználók hogyan a csomag javasolt használni.
Sok fejlesztő tudatja Önnel, hogy megtekintik a példákat, mielőtt dokumentáció segít megérteni, hogyan dolgot használni.
Példák megjelenítése alapvető használatát, plusz egy szimulált valósághű használati esetekhez és a kód a legjobb típusa nem jól megjegyzésekkel.
Példák a PowerShell-galériában közzétett modulok egy példa a modul legfelső szintű mappát kell lennie.

Egy jó minta példákat találhat a [PSDscResource modul](https://www.powershellgallery.com/packages/PSDscResources) a Examples\RegistryResource mappában.
Nincsenek négy minta használati esetek az egyes fájlok tetején egy rövid leírást, hogy milyen bemutatott dokumentumokat.

## <a name="respond-to-feedback"></a>Visszajelzés válaszolni

A Közösség által magas értékelni csomag tulajdonosok, akik visszajelzést megfelelően válaszolnak.
Felhasználók, akik visszajelzést vélelmezett fontosak válaszolni, mivel ezek elég iránt javítására, próbálja ki a csomagot.

Visszajelzés két módszer érhető el a PowerShell-galériában található:

- Kapcsolattartási tulajdonos: Ez lehetővé teszi, hogy egy felhasználó egy e-mailt küldhet a csomag tulajdonost. Csomag tulajdonosai fontos, hogy a PowerShell-galériából csomagok használt e-mail cím figyelheti, és reagálhat rájuk problémákat, amelyek akkor aktiválódnak. Egy ezt a módszert hátránya, hogy csak a felhasználó és a tulajdonos minden eddiginél megjelenik a kommunikációt, így a tulajdonos ugyanezt a kérdést megválaszolni sokszor előfordulhat, hogy rendelkezik.
- Megjegyzés: A csomag lap alján megjegyzés mező kitöltése.
  Ebbe a rendszerbe előnye, hogy más felhasználók láthatják a megjegyzések és a válaszok, ami csökkenti az, hogy hányszor bármely egyetlen kérdésre válaszolni kell.
  A csomag tulajdonosával, erősen ajánlott, hogy kövesse az egyes csomagokhoz tartozó megjegyzések.
Lásd: [visszajelzés biztosít a közösségi médiában vagy megjegyzésekkel](../how-to/working-with-packages/social-media-feedback.md) hogyan valósítható meg a részleteket.

A tulajdonosok, akik visszajelzést zárójelentésben válaszolni a Közösség által vannak értékeljük.
A jelentés a lehetőség segítségével további információt kérhet, ha szükséges, adja meg a probléma megoldásához, vagy azonosítását, ha egy frissítés kijavítja a hibát.

Ha nem megfelelő viselkedésének megfigyelt vagy a kommunikációs csatornákat, a PowerShell-galériából visszaélés jelentése funkcióját használja, lépjen kapcsolatba a katalógus-rendszergazdák.

## <a name="modules-versus-scripts"></a>Szkriptek és modulok

Parancsfájl más felhasználókkal való megosztás is remek megoldást kínál, és más biztosít a példa bemutatja, hogyan lehet a problémák megoldásában.
A probléma oka, hogy a PowerShell-galériából a parancsfájlok-e külön dokumentáció, példákat és tesztek nélkül egyetlen fájlokat.

PowerShell-modulok a mappastruktúrát, amely lehetővé teszi több mappákat és fájlokat a csomag része van.
A modul szerkezete lehetővé teszi, hogy többek között a más csomagokat, hogy listában ajánlott eljárások: parancsmag súgójában, dokumentáció, példák és tesztek.
A legnagyobb hátránya, hogy a parancsfájl egy modul belül elérhetővé tett kell, és függvényében használatos.
Modul létrehozásával kapcsolatos információkért lásd: [Windows PowerShell-modul írása](http://go.microsoft.com/fwlink/?LinkId=144916).

Vannak helyzetek, ahol a parancsfájl DSC-konfigurációk, különösen a felhasználót jobb felhasználói élményt biztosít.
DSC-konfigurációk esetén az ajánlott eljárás, hogy a konfiguráció közzététele egy kísérő modult, amely tartalmazza a docs, példákat és tesztek parancsfájlként.
A parancsfájl tartalmazza a kísérő modul RequiredModules = @(a modul neve).
Ez a módszer minden más parancsfájl használható.

Kövesse az ajánlott eljárásokat önálló parancsprogramok valós értéket adjon meg más felhasználók számára.
Biztosít egy parancsfájlt a PowerShell-galériából való közzétételkor erősen ajánlott dokumentáció Megjegyzés-alapú és a egy projekt webhelyre mutató hivatkozás.

## <a name="provide-a-link-to-a-project-site"></a>Adjon meg egy hivatkozást a projekt hely

Egy projekt hely, ahol a közzétevő is közvetlenül kommunikál a felhasználók a saját PowerShell-galériából csomagok.
Felhasználók inkább a csomagok, amelyek biztosították ezt, mert lehetővé teszi számukra, hogy könnyebben csomaggal kapcsolatos információkat.
A PowerShell-galériából a csomagok számát a GitHub lettek kifejlesztve, mások által biztosított dedikált webes telephellyel rendelkező szervezetek számára.
Minden egyes lehessen venni egy projekt helyet.

Hivatkozás hozzáadása azzal ProjectURI a jegyzékfájl PSData szakaszban a következő történik:

        # A URL to the main website for this project.
        ProjectUri = 'https://github.com/powershell/powershell'

Ha egy ProjectURI áll rendelkezésre, a PowerShell-galériából tartalmaz egy hivatkozást a projekt webhelyére, a csomag lap bal oldalán.

## <a name="include-tests"></a>Tesztek belefoglalása

Többek között a nyílt forráskóddal tesztek fontos a felhasználók számára, garancia, ellenőrizze, és mit információkat biztosít a kód működése nyújtja őket. Lehetővé teszi továbbá a felhasználókat irányítva biztosítják, hogy azok nem hibásodik az eredeti funkciót, ha a kód megfelelően környezetükben módosíthatják.

Erősen ajánlott, hogy tesztek írható kihasználhatja a Pester teszt keretrendszer, amely kifejezetten a PowerShell úgy lett kialakítva.
Pester érhető el [GitHub](https://github.com/Pester/Pester), a [PowerShell-galériából](https://www.powershellgallery.com/packages/Pester/), és a Windows 10-es, a Windows Server 2016, a WMF 5.0 és a WMF 5.1 letöltésként érhető el.

A [github project-webhely Pester](https://github.com/Pester/Pester) Pester teszteket, írásáról az első lépésektől ajánlott eljárások a megfelelő dokumentációja tartalmazza.

Tesztelési lefedettségről célértékei hívjuk a [magas minőségű Resource modul dokumentációjában](https://github.com/PowerShell/DscResources/blob/master/HighQualityModuleGuidelines.md), 70 %-os egységgel tesztelje a kódot lefedettség ajánlott.

## <a name="include-andor-link-to-license-terms"></a>Közé tartozik, és/vagy a szerződés csatolása

A PowerShell-galériában közzétett összes csomag meg kell adnia a licencfeltételek figyelje, illetve a licenc tartalmazza a [használati](https://www.powershellgallery.com/policies/Terms) "Függelék A" alatt.
Adjon meg egy másik licenc a legjobb módja, hogy adjon meg egy hivatkozást a licenc az LicenseURI PSData használatával.
A jegyzékfájl mezők ajánlott témakörben találhat egy példát.

```powershell
PrivateData = @{
    PSData = @{

        # Tags applied to this module. These help with module discovery in online galleries.
        Tags = @('.net','acl','active-directory')

        # A URL to the license for this module.
        LicenseUri = 'http://www.apache.org/licenses/LICENSE-2.0'
```

## <a name="sign-your-code"></a>A kód aláírása

Kód aláírása biztosítja a legmagasabb szintű megbízhatóságra számára közzétett, a csomagot a felhasználók, és, hogy a kód másolatát vásárolnak pontosan a közzétevő nyilvánosan.
Kód aláírása általában kapcsolatos további információkért lásd: [Bevezetés a kódaláírás](http://go.microsoft.com/fwlink/?LinkId=106296).
PowerShell érvényesítési kód két elsődleges megközelítés keresztül regisztráló támogatja:

- Parancsfájl fájlok aláírása
- A katalógus aláíró modul

PowerShell fájlok aláírása nem jól bevált megoldást arra, hogy a kód a végrehajtás alatt egy megbízható forrás által előállított volt, és nem lett módosítva.
PowerShell-parancsfájlok aláírásáról részletek tárgyalja a [kapcsolatos aláírási](/powershell/module/microsoft.powershell.core/about/about_signing) témakör.
Az Áttekintés aláírás bármely is hozzáadhatók. PS1 fájlnevet, amely PowerShell ellenőrzi a parancsfájl betöltésekor.
PowerShell használatával lehet korlátozott a [végrehajtási házirend](/powershell/module/microsoft.powershell.core/about/about_execution_policies) parancsmagok használata érdekében aláírt parancsfájlok.

Modulok aláírási katalógus funkciója PowerShell 5.1-es hozzáadva.
Csatlakozás a modul foglalkozik a [katalógus parancsmagok](/powershell/wmf/5.1/catalog-cmdlets) témakör.
Az Áttekintés katalógus aláírási végzi el hozzon létre egy katalógus fájlt, amely minden fájlhoz, a modul ujjlenyomat értéket tartalmaz, és majd a fájl aláírása.
A PowerShellGet modul közzététele, install-module, save-module és update-modul parancsmagjaival fog ellenőrizze, hogy érvényes az aláírást, majd győződjön meg arról, hogy az egyes csomagokhoz tartozó kivonat értéke megegyezik-e a Mi az a katalógusban.
Ha a modul egy korábbi verziója telepítve van a rendszeren, install-module megerősíti, hogy az aláíró szolgáltató az új verzióhoz tartozó megegyezik, amit korábban telepítve lett.
Katalógus aláírási együttműködik, de aláíró parancsfájlok nem cseréli le. PowerShell modul betöltési idő, nem hitelesíti a katalógus aláírások.

## <a name="follow-semver-guidelines-for-versioning"></a>SemVer irányelvekhez verziószámozása

[SemVer](http://semver.org/) van egy nyilvános egyezmény, amely azt ismerteti, hogyan struktúra és a egy verziót, hogy a változások könnyen intepretation módosítása.
A verzió a csomag az alkalmazásjegyzék adatokat kell szerepelnie.

- A verzió megfelelően strukturálni kell, mint 3 numerikus blokkok elválasztott, mint 0.1.1 vagy 4.11.192
- Rendszertől kezdődően a "0" azt jelzik, hogy a csomag még nem éles üzemre, és az első szám csak kezdődjön 0-s, ha egyetlen számot
- Az első szám (1.9.9999 2.0.0) változása jelezheti a verziók közötti fő- és kompatibilitástörő változásokat
- A második szám (1.01 1.02) módosításai jelezheti szövegen túl szolgáltatásszintű változásakor, például új parancsmagok hozzáadása a modul
- A harmadik szám módosításai nem kompatibilitástörő változások, például új paraméterei, frissített minták vagy új tesztek jelzi
- Verziók listázása, amikor PowerShell rendezhető a verziók karakterláncként, így 1.01.0 lesz kezelve a nagyobb 1.001.0

Így támogatást biztosít a legtöbb, de nem minden elemét SemVer, kifejezetten PowerShell SemVer úgy lett közzétéve, mielőtt lett létrehozva:

- Előzetes karakterláncok nem támogatja a verziószámok. Ez akkor hasznos, ha a kiadó által blokkolni kívánt új főbb verziók előzetes kiadása biztosít egy 1.0.0-s verziójának megadása után. Ez a PowerShell-galéria és a PowerShellGet-parancsmagok egy későbbi kiadásban támogatott lesz.
- PowerShell és a PowerShell-galériából, hogy verzió karakterláncok 1, 2 és 4 szegmensek. Számos korai modulok nem követte az irányelveket, és a Microsoft termék-verziók tartalmazzák a build információt (például 5.1.14393.1066) számok letiltása a 4. Ezek a különbségek versioning szempontból, figyelmen kívül hagyja.

## <a name="test-using-a-local-repository"></a>Tesztelheti a helyi tárház használatával

A PowerShell-galériából célja nem lehet egy a közzétételi folyamat tesztelési célt.
A legjobb módszer a teljes körű folyamatot, a PowerShell-galériából való közzététel kipróbálásához, hogy állítsa be, és használja a saját helyi tárházában.
Ez több módon is, beleértve a teheti meg:

- Egy helyi PowerShell-galériából példány beállítása használatával a [PS saját katalógus projekt](https://github.com/PowerShell/PSPrivateGallery) a Githubon. Ezen előzetes projekt segít a PowerShell-galériából, amely szabályozhatja, és a vizsgálatok használni egy példányát.
- Állítsa be egy [belső Nuget-tárház](https://blogs.msdn.microsoft.com/powershell/2014/05/20/setting-up-an-internal-powershellget-repository/). Több munka beállításához van szükség, de érvényesíteni a követelmények, nevezetesen az API-kulcs és az e függőségek szerepelnek a cél közzétételekor ellenőrzése még néhány előnye.
- A teszt "tárház" egy fájlmegosztás állíthatja be. Ez egyszerűen elvégezhető, de, egy fájlmegosztást, mert a fentebb feltüntetett ellenőrzések nem kerül sor. Egy lehetséges ebben az esetben előnye, hogy a fájlmegosztás nem ellenőrzi az (kötelező) API-kulcsot, így azonos fő ugyanúgy a PowerShell-galériából való közzétételéhez.

Ezek a megoldások azokkal a Register-PSRepository használatával egy új "tárház", amely használ a - tárház tulajdonság a Publish-Module definiálhat.

Egy további pont teszt közzétételre vonatkozó: minden olyan csomag, a PowerShell-galériából való közzététel nem lehet törölni a az üzemeltetési csapat, akik megerősíti, hogy semmi nem függ a közzétenni kívánt csomag nélkül.
Éppen ezért azt nem támogatják a PowerShell-galériából tesztelési célként, és felveszi a kapcsolatot minden közzétevő, akik úgy valósítja meg.

## <a name="use-powershellget-to-publish"></a>A PowerShellGet használatával elvégezhető a közzététel

Erősen ajánlott, hogy a kiadók a Publish-Module és Publish-Script parancsmagokat használja, a PowerShell-galériából való munka során.
A PowerShellGet létrejött való telepítés és a PowerShell-galériából történő közzétételével kapcsolatos fontos részleteket megjegyzésénél elkerülése érdekében.
A kiadók előfordulhat, hagyja ki a PowerShellGet, és a NuGet-ügyfél vagy a PackageManagement-parancsmagok használata helyett a Publish-Module választotta.
Nincsenek részletek, amelyek egyszerűen kihagyva, számos különböző támogatási kérések eredményez, amelyek.

Ha a nem használt Publish-Module vagy a Publish-Script indok van, kérjük tudassa velünk, a következő címen.
A PowerShellGet GitHub-adattárat probléma fájlt, majd adja meg, amely miatt a válassza a NuGet vagy PackageManagement részleteit.

## <a name="recommended-workflow"></a>Ajánlott munkafolyamat

A legtöbb sikeres megközelítés található, a csomagokhoz, a PowerShell-galériában közzétett szó:

- A kezdeti fejlesztéshez, az egy olyan nyílt forráskódú projekt hely. A PowerShell csapata használ a Githubon.
- Használja a felülvizsgálók visszajelzései és [Powershell parancsfájl Analyzer](https://aka.ms/psscriptanalyzer) beolvasni a kódot, és stabil állapotban
- Dokumentáció, tartalmazza, így mások tudja, hogyan használja a munkahelyi
- A helyi tárház használatával közzétételi művelet kipróbálásához.
- A PowerShell-galériából, ügyelve arra, hogy a dokumentáció és a projekt helyre mutató hivatkozást tartalmazza, hogy egy stabil vagy alfa kiadás közzététele
- Visszajelzések, és a kódba a projekt webhely ismételt futtatásával, majd a stabil frissítések közzétételéhez a PowerShell-galériában
- Példák és Pester tesztek hozzáadása a projekthez, és a modul
- Döntse el, ha szeretné a kódot írja alá a csomagot
- Ha úgy gondolja, hogy a projekt készen áll a használatra az éles környezetben, tegye közzé egy 1.0.0-s verziót a PowerShell-galériában
- Folytassa a visszajelzések és újrafuttathatja a kódban felhasználói bemenet alapján

