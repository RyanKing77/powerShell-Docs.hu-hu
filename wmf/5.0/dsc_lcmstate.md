---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: db9b48c188b3bfe2e20c06875606a285922f55a6
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/17/2018
ms.locfileid: "34219861"
---
# <a name="detailed-information-about-lcm-state"></a><span data-ttu-id="5b61d-102">LCM állapotával kapcsolatos részletes információk</span><span class="sxs-lookup"><span data-stu-id="5b61d-102">Detailed information about LCM state</span></span>

<span data-ttu-id="5b61d-103">Fejlesztéseket hajtottunk kitettségének LCM állapotára vonatkozó részletek.</span><span class="sxs-lookup"><span data-stu-id="5b61d-103">We have made improvements in exposing details about the LCM state.</span></span> <span data-ttu-id="5b61d-104">A Get-DscLocalConfigurationManager által visszaadott LCMState most már tartalmazza a következő értékeket:</span><span class="sxs-lookup"><span data-stu-id="5b61d-104">The LCMState that is returned by Get-DscLocalConfigurationManager can now contain the following values:</span></span>

* <span data-ttu-id="5b61d-105">**Üresjárati**</span><span class="sxs-lookup"><span data-stu-id="5b61d-105">**Idle**</span></span>
* <span data-ttu-id="5b61d-106">**elfoglalt**</span><span class="sxs-lookup"><span data-stu-id="5b61d-106">**Busy**</span></span>
* <span data-ttu-id="5b61d-107">**PendingReboot**</span><span class="sxs-lookup"><span data-stu-id="5b61d-107">**PendingReboot**</span></span>
* <span data-ttu-id="5b61d-108">**PendingConfiguration**</span><span class="sxs-lookup"><span data-stu-id="5b61d-108">**PendingConfiguration**</span></span>

<span data-ttu-id="5b61d-109">Egy LCMStateDetail tulajdonság, amely tartalmazza a állapotával kapcsolatos további információk is jelentek meg.</span><span class="sxs-lookup"><span data-stu-id="5b61d-109">We have also added an LCMStateDetail property that contains more information about the state.</span></span>
