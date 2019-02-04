---
ms.date: 06/12/2017
contributor: JKeithB
keywords: katalógus, a powershell, a parancsmag, a psgallery
title: A PowerShell-galériából használatának első lépései
ms.openlocfilehash: c8beba3009e462ce52cdecd34fc0313d9234f289
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55688846"
---
# <a name="getting-started-with-the-powershell-gallery"></a>A PowerShell-galériából – első lépések

A PowerShell-galériából tárháza csomagot tartalmazó parancsfájlok, a modulok és a DSC-erőforrások letöltheti és használhatja. A parancsmagok használata a [PowerShellGet](/powershell/module/powershellget) modul a PowerShell-galériából csomagok telepítéséhez. Jelentkezzen be a PowerShell-galériából töltse le a cikkek nem kell.

> [!NOTE]
> Lehetséges, hogy közvetlenül a PowerShell-galériából töltse le a csomag, de ez nem ajánlott eljárás.
> További részletekért lásd: [manuális letöltés](/powershell/gallery/how-to/working-with-packages/manual-download).

## <a name="discovering-packages-from-the-powershell-gallery"></a>A PowerShell-galériából csomagok felderítése

Található csomagokat a PowerShell-galériából használatával a **keresési** vezérlőelem a PowerShell-galériából [kezdőlap](https://www.powershellgallery.com), vagy keresse a modulok és a parancsfájlokat a a [csomagok lapján ](https://www.powershellgallery.com/packages). A PowerShell-galériából csomagok futtatásával is talál a [Find-Module][], [Find-DscResource], és [Find-Script][] parancsmagok, a csomag típusától függően a `-Repository PSGallery`.

A katalógus eredményeit az alábbi paraméterek használatával szűrheti:

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

## <a name="learning-about-packages-in-the-powershell-gallery"></a>Tudnivalók a PowerShell-galériából-csomagok

Egy csomagot, amely az Önt érdeklő azonosítása, után érdemes többet szeretne megtudni róla. Ehhez megvizsgálja az adott oldalra a csomag a katalógusban. A oldalon láthatja az összes a metaadatokat a csomag feltöltése. Ezeket a metaadatokat a csomag szerzője által biztosított, és a Microsoft nem ellenőrzi. A csomag tulajdonosát erősen vannak kötve, a katalógus fiók tesz közzé a csomagot, és több megbízható-e, mint az Author mező.

Ha egy csomagot, amely úgy gondolja, hogy nincs közzétéve jóhiszeműen, kattintson a **visszaélés jelentése** a kérdéses csomag lapon.

Ha [Find-Module][] vagy [Find-Script][], a visszaadott PSGetModuleInfo objektumban is megtekintheti ezeket az adatokat. Ha például fut `Find-Module -Name PSReadLine -Repository PSGallery |Get-Member`
a katalógusban az PSReadLine modulban adatokat ad vissza.

## <a name="downloading-packages-from-the-powershell-gallery"></a>A PowerShell-galériából csomagok letöltése

A PowerShell-galériából való letöltése a csomagok esetén a következőket javasoljuk:

### <a name="inspect"></a>Vizsgálja meg

A csomag letöltéséhez vizsgálatra a katalógusból, futtathatja az alábbiak a [Save-Module][] vagy [Save-Script][] parancsmagot, a csomag típusától függően. Ez lehetővé teszi a csomag mentéséhez helyi telepítés nélküli, és vizsgálja meg a csomag tartalma. Ne felejtse el kézzel törölje a mentett csomagot.

Néhány ezeket a csomagokat a Microsoft által lett létrehozva, és mások vannak a PowerShell-Közösség által készített.
A Microsoft azt javasolja, hogy tekintse át a tartalmát és kódját a csomagok a katalógusban a telepítés előtt.

Ha egy csomagot, amely úgy gondolja, hogy nincs közzétéve jóhiszeműen, kattintson a **visszaélés jelentése** a kérdéses csomag lapon.

### <a name="install"></a>Telepítés

A csomag telepítéséhez használható a katalógusból, futtathatja az alábbiak a [Install-Module][] vagy [Install-Script][] parancsmagot, a csomag típusától függően.

[Install-Module][] telepíti a modult `$env:ProgramFiles\WindowsPowerShell\Modules` alapértelmezés szerint.
Ehhez rendszergazdai fiókkal. Ha a `-Scope CurrentUser` paramétert, telepítve van a modul `$env:USERPROFILE\Documents\WindowsPowerShell\Modules` .

[Install-Script][] a parancsfájl telepíti `$env:ProgramFiles\WindowsPowerShell\Scripts` alapértelmezés szerint.
Ehhez rendszergazdai fiókkal. Ha a `-Scope CurrentUser` paramétert, telepítve van a parancsfájl `$env:USERPROFILE\Documents\WindowsPowerShell\Scripts` .

Alapértelmezés szerint [Install-Module][] és [Install-Script][] telepíti egy csomagot a legújabb verzióját.
Egy régebbi verzióját a csomag telepítéséhez, adja hozzá a `-RequiredVersion` paraméter.

### <a name="deploy"></a>telepítése Telepítse a

Egy csomag az Azure Automation PowerShell-galériából történő üzembe helyezéséhez kattintson **Azure Automation**, majd kattintson a **üzembe helyezés az Azure Automation** csomag részleteit megjelenítő oldalon. Ekkor megnyílik az Azure felügyeleti portálon, ha bejelentkezik az Azure-fiók hitelesítő adataival. Vegye figyelembe, hogy függőségekkel rendelkező csomagok telepítése telepíti a függőségeket az Azure Automationhöz. Adja hozzá a "Üzembe helyezés az Azure Automation" gomb letiltható a **AzureAutomationNotSupported** a csomag metaadata címkét.

Azure Automation kapcsolatos további információkért tekintse meg a [Azure Automation](/azure/automation) dokumentációját.

## <a name="updating-packages-from-the-powershell-gallery"></a>A PowerShell-galériából csomagok frissítése

A PowerShell-galériából telepített csomagok frissítéséhez futtassa a [Update-modul] [-] vagy [frissítési parancsfájl] [] parancsmagot. Ha további paraméterek nélkül futtatja, [Update-modul] [-] futtatásával telepített összes modul frissíteni próbálja [Install-Module][]. Szelektív-modulok frissítése, adja hozzá a `-Name` paraméter. 

Ehhez hasonlóan további paraméterek nélkül futtatásakor [frissítési parancsfájl] [-] is frissíteni próbálja az összes parancsfájl futtatásával telepített [Install-Script][]. Külön-külön frissíteni a parancsfájlok, adja hozzá a `-Name` paraméter.

## <a name="list-packages-that-you-have-installed-from-the-powershell-gallery"></a>A PowerShell-galériából telepített csomagok

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
