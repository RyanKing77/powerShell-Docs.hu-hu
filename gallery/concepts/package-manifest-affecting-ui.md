---
ms.date: 06/09/2017
schema: 2.0.0
keywords: PowerShell
title: Jegyzékfájl értékek csomagot, amely hatással van a PowerShell-galéria felhasználói felülete
ms.openlocfilehash: cedf81df8de29c54ef559a800d654305029491ec
ms.sourcegitcommit: caac7d098a448232304c9d6728e7340ec7517a71
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/16/2019
ms.locfileid: "58058215"
---
# <a name="package-manifest-values-that-impact-the-powershell-gallery-ui"></a>Jegyzékfájl értékek csomagot, amely hatással van a PowerShell-galéria felhasználói felülete

Ez a témakör összefoglaló információkat közzétevőket módosítása a PowerShell-galériából kiadványok esetén használható a jegyzékfájlt, hogy a PowerShellGet-parancsmagok és a PowerShell-galéria felhasználói felülete funkciói hatással lesz a. Ezt a tartalmat, a módosítás megjelenik, kezdődően a középen, majd a bal oldali navigációs felületén szerint vannak rendszerezve. Nincs a részletek szakasz fedi le a címkék, amely azonosítja a fontos címkék, valamint a gyakrabban gyakran használt címkéket. Van két olyan témakörök, amelyek a jegyzékfájl példákat biztosítanak:

- Modulok, lásd: [frissítés modul Manifest](/powershell/module/powershellget/Update-ModuleManifest)
- Parancsfájlok, lásd: [metaadatokat tartalmazó parancsfájl létrehozása](/powershell/module/powershellget/New-ScriptFileInfo)

## <a name="powershell-gallery-feature-elements-controlled-by-the-manifest"></a>A jegyzékfájl által vezérelt PowerShell-galériából funkció elemek

Az alábbi táblázat a közzétevő által vezérelt a PowerShell-galériából csomag lap felhasználói felületi elemei. Minden elem azt jelzi, ha, előfordulhat, hogy szabályozni a modul vagy a parancsfájl jegyzékfájlt.

