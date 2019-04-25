---
ms.date: 12/11/2018
contributor: JKeithB, SydneyhSmith
keywords: katalógus, a powershell, a parancsmag, a psgallery
title: Kompatibilis PowerShell-kiadások vagy operációs rendszert tartalmazó csomagok
ms.openlocfilehash: 14038aa9b0453e1d06e6587e97da391b56297c75
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62084557"
---
# <a name="packages-with-compatible-powershell-editions-or-operating-systems"></a>Kompatibilis PowerShell-kiadások vagy operációs rendszert tartalmazó csomagok

5.1-es verziótól kezdődően PowerShell érhető el a különböző kiadásait, amelyek különböző szolgáltatáskészleteket és platform való kompatibilitása jelöl.

## <a name="searching-by-powershell-edition"></a>Keresés a PowerShell-kiadás alapján

A PowerShell-kiadások a következők:
- **Desktop kiadás:** .NET-keretrendszer épül, és kompatibilis a Windows például a Server Core és a Windows asztal teljes erőforrás-igényű kiadásain fut PowerShell-verziókat célzó szkriptekhez és modulokhoz biztosít.
- **Core kiadás:** .NET Core épül, és kompatibilis csökkentett erőforrás-igényű kiadása esetén például a Nano Server Windows és Windows IoT kiadásokon futtatott PowerShell-verziókat célzó szkriptekhez és modulokhoz biztosít.

### <a name="powershell-gallery-allows-you-to-filter-packages-compatible-for-specific-powershell-editions"></a>PowerShell-galériából lehetővé teszi a csomagok kompatibilis szűrését megadott PowerShell-kiadások

Ha egy csomag kompatibilis psedition paraméterrel megadott, PowerShell-kiadások részeként sorrendjében a csomag megjelenített lapon és a csomagok eredményekben.
PowerShell-lel kompatibilis csomagokat is kereshet.

![Pseditions paraméterrel rendelkező lap elem megjelenítése](../../Images/packagedisplaypagewithpseditions.PNG)

### <a name="search-for-packages-in-the-gallery-ui-that-work-on-powershell-core"></a>Keresse meg a katalógus felhasználói felület csomagokat, amelyek működnek a PowerShell Core-on

Címkék használata: "PSEdition_Desktop" és a címkék: "PSEdition_Core" szűrőkkel a csomagokat a PowerShell-galériában.

### <a name="use-tagspseditioncore-to-search-items-compatible-with-powershell-core-edition"></a>Címkék használata: "PSEdition_Core" elemek kompatibilisek a PowerShell Core kiadás.

![Kompatibilis Core PSEdition elemek a keresési eredmények](../../Images/searchresultswithpseditions.PNG)

### <a name="use-tagspseditiondesktop-to-search-items-compatible-with-powershell-desktop-edition"></a>Címkék használata: "PSEdition_Desktop" PowerShell-Desktop kiadás kompatibilis elemek.

![Kompatibilis PSEdition asztali elemek a keresési eredmények](../../Images/searchresultswithpseditionsdesktop.PNG)

### <a name="search-for-packages-to-find-compatible-editions-using-powershell"></a>Keresse meg a PowerShell-lel kompatibilis kiadások-csomagok keresése
A PowerShell-kiadás és az operációs rendszer szűrése címkék is megadhat.
Használja a `Find-Package` parancsmag megadásával a `-Tag` paraméterrel adja meg a Kiadásfrissítési (és az operációs rendszer) céloz meg.
tetszik:

```powershell
# Find modules compatible with PowerShell Core:
Find-Module -Tag PSEdition_Core

# Find modules compatible with PowerShell Core on Linux:
Find-Module -Tag PSEdition_Core, Linux
```

## <a name="searching-by-operating-system"></a>Operációs rendszer által keresése

A PowerShell Core a Windows, Linux és MacOS rendszeren érhető el, mivel csomagok a katalógusban előfordulhat, hogy ezek az operációs rendszerek bármely kombinációja tervezve. A katalógus felhasználói felületén a következő searchs címkék használatával keresse meg az operációs rendszer által címkézett csomagok:

- Címkék: "Windows"
- Címkék: "Linux"
- Címkék: "MacOS"

Ezekkel a címkékkel is meghatározhat `Find-Module` (és a PowerShellGet modul más parancsmagjai), ehhez hasonló:

```powershell
# Find Modules compatible with Windows
Find-Module -Tag Linux
```

## <a name="searching-for-multiple-compatibilities"></a>Több való kompatibilitása keresése

Kereshet egy csomag, amelynek több való kompatibilitása a szintaxis használatával:

Címkék: "Compatibility1" "Compatibility2"

Például ha a PowerShell Core kompatibilitás a Windows és a Linux rendszerű gépeken futó rendelkező, használja a keresési címkéket:

Címkék: "PSEdition_Core" "Windows" "Linux"

Keresés a PowerShell használatával, használhatja a `Find-Module` (és a PowerShellGet modul más parancsmagjai), ehhez hasonló:

```powershell
# Find scripts compatible with PowerShell Core, Windows, and Linux
Find-Script -Tag PSEdition_Core,Linux,Windows

# Find modules compatible with PowerSHellCore and MacOS
Find-Module -Tag PSEdition_Core,MacOS
```

## <a name="more-details-on-authoring-and-finding-the-packages-with-compatible-powershell-editions"></a>Szerzői műveletek, és kompatibilis PowerShell-kiadások csomagjaival megkeresésével kapcsolatos további információk

- [PSEditions paraméterrel rendelkező modulok](../../concepts/module-psedition-support.md)
- [PSEditions paraméterrel rendelkező parancsfájlok](../../concepts/script-psedition-support.md)
