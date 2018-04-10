---
ms.date: 06/12/2017
contributor: JKeithB
ms.topic: conceptual
keywords: gyűjtemény, a powershell, a parancsmag, a psgallery
title: psgallery_gettingstarted
ms.openlocfilehash: 599b148e141ba4205a7c774581e737a5d54bfae1
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="get-started-with-the-powershell-gallery"></a>Ismerkedjen meg a PowerShell-galériában

## <a name="what-is-the-powershell-gallery"></a>Mi az a PowerShell-galériában?

A PowerShell-galériában PowerShell tartalom központi tárháza.
Az oktatóanyagban található PowerShell-parancsokat és a kívánt állapot konfigurációs szolgáltatása (DSC) erőforrásokat tartalmazó hasznos PowerShell-modulok. PowerShell-parancsfájlok, amelyek PowerShell-munkafolyamatok, és amely szerkezeti feladatokhoz és tartalmazhat adja meg a műveleti sorrend a ezeket a feladatokat is tájékozódhat.
Ezek az elemek egy része felhasználók a Microsoft által készített, és más felhasználók által a PowerShell közösségi készített.

## <a name="requirements"></a>Követelmények

Elemek letöltése a PowerShell-galériából a rendszerre van szükség a [PowerShellGet](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409) modul. A PowerShellGet modul megtalálható a következők bármelyike lehet. Jelentkezzen be a PowerShell-galériából töltse le a cikkek nem kell.

