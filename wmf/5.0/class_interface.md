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
# <a name="declare-implemented-interface"></a><span data-ttu-id="0cc6f-102">Megvalósított interfész deklarálása</span><span class="sxs-lookup"><span data-stu-id="0cc6f-102">Declare Implemented Interface</span></span>

<span data-ttu-id="0cc6f-103">Deklarálhatja megvalósított illesztőfelületek alaptípusában vagy után azonnal kettőspontot (:), ha nincs megadva alap típus.</span><span class="sxs-lookup"><span data-stu-id="0cc6f-103">You can declare implemented interfaces after base types, or immediately after a colon (:), if there is no base type specified.</span></span> <span data-ttu-id="0cc6f-104">Minden típusnevek külön vesszővel válassza el.</span><span class="sxs-lookup"><span data-stu-id="0cc6f-104">Separate all type names by using commas.</span></span> <span data-ttu-id="0cc6f-105">Nagyon hasonlít, a C# szintaxis.</span><span class="sxs-lookup"><span data-stu-id="0cc6f-105">It’s very similar to C# syntax.</span></span>

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