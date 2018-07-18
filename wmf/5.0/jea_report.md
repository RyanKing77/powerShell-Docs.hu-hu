---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: 2fb2e4b0c40322b5ec78fabede22a7e3ecbbd2aa
ms.sourcegitcommit: 77f62a55cac8c13d69d51eef5fade18f71d66955
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/17/2018
ms.locfileid: "39093762"
---
# <a name="reporting-on-jea"></a>JEA-jelentések

Annak érdekében, hogy a jelentést a JEA konfigurációs állapotát, használhatja:

1. **Get-PSSessionConfiguration** regisztrálva végpontok az adott számítógépen az összes listáját adja vissza.
1. **Get-PSSessionCapability** jelenti a képességekkel rendelkezik az adott felhasználó egy adott végpontnak.

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