-   [Windows 10](http://go.microsoft.com/fwlink/?LinkID=624830&clcid=0x409)
-   [A Windows Management Framework 5.0](http://go.microsoft.com/fwlink/?LinkId=398175)
-   [Az MSI telepítő (a PowerShell 3. és 4)](http://go.microsoft.com/fwlink/?LinkID=746217&clcid=0x409)

PowerShellGet is szükséges a [NuGet szolgáltató](http://go.microsoft.com/fwlink/?LinkId=722208) a PowerShell-galériában együttműködni. Automatikusan PowerShellGet első használata esetén a NuGet szolgáltató telepítéséhez, ha a NuGet-szolgáltató nem a következő helyek valamelyikén kell megadnia:

- `$env:ProgramFiles\PackageManagement\ProviderAssemblies`
- `$env:LOCALAPPDATA\PackageManagement\ProviderAssemblies`

Vagy futtassa `Install-PackageProvider -Name NuGet -Force` letöltését és telepítését a NuGet-szolgáltató automatizálásához.


Ha egy régebbi, mint a NuGet 2.8.5.201 verziójával rendelkezik, szüksége lesz hívása a következő PowerShell-parancsmagok telepítéséhez és a legújabb NuGet váltani.

1.  `Install-PackageProvider NuGet -MinimumVersion '2.8.5.201' -Force`
2.  `Import-PackageProvider NuGet -MinimumVersion '2.8.5.201' -Force`
3.  Törölje a régebbi verziójú NuGet a fenti telepítési helyét.

További információkért lásd: <http://oneget.org/> .


Megjegyzés: Végrehajtott módosítás csomagolási formátumban, miatt javasoljuk PowerShellGet és PackageManagement nemrég frissített elemeket telepíteni a legújabb verzióra frissíti. PowerShellGet megtalálható a Windows 10, amely meg többet is megtudhat [Itt](http://go.microsoft.com/fwlink/?LinkID=624830&clcid=0x409).
PowerShellGet, letöltheti a a Windows Management Framework (WMF) 5.0, részben [Itt](http://go.microsoft.com/fwlink/?LinkId=398175).

## <a name="discovering-items-from-the-powershell-gallery"></a>A PowerShell-galériából elemek felfedezése

Az elemek találhatók a PowerShell-galériában használatával a **keresési** ezen a webhelyen, vagy keresse meg a modulok és a parancsfájlok lap vezérlőelem. A PowerShell-galériából elemek futtatásával is találhatók a [keresés-modul](https://go.microsoft.com/fwlink/?LinkId=821658) és [keresés-parancsfájl](https://go.microsoft.com/fwlink/?LinkId=822322) elemtípus, attól függően, a parancsmagok `-Repository PSGallery`.

A gyűjteményből eredmények szűréséhez végezhető el a következő paraméterekkel [keresés-modul](https://go.microsoft.com/fwlink/?LinkId=821658) és [keresés-parancsfájl](https://go.microsoft.com/fwlink/?LinkId=822322)

- Név
- AllVersions
- MinimumVersion
- RequiredVersion
- Címke
- Magában foglalja
- DscResource
- RoleCapability
- Parancs
- Szűrő

Ha csak kíváncsiak vagyunk a katalógusban adott DSC-erőforrások felderítéséhez, futtathatja a [keresés-DscResource](https://go.microsoft.com/fwlink/?LinkId=517196) parancsmag.
[Keresés – DscResource](https://go.microsoft.com/fwlink/?LinkId=517196) adatait jeleníti meg a gyűjteményben található DSC-erőforrást. A DSC-erőforrások mindig érkeznek modul részeként, mert továbbra is szeretné futtatni [Install-modul](https://go.microsoft.com/fwlink/?LinkId=821663) ezen DSC-erőforrások telepítéséhez.

## <a name="learning-about-items-in-the-powershell-gallery"></a>A PowerShell-galériában elemeinek megismerése

Ha érdekli a cikk állapította meg, érdemes lehet további információ. Ehhez úgy, hogy az elem adott oldalon, a gyűjteményben. Adott oldalon, képes lesz látható az összes, a metaadatok feltöltése a cikkhez. Ezeket a metaadatokat egy elem az elem szerzői szolgáltatja, és nem ellenőrzi a Microsoft által. A tulajdonos elem a cikk közzétételéhez használt gyűjtemény fiók erősen kötődik, és több megbízható, mint az Author mező.

Ha úgy érzi, hogy egy elem nincs közzétéve jóhiszeműen, kattintson a **jelentés visszaélés** , hogy az elem oldalon.

Ha fut [keresés-modul](https://go.microsoft.com/fwlink/?LinkId=821658) vagy [keresés-parancsfájl](https://go.microsoft.com/fwlink/?LinkId=822322), a visszaadott PSGetModuleInfo objektumot meg tudja tekinteni ezeket az adatokat.
Ahhoz például, `Find-Module -Name PSReadLine -Repository PSGallery | Get-Member` adatait jeleníti meg a PSReadLine modul a gyűjteményben.

## <a name="downloading-items-from-the-powershell-gallery"></a>Elemek letöltése a PowerShell-galériából

Ha elemek letöltése a PowerShell-galériából javasoljuk a következő folyamat:

### <a name="inspect"></a>Vizsgálja meg

Egy elemet a gyűjteményből, a vizsgálathoz letöltéséhez futtassa vagy a [mentés-modul](https://go.microsoft.com/fwlink/?LinkId=821669) vagy [mentés-parancsfájl](https://go.microsoft.com/fwlink/?LinkId=822334) parancsmag, attól függően, hogy az elem típusa. Ez lehetővé teszi a helyileg menteni az elemet a telepítés nélküli, és vizsgálja meg a cikk tartalma. Ne felejtse el kézzel törölje a mentett elemet.

Ezek az elemek egy része felhasználók a Microsoft által készített, és más felhasználók által a PowerShell közösségi készített. A Microsoft azt javasolja, hogy tekintse át a tartalom és a kód elemeknek a telepítés előtti tár.

Ha úgy érzi, hogy egy elem nincs közzétéve jóhiszeműen, kattintson a **jelentés visszaélés** , hogy az elem oldalon.

### <a name="install"></a>Telepítés

Egy elem a katalógusból való használatra telepítéséhez futtassa vagy a [Install-modul](https://go.microsoft.com/fwlink/?LinkId=821663) vagy [telepítési-parancsfájl](https://go.microsoft.com/fwlink/?LinkId=822327) parancsmag, attól függően, hogy az elem típusa.

[Install-modul](https://go.microsoft.com/fwlink/?LinkId=821663) telepíti a modult `$env:ProgramFiles\WindowsPowerShell\Modules` alapértelmezés szerint. Ehhez szükséges, hogy rendszergazdai fiókkal. Ha ad hozzá a `-Scope
CurrentUser` paraméter, a modul telepítve van a `$env:USERPROFILE\Documents\WindowsPowerShell\Modules` .

[Install-parancsfájl](https://go.microsoft.com/fwlink/?LinkId=822327) telepíti a parancsfájlt, amellyel `$env:ProgramFiles\WindowsPowerShell\Scripts` alapértelmezés szerint. Ehhez szükséges, hogy rendszergazdai fiókkal. Ha ad hozzá a `-Scope
CurrentUser` paraméter, telepítve van a parancsfájl `$env:USERPROFILE\Documents\WindowsPowerShell\Scripts` .

Alapértelmezés szerint [Install-modul](https://go.microsoft.com/fwlink/?LinkId=821663) és [telepítési-parancsfájl](https://go.microsoft.com/fwlink/?LinkId=822327) elem legfrissebb verzióját telepíti. A cikk korábbi verziója telepítéséhez adja hozzá a `-RequiredVersion` paraméter.

### <a name="deploy"></a>telepítése Telepítse a

Azure Automation a PowerShell-galériából elemet telepítéséhez kattintson **központi telepítése az Azure Automation** elem részleteit megjelenítő oldalon. Az Azure felügyeleti portálra, ahol regisztrál Azure-fiók hitelesítő adataival irányítja. Vegye figyelembe, hogy függőségekkel rendelkező elemek telepítését helyezik üzembe a függőségek az Azure Automation. A "Központi telepítése az Azure Automation" gomb letiltható hozzáadásával a **AzureAutomationNotSupported** címkén belül, hogy a konfigurációelem-metaadatok.

Azure Automation kapcsolatos további tudnivalókért tekintse meg a [Azure Automation-webhely](http://azure.microsoft.com/services/automation/).

## <a name="updating-items-from-the-powershell-gallery"></a>A PowerShell-galériából elemek frissítése

A PowerShell-galériából telepített elemek frissítését, futtatása vagy a [frissítés-modul](https://go.microsoft.com/fwlink/?LinkID=398576) vagy [frissítés-parancsfájl](http://go.microsoft.com/fwlink/?LinkId=619787) parancsmag. További paraméterek, nélküli futása közben [frissítés-modul](https://go.microsoft.com/fwlink/?LinkID=398576) minden futtatásával telepített modulokban frissíteni próbálja [Install-modul](https://go.microsoft.com/fwlink/?LinkId=821663).
Modulok szelektív frissítéséhez vegye fel a `-Name` paraméter.

Ehhez hasonlóan futása közben további paraméter nélkül [frissítés-parancsfájl](http://go.microsoft.com/fwlink/?LinkId=619787) is frissíteni minden parancsfájl futtatásával telepíteni próbálja [telepítési-parancsfájl](https://go.microsoft.com/fwlink/?LinkId=822327).
Parancsfájlok szelektív frissítéséhez vegye fel a `-Name` paraméter.

## <a name="list-items-that-you-have-installed-from-the-powershell-gallery"></a>A PowerShell-galériából telepített listaelemek

Szeretné tudni, melyik modulokat a PowerShell-galériából telepítette, futtassa a [Get-InstalledModule](https://go.microsoft.com/fwlink/?LinkId=526863) parancsmag. Ez a parancs megjeleníti a modulok, a rendszeren, hogy közvetlenül a PowerShell-galériából telepített.

Hasonlóképpen, a PowerShell-galériából telepítése parancsfájlok tudni, futtassa a [Get-InstalledScript](https://go.microsoft.com/fwlink/?LinkId=619790) parancsmag. Ez a parancs felsorolja az összes parancsfájlját a rendszeren, hogy közvetlenül a PowerShell-galériából telepített.