---
ms.date: 2017-06-12
contributor: JKeithB
ms.topic: conceptual
keywords: "gyűjtemény, a powershell, a parancsmag, a psgallery"
description: "Közzétevők vonatkozó irányelvek"
title: "PowerShell-galériában irányelvek és bevált gyakorlatok közzététele"
ms.openlocfilehash: 25bbe31bcc805808c311829598e3c29991f72aad
ms.sourcegitcommit: 99227f62dcf827354770eb2c3e95c5cf6a3118b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/15/2018
---
# <a name="powershellgallery-publishing-guidelines-and-best-practices"></a>PowerShellGallery irányelvek és bevált gyakorlatok közzététele

Ez a témakör ismerteti a javasolt lépéseket, győződjön meg arról, a PowerShell-galériában közzétett cikkek széles körben fogad el, és adja meg a nagy értékű a felhasználóknak, miként kezeli a PowerShell-galériában a jegyzék adatok és sok visszajelzései alapján Microsoft csapatai által használt a PowerShell-galériában felhasználók.
A cikkeket betartásuk közzétett telepíthető, nagy valószínűséggel megbízható, pedig további felhasználók vonzerőt.

Egy jó PowerShell gyűjteményelem, mely opcionális jegyzék beállításokat a legfontosabbak, a kódot a kezdeti véleményezők visszajelzést javítása hasznossá vonatkozó irányelvek alábbi vannak és [Powershell parancsfájl Analyzer](https://aka.ms/psscriptanalyzer), versioning a modul, dokumentáció, a vizsgálatok és az használata, mi megosztott példák.
Nagy részét a dokumentáció a következő közzétételi irányelveiről [magas minőségi DSC erőforrás modulok](https://github.com/PowerShell/DscResources/blob/master/HighQualityModuleGuidelines.md).

A cikk közzétételéhez a PowerShell-galériában idejéről, lásd: [létrehozása és közzététele egy elem](https://msdn.microsoft.com/powershell/gallery/psgallery/creating-and-publishing-an-item).

Ezeket az irányelveket kapcsolatos visszajelzéseket üdvözölte van. Ha van, nyissa meg a problémákat a [dokumentáció Github-tárházban](https://github.com/powershell/powershell-docs/).

## <a name="best-practices-for-publishing-items"></a>Ajánlott eljárások az elem közzététele

A következő gyakorlati tanácsok mi PowerShell gyűjteményelemek felhasználóinak tegyük fel például azért fontos, és névleges prioritási sorrendben vannak felsorolva.
Kövesse az alábbi irányelveket elemekre valószínűleg sokkal letöltött és mások által elfogadott.

* PSScriptAnalyzer használata
* Dokumentáció és példák
* Visszajelzés válaszol kell
* Adja meg a parancsfájlok helyett modulok
* Adja meg a projekt hely mutató hivatkozások
* A modulok tesztek tartalmazza
* Tartalmaznak és/vagy csatolja a licencfeltételeket
* A kód aláírása
* Hajtsa végre a [SemVer](http://semver.org/) versioning vonatkozó irányelvek
* Használja a címkéket, dokumentált módon gyakori PowerShell-galériában címkék
* Egy helyi tárház közzétételen tesztelése

Ezek mindegyikének vonatkozik röviden az alábbi szakaszokban.

## <a name="use-psscriptanalyzer"></a>PSScriptAnalyzer használata

[PSScriptAnalyzer](https://www.powershellgallery.com/packages/PSScriptAnalyzer) szabad statikus kód elemző eszköz, amely PowerShell-kódjába működéséről.
PSScriptAnalyzer látható a PowerShell-kódot, és gyakran egy javaslatot a probléma megoldásával kapcsolatos leggyakoribb hibák azonosítja.
Az eszköz könnyen használható, és a problémákat hibaként kategorizálja (súlyos, számos), figyelmeztetés (át kell tekinteni & foglalkozzon), és információkat (érdemes kikérése ajánlott eljárások).
A PowerShell-galériában közzétett összes elemek elem PSScriptAnalyzer beolvasandó, és az esetleges hibákat jelentett vissza a tulajdonos, és kell figyelembe venni.

A bevált gyakorlat az, hogy futtassa `Invoke-ScriptAnalyzer` rendelkező `-Recurse` és `-Severity` figyelmeztetés.

Tekintse át az eredményeket, és győződjön meg arról, hogy:

* Az összes hiba kijavítására sor vagy dokumentumban tárgyalt
* Az összes figyelmeztetés felülvizsgálata és adott esetben címzett

Szerezzen be a PowerShell-galériából elemek felhasználók javasoljuk, hogy a PSScriptAnalyzer futtatni, és értékelje ki az összes hiba és figyelmeztetés.
A felhasználók nagyon valószínűleg elem tulajdonosok csatlakozni, ha akkor jelenik meg, hogy van-e PSScriptAnalyzer által jelentett hiba.
Ha a kódot hibaként megjelölt tartani a cikkhez jelentős indok arra, vegye fel ezt az információt a dokumentációját, ne kelljen ugyanezt a kérdést válaszoljon sokszor.

## <a name="include-documentation-and-examples"></a>Dokumentáció és példák

Dokumentáció és példák, amelyek a legjobb felhasználók mértékben kihasználhassa az összes megosztott kódot.

Dokumentáció a lehető leghasznosabb tudnivaló, hogy szerepeljen a PowerShell-galériában közzétett elemeket is.
Felhasználók általában kihagyása a cikkek dokumentáció nélkül, mivel ez esetben olvassa el a kódot, hogy megtudja, mi az az elem és való használatát.
Nincsenek elérhető az MSDN dokumentációját a PowerShell elemek, beleértve a vonatkozó több olyan cikket:

* Súgó vonatkozó irányelvek szerepelnek [arról, hogy miként írási parancsmag](https://go.microsoft.com/fwlink/?LinkID=123415)
* Parancsmag súgójának létrehozására, akkor a legjobb módszer a PowerShell-parancsfájl, függvényt vagy parancsmagot.
  A parancsmag súgójában talál létrehozásával kapcsolatos információért kezdje [arról, hogy miként írási parancsmag](https://go.microsoft.com/fwlink/?LinkID=123415) az MSDN könyvtárában.
  Egy parancsfájlban súgó hozzáadása, lásd: [Megjegyzés-alapú súgó](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/about/about_comment_based_help).
* Számos modult is dokumentáció szöveges formátumú, például a MarkDown-fájlokat.
  Ez különösen hasznos lehet, ha a github webhelyen, ahol a Markdown terhelésnek kitett formátum a projekt hely van.
  A bevált gyakorlat [Github-stílusú Markdown](https://help.github.com/categories/writing-on-github/)

Példák megjelenítése a felhasználók hogyan a cikk célja, hogy használható.
Sok fejlesztők megtudhatja, hogy, hogy megnézi a példák dokumentációját, valami használata előtt.
A legjobb a példák megjelenítése alapvető használata, valamint szimulált valósághű használati esetek és a kód típus jól megjegyzésként.
A PowerShell-galériában közzétett modulok példák a modul legfelső szintű példák mappában kell lennie.

Egy jó példák mintát itt található: a [PSDscResource modul](https://www.powershellgallery.com/packages/PSDscResources) a Examples\RegistryResource mappában.
Nincsenek négy minta használati esetek az egyes fájlok tetején rövid leírását, hogy mi bemutatott dokumentumok.

## <a name="respond-to-feedback"></a>Visszajelzés válaszolni

Visszajelzés megfelelően válaszolni elem tulajdonosok magas kell értékelni a Közösség által.
Felhasználók, akik vélelmezett visszajelzést fontosak válaszolni, mivel ezek érdekelt, elég azt javítása érdekében próbálkozzon az elemben.

Kétféleképpen visszajelzés érhető el a PowerShell-galériában:

* Kapcsolattartási tulajdonos: Ezzel a felhasználó egy e-mailt küldhet a cikk tulajdonos(ok). Elem tulajdonos fontos, hogy a PowerShell gyűjteményelemek használt e-mail cím figyelése és problémák előállított válaszolni. Egy ezt a módszert hátránya, hogy csak a felhasználó és a tulajdonos legalább egyszer jelenik meg a kommunikációt, előfordulhat, hogy ugyanezt a kérdést válaszoljon hány alkalommal kell a tulajdonos.
* Megjegyzés: A cikk lap alján megjegyzés mező kitöltése.
  Ebbe a rendszerbe előnye, hogy más felhasználók láthatják a megjegyzések és a válaszok, ami csökkenti a szám, ahányszor bármely egyetlen kérdésre válaszolni kell.
  Elem tulajdonos erősen ajánlott, hogy kövesse a megjegyzésekkel minden elemhez.
Lásd: [biztosító visszajelzés keresztül a közösségi média és a megjegyzések](https://msdn.microsoft.com/en-us/powershell/gallery/psgallery/psgallery-SocialMediaFeedback) hogyan valósítható meg.

Visszajelzés zárójelentésben válaszolni tulajdonosok vannak értékeljük a Közösség által.
A jelentés a lehetőség segítségével szükség esetén további adatokat kér, adja meg a probléma megoldásához, vagy megállapítani, hogy egy frissítés kijavítja a hibát.

Ha nem megfelelő vagy a kommunikációs csatornát a megfigyelt viselkedés, a PowerShell-galériában jelentés visszaélés funkcióját használja a gyűjtemény rendszergazdák kapcsolódni.

## <a name="modules-versus-scripts"></a>Modulok és parancsfájlok

Egy parancsfájl megosztása más felhasználókkal nagy, és kapcsolatos problémák megoldását, hogy példát biztosít.
A probléma oka, hogy a parancsfájlok a PowerShell-galériában külön dokumentáció, példák és tesztek nélkül egyetlen fájl.

PowerShell-modul, amely lehetővé teszi több mappákról és fájlokról, hogy bekerüljenek a csomag mappa struktúrával rendelkezik.
A modul szerkezete lehetővé teszi, beleértve a többi elem látható ajánlott eljárásokat: parancsmag súgó, dokumentáció, példák és teszteket.
A nagy hátránya, hogy egy modul egy parancsfájlt kell kitett és használatos függvényében.
Egy modul létrehozásával kapcsolatos további információkért lásd: [Windows PowerShell-modul írása](http://go.microsoft.com/fwlink/?LinkId=144916).

Vannak olyan helyzetek, ahol egy parancsfájl jobb élményt nyújt a DSC-konfigurációk, különösen a felhasználót.
A DSC-konfigurációk esetén ajánlott eljárás az, ha a konfigurációs közzétesszük egy kísérő modul, amely tartalmazza a dokumentumok, példákat és tesztek parancsfájlként.
A parancsfájl tartalmazza a kísérő moduljának használatával. a RequiredModules = @(a modul neve).
Ez a módszer minden parancsfájl használható.

Önálló olyan parancsfájlok, amelyek a bevált gyakorlat valós értéket adjon meg más felhasználók számára.
Megadása egy parancsfájlt a PowerShell-galériában közzétételekor erősen ajánlott dokumentáció Megjegyzés-alapú és a hivatkozást a projekt helyre.

## <a name="provide-a-link-to-a-project-site"></a>Adjon meg egy hivatkozást a projekt hely

A projekt hely, ahol a közzétevők használhatják közvetlenül a felhasználók a PowerShell-galériában elemek.
Felhasználók által előnyben részesített elemeket, adja meg, mivel lehetővé teszi az elemek könnyebb kapcsolatos információkat.
Sok eleme van a PowerShell-galériában fejlesztett a Githubon, mások által biztosított dedikált webszolgáltatás rendelkező szervezetek számára.
Ezek mindegyikének lehet tekinteni a projekt hely.

Ha hozzáad egy hivatkozást a PSData szakasza a jegyzék ProjectURI belefoglalja az alábbiak szerint történik:

        # A URL to the main website for this project.
        ProjectUri = 'https://github.com/powershell/powershell'

Ha egy ProjectURI valósul meg, a PowerShell-galériában tartalmaz egy hivatkozást a projekt helyre a cikk lap bal oldalán.

## <a name="include-tests"></a>Tesztek tartalmazza

Többek között a nyílt forráskód teszteken fontos a felhasználók, megakadályozni, hogy mit, ellenőrizze, és bemutatja, hogyan működik, a kódot nyújtja őket. Azt is lehetővé teszi a felhasználóknak nem azok törés az eredeti funkciókat, ha módosíthatják a kódot a környezetükben elférjen biztosításához.

Erősen ajánlott, hogy tesztek írva a teszt úgy tervezték, kifejezetten a PowerShell Pester keretrendszer előnyeit.
Pester érhető el [GitHub](https://github.com/Pester/Pester), a [PowerShell-galériában](https://www.powershellgallery.com/packages/Pester/), és a Windows 10, Windows Server 2016-os, WMF 5.0 és WMF 5.1 érhető el.

A [Pester project webhely a Githubon](https://github.com/Pester/Pester) Pester tesztek írása gyakorlati tanácsok a kezdeti lépések a megfelelő dokumentációt tartalmaz.

A teszt érvényességének célok külön felhívjuk a [magas minőségi erőforrásmodul dokumentáció](https://github.com/PowerShell/DscResources/blob/master/HighQualityModuleGuidelines.md), 70 % egységgel tesztelése a kód érvényességének ajánlott.

## <a name="include-andor-link-to-license-terms"></a>Tartalmaznak és/vagy csatolja a licencfeltételeket

A PowerShell-galériában közzétett összes elemet kell megadnia a licencfeltételeket, illetve azokhoz kötődjön, a licenc szereplő által a [használati](https://www.powershellgallery.com/policies/Terms) "Rendellenesen A" alatt.
A legjobb módja a adja meg egy másik licenc-hoz a LicenseURI használatát PSData licenc mutató hivatkozás biztosítása.
Példa Manifest mezők ajánlott témakörben találja.

```powershell
PrivateData = @{
    PSData = @{

        # Tags applied to this module. These help with module discovery in online galleries.
        Tags = @('.net','acl','active-directory')

        # A URL to the license for this module.
        LicenseUri = 'http://www.apache.org/licenses/LICENSE-2.0'
```

## <a name="sign-your-code"></a>A kód aláírása

Kód aláírása biztosítja a felhasználók számára a legmagasabb szintű megbízhatóság ki tette közzé a cikk a, és, hogy a kód példányát vásárolnak pontosan a közzétevő kiadott.
A kódaláírás általában kapcsolatos további információkért lásd: [bemutatása kódaláíró](http://go.microsoft.com/fwlink/?LinkId=106296).
PowerShell érvényesítése kódaláíró két elsődleges megközelítés keresztül támogatja:

* Aláírási parancsfájlok
* Katalógus-aláíró modul

PowerShell fájlok aláírása nem egy jól bevált módszer annak biztosításához, hogy a kód végrehajtott egy megbízható forrás által létrehozott volt, és nem lett módosítva.
PowerShell-parancsfájlok aláírásáról részletek tárgyalja a [kapcsolatos aláírási](https://msdn.microsoft.com/en-us/powershell/reference/5.1/microsoft.powershell.core/about/about_signing) témakör.
Az Áttekintés egy aláírás sem lehet hozzáadni. PS1 fájlnevet, amely PowerShell ellenőrzi a parancsfájl betöltésekor.
PowerShell használatával is korlátozható a [végrehajtási házirend](https://msdn.microsoft.com/en-us/powershell/reference/5.1/microsoft.powershell.core/about/about_execution_policies) parancsmagok használata érdekében aláírt parancsfájlok.

Katalógus aláírási modult egy olyan szolgáltatás, 5.1 verzióban PowerShell hozzáadni.
Egy modul aláírásáról kapcsolatban lásd a [katalógus parancsmagok](https://msdn.microsoft.com/en-us/powershell/wmf/5.1/catalog-cmdlets) témakör.
Az Áttekintés katalógus aláíró végezhető el a katalógus fájlt készít, minden fájlhoz a modul kivonatoló értéket tartalmaz, és majd a fájl aláírása.
A PowerShellGet közzététele modul, az install-modul, a mentés-modul, és a frissítés-modul parancsmagokkal lesz érvényes biztosításához az aláírás ellenőrzéséhez, majd győződjön meg arról, hogy az egyes elemekhez tartozó kivonat értéke megegyezik a katalógusban.
A modul egy korábbi verziója telepítve van a rendszeren, ha a telepítés-modul megerősíti, hogy az új verzióhoz tartozó aláíró hatóság megegyezik-e a mi korábban telepítve lett.
Katalógus aláíró működik együtt, de ez nem helyettesíti a aláíró parancsfájlok. PowerShell nem felel meg a katalógus aláírások modul betöltése során.

## <a name="follow-semver-guidelines-for-versioning"></a>Kövesse a verziókövetés SemVer irányelveket

[SemVer](http://semver.org/) van egy nyilvános konvenciót ismerteti, hogyan lehet struktúra, és módosítsa a verzió változásainak könnyen intepretation engedélyezéséhez.
A cikk verzióját kell szerepelnie a jegyzék adatokat.

* A verzió meg kell felelnie, mint 3 numerikus blokkok elválasztott, mint 0.1.1 vagy 4.11.192
* Rendszertől kezdődően a "0" jelzi, hogy az elem még nincs készen áll a termelési, és az első szám csak kezdjen "0", ha ez az egyetlen számát
* Az első szám (1.9.9999 2.0.0) megváltoztatása jelzi a verziók közötti fő- és megtörje módosítása
* A második szám (1.01 1.02) módosításai jelzi a szolgáltatás szintű változtatások, például az új parancsmagok ad hozzá egy modul
* A harmadik szám módosításai jelző nem jelentős változásokat, például új paraméterek, a frissített minták vagy az új vizsgálat
* Verziók listázásakor PowerShell rendezze a verziók karakterláncként, így 1.01.0 kezeli a program nagyobb, mint 1.001.0

PowerShell során jött létre, megelőzően SemVer, ezért azt támogatást nyújt a SemVer, nem minden elemek kifejezetten:

* Előzetes karakterláncok nem támogatja a verziószámok. Ez akkor hasznos, ha a közzétevők kívánja biztosítanak egy új főverzió az előzetes verziót egy 1.0.0 megadása után. Ez a PowerShell-galériában és PowerShellGet parancsmagok egy későbbi kiadásban lesz támogatott.
* PowerShell és a PowerShell-galériában engedélyezése verzió karakterláncok 1, 2 és 4 szegmensek. Számos korai modult nem követte az irányelveket, és a termék a Microsoft kiadásai build adatai, a 4. a számok (például 5.1.14393.1066) letiltása. Ezek a különbségek versioning szempontból, figyelmen kívül hagyja.

## <a name="test-using-a-local-repository"></a>Tesztelése egy helyi tárház használatával

A PowerShell-galériában célja nem lehet célja a közzétételi folyamat teszteléséhez.
A legjobb módszer a PowerShell-galériában közzétételt a végpont technológia és a saját helyi tárházon.
Ezt megteheti a néhány módokon, például:

* Állítson be egy helyi PowerShell-galériában példány használatával a [PS saját gyűjtemény projekt](https://github.com/PowerShell/PSPrivateGallery) a Githubon. A kép projekt segítséget a PowerShell-galériában, amely befolyásolhatja, és használja a tesztek példányának beállításához.
* Állítson be egy [belső Nuget-tárház](https://blogs.msdn.microsoft.com/powershell/2014/05/20/setting-up-an-internal-powershellget-repository/). Ez több munkát beállításához szükséges, de még néhány követelményt, nevezetesen ellenőrzése az API-kulcs és a-e függőségek szerepelnek a cél közzétételekor érvényesíteni előnye.
* A vizsgálat "tárház" egy fájlmegosztás állíthatja be. Ez egyszerűen állíthat be, de mivel ez egy fájlmegosztást, a fent leírt ellenőrzések nem kerül sor. Egy lehetséges ebben az esetben előnye, hogy a fájlmegosztás nem ellenőrzi az (kötelező) API-kulcsot, így azonos kulcs üzembe helyezése a PowerShell-galériában közzétételére.

Ezek a megoldások a Register-PSRepository segítségével határozza meg az új "tárház", amely használja a - tárház tulajdonságban Publish-modul.

Egy kiegészítő kapcsolattartót teszt közzétételre vonatkozó: bármely teszi közzé a PowerShell-galériában elem nem törölhető a műveletek csapat, akik fog erősítse meg, hogy semmi sem függ a közzétenni kívánt elemek segítség nélkül.
Éppen ezért jelenleg nem támogatják a PowerShell-galériában tesztelési célként, és bármelyik közzétevőt, aki így kapcsolatba lép.

## <a name="recommended-workflow"></a>Ajánlott munkafolyamat

A legtöbb sikeres megközelítés a PowerShell-galériában közzétett cikkek találtunk, amelyeknek ez:

* A fejlesztési kezdeti egy egy nyílt forráskódú projekt helyet. A PowerShell csapat Github használja.
* Használja a felülvizsgálók visszajelzései és [Powershell parancsfájl Analyzer](https://aka.ms/psscriptanalyzer) lekérni a kódot a stabil állapot
* Dokumentáció, tartalmazza, így mások tudja, hogyan használja a munkahelyi
* Tesztelje a közzétételi művelet egy helyi tárházat.
* Egy állandó vagy alfa kiadási közzétételére a PowerShell-galériában, meggyőződött arról, hogy hivatkozást a projekt helyre és dokumentációja
* Visszajelzések és a kódba a projekt hely többször, majd stabil frissítések közzétételéhez a PowerShell-galériában
* Példák és Pester tesztek hozzáadása a projekthez, és a modul
* Döntse el, ha szeretné a kód aláírása, az elem
* Ha úgy érzi, hogy a projekt éles környezetben használatra kész, tegye közzé a 1.0.0 verzióra, amellyel a PowerShell-galériában
* Folytassa a visszajelzések és a kódot a felhasználói bevitel alapján többször
