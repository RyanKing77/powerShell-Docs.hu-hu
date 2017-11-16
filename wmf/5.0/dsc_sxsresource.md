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
# <a name="side-by-side-module-versioning-support-for-dsc-resources"></a>A DSC-erőforrások párhuzamos modul Versioning támogatása

Modulok tartalmazó DSC-erőforrások lehetnek egymás melletti telepítve, és a DSC-konfigurációk használhatja az erőforrást, amelyre telepítve van a rendszeren egy adott verziójához.

További információkért lásd: [erőforrásokat használó többféle verzióját tartalmazó](https://msdn.microsoft.com/powershell/dsc/sxsresource).

## <a name="known-issues"></a>Ismert problémák

Ebben a kiadásban a következő ismert problémákat olvashatja egymás melletti telepítés:

-   A DSC-erőforrás belül ugyanaz a konfiguráció két különböző verzióinak használata nem támogatott.

