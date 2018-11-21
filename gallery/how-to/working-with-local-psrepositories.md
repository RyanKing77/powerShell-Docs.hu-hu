---
ms.date: 11/06/2018
contributor: JKeithB
keywords: katalógus, powershell, a parancsmag, psgallery, psget
title: Helyi PSRepositories használata
ms.openlocfilehash: 94824ea584c097838b24c6f2cd02407b6147a781
ms.sourcegitcommit: 91786b03704fbd2d185f674df0bc67faddfb6288
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 11/14/2018
ms.locfileid: "51619258"
---
# <a name="working-with-local-powershellget-repositories"></a>A PowerShellGet helyi tárház használata

A PowerShellGet modul támogatási tárházak kívül a PowerShell-galériában.
Ezeket a parancsmagokat a következő forgatókönyvek megvalósítását teszik lehetővé:

- PowerShell-modulok megbízható, előre ellenőrzött készletét támogatja a környezetben való használatra
- PowerShell-modulok vagy parancsfájlok olyan CI/CD-folyamat tesztelése
- PowerShell-szkriptek és modulok továbbítására rendszerek nem férnek hozzá az internethez

Ez a cikk ismerteti, hogyan állítható be egy helyi PowerShell-tárház. A cikk emellett ismerteti a [OfflinePowerShellGetDeploy][] modulban elérhető PowerShell-galériából történő. Ez a modul tartalmazza a parancsmagok a PowerShellGet legújabb verziójának telepítéséhez a helyi tárházba.

## <a name="local-repository-types"></a>Helyi tárház típusa

Kétféleképpen hozhat létre egy helyi PSRepository: NuGet server vagy a fájlmegosztásnak. Minden típusának van előnyeit és hátrányait:

NuGet-kiszolgáló

| Előnyök| Hátrányok |
| --- | --- |
| PowerShell-Galériabeli funkció szorosan utánozza | Többrétegű alkalmazást szükséges műveletek tervezési és támogatás |
| NuGet integrálja a Visual Studiót, más eszközök | Hitelesítési modellre és a szükséges NuGet-fiókok kezelése |
| NuGet támogatja a metaadatok `.Nupkg` csomagok | A közzétételhez API-kulcs felügyelet és karbantartás |
| Itt a keresés, a felügyeleti csomag, stb. | |

Fájlmegosztás

| Előnyök| Hátrányok |
| --- | --- |
| Állítsa be, biztonsági mentése és kezelése egyszerűen | A PowerShellGet által használt metaadatok nem érhető el |
| Egyszerű biztonsági modell – felhasználói engedélyek a megosztáson | Alapszintű fájlmegosztás túli felhasználói felület |
| Cserélje le a meglévő elemeket, például a korlátozások nélkül | Korlátozott biztonságot és, aki frissíti, hogy mi nincs rögzítés |

A PowerShellGet működik, típusú és a verziója és a függőség telepítése megkeresése támogatja.
Azonban az egyes szolgáltatásai számára a PowerShell-galériából nem érhetők el alap NuGet-kiszolgálók vagy fájlmegosztásokat.

- Minden csomag egy - parancsfájlokat, a modulok, a DSC-erőforrások vagy a szerepkörrel képességeket különbséget tenni.
- Megosztás fájlkiszolgálók metaadatcsomagok, beleértve a címkék nem látható.

## <a name="creating-a-local-repository"></a>Helyi tárház létrehozására

A következő cikk a saját NuGet-kiszolgáló beállításának lépéseit sorolja fel.

- [NuGet.Server][]

