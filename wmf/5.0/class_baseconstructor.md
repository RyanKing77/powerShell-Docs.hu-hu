---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: 424e0b7a4d62fc35e5040a7e425950e887021d7e
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55683778"
---
# <a name="call-base-class-constructor"></a>Alaposztály konstruktorának hívása

Alaposztály konstruktorának hívása egy alosztályt, használja a kulcsszó **alap**:

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

Ha egy osztály (nincs paraméter) alapértelmezett konstruktort, kihagyhatja egy explicit konstruktor hívás:

```powershell
class C : B
{
    C([int]$c) {}
}
```
