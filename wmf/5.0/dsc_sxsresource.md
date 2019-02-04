---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: 5b31fe833fb0f9d0f3f2733e777e4608a697d583
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55685633"
---
# <a name="side-by-side-module-versioning-support-for-dsc-resources"></a><span data-ttu-id="e97fc-102">Egymás melletti modul verziószámozás támogatása a DSC-erőforrásokhoz</span><span class="sxs-lookup"><span data-stu-id="e97fc-102">Side-By-Side Module Versioning Support for DSC Resources</span></span>

<span data-ttu-id="e97fc-103">A modulok DSC-erőforrásokat tartalmazó lehet telepítve egymás mellett, és a DSC-konfigurációk használhatja az erőforrást, amelyre telepítve van a rendszeren egy adott verzióját.</span><span class="sxs-lookup"><span data-stu-id="e97fc-103">Modules containing DSC resources can be installed side-by-side, and DSC configurations can use a specific version of the resource that is installed on the system.</span></span>

<span data-ttu-id="e97fc-104">További információkért lásd: [eltérő verziójú erőforrások használata](https://msdn.microsoft.com/powershell/dsc/sxsresource).</span><span class="sxs-lookup"><span data-stu-id="e97fc-104">For more information, see [Using resources with multiple versions](https://msdn.microsoft.com/powershell/dsc/sxsresource).</span></span>

## <a name="known-issues"></a><span data-ttu-id="e97fc-105">Ismert problémák</span><span class="sxs-lookup"><span data-stu-id="e97fc-105">Known issues</span></span>

<span data-ttu-id="e97fc-106">Ebben a kiadásban a következő ismert problémák egymás melletti telepítés:</span><span class="sxs-lookup"><span data-stu-id="e97fc-106">In this release, the following are known issues of side-by-side installation:</span></span>

-   <span data-ttu-id="e97fc-107">Két különböző verzióit a DSC-erőforrás belül ugyanaz a konfiguráció használata nem támogatott.</span><span class="sxs-lookup"><span data-stu-id="e97fc-107">Using two different versions of the DSC resource within the same configuration is not supported.</span></span>
