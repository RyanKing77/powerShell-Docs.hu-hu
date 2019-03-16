---
ms.date: 12/11/2018
contributor: JKeithB, SydneyhSmith
keywords: katalógus, a powershell, a parancsmag, a psgallery
title: Kompatibilis PowerShell-kiadások vagy operációs rendszert tartalmazó csomagok
ms.openlocfilehash: 14038aa9b0453e1d06e6587e97da391b56297c75
ms.sourcegitcommit: caac7d098a448232304c9d6728e7340ec7517a71
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/16/2019
ms.locfileid: "58057178"
---
# <a name="packages-with-compatible-powershell-editions-or-operating-systems"></a><span data-ttu-id="8da36-103">Kompatibilis PowerShell-kiadások vagy operációs rendszert tartalmazó csomagok</span><span class="sxs-lookup"><span data-stu-id="8da36-103">Packages with compatible PowerShell Editions or Operating Systems</span></span>

<span data-ttu-id="8da36-104">5.1-es verziótól kezdődően PowerShell érhető el a különböző kiadásait, amelyek különböző szolgáltatáskészleteket és platform való kompatibilitása jelöl.</span><span class="sxs-lookup"><span data-stu-id="8da36-104">Starting with version 5.1, PowerShell is available in different editions which denote varying feature sets and platform compatibilities.</span></span>

## <a name="searching-by-powershell-edition"></a><span data-ttu-id="8da36-105">Keresés a PowerShell-kiadás alapján</span><span class="sxs-lookup"><span data-stu-id="8da36-105">Searching by PowerShell Edition</span></span>

<span data-ttu-id="8da36-106">A PowerShell-kiadások a következők:</span><span class="sxs-lookup"><span data-stu-id="8da36-106">The two editions of PowerShell are:</span></span>
- <span data-ttu-id="8da36-107">**Desktop kiadás:** .NET-keretrendszer épül, és kompatibilis a Windows például a Server Core és a Windows asztal teljes erőforrás-igényű kiadásain fut PowerShell-verziókat célzó szkriptekhez és modulokhoz biztosít.</span><span class="sxs-lookup"><span data-stu-id="8da36-107">**Desktop Edition:** Built on .NET Framework and provides compatibility with scripts and modules targeting versions of PowerShell running on full footprint editions of Windows such as Server Core and Windows Desktop.</span></span>
- <span data-ttu-id="8da36-108">**Core kiadás:** .NET Core épül, és kompatibilis csökkentett erőforrás-igényű kiadása esetén például a Nano Server Windows és Windows IoT kiadásokon futtatott PowerShell-verziókat célzó szkriptekhez és modulokhoz biztosít.</span><span class="sxs-lookup"><span data-stu-id="8da36-108">**Core Edition:** Built on .NET Core and provides compatibility with scripts and modules targeting versions of PowerShell running on reduced footprint editions of Windows such as Nano Server and Windows IoT.</span></span>

### <a name="powershell-gallery-allows-you-to-filter-packages-compatible-for-specific-powershell-editions"></a><span data-ttu-id="8da36-109">PowerShell-galériából lehetővé teszi a csomagok kompatibilis szűrését megadott PowerShell-kiadások</span><span class="sxs-lookup"><span data-stu-id="8da36-109">PowerShell Gallery allows you to filter packages compatible for specific PowerShell Editions</span></span>

<span data-ttu-id="8da36-110">Ha egy csomag kompatibilis psedition paraméterrel megadott, PowerShell-kiadások részeként sorrendjében a csomag megjelenített lapon és a csomagok eredményekben.</span><span class="sxs-lookup"><span data-stu-id="8da36-110">If a package has compatible PSEditions specified, they are listed as part of 'PowerShell Editions' in the package display page and also in packages results.</span></span>
<span data-ttu-id="8da36-111">PowerShell-lel kompatibilis csomagokat is kereshet.</span><span class="sxs-lookup"><span data-stu-id="8da36-111">You can also search for compatible packages using PowerShell.</span></span>

![Pseditions paraméterrel rendelkező lap elem megjelenítése](../../Images/packagedisplaypagewithpseditions.PNG)

