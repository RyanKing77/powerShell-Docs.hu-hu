---
ms.date: 06/12/2017
contributor: JKeithB
keywords: katalógus, a powershell, a parancsmag, a psgallery
title: Csomagok törlésével
ms.openlocfilehash: ca5e68fcad52e4c7561d2c2b3858228652f22e0b
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62084164"
---
# <a name="deleting-packages"></a><span data-ttu-id="117ab-103">Csomagok törlése</span><span class="sxs-lookup"><span data-stu-id="117ab-103">Deleting Packages</span></span>

<span data-ttu-id="117ab-104">A PowerShell-galériából nem támogatja a végleges törlés csomagok, mert, amely megtörnék bárki, aki attól függően, a fennmaradó rendelkezésre álló.</span><span class="sxs-lookup"><span data-stu-id="117ab-104">The PowerShell Gallery does not support permanent deletion of packages, because that would break anyone who is depending on it remaining available.</span></span>

<span data-ttu-id="117ab-105">Ehelyett a PowerShell-galériából támogatja olyan módon, a "unlist" egy csomagot, amely a csomag kezelése lap a webhelyen teheti meg.</span><span class="sxs-lookup"><span data-stu-id="117ab-105">Instead, the PowerShell Gallery supports a way to 'unlist' a package, which can be done in the package management page on the web site.</span></span>
<span data-ttu-id="117ab-106">Ha egy csomag fel nem sorolt, már nem megjelenik a keresési és minden olyan csomag, listázása, a PowerShell-galériából egyaránt, és a PowerShellGet-parancsokkal.</span><span class="sxs-lookup"><span data-stu-id="117ab-106">When a package is unlisted, it no longer shows up in search and in any package listing, both on the PowerShell Gallery and using PowerShellGet commands.</span></span>
<span data-ttu-id="117ab-107">Azonban továbbra is letölthető a pontos verziót, amely a munka folytatásához automatizált parancsfájlokat teszi megadásával.</span><span class="sxs-lookup"><span data-stu-id="117ab-107">However, it remains downloadable by specifying its exact version, which is what allows the automated scripts to continue working.</span></span>

<span data-ttu-id="117ab-108">Ha egy kivételes helyzet, ha úgy gondolja, hogy a csomagok egyik törölni kell, ez lehet kezelni, manuálisan a PowerShell-galériából csapat.</span><span class="sxs-lookup"><span data-stu-id="117ab-108">If you run into an exceptional situation where you think one of your packages must be deleted, this can be handled manually by the PowerShell Gallery team.</span></span>
<span data-ttu-id="117ab-109">Például ha a szerzői jogsértés probléma vagy potenciálisan káros tartalmat, amely lehet törli-e érvényes okát.</span><span class="sxs-lookup"><span data-stu-id="117ab-109">For example, if there is a copyright infringement issue, or potentially harmful content, that could be a valid reason to delete it.</span></span>
<span data-ttu-id="117ab-110">Küldjön egy támogatási kérést [PowerShell-galériából](http://www.PowerShellGallery.com) ebben az esetben.</span><span class="sxs-lookup"><span data-stu-id="117ab-110">You should submit a support request through [PowerShell Gallery](http://www.PowerShellGallery.com) in that case.</span></span>
