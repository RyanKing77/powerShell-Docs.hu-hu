---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: 424e0b7a4d62fc35e5040a7e425950e887021d7e
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62085881"
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
