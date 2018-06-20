---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: 116f79a95126d0a1c579a95ec99eb5d8b75cc1e0
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/17/2018
ms.locfileid: "34225487"
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
