---
ms.date: 06/09/2017
schema: 2.0.0
keywords: PowerShell
title: Jegyzékfájl értékek elem, amely hatással van a PowerShell-galéria felhasználói felülete
ms.openlocfilehash: 00350d3558e2bfa487fb116304956ffa7291ee05
ms.sourcegitcommit: 77f62a55cac8c13d69d51eef5fade18f71d66955
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/17/2018
ms.locfileid: "39093973"
---
# <a name="item-manifest-values-that-impact-the-powershell-gallery-ui"></a>Jegyzékfájl értékek elem, amely hatással van a PowerShell-galéria felhasználói felülete

Ez a témakör összefoglaló információkat közzétevőket módosítása a PowerShell-galériából kiadványok esetén használható a jegyzékfájlt, hogy a PowerShellGet-parancsmagok és a PowerShell-galéria felhasználói felülete funkciói hatással lesz a.
Ezt a tartalmat, a módosítás megjelenik, kezdődően a középen, majd a bal oldali navigációs felületén szerint vannak rendszerezve. Nincs a részletek szakasz fedi le a címkék, amely azonosítja a fontos címkék, valamint a gyakrabban gyakran használt címkéket.
Van két olyan témakörök, amelyek a jegyzékfájl példákat biztosítanak:

- Modulok, lásd: [frissítés modul Manifest](/powershell/module/powershellget/Update-ModuleManifest)
- Parancsfájlok, lásd: [metaadatokat tartalmazó parancsfájl létrehozása](/powershell/module/powershellget/New-ScriptFileInfo)

## <a name="powershell-gallery-feature-elements-controlled-by-the-manifest"></a>A jegyzékfájl által vezérelt PowerShell-galériából funkció elemek

Az alábbi táblázat a közzétevő által vezérelt a PowerShell-Galériabeli elem lap felhasználói felületi elemei.
Minden elem azt jelzi, ha, előfordulhat, hogy szabályozni a modul vagy a parancsfájl jegyzékfájlt.

