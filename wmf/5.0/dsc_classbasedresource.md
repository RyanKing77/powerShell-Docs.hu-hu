---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: a1e90a0b96f74decb55343292b97befaf1a85f8a
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62058114"
---
# <a name="class-based-dsc-resources"></a><span data-ttu-id="d2d8b-102">Osztályalapú DSC-erőforrások</span><span class="sxs-lookup"><span data-stu-id="d2d8b-102">Class-based DSC Resources</span></span>

## <a name="defining-dsc-resources-with-classes"></a><span data-ttu-id="d2d8b-103">DSC-erőforrások osztályok definiálása</span><span class="sxs-lookup"><span data-stu-id="d2d8b-103">Defining DSC resources with classes</span></span>

<span data-ttu-id="d2d8b-104">A visszajelzések függvényében végeztünk osztályalapú DSC erőforrások egyszerűbb és könnyebben átláthatóak készítése.</span><span class="sxs-lookup"><span data-stu-id="d2d8b-104">Based on feedback, we’ve made authoring class-based DSC resources simpler and easier to understand.</span></span>
<span data-ttu-id="d2d8b-105">Osztályalapú DSC-erőforrás és a egy parancsmag DSC erőforrás-szolgáltató közötti fő különbségek a következők:</span><span class="sxs-lookup"><span data-stu-id="d2d8b-105">The major differences between a class-based DSC resource and a cmdlet DSC resource provider are:</span></span>

* <span data-ttu-id="d2d8b-106">A séma MOF-fájlt, nem szükséges.</span><span class="sxs-lookup"><span data-stu-id="d2d8b-106">A MOF file for the schema is not required.</span></span>
* <span data-ttu-id="d2d8b-107">A **DSCResource** almappát a modul mappában, nem szükséges.</span><span class="sxs-lookup"><span data-stu-id="d2d8b-107">A **DSCResource** subfolder in the module folder is not required.</span></span>
* <span data-ttu-id="d2d8b-108">Egy PowerShell-modul fájlt tartalmazhat több DSC-erőforrás osztályok.</span><span class="sxs-lookup"><span data-stu-id="d2d8b-108">A PowerShell module file can contain multiple DSC resource classes.</span></span>

<span data-ttu-id="d2d8b-109">További információkért lásd: [PowerShell-osztályokkal egyéni DSC-erőforrás írása](https://msdn.microsoft.com/powershell/dsc/authoringresource).</span><span class="sxs-lookup"><span data-stu-id="d2d8b-109">For more information, see [Writing a custom DSC resource with PowerShell classes](https://msdn.microsoft.com/powershell/dsc/authoringresource).</span></span>
