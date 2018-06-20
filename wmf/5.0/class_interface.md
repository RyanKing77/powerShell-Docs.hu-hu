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
# <a name="declare-implemented-interface"></a><span data-ttu-id="24fe9-102">Megvalósított interfész deklarálása</span><span class="sxs-lookup"><span data-stu-id="24fe9-102">Declare Implemented Interface</span></span>

<span data-ttu-id="24fe9-103">Deklarálhatja megvalósított illesztőfelületek alaptípusában vagy után azonnal kettőspontot (:), ha nincs megadva alap típus.</span><span class="sxs-lookup"><span data-stu-id="24fe9-103">You can declare implemented interfaces after base types, or immediately after a colon (:), if there is no base type specified.</span></span> <span data-ttu-id="24fe9-104">Minden típusnevek külön vesszővel válassza el.</span><span class="sxs-lookup"><span data-stu-id="24fe9-104">Separate all type names by using commas.</span></span> <span data-ttu-id="24fe9-105">Nagyon hasonlít, a C# szintaxis.</span><span class="sxs-lookup"><span data-stu-id="24fe9-105">It’s very similar to C# syntax.</span></span>

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
