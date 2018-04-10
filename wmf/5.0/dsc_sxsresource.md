---
ms.date: 06/12/2017
author: JKeithB
ms.topic: reference
keywords: WMF, powershell, beállítás
ms.openlocfilehash: a565f2befddc32f5088fa3e158f58d2dd78d41b4
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="side-by-side-module-versioning-support-for-dsc-resources"></a><span data-ttu-id="81d22-102">A DSC-erőforrások párhuzamos modul Versioning támogatása</span><span class="sxs-lookup"><span data-stu-id="81d22-102">Side-By-Side Module Versioning Support for DSC Resources</span></span>

<span data-ttu-id="81d22-103">Modulok tartalmazó DSC-erőforrások lehetnek egymás melletti telepítve, és a DSC-konfigurációk használhatja az erőforrást, amelyre telepítve van a rendszeren egy adott verziójához.</span><span class="sxs-lookup"><span data-stu-id="81d22-103">Modules containing DSC resources can be installed side-by-side, and DSC configurations can use a specific version of the resource that is installed on the system.</span></span>

<span data-ttu-id="81d22-104">További információkért lásd: [erőforrásokat használó többféle verzióját tartalmazó](https://msdn.microsoft.com/powershell/dsc/sxsresource).</span><span class="sxs-lookup"><span data-stu-id="81d22-104">For more information, see [Using resources with multiple versions](https://msdn.microsoft.com/powershell/dsc/sxsresource).</span></span>

## <a name="known-issues"></a><span data-ttu-id="81d22-105">Ismert problémák</span><span class="sxs-lookup"><span data-stu-id="81d22-105">Known issues</span></span>

<span data-ttu-id="81d22-106">Ebben a kiadásban a következő ismert problémákat olvashatja egymás melletti telepítés:</span><span class="sxs-lookup"><span data-stu-id="81d22-106">In this release, the following are known issues of side-by-side installation:</span></span>

-   <span data-ttu-id="81d22-107">A DSC-erőforrás belül ugyanaz a konfiguráció két különböző verzióinak használata nem támogatott.</span><span class="sxs-lookup"><span data-stu-id="81d22-107">Using two different versions of the DSC resource within the same configuration is not supported.</span></span>