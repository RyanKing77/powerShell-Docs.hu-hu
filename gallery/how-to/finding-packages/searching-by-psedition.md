---
ms.date: 06/12/2017
contributor: JKeithB
keywords: katalógus, a powershell, a parancsmag, a psgallery
title: Csomagok kompatibilis PowerShell kiadás
ms.openlocfilehash: e16cfb0ee30e344c9399bec2985baafc5a252fd7
ms.sourcegitcommit: 98b7cfd8ad5718efa8e320526ca76c3cc4141d78
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/25/2018
ms.locfileid: "50004082"
---
# <a name="packages-with-compatible-powershell-editions"></a>Csomagok kompatibilis PowerShell kiadás

Az 5.1-es verziótól kezdődően a PowerShell különböző kiadásokban érhető el, amelyek különböző szolgáltatáskészleteket és platformkompatibilitást kínálnak.

- **Desktop kiadás:** A .NET-keretrendszeren alapul, és a Windows teljes erőforrás-igényű kiadásain, például a Server Core és a Windows asztali kiadásain futtatott PowerShell-verziókat célzó szkriptekhez és modulokhoz biztosít kompatibilitást.
- **Core kiadás:** .NET Core-on alapul, és a Windows csökkentett erőforrás-igényű kiadásain, például a Nano Serveren és a Windows IoT kiadásokon futtatott PowerShell-verziókat célzó szkriptekhez és modulokhoz biztosít kompatibilitást.

## <a name="powershell-gallery-extracts-supported-pseditions-metadata-and-allows-you-to-filters-the-packages-compatible-for-specific-powershell-editions"></a>PowerShell-galériából kinyeri a támogatott psedition paraméterrel metaadatokat, és lehetővé teszi, hogy a csomagok szűrők kompatibilis az adott PowerShell-kiadások

Ha egy csomag kompatibilis psedition paraméterrel megadott, a PowerShell-kiadások részeként jelennek a csomag megjelenített lapon és a csomagok eredmények.

![Pseditions paraméterrel rendelkező lap elem megjelenítése](../../Images/manual_package_download.png)

## <a name="search-for-packages-in-the-gallery-ui-which-works-on-powershellcore"></a>A katalógus felhasználói felület, amely PowerShellCore működik csomagok keresése

Címkék használata: "PSEdition_Desktop" és a címkék: "PSEdition_Core" szűrőkkel a csomagokat a PowerShell-galériában.

### <a name="use-tagspseditioncore-to-search-items-compatible-with-powershell-core-edition"></a>Címkék használata: "PSEdition_Core" elemek kompatibilisek a PowerShell Core kiadás.

![Kompatibilis Core PSEdition elemek a keresési eredmények](../../Images/SearchResultsWithPSEditions.PNG)

### <a name="use-tagspseditiondesktop-to-search-items-compatible-with-powershell-desktop-edition"></a>Címkék használata: "PSEdition_Desktop" PowerShell-Desktop kiadás kompatibilis elemek.

![Kompatibilis PSEdition asztali elemek a keresési eredmények](../../Images/SearchResultsWithPSEdition-Desktop.PNG)

## <a name="more-details-on-authoring-and-finding-the-packages-with-compatible-powershell-editions"></a>Szerzői műveletek, és kompatibilis PowerShell-kiadások csomagjaival megkeresésével kapcsolatos további információk

- [PSEditions paraméterrel rendelkező modulok](../../concepts/module-psedition-support.md)
- [PSEditions paraméterrel rendelkező parancsfájlok](../../concepts/script-psedition-support.md)
