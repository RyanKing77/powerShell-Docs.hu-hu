---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "WMF, a powershell, a beállítása"
ms.openlocfilehash: 4fc146f84588d368ac3eb819e3acb4cb8c5d8793
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2017
---
# <a name="detailed-information-about-lcm-state"></a><span data-ttu-id="2f0f2-102">LCM állapotával kapcsolatos részletes információk</span><span class="sxs-lookup"><span data-stu-id="2f0f2-102">Detailed information about LCM state</span></span>

<span data-ttu-id="2f0f2-103">Fejlesztéseket hajtottunk kitettségének LCM állapotára vonatkozó részletek.</span><span class="sxs-lookup"><span data-stu-id="2f0f2-103">We have made improvements in exposing details about the LCM state.</span></span> <span data-ttu-id="2f0f2-104">A Get-DscLocalConfigurationManager által visszaadott LCMState most már tartalmazza a következő értékeket:</span><span class="sxs-lookup"><span data-stu-id="2f0f2-104">The LCMState that is returned by Get-DscLocalConfigurationManager can now contain the following values:</span></span>

* <span data-ttu-id="2f0f2-105">**Üresjárati**</span><span class="sxs-lookup"><span data-stu-id="2f0f2-105">**Idle**</span></span>
* <span data-ttu-id="2f0f2-106">**elfoglalt**</span><span class="sxs-lookup"><span data-stu-id="2f0f2-106">**Busy**</span></span>
* <span data-ttu-id="2f0f2-107">**PendingReboot**</span><span class="sxs-lookup"><span data-stu-id="2f0f2-107">**PendingReboot**</span></span>
* <span data-ttu-id="2f0f2-108">**PendingConfiguration**</span><span class="sxs-lookup"><span data-stu-id="2f0f2-108">**PendingConfiguration**</span></span>

<span data-ttu-id="2f0f2-109">Egy LCMStateDetail tulajdonság, amely tartalmazza a állapotával kapcsolatos további információk is jelentek meg.</span><span class="sxs-lookup"><span data-stu-id="2f0f2-109">We have also added an LCMStateDetail property that contains more information about the state.</span></span>

