---
ms.date: 06/12/2017
author: JKeithB
ms.topic: reference
keywords: WMF, powershell, beállítás
ms.openlocfilehash: 3269c8cc871f22488b64fb072dac72698983f360
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
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