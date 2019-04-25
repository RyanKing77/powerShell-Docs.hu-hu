---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: 5b31fe833fb0f9d0f3f2733e777e4608a697d583
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62057927"
---
# <a name="side-by-side-module-versioning-support-for-dsc-resources"></a>Egymás melletti modul verziószámozás támogatása a DSC-erőforrásokhoz

A modulok DSC-erőforrásokat tartalmazó lehet telepítve egymás mellett, és a DSC-konfigurációk használhatja az erőforrást, amelyre telepítve van a rendszeren egy adott verzióját.

További információkért lásd: [eltérő verziójú erőforrások használata](https://msdn.microsoft.com/powershell/dsc/sxsresource).

## <a name="known-issues"></a>Ismert problémák

Ebben a kiadásban a következő ismert problémák egymás melletti telepítés:

-   Két különböző verzióit a DSC-erőforrás belül ugyanaz a konfiguráció használata nem támogatott.
