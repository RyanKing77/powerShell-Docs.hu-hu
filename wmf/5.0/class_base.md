---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: 8b3ebd22e03bf9bdd5f26965137a1b1ce9f47c3e
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62058777"
---
# <a name="declare-base-class"></a><span data-ttu-id="c4daa-102">Alaposztály deklarálása</span><span class="sxs-lookup"><span data-stu-id="c4daa-102">Declare Base Class</span></span>
<span data-ttu-id="c4daa-103">Egy Windows PowerShell osztály eszközhöz adhat meg, egy Windows PowerShell egy másik osztály alaptípusa.</span><span class="sxs-lookup"><span data-stu-id="c4daa-103">You can declare a Windows PowerShell class as a base type for another Windows PowerShell class.</span></span>

```powershell
class bar
{
   [int]foo()
       {
           return 100500
       }
}

class baz : bar {}

[baz]::new().foo() # return 100500
```

<span data-ttu-id="c4daa-104">Használhatja a meglévő .NET-keretrendszer típusok osztályok:</span><span class="sxs-lookup"><span data-stu-id="c4daa-104">You can also use existing .NET Framework types as base classes:</span></span>

```powershell
class MyIntList : system.collections.generic.list[int]
{

}

$list = [MyIntList]::new()

$list.Add(100)

$list[0] # return 100
```
