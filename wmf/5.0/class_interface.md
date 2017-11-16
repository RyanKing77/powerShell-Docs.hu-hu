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
# <a name="declare-implemented-interface"></a><span data-ttu-id="5bbb7-102">Megvalósított illesztőfelület deklarálható</span><span class="sxs-lookup"><span data-stu-id="5bbb7-102">Declare Implemented Interface</span></span>

<span data-ttu-id="5bbb7-103">Deklarálhatja megvalósított illesztőfelületek alaptípusában vagy után azonnal kettőspontot (:), ha nincs megadva alap típus.</span><span class="sxs-lookup"><span data-stu-id="5bbb7-103">You can declare implemented interfaces after base types, or immediately after a colon (:), if there is no base type specified.</span></span> <span data-ttu-id="5bbb7-104">Minden típusnevek külön vesszővel válassza el.</span><span class="sxs-lookup"><span data-stu-id="5bbb7-104">Separate all type names by using commas.</span></span> <span data-ttu-id="5bbb7-105">Nagyon hasonlít, a C# szintaxis.</span><span class="sxs-lookup"><span data-stu-id="5bbb7-105">It’s very similar to C# syntax.</span></span>

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

