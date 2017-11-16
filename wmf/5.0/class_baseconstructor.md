---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "WMF, a powershell, a beállítása"
ms.openlocfilehash: 1fd6d80d6b7effb4bd98c1594d64e531c4e5c9b5
ms.sourcegitcommit: a5c0795ca6ec9332967bff9c151a8572feb1a53a
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/27/2017
---
# <a name="call-base-class-constructor"></a>Alaposztály konstruktor hívása

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

