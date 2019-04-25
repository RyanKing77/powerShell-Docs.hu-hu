---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: 90fd26f9f27d2398da839b309c17b921bb3b8521
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62085326"
---
# <a name="new-guid"></a>New-Guid
Gyakran a parancsfájl (vagy akár a DSC-erőforrás írása), nincs szüksége az egyedi azonosítója. GUID-azonosítói megfelelően működjön, és hívja meg a .NET-keretrendszer Guid osztályt hozhat létre egy egyszerű, de kellene parancsmag segítségével könnyebben felfedezhetővé teheti a végfelhasználók számára, akik még nem ismeri a .NET-keretrendszer osztály:

PS C:\\&gt; New-Guid

Guid

----

e19d6ea5-3cc2-4db9-8095-0cdaed5a703d
