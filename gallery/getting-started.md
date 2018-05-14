---
ms.date: 06/12/2017
contributor: JKeithB
ms.topic: conceptual
keywords: gyűjtemény, a powershell, a parancsmag, a psgallery
title: psgallery_gettingstarted
ms.openlocfilehash: c3aafe9e76eda9acdd4787f63dc0f8c71a20d02a
ms.sourcegitcommit: e9ad4d85fd7eb72fb5bc37f6ca3ae1282ae3c6d7
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/10/2018
---
# <a name="get-started-with-the-powershell-gallery"></a>Ismerkedjen meg a PowerShell-galériában

Elemek letöltése a PowerShell-galériából a rendszerre van szükség a [PowerShellGet](/powershell/module/powershellget) modul. A PowerShellGet modul megtalálható a következők bármelyike lehet. Jelentkezzen be a PowerShell-galériából töltse le a cikkek nem kell.

## <a name="discovering-items-from-the-powershell-gallery"></a>A PowerShell-galériából elemek felfedezése

Az elemek találhatók a PowerShell-galériában használatával a **keresési** ezen a webhelyen, vagy keresse meg a modulok és a parancsfájlok lap vezérlőelem. A PowerShell-galériából elemek futtatásával is találhatók a [keresés-modul][] és [keresés-parancsfájl][] elemtípus, attól függően, a parancsmagok `-Repository PSGallery`.

A gyűjteményből eredmények szűréséhez hajtható végre a következő paraméterekkel:

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

Ha csak kíváncsiak vagyunk a katalógusban adott DSC-erőforrások felderítéséhez, futtathatja a [keresés-DscResource] parancsmag. Keresés – DscResource a gyűjteményben található DSC erőforrást adatait jeleníti meg.
A DSC-erőforrások mindig érkeznek modul részeként, mert továbbra is szeretné futtatni [Install-modul][] ezen DSC-erőforrások telepítéséhez.

## <a name="learning-about-items-in-the-powershell-gallery"></a>A PowerShell-galériában elemeinek megismerése

Ha érdekli a cikk állapította meg, érdemes lehet további információ. Ehhez úgy, hogy az elem adott oldalon, a gyűjteményben. Adott oldalon, képes lesz látható az összes, a metaadatok feltöltése a cikkhez. Ezeket a metaadatokat egy elem az elem szerzői szolgáltatja, és nem ellenőrzi a Microsoft által. A tulajdonos elem a cikk közzétételéhez használt gyűjtemény fiók erősen kötődik, és több megbízható, mint az Author mező.

Ha úgy érzi, hogy egy elem nincs közzétéve jóhiszeműen, kattintson a **jelentés visszaélés** , hogy az elem oldalon.

Ha fut [keresés-modul][] vagy [keresés-parancsfájl][], a visszaadott PSGetModuleInfo objektumot meg tudja tekinteni ezeket az adatokat. Ahhoz például, `Find-Module -Name PSReadLine -Repository PSGallery |Get-Member` adatait jeleníti meg a PSReadLine modul a gyűjteményben.

## <a name="downloading-items-from-the-powershell-gallery"></a>Elemek letöltése a PowerShell-galériából

Ha elemek letöltése a PowerShell-galériából javasoljuk a következő folyamat:

### <a name="inspect"></a>Vizsgálja meg

Egy elemet a gyűjteményből, a vizsgálathoz letöltéséhez futtassa vagy a [mentés-modul][] vagy [mentés-parancsfájl][] parancsmag, attól függően, hogy az elem típusa. Ez lehetővé teszi a helyileg menteni az elemet a telepítés nélküli, és vizsgálja meg a cikk tartalma. Ne felejtse el kézzel törölje a mentett elemet.

Ezek az elemek egy része felhasználók a Microsoft által készített, és más felhasználók által a PowerShell közösségi készített.
A Microsoft azt javasolja, hogy tekintse át a tartalom és a kód elemeknek a telepítés előtti tár.

Ha úgy érzi, hogy egy elem nincs közzétéve jóhiszeműen, kattintson a **jelentés visszaélés** , hogy az elem oldalon.

### <a name="install"></a>Telepítés

Egy elem a katalógusból való használatra telepítéséhez futtassa vagy a [Install-modul][] vagy [telepítési-parancsfájl][] parancsmag, attól függően, hogy az elem típusa.

