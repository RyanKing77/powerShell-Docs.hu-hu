---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: 42f323590609319388e9a0a2c7c305dfa80c2d49
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/17/2018
ms.locfileid: "34221850"
---
# <a name="class-based-dsc-resources"></a><span data-ttu-id="8e582-102">Osztályalapú DSC-erőforrások</span><span class="sxs-lookup"><span data-stu-id="8e582-102">Class-based DSC Resources</span></span>

## <a name="defining-dsc-resources-with-classes"></a><span data-ttu-id="8e582-103">Osztályok DSC erőforrások meghatározása</span><span class="sxs-lookup"><span data-stu-id="8e582-103">Defining DSC resources with classes</span></span>

<span data-ttu-id="8e582-104">Visszajelzések alapján hajtottunk szerzői osztály DSC erőforrásokhoz egyszerűbb és könnyebben érthetőek legyenek.</span><span class="sxs-lookup"><span data-stu-id="8e582-104">Based on feedback, we’ve made authoring class-based DSC resources simpler and easier to understand.</span></span>
<span data-ttu-id="8e582-105">Egy osztály-alapú DSC erőforrás és a parancsmag DSC erőforrás-szolgáltató közötti fő különbségek a következők:</span><span class="sxs-lookup"><span data-stu-id="8e582-105">The major differences between a class-based DSC resource and a cmdlet DSC resource provider are:</span></span>

* <span data-ttu-id="8e582-106">Nincs szükség a séma MOF-fájlt.</span><span class="sxs-lookup"><span data-stu-id="8e582-106">A MOF file for the schema is not required.</span></span>
* <span data-ttu-id="8e582-107">A **DSCResource** nincs szükség a modul mappa almappája.</span><span class="sxs-lookup"><span data-stu-id="8e582-107">A **DSCResource** subfolder in the module folder is not required.</span></span>
* <span data-ttu-id="8e582-108">A PowerShell modul is tartalmazhatnak, több DSC erőforrás osztályok.</span><span class="sxs-lookup"><span data-stu-id="8e582-108">A PowerShell module file can contain multiple DSC resource classes.</span></span>

<span data-ttu-id="8e582-109">További információkért lásd: [PowerShell osztályokra egyéni DSC-erőforrás írása](https://msdn.microsoft.com/powershell/dsc/authoringresource).</span><span class="sxs-lookup"><span data-stu-id="8e582-109">For more information, see [Writing a custom DSC resource with PowerShell classes](https://msdn.microsoft.com/powershell/dsc/authoringresource).</span></span>
