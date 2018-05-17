---
ms.date: 06/12/2017
contributor: JKeithB
keywords: gyűjtemény, a powershell, a parancsmag, a psgallery
title: Elemek verzióval kompatibilis PowerShell
ms.openlocfilehash: f661c2cd076acb9c11394ba0b752ebd154965ff4
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/16/2018
---
# <a name="items-with-compatible-powershell-editions"></a>Elemek verzióval kompatibilis PowerShell

Az 5.1-es verziótól kezdődően a PowerShell különböző kiadásokban érhető el, amelyek különböző szolgáltatáskészleteket és platformkompatibilitást kínálnak.

- **Desktop kiadás:** A .NET-keretrendszeren alapul, és a Windows teljes erőforrás-igényű kiadásain, például a Server Core és a Windows asztali kiadásain futtatott PowerShell-verziókat célzó szkriptekhez és modulokhoz biztosít kompatibilitást.
- **Core kiadás:** .NET Core-on alapul, és a Windows csökkentett erőforrás-igényű kiadásain, például a Nano Serveren és a Windows IoT kiadásokon futtatott PowerShell-verziókat célzó szkriptekhez és modulokhoz biztosít kompatibilitást.

## <a name="powershell-gallery-extracts-supported-pseditions-metadata-and-allows-you-to-filters-the-items-compatible-for-specific-powershell-editions"></a>PowerShell-galériában bontja ki a támogatott PSEditions metaadatok, és lehetővé teszi a szűrők a cikkek kompatibilis a megadott PowerShell esetén

Ha egy cikk kompatibilis PSEditions megadott, "PowerShell kiadások" részeként jelennek lap az elem megjelenítése, illetve is elemek eredményekben.

![Elem a lap megjelenítése az PSEditions](../../Images/ItemDisplayPageWithPSEditions.PNG)

## <a name="search-for-items-in-the-gallery-ui-which-works-on-powershellcore"></a>Keresse meg a felhasználói felület, amely működik-e az PowerShellCore gyűjteményben szereplő elemek

Címkék használata: "PSEdition_Desktop" és a címkék: "PSEdition_Core" szűrőkkel PowerShell-galériában elemeket.

### <a name="use-tagspseditioncore-to-search-items-compatible-with-powershell-core-edition"></a>Címkék használata: "PSEdition_Core" kompatibilis PowerShell Core Edition elemek kereséséhez.

![Keresési eredmények Core PSEdition kompatibilis elemek](../../Images/SearchResultsWithPSEditions.PNG)

### <a name="use-tagspseditiondesktop-to-search-items-compatible-with-powershell-desktop-edition"></a>Címkék használata: "PSEdition_Desktop" kompatibilis PowerShell asztali Edition elemek kereséséhez.

![Az asztali PSEdition kompatibilis elemek keresési eredmények](../../Images/SearchResultsWithPSEdition-Desktop.PNG)

## <a name="more-details-on-authoring-and-finding-the-items-with-compatible-powershell-editions"></a>További részleteket a jelentéskészítő és -verzióval kompatibilis PowerShell cikkek keresése

- [PSEditions paraméterrel rendelkező modulok](../../concepts/module-psedition-support.md)
- [PSEditions paraméterrel rendelkező parancsfájlok](../../concepts/script-psedition-support.md)