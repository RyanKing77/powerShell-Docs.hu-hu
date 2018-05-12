---
ms.date: 06/12/2017
contributor: JKeithB
ms.topic: conceptual
keywords: gyűjtemény, a powershell, a parancsmag, a psgallery
title: Létrehozása és közzététele egy elemet
ms.openlocfilehash: 1640d35d684bbb399336eecef529e6efd8075da3
ms.sourcegitcommit: e9ad4d85fd7eb72fb5bc37f6ca3ae1282ae3c6d7
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/10/2018
---
# <a name="creating-and-publishing-an-item"></a>Létrehozása és közzététele egy elemet

A PowerShell-galériában közzététele és megosztása stabil PowerShell-modulok, a parancsfájlok és a DSC-erőforrások az PowerShell szélesebb körű felhasználói Közösséggel a hely.

Ez a cikk ismerteti a mechanika és fontos történő előkészítésének lépéseit egy parancsfájl vagy modul, és közzéteheti azt a PowerShell-galériában.
Azt javasoljuk, hogy tekintse át a [közzétételi irányelvek](https://msdn.microsoft.com/en-us/powershell/gallery/psgallery/psgallery-PublishingGuidelines) győződjön meg arról, hogy a elemeket tesz közzé szélesebb körben elfogadják PowerShell-galériában felhasználók megismerése.

A cikk közzétételéhez a PowerShell-galériában minimális követelmények a következők:

- PowerShell-galériában fiókkal rendelkezik, és a vele társított az API-kulcs
- Győződjön meg arról metaadat szükséges az elemben
- Győződjön meg arról, a cikk közzétételéhez készen áll az előzetes ellenőrzése eszközök segítségével
- A cikk közzétételéhez a Publish-modul és a közzététel-parancsfájl paranccsal PowerShell-galériában
- Válaszol kérdéseivel és észrevételeivel a elemével kapcsolatban

A PowerShell-galériában PowerShell-modulok és a PowerShell-parancsfájlok fogad el.
Ha a parancsfájlok hivatkozunk, azt egy PowerShell-parancsfájlt, amely egy egyetlen fájlt, és nem nagyobb modulja részét jelenti.

## <a name="powershell-gallery-account-and-api-key"></a>PowerShell-galériában fiók és API-kulcs

Lásd: [PowerShell gyűjtemény fiók létrehozása](https://msdn.microsoft.com/en-us/powershell/gallery/psgallery/psgallery_creating_an_account) a PowerShell-galériában fiókja beállításával.

Fiók létrehozását követően érheti el a cikk közzétételéhez szükséges API-kulcs.
A fiókkal jelentkezik be, miután a felhasználónév regisztrálása helyett a PowerShell-galériában lap tetején fog megjelenni.
Kattintson a felhasználónevére elindítjuk ezt a saját fiók lapra, ahol megtalálja az API-kulcsot.

Megjegyzés: Az API-kulcsot kell kezelni, a felhasználónevet és jelszót biztonságos helyen.
A kulcshoz, vagy valaki másról, frissítheti a PowerShell-galériában saját elemek.
Javasoljuk, hogy rendszeresen, a kulcs, amely végezhető frissítése kulccsal alaphelyzetbe a saját fiók-lapon.

## <a name="required-metadata-for-items-published-to-the-powershell-gallery"></a>A PowerShell-galériában közzétett cikkek kötelező metaadatok

A PowerShell-galériában alapján a parancsfájl vagy modul jegyzékben szereplő metaadatok mezők gallery felhasználói adatokat szolgáltat.
Létrehozása vagy módosítása a PowerShell-galériában kiadvány elemek rendelkezik egy kis készletét a cikk jegyzékben szereplő adatok követelményeinek.
Azt javasoljuk, hogy a cikk metaadatok részében tekintse át a [közzétételi irányelvek](https://msdn.microsoft.com/en-us/powershell/gallery/psgallery/psgallery-PublishingGuidelines) a legjobb információt nyújt a felhasználók számára az elemek hogyan.

A [New-ModuleManifest](https://msdn.microsoft.com/en-us/powershell/gallery/psget/module/ModuleManifest-Reference) és [New-ScriptFileInfo](https://msdn.microsoft.com/en-us/powershell/gallery/psget/script/psget_new-scriptfileinfo) parancsmagok a jegyzék sablon hozza létre, a helyőrzők a jegyzék elemek.

Mind jegyzékfájlokat rendelkezik két szakaszok fontos a közzétételt, a PrivateData a PowerShell modul jegyzék elsődleges kulcs adatainak elsődleges kulcs az adatok és PSData területe mindent kívül a PrivateData szakasz.
Az elsődleges kulcsok van kötve a PowerShell verzióját használja, és nincs definiálva nem támogatottak.
PrivateData támogatja az új kulcsok hozzáadása, úgy, hogy a PowerShell-galériában vonatkozó elemeket a PSData.


Közzéteszi a PowerShell-galériában elem kitöltése legfontosabb jegyzék elemei a következők:

- Parancsfájl vagy modulnév - azokat a paraméterkészletben található állítják a. Egy olyan parancsfájlt, PS1 vagy a. Egy modul psd1 kiterjesztésű.
- Verzió - Ez egy szükséges elsődleges kulcs, formátumot kell követnie (ajánlott eljárások talál információt) SemVer irányelvek
- Szerző - ez szükséges elsődleges kulcs, és a cikk társítani kell a nevét tartalmazza (lásd a szerzők és tulajdonosai alatt)
- Leírás – Ez az elsődleges kulcs kötelező, segítségével ismertetik a mi nem ezt az elemet, és a bármely vonatkozó követelményekhez
- ProjectURI - a mező értéke egy erősen ajánlott URI, amely egy Github-tárház egy hivatkozást kínál a PSData vagy az elem fejlesztési végezheti hasonló helyen

Szerzők és a PowerShell-galériában tulajdonosok elemek kapcsolatos fogalmak, de nem mindig felelnek meg.
Konfigurációelem tulajdonosainak PowerShell-galériában fiókkal a cikk kezelése engedéllyel rendelkező felhasználók. Előfordulhat, hogy sok tulajdonosai, aki frissítheti bármelyik elemre.
A tulajdonos csak érhető el a PowerShell-galériából, és elvész, ha a cikk egy rendszer átmásolva a másikra.
Szerző: beépített a jegyzék adatokat, így az mindig az elem részét karakterlánc.
A Microsoft-termékek elemek kapcsolatos ajánlások a következők:

- Több tulajdonosokra bízza, legalább egy, a csapat a cikk; előállító nevét folyamatban van
- Rendelkeznie kell a jól ismert csoport nevét (például az Azure SDK csoport) Szerző vagy a Microsoft Corporation.


## <a name="pre-validate-your-item"></a>A cikk előzetes ellenőrzése

Van néhány eszközök futtatásához a kódot a cikk a PowerShell-galériában való közzététele előtt kell:

- [PowerShell parancsfájl Analyzer](https://www.powershellgallery.com/packages/PSScriptAnalyzer/), amely van a PowerShell-galériában
- A modulok, PowerShell részét képező teszt ModuleManifest
- Parancsfájlok, amely PowerShell Get teszt ScriptFileInfo

[PowerShell parancsfájl Analyzer](https://www.powershellgallery.com/packages/PSScriptAnalyzer/) egy statikus kód elemző eszköz, amely a rendszer ellenőrzi a kód azt irányelvek kódolási alapvető PowerShell megfelel-e. Az eszköz közös és fontos problémák a kódban azonosítja, és rendszeresen közzététele készülhet a cikk a fejlesztés során kell futtatni.
PowerShell parancsfájl Analyzer nyújtják a hibákat, figyelmeztetés és információs forrásként azonosított problémák listája.
Az összes hiba kell figyelembe venni, a PowerShell-galériában való közzététel előtt. Figyelmeztetések kell vizsgálni, és a legtöbb kell figyelembe venni.
PowerShell parancsfájl Analyzer futtatása minden alkalommal, amikor egy elem közzétéve, vagy a PowerShell-galériában frissítve.
A gyűjtemény műveleti csapata kapcsolatba fog lépni elem tulajdonosai számára a cím hibákat talált.

Ha a cikk a jegyzék adatokat nem lehet olvasni a PowerShell-galériában infrastruktúra, csak akkor tudja közzétenni.
[Teszt-ModuleManifest](https://msdn.microsoft.com/en-us/powershell/reference/5.1/microsoft.powershell.core/test-modulemanifest) fog dolgozza fel a gyakori problémák, amelyek a modul nem lesz használható, ha telepítve van. Minden modul közzéteheti azt a PowerShell-galériában előtt kell futtatni.

Hasonlóképpen [teszt-ScriptFileInfo](https://msdn.microsoft.com/en-us/powershell/gallery/psget/script/psget_test-scriptfileinfo) érvényesíti a metaadatokat egy parancsfájlt, és minden parancsfájl (közzétett külön, és a modulok) közzéteheti azt a Powershell-galériában előtt kell futtatni.


## <a name="publishing-items"></a>Közzétételi elemek

Kell használnia a [Publish-parancsfájl](https://msdn.microsoft.com/en-us/powershell/gallery/psget/script/psget_publish-script) vagy [Publish-modul](https://msdn.microsoft.com/en-us/powershell/gallery/psget/module/psget_publish-module) elemek közzététele a PowerShell-galériában.
Ezek a parancsok mindkét esetében

- Az elem elérési útját lesznek közzétéve. Egy modul a modul nevű mappát használja. Ha megad egy mappát, amely ugyanabban a modulban több verzióját tartalmazza, RequiredVersion kell megadnia.
- A Nuget API-kulcsot. Ez az API-kulcsot a PowerShell-galériában saját fiók lapján található.

A többi beállítást, a parancssorban a legtöbb, akkor nem kell a parancsban adja meg azokat a cikk közzétételekor, a jegyzék adatokat kell megadni.

Hibák elkerülése érdekében javasolt, hogy a parancsok - Whatif használatával megpróbál-Verbose, a közzététel előtt.
Megtakarít jelentős időt, mivel minden alkalommal, amikor a PowerShell-galériában közzéteszi, frissítenie kell a cikk a manifest szakasz a verziószámot.

Példák lenne: "Publish-modul-elérési út". \MyModule "- RequiredVersion"0.0.1"- NugetAPIKey"GUID"- Whatif-részletes" "Publish-parancsfájl-elérési út".\MyScriptFile.PS1"- NugetAPIKey"GUID"- Whatif-Verbose"

Gondosan tekintse át a kimenetet, és ha nincs hiba vagy figyelmeztetés jelenik meg, ismételje meg a parancs - Whatif nélkül.

A PowerShell-galériában közzétett összes elemet vírusok megvizsgálja, és a PowerShell parancsfájl Analyzer segítségével elemzik.
A problémák merülnek fel a jelenleg a közzétevőjének kapnak a feloldásához.

Amint egy elem közzétette a PowerShell-galériában, szüksége lesz a cikk kapcsolatos visszajelzéseket figyelendő.

- Győződjön meg arról, figyelemmel kísérni a közzétételéhez használt fiókhoz tartozó e-mail címet.
A felhasználók és a PowerShell-Galériabeli műveleti csapata fog visszajelzést keresztül fiók, beleértve a PSSA vagy a víruskereső vizsgálatok problémákat.
Ha az e-mail fiók érvénytelen, vagy ha komoly problémákat a fiók és a hosszú ideig feloldatlan balra jelentett, elemek hagyva, ezért el lesz távolítva a PowerShell-galériából ismertetett lehet tekinteni a [használati](https://www.powershellgallery.com/policies/Terms).
- Azt javasoljuk, hogy az egyes PowerShell gyűjteményelem közzététele megjegyzések előfizetni.
Ez lehetővé teszi, hogy értesítést, ha bárki, aki a PowerShell-galériában a elemén megjegyzések.
Ez nem kötelező, mivel az LiveFyre rendelkező fiók létrehozása.