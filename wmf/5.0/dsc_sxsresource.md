---
ms.date: 06/12/2017
author: JKeithB
ms.topic: reference
keywords: WMF, powershell, beállítás
ms.openlocfilehash: a565f2befddc32f5088fa3e158f58d2dd78d41b4
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="side-by-side-module-versioning-support-for-dsc-resources"></a>A DSC-erőforrások párhuzamos modul Versioning támogatása

Modulok tartalmazó DSC-erőforrások lehetnek egymás melletti telepítve, és a DSC-konfigurációk használhatja az erőforrást, amelyre telepítve van a rendszeren egy adott verziójához.

További információkért lásd: [erőforrásokat használó többféle verzióját tartalmazó](https://msdn.microsoft.com/powershell/dsc/sxsresource).

## <a name="known-issues"></a>Ismert problémák

Ebben a kiadásban a következő ismert problémákat olvashatja egymás melletti telepítés:

-   A DSC-erőforrás belül ugyanaz a konfiguráció két különböző verzióinak használata nem támogatott.