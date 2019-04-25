---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: 0e79127faf3f9bf6fe7d525db5bb946daf3b93e1
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62058624"
---
# <a name="call-base-class-method"></a><span data-ttu-id="67983-102">Alaposztály metódusának hívása</span><span class="sxs-lookup"><span data-stu-id="67983-102">Call Base Class Method</span></span>

<span data-ttu-id="67983-103">A meglévő módszerek az alosztályok felül lehet bírálni.</span><span class="sxs-lookup"><span data-stu-id="67983-103">You can override existing methods in subclasses.</span></span> <span data-ttu-id="67983-104">Ehhez deklarálja a módszerek ilyen névvel és aláírás használatával:</span><span class="sxs-lookup"><span data-stu-id="67983-104">To do this, declare methods by using the same name and signature:</span></span>

```powershell
class baseClass
{
    [int]foo() {return 100500}
}

class childClass1 : baseClass
{
    [int]foo() {return 200600}
}

[childClass1]::new().foo() # return 200600
```

<span data-ttu-id="67983-105">Alaposztály módszerek meghívhatnak felülbírált megvalósításokhoz, konvertálni az alaposztály ([baseClass] $Ez) a meghívási:</span><span class="sxs-lookup"><span data-stu-id="67983-105">To call base class methods from overridden implementations, cast to the base class ([baseClass]$this) on invocation:</span></span>

```powershell
class childClass2 : baseClass
{
    [int]foo()
    {
        return 3 * ([baseClass]$this).foo()
    }
}

[childClass2]::new().foo() # return 301500
```

<span data-ttu-id="67983-106">Az összes PowerShell-módszer olyan virtuális.</span><span class="sxs-lookup"><span data-stu-id="67983-106">All PowerShell methods are virtual.</span></span> <span data-ttu-id="67983-107">Ugyanazt a szintaxist is felülbírálás használatával elrejtheti alosztályát nem virtuális .NET-metódusokat: csak az azonos nevű és aláírás módszerek deklarálható.</span><span class="sxs-lookup"><span data-stu-id="67983-107">You can hide non-virtual .NET methods in a subclass by using the same syntax as you do for an override: just declare methods with same name and signature.</span></span>

```powershell
class MyIntList : system.collections.generic.list[int]
{
    # Add is final in system.collections.generic.list
    [void] Add([int]$arg)
    {
        ([system.collections.generic.list[int]]$this).Add($arg * 2)
    }
}

$list = [MyIntList]::new()
$list.Add(100)
$list[0] # return 200
```
