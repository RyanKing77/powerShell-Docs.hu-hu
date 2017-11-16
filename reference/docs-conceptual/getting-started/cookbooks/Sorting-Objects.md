---
ms.date: 2017-06-05
keywords: PowerShell parancsmag
title: "Rendezési objektumok"
ms.assetid: 8530caa8-3ed4-4c56-aed7-1295dd9ba199
ms.openlocfilehash: 2df45c64656e74dc8b72957ce59f2a5e5ee663b6
ms.sourcegitcommit: 74255f0b5f386a072458af058a15240140acb294
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/03/2017
---
# <a name="sorting-objects"></a>Rendezési objektumok
Azt rendszerezheti könnyebb használatával megjelenített adatok a **rendezési-objektum** parancsmag. **Rendezés-objektum** rendezéshez egy vagy több tulajdonságának neve, és ezek a tulajdonságok értékeit rendezve adatait jeleníti meg.

Fontolja meg a probléma Win32_SystemDriver példányok listázása. Rendezés szeretnénk **állapot** és a majd **neve**, azt is megteheti beírásával:

```
Get-WmiObject -Class Win32_SystemDriver | Sort-Object -Property State,Name | Format-Table -Property Name,State,Started,DisplayName -AutoSize -Wrap
```

Bár ez hosszabb megjelenítésre, csoportosított állapotú elemek látható:

```
Name           State   Started DisplayName
----           -----   ------- -----------
ACPI           Running    True Microsoft ACPI Driver
AFD            Running    True AFD
AmdK7          Running    True AMD K7 Processor Driver
AsyncMac       Running    True RAS Asynchronous Media Driver
...
Abiosdsk       Stopped   False Abiosdsk
ACPIEC         Stopped   False ACPIEC
aec            Stopped   False Microsoft Kernel Acoustic Echo Canceller
...
```

Is rendezheti az objektumok fordított sorrendben megadásával a **csökkenő** paraméter. A rendezési sorrend Ezzel visszavonja, így fordított betűrendben rendezi a nevek és számok alapján vannak rendezve csökkenő mérete.

```
PS> Get-WmiObject -Class Win32_SystemDriver | Sort-Object -Property State,Name -Descending | Format-Table -Property Name,State,Started,DisplayName -AutoSize -Wrap

Name           State   Started DisplayName
----           -----   ------- -----------
WS2IFSL        Stopped   False Windows Socket 2.0 Non-IFS Service Provider Supp
                               ort Environment
wceusbsh       Stopped   False Windows CE USB Serial Host Driver...
...
wdmaud         Running    True Microsoft WINMM WDM Audio Compatibility Driver
Wanarp         Running    True Remote Access IP ARP Driver
...
```

