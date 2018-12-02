---
ms.date: 06/12/2017
contributor: JKeithB
keywords: katalógus, a powershell, a parancsmag, a psgallery
title: Katalóguskeresési szintaxis
ms.openlocfilehash: aabcaa1f1b5b641ab5033c9ba2e358477c84a23b
ms.sourcegitcommit: e24525046dd37166b9d83eeecdc534726316f429
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/01/2018
ms.locfileid: "52742856"
---
# <a name="gallery-search-syntax"></a><span data-ttu-id="5cd2c-103">Katalóguskeresési szintaxis</span><span class="sxs-lookup"><span data-stu-id="5cd2c-103">Gallery Search Syntax</span></span>

<span data-ttu-id="5cd2c-104">A PowerShell-galériából használatával kereshet a [PowerShell-galériából webhely](https://www.powershellgallery.com/).</span><span class="sxs-lookup"><span data-stu-id="5cd2c-104">You can search the PowerShell Gallery using the [PowerShell Gallery's web site](https://www.powershellgallery.com/).</span></span>
<span data-ttu-id="5cd2c-105">PowerShell-galériából webhely kínál egy szöveges searchbox, ahol szavak, kifejezéseket és kulcsszó kifejezések használhatja meg a keresési eredmények szűkítéséhez.</span><span class="sxs-lookup"><span data-stu-id="5cd2c-105">PowerShell Gallery web site offers a text searchbox where you can use words, phrases and keyword expressions to narrow down search results.</span></span>

## <a name="search-by-keywords"></a><span data-ttu-id="5cd2c-106">Keresés kulcsszavak szerint</span><span class="sxs-lookup"><span data-stu-id="5cd2c-106">Search by Keywords</span></span>

    dsc azure sql

<span data-ttu-id="5cd2c-107">Keresési megpróbálja megkeresni a megfelelő, az összes 3 kulcsszavakat tartalmazó dokumentumok, és megfelelő dokumentumokat.</span><span class="sxs-lookup"><span data-stu-id="5cd2c-107">Search attempts to find relevant documents containing all 3 keywords, and return matching documents.</span></span>

## <a name="search-using-phrases-and-keywords"></a><span data-ttu-id="5cd2c-108">Mondatok és a kulcsszavak keresése</span><span class="sxs-lookup"><span data-stu-id="5cd2c-108">Search using Phrases and keywords</span></span>

    "azure sql" deployment

<span data-ttu-id="5cd2c-109">Írja be egy kifejezést idézőjelek között ("") módosítsa a keresési, keresse meg az adott kifejezést külön kulcsszavak helyett.</span><span class="sxs-lookup"><span data-stu-id="5cd2c-109">Entering a phrase between quotation marks ("") change the search to look for the particular phrase instead of separate keywords.</span></span>
<span data-ttu-id="5cd2c-110">Egyező dokumentumok általában tartalmaznia kell a pontos kifejezés "az azure sql", így például a kis-és nagybetűk változata "Az azure SQL", és a "telepítés" szó általában is tartalmaznak.</span><span class="sxs-lookup"><span data-stu-id="5cd2c-110">Matching documents should usually contain the exact phrase "azure sql", including variations on capitalization e.g. "Azure SQL", and also usually contain the word 'deployment'.</span></span>

## <a name="filtering-on-fields"></a><span data-ttu-id="5cd2c-111">A mezők szűrése</span><span class="sxs-lookup"><span data-stu-id="5cd2c-111">Filtering on fields</span></span>

<span data-ttu-id="5cd2c-112">Kereshet egy adott csomag azonosítója (vagy "Id" vagy "id"), vagy bizonyos más mezők illesztésével keresse a mező nevét a kifejezéseket.</span><span class="sxs-lookup"><span data-stu-id="5cd2c-112">You can search for a specific package ID (or 'Id' or 'id'), or certain other fields by prefixing search terms with the field name.</span></span>

<span data-ttu-id="5cd2c-113">A kereshető mezők jelenleg "Id", "Verziójú", "Címke", "Szerző", "Tulajdonos", "Függvények", 'Parancsmagok', "DscResources" és "PowerShellVersion".</span><span class="sxs-lookup"><span data-stu-id="5cd2c-113">Currently the searchable fields are 'Id', 'Version', 'Tags', 'Author', 'Owner', 'Functions', 'Cmdlets', 'DscResources' and 'PowerShellVersion'.</span></span>

<span data-ttu-id="5cd2c-114">[Mi a különbség a között Azonosítóját és címét?</span><span class="sxs-lookup"><span data-stu-id="5cd2c-114">[What's the difference between ID and Title?</span></span> <span data-ttu-id="5cd2c-115">ID az a név, használja a konzolon.</span><span class="sxs-lookup"><span data-stu-id="5cd2c-115">ID is the name you use in the console.</span></span> <span data-ttu-id="5cd2c-116">Cím értéke: Mi látható az oldal felső részén található a csomagot a keresési eredmények között.]</span><span class="sxs-lookup"><span data-stu-id="5cd2c-116">Title is what is shown at the top of the package page in search results.]</span></span>

## <a name="examples"></a><span data-ttu-id="5cd2c-117">Példák</span><span class="sxs-lookup"><span data-stu-id="5cd2c-117">Examples</span></span>

    ID:PSReadline
    
<span data-ttu-id="5cd2c-118">megtalálja a csomagokat tartalmazó "PSReadline" azonosítóval.</span><span class="sxs-lookup"><span data-stu-id="5cd2c-118">finds packages with an ID containing "PSReadline".</span></span>

    Id:"AzureRM.Profile"

<span data-ttu-id="5cd2c-119">az azonosító mezőben keresse meg a csomagokat az "AzureRM.Profile" egy másik módja van.</span><span class="sxs-lookup"><span data-stu-id="5cd2c-119">is another way to find packages with "AzureRM.Profile" in their ID field.</span></span>

<span data-ttu-id="5cd2c-120">Az "Id" szűrő abban az esetben egy karakterláncrészletet egyeznek, így ha, keresse meg a következő:</span><span class="sxs-lookup"><span data-stu-id="5cd2c-120">The 'Id' filter is a substring match, so if you search for the following:</span></span>

    Id:"azure"

<span data-ttu-id="5cd2c-121">Ez biztosítja, hogy eredmények, amelyek tartalmazzák az AzureRM.Profile "és"Azure.Storage".</span><span class="sxs-lookup"><span data-stu-id="5cd2c-121">This provides results that include AzureRM.Profile' and 'Azure.Storage'.</span></span>

<span data-ttu-id="5cd2c-122">Egyetlen mezőben több kulcsszavak alapján is kereshet.</span><span class="sxs-lookup"><span data-stu-id="5cd2c-122">You can also search for multiple keywords in a single field.</span></span> 

    id:azure tags:intellisense

<span data-ttu-id="5cd2c-123">És kifejezés kereshet idézőjelek használata:</span><span class="sxs-lookup"><span data-stu-id="5cd2c-123">And you can perform phrase searches using double quotes:</span></span>

    id:"azure.storage"

<span data-ttu-id="5cd2c-124">DSC-címkével ellátott összes csomagok keresése.</span><span class="sxs-lookup"><span data-stu-id="5cd2c-124">To search all packages with DSC tag.</span></span>

    Tags:DSC

<span data-ttu-id="5cd2c-125">Keresés a megadott függvény az összes csomagot.</span><span class="sxs-lookup"><span data-stu-id="5cd2c-125">To search all packages with the specified function.</span></span>

    Functions:Get-TreeSize

<span data-ttu-id="5cd2c-126">Keresés a megadott parancsmag az összes csomagot.</span><span class="sxs-lookup"><span data-stu-id="5cd2c-126">To search all packages with the specified cmdlet.</span></span>

    Cmdlets:Get-AzureRmEnvironment

<span data-ttu-id="5cd2c-127">Keresés az összes csomag DSC erőforrás a megadott névvel.</span><span class="sxs-lookup"><span data-stu-id="5cd2c-127">To search all packages with the specified DSC Resource name.</span></span>

    DscResources:xArchive

<span data-ttu-id="5cd2c-128">A megadott PowerShellVersion az összes csomag keresése</span><span class="sxs-lookup"><span data-stu-id="5cd2c-128">To search all packages with the specified PowerShellVersion</span></span>

    PowerShellVersion:2.0

<span data-ttu-id="5cd2c-129">Végül ha egy mező nem támogatjuk, például a "parancs", azt fogja csak figyelmen kívül hagyhatja azt és a Keresés az összes mezőt.</span><span class="sxs-lookup"><span data-stu-id="5cd2c-129">Finally, if you use a field we don't support, such as 'commands', we'll just ignore it and search all the fields.</span></span> <span data-ttu-id="5cd2c-130">Ezért a következő lekérdezést</span><span class="sxs-lookup"><span data-stu-id="5cd2c-130">So the following query</span></span>

    commands:blobs storage

<span data-ttu-id="5cd2c-131">Az értelmezett pontosan ugyanaz, mint ez a lekérdezés:</span><span class="sxs-lookup"><span data-stu-id="5cd2c-131">Is interpreted exactly the same as this query:</span></span>

    blobs storage
