---
ms.date: 2017-06-05
keywords: PowerShell parancsmag
title: "Objektumok kiválasztásával részét jelölje ki az objektumot"
ms.assetid: 72e64b1a-d351-4500-9da3-24d8a71d7a92
ms.openlocfilehash: 8c9633e80f63e1d474c46fa772108aee4f79751d
ms.sourcegitcommit: 74255f0b5f386a072458af058a15240140acb294
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/03/2017
---
# <a name="selecting-parts-of-objects-select-object"></a><span data-ttu-id="95c26-103">Objektumok (Select-Object) részek kijelölése</span><span class="sxs-lookup"><span data-stu-id="95c26-103">Selecting Parts of Objects (Select-Object)</span></span>
<span data-ttu-id="95c26-104">Használhatja a **Select-Object** parancsmaggal hozzon létre új, egyéni ki az objektumokat hozhat létre, azokat a tulajdonságokat tartalmazó Windows PowerShell objektumokra.</span><span class="sxs-lookup"><span data-stu-id="95c26-104">You can use the **Select-Object** cmdlet to create new, custom Windows PowerShell objects that contain properties selected from the objects you use to create them.</span></span> <span data-ttu-id="95c26-105">A következő paranccsal hozzon létre egy új objektumot, amely tartalmazza az csak a nevét és FreeSpace a Win32_LogicalDisk WMI-osztály tulajdonságai:</span><span class="sxs-lookup"><span data-stu-id="95c26-105">Type the following command to create a new object that includes only the Name and FreeSpace properties of the Win32_LogicalDisk WMI class:</span></span>

```
PS> Get-WmiObject -Class Win32_LogicalDisk | Select-Object -Property Name,FreeSpace

Name                                    FreeSpace
----                                    ---------
C:                                      50664845312
```

<span data-ttu-id="95c26-106">Az adatok típusa nem látható, hogy a parancs kiadása után, de ha a Get-tag eredmény után a Select-Object csövön keresztüli, állapítható meg, hogy rendelkezik-e új típusú objektum, egy PSCustomObject:</span><span class="sxs-lookup"><span data-stu-id="95c26-106">You cannot see the type of data after issuing that command, but if you pipe the result to Get-Member after the Select-Object, you can tell that you have a new type of object, a PSCustomObject:</span></span>

```
PS> Get-WmiObject -Class Win32_LogicalDisk | Select-Object -Property Name,FreeSpace| Get-Member

   TypeName: System.Management.Automation.PSCustomObject

Name        MemberType   Definition
----        ----------   ----------
Equals      Method       System.Boolean Equals(Object obj)
GetHashCode Method       System.Int32 GetHashCode()
GetType     Method       System.Type GetType()
ToString    Method       System.String ToString()
FreeSpace   NoteProperty  FreeSpace=...
Name        NoteProperty System.String Name=C:
```

<span data-ttu-id="95c26-107">Select-Object számos felhasználása van.</span><span class="sxs-lookup"><span data-stu-id="95c26-107">Select-Object has many uses.</span></span> <span data-ttu-id="95c26-108">Az egyik legyen replikálódik adatokat, majd módosíthatja.</span><span class="sxs-lookup"><span data-stu-id="95c26-108">One of them is replicating data that you can then modify.</span></span> <span data-ttu-id="95c26-109">Azt már tudja kezelni a problémát az előző szakaszban miatt.</span><span class="sxs-lookup"><span data-stu-id="95c26-109">We can now handle the problem we ran across in the previous section.</span></span> <span data-ttu-id="95c26-110">Azt is FreeSpace értékét az újonnan létrehozott objektumokat a frissítést, és a kimenet tartalmazza a leíró nevet:</span><span class="sxs-lookup"><span data-stu-id="95c26-110">We can update the value of FreeSpace in our newly-created objects and the output will include the descriptive label:</span></span>

```
Get-WmiObject -Class Win32_LogicalDisk | Select-Object -Property Name,FreeSpace | ForEach-Object -Process {$_.FreeSpace = ($_.FreeSpace)/1024.0/1024.0; $_}
Name                                                                  FreeSpace
----                                                                  ---------
C:                                                                48317.7265625
```

