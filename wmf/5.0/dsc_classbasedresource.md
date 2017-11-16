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
# <a name="class-based-dsc-resources"></a>A DSC osztály-alapú erőforrások

## <a name="defining-dsc-resources-with-classes"></a>Osztályok DSC erőforrások meghatározása

Visszajelzések alapján hajtottunk szerzői osztály DSC erőforrásokhoz egyszerűbb és könnyebben érthetőek legyenek. Egy osztály-alapú DSC erőforrás és a parancsmag DSC erőforrás-szolgáltató közötti fő különbségek a következők:

* Nincs szükség a séma MOF-fájlt.
* A **DSCResource** nincs szükség a modul mappa almappája.
* A PowerShell modul is tartalmazhatnak, több DSC erőforrás osztályok.

További információkért lásd: [PowerShell osztályokra egyéni DSC-erőforrás írása](https://msdn.microsoft.com/powershell/dsc/authoringresource).

