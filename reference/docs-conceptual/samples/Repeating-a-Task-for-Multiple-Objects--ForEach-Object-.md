---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: Feladatok megismétlése több objektumon ForEach-Object
ms.assetid: 6697a12d-2470-4ed6-b5bb-c35e5d525eb6
ms.openlocfilehash: 64d85edad4a6931b2376b95b6d1f5b4d5194399f
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/14/2018
ms.locfileid: "53404564"
---
# <a name="repeating-a-task-for-multiple-objects-foreach-object"></a>Feladatok megismétlése több objektumon (ForEach-Object)

A **ForEach-Object** parancsmagot használja a parancsfájl-blokkokban és a `$_` az aktuális folyamat objektum lehetővé teszi, hogy a folyamat minden egyes objektumában parancsot futtató leíró. Ez bonyolult feladatok elvégzésére is használható.

Egy olyan helyzetet, ahol ez hasznos lehet, hogy több hasznos adat van módosítása. Például a Win32_LogicalDisk osztály a WMI segítségével minden helyi lemez szabad terület információkat ad vissza. Az ad vissza, tekintetében bájt, azonban, ami lehetővé teszi az nehezen olvasható:

```
PS> Get-WmiObject -Class Win32_LogicalDisk

DeviceID     : C:
DriveType    : 3
ProviderName :
FreeSpace    : 50665070592
Size         : 203912880128
VolumeName   : Local Disk
```

Azt is átalakítani a FreeSpace értéket (MB): az egyes értékek kétszer; elosztja 1024 az első osztás után az adatok kilobájtban, pedig a második osztás után azt (MB). Teheti, hogy egy ForEach-Object parancsfájlblokkban lévő beírásával:

```
PS> Get-WmiObject -Class Win32_LogicalDisk | ForEach-Object -Process {($_.FreeSpace)/1024.0/1024.0}
48318.01171875
```

Sajnos a kimenet mostantól adatok nincsenek társított címkével. A WMI-tulajdonságok írásvédettek, mivel FreeSpace közvetlenül nem konvertálhatóak. Írja be ezt:

```powershell
Get-WmiObject -Class Win32_LogicalDisk | ForEach-Object -Process {$_.FreeSpace = ($_.FreeSpace)/1024.0/1024.0}
```

Hibaüzenetet kap:

```output
"FreeSpace" is a ReadOnly property.
At line:1 char:70
+ Get-WmiObject -Class Win32_LogicalDisk | ForEach-Object -Process {$_.F <<<< r
eeSpace = ($_.FreeSpace)/1024.0/1024.0}
```

Néhány speciális technikák segítségével az adatok sikerült rendezhetők át, de egy egyszerűbb módszert hozhat létre egy új objektum használatával **Select-Object**.