---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "WMF, a powershell, a beállítása"
ms.openlocfilehash: d40e5475c4132d6377c9a4559262a41b4842180a
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2017
---
# <a name="class-based-dsc-resources"></a><span data-ttu-id="373d2-102">A DSC osztály-alapú erőforrások</span><span class="sxs-lookup"><span data-stu-id="373d2-102">Class-based DSC Resources</span></span>

## <a name="defining-dsc-resources-with-classes"></a><span data-ttu-id="373d2-103">Osztályok DSC erőforrások meghatározása</span><span class="sxs-lookup"><span data-stu-id="373d2-103">Defining DSC resources with classes</span></span>

<span data-ttu-id="373d2-104">Visszajelzések alapján hajtottunk szerzői osztály DSC erőforrásokhoz egyszerűbb és könnyebben érthetőek legyenek.</span><span class="sxs-lookup"><span data-stu-id="373d2-104">Based on feedback, we’ve made authoring class-based DSC resources simpler and easier to understand.</span></span> <span data-ttu-id="373d2-105">Egy osztály-alapú DSC erőforrás és a parancsmag DSC erőforrás-szolgáltató közötti fő különbségek a következők:</span><span class="sxs-lookup"><span data-stu-id="373d2-105">The major differences between a class-based DSC resource and a cmdlet DSC resource provider are:</span></span>

* <span data-ttu-id="373d2-106">Nincs szükség a séma MOF-fájlt.</span><span class="sxs-lookup"><span data-stu-id="373d2-106">A MOF file for the schema is not required.</span></span>
* <span data-ttu-id="373d2-107">A **DSCResource** nincs szükség a modul mappa almappája.</span><span class="sxs-lookup"><span data-stu-id="373d2-107">A **DSCResource** subfolder in the module folder is not required.</span></span>
* <span data-ttu-id="373d2-108">A PowerShell modul is tartalmazhatnak, több DSC erőforrás osztályok.</span><span class="sxs-lookup"><span data-stu-id="373d2-108">A PowerShell module file can contain multiple DSC resource classes.</span></span>

<span data-ttu-id="373d2-109">További információkért lásd: [PowerShell osztályokra egyéni DSC-erőforrás írása](https://msdn.microsoft.com/powershell/dsc/authoringresource).</span><span class="sxs-lookup"><span data-stu-id="373d2-109">For more information, see [Writing a custom DSC resource with PowerShell classes](https://msdn.microsoft.com/powershell/dsc/authoringresource).</span></span>

