---
ms.date: 06/12/2017
contributor: JKeithB
ms.topic: conceptual
keywords: gyűjtemény, a powershell, a parancsmag, a psgallery
title: Gyűjteményelem keresési szintaxisának
ms.openlocfilehash: 4c0e357957ef970826ee90868db78ac07a14c804
ms.sourcegitcommit: e9ad4d85fd7eb72fb5bc37f6ca3ae1282ae3c6d7
ms.contentlocale: hu-HU
ms.lasthandoff: 05/10/2018
---
# <a name="gallery-search-syntax"></a><span data-ttu-id="74e31-103">Gyűjteményelem keresési szintaxisának</span><span class="sxs-lookup"><span data-stu-id="74e31-103">Gallery Search Syntax</span></span>

<span data-ttu-id="74e31-104">PowerShell-galériában kínál a szöveg searchbox, ahol ugyanúgy használhatók szavak, kifejezések és kulcsszó kifejezések keresési eredmények szűkítéséhez.</span><span class="sxs-lookup"><span data-stu-id="74e31-104">PowerShell Gallery offers a text searchbox where you can use words, phrases and keyword expressions to narrow down search results.</span></span>

## <a name="search-by-keywords"></a><span data-ttu-id="74e31-105">Keresési kulcsszavakat</span><span class="sxs-lookup"><span data-stu-id="74e31-105">Search by Keywords</span></span>

    dsc azure sql

<span data-ttu-id="74e31-106">Keresés a lehető legkedvezőbb módon vonatkozó összes 3 kulcsszavak tartalmazó dokumentumok kereséséhez tegye, és térjen vissza a megfelelő dokumentumok.</span><span class="sxs-lookup"><span data-stu-id="74e31-106">Search will do its best effort to find relevant documents containing all 3 keywords, and return matching documents.</span></span>

## <a name="search-using-phrases-and-keywords"></a><span data-ttu-id="74e31-107">A keresés kifejezések és kulcsszavak használatával</span><span class="sxs-lookup"><span data-stu-id="74e31-107">Search using Phrases and keywords</span></span>

    "azure sql" deployment

<span data-ttu-id="74e31-108">Írja be a kódját idézőjelek között ("") módosíthatja a keresés keresse meg az adott kifejezést külön kulcsszavak helyett.</span><span class="sxs-lookup"><span data-stu-id="74e31-108">Entering a phrase between quotation marks ("") change the search to look for the particular phrase instead of separate keywords.</span></span>
<span data-ttu-id="74e31-109">Dokumentumok megfelelő általában tartalmaznia kell a pontos kifejezés "azure sql", így például a kis-és nagybetűk változata "Az azure SQL", és általában is a "telepítés" szót tartalmaz.</span><span class="sxs-lookup"><span data-stu-id="74e31-109">Matching documents should usually contain the exact phrase "azure sql", including variations on capitalization e.g. "Azure SQL", and also usually contain the word 'deployment'.</span></span>

## <a name="filtering-on-fields"></a><span data-ttu-id="74e31-110">A mezőkre szűrése</span><span class="sxs-lookup"><span data-stu-id="74e31-110">Filtering on fields</span></span>

<span data-ttu-id="74e31-111">Kereshet egy adott cikk azonosítója (vagy "Id" vagy "id"), vagy bizonyos más mezők illesztésével végezzen keresést a mező nevét a kifejezéseket.</span><span class="sxs-lookup"><span data-stu-id="74e31-111">You can search for a specific item ID (or 'Id' or 'id'), or certain other fields by prefixing search terms with the field name.</span></span>

<span data-ttu-id="74e31-112">A kereshető mezők jelenleg "Id", "Version", "Címke", "Szerző", "Tulajdonos", "Függvények", "Parancsmagok", "DscResources" és "PowerShellVersion".</span><span class="sxs-lookup"><span data-stu-id="74e31-112">Currently the searchable fields are 'Id', 'Version', 'Tags', 'Author', 'Owner', 'Functions', 'Cmdlets', 'DscResources' and 'PowerShellVersion'.</span></span>

