---
ms.date: 06/12/2017
contributor: JKeithB
keywords: katalógus, a powershell, a parancsmag, a psgallery
title: A PowerShell-galériából használatának első lépései
ms.openlocfilehash: 39998df1a2bf9363dd008dc96a802157c8d691d7
ms.sourcegitcommit: e46b868f56f359909ff7c8230b1d1770935cce0e
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/13/2018
ms.locfileid: "45523053"
---
# <a name="get-started-with-the-powershell-gallery"></a>A PowerShell-galériából használatának első lépései

A megfelelő elemeket telepíthet a PowerShell-galériából módja a parancsmagok használata a [PowerShellGet](/powershell/module/powershellget) modul. Jelentkezzen be a PowerShell-galériából töltse le a cikkek nem kell.

> [!NOTE]
> Lehetséges, hogy közvetlenül a PowerShell-galériából töltse le a csomag, de ez nem ajánlott eljárás. További részletekért lásd: [manuális letöltés](https://msdn.microsoft.com/en-us/powershell/gallery/psgallery/how-to/working-with-items/manual-download.md).  


## <a name="discovering-items-from-the-powershell-gallery"></a>A PowerShell-galériából elemek felderítése...

Található elemek a PowerShell-galériából használatával a **keresési** vezérlőelem ezen a webhelyen, vagy a modulok és a parancsfájlok lapok tallózva. A PowerShell-galériából elemek futtatásával is találhatók a [Find-Module][] és [Find-Script][] parancsmagok, az elem típusa, attól függően `-Repository PSGallery`.

A katalógus eredményeinek szűrése hajtható végre a következő paraméterekkel:

- Név
- Allversions paramétert
- MinimumVersion
- RequiredVersion
- Címke
- Magában foglalja
- DscResource
- RoleCapability
- Parancs
- Szűrő

Ha érdekli csak a katalógus adott DSC-erőforrások felderítéséhez, akkor futtathatja a [Find-DscResource] parancsmagot. Find-DscResource DSC-erőforrások a katalógusban szereplő adatokat ad vissza.
DSC-erőforrások mindig érkezzenek a modul részét képező, mert továbbra is szeretné futtatni [Install-Module][] ezen DSC-erőforrások telepítéséhez.

## <a name="learning-about-items-in-the-powershell-gallery"></a>A PowerShell-galériából elemeinek megismerése

Egy elem érdekli azonosítása, után érdemes többet szeretne megtudni róla. Ehhez megvizsgálja az adott lapon adott elemet a katalógusban. A oldalon láthatja az összes elem a hardvertokenfájlok feltöltése a metaadatok. Ezeket a metaadatokat egy elem a cikk szerzője által biztosított, és a Microsoft nem ellenőrzi. A tulajdonos elem erősen vannak kötve, a katalógus fiók tesz közzé az elemet, és több megbízható-e, mint az Author mező.

Ha úgy gondolja, hogy egy elem nincs közzétéve jóhiszeműen, kattintson a **visszaélés jelentése** adott elemet oldalon.

Ha [Find-Module][] vagy [Find-Script][], a visszaadott PSGetModuleInfo objektumban is megtekintheti ezeket az adatokat. Ha például fut `Find-Module -Name PSReadLine -Repository PSGallery |Get-Member`
a katalógusban az PSReadLine modulban adatokat ad vissza.

## <a name="downloading-items-from-the-powershell-gallery"></a>PowerShell-galériából történő elemletöltés

Ha a PowerShell-galériából történő elemletöltés javasoljuk a következő folyamatot:

### <a name="inspect"></a>Vizsgálja meg

Egy elem a katalógusból vizsgálatra letöltéséhez futtathatja az alábbiak a [Save-Module][] vagy [Save-Script][] parancsmagot, a konfigurációelem típusától függően. Ez lehetővé teszi az elem mentése helyi telepítés nélküli, és vizsgálja meg az elem tartalma. Ne felejtse el kézzel törölje a mentett elemet.

Ezek az elemek egyes készült Microsoft és mások vannak a PowerShell-Közösség által készített.
A Microsoft azt javasolja, hogy tekintse át a tartalmát, és a telepítés előtt a katalógus elemeinek kódot.

Ha úgy gondolja, hogy egy elem nincs közzétéve jóhiszeműen, kattintson a **visszaélés jelentése** adott elemet oldalon.

### <a name="install"></a>Telepítés

Egy elem telepíteni a galériából való használatra, futtathatja az alábbiak a [Install-Module][] vagy [Install-Script][] parancsmagot, a konfigurációelem típusától függően.

[Install-Module][] telepíti a modult `$env:ProgramFiles\WindowsPowerShell\Modules` alapértelmezés szerint.
Ehhez rendszergazdai fiókkal. Ha a `-Scope CurrentUser` paramétert, telepítve van a modul `$env:USERPROFILE\Documents\WindowsPowerShell\Modules` .

[Install-Script][] a parancsfájl telepíti `$env:ProgramFiles\WindowsPowerShell\Scripts` alapértelmezés szerint.
Ehhez rendszergazdai fiókkal. Ha a `-Scope CurrentUser` paramétert, telepítve van a parancsfájl `$env:USERPROFILE\Documents\WindowsPowerShell\Scripts` .

Alapértelmezés szerint [Install-Module][] és [Install-Script][] telepíti egy elemet a legújabb verzióját.
A cikk egy régebbi verziója hozzáadásával a `-RequiredVersion` paraméter.

### <a name="deploy"></a>telepítése Telepítse a

Egy elemet az Azure Automation PowerShell-galériából történő üzembe helyezéséhez kattintson **üzembe helyezés az Azure Automation** elem részleteit megjelenítő oldalon. Átirányítjuk az Azure felügyeleti portálon, ha bejelentkezik az Azure-fiók hitelesítő adataival. Vegye figyelembe, hogy telepítése függőségekkel rendelkező elemek telepíti a függőségeket az Azure Automationhöz. Adja hozzá a "Üzembe helyezés az Azure Automation" gomb letiltható a **AzureAutomationNotSupported** a elemmetaadatok címkét.

Azure Automation kapcsolatos további információkért tekintse meg a [Azure Automation](/azure/automation) dokumentációját.

## <a name="updating-items-from-the-powershell-gallery"></a>A PowerShell-galériából elemek frissítése

A PowerShell-galériából származó elemek frissítéséhez futtassa a [Update-modul] [-] vagy [frissítési parancsfájl] [] parancsmagot. Ha további paraméterek nélkül futtatja, [Update-modul] [-] próbál meg minden egyes futtatásával telepített modulok frissítésére, [Install-Module][]. Szelektív-modulok frissítése, adja hozzá a `-Name` paraméter.

Ehhez hasonlóan ha további paraméterek nélkül futtatja, [frissítési parancsfájl] [-] is frissíteni próbálja minden parancsprogram futtatásával telepített [Install-Script][]. Külön-külön frissíteni a parancsfájlok, adja hozzá a `-Name` paraméter.

## <a name="list-items-that-you-have-installed-from-the-powershell-gallery"></a>A PowerShell-galériából telepített listaelemek

Ismerje meg, melyik modulokat a PowerShell-galériából telepítette, futtassa a [Get-InstalledModule][] parancsmagot. Ez a parancs felsorolja az összes van a rendszeren telepített, közvetlenül a PowerShell-galériából.

Hasonlóképpen, a PowerShell-galériából telepített parancsfájlok, futtassa a [Get-InstalledScript][] parancsmagot. Ez a parancs megjeleníti a parancsfájlokat a rendszeren telepített, közvetlenül a PowerShell-galériából.

[Find-DscResource]: /powershell/module/powershellget/Find-DscResource
[Find-Module]: /powershell/module/powershellget/Find-Module
[Find-Script]: /powershell/module/powershellget/Find-Script
[Get-InstalledModule]: /powershell/module/powershellget/Get-InstalledModule
[Get-InstalledScript]: /powershell/module/powershellget/Get-InstalledScript
[Install-Module]: /powershell/module/powershellget/Install-Module
[Install-Script]: /powershell/module/powershellget/Install-Script
[Publish-Module]: /powershell/module/powershellget/Publish-Module
[Publish-Script]: /powershell/module/powershellget/Publish-Script
[Register-PSRepository]: /powershell/module/powershellget/Register-Repository
[Save-Module]: /powershell/module/powershellget/Save-Module
[Save-Script]: /powershell/module/powershellget/Save-Script