---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: 4b593e9a1eca43ee7ad85fc921ae3c1d62722db9
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55687859"
---
# <a name="declare-implemented-interface"></a>Megvalósított interfész deklarálása

Eszközhöz adhat meg implementovaná rozhraní típusok, vagy közvetlenül egy kettőspontot (:), ha nincs megadva alap típus. Írja be az összes vesszőkkel válassza el egymástól a neveket. Nagyon hasonló a C# szintaxist.

```powershell
class MyComparable : system.IComparable
{
    [int] CompareTo([object] $obj)
    {
        return 0;
    }
}

class MyComparableBar : bar, system.IComparable
{
    [int] CompareTo([object] $obj)
    {
        return 0;
    }
}
```
