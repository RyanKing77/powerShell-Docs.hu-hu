---
ms.date: 06/09/2017
schema: 2.0.0
keywords: PowerShell
title: Elem jegyzék értékek, amelyek hatással van a PowerShell-Galériabeli felhasználói felület
ms.openlocfilehash: 39522396b179c54b981e6292cddacec27b32506c
ms.sourcegitcommit: e9ad4d85fd7eb72fb5bc37f6ca3ae1282ae3c6d7
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/10/2018
ms.locfileid: "34048944"
---
# <a name="item-manifest-values-that-impact-the-powershell-gallery-ui"></a>Elem jegyzék értékek, amelyek hatással van a PowerShell-Galériabeli felhasználói felület

Ez a témakör összefoglaló információkat a közzétevők hogyan lehet módosítani a PowerShell-galériában kiadványokat jegyzékfájljának, hogy az érintett szolgáltatások PowerShellGet parancsmagok és a PowerShell-Galériabeli felhasználói felületén.
Ez a tartalom ahol a változás megjelenik, kezdve a középen, akkor az a bal oldali navigációs területen van rendezve. Nincs olyan részletei című szakaszban fedi le címkék azonosítja az fontos címkék, valamint a gyakrabban általánosan használt címkék.
Számos jegyzékszakaszban példákat biztosítanak két témakörök.

