---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: 4b593e9a1eca43ee7ad85fc921ae3c1d62722db9
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62085861"
---
# <a name="declare-implemented-interface"></a><span data-ttu-id="26730-102">Megvalósított interfész deklarálása</span><span class="sxs-lookup"><span data-stu-id="26730-102">Declare Implemented Interface</span></span>

<span data-ttu-id="26730-103">Eszközhöz adhat meg implementovaná rozhraní típusok, vagy közvetlenül egy kettőspontot (:), ha nincs megadva alap típus.</span><span class="sxs-lookup"><span data-stu-id="26730-103">You can declare implemented interfaces after base types, or immediately after a colon (:), if there is no base type specified.</span></span> <span data-ttu-id="26730-104">Írja be az összes vesszőkkel válassza el egymástól a neveket.</span><span class="sxs-lookup"><span data-stu-id="26730-104">Separate all type names by using commas.</span></span> <span data-ttu-id="26730-105">Nagyon hasonló a C# szintaxist.</span><span class="sxs-lookup"><span data-stu-id="26730-105">It’s very similar to C# syntax.</span></span>

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
