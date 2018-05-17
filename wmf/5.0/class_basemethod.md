---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: d7aec1a2ba8964e877ddd7406609fe135b1eb462
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/17/2018
---
# <a name="call-base-class-method"></a>Alaposztály metódusának hívása

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
