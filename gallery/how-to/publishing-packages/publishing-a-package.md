---
ms.date: 06/12/2017
contributor: JKeithB
keywords: katalógus, a powershell, a parancsmag, a psgallery
title: Létrehozása és közzététele egy elem
ms.openlocfilehash: 70696535a3bf540ff75a2dc43bca80cb1adf8f45
ms.sourcegitcommit: 9df29dfc637191b62ca591893c251c1e02d4eb4c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 01/04/2019
ms.locfileid: "54012534"
---
# <a name="creating-and-publishing-an-item"></a>Létrehozása és közzététele egy elem

A PowerShell-galériából az a hely közzététele és stabil PowerShell-modulok, a parancsfájlokat és a DSC-erőforrások megosztása a szélesebb körű PowerShell felhasználói Közösség.

Ez a cikk ismerteti a mechanics és a egy parancsfájl vagy a modul előkészítése és közzétételével az a PowerShell-galériából, fontos lépéseket. Azt javasoljuk, hogy tekintse át a [a közzététellel kapcsolatos irányelvek](../../concepts/publishing-guidelines.md) győződjön meg arról, hogy a közzétett elemeket is szélesebb körben elfogad, PowerShell-galériából felhasználók megismerése.

A cikk közzétételéhez a PowerShell-galériából minimális követelmények a következők:

- Egy PowerShell-Galériabeli fiók rendelkezik, és az API-kulcs társítva
- Az elem szükséges metaadatok ellenőrzéséhez
- Az előzetes érvényesítési eszközök segítségével győződjön meg arról, az elem közzétételre kész
- A cikk közzétételéhez a PowerShell-galériából, a Publish-Module és Publish-Script-parancsok használatával
- Reagálás a kérdése vagy aggodalma van az elemmel kapcsolatos

A PowerShell-galériából a PowerShell-modulok és a PowerShell-parancsfájlok fogad el. Parancsfájlok nevezzük, amikor egy PowerShell-parancsprogram, amely egy egyetlen fájlt, és nem egy nagyobb modul részét értjük.

## <a name="powershell-gallery-account-and-api-key"></a>PowerShell-Galériabeli fiók és API-kulcs

Lásd: [létrehozása egy PowerShell-galéria fiók](/powershell/gallery/how-to/publishing-packages/creating-an-account) beállítása a PowerShell-Galériabeli fiók számára.

Miután létrehozott egy fiókot, egy elem közzététele szükséges API-kulcs kérheti le. A fiókkal jelentkezik be, miután a felhasználónév regisztrálása helyett a PowerShell-galériából lapok tetején jelennek meg. Kattintson a felhasználónevére vesz igénybe, a saját fiók oldalra, ahol megtalálja az API-kulcsot.

Megjegyzés: Az API-kulcsot kell kezelni, így a felhasználónevét és jelszavát.
Ezzel a kulccsal, vagy bármely más, frissítheti bármelyik a saját a PowerShell-galériából.
Javasoljuk, hogy rendszeresen, a kulcs, amely végezhető frissítse a saját fiókoldal alaphelyzetbe kulcs használatával.

## <a name="required-metadata-for-items-published-to-the-powershell-gallery"></a>A PowerShell-galériában közzétett cikkekhez szükséges metaadatokat

A PowerShell-galériából származó metaadatokat tartalmazó mezőket a parancsfájl vagy a modul jegyzékfájlban szereplő gyűjtemény felhasználók információkat biztosít. Létrehozása vagy módosítása a PowerShell-galériában kiadvány elemek van egy kis készletét a cikk jegyzékfájlban megadott információk követelményei.
Azt javasoljuk, hogy az elemek metaadatokat tartalmazó szakasz, tekintse át a [a közzététellel kapcsolatos irányelvek](../../concepts/publishing-guidelines.md) megtudhatja, hogyan lehet a legjobb információt nyújt a felhasználók számára az elemek.

