---
ms.date: 06/12/2017
author: JKeithB
ms.topic: reference
keywords: WMF, powershell, beállítás
ms.openlocfilehash: 2c007321789ae22b4a2e048d2d64162b065f9a75
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="declare-implemented-interface"></a>Megvalósított interfész deklarálása

Deklarálhatja megvalósított illesztőfelületek alaptípusában vagy után azonnal kettőspontot (:), ha nincs megadva alap típus. Minden típusnevek külön vesszővel válassza el. Nagyon hasonlít, a C# szintaxis.

```powershell
class MyComparable : system.IComparable
{
    [int] CompareTo([object] $obj)
    {
        return 0;
    }
}

class MyComparableBar : bar, system.IComparable
{
    [int] CompareTo([object] $obj)
    {
        return 0;
    }
}
```