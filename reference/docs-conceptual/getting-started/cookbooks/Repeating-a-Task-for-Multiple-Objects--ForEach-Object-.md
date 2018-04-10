---
ms.date: 06/05/2017
keywords: PowerShell parancsmag
title: Ismétlődő feladat több objektumok ForEach objektum számára
ms.assetid: 6697a12d-2470-4ed6-b5bb-c35e5d525eb6
ms.openlocfilehash: 8b8002af3ade0905421760ce29cdc84b084236e9
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="repeating-a-task-for-multiple-objects-foreach-object"></a><span data-ttu-id="a6ffc-103">Ismétlődő feladat több objektum (ForEach-Object)</span><span class="sxs-lookup"><span data-stu-id="a6ffc-103">Repeating a Task for Multiple Objects (ForEach-Object)</span></span>

<span data-ttu-id="a6ffc-104">A **ForEach-Object** parancsmag parancsfájlblokkokban és használja az aktuális folyamat objektum $_ leíróját lehetővé teszik, hogy a parancsok a minden objektumon a folyamat.</span><span class="sxs-lookup"><span data-stu-id="a6ffc-104">The **ForEach-Object** cmdlet uses script blocks and the $_ descriptor for the current pipeline object to let you run a command on each object in the pipeline.</span></span> <span data-ttu-id="a6ffc-105">Ez összetett feladatok elvégzésére is használható.</span><span class="sxs-lookup"><span data-stu-id="a6ffc-105">This can be used to perform some complicated tasks.</span></span>

<span data-ttu-id="a6ffc-106">Amennyiben ez hasznos lehet egy helyzet adatokba, így több hasznos van kezelésére.</span><span class="sxs-lookup"><span data-stu-id="a6ffc-106">One situation where this can be useful is manipulating data to make it more useful.</span></span> <span data-ttu-id="a6ffc-107">Például a Win32_LogicalDisk osztály a WMI segítségével minden helyi lemez szabad terület adatokat ad vissza.</span><span class="sxs-lookup"><span data-stu-id="a6ffc-107">For example, the Win32_LogicalDisk class from WMI can be used to return free space information for each local disk.</span></span> <span data-ttu-id="a6ffc-108">A visszaküldött adatok tekintetében bájt, azonban így nehezen olvasható:</span><span class="sxs-lookup"><span data-stu-id="a6ffc-108">The data is returned in terms of bytes, however, which makes it difficult to read:</span></span>

```
PS> Get-WmiObject -Class Win32_LogicalDisk

DeviceID     : C:
DriveType    : 3
ProviderName :
FreeSpace    : 50665070592
Size         : 203912880128
VolumeName   : Local Disk
```

<span data-ttu-id="a6ffc-109">Azt is átalakítani a FreeSpace értéket megabájt elosztásával minden egyes értéknek 1024 kétszer; az első felosztás után ezeket az adatokat kilobájtban, pedig a második felosztás után mérete (MB).</span><span class="sxs-lookup"><span data-stu-id="a6ffc-109">We can convert the FreeSpace value to megabytes by dividing each value by 1024 twice; after the first division, the data is in kilobytes, and after the second division it is megabytes.</span></span> <span data-ttu-id="a6ffc-110">Teheti, hogy egy ForEach-Object parancsfájlblokk beírásával:</span><span class="sxs-lookup"><span data-stu-id="a6ffc-110">You can do that in a ForEach-Object script block by typing:</span></span>

```
PS> Get-WmiObject -Class Win32_LogicalDisk | ForEach-Object -Process {($_.FreeSpace)/1024.0/1024.0}
48318.01171875
```

<span data-ttu-id="a6ffc-111">Sajnos a kimeneti már adatok nem társított címkével.</span><span class="sxs-lookup"><span data-stu-id="a6ffc-111">Unfortunately, the output is now data with no associated label.</span></span> <span data-ttu-id="a6ffc-112">Mivel a WMI-tulajdonságait, például a csak olvasható, FreeSpace közvetlenül nem lehet konvertálni.</span><span class="sxs-lookup"><span data-stu-id="a6ffc-112">Because WMI properties such as this are read-only, you cannot directly convert FreeSpace.</span></span> <span data-ttu-id="a6ffc-113">Ha ez:</span><span class="sxs-lookup"><span data-stu-id="a6ffc-113">If you type this:</span></span>

```powershell
Get-WmiObject -Class Win32_LogicalDisk | ForEach-Object -Process {$_.FreeSpace = ($_.FreeSpace)/1024.0/1024.0}
```

<span data-ttu-id="a6ffc-114">Hibaüzenetet kapja:</span><span class="sxs-lookup"><span data-stu-id="a6ffc-114">You get an error message:</span></span>

```output
"FreeSpace" is a ReadOnly property.
At line:1 char:70
+ Get-WmiObject -Class Win32_LogicalDisk | ForEach-Object -Process {$_.F <<<< r
eeSpace = ($_.FreeSpace)/1024.0/1024.0}
```

<span data-ttu-id="a6ffc-115">Néhány speciális technikák segítségével az adatok sikerült rendezhetők át, de egy egyszerűbb módszert hozhat létre egy új objektum használatával **Select-Object**.</span><span class="sxs-lookup"><span data-stu-id="a6ffc-115">You could reorganize the data by using some advanced techniques, but a simpler approach is to create a new object, by using **Select-Object**.</span></span>