---
ms.date: 2017-06-12
contributor: JKeithB
ms.topic: conceptual
keywords: "gyűjtemény, a powershell, a parancsmag, a psgallery"
title: "Az elemek törlése"
ms.openlocfilehash: 00452f9b6625a51e95f3f46dbd66291fa20e17ad
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2017
---
# <a name="deleting-items"></a><span data-ttu-id="f43e6-103">Az elemek törlése</span><span class="sxs-lookup"><span data-stu-id="f43e6-103">Deleting items</span></span>

<span data-ttu-id="f43e6-104">A PowerShell-galériában nem támogatja a cikkek, végleges törlését, mert, amely bárki, aki van attól függően, hogy fennmaradó rendelkezésre álló megszűnését.</span><span class="sxs-lookup"><span data-stu-id="f43e6-104">The PowerShell Gallery does not support permanent deletion of items, because that would break anyone who is depending on it remaining available.</span></span>

<span data-ttu-id="f43e6-105">A PowerShell-galériában ehelyett "unlist" elem, amely webhelyén, a cikk kezelése lapon végezhető módot támogatja.</span><span class="sxs-lookup"><span data-stu-id="f43e6-105">Instead, the PowerShell Gallery supports a way to 'unlist' an item, which can be done in the item management page on the web site.</span></span> <span data-ttu-id="f43e6-106">Ha egy elemet fel nem sorolt, akkor nem jelenik meg a keresési és bármelyik elem listázása, mind a PowerShell-galériában és PowerShellGet-parancsok használatával.</span><span class="sxs-lookup"><span data-stu-id="f43e6-106">When an item is unlisted, it no longer shows up in search and in any item listing, both on the PowerShell Gallery and using PowerShellGet commands.</span></span> <span data-ttu-id="f43e6-107">Azonban a maradnak letölthető a pontos verziót, amely mi lehetővé teszi, hogy a munka folytatásához automatizált parancsfájlokat megadásával.</span><span class="sxs-lookup"><span data-stu-id="f43e6-107">However, it remains downloadable by specifying its exact version, which is what allows the automated scripts to continue working.</span></span>

<span data-ttu-id="f43e6-108">Ha úgy gondolja, hogy az elemek törlése kivételes helyzet tapasztal, ha ez kezelhetik manuálisan a PowerShell-galériában csapatával.</span><span class="sxs-lookup"><span data-stu-id="f43e6-108">If you run into an exceptional situation where you think one of your items must be deleted, this can be handled manually by the PowerShell Gallery team.</span></span> <span data-ttu-id="f43e6-109">Például ha egy szerzői jogsértéssel kapcsolatos probléma vagy potenciálisan káros tartalom, amely lehet törli-e érvényes okát.</span><span class="sxs-lookup"><span data-stu-id="f43e6-109">For example, if there is a copyright infringement issue, or potentially harmful content, that could be a valid reason to delete it.</span></span> <span data-ttu-id="f43e6-110">Ebben az esetben egy támogatási kérést [PowerShell-galériában] (http://www.PowerShellGallery.com) keresztül kell elküldeni.</span><span class="sxs-lookup"><span data-stu-id="f43e6-110">You should submit a support request through [PowerShell Gallery] (http://www.PowerShellGallery.com) in that case.</span></span>