### <a name="search-for-packages-in-the-gallery-ui-that-work-on-powershell-core"></a><span data-ttu-id="8da36-113">Keresse meg a katalógus felhasználói felület csomagokat, amelyek működnek a PowerShell Core-on</span><span class="sxs-lookup"><span data-stu-id="8da36-113">Search for packages in the gallery UI that work on PowerShell Core</span></span>

<span data-ttu-id="8da36-114">Címkék használata: "PSEdition_Desktop" és a címkék: "PSEdition_Core" szűrőkkel a csomagokat a PowerShell-galériában.</span><span class="sxs-lookup"><span data-stu-id="8da36-114">Use Tags:"PSEdition_Desktop" and Tags:"PSEdition_Core" to filters the packages on PowerShell Gallery.</span></span>

### <a name="use-tagspseditioncore-to-search-items-compatible-with-powershell-core-edition"></a><span data-ttu-id="8da36-115">Címkék használata: "PSEdition_Core" elemek kompatibilisek a PowerShell Core kiadás.</span><span class="sxs-lookup"><span data-stu-id="8da36-115">Use Tags:"PSEdition_Core" to search items compatible with PowerShell Core Edition.</span></span>

![Kompatibilis Core PSEdition elemek a keresési eredmények](../../Images/searchresultswithpseditions.PNG)

### <a name="use-tagspseditiondesktop-to-search-items-compatible-with-powershell-desktop-edition"></a><span data-ttu-id="8da36-117">Címkék használata: "PSEdition_Desktop" PowerShell-Desktop kiadás kompatibilis elemek.</span><span class="sxs-lookup"><span data-stu-id="8da36-117">Use Tags:"PSEdition_Desktop" to search items compatible with PowerShell Desktop Edition.</span></span>

![Kompatibilis PSEdition asztali elemek a keresési eredmények](../../Images/searchresultswithpseditionsdesktop.PNG)

### <a name="search-for-packages-to-find-compatible-editions-using-powershell"></a><span data-ttu-id="8da36-119">Keresse meg a PowerShell-lel kompatibilis kiadások-csomagok keresése</span><span class="sxs-lookup"><span data-stu-id="8da36-119">Search for packages to find compatible editions using PowerShell</span></span>
<span data-ttu-id="8da36-120">A PowerShell-kiadás és az operációs rendszer szűrése címkék is megadhat.</span><span class="sxs-lookup"><span data-stu-id="8da36-120">You can specify tags to filter for the PowerShell edition and OS.</span></span>
<span data-ttu-id="8da36-121">Használja a `Find-Package` parancsmag megadásával a `-Tag` paraméterrel adja meg a Kiadásfrissítési (és az operációs rendszer) céloz meg.</span><span class="sxs-lookup"><span data-stu-id="8da36-121">You use the `Find-Package` cmdlet specifying the `-Tag` parameter to specify the edition (and OS) you are targeting.</span></span>
<span data-ttu-id="8da36-122">tetszik:</span><span class="sxs-lookup"><span data-stu-id="8da36-122">Like this:</span></span>

```powershell
# Find modules compatible with PowerShell Core:
Find-Module -Tag PSEdition_Core

# Find modules compatible with PowerShell Core on Linux:
Find-Module -Tag PSEdition_Core, Linux
```

## <a name="searching-by-operating-system"></a><span data-ttu-id="8da36-123">Operációs rendszer által keresése</span><span class="sxs-lookup"><span data-stu-id="8da36-123">Searching by Operating System</span></span>

<span data-ttu-id="8da36-124">A PowerShell Core a Windows, Linux és MacOS rendszeren érhető el, mivel csomagok a katalógusban előfordulhat, hogy ezek az operációs rendszerek bármely kombinációja tervezve.</span><span class="sxs-lookup"><span data-stu-id="8da36-124">Since PowerShell Core is available for Windows, Linux, and MacOS, packages in the Gallery may be designed for any combination of these operating systems.</span></span> <span data-ttu-id="8da36-125">A katalógus felhasználói felületén a következő searchs címkék használatával keresse meg az operációs rendszer által címkézett csomagok:</span><span class="sxs-lookup"><span data-stu-id="8da36-125">In the gallery UI use the following searchs tags to find packages tagged by operating system:</span></span>

