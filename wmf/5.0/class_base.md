---
ms.date: 06/12/2017
author: JKeithB
ms.topic: reference
keywords: WMF, powershell, beállítás
ms.openlocfilehash: 43b26426a76b6503a83e35ae0c02a0af69902ed6
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="declare-base-class"></a><span data-ttu-id="7e365-102">Alaposztály deklarálása</span><span class="sxs-lookup"><span data-stu-id="7e365-102">Declare Base Class</span></span>
<span data-ttu-id="7e365-103">A Windows PowerShell-osztály egy másik Windows PowerShell osztály alaptípusként deklarálhatnak.</span><span class="sxs-lookup"><span data-stu-id="7e365-103">You can declare a Windows PowerShell class as a base type for another Windows PowerShell class.</span></span>

```powershell
class bar
{
   [int]foo()
       {
           return 100500
       }
}

class baz : bar {}

[baz]::new().foo() # return 100500
```

<span data-ttu-id="7e365-104">Meglévő .NET-keretrendszer típusok alaposztályok is használhatja:</span><span class="sxs-lookup"><span data-stu-id="7e365-104">You can also use existing .NET Framework types as base classes:</span></span>

```powershell
class MyIntList : system.collections.generic.list[int]
{

}

$list = [MyIntList]::new()

$list.Add(100)

$list[0] # return 100
```