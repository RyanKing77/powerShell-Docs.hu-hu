---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: Objektumrészek objektum kijelölése
ms.assetid: 72e64b1a-d351-4500-9da3-24d8a71d7a92
ms.openlocfilehash: 323c57ba4462e20d9713fb74732989584f5a993f
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55684513"
---
# <a name="selecting-parts-of-objects-select-object"></a>Objektumrészek (Select-Object)

Használhatja a **Select-Object** parancsmaggal hozhat létre, azokat az objektumokat a kiválasztott tulajdonságokat tartalmazó új, egyéni Windows PowerShell-objektumok létrehozásához. Írja be a következő parancsot egy új objektum, amely csak a nevét és FreeSpace tulajdonságok a Win32_LogicalDisk WMI-osztály tartalmazza:

```
PS> Get-WmiObject -Class Win32_LogicalDisk | Select-Object -Property Name,FreeSpace

Name                                    FreeSpace
----                                    ---------
C:                                      50664845312
```

Az adatok típusát, hogy a parancs kiadása után nem látható, de azt az eredményt a Get-Member kanálu után a Select-Object, ha, hogy egy új típusú objektumot, egy PSCustomObject feliratból:

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

Select-Object számos célra rendelkezik. Adatok, amelyek ezt követően módosíthatja az egyiket áll replikálás alatt. Most már tudjuk képes kezelni az előző szakaszban ütköztünk a problémát. Az újonnan létrehozott objektumok is frissítjük, FreeSpace értékét, és a kimenet tartalmazza a leíró:

```
Get-WmiObject -Class Win32_LogicalDisk | Select-Object -Property Name,FreeSpace | ForEach-Object -Process {$_.FreeSpace = ($_.FreeSpace)/1024.0/1024.0; $_}
Name                                                                  FreeSpace
----                                                                  ---------
C:                                                                48317.7265625
```