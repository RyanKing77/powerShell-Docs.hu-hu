---
ms.date: 06/12/2017
contributor: JKeithB
keywords: katalógus, a powershell, a parancsmag, a psgallery
title: Katalóguskeresési szintaxis
ms.openlocfilehash: 9aadb6771c85845cc3fa05cb56f0194b060d1c1b
ms.sourcegitcommit: 98b7cfd8ad5718efa8e320526ca76c3cc4141d78
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/25/2018
ms.locfileid: "50004078"
---
# <a name="gallery-search-syntax"></a><span data-ttu-id="0d280-103">Katalóguskeresési szintaxis</span><span class="sxs-lookup"><span data-stu-id="0d280-103">Gallery Search Syntax</span></span>

<span data-ttu-id="0d280-104">PowerShell-galériából kínál egy szöveges searchbox, ahol szavak, kifejezéseket és kulcsszó kifejezések használhatja meg a keresési eredmények szűkítéséhez.</span><span class="sxs-lookup"><span data-stu-id="0d280-104">PowerShell Gallery offers a text searchbox where you can use words, phrases and keyword expressions to narrow down search results.</span></span>

## <a name="search-by-keywords"></a><span data-ttu-id="0d280-105">Keresés kulcsszavak szerint</span><span class="sxs-lookup"><span data-stu-id="0d280-105">Search by Keywords</span></span>

    dsc azure sql

<span data-ttu-id="0d280-106">Keresés hajtsa végre az ajánlott annak érdekében, hogy az összes 3 kulcsszavakat tartalmazó megfelelő dokumentumok keresése, és megfelelő dokumentumokat.</span><span class="sxs-lookup"><span data-stu-id="0d280-106">Search will do its best effort to find relevant documents containing all 3 keywords, and return matching documents.</span></span>

## <a name="search-using-phrases-and-keywords"></a><span data-ttu-id="0d280-107">Mondatok és a kulcsszavak keresése</span><span class="sxs-lookup"><span data-stu-id="0d280-107">Search using Phrases and keywords</span></span>

    "azure sql" deployment

<span data-ttu-id="0d280-108">Írja be egy kifejezést idézőjelek között ("") módosítsa a keresési, keresse meg az adott kifejezést külön kulcsszavak helyett.</span><span class="sxs-lookup"><span data-stu-id="0d280-108">Entering a phrase between quotation marks ("") change the search to look for the particular phrase instead of separate keywords.</span></span>
<span data-ttu-id="0d280-109">Egyező dokumentumok általában tartalmaznia kell a pontos kifejezés "az azure sql", így például a kis-és nagybetűk változata "Az azure SQL", és a "telepítés" szó általában is tartalmaznak.</span><span class="sxs-lookup"><span data-stu-id="0d280-109">Matching documents should usually contain the exact phrase "azure sql", including variations on capitalization e.g. "Azure SQL", and also usually contain the word 'deployment'.</span></span>

## <a name="filtering-on-fields"></a><span data-ttu-id="0d280-110">A mezők szűrése</span><span class="sxs-lookup"><span data-stu-id="0d280-110">Filtering on fields</span></span>

<span data-ttu-id="0d280-111">Kereshet egy adott csomag azonosítója (vagy "Id" vagy "id"), vagy bizonyos más mezők illesztésével keresse a mező nevét a kifejezéseket.</span><span class="sxs-lookup"><span data-stu-id="0d280-111">You can search for a specific package ID (or 'Id' or 'id'), or certain other fields by prefixing search terms with the field name.</span></span>

<span data-ttu-id="0d280-112">A kereshető mezők jelenleg "Id", "Verziójú", "Címke", "Szerző", "Tulajdonos", "Függvények", 'Parancsmagok', "DscResources" és "PowerShellVersion".</span><span class="sxs-lookup"><span data-stu-id="0d280-112">Currently the searchable fields are 'Id', 'Version', 'Tags', 'Author', 'Owner', 'Functions', 'Cmdlets', 'DscResources' and 'PowerShellVersion'.</span></span>

