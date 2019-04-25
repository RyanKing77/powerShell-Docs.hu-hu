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
# <a name="clipboard-cmdlets"></a><span data-ttu-id="3ee68-102">Vágólap-parancsmagok</span><span class="sxs-lookup"><span data-stu-id="3ee68-102">Clipboard cmdlets</span></span>
<span data-ttu-id="3ee68-103">**Get-vágólapra** és **Set-vágólapra** könnyebben, tartalom, és a egy Windows PowerShell-munkamenetből átvitelét.</span><span class="sxs-lookup"><span data-stu-id="3ee68-103">**Get-Clipboard** and **Set-Clipboard** make it easier for you to transfer content to and from a Windows PowerShell session.</span></span> <span data-ttu-id="3ee68-104">Például, ha a Windows Explorer használatával három fájlok másolása a vágólapra (Ha kiválasztja őket, majd nyomja le az `ctrl-c`, például), majd könnyedén hozzáférhet a vágólap tartalmát, azon fájlok listáját:</span><span class="sxs-lookup"><span data-stu-id="3ee68-104">For example, if you use Windows Explorer to copy three files to the clipboard (by selecting them and pressing `ctrl-c`, for example), you can then easily access the contents of the clipboard as a list of files:</span></span>

```powershell
PS C:\\&gt; Get-Clipboard -Format FileDropList

Directory: C:\\Users\\slee\\Downloads\\Example

Mode LastWriteTime Length Name

---- ------------- ------ ----

-a---- 4/14/2015 1:19 PM 0 File2.txt

-a---- 4/14/2015 1:19 PM 0 File3.txt

-a---- 4/14/2015 1:19 PM 0 File1.txt
```


<span data-ttu-id="3ee68-105">A vágólap-parancsmagok támogatják a lemezképek, a hangfájlok, a fájl listák és a szöveg.</span><span class="sxs-lookup"><span data-stu-id="3ee68-105">The Clipboard cmdlets support images, audio files, file lists, and text.</span></span>
