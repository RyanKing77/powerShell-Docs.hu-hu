---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: 0543afbc72148b1ba713e59655126c069b16ef33
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/17/2018
ms.locfileid: "34218433"
---
# <a name="side-by-side-module-versioning-support-for-dsc-resources"></a>A DSC-erőforrások párhuzamos modul Versioning támogatása

Modulok tartalmazó DSC-erőforrások lehetnek egymás melletti telepítve, és a DSC-konfigurációk használhatja az erőforrást, amelyre telepítve van a rendszeren egy adott verziójához.

További információkért lásd: [erőforrásokat használó többféle verzióját tartalmazó](https://msdn.microsoft.com/powershell/dsc/sxsresource).

## <a name="known-issues"></a>Ismert problémák

Ebben a kiadásban a következő ismert problémákat olvashatja egymás melletti telepítés:

-   A DSC-erőforrás belül ugyanaz a konfiguráció két különböző verzióinak használata nem támogatott.
