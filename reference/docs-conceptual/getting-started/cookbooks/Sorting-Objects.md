---
ms.date: 06/05/2017
keywords: PowerShell parancsmag
title: Objektumok rendezése
ms.assetid: 8530caa8-3ed4-4c56-aed7-1295dd9ba199
ms.openlocfilehash: 272d550a67b206f9924ebe143eca2f5906c0a304
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
ms.locfileid: "30949978"
---
# <a name="sorting-objects"></a>Objektumok rendezése

Azt rendszerezheti könnyebb használatával megjelenített adatok a **rendezési-objektum** parancsmag. **Rendezés-objektum** rendezéshez egy vagy több tulajdonságának neve, és ezek a tulajdonságok értékeit rendezve adatait jeleníti meg.

Fontolja meg a probléma Win32_SystemDriver példányok listázása. Rendezés szeretnénk **állapot** és a majd **neve**, azt is megteheti beírásával:

```powershell
Get-WmiObject -Class Win32_SystemDriver | Sort-Object -Property State,Name | Format-Table -Property Name,State,Started,DisplayName -AutoSize -Wrap
```

Bár ez hosszabb megjelenítésre, csoportosított állapotú elemek látható:

```output
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