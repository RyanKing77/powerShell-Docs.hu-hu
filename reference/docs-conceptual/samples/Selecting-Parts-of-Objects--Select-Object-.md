---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: Objektumrészek objektum kijelölése
ms.assetid: 72e64b1a-d351-4500-9da3-24d8a71d7a92
ms.openlocfilehash: 323c57ba4462e20d9713fb74732989584f5a993f
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62057895"
---
# <a name="selecting-parts-of-objects-select-object"></a><span data-ttu-id="234e3-103">Objektumrészek (Select-Object)</span><span class="sxs-lookup"><span data-stu-id="234e3-103">Selecting Parts of Objects (Select-Object)</span></span>

<span data-ttu-id="234e3-104">Használhatja a **Select-Object** parancsmaggal hozhat létre, azokat az objektumokat a kiválasztott tulajdonságokat tartalmazó új, egyéni Windows PowerShell-objektumok létrehozásához.</span><span class="sxs-lookup"><span data-stu-id="234e3-104">You can use the **Select-Object** cmdlet to create new, custom Windows PowerShell objects that contain properties selected from the objects you use to create them.</span></span> <span data-ttu-id="234e3-105">Írja be a következő parancsot egy új objektum, amely csak a nevét és FreeSpace tulajdonságok a Win32_LogicalDisk WMI-osztály tartalmazza:</span><span class="sxs-lookup"><span data-stu-id="234e3-105">Type the following command to create a new object that includes only the Name and FreeSpace properties of the Win32_LogicalDisk WMI class:</span></span>

```
PS> Get-WmiObject -Class Win32_LogicalDisk | Select-Object -Property Name,FreeSpace

Name                                    FreeSpace
----                                    ---------
C:                                      50664845312
```

<span data-ttu-id="234e3-106">Az adatok típusát, hogy a parancs kiadása után nem látható, de azt az eredményt a Get-Member kanálu után a Select-Object, ha, hogy egy új típusú objektumot, egy PSCustomObject feliratból:</span><span class="sxs-lookup"><span data-stu-id="234e3-106">You cannot see the type of data after issuing that command, but if you pipe the result to Get-Member after the Select-Object, you can tell that you have a new type of object, a PSCustomObject:</span></span>

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

<span data-ttu-id="234e3-107">Select-Object számos célra rendelkezik.</span><span class="sxs-lookup"><span data-stu-id="234e3-107">Select-Object has many uses.</span></span> <span data-ttu-id="234e3-108">Adatok, amelyek ezt követően módosíthatja az egyiket áll replikálás alatt.</span><span class="sxs-lookup"><span data-stu-id="234e3-108">One of them is replicating data that you can then modify.</span></span> <span data-ttu-id="234e3-109">Most már tudjuk képes kezelni az előző szakaszban ütköztünk a problémát.</span><span class="sxs-lookup"><span data-stu-id="234e3-109">We can now handle the problem we ran across in the previous section.</span></span> <span data-ttu-id="234e3-110">Az újonnan létrehozott objektumok is frissítjük, FreeSpace értékét, és a kimenet tartalmazza a leíró:</span><span class="sxs-lookup"><span data-stu-id="234e3-110">We can update the value of FreeSpace in our newly-created objects and the output will include the descriptive label:</span></span>

```
Get-WmiObject -Class Win32_LogicalDisk | Select-Object -Property Name,FreeSpace | ForEach-Object -Process {$_.FreeSpace = ($_.FreeSpace)/1024.0/1024.0; $_}
Name                                                                  FreeSpace
----                                                                  ---------
C:                                                                48317.7265625
```