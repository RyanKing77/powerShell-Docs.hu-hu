---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "WMF, a powershell, a beállítása"
ms.openlocfilehash: 7817769c3fc060a51c833b7469f7b556b9b40e87
ms.sourcegitcommit: a5c0795ca6ec9332967bff9c151a8572feb1a53a
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/27/2017
---
# <a name="call-base-class-method"></a><span data-ttu-id="d3ffb-102">Alaposztály metódus hívása</span><span class="sxs-lookup"><span data-stu-id="d3ffb-102">Call Base Class Method</span></span>

<span data-ttu-id="d3ffb-103">Ha szeretné felülbírálni az alosztályok módszerek.</span><span class="sxs-lookup"><span data-stu-id="d3ffb-103">You can override existing methods in subclasses.</span></span> <span data-ttu-id="d3ffb-104">Ehhez deklarálható módszerek használatával, az azonos névvel és aláírással:</span><span class="sxs-lookup"><span data-stu-id="d3ffb-104">To do this, declare methods by using the same name and signature:</span></span>

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

<span data-ttu-id="d3ffb-105">Alaposztály metódusok hívására a felülbírált implementációiból, típusúvá az alaposztály ([baseClass] $Ez) a meghívási:</span><span class="sxs-lookup"><span data-stu-id="d3ffb-105">To call base class methods from overridden implementations, cast to the base class ([baseClass]$this) on invocation:</span></span>

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

<span data-ttu-id="d3ffb-106">Az összes PowerShell módszereket virtuális.</span><span class="sxs-lookup"><span data-stu-id="d3ffb-106">All PowerShell methods are virtual.</span></span> <span data-ttu-id="d3ffb-107">Ugyanaz a szintaxis használatával, mint egy felülbírálás elrejthetők alosztály nem virtuális .NET-metódusokat: csak az azonos névvel és aláírással rendelkező metódusok deklarálható.</span><span class="sxs-lookup"><span data-stu-id="d3ffb-107">You can hide non-virtual .NET methods in a subclass by using the same syntax as you do for an override: just declare methods with same name and signature.</span></span>

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

