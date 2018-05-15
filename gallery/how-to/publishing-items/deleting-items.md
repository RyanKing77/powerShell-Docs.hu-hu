---
ms.date: 06/12/2017
contributor: JKeithB
ms.topic: conceptual
keywords: gyűjtemény, a powershell, a parancsmag, a psgallery
title: Elemek törlése
ms.openlocfilehash: 5af66c5b7edf8f0d7049a98ed4dd10b13d4e9471
ms.sourcegitcommit: e9ad4d85fd7eb72fb5bc37f6ca3ae1282ae3c6d7
ms.contentlocale: hu-HU
ms.lasthandoff: 05/10/2018
---
# <a name="deleting-items"></a><span data-ttu-id="33615-103">Elemek törlése</span><span class="sxs-lookup"><span data-stu-id="33615-103">Deleting items</span></span>

<span data-ttu-id="33615-104">A PowerShell-galériában nem támogatja a cikkek, végleges törlését, mert, amely bárki, aki van attól függően, hogy fennmaradó rendelkezésre álló megszűnését.</span><span class="sxs-lookup"><span data-stu-id="33615-104">The PowerShell Gallery does not support permanent deletion of items, because that would break anyone who is depending on it remaining available.</span></span>

<span data-ttu-id="33615-105">A PowerShell-galériában ehelyett "unlist" elem, amely webhelyén, a cikk kezelése lapon végezhető módot támogatja.</span><span class="sxs-lookup"><span data-stu-id="33615-105">Instead, the PowerShell Gallery supports a way to 'unlist' an item, which can be done in the item management page on the web site.</span></span>
<span data-ttu-id="33615-106">Ha egy elemet fel nem sorolt, akkor nem jelenik meg a keresési és bármelyik elem listázása, mind a PowerShell-galériában és PowerShellGet-parancsok használatával.</span><span class="sxs-lookup"><span data-stu-id="33615-106">When an item is unlisted, it no longer shows up in search and in any item listing, both on the PowerShell Gallery and using PowerShellGet commands.</span></span>
<span data-ttu-id="33615-107">Azonban a maradnak letölthető a pontos verziót, amely mi lehetővé teszi, hogy a munka folytatásához automatizált parancsfájlokat megadásával.</span><span class="sxs-lookup"><span data-stu-id="33615-107">However, it remains downloadable by specifying its exact version, which is what allows the automated scripts to continue working.</span></span>

<span data-ttu-id="33615-108">Ha úgy gondolja, hogy az elemek törlése kivételes helyzet tapasztal, ha ez kezelhetik manuálisan a PowerShell-galériában csapatával.</span><span class="sxs-lookup"><span data-stu-id="33615-108">If you run into an exceptional situation where you think one of your items must be deleted, this can be handled manually by the PowerShell Gallery team.</span></span>
<span data-ttu-id="33615-109">Például ha egy szerzői jogsértéssel kapcsolatos probléma vagy potenciálisan káros tartalom, amely lehet törli-e érvényes okát.</span><span class="sxs-lookup"><span data-stu-id="33615-109">For example, if there is a copyright infringement issue, or potentially harmful content, that could be a valid reason to delete it.</span></span>
<span data-ttu-id="33615-110">Egy támogatási kérést [PowerShell-galériában] keresztül kell elküldeni (http://www.PowerShellGallery.com) ebben az esetben.</span><span class="sxs-lookup"><span data-stu-id="33615-110">You should submit a support request through [PowerShell Gallery] (http://www.PowerShellGallery.com) in that case.</span></span>