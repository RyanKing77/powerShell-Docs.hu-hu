---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: 0543afbc72148b1ba713e59655126c069b16ef33
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/17/2018
---
# <a name="side-by-side-module-versioning-support-for-dsc-resources"></a><span data-ttu-id="851b9-102">A DSC-erőforrások párhuzamos modul Versioning támogatása</span><span class="sxs-lookup"><span data-stu-id="851b9-102">Side-By-Side Module Versioning Support for DSC Resources</span></span>

<span data-ttu-id="851b9-103">Modulok tartalmazó DSC-erőforrások lehetnek egymás melletti telepítve, és a DSC-konfigurációk használhatja az erőforrást, amelyre telepítve van a rendszeren egy adott verziójához.</span><span class="sxs-lookup"><span data-stu-id="851b9-103">Modules containing DSC resources can be installed side-by-side, and DSC configurations can use a specific version of the resource that is installed on the system.</span></span>

<span data-ttu-id="851b9-104">További információkért lásd: [erőforrásokat használó többféle verzióját tartalmazó](https://msdn.microsoft.com/powershell/dsc/sxsresource).</span><span class="sxs-lookup"><span data-stu-id="851b9-104">For more information, see [Using resources with multiple versions](https://msdn.microsoft.com/powershell/dsc/sxsresource).</span></span>

## <a name="known-issues"></a><span data-ttu-id="851b9-105">Ismert problémák</span><span class="sxs-lookup"><span data-stu-id="851b9-105">Known issues</span></span>

<span data-ttu-id="851b9-106">Ebben a kiadásban a következő ismert problémákat olvashatja egymás melletti telepítés:</span><span class="sxs-lookup"><span data-stu-id="851b9-106">In this release, the following are known issues of side-by-side installation:</span></span>

-   <span data-ttu-id="851b9-107">A DSC-erőforrás belül ugyanaz a konfiguráció két különböző verzióinak használata nem támogatott.</span><span class="sxs-lookup"><span data-stu-id="851b9-107">Using two different versions of the DSC resource within the same configuration is not supported.</span></span>
