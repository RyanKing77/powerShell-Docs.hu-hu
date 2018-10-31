---
ms.date: 06/12/2017
contributor: JKeithB
keywords: katalógus, a powershell, a parancsmag, a psgallery
title: Csomagok törlésével
ms.openlocfilehash: ca5e68fcad52e4c7561d2c2b3858228652f22e0b
ms.sourcegitcommit: 98b7cfd8ad5718efa8e320526ca76c3cc4141d78
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/25/2018
ms.locfileid: "50004119"
---
# <a name="deleting-packages"></a><span data-ttu-id="8fa61-103">Csomagok törlésével</span><span class="sxs-lookup"><span data-stu-id="8fa61-103">Deleting Packages</span></span>

<span data-ttu-id="8fa61-104">A PowerShell-galériából nem támogatja a végleges törlés csomagok, mert, amely megtörnék bárki, aki attól függően, a fennmaradó rendelkezésre álló.</span><span class="sxs-lookup"><span data-stu-id="8fa61-104">The PowerShell Gallery does not support permanent deletion of packages, because that would break anyone who is depending on it remaining available.</span></span>

<span data-ttu-id="8fa61-105">Ehelyett a PowerShell-galériából támogatja olyan módon, a "unlist" egy csomagot, amely a csomag kezelése lap a webhelyen teheti meg.</span><span class="sxs-lookup"><span data-stu-id="8fa61-105">Instead, the PowerShell Gallery supports a way to 'unlist' a package, which can be done in the package management page on the web site.</span></span>
<span data-ttu-id="8fa61-106">Ha egy csomag fel nem sorolt, már nem megjelenik a keresési és minden olyan csomag, listázása, a PowerShell-galériából egyaránt, és a PowerShellGet-parancsokkal.</span><span class="sxs-lookup"><span data-stu-id="8fa61-106">When a package is unlisted, it no longer shows up in search and in any package listing, both on the PowerShell Gallery and using PowerShellGet commands.</span></span>
<span data-ttu-id="8fa61-107">Azonban továbbra is letölthető a pontos verziót, amely a munka folytatásához automatizált parancsfájlokat teszi megadásával.</span><span class="sxs-lookup"><span data-stu-id="8fa61-107">However, it remains downloadable by specifying its exact version, which is what allows the automated scripts to continue working.</span></span>

<span data-ttu-id="8fa61-108">Ha egy kivételes helyzet, ha úgy gondolja, hogy a csomagok egyik törölni kell, ez lehet kezelni, manuálisan a PowerShell-galériából csapat.</span><span class="sxs-lookup"><span data-stu-id="8fa61-108">If you run into an exceptional situation where you think one of your packages must be deleted, this can be handled manually by the PowerShell Gallery team.</span></span>
<span data-ttu-id="8fa61-109">Például ha a szerzői jogsértés probléma vagy potenciálisan káros tartalmat, amely lehet törli-e érvényes okát.</span><span class="sxs-lookup"><span data-stu-id="8fa61-109">For example, if there is a copyright infringement issue, or potentially harmful content, that could be a valid reason to delete it.</span></span>
<span data-ttu-id="8fa61-110">Küldjön egy támogatási kérést [PowerShell-galériából](http://www.PowerShellGallery.com) ebben az esetben.</span><span class="sxs-lookup"><span data-stu-id="8fa61-110">You should submit a support request through [PowerShell Gallery](http://www.PowerShellGallery.com) in that case.</span></span>
