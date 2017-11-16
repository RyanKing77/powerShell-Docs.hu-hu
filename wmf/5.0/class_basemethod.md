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
# <a name="call-base-class-method"></a>Alaposztály metódus hívása

Ha szeretné felülbírálni az alosztályok módszerek. Ehhez deklarálható módszerek használatával, az azonos névvel és aláírással:

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

Alaposztály metódusok hívására a felülbírált implementációiból, típusúvá az alaposztály ([baseClass] $Ez) a meghívási:

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

Az összes PowerShell módszereket virtuális. Ugyanaz a szintaxis használatával, mint egy felülbírálás elrejthetők alosztály nem virtuális .NET-metódusokat: csak az azonos névvel és aláírással rendelkező metódusok deklarálható.

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