<span data-ttu-id="74e31-113">[Mi az a különbség azonosítója és a cím?</span><span class="sxs-lookup"><span data-stu-id="74e31-113">[What's the difference between ID and Title?</span></span> <span data-ttu-id="74e31-114">Azonosító a konzol használata esetén.</span><span class="sxs-lookup"><span data-stu-id="74e31-114">ID is the name you use in the console.</span></span> <span data-ttu-id="74e31-115">-E a keresési eredmények elem lap tetején látható.]</span><span class="sxs-lookup"><span data-stu-id="74e31-115">Title is what is shown at the top of the item page in search results.]</span></span>

## <a name="examples"></a><span data-ttu-id="74e31-116">Példák</span><span class="sxs-lookup"><span data-stu-id="74e31-116">Examples</span></span>

    ID:"PSReadline"
    id:"AzureRM.Profile"

<span data-ttu-id="74e31-117">illetve talál "PSReadline" vagy "AzureRM.Profile" elemet az Azonosítót tartalmazó mezőt.</span><span class="sxs-lookup"><span data-stu-id="74e31-117">finds items with "PSReadline" or "AzureRM.Profile" in their ID field respectively.</span></span>

    Id:"AzureRM.Profile"

<span data-ttu-id="74e31-118">egy másik módja az azonosító mezőben "AzureRM.Profile" elemek kereséséhez.</span><span class="sxs-lookup"><span data-stu-id="74e31-118">is another way to find items with "AzureRM.Profile" in their ID field.</span></span>

<span data-ttu-id="74e31-119">Az "Id" szűrő karakterláncrész egyeznek, így ha a a következő:</span><span class="sxs-lookup"><span data-stu-id="74e31-119">The 'Id' filter is a substring match, so if you search for the following:</span></span>

    Id:"azure"

<span data-ttu-id="74e31-120">Például a "AzureRM.Profile" és "Azure.Storage" eredmények lesz.</span><span class="sxs-lookup"><span data-stu-id="74e31-120">You'll get results like 'AzureRM.Profile' and 'Azure.Storage'.</span></span>

<span data-ttu-id="74e31-121">Egy mező több kulcsszavak is kereshet.</span><span class="sxs-lookup"><span data-stu-id="74e31-121">You can also search for multiple keywords in a single field.</span></span> <span data-ttu-id="74e31-122">Vagy kombinációs mezőket.</span><span class="sxs-lookup"><span data-stu-id="74e31-122">Or mix and match fields.</span></span>

    id:azure tags:intellisense
    id:azure id:storage

<span data-ttu-id="74e31-123">És kifejezés kereshet:</span><span class="sxs-lookup"><span data-stu-id="74e31-123">And you can perform phrase searches:</span></span>

    id:"azure.storage"


<span data-ttu-id="74e31-124">A DSC-címkével ellátott összes elemek kereséséhez.</span><span class="sxs-lookup"><span data-stu-id="74e31-124">To search all items with DSC tag.</span></span>

    Tags:"DSC"

<span data-ttu-id="74e31-125">A megadott függvény összes elemek kereséséhez.</span><span class="sxs-lookup"><span data-stu-id="74e31-125">To search all items with the specified function.</span></span>

    Functions:"Update-AzureRM"

<span data-ttu-id="74e31-126">A megadott parancsmaggal minden elem kereséséhez.</span><span class="sxs-lookup"><span data-stu-id="74e31-126">To search all items with the specified cmdlet.</span></span>

    Cmdlets:"Get-AzureRmEnvironment"

<span data-ttu-id="74e31-127">A megadott nevű DSC erőforrás minden elem kereséséhez.</span><span class="sxs-lookup"><span data-stu-id="74e31-127">To search all items with the specified DSC Resource name.</span></span>

    DscResources:"xArchive"

<span data-ttu-id="74e31-128">A megadott PowerShellVersion tartalmazó összes elemek kereséséhez</span><span class="sxs-lookup"><span data-stu-id="74e31-128">To search all items with the specified PowerShellVersion</span></span>

    PowerShellVersion:"5.0"
    PowerShellVersion:"3.0"
    PowerShellVersion:"2.0"


<span data-ttu-id="74e31-129">Végül egy mező nem támogatottak, például a "parancs" használata azt fogja csak figyelmen kívül hagyja, és keresse a mezőket.</span><span class="sxs-lookup"><span data-stu-id="74e31-129">Finally, if you use a field we don't support, such as 'commands', we'll just ignore it and search all the fields.</span></span> <span data-ttu-id="74e31-130">Ezért a következő lekérdezés</span><span class="sxs-lookup"><span data-stu-id="74e31-130">So the following query</span></span>

    commands:blobs storage

<span data-ttu-id="74e31-131">Az értelmezett pontosan ugyanaz, mint ez a lekérdezés:</span><span class="sxs-lookup"><span data-stu-id="74e31-131">Is interpreted exactly the same as this query:</span></span>

    blobs storage