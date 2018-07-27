---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: cd3338ae305896e282056a871974e5f899ef6ff5
ms.sourcegitcommit: c3f1a83b59484651119630f3089aa51b6e7d4c3c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/26/2018
ms.locfileid: "39268578"
---
# <a name="reporting-on-jea"></a>JEA-jelentések

Annak érdekében, hogy a jelentést a JEA konfigurációs állapotát, használhatja:

1. **Get-PSSessionConfiguration** regisztrálva végpontok az adott számítógépen az összes listáját adja vissza.
2. **Get-PSSessionCapability** jelenti a képességekkel rendelkezik az adott felhasználó egy adott végpontnak.

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

A jelentés a _műveletek_ felhasználók JEA munkamenet során vett igénybe, használhatja:

1. Engedélyezze az "over-the-váll" átiratok a JEA-végpont, és tekintse meg a szöveges könyvtár minden egyes felhasználói műveletek teljes naplók
2. Kapcsolja be a PowerShell-modul naplózást, és vizsgálja meg a PowerShell eseménynaplóit.