- A modulok, lásd: [frissítés modul Manifest](https://docs.microsoft.com/powershell/gallery/psget/module/psget_update-modulemanifest)
- Parancsfájlok, lásd: [metaadatokkal parancsfájl létrehozása](https://docs.microsoft.com/powershell/gallery/psget/script/psget_new-scriptfileinfo)

## <a name="powershell-gallery-feature-elements-controlled-by-the-manifest"></a>PowerShell-galériában szolgáltatás elemek szabályozzák a jegyzék

Az alábbi táblázat bemutatja a közzétevő által vezérelt a PowerShell-galériában elem lap felhasználói felületi elemei.
Minden elem azt jelzi, ha azt is kell vezérelnie a modul vagy parancsfájl jegyzékfájlt.

| Felhasználói felületi elem | Leírás | Modul | Parancsfájl |
| --- | --- | --- | --- |
| **Cím** | A cikk a katalógusban közzétett neve  | Nem | Nem |
| **Verzió** | A verzió jelenik meg a verzió-karakterlánca a metaadatok, és egy előzetes Ha meg van adva. Egy moduljegyzék a verzióját elsődleges része a ModuleVersion. Egy olyan parancsfájlt azonosított. VERZIÓ. Egy előzetes verziójának karakterlánc esetén, azt fogja a modulok ModuleVersion fűzött, vagy részeként megadott. Parancsprogramok verziója. Nincs előzetes tartalmazó karakterlánc megadása dokumentációja [modulok](https://docs.microsoft.com/en-us/powershell/gallery/psget/module/prereleasemodule), majd a [parancsfájlok](https://docs.microsoft.com/en-us/powershell/gallery/psget/script/prereleasescript) | Igen | Igen |
| **Leírás** | A moduljegyzékben leírás, és az egy parancsfájl fájladatokat is. LEÍRÁS | Igen | Igen |
| **Licenc elfogadására van szükség** | A modul lehet szükség, ha a felhasználó licenc, fogadja el a moduljegyzékben módosításával a RequireLicenseAcceptance = $true, egy LicenseURI biztosítja, és egy license.txt fájlt a modul mappa gyökeréhez. További információkat a [licenc elfogadása szükséges](https://docs.microsoft.com/en-us/powershell/gallery/psgallery/psgallery_requires_license_acceptance) témakör. | Igen | Nem |
| **Kibocsátási megjegyzések** | A modulok ezek az információk ReleaseNotes szakasz alatt PSData\PrivateData megrajzolása. Parancsfájl jegyzékfájlokban, hogy a rendszer a. RELEASENOTES elemet. | Igen | Igen |
| **Tulajdonos** | Tulajdonosok a PowerShell-galériában, aki frissítheti egy elemet a felhasználók listáját. A tulajdonos listában nem szerepel a cikk jegyzékfájlt. További dokumentációja ismerteti, hogyan [konfigurációelem tulajdonosainak kezelése](https://docs.microsoft.com/en-us/powershell/gallery/psgallery/managing-item-owners). | Nem | Nem |
| **Szerző** | Ez szerepel a moduljegyzékben a szerző, és egy parancsfájl jegyzékben. SZERZŐ. Adjon meg egy vállalat vagy szervezet egy elemhez tartozó gyakran szolgál az Author mező. | Igen | Igen |
| **Szerzői jog** | A szerzői jogi mező a moduljegyzékben és. COPYRIGHT egy parancsfájl jegyzékben. | Igen | Igen |
| **FileList** | A lista a csomagban található megrajzolása a PowerShell-galériában való közzétételekor. Nincs vezérelhető a jegyzék információkkal. Megjegyzés: az összes eleme, amely nem található a rendszeren a cikk telepítése után a PowerShell-galériában felsorolt további .nuspec fájl van. Ez a cikk a Nuget csomag jegyzékfájlt, és figyelmen kívül hagyja. | Nem | Nem |
| **Címkék** | A modulok a címkék PSData\PrivateData alatt jelennek meg. Parancsfájlok a szakasz címkével jelölt. CÍMKÉK. Vegye figyelembe, hogy címkéket nem tartalmazhat szóközt, akkor is, ha azok idézőjelben. Címkék további követelmények és jelentését, amely később a Tag részletei szakasz a jelen témakörben leírt rendelkezik. | Igen | Igen |
| **Parancsmagok** | Ez a modul jegyzéket CmdletsToExport találhatók. Vegye figyelembe, hogy a bevált gyakorlat az, hogy explicit módon a listaelemet, nem pedig a helyettesítő "*", mert a, amely javítani fogja a terhelés-modul a felhasználók számára. | Igen | Nem |
| **Funkciók** | Ez a modul jegyzéket FunctionsToExport találhatók. Vegye figyelembe, hogy a bevált gyakorlat az, hogy explicit módon a listaelemet, nem pedig a helyettesítő "*", mert a, amely javítani fogja a terhelés-modul a felhasználók számára. | Igen | Nem |
| **A DSC-erőforrások** | A PowerShell 5.0-s verzió vagy újabb használandó modulok Ez biztosítja a jegyzékfájlban DscResourcesToExport használatával. Ha a modul PowerShell 4 használni, a DSCResourcesToExport nem használandó, mert nincs olyan támogatott jegyzékének kulcsot. (DSC nem volt elérhető előtt PowerShell 4.) | Igen | Nem |
| **Munkafolyamatok** | Munkafolyamatok közzétett a PowerShell-galériában parancsfájlokat és munkafolyamatok azonosítottak (lásd: [Connect-AzureVM](https://www.powershellgallery.com/packages/Connect-AzureVM/1.0/Content/Connect-AzureVM.ps1) példát) a kódban. A jegyzékfájl nem szabályozza ezt. | Nem | Nem |
| **Szerepkör-képességek** | Ez megjelenik, ha a modul, a PowerShell-galériában közzétett tartalmaz egy vagy több szerepkör funkció (.psrc) fájlokat, amelyek JEA használják. A JEA dokumentációjában talál további részleteket [szerepkör képességek](https://docs.microsoft.com/en-us/powershell/jea/role-capabilities). | Igen | Nem |
| **PowerShell Editions** | Egy parancsfájl vagy modul jegyzékben megadott. A modulok használható PowerShell 5.0-s, és ez alatt szabályozott címkék használatával. Asztal a címke PSEdition_Desktop használják, de a core, a címke PSEdition_Core. Csak a PowerShell 5.1-es vagy újabb használandó modulok nincs egy CompatiblePSEditions kulcsot a fő jegyzékben. Részletesebben is tárgyaljuk, tekintse át a PS Edition szolgáltatásából [a PowerShell Get-dokumentáció](https://docs.microsoft.com/en-us/powershell/gallery/psget/module/modulewithpseditionsupport). | Igen | Igen |
| **Függőségek** | Függőségek használhatók a modulok a PowerShell-galériában RequiredModules vagy a modul, vagy, a parancsfájl jegyzékfájlban deklarált #Requires – modul (név). | Igen | Igen |
| **Powershell minimális verziója** | Ez lehet megadni egy moduljegyzék PowerShellVersion | Igen | Nem |
| **Verzióelőzmények** | A korábbi verziók által adott jelentéseket tükrözik a PowerShell-galériában modulra végrehajtott frissítések. Ha egy elem egy verziója van-e rejtve törlése funkcióval, azt nem jelenik meg a korábbi verziók kivéve elem tulajdonosai. | Nem | Nem |
| **Projekt hely** | A projekt hely egy ProjectURI megadásával a modulok a moduljegyzékben Privatedata\PSData szakaszában valósul meg. A parancsfájl jegyzékfájlban szabályozza azt adja meg. PROJECTURI. | Igen | Igen |
| **Licenc** | Licenc találhatóak a modulok a moduljegyzékben Privatedata\PSData szakaszában egy LicenseURI megadásával. A parancsfájl jegyzékfájlban szabályozza azt adja meg. LICENSEURI. Fontos megjegyezni, hogy ha a licenc nem áll rendelkezésre a LicenseURI keresztül, vagy belül egy modult, majd a használati feltételeket a PowerShell galéria adja meg a használati feltételeket a cikkhez. A használati feltételeket a részletekért tekintse meg. | Igen | Igen |

## <a name="editing-item-details"></a>Szerkesztési elem adatai

A PowerShell-tár szerkesztése elem lap lehetővé teszi, hogy a közzétevők kifejezetten egy elem megjelenített számos módosítása:

- Title
- Leírás
- Összefoglalás
- Ikon URL-címe
- Projekt kezdőlap URL-címe
- Szerzői alapfogalmak
- Szerzői jog
- Címkék
- Kibocsátási megjegyzések
- Licenchez

Ez a módszer nem általában javasolt, kivéve, ha a szükséges javítsa ki, milyen egy modul egy régebbi verziója nem jelenik meg.
Felhasználók, akik szereznek a modul jelenik meg a metaadatok nem felel meg a PowerShell-galériában, amely kiváltja a cikk kétségei meg.
Ez gyakran a cikk tulajdonosait, hogy a módosítás megerősítéséhez Ugrás lekérdezések eredményez.
Erősen ajánlott, hogy ezt a módszert használja, amikor a elem egy új verziója közzé kell tenni a ugyanazon módosításokat.

## <a name="tag-details"></a>Címke részletei

Címke található egyszerű karakterláncok fogyasztók használatával megkeresheti az elemeket.
Címke található a legértékesebb, használatukról egységesen ugyanazon a témakörhöz kapcsolódó elemek között. Több változatban is elkészíti a word (például adatbázis és adatbázis, vagy teszt- és tesztelése) általában használatának kevés juttatásra.
Címkék egyszavas nem betűérzékeny karakterláncok, és nem tartalmazhat üres értékeket. Ha úgy gondolja, hogy a felhasználók meg fogja keresni egy kifejezést, adja hozzá, amelyek a leírása és a keresési eredmények között található. Használja a Pascal kis-és nagybetűk, kötőjelet, aláhúzásjellel vagy ponttal, ha a kívánt olvashatóságának javítása érdekében. Legyen a hosszú összetett és szokatlan címkék létrehozása elővigyázatos, mivel azok gyakran lett beírva.

Nincs címkék fontos megjegyezni, hogy a PowerShell-galériában és PowerShellGet parancsmagok kezeli őket egyedi. PSEdition_Desktop PSEdition_Core az adott példák és fenti.

A fentieknek megfelelően a címkék a legtöbb értéket adjon meg, ha adott és használt következetesen elemek között.
Közzétevőként a legjobb címkék megkeresésére tett kísérlet használatára a legegyszerűbb megoldás, a PowerShell-galériában tervezi címkék kereséséhez.
Ideális esetben lesz, hogy hány elemet adott vissza, és a cikk leírások megfelelően igazodnak a kulcs szó használatára.

Összehasonlításul az alábbiakban néhány leggyakrabban használt címkék frissítésétől 12/14/2017.
Bizonyos esetekben nincsenek hasonló, de lehet, hogy kevesebb ideális beállítások mellett a címke szerepel.
Ajánlott eljárás az előnyben részesített címke használják, amelyek kevesebb zaj eredményez, és jobban találatok a fogyasztók számára is.


| **Előnyben részesített címke** | **Alternatívák és megjegyzések** |
| --- | --- |
| **Azure** |  |
| **DSC** | DesiredStateConfiguration kevésbé kívánatos, túl hosszú |
| **ResourceManager** | ARM processzorok csoport leírására használatos, és ne használja az Azure Resource Manager | **DSCResourceKit** |  |
| **SQL** |  |
| **AWS** |  |
| **DSCResource** |  |
| **Automatizálás** |  |
| **REST** |  |
| **ActiveDirectory** | AD jelenleg nincs használatban önmagában  |
| **SQLServer** |  |
| **DBA** |  |
| **Biztonság** | Védelmi kevésbé pontos. |
| **adatbázis** | Adatbázisok (többes számú) kevésbé kívánatos |
| **DevOps** |  |
| **Windows** |  |
| **Build** |  |
| **központi telepítés** | Telepítése kevésbé gyakran használt |
| **Felhő** |  |
| **GIT** |  |
| **Teszt** | Tesztelése kevésbé kívánatos |
| **VersionControl** | Verziója kevésbé pontos, bár a gyakrabban használt  |
| **Logging** | A naplózási művelet előnyben részesített használata |
| **Log** | Egy dolog napló előnyben részesített használni |
| **Biztonsági mentés** |  |
| **IaaS** |  |
| **Linux** |  |
| **IIS** |  |
| **AzureAutomation** |  |
| **Storage** |  |
| **GitHub** |  |
| **Json** |  |
| **Exchange** |  |
| **Hálózati** | Hálózatkezelés hasonló, a ritkábban használt |
| **SharePoint** |  |
| **Jelentéskészítés** | Jelentési művelet, a jelentés egy dolog |
| **A jelentés** | A jelentés egy dolog |
| **WinRM** |  |
| **Figyelés** |  |
| **VSTS** |  |
| **Excel** |  |
| **Google** |  |
| **Szín** |  |
| **DNS** |  |
| **Office365** | Célszerű a helyesírás Office ki. Office 365 ritkább esetben használja, bár rövidebb | **Gitlab** |  |
| **Pester** |  |
| **AzureAD** |  |
| **HTML** |  |
| **Hyper-V** | Hyper-v rendszer címkeként ritkább |
| **Konfiguráció** |  |
| **ChatOps** |  |
| **PackageManagement** |  |
| **WMI** |  |
| **Tűzfal** |  |
| **Docker** |  |
| **Appveyor** |  |
| **AzureRm** | Elsősorban az AzureRM modulok használható |
| **Zip** |  |
| **MSI** |  |
| **Mac** |  |
| **PoshBot** |  |