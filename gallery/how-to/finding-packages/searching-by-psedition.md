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
# <a name="packages-with-compatible-powershell-editions"></a><span data-ttu-id="4d111-103">Csomagok kompatibilis PowerShell kiadás</span><span class="sxs-lookup"><span data-stu-id="4d111-103">Packages with compatible PowerShell Editions</span></span>

<span data-ttu-id="4d111-104">Az 5.1-es verziótól kezdődően a PowerShell különböző kiadásokban érhető el, amelyek különböző szolgáltatáskészleteket és platformkompatibilitást kínálnak.</span><span class="sxs-lookup"><span data-stu-id="4d111-104">Starting with version 5.1, PowerShell is available in different editions which denote varying feature sets and platform compatibility.</span></span>

- <span data-ttu-id="4d111-105">**Desktop kiadás:** A .NET-keretrendszeren alapul, és a Windows teljes erőforrás-igényű kiadásain, például a Server Core és a Windows asztali kiadásain futtatott PowerShell-verziókat célzó szkriptekhez és modulokhoz biztosít kompatibilitást.</span><span class="sxs-lookup"><span data-stu-id="4d111-105">**Desktop Edition:** Built on .NET Framework and provides compatibility with scripts and modules targeting versions of PowerShell running on full footprint editions of Windows such as Server Core and Windows Desktop.</span></span>
- <span data-ttu-id="4d111-106">**Core kiadás:** .NET Core-on alapul, és a Windows csökkentett erőforrás-igényű kiadásain, például a Nano Serveren és a Windows IoT kiadásokon futtatott PowerShell-verziókat célzó szkriptekhez és modulokhoz biztosít kompatibilitást.</span><span class="sxs-lookup"><span data-stu-id="4d111-106">**Core Edition:** Built on .NET Core and provides compatibility with scripts and modules targeting versions of PowerShell running on reduced footprint editions of Windows such as Nano Server and Windows IoT.</span></span>

## <a name="powershell-gallery-extracts-supported-pseditions-metadata-and-allows-you-to-filters-the-packages-compatible-for-specific-powershell-editions"></a><span data-ttu-id="4d111-107">PowerShell-galériából kinyeri a támogatott psedition paraméterrel metaadatokat, és lehetővé teszi, hogy a csomagok szűrők kompatibilis az adott PowerShell-kiadások</span><span class="sxs-lookup"><span data-stu-id="4d111-107">PowerShell Gallery extracts supported PSEditions metadata and allows you to filters the packages compatible for specific PowerShell Editions</span></span>

<span data-ttu-id="4d111-108">Ha egy csomag kompatibilis psedition paraméterrel megadott, a PowerShell-kiadások részeként jelennek a csomag megjelenített lapon és a csomagok eredmények.</span><span class="sxs-lookup"><span data-stu-id="4d111-108">If a package has compatible PSEditions specified, they will be listed as part of 'PowerShell Editions' in the package display page and also in packages results.</span></span>

![Pseditions paraméterrel rendelkező lap elem megjelenítése](../../Images/manual_package_download.png)

## <a name="search-for-packages-in-the-gallery-ui-which-works-on-powershellcore"></a><span data-ttu-id="4d111-110">A katalógus felhasználói felület, amely PowerShellCore működik csomagok keresése</span><span class="sxs-lookup"><span data-stu-id="4d111-110">Search for packages in the gallery UI which works on PowerShellCore</span></span>

<span data-ttu-id="4d111-111">Címkék használata: "PSEdition_Desktop" és a címkék: "PSEdition_Core" szűrőkkel a csomagokat a PowerShell-galériában.</span><span class="sxs-lookup"><span data-stu-id="4d111-111">Use Tags:"PSEdition_Desktop" and Tags:"PSEdition_Core" to filters the packages on PowerShell Gallery.</span></span>

### <a name="use-tagspseditioncore-to-search-items-compatible-with-powershell-core-edition"></a><span data-ttu-id="4d111-112">Címkék használata: "PSEdition_Core" elemek kompatibilisek a PowerShell Core kiadás.</span><span class="sxs-lookup"><span data-stu-id="4d111-112">Use Tags:"PSEdition_Core" to search items compatible with PowerShell Core Edition.</span></span>

![Kompatibilis Core PSEdition elemek a keresési eredmények](../../Images/SearchResultsWithPSEditions.PNG)

### <a name="use-tagspseditiondesktop-to-search-items-compatible-with-powershell-desktop-edition"></a><span data-ttu-id="4d111-114">Címkék használata: "PSEdition_Desktop" PowerShell-Desktop kiadás kompatibilis elemek.</span><span class="sxs-lookup"><span data-stu-id="4d111-114">Use Tags:"PSEdition_Desktop" to search items compatible with PowerShell Desktop Edition.</span></span>

![Kompatibilis PSEdition asztali elemek a keresési eredmények](../../Images/SearchResultsWithPSEdition-Desktop.PNG)

## <a name="more-details-on-authoring-and-finding-the-packages-with-compatible-powershell-editions"></a><span data-ttu-id="4d111-116">Szerzői műveletek, és kompatibilis PowerShell-kiadások csomagjaival megkeresésével kapcsolatos további információk</span><span class="sxs-lookup"><span data-stu-id="4d111-116">More details on authoring and finding the packages with compatible PowerShell Editions</span></span>

- [<span data-ttu-id="4d111-117">PSEditions paraméterrel rendelkező modulok</span><span class="sxs-lookup"><span data-stu-id="4d111-117">Modules with PSEditions</span></span>](../../concepts/module-psedition-support.md)
- [<span data-ttu-id="4d111-118">PSEditions paraméterrel rendelkező parancsfájlok</span><span class="sxs-lookup"><span data-stu-id="4d111-118">Scripts with PSEditions</span></span>](../../concepts/script-psedition-support.md)
