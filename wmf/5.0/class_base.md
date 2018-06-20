---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: 188ede0c558210a746ad0f6c6cef6f571b280878
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/17/2018
ms.locfileid: "34219905"
---
# <a name="declare-base-class"></a><span data-ttu-id="e5db6-102">Alaposztály deklarálása</span><span class="sxs-lookup"><span data-stu-id="e5db6-102">Declare Base Class</span></span>
<span data-ttu-id="e5db6-103">A Windows PowerShell-osztály egy másik Windows PowerShell osztály alaptípusként deklarálhatnak.</span><span class="sxs-lookup"><span data-stu-id="e5db6-103">You can declare a Windows PowerShell class as a base type for another Windows PowerShell class.</span></span>

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

<span data-ttu-id="e5db6-104">Meglévő .NET-keretrendszer típusok alaposztályok is használhatja:</span><span class="sxs-lookup"><span data-stu-id="e5db6-104">You can also use existing .NET Framework types as base classes:</span></span>

```powershell
class MyIntList : system.collections.generic.list[int]
{

}

$list = [MyIntList]::new()

$list.Add(100)

$list[0] # return 100
```
