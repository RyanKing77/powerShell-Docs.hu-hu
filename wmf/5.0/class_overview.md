---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: 5919a68c87ae8827a1b97befc653bb74713f33fe
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55686445"
---
# <a name="creating-custom-types-using-powershell-classes"></a>Egyéni típusok létrehozása PowerShell-osztályokkal

Továbbfejlesztettük a PowerShell nyelv osztályok és a többi felhasználó által meghatározott típusok definiálása formális szintaxist és a hasonló más objektumorientált programozási nyelveket szemantika használatával. A cél, hogy a fejlesztők és informatikai szakemberek PowerShell kihasználni a használati esetek szélesebb köre, leegyszerűsítheti a fejlesztést az PowerShell-összetevők (például a DSC-erőforrások) és gyorsítsa fel a felügyeleti felületek lefedettség engedélyezése.

## <a name="supported-scenarios-in-this-release"></a>Ebben a kiadásban támogatott helyzetek

-   DSC-erőforrások és az azokhoz társított típusokat megadása a PowerShell nyelv segítségével
-   Egyéni típusok definiálása a PowerShellben a jól ismert objektumorientált programozási módszerek, például az osztályokat, tulajdonságokat, módszerek használatával.
-   Öröklés támogatására az osztály a PowerShell és az osztály base DSC-erőforrás
-   Típusok hibakeresés a PowerShell nyelv használatával
-   Hozzon létre, és a kivételek kezelésére, formális mechanizmusok használatával, és a megfelelő szinten