| Felhasználói felületi elemben | Leírás | Modul | Parancsfájl |
| --- | --- | --- | --- |
| **Cím** | A katalógusban közzétett elem neve  | Nem | Nem |
| **Verzió** | A verzió jelenik meg a metaadatok verzió-karakterlánca, és egy előzetes if van megadva. Az a verzió egy moduljegyzék elsődleges része a ModuleVersion. A parancsprogramhoz azonosított. VERZIÓ. Ha egy kiadás előtti verzió-karakterlánccal van megadva, azt fogja hozzáfűzi a modulok ModuleVersion, vagy részeként megadott. Szkriptek verziója. Nincs előzetes karakterláncok megadásával dokumentációját [modulok](/powershell/gallery/concepts/module-prerelease-support), majd a [parancsfájlok](/powershell/gallery/concepts/script-prerelease-support) | Igen | Igen |
| **Leírás** | A leírás a moduljegyzékben, és a egy parancsfájl fájladatokat. LEÍRÁS | Igen | Igen |
| **Licencfeltételek elfogadásának megkövetelése** | Egy modul lehet szükség, ha a felhasználó egy licencet, fogadja el a moduljegyzékben módosításával a RequireLicenseAcceptance = $true, egy LicenseURI ellátására, és a egy license.txt fájlt, a modul mappába gyökere. További információkat a [licencfeltételek elfogadásának megkövetelése](/powershell/gallery/how-to/working-with-items/items-that-require-license-acceptance) témakör. | Igen | Nem |
| **Kibocsátási megjegyzések** | Modulok Ez az információ alapszanak ReleaseNotes szakaszban PSData\PrivateData alatt. Parancsfájl manifestech van a. RELEASENOTES eleme. | Igen | Igen |
| **Tulajdonosok** | A kiválasztott elem frissítésére felhatalmazott fiókadminisztrátorról a PowerShell-galériából a felhasználók olyan. A tulajdonos listában nem szerepel az elemek jegyzéke. További dokumentáció azt ismerteti, hogyan [konfigurációelem tulajdonosainak kezelése](/powershell/gallery/how-to/publishing-items/managing-item-owners). | Nem | Nem |
| **Szerző** | Ez az a moduljegyzékben szerzőként, és a egy parancsfájl-jegyzékfájlt, része. SZERZŐ. Az Author mező gyakran használják olyan cég vagy szervezet társított elem megadásához. | Igen | Igen |
| **A szerzői jog** | Ez az a szerzői jog mező a moduljegyzékben és. Szerzői jogi egy parancsfájl-jegyzékfájlban. | Igen | Igen |
| **FileList** | A fájlok listájának megjelenítése a csomag közzététele után a PowerShell-galériában. Már nem vezérelheti a jegyzékfájl információkat. Megjegyzés: az összes elemét a PowerShell-galériából, amely nem található a elem egy rendszer telepítését követően a felsorolt további .nuspec fájl van. Ez a cikk a Nuget csomag jegyzékfájlt, és figyelmen kívül hagyhatja. | Nem | Nem |
| **A címkék** | Modulok címkék szerinti PSData\PrivateData tartalmaznak. A parancsfájlok a szakaszban van címkézve. CÍMKÉK. Vegye figyelembe, hogy a címkék nem tartalmazhat szóközt, akkor is, ha idézőjelek között vannak. A címkék rendelkezik további követelmények és jelentését, amely a címke részletek szakaszban Ez a témakör későbbi része ismerteti. | Igen | Igen |
| **Parancsmagok** | Ez a modul jegyzéket CmdletsToExport megtalálható. Vegye figyelembe, hogy az ajánlott eljárás az explicit módon a listaelemek helyett a helyettesítő karakterek használatával "*", ahogy, amely javítja a terhelés-module teljesítményét a felhasználók számára. | Igen | Nem |
| **Függvények** | Ez a modul jegyzéket FunctionsToExport megtalálható. Vegye figyelembe, hogy az ajánlott eljárás az explicit módon a listaelemek helyett a helyettesítő karakterek használatával "*", ahogy, amely javítja a terhelés-module teljesítményét a felhasználók számára. | Igen | Nem |
| **DSC-erőforrások** | A PowerShell 5.0-s verzió vagy újabb használt modulok Ez a jegyzéket DscResourcesToExport megtalálható. Ha a modul PowerShell 4 használandó, a DSCResourcesToExport nem használandó, mert nem támogatott jegyzékfájl kulcs. (DSC nem volt elérhető előtt PowerShell 4.) | Igen | Nem |
| **Munkafolyamatok** | Munkafolyamatok a PowerShell-galériában közzétett parancsfájlok és munkafolyamatok azonosította (lásd: [Connect-AzureVM](https://www.powershellgallery.com/packages/Connect-AzureVM/1.0/Content/Connect-AzureVM.ps1) példaként) a kódban. A jegyzékfájl nem szabályozza ezt. | Nem | Nem |
| **Szerepköri funkciók** | Ez megjelenik, ha a modul a PowerShell-galériában közzétett tartalmaz egy vagy több szerepkör képesség (.psrc) fájl, JEA által használt. A JEA dokumentációjában talál további részleteket [szerepkörrel képességeket](https://docs.microsoft.com/en-us/powershell/jea/role-capabilities). | Igen | Nem |
| **PowerShell Editions** | Ez a szkript vagy a modul jegyzékfájl van megadva. Használható a PowerShell 5.0-s, és ez alatt modulok szabályozott címkék használatával. Az asztali PSEdition_Desktop címke, majd a core, a címke PSEdition_Core. Csak a PowerShell 5.1-es vagy újabb használt modulok nincs CompatiblePSEditions kulcsot a fő jegyzékfájlban. További részletekért tekintse át a PS-Edition szolgáltatása [a PowerShell Get-dokumentáció](/powershell/gallery/concepts/module-psedition-support). | Igen | Igen |
| **Függőségek** | A függőségek a modulokat a PowerShell-galériából, amely RequiredModules, vagy a modul, vagy, a parancsfájl jegyzékfájlban deklarált olyan #Requires – modul (név). | Igen | Igen |
| **Powershell minimális verziója** | Ennek segítségével is megadható egy moduljegyzék PowerShellVersion | Igen | Nem |
| **Korábbi verziók** | A korábbi verziók a frissítések, egy modulban, a PowerShell-galériából történő tükrözi. Egy elem verzióját el van rejtve a törlési funkció használatával, ha azt nem megjelennek a korábbi verziók, kivéve a konfigurációelem tulajdonosainak. | Nem | Nem |
| **Project-webhely** | A projekt hely a moduljegyzékben Privatedata\PSData szakaszában modulok biztosítunk egy ProjectURI megadásával. A parancsfájl jegyzékfájlban szabályozza azt megadásával. PROJECTURI. | Igen | Igen |
| **Licenc** | Egy licenc hivatkozást a moduljegyzékben Privatedata\PSData szakaszában modulok egy LicenseURI megadásával. A parancsfájl jegyzékfájlban szabályozza azt megadásával. LICENSEURI. Fontos megjegyezni, hogy ha a licenc nem áll rendelkezésre a LicenseURI keresztül, vagy belül egy modult, majd a használati feltételeket a PowerShell-galéria adja meg a használati feltételeket a cikkhez. Tekintse meg a részletes használati feltételeit. | Igen | Igen |

## <a name="editing-item-details"></a>Elem részleteinek szerkesztése

A PowerShell-galéria szerkesztése elemet oldalon lehetővé teszi a közzétevők kifejezetten megjelenített egy elem, számos módosítása:

- Title
- Leírás
- Összefoglalás
- Ikon URL-címe
- Projekt kezdőlap URL-címe
- Szerzők
- Szerzői jog
- Címkék
- Kibocsátási megjegyzések
- Licenc szükséges

Ez a módszer nem általánosan ajánlott, kivéve, ha szükséges, javítsa ki a modul egy régebbi verziója jelenik meg.
Felhasználók, akik a modul beszerzése jelenik meg a metaadatok nem egyezik, mi jelenjen meg a PowerShell-galériából, amely a cikkel kapcsolatos aggályokat vet fel.
Ez gyakran a konfigurációelem tulajdonosainak, a módosítás megerősítéséhez lépjen lekérdezések eredményez.
Erősen ajánlott, hogy ezt a módszert használja, amikor egy új verzió elem közzé kell tenni a módosításokat a.

## <a name="tag-details"></a>Címke részleteinek

A címkék olyan egyszerű karakterláncok fogyasztók használatával megkeresheti az elemeket.
A címkék olyan esetben a legértékesebb, használatukról következetesen között számos kapcsolódó elemekre is ugyanabban a témában találhatók. Használatával több változatban is azonos (például adatbázis-adatbázisok vagy a tesztelési és tesztelésre) szó általában biztosít kis benefit.
A címkék olyan kis-és karakterláncok egyszavas, és nem tartalmazhat üres. Ha úgy gondolja, hogy a felhasználók meg fogja keresni egy kifejezés, hozzáadása, amely a konfigurációelem leírását, és a keresési eredmények között található. Használja a Pascal kis-és nagybetűhasználatot, kötőjelet, aláhúzásjellel vagy ponttal, ha a jobb olvashatóság érdekében szeretne. Legyen a hosszú, az összetett és a szokatlan címkék létrehozása óvatos, mert azok gyakran hibásan.

Nincsenek címkék, fontos megjegyezni, a PowerShell-galéria és a PowerShellGet parancsmagok kezeli őket egyedileg. PSEdition_Desktop PSEdition_Core a konkrét példák és fenti.

A fentieknek megfelelően a címkéket a legtöbb értéket adjon meg, amelyek adott és használt következetesen sok elem között.
Kiadói keresi a legjobb címkék használata a legegyszerűbb megközelítés az keresése a PowerShell-galériából, a címkék használatát fontolgatja.
Ideális esetben számítunk, hogy hány elemet adott vissza, és a cikkleírások fog összhangba kerüljenek a kulcsszavakat használatát.

Referenciaként itt található néhány leggyakrabban használt címkék 12/14/2017.
Bizonyos esetekben vannak hasonló, de talán kevésbé ideális lehetőségek mellett a címke szerepel.
Ajánlott eljárás a javasolt címkét használják, amelyek kevesebb zaj eredményez, és jobb keresési eredmények a fogyasztók számára fontos.

| Előnyben részesített címke | Alternatívák és megjegyzések |
| --- | --- |
| Azure |  |
| DSC | Kevésbé kívánatosak DesiredStateConfiguration, túl hosszú |
| Erőforrás-kezelő | ARM feldolgozók csoportja leírására szolgál, és ne használja az Azure Resource Manager |
| DSCResourceKit |  |
| AZ SQL |  |
| AWS |  |
| DSCResource |  |
| Automatizálás |  |
| REST |  |
| ActiveDirectory | AD jelenleg nem használja önmagában  |
| SQL Server |  |
| DBA |  |
| Biztonság | Defense rendszer kevésbé pontos |
| Adatbázis | Kevésbé kívánatos (többes számú) adatbázisok |
| Fejlesztés és üzemeltetés |  |
| Windows |  |
| Build |  |
| Telepítés | Üzembe helyezése kevésbé gyakran használt |
| Felhő |  |
| A GIT |  |
| Teszt | Tesztelése kevésbé kívánatos |
| VersionControl | Verzió: kevésbé pontos, bár a gyakrabban használt  |
| Naplózás | Előnyben részesített műveletként naplózás használata |
| Napló | Egy dolog Log előnyben részesített használata |
| Tartalék |  |
| IaaS |  |
| Linux |  |
| IIS |  |
| AzureAutomation |  |
| Tárolás |  |
| GitHub |  |
| JSON-ban |  |
| Exchange |  |
| Hálózat | Hálózatkezelés hasonlóan, a kevésbé gyakran használt |
| SharePoint |  |
| Jelentés | Jelentési művelet, a jelentés egy dolog |
| A jelentés | A jelentés azért is lehet |
| A Rendszerfelügyeleti webszolgáltatások |  |
| Figyelés |  |
| VSTS-BEN |  |
| Excel |  |
| Google |  |
| Szín |  |
| DNS |  |
| Office 365 | Célszerű a helyesírás-ellenőrzés Office ki. Office 365 ritkább esetben használja, bár a rövidebb |
| Gitlab |  |
| Pester |  |
| Azure ad |  |
| HTML |  |
| Hyper-V | Hyper-v rendszer kevésbé gyakori címkeként |
| Konfiguráció |  |
| ChatOps |  |
| A PackageManagement |  |
| WMI |  |
| Tűzfal |  |
| Docker |  |
| Appveyor |  |
| AzureRm | Elsősorban az AzureRM-modulok használják |
| Zip |  |
| MSI |  |
| Mac |  |
| PoshBot |  |