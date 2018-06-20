---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: d7aec1a2ba8964e877ddd7406609fe135b1eb462
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/17/2018
ms.locfileid: "34219742"
---
# <a name="call-base-class-method"></a><span data-ttu-id="c2ffa-102">Alaposztály metódusának hívása</span><span class="sxs-lookup"><span data-stu-id="c2ffa-102">Call Base Class Method</span></span>

<span data-ttu-id="c2ffa-103">Ha szeretné felülbírálni az alosztályok módszerek.</span><span class="sxs-lookup"><span data-stu-id="c2ffa-103">You can override existing methods in subclasses.</span></span> <span data-ttu-id="c2ffa-104">Ehhez deklarálható módszerek használatával, az azonos névvel és aláírással:</span><span class="sxs-lookup"><span data-stu-id="c2ffa-104">To do this, declare methods by using the same name and signature:</span></span>

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

<span data-ttu-id="c2ffa-105">Alaposztály metódusok hívására a felülbírált implementációiból, típusúvá az alaposztály ([baseClass] $Ez) a meghívási:</span><span class="sxs-lookup"><span data-stu-id="c2ffa-105">To call base class methods from overridden implementations, cast to the base class ([baseClass]$this) on invocation:</span></span>

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

<span data-ttu-id="c2ffa-106">Az összes PowerShell módszereket virtuális.</span><span class="sxs-lookup"><span data-stu-id="c2ffa-106">All PowerShell methods are virtual.</span></span> <span data-ttu-id="c2ffa-107">Ugyanaz a szintaxis használatával, mint egy felülbírálás elrejthetők alosztály nem virtuális .NET-metódusokat: csak az azonos névvel és aláírással rendelkező metódusok deklarálható.</span><span class="sxs-lookup"><span data-stu-id="c2ffa-107">You can hide non-virtual .NET methods in a subclass by using the same syntax as you do for an override: just declare methods with same name and signature.</span></span>

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
