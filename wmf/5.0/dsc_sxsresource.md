---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "WMF, a powershell, a beállítása"
ms.openlocfilehash: 3261e5a07b8181190a04de3f210da50f23bb2953
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2017
---
# <a name="side-by-side-module-versioning-support-for-dsc-resources"></a><span data-ttu-id="cdc5f-102">A DSC-erőforrások párhuzamos modul Versioning támogatása</span><span class="sxs-lookup"><span data-stu-id="cdc5f-102">Side-By-Side Module Versioning Support for DSC Resources</span></span>

<span data-ttu-id="cdc5f-103">Modulok tartalmazó DSC-erőforrások lehetnek egymás melletti telepítve, és a DSC-konfigurációk használhatja az erőforrást, amelyre telepítve van a rendszeren egy adott verziójához.</span><span class="sxs-lookup"><span data-stu-id="cdc5f-103">Modules containing DSC resources can be installed side-by-side, and DSC configurations can use a specific version of the resource that is installed on the system.</span></span>

<span data-ttu-id="cdc5f-104">További információkért lásd: [erőforrásokat használó többféle verzióját tartalmazó](https://msdn.microsoft.com/powershell/dsc/sxsresource).</span><span class="sxs-lookup"><span data-stu-id="cdc5f-104">For more information, see [Using resources with multiple versions](https://msdn.microsoft.com/powershell/dsc/sxsresource).</span></span>

## <a name="known-issues"></a><span data-ttu-id="cdc5f-105">Ismert problémák</span><span class="sxs-lookup"><span data-stu-id="cdc5f-105">Known issues</span></span>

<span data-ttu-id="cdc5f-106">Ebben a kiadásban a következő ismert problémákat olvashatja egymás melletti telepítés:</span><span class="sxs-lookup"><span data-stu-id="cdc5f-106">In this release, the following are known issues of side-by-side installation:</span></span>

-   <span data-ttu-id="cdc5f-107">A DSC-erőforrás belül ugyanaz a konfiguráció két különböző verzióinak használata nem támogatott.</span><span class="sxs-lookup"><span data-stu-id="cdc5f-107">Using two different versions of the DSC resource within the same configuration is not supported.</span></span>