<span data-ttu-id="0d280-113">[Mi a különbség a között Azonosítóját és címét?</span><span class="sxs-lookup"><span data-stu-id="0d280-113">[What's the difference between ID and Title?</span></span> <span data-ttu-id="0d280-114">ID az a név, használja a konzolon.</span><span class="sxs-lookup"><span data-stu-id="0d280-114">ID is the name you use in the console.</span></span> <span data-ttu-id="0d280-115">Cím értéke: Mi látható az oldal felső részén található a csomagot a keresési eredmények között.]</span><span class="sxs-lookup"><span data-stu-id="0d280-115">Title is what is shown at the top of the package page in search results.]</span></span>

## <a name="examples"></a><span data-ttu-id="0d280-116">Példák</span><span class="sxs-lookup"><span data-stu-id="0d280-116">Examples</span></span>

    ID:"PSReadline"
    id:"AzureRM.Profile"

<span data-ttu-id="0d280-117">megtalálja a csomagokat az "PSReadline" vagy "AzureRM.Profile" az azonosító mezőben jelölik.</span><span class="sxs-lookup"><span data-stu-id="0d280-117">finds packages with "PSReadline" or "AzureRM.Profile" in their ID field respectively.</span></span>

    Id:"AzureRM.Profile"

<span data-ttu-id="0d280-118">az azonosító mezőben keresse meg a csomagokat az "AzureRM.Profile" egy másik módja van.</span><span class="sxs-lookup"><span data-stu-id="0d280-118">is another way to find packages with "AzureRM.Profile" in their ID field.</span></span>

<span data-ttu-id="0d280-119">Az "Id" szűrő abban az esetben egy karakterláncrészletet egyeznek, így ha, keresse meg a következő:</span><span class="sxs-lookup"><span data-stu-id="0d280-119">The 'Id' filter is a substring match, so if you search for the following:</span></span>

    Id:"azure"

<span data-ttu-id="0d280-120">Például a "AzureRM.Profile" és "Azure.Storage" eredményt fog kapni.</span><span class="sxs-lookup"><span data-stu-id="0d280-120">You'll get results like 'AzureRM.Profile' and 'Azure.Storage'.</span></span>

<span data-ttu-id="0d280-121">Egyetlen mezőben több kulcsszavak alapján is kereshet.</span><span class="sxs-lookup"><span data-stu-id="0d280-121">You can also search for multiple keywords in a single field.</span></span> <span data-ttu-id="0d280-122">Vagy keverheti a mezőket.</span><span class="sxs-lookup"><span data-stu-id="0d280-122">Or mix and match fields.</span></span>

    id:azure tags:intellisense
    id:azure id:storage

<span data-ttu-id="0d280-123">És kifejezés kereshet:</span><span class="sxs-lookup"><span data-stu-id="0d280-123">And you can perform phrase searches:</span></span>

    id:"azure.storage"


<span data-ttu-id="0d280-124">DSC-címkével ellátott összes csomagok keresése.</span><span class="sxs-lookup"><span data-stu-id="0d280-124">To search all packages with DSC tag.</span></span>

    Tags:"DSC"

<span data-ttu-id="0d280-125">Keresés a megadott függvény az összes csomagot.</span><span class="sxs-lookup"><span data-stu-id="0d280-125">To search all packages with the specified function.</span></span>

    Functions:"Update-AzureRM"

<span data-ttu-id="0d280-126">Keresés a megadott parancsmag az összes csomagot.</span><span class="sxs-lookup"><span data-stu-id="0d280-126">To search all packages with the specified cmdlet.</span></span>

    Cmdlets:"Get-AzureRmEnvironment"

<span data-ttu-id="0d280-127">Keresés az összes csomag DSC erőforrás a megadott névvel.</span><span class="sxs-lookup"><span data-stu-id="0d280-127">To search all packages with the specified DSC Resource name.</span></span>

    DscResources:"xArchive"

<span data-ttu-id="0d280-128">A megadott PowerShellVersion az összes csomag keresése</span><span class="sxs-lookup"><span data-stu-id="0d280-128">To search all packages with the specified PowerShellVersion</span></span>

    PowerShellVersion:"5.0"
    PowerShellVersion:"3.0"
    PowerShellVersion:"2.0"


<span data-ttu-id="0d280-129">Végül ha egy mező nem támogatjuk, például a "parancs", azt fogja csak figyelmen kívül hagyhatja azt és a Keresés az összes mezőt.</span><span class="sxs-lookup"><span data-stu-id="0d280-129">Finally, if you use a field we don't support, such as 'commands', we'll just ignore it and search all the fields.</span></span> <span data-ttu-id="0d280-130">Ezért a következő lekérdezést</span><span class="sxs-lookup"><span data-stu-id="0d280-130">So the following query</span></span>

    commands:blobs storage

<span data-ttu-id="0d280-131">Az értelmezett pontosan ugyanaz, mint ez a lekérdezés:</span><span class="sxs-lookup"><span data-stu-id="0d280-131">Is interpreted exactly the same as this query:</span></span>

    blobs storage
