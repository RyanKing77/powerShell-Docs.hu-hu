---
ms.date: 06/12/2017
author: JKeithB
ms.topic: reference
keywords: WMF, powershell, beállítás
ms.openlocfilehash: 7eaa4dfb68bc299ad31bce81af96b6a760c4fcc5
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="creating-custom-types-using-powershell-classes"></a>Egyéni típusok létrehozása PowerShell-osztályokkal

Azt is javult a PowerShell nyelvi osztályok és más felhasználó által definiált típusok meghatározásához formális szintaxisát és egyéb objektumorientált programozási nyelvek hasonló szemantika használatával. A cél, hogy engedélyezze a fejlesztők és informatikai szakemberek számára bevezetni a PowerShell szélesebb köre által használati esetek, fejlesztési PowerShell összetevők (például a DSC) egyszerűbbé és felgyorsítani felügyeleti felületek körét.

## <a name="supported-scenarios-in-this-release"></a>Ez a kiadás támogatott helyzetek

-   Adja meg a DSC-erőforrások és a kapcsolódó típusukat a PowerShell nyelv használatával
-   Egyéni típusainak definiálása a PowerShell használatával a megszokott objektumorientált programozási módszerek, például az osztályokat, tulajdonságokat, módszerek, stb.
-   A PowerShell és az osztály base DSC erőforrás osztály öröklési támogatása
-   Debug típusok a PowerShell nyelv használatával
-   Létrehozni és kezelni a kivételek formális mechanizmusok használatával, és a megfelelő szintű