| Felhasználói felületi elemben | Leírás | Modul | Parancsfájl |
| --- | --- | --- | --- |
| **Cím** | A katalógusban közzétett csomag neve  | Nem | Nem |
| **Verzió** | A verzió jelenik meg a metaadatok verzió-karakterlánca, és egy előzetes if van megadva. Az a verzió egy moduljegyzék elsődleges része a ModuleVersion. A parancsprogramhoz azonosított. VERZIÓ. Ha egy kiadás előtti verzió-karakterlánccal van megadva, azt fogja hozzáfűzi a modulok ModuleVersion, vagy részeként megadott. Szkriptek verziója. Nincs előzetes karakterláncok megadásával dokumentációját [modulok](module-prerelease-support.md), majd a [parancsfájlok](script-prerelease-support.md) | Igen | Igen |
| **Leírás** | A leírás a moduljegyzékben, és a egy parancsfájl fájladatokat. LEÍRÁS | Igen | Igen |
| **Licencfeltételek elfogadásának megkövetelése** | Egy modul lehet szükség, ha a felhasználó egy licencet, fogadja el a moduljegyzékben módosításával a RequireLicenseAcceptance = $true, egy LicenseURI ellátására, és a egy license.txt fájlt, a modul mappába gyökere. További információkat a [licencfeltételek elfogadásának megkövetelése](../how-to/working-with-packages/packages-that-require-license-acceptance.md) témakör. | Igen | Nem |
| **Kibocsátási megjegyzések** | Modulok Ez az információ alapszanak ReleaseNotes szakaszban PSData\PrivateData alatt. Parancsfájl manifestech van a. RELEASENOTES eleme. | Igen | Igen |
| **Tulajdonosok** | Tulajdonosok a PowerShell-galériából, a csomag frissítésére felhatalmazott fiókadminisztrátorról felhasználóinak listája. A tulajdonos listában nem szerepel a csomagjegyzéket. További dokumentáció azt ismerteti, hogyan [konfigurációelem tulajdonosainak kezelése](../how-to/publishing-packages/managing-package-owners.md). | Nem | Nem |
| **Szerző** | Ez az a moduljegyzékben szerzőként, és a egy parancsfájl-jegyzékfájlt, része. SZERZŐ. Az Author mező gyakran használják, adjon meg egy vállalat vagy szervezet csomagokkal társított. | Igen | Igen |
| **Copyright** | Ez az a szerzői jog mező a moduljegyzékben és. Szerzői jogi egy parancsfájl-jegyzékfájlban. | Igen | Igen |
| **FileList** | A fájlok listájának megjelenítése a csomag közzététele után a PowerShell-galériában. Már nem vezérelheti a jegyzékfájl információkat. Megjegyzés: egy további .nuspec fájl szerepel a PowerShell-galériából, amely nem található a rendszeren a csomag telepítése után minden csomag-van. Ez a csomag a Nuget csomag jegyzékfájlt, és figyelmen kívül hagyhatja. | Nem | Nem |
| **Címkék** | Modulok címkék szerinti PSData\PrivateData tartalmaznak. A parancsfájlok a szakaszban van címkézve. CÍMKÉK. Vegye figyelembe, hogy a címkék nem tartalmazhat szóközt, akkor is, ha idézőjelek között vannak. A címkék rendelkezik további követelmények és jelentését, amely a címke részletek szakaszban Ez a témakör későbbi része ismerteti. | Igen | Igen |
| **Parancsmagok** | Ez a modul jegyzéket CmdletsToExport megtalálható. Vegye figyelembe, hogy az ajánlott eljárás az explicit módon a listaelemek helyett a helyettesítő karakterek használatával "*", ahogy, amely javítja a terhelés-module teljesítményét a felhasználók számára. | Igen | Nem |
| **Függvények** | Ez a modul jegyzéket FunctionsToExport megtalálható. Vegye figyelembe, hogy az ajánlott eljárás az explicit módon a listaelemek helyett a helyettesítő karakterek használatával "*", ahogy, amely javítja a terhelés-module teljesítményét a felhasználók számára. | Igen | Nem |
| **DSC-erőforrások** | A PowerShell 5.0-s verzió vagy újabb használt modulok Ez a jegyzéket DscResourcesToExport megtalálható. Ha a modul PowerShell 4 használandó, a DSCResourcesToExport nem használandó, mert nem támogatott jegyzékfájl kulcs. (DSC nem volt elérhető előtt PowerShell 4.) | Igen | Nem |
| **Munkafolyamatok** | Munkafolyamatok a PowerShell-galériában közzétett parancsfájlok és munkafolyamatok azonosította (lásd: [Connect-AzureVM](https://www.powershellgallery.com/packages/Connect-AzureVM/1.0/Content/Connect-AzureVM.ps1) példaként) a kódban. A jegyzékfájl nem szabályozza ezt. | Nem | Nem |
| **Szerepköri funkciók** | Ez megjelenik, ha a modul a PowerShell-galériában közzétett tartalmaz egy vagy több szerepkör képesség (.psrc) fájl, JEA által használt. A JEA dokumentációjában talál további részleteket [szerepkörrel képességeket](/powershell/jea/role-capabilities). | Igen | Nem |
| **PowerShell Editions** | Ez a szkript vagy a modul jegyzékfájl van megadva. Használható a PowerShell 5.0-s, és ez alatt modulok szabályozott címkék használatával. Az asztali PSEdition_Desktop címke, majd a core, a címke PSEdition_Core. Csak a PowerShell 5.1-es vagy újabb használt modulok nincs CompatiblePSEditions kulcsot a fő jegyzékfájlban. További részletekért tekintse át a PS-Edition szolgáltatása [a PowerShell Get-dokumentáció](module-psedition-support.md). | Igen | Igen |
| **Függőségek** | A függőségek a modulokat a PowerShell-galériából, amely RequiredModules, vagy a modul, vagy, a parancsfájl jegyzékfájlban deklarált olyan #Requires – modul (név). | Igen | Igen |
| **PowerShell minimális verziója** | Ennek segítségével is megadható egy moduljegyzék PowerShellVersion | Igen | Nem |
| **Korábbi verziók** | A korábbi verziók a frissítések, egy modulban, a PowerShell-galériából történő tükrözi. Ha egy csomag verziója rejtett a törlési funkció használatával, azt nem megjelennek a korábbi verziók, kivéve csomag tulajdonosai. | Nem | Nem |
| **Project Site** | A projekt hely a moduljegyzékben Privatedata\PSData szakaszában modulok biztosítunk egy ProjectURI megadásával. A parancsfájl jegyzékfájlban szabályozza azt megadásával. PROJECTURI. | Igen | Igen |
| **Licenc** | Egy licenc hivatkozást a moduljegyzékben Privatedata\PSData szakaszában modulok egy LicenseURI megadásával. A parancsfájl jegyzékfájlban szabályozza azt megadásával. LICENSEURI. Fontos megjegyezni, hogy ha a licenc nem áll rendelkezésre a LicenseURI keresztül, vagy belül egy modult, majd a használati feltételeket a PowerShell-galériából a adja meg a csomag a használati feltételeket. Tekintse meg a részletes használati feltételeit. | Igen | Igen |
| **Icon** | Egy ikont az IconURI jelzőt a parancsfájl-jegyzékfájlban, vagy a moduljegyzékben Privatedata-PSData szakaszában megadásával minden olyan csomag, a PowerShell-galériából a adható meg. Az IconURI egy 32 x 32 átláthatóság háttér-rendszerképet kell mutatnia. Az URI-t **kell** közvetlen kép URL-cím és **nem kell** keresse fel a képet, vagy annak egy fájljához a PowerShell-galériából csomagot tartalmazó webhelyet. | Igen | Igen |


## <a name="editing-package-details"></a>Csomag részleteinek szerkesztése

A PowerShell-galéria szerkesztése csomag lap lehetővé teszi, hogy a kiadók milyen mezőket jelenít meg a csomaghoz, kifejezetten számos módosítása:

- Title
- Leírás
- Összefoglalás
- Icon URL
- Projekt kezdőlap URL-címe
- Szerzők
- Szerzői jog
- Címkék
- Kibocsátási megjegyzések
- Licenc szükséges

Ez a módszer nem általánosan ajánlott, kivéve, ha szükséges, javítsa ki a modul egy régebbi verziója jelenik meg. Felhasználók, akik a modul beszerzése jelenik meg a metaadatok nem egyezik, mi jelenjen meg a PowerShell-galériából, amely a csomag aggályokat vet fel. Ez gyakran a csomag tulajdonosait, a módosítás megerősítéséhez lépjen lekérdezések eredményez. Erősen ajánlott, hogy ezt a módszert használja, amikor a csomag új verziójának közzé kell tenni a módosításokat a.

## <a name="tag-details"></a>Címke részleteinek

A címkék olyan egyszerű karakterláncok fogyasztók használatával megkeresheti az csomagokat. A címkék olyan esetben a legértékesebb, különböző ugyanahhoz a témakörhöz kapcsolódó csomagok száma folyamatosan használt. Használatával több változatban is azonos (például adatbázis-adatbázisok vagy a tesztelési és tesztelésre) szó általában biztosít kis benefit. A címkék olyan kis-és karakterláncok egyszavas, és nem tartalmazhat üres. Ha úgy gondolja, hogy a felhasználók meg fogja keresni egy kifejezés, hozzáadása, amely a csomag leírása, és a keresési eredmények között található. Használja a Pascal kis-és nagybetűhasználatot, kötőjelet, aláhúzásjellel vagy ponttal, ha a jobb olvashatóság érdekében szeretne.
Legyen a hosszú, az összetett és a szokatlan címkék létrehozása óvatos, mert azok gyakran hibásan.

Nincsenek címkék, fontos megjegyezni, a PowerShell-galéria és a PowerShellGet parancsmagok kezeli őket egyedileg. PSEdition_Desktop PSEdition_Core a konkrét példák és fenti.

A fentieknek megfelelően a címkéket a legtöbb értéket adjon meg, amelyek adott és használt következetesen csomagok száma között. Kiadói keresi a legjobb címkék használata a legegyszerűbb megközelítés az keresése a PowerShell-galériából, a címkék használatát fontolgatja. Ideális esetben számítunk, hogy a csomagok számát adja vissza, és a csomag leírása a kulcsszavakat használatára lesz igazodva.

Referenciaként itt található néhány leggyakrabban használt címkék 12/14/2017. Bizonyos esetekben vannak hasonló, de talán kevésbé ideális lehetőségek mellett a címke szerepel. Ajánlott eljárás a javasolt címkét használják, amelyek kevesebb zaj eredményez, és jobb keresési eredmények a fogyasztók számára fontos.

| Előnyben részesített címke | Alternatívák és megjegyzések |
| --- | --- |
| Azure |  |
| DSC | Kevésbé kívánatosak DesiredStateConfiguration, túl hosszú |
| ResourceManager | ARM feldolgozók csoportja leírására szolgál, és ne használja az Azure Resource Manager |
| DSCResourceKit |  |
| SQL |  |
| AWS |  |
| DSCResource |  |
| Automatizálás |  |
| REST |  |
| ActiveDirectory | AD jelenleg nem használja önmagában  |
| SQLServer |  |
| DBA |  |
| Biztonság | Defense rendszer kevésbé pontos |
| Adatbázis | Kevésbé kívánatos (többes számú) adatbázisok |
| DevOps |  |
| Windows |  |
| Felépítés |  |
| Telepítés | Üzembe helyezése kevésbé gyakran használt |
| Felhő |  |
| A GIT |  |
| Teszt | Tesztelése kevésbé kívánatos |
| VersionControl | Verzió: kevésbé pontos, bár a gyakrabban használt  |
| Naplózás | Előnyben részesített műveletként naplózás használata |
| Napló | Egy dolog Log előnyben részesített használata |
| Biztonsági mentés |  |
| IaaS |  |
| Linux |  |
| IIS |  |
| AzureAutomation |  |
| Tárolás |  |
| GitHub |  |
| Json |  |
| Exchange |  |
| Hálózat | Hálózatkezelés hasonlóan, a kevésbé gyakran használt |
| SharePoint |  |
| Jelentés | Jelentési művelet, a jelentés egy dolog |
| Jelentés | A jelentés azért is lehet |
| WinRM |  |
| Figyelés |  |
| VSTS |  |
| Excel |  |
| Google |  |
| Szín |  |
| DNS |  |
| Office365 | Célszerű a helyesírás-ellenőrzés Office ki. Office 365 ritkább esetben használja, bár a rövidebb |
| Gitlab |  |
| Pester |  |
| AzureAD |  |
| HTML |  |
| Hyper-V | Hyper-v rendszer kevésbé gyakori címkeként |
| Konfiguráció |  |
| ChatOps |  |
| PackageManagement |  |
| WMI |  |
| Tűzfal |  |
| Docker |  |
| Appveyor |  |
| AzureRm | Elsősorban az AzureRM-modulok használják |
| Zip |  |
| MSI |  |
| MacOS |  |
| PoshBot |  |