[Install-modul][] telepíti a modult `$env:ProgramFiles\WindowsPowerShell\Modules` alapértelmezés szerint.
Ehhez szükséges, hogy rendszergazdai fiókkal. Ha ad hozzá a `-Scope CurrentUser` paraméter, a modul telepítve van a `$env:USERPROFILE\Documents\WindowsPowerShell\Modules` .

[telepítési-parancsfájl][] telepíti a parancsfájlt, amellyel `$env:ProgramFiles\WindowsPowerShell\Scripts` alapértelmezés szerint.
Ehhez szükséges, hogy rendszergazdai fiókkal. Ha ad hozzá a `-Scope CurrentUser` paraméter, telepítve van a parancsfájl `$env:USERPROFILE\Documents\WindowsPowerShell\Scripts` .

Alapértelmezés szerint [Install-modul][] és [telepítési-parancsfájl][] elem legfrissebb verzióját telepíti.
A cikk korábbi verziója telepítéséhez adja hozzá a `-RequiredVersion` paraméter.

### <a name="deploy"></a>telepítése Telepítse a

Azure Automation a PowerShell-galériából elemet telepítéséhez kattintson **központi telepítése az Azure Automation** elem részleteit megjelenítő oldalon. Az Azure felügyeleti portálra, ahol regisztrál Azure-fiók hitelesítő adataival irányítja. Vegye figyelembe, hogy függőségekkel rendelkező elemek telepítését helyezik üzembe a függőségek az Azure Automation. A "Központi telepítése az Azure Automation" gomb letiltható hozzáadásával a **AzureAutomationNotSupported** címkén belül, hogy a konfigurációelem-metaadatok.

Azure Automation kapcsolatos további tudnivalókért tekintse meg a [Azure Automation](/azure/automation) dokumentációját.

## <a name="updating-items-from-the-powershell-gallery"></a>A PowerShell-galériából elemek frissítése

Elemek telepítve a PowerShell-galériából frissítéséhez futtassa a [frissítés-modul] [-] vagy az [Update-parancsfájl] [] parancsmag. További paraméterek nélküli futtatásakor [frissítés-modul] [-] minden egyes futtatásával telepített modulokban frissíteni próbálja [Install-modul][]. Modulok szelektív frissítéséhez vegye fel a `-Name` paraméter.

Hasonlóképpen, további paraméterek nélküli futtatásakor [parancsfájl-frissítés] [-] is frissíteni próbálja minden parancsfájl futtatásával telepítve [telepítési-parancsfájl][]. Parancsfájlok szelektív frissítéséhez vegye fel a `-Name` paraméter.

## <a name="list-items-that-you-have-installed-from-the-powershell-gallery"></a>A PowerShell-galériából telepített listaelemek

Szeretné tudni, melyik modulokat a PowerShell-galériából telepítette, futtassa a [Get-InstalledModule][] parancsmag. Ez a parancs megjeleníti a modulok, a rendszeren, hogy közvetlenül a PowerShell-galériából telepített.

Hasonlóképpen, a PowerShell-galériából telepítése parancsfájlok tudni, futtassa a [Get-InstalledScript][] parancsmag. Ez a parancs felsorolja az összes parancsfájlját a rendszeren, hogy közvetlenül a PowerShell-galériából telepített.

[keresés-DscResource]: /powershell/module/powershellget/Find-DscResource
[keresés-modul]: /powershell/module/powershellget/Find-Module
[keresés-parancsfájl]: /powershell/module/powershellget/Find-Script
[Get-InstalledModule]: /powershell/module/powershellget/Get-InstalledModule
[Get-InstalledScript]: /powershell/module/powershellget/Get-InstalledScript
[Install-modul]: /powershell/module/powershellget/Install-Module
[telepítési-parancsfájl]: /powershell/module/powershellget/Install-Script
[Publish-Module]: /powershell/module/powershellget/Publish-Module
[Publish-Script]: /powershell/module/powershellget/Publish-Script
[Register-PSRepository]: /powershell/module/powershellget/Register-Repository
[mentés-modul]: /powershell/module/powershellget/Save-Module
[mentés-parancsfájl]: /powershell/module/powershellget/Save-Script