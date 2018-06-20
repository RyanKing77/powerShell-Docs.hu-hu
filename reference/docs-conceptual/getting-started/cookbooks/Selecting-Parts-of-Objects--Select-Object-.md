---
ms.date: 06/05/2017
keywords: PowerShell parancsmag
title: Objektumok kiválasztásával részét jelölje ki az objektumot
ms.assetid: 72e64b1a-d351-4500-9da3-24d8a71d7a92
ms.openlocfilehash: 323c57ba4462e20d9713fb74732989584f5a993f
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
ms.locfileid: "30953888"
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