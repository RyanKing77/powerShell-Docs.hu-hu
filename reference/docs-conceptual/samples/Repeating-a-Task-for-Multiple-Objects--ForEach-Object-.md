---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: Feladatok megismétlése több objektumon ForEach-Object
ms.openlocfilehash: 1442507c4213476f65df3401c1021f8d0fc31956
ms.sourcegitcommit: a6f13c16a535acea279c0ddeca72f1f0d8a8ce4c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2019
ms.locfileid: "67030814"
---
# <a name="repeating-a-task-for-multiple-objects-foreach-object"></a><span data-ttu-id="007d5-103">Feladatok megismétlése több objektumon (ForEach-Object)</span><span class="sxs-lookup"><span data-stu-id="007d5-103">Repeating a Task for Multiple Objects (ForEach-Object)</span></span>

<span data-ttu-id="007d5-104">A **ForEach-Object** parancsmagot használja a parancsfájl-blokkokban és a `$_` az aktuális folyamat objektum lehetővé teszi, hogy a folyamat minden egyes objektumában parancsot futtató leíró.</span><span class="sxs-lookup"><span data-stu-id="007d5-104">The **ForEach-Object** cmdlet uses script blocks and the `$_` descriptor for the current pipeline object to let you run a command on each object in the pipeline.</span></span> <span data-ttu-id="007d5-105">Ez bonyolult feladatok elvégzésére is használható.</span><span class="sxs-lookup"><span data-stu-id="007d5-105">This can be used to perform some complicated tasks.</span></span>

<span data-ttu-id="007d5-106">Egy olyan helyzetet, ahol ez hasznos lehet, hogy több hasznos adat van módosítása.</span><span class="sxs-lookup"><span data-stu-id="007d5-106">One situation where this can be useful is manipulating data to make it more useful.</span></span> <span data-ttu-id="007d5-107">Például a Win32_LogicalDisk osztály a WMI segítségével minden helyi lemez szabad terület információkat ad vissza.</span><span class="sxs-lookup"><span data-stu-id="007d5-107">For example, the Win32_LogicalDisk class from WMI can be used to return free space information for each local disk.</span></span> <span data-ttu-id="007d5-108">Az ad vissza, tekintetében bájt, azonban, ami lehetővé teszi az nehezen olvasható:</span><span class="sxs-lookup"><span data-stu-id="007d5-108">The data is returned in terms of bytes, however, which makes it difficult to read:</span></span>

```
PS> Get-WmiObject -Class Win32_LogicalDisk

DeviceID     : C:
DriveType    : 3
ProviderName :
FreeSpace    : 50665070592
Size         : 203912880128
VolumeName   : Local Disk
```

<span data-ttu-id="007d5-109">Azt is átalakítani a FreeSpace értéket (MB): az egyes értékek kétszer; elosztja 1024 az első osztás után az adatok kilobájtban, pedig a második osztás után azt (MB).</span><span class="sxs-lookup"><span data-stu-id="007d5-109">We can convert the FreeSpace value to megabytes by dividing each value by 1024 twice; after the first division, the data is in kilobytes, and after the second division it is megabytes.</span></span> <span data-ttu-id="007d5-110">Teheti, hogy egy ForEach-Object parancsfájlblokkban lévő beírásával:</span><span class="sxs-lookup"><span data-stu-id="007d5-110">You can do that in a ForEach-Object script block by typing:</span></span>

```
PS> Get-WmiObject -Class Win32_LogicalDisk | ForEach-Object -Process {($_.FreeSpace)/1024.0/1024.0}
48318.01171875
```

<span data-ttu-id="007d5-111">Sajnos a kimenet mostantól adatok nincsenek társított címkével.</span><span class="sxs-lookup"><span data-stu-id="007d5-111">Unfortunately, the output is now data with no associated label.</span></span> <span data-ttu-id="007d5-112">A WMI-tulajdonságok írásvédettek, mivel FreeSpace közvetlenül nem konvertálhatóak.</span><span class="sxs-lookup"><span data-stu-id="007d5-112">Because WMI properties such as this are read-only, you cannot directly convert FreeSpace.</span></span> <span data-ttu-id="007d5-113">Írja be ezt:</span><span class="sxs-lookup"><span data-stu-id="007d5-113">If you type this:</span></span>

```powershell
Get-WmiObject -Class Win32_LogicalDisk | ForEach-Object -Process {$_.FreeSpace = ($_.FreeSpace)/1024.0/1024.0}
```

<span data-ttu-id="007d5-114">Hibaüzenetet kap:</span><span class="sxs-lookup"><span data-stu-id="007d5-114">You get an error message:</span></span>

```output
"FreeSpace" is a ReadOnly property.
At line:1 char:70
+ Get-WmiObject -Class Win32_LogicalDisk | ForEach-Object -Process {$_.F <<<< r
eeSpace = ($_.FreeSpace)/1024.0/1024.0}
```

<span data-ttu-id="007d5-115">Néhány speciális technikák segítségével az adatok sikerült rendezhetők át, de egy egyszerűbb módszert hozhat létre egy új objektum használatával **Select-Object**.</span><span class="sxs-lookup"><span data-stu-id="007d5-115">You could reorganize the data by using some advanced techniques, but a simpler approach is to create a new object, by using **Select-Object**.</span></span>
