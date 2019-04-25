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
# <a name="call-base-class-method"></a>Alaposztály metódusának hívása

A meglévő módszerek az alosztályok felül lehet bírálni. Ehhez deklarálja a módszerek ilyen névvel és aláírás használatával:

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

Alaposztály módszerek meghívhatnak felülbírált megvalósításokhoz, konvertálni az alaposztály ([baseClass] $Ez) a meghívási:

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

Az összes PowerShell-módszer olyan virtuális. Ugyanazt a szintaxist is felülbírálás használatával elrejtheti alosztályát nem virtuális .NET-metódusokat: csak az azonos nevű és aláírás módszerek deklarálható.

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
