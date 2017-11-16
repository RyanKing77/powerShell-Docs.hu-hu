---
ms.date: 2017-06-05
keywords: PowerShell parancsmag
title: "Ismétlődő feladat több objektumok ForEach objektum számára"
ms.assetid: 6697a12d-2470-4ed6-b5bb-c35e5d525eb6
ms.openlocfilehash: 33ae2c76a512a651ba1b91d15d876608f0d43ccc
ms.sourcegitcommit: 74255f0b5f386a072458af058a15240140acb294
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/03/2017
---
# <a name="repeating-a-task-for-multiple-objects-foreach-object"></a>Ismétlődő feladat több objektum (ForEach-Object)
A **ForEach-Object** parancsmag parancsfájlblokkokban és használja az aktuális folyamat objektum $_ leíróját lehetővé teszik, hogy a parancsok a minden objektumon a folyamat. Ez összetett feladatok elvégzésére is használható.

Amennyiben ez hasznos lehet egy helyzet adatokba, így több hasznos van kezelésére. Például a Win32_LogicalDisk osztály a WMI segítségével minden helyi lemez szabad terület adatokat ad vissza. A visszaküldött adatok tekintetében bájt, azonban így nehezen olvasható:

```
PS> Get-WmiObject -Class Win32_LogicalDisk

DeviceID     : C:
DriveType    : 3
ProviderName :
FreeSpace    : 50665070592
Size         : 203912880128
VolumeName   : Local Disk
```

Azt is átalakítani a FreeSpace értéket megabájt elosztásával minden egyes értéknek 1024 kétszer; az első felosztás után ezeket az adatokat kilobájtban, pedig a második felosztás után mérete (MB). Teheti, hogy egy ForEach-Object parancsfájlblokk beírásával:

```
Get-WmiObject -Class Win32_LogicalDisk | ForEach-Object -Process {($_.FreeSpace)/1024.0/1024.0}
48318.01171875
```

Sajnos a kimeneti már adatok nem társított címkével. Mivel a WMI-tulajdonságait, például a csak olvasható, FreeSpace közvetlenül nem lehet konvertálni. Ha ez:

```
Get-WmiObject -Class Win32_LogicalDisk | ForEach-Object -Process {$_.FreeSpace = ($_.FreeSpace)/1024.0/1024.0}
```

Hibaüzenetet kapja:

```
"FreeSpace" is a ReadOnly property.
At line:1 char:70
+ Get-WmiObject -Class Win32_LogicalDisk | ForEach-Object -Process {$_.F <<<< r
eeSpace = ($_.FreeSpace)/1024.0/1024.0}
```

Néhány speciális technikák segítségével az adatok sikerült rendezhetők át, de egy egyszerűbb módszert hozhat létre egy új objektum használatával **Select-Object**.

