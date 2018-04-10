---
ms.date: 06/12/2017
author: JKeithB
ms.topic: reference
keywords: WMF, powershell, beállítás
ms.openlocfilehash: baa35e9acd24d6f6155acf617a0d2c2210742af7
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="detailed-information-about-lcm-state"></a><span data-ttu-id="121a1-102">LCM állapotával kapcsolatos részletes információk</span><span class="sxs-lookup"><span data-stu-id="121a1-102">Detailed information about LCM state</span></span>

<span data-ttu-id="121a1-103">Fejlesztéseket hajtottunk kitettségének LCM állapotára vonatkozó részletek.</span><span class="sxs-lookup"><span data-stu-id="121a1-103">We have made improvements in exposing details about the LCM state.</span></span> <span data-ttu-id="121a1-104">A Get-DscLocalConfigurationManager által visszaadott LCMState most már tartalmazza a következő értékeket:</span><span class="sxs-lookup"><span data-stu-id="121a1-104">The LCMState that is returned by Get-DscLocalConfigurationManager can now contain the following values:</span></span>

* <span data-ttu-id="121a1-105">**Üresjárati**</span><span class="sxs-lookup"><span data-stu-id="121a1-105">**Idle**</span></span>
* <span data-ttu-id="121a1-106">**Busy**</span><span class="sxs-lookup"><span data-stu-id="121a1-106">**Busy**</span></span>
* <span data-ttu-id="121a1-107">**PendingReboot**</span><span class="sxs-lookup"><span data-stu-id="121a1-107">**PendingReboot**</span></span>
* <span data-ttu-id="121a1-108">**PendingConfiguration**</span><span class="sxs-lookup"><span data-stu-id="121a1-108">**PendingConfiguration**</span></span>

<span data-ttu-id="121a1-109">Egy LCMStateDetail tulajdonság, amely tartalmazza a állapotával kapcsolatos további információk is jelentek meg.</span><span class="sxs-lookup"><span data-stu-id="121a1-109">We have also added an LCMStateDetail property that contains more information about the state.</span></span>