Kövesse a lépéseket azon csomagok hozzáadása. A lépések a [egy csomag közzététele](#publishing-to-a-local-repository) terjed ki a cikk későbbi részében.

Egy fájl fájlmegosztás-alapú adattárat ügyeljen arra, hogy a felhasználók rendelkeznek-e engedélyekkel a fájlmegosztás eléréséhez.

## <a name="registering-a-local-repository"></a>A helyi tárház regisztrálása

Egy adattár használata előtt regisztrálnia kell azt használatával a `Register-PSRepository` parancsot.
Az alábbi példákban a **InstallationPolicy** értékre van állítva *megbízható*, feltételezve, hogy megbízható-e a saját tárház.

```powershell
# Register a NuGet-based server
Register-PSRepository -Name LocalPSRepo -SourceLocation http://MyLocalNuget/Api/V2/ -ScriptSourceLocation http://MyLocalNuget/Api/V2 -InstallationPolicy Trusted

# Register a file share on my local machine
Register-PSRepository -Name LocalPSRepo -SourceLocation '\\localhost\PSRepoLocal\' -ScriptSourceLocation '\\localhost\PSRepoLocal\' -InstallationPolicy Trusted
```

Jegyezze fel a különbség, hogy hogyan kezeli a a két parancs **ScriptSourceLocation**. Egy fájl fájlmegosztás-alapú tárházakhoz készült a **SourceLocation** és **ScriptSourceLocation** egyeznie kell. Egy webes tárház kell lenniük különböző, így ebben a példában egy záró "/" adnak hozzá a **SourceLocation**.

Ha azt szeretné, hogy az újonnan létrehozott PSRepository kell az alapértelmezett tárházban, akkor az összes többi PSRepositories kell regisztrációját. Például:

```powershell
Unregister-PSRepository -Name PSGallery
```

> [!NOTE]
> A tárház nevének "PSGallery" az a PowerShell-galériából használatra van fenntartva. PSGallery regisztrációját is, de nem használhat újra bármely más adattárból PSGallery nevét.

Ha a PSGallery visszaállítására van szüksége, futtassa a következő parancsot:

```powershell
Register-PSRepository -Default
```

## <a name="publishing-to-a-local-repository"></a>A helyi tárházban való közzététel

Miután regisztrálta a helyi PSRepository, akkor a helyi PSRepository tehetnek közzé. Két fő közzétételi forgatókönyv közül választhat: közzététele saját modult, és a modulnak a PSGallery a közzététele.

### <a name="publishing-a-module-you-authored"></a>Ön készített modul közzététele

Használat `Publish-Module` és `Publish-Script` a modul közzétételére a helyi PSRepository végezhet el, a PowerShell-galéria azonos módon.

- Adja meg a kód helyét
- Adja meg az API-kulcs
- Adja meg a tárház nevét. Például: `-PSRepository LocalPSRepo`

> [!NOTE]
> Hozzon létre egy fiókot a NuGet-kiszolgálón, majd jelentkezzen be létrehozni és menteni az API-kulcsot.
> Egy fájlmegosztás NuGetApiKey értékét minden nem lehet üres karakterlánc használható.

Példák:

```powershell
# Publish to a NuGet Server repository using my NuGetAPI key
Publish-Module -Path 'c:\projects\MyModule' -Repository LocalPsRepo -NuGetApiKey 'oy2bi4avlkjolp6bme6azdyssn6ps3iu7ib2qpiudrtbji'

# Publish to a file share repo - the NuGet API key must be a non-blank string
Publish-Module -Path 'c:\projects\MyModule' -Repository LocalPsRepo -NuGetApiKey 'AnyStringWillDo'
```

> [!IMPORTANT]
> Ahhoz, hogy a biztonsági, API-kulcsok nem lehet változtatható parancsfájlokban. A biztonságos rendszert kell használnia.

### <a name="publishing-a-module-from-the-psgallery"></a>A modul a PSGallery közzététele

A modul a PSGallery a helyi PSRepository való közzétételéhez használhatja a "Mentés-Package" parancsmagot.

- Adja meg a csomag nevét
- Adja meg a "NuGet" szolgáltatója
- Adja meg a PSGallery helyeként a forrás (https://www.powershellgallery.com/api/v2)
- Adja meg az elérési útját a helyi tárház

Példa:

```powershell
# Publish from the PSGallery to your local Repository
Save-Package -Name 'PackageName' -Provider Nuget -Source https://www.powershellgallery.com/api/v2 -Path '\\localhost\PSRepoLocal\'
```

Ha a helyi PSRepository webes, egy további lépést használó nuget.exe közzétételéhez szükséges.

A dokumentációt a [nuget.exe][].

## <a name="installing-powershellget-on-a-disconnected-system"></a>A PowerShellGet telepítése kapcsolat nélküli rendszerre

A PowerShellGet telepítése is nehézkes olyan környezetekben, amelyek az internetről leválasztását rendszerek igényelnek. A PowerShellGet rendelkezik egy rendszerindítási folyamatot, amely telepíti a legújabb verziót az első alkalommal használják. A PowerShell-galériából a OfflinePowerShellGetDeploy modul, amely támogatja a rendszerindítási folyamat-parancsmagokat kínál.

Elindíthat egy kapcsolat nélküli üzembe helyezés, kell tennie:

- Töltse le és telepítse a OfflinePowerShellGetDeploy az internethez csatlakozó system és a leválasztott rendszerek
- A PowerShellGet és annak függőségeit, az internethez csatlakozó system használatával töltse le a `Save-PowerShellGetForOffline` parancsmag
- A leválasztott rendszerhez az internethez csatlakoztatott rendszer PowerShellGet és annak függőségeit másolása
- Használja a `Install-PowerShellGetOffline` a PowerShellGet és annak függőségeit helyezze a megfelelő mappákat a leválasztott rendszeren

A következő parancsokat használja `Save-PowerShellGetForOffline` üzembe helyezhető egy mappa összes összetevő `f:\OfflinePowerShellGet`

```powershell
# Requires -RunAsAdministrator
#Download the OfflinePowerShellGetDeploy to a location that can be accessed
# by both the connected and disconnected systems.
Save-Module -Name OfflinePowerShellGetDeploy -Path 'F:\' -Repository PSGallery
Import-Module F:\OfflinePowerShellGetDeploy

# Put PowerShellGet somewhere locally
Save-PowerShellGetForOffline -LocalFolder 'F:\OfflinePowerShellGet'
```

Ezen a ponton, végezze el a tartalmát `F:\OfflinePowerShellGet` kapcsolat nélküli rendszerekhez érhető el. Futtassa a `Install-PowerShellGetOffline` parancsmagot, hogy a kapcsolat nélküli rendszeren a PowerShellGet telepítése.

> [!NOTE]
> Fontos, hogy nem futtatja a PowerShellGet a PowerShell-munkamenetben, ezek a parancsok futtatása előtt. A PowerShellGet abba a munkamenetbe betöltése után az összetevőket nem lehet frissíteni. Ha a PowerShellGet véletlenül elindítani, akkor lépjen ki, és indítsa újra a PowerShell.

```powershell
Import-Module F:\OfflinePowerShellGetDeploy

Install-PowerShellGetOffline -LocalFolder 'F:\OfflinePowerShellGet'
```

A parancsok futtatása után készen áll a helyi tárházra a PowerShellGet közzététele.

```powershell
# Publish to a NuGet Server repository using my NuGetAPI key
Publish-Module -Path 'F:\OfflinePowershellGet' -Repository LocalPsRepo -NuGetApiKey 'oy2bi4avlkjolp6bme6azdyssn6ps3iu7ib2qpiudrtbji'

# Publish to a file share repo - the NuGet API key must be a non-blank string
Publish-Module -Path 'F:\OfflinePowerShellGet' -Repository LocalPsRepo -NuGetApiKey 'AnyStringWillDo'
```

> [!IMPORTANT]
> Ahhoz, hogy a biztonsági, API-kulcsok nem lehet változtatható parancsfájlokban. A biztonságos rendszert kell használnia.

<!-- external links -->
[OfflinePowerShellGetDeploy]: https://www.powershellgallery.com/packages/OfflinePowerShellGetDeploy/0.1.1
[Nuget.Server]: /nuget/hosting-packages/nuget-server
[nuget.exe]: /nuget/tools/nuget-exe-cli-reference
