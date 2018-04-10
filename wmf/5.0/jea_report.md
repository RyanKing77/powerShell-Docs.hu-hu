---
ms.date: 06/12/2017
author: JKeithB
ms.topic: reference
keywords: WMF, powershell, beállítás
ms.openlocfilehash: 2af56be1915c148809f52cd9040c45da160ae0a2
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="reporting-on-jea"></a>JEA-jelentések
Ahhoz, hogy a jelentés a JEA konfigurációs állapotát, használhatja:
1.  **Get-PSSessionConfiguration** vissza az összes regisztrált végpontok az adott számítógépen.
2.  **Get-PSSessionCapability** képességeit jelentés az adott felhasználó számára egy adott végpont.

Íme egy példa **Get-PSSessionCapability**:
```powershell
Get-PSSessionCapability -ConfigurationName Maintenance -Username "CONTOSO\JohnDoe"

CommandType     Name                                               Version    Source
-----------     ----                                               -------    ------
Alias           clear -> Clear-Host
Alias           cls -> Clear-Host
Alias           exsn -> Exit-PSSession
Alias           gcm -> Get-Command
Alias           measure -> Measure-Object
Alias           select -> Select-Object
Function        Clear-Host
Function        Exit-PSSession
Function        Get-Command
Function        Get-FormatData
Function        Get-Help
Function        Get-UserInfo
Function        Measure-Object
Function        Out-Default
Function        Select-Object
Cmdlet          Restart-Service                                    3.0.0.0 Microsof...


```

A jelentés a _műveletek_ felhasználók tartott JEA munkamenet során, akkor is:
1. Engedélyezze az "over-az-a képernyőre pillant" ki, hogy JEA végpont, és tekintse át a Beszélgetés szövegének könyvtár az egyes felhasználói műveletek teljes naplók
2. PowerShell modul naplózás bekapcsolása, és vizsgálja meg a PowerShell eseménynaplóit.