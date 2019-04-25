---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: d5ec95abb1d3160afc4179cff991cb5ef72d85fe
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62057298"
---
# <a name="clipboard-cmdlets"></a>Vágólap-parancsmagok
**Get-vágólapra** és **Set-vágólapra** könnyebben, tartalom, és a egy Windows PowerShell-munkamenetből átvitelét. Például, ha a Windows Explorer használatával három fájlok másolása a vágólapra (Ha kiválasztja őket, majd nyomja le az `ctrl-c`, például), majd könnyedén hozzáférhet a vágólap tartalmát, azon fájlok listáját:

```powershell
PS C:\\&gt; Get-Clipboard -Format FileDropList

Directory: C:\\Users\\slee\\Downloads\\Example

Mode LastWriteTime Length Name

---- ------------- ------ ----

-a---- 4/14/2015 1:19 PM 0 File2.txt

-a---- 4/14/2015 1:19 PM 0 File3.txt

-a---- 4/14/2015 1:19 PM 0 File1.txt
```


A vágólap-parancsmagok támogatják a lemezképek, a hangfájlok, a fájl listák és a szöveg.
