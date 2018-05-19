---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: 9486fdbaeca66c83551564c76ce47482f77c36b9
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/17/2018
---
# <a name="call-base-class-constructor"></a>Alaposztály konstruktorának hívása

Alaposztály konstruktora felelnek meg, és egy alosztályt, használja a kulcsszó **alap**:

```powershell
class A
{
    [int]$a

    A([int]$a)
    {
        $this.a = $a
    }
}

class B : A
{
    B() : base(103) {}
}

[B]::new().a # return 103
```

Ha egy olyan alaposztályból alapértelmezett (paraméter nélküli) konstruktort, akkor kihagyhatja egy explicit konstruktor hívása:

```powershell
class C : B
{
    C([int]$c) {}
}
```
