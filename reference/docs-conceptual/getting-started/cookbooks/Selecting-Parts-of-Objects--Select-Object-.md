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
# <a name="selecting-parts-of-objects-select-object"></a>Objektumok (Select-Object) részek kijelölése
Használhatja a **Select-Object** parancsmaggal hozzon létre új, egyéni ki az objektumokat hozhat létre, azokat a tulajdonságokat tartalmazó Windows PowerShell objektumokra. A következő paranccsal hozzon létre egy új objektumot, amely tartalmazza az csak a nevét és FreeSpace a Win32_LogicalDisk WMI-osztály tulajdonságai:

```
PS> Get-WmiObject -Class Win32_LogicalDisk | Select-Object -Property Name,FreeSpace

Name                                    FreeSpace
----                                    ---------
C:                                      50664845312
```

Az adatok típusa nem látható, hogy a parancs kiadása után, de ha a Get-tag eredmény után a Select-Object csövön keresztüli, állapítható meg, hogy rendelkezik-e új típusú objektum, egy PSCustomObject:

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

Select-Object számos felhasználása van. Az egyik legyen replikálódik adatokat, majd módosíthatja. Azt már tudja kezelni a problémát az előző szakaszban miatt. Azt is FreeSpace értékét az újonnan létrehozott objektumokat a frissítést, és a kimenet tartalmazza a leíró nevet:

```
Get-WmiObject -Class Win32_LogicalDisk | Select-Object -Property Name,FreeSpace | ForEach-Object -Process {$_.FreeSpace = ($_.FreeSpace)/1024.0/1024.0; $_}
Name                                                                  FreeSpace
----                                                                  ---------
C:                                                                48317.7265625
```

