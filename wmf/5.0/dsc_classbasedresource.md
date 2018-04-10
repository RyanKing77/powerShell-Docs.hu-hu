---
ms.date: 06/12/2017
author: JKeithB
ms.topic: reference
keywords: WMF, powershell, beállítás
ms.openlocfilehash: 4def20aa95f66ab23c9eee575150bc3db02541d8
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="class-based-dsc-resources"></a>Osztályalapú DSC-erőforrások

## <a name="defining-dsc-resources-with-classes"></a>Osztályok DSC erőforrások meghatározása

Visszajelzések alapján hajtottunk szerzői osztály DSC erőforrásokhoz egyszerűbb és könnyebben érthetőek legyenek.
Egy osztály-alapú DSC erőforrás és a parancsmag DSC erőforrás-szolgáltató közötti fő különbségek a következők:

* Nincs szükség a séma MOF-fájlt.
* A **DSCResource** nincs szükség a modul mappa almappája.
* A PowerShell modul is tartalmazhatnak, több DSC erőforrás osztályok.

További információkért lásd: [PowerShell osztályokra egyéni DSC-erőforrás írása](https://msdn.microsoft.com/powershell/dsc/authoringresource).