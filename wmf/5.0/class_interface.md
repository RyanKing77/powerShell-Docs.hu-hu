---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "WMF, a powershell, a beállítása"
ms.openlocfilehash: 968e78beb8df77588a08a9ce8732e4abcadde4d0
ms.sourcegitcommit: a5c0795ca6ec9332967bff9c151a8572feb1a53a
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/27/2017
---
# <a name="declare-implemented-interface"></a>Megvalósított illesztőfelület deklarálható

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

