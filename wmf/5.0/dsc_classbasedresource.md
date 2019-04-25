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
# <a name="class-based-dsc-resources"></a>Osztályalapú DSC-erőforrások

## <a name="defining-dsc-resources-with-classes"></a>DSC-erőforrások osztályok definiálása

A visszajelzések függvényében végeztünk osztályalapú DSC erőforrások egyszerűbb és könnyebben átláthatóak készítése.
Osztályalapú DSC-erőforrás és a egy parancsmag DSC erőforrás-szolgáltató közötti fő különbségek a következők:

* A séma MOF-fájlt, nem szükséges.
* A **DSCResource** almappát a modul mappában, nem szükséges.
* Egy PowerShell-modul fájlt tartalmazhat több DSC-erőforrás osztályok.

További információkért lásd: [PowerShell-osztályokkal egyéni DSC-erőforrás írása](https://msdn.microsoft.com/powershell/dsc/authoringresource).