- <span data-ttu-id="8da36-126">Címkék: "Windows"</span><span class="sxs-lookup"><span data-stu-id="8da36-126">Tags: "Windows"</span></span>
- <span data-ttu-id="8da36-127">Címkék: "Linux"</span><span class="sxs-lookup"><span data-stu-id="8da36-127">Tags: "Linux"</span></span>
- <span data-ttu-id="8da36-128">Címkék: "MacOS"</span><span class="sxs-lookup"><span data-stu-id="8da36-128">Tags: "MacOS"</span></span>

<span data-ttu-id="8da36-129">Ezekkel a címkékkel is meghatározhat `Find-Module` (és a PowerShellGet modul más parancsmagjai), ehhez hasonló:</span><span class="sxs-lookup"><span data-stu-id="8da36-129">You can specify these tags on `Find-Module` (and other cmdlets in the PowerShellGet module), like this:</span></span>

```powershell
# Find Modules compatible with Windows
Find-Module -Tag Linux
```

## <a name="searching-for-multiple-compatibilities"></a><span data-ttu-id="8da36-130">Több való kompatibilitása keresése</span><span class="sxs-lookup"><span data-stu-id="8da36-130">Searching for Multiple Compatibilities</span></span>

<span data-ttu-id="8da36-131">Kereshet egy csomag, amelynek több való kompatibilitása a szintaxis használatával:</span><span class="sxs-lookup"><span data-stu-id="8da36-131">You can look for a package that has multiple compatibilities by using the syntax:</span></span>

<span data-ttu-id="8da36-132">Címkék: "Compatibility1" "Compatibility2"</span><span class="sxs-lookup"><span data-stu-id="8da36-132">Tags: "Compatibility1" "Compatibility2"</span></span>

<span data-ttu-id="8da36-133">Például ha a PowerShell Core kompatibilitás a Windows és a Linux rendszerű gépeken futó rendelkező, használja a keresési címkéket:</span><span class="sxs-lookup"><span data-stu-id="8da36-133">For example, if you are looking for a package with PowerShell Core Compatibility that runs on both my Windows and Linux machines, use the search tags:</span></span>

<span data-ttu-id="8da36-134">Címkék: "PSEdition_Core" "Windows" "Linux"</span><span class="sxs-lookup"><span data-stu-id="8da36-134">Tags: "PSEdition_Core" "Windows" "Linux"</span></span>

<span data-ttu-id="8da36-135">Keresés a PowerShell használatával, használhatja a `Find-Module` (és a PowerShellGet modul más parancsmagjai), ehhez hasonló:</span><span class="sxs-lookup"><span data-stu-id="8da36-135">To search using PowerShell, you can use the `Find-Module` (and the other cmdlets in the PowerShellGet module), like this:</span></span>

```powershell
# Find scripts compatible with PowerShell Core, Windows, and Linux
Find-Script -Tag PSEdition_Core,Linux,Windows

# Find modules compatible with PowerSHellCore and MacOS
Find-Module -Tag PSEdition_Core,MacOS
```

## <a name="more-details-on-authoring-and-finding-the-packages-with-compatible-powershell-editions"></a><span data-ttu-id="8da36-136">Szerzői műveletek, és kompatibilis PowerShell-kiadások csomagjaival megkeresésével kapcsolatos további információk</span><span class="sxs-lookup"><span data-stu-id="8da36-136">More details on authoring and finding the packages with compatible PowerShell Editions</span></span>

- [<span data-ttu-id="8da36-137">PSEditions paraméterrel rendelkező modulok</span><span class="sxs-lookup"><span data-stu-id="8da36-137">Modules with PSEditions</span></span>](../../concepts/module-psedition-support.md)
- [<span data-ttu-id="8da36-138">PSEditions paraméterrel rendelkező parancsfájlok</span><span class="sxs-lookup"><span data-stu-id="8da36-138">Scripts with PSEditions</span></span>](../../concepts/script-psedition-support.md)
