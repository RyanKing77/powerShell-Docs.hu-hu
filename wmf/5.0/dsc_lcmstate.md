---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: 57152e9f62c34600df63a2db8e9683928e825d93
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62085796"
---
# <a name="detailed-information-about-lcm-state"></a><span data-ttu-id="69895-102">Az LCM állapotának részletes adatai</span><span class="sxs-lookup"><span data-stu-id="69895-102">Detailed information about LCM state</span></span>

<span data-ttu-id="69895-103">Fejlesztéseket hajtottunk is közzéteheti az LCM állapotának részleteit.</span><span class="sxs-lookup"><span data-stu-id="69895-103">We have made improvements in exposing details about the LCM state.</span></span> <span data-ttu-id="69895-104">A Get-DscLocalConfigurationManager által visszaadott LCMState mostantól tartalmazza a következő értékeket:</span><span class="sxs-lookup"><span data-stu-id="69895-104">The LCMState that is returned by Get-DscLocalConfigurationManager can now contain the following values:</span></span>

* <span data-ttu-id="69895-105">**Inaktív**</span><span class="sxs-lookup"><span data-stu-id="69895-105">**Idle**</span></span>
* <span data-ttu-id="69895-106">**elfoglalt**</span><span class="sxs-lookup"><span data-stu-id="69895-106">**Busy**</span></span>
* <span data-ttu-id="69895-107">**PendingReboot**</span><span class="sxs-lookup"><span data-stu-id="69895-107">**PendingReboot**</span></span>
* <span data-ttu-id="69895-108">**PendingConfiguration**</span><span class="sxs-lookup"><span data-stu-id="69895-108">**PendingConfiguration**</span></span>

<span data-ttu-id="69895-109">Bővítettük egy LCMStateDetail tulajdonsággal, amely tartalmazza az állam bővebben is.</span><span class="sxs-lookup"><span data-stu-id="69895-109">We have also added an LCMStateDetail property that contains more information about the state.</span></span>
