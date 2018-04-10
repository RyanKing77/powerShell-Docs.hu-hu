---
ms.date: 06/12/2017
contributor: JKeithB
ms.topic: conceptual
keywords: gyűjtemény, a powershell, a parancsmag, a psgallery
title: psgallery_pseditions
ms.openlocfilehash: 0b30c1da53832a6b74be7aa14ed9331b1e9fe643
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="items-with-compatible-powershell-editions"></a><span data-ttu-id="e060d-103">Elemek verzióval kompatibilis PowerShell</span><span class="sxs-lookup"><span data-stu-id="e060d-103">Items with compatible PowerShell Editions</span></span>
<span data-ttu-id="e060d-104">Az 5.1-es verziótól kezdődően a PowerShell különböző kiadásokban érhető el, amelyek különböző szolgáltatáskészleteket és platformkompatibilitást kínálnak.</span><span class="sxs-lookup"><span data-stu-id="e060d-104">Starting with version 5.1, PowerShell is available in different editions which denote varying feature sets and platform compatibility.</span></span>

- <span data-ttu-id="e060d-105">**Desktop kiadás:** A .NET-keretrendszeren alapul, és a Windows teljes erőforrás-igényű kiadásain, például a Server Core és a Windows asztali kiadásain futtatott PowerShell-verziókat célzó szkriptekhez és modulokhoz biztosít kompatibilitást.</span><span class="sxs-lookup"><span data-stu-id="e060d-105">**Desktop Edition:** Built on .NET Framework and provides compatibility with scripts and modules targeting versions of PowerShell running on full footprint editions of Windows such as Server Core and Windows Desktop.</span></span>
- <span data-ttu-id="e060d-106">**Core kiadás:** .NET Core-on alapul, és a Windows csökkentett erőforrás-igényű kiadásain, például a Nano Serveren és a Windows IoT kiadásokon futtatott PowerShell-verziókat célzó szkriptekhez és modulokhoz biztosít kompatibilitást.</span><span class="sxs-lookup"><span data-stu-id="e060d-106">**Core Edition:** Built on .NET Core and provides compatibility with scripts and modules targeting versions of PowerShell running on reduced footprint editions of Windows such as Nano Server and Windows IoT.</span></span>

## <a name="powershell-gallery-extracts-supported-pseditions-metadata-and-allows-you-to-filters-the-items-compatible-for-specific-powershell-editions"></a><span data-ttu-id="e060d-107">PowerShell-galériában bontja ki a támogatott PSEditions metaadatok, és lehetővé teszi a szűrők a cikkek kompatibilis a megadott PowerShell esetén</span><span class="sxs-lookup"><span data-stu-id="e060d-107">PowerShell Gallery extracts supported PSEditions metadata and allows you to filters the items compatible for specific PowerShell Editions</span></span>

<span data-ttu-id="e060d-108">Ha egy cikk kompatibilis PSEditions megadott, "PowerShell kiadások" részeként jelennek lap az elem megjelenítése, illetve is elemek eredményekben.</span><span class="sxs-lookup"><span data-stu-id="e060d-108">If an item has compatible PSEditions specified, they will be listed as part of 'PowerShell Editions' in the item display page and also in items results.</span></span>
<span data-ttu-id="e060d-109">![Elem a lap megjelenítése az PSEditions](Images/ItemDisplayPageWithPSEditions.PNG)</span><span class="sxs-lookup"><span data-stu-id="e060d-109">![Item display page with PSEditions](Images/ItemDisplayPageWithPSEditions.PNG)</span></span>

## <a name="search-for-items-in-the-gallery-ui-which-works-on-powershellcore"></a><span data-ttu-id="e060d-110">Keresse meg a felhasználói felület, amely működik-e az PowerShellCore gyűjteményben szereplő elemek</span><span class="sxs-lookup"><span data-stu-id="e060d-110">Search for items in the gallery UI which works on PowerShellCore</span></span>
<span data-ttu-id="e060d-111">Címkék használata: "PSEdition_Desktop" és a címkék: "PSEdition_Core" szűrőkkel PowerShell-galériában elemeket.</span><span class="sxs-lookup"><span data-stu-id="e060d-111">Use Tags:"PSEdition_Desktop" and Tags:"PSEdition_Core" to filters the items on PowerShell Gallery.</span></span>

### <a name="use-tagspseditioncore-to-search-items-compatible-with-powershell-core-edition"></a><span data-ttu-id="e060d-112">Címkék használata: "PSEdition_Core" kompatibilis PowerShell Core Edition elemek kereséséhez.</span><span class="sxs-lookup"><span data-stu-id="e060d-112">Use Tags:"PSEdition_Core" to search items compatible with PowerShell Core Edition.</span></span>
![Keresési eredmények Core PSEdition kompatibilis elemek](Images/SearchResultsWithPSEditions.PNG)

### <a name="use-tagspseditiondesktop-to-search-items-compatible-with-powershell-desktop-edition"></a><span data-ttu-id="e060d-114">Címkék használata: "PSEdition_Desktop" kompatibilis PowerShell asztali Edition elemek kereséséhez.</span><span class="sxs-lookup"><span data-stu-id="e060d-114">Use Tags:"PSEdition_Desktop" to search items compatible with PowerShell Desktop Edition.</span></span>
![Az asztali PSEdition kompatibilis elemek keresési eredmények](Images/SearchResultsWithPSEdition_Desktop.PNG)

## <a name="more-details-on-authoring-and-finding-the-items-with-compatible-powershell-editions"></a><span data-ttu-id="e060d-116">További részleteket a jelentéskészítő és -verzióval kompatibilis PowerShell cikkek keresése</span><span class="sxs-lookup"><span data-stu-id="e060d-116">More details on authoring and finding the items with compatible PowerShell Editions</span></span>
### <a name="modules-with-pseditionspsgetmodulemodulewithpseditionsupportmd"></a>[<span data-ttu-id="e060d-117">PSEditions paraméterrel rendelkező modulok</span><span class="sxs-lookup"><span data-stu-id="e060d-117">Modules with PSEditions</span></span>](../psget/module/modulewithpseditionsupport.md)
### <a name="scripts-with-pseditionspsgetscriptscriptwithpseditionsupportmd"></a>[<span data-ttu-id="e060d-118">PSEditions paraméterrel rendelkező parancsfájlok</span><span class="sxs-lookup"><span data-stu-id="e060d-118">Scripts with PSEditions</span></span>](../psget/script/scriptwithpseditionsupport.md)