A [New-ModuleManifest](/powershell/module/microsoft.powershell.core/new-modulemanifest) és [New-ScriptFileInfo](/powershell/module/PowerShellGet/New-ScriptFileInfo) parancsmagok a jegyzékfájl sablon hozza létre, a helyőrzőket a jegyzékfájl elemek.

Mindkét jegyzékek fontos közzétételéhez, az elsődleges kulcs adatokat és PSData területére PrivateData két szakaszra van. Elsődleges kulcs egy PowerShell moduljegyzék adatai mindent kívül a PrivateData szakaszban. Elsődleges kulcsok halmaza vannak kötve, a PowerShell verzióját használja, és nincs definiálva nem támogatottak. PrivateData hozzáadását az új kulcsok, így az elemeket a PowerShell-galériából a PSData támogatja.


A PowerShell-galériában közzétett elem kitöltése legfontosabb jegyzékfájl elemek a következők:

- Parancsfájl vagy a modul neve – azokat a paraméterkészletben található állítják a. Egy parancsfájl PS1 vagy a. Egy modul psd1 kiterjesztésű.
- Verzió - formátum SemVer irányelveket kell követniük, mert elsődleges kulcs szükséges. Részletekért lásd: ajánlott eljárások.
- Szerző – ez szükséges elsődleges kulccsal, és az elem társítani kell a nevét tartalmazza.
Szerzők és a tulajdonosok az alábbi témakörben talál.
- Leírás – Ez az elsődleges kulcs kötelező, segítségével röviden elmagyarázza, Mire jó ez az elem és az azt használó
- ProjectURI – a mező értéke egy erősen ajánlott URI, amely egy hivatkozást kínál a Github-tárházba PSData vagy hasonló helyre, ahol mégis fejlesztését az elem
- Címkék - a csomag alapján a kompatibilis psedition paraméterrel és platformok címkézése erős javaslatot. További információkért lásd: a [a közzététellel kapcsolatos irányelvek](../../concepts/publishing-guidelines.md#tag-your-package-with-the-compatible-pseditions-and-platforms).

Szerzők és a PowerShell-galériából tulajdonosok elemek kapcsolódó fogalmak, de nem mindig egyezik. Konfigurációelem tulajdonosainak engedélye az elem kezelése PowerShell-galéria-fiókkal rendelkező felhasználók. Előfordulhat, hogy minden elem frissítésére felhatalmazott fiókadminisztrátorról sok tulajdonos. A tulajdonos csak akkor érhető el a PowerShell-galériából, és megszakad, ha a cikk egy rendszer lesz átmásolva a másikra. Szerző: beépített az alkalmazásjegyzék adatokat, így az mindig az elem részét karakterlánc. A Microsoft-termékek elemek kapcsolatos ajánlások a következők:

- Több tulajdonosok, legalább egy, a csapatot, amely a konfigurációelem neve alatt van
- A szerző kell egy jól ismert csoport neve (például az Azure SDK csapata), vagy a Microsoft Corporation


## <a name="pre-validate-your-item"></a>A cikk előre ellenőrzése

Van néhány, a PowerShell-galériából, az elem közzététele előtt a kód futtatásához szükséges eszközöket:

- [PowerShell parancsfájl Analyzer](https://www.powershellgallery.com/packages/PSScriptAnalyzer/), amely szerepel a PowerShell-galéria
- A Test-ModuleManifest, amely része a PowerShell-modulok
- A parancsfájlok, ez a PowerShell Get teszt ScriptFileInfo

[PowerShell parancsfájl Analyzer](https://www.powershellgallery.com/packages/PSScriptAnalyzer/) egy statikus elemző eszköz, amely megvizsgálja, hogy a kód kódolási irányelvek basic PowerShell megfelel-e. Ez az eszköz azonosítja a kódban a gyakori és a kritikus problémák, és rendszeresen segítséget nyújtanak a cikk közzététele készen álljon a fejlesztés során kell futtatni. PowerShell parancsfájl Analyzer hibáit, azonosított hibák, figyelmeztetés és információkat nyújt. Hibákat kell foglalkozni, a PowerShell-galériából való közzététel előtt. Figyelmeztetések kell vizsgálni, és a legtöbb beavatkozást igényel. PowerShell parancsfájl Analyzer futtatása minden alkalommal, amikor elem közzétett vagy a PowerShell-galériából frissíteni. A katalógus műveletek csapata kapcsolatba lép a konfigurációelem tulajdonosainak kapcsolatos hibák megoldásához található.

A jegyzékfájl információkat az elem nem lehet olvasni a PowerShell-galériából infrastruktúra által, ha nem tudja közzétenni.
[Test-ModuleManifest](/powershell/module/microsoft.powershell.core/test-modulemanifest) fogja a tényleges előforduló problémákat okozhat a modul nem lesz használható, ha telepítve van. Minden modul, a PowerShell-galériából történő közzététele előtt kell futtatni.

Hasonlóképpen [Test-ScriptFileInfo](/powershell/module/PowerShellGet/test-scriptfileinfo) érvényesíti a metaadatokat egy parancsfájlban, és minden parancsfájlt (modul közzétett webszolgáltatáson), a Powershell-galériából történő közzététele előtt kell futtatni.


## <a name="publishing-items"></a>Közzétételi elemek

Kell használnia a [Publish-Script](/powershell/module/PowerShellGet/publish-script) vagy [Publish-Module](/powershell/module/PowerShellGet/publish-module) elemek közzététele a PowerShell-galériában. Ezek a parancsok mindkét van szükség:

- Teszi közzé az elem elérési útja. Egy modul használja a mappát, a modul neve. Ha megad egy mappát, amely ugyanazon modul több verzióját tartalmazza, RequiredVersion kell megadnia.
- A Nuget-API-kulcs. Ez az API-kulcsot a My Account oldal a PowerShell-galériában található.

Így nem kell megadnia őket a parancsban az alkalmazásjegyzék adatokat tesz közzé, az elem a többi beállítást, a parancssorban a legtöbb legyen.

Hibák elkerülése érdekében, erősen ajánlott, hogy a parancsok használata a – Whatif megpróbál-Verbose, a közzététel előtt. Ez menti jelentős időt, mivel minden alkalommal, amikor közzéteszi a PowerShell-galériából, a verziószámot a manifest szakasz elem frissítenie kell.

Példák a következő lesz:

* `Publish-Module -Path ".\MyModule" -NugetAPIKey "GUID" -Whatif -Verbose`
* `Publish-Script -Path ".\MyScriptFile.PS1" -NugetAPIKey "GUID" -Whatif -Verbose`

Gondosan tekintse át a kimenetet, és ha nincsenek hibák vagy figyelmeztetések látja, ismételje meg a parancsot,-Whatif nélkül.

Minden elem, a PowerShell-galériában közzétett vírusok esetén sor fog kerülni, és a PowerShell-parancsfájl Analyzer segítségével elemzik. Minden olyan problémák merülnek fel, hogy küld vissza a közzétevő a feloldásához.

A PowerShell-galériában egy cikk közzététele után kell tekintse meg az elemet a visszajelzés.

- Győződjön meg, hogy a közzétételéhez használt fiókhoz tartozó e-mail cím figyelheti. A felhasználók és a PowerShell-galéria üzemeltetési csapat fogja visszajelzést felmerülő problémák megoldásáról a PSSA vagy víruskereső vizsgálatok fiókon keresztül. Ha az e-mail-fiók érvénytelen, vagy ha a fiók és a hosszú ideig feloldatlan balra jelentett súlyos problémákat, elemek elhagyott és törlődik a PowerShell-galériából leírtak szerint lehessen venni a [használati](https://www.powershellgallery.com/policies/Terms).
- Azt javasoljuk, hogy minden egyes közzétett PowerShell Katalóguselem megjegyzések előfizetni. Ez lehetővé teszi, hogy értesítést kapjon, ha bárki észrevételeit az elemek, a PowerShell-galériában. Ez nem kötelező, mivel a LiveFyre-fiók létrehozása.
