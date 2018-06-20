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
# <a name="class-based-dsc-resources"></a>Osztályalapú DSC-erőforrások

## <a name="defining-dsc-resources-with-classes"></a>Osztályok DSC erőforrások meghatározása

Visszajelzések alapján hajtottunk szerzői osztály DSC erőforrásokhoz egyszerűbb és könnyebben érthetőek legyenek.
Egy osztály-alapú DSC erőforrás és a parancsmag DSC erőforrás-szolgáltató közötti fő különbségek a következők:

* Nincs szükség a séma MOF-fájlt.
* A **DSCResource** nincs szükség a modul mappa almappája.
* A PowerShell modul is tartalmazhatnak, több DSC erőforrás osztályok.

További információkért lásd: [PowerShell osztályokra egyéni DSC-erőforrás írása](https://msdn.microsoft.com/powershell/dsc/authoringresource).
