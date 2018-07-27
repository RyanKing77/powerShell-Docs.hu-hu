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
# <a name="reporting-on-jea"></a><span data-ttu-id="f6fbe-102">JEA-jelentések</span><span class="sxs-lookup"><span data-stu-id="f6fbe-102">Reporting on JEA</span></span>

<span data-ttu-id="f6fbe-103">Annak érdekében, hogy a jelentést a JEA konfigurációs állapotát, használhatja:</span><span class="sxs-lookup"><span data-stu-id="f6fbe-103">In order to report on the state of your JEA configuration, you can use:</span></span>

1. <span data-ttu-id="f6fbe-104">**Get-PSSessionConfiguration** regisztrálva végpontok az adott számítógépen az összes listáját adja vissza.</span><span class="sxs-lookup"><span data-stu-id="f6fbe-104">**Get-PSSessionConfiguration** to return a list of all registered endpoints on a given machine.</span></span>
2. <span data-ttu-id="f6fbe-105">**Get-PSSessionCapability** jelenti a képességekkel rendelkezik az adott felhasználó egy adott végpontnak.</span><span class="sxs-lookup"><span data-stu-id="f6fbe-105">**Get-PSSessionCapability** to report on the capabilities any given user has on a specific endpoint.</span></span>

<span data-ttu-id="f6fbe-106">Íme egy példa **Get-PSSessionCapability**:</span><span class="sxs-lookup"><span data-stu-id="f6fbe-106">Here's an example of **Get-PSSessionCapability**:</span></span>

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

<span data-ttu-id="f6fbe-107">A jelentés a _műveletek_ felhasználók JEA munkamenet során vett igénybe, használhatja:</span><span class="sxs-lookup"><span data-stu-id="f6fbe-107">To report on the _actions_ users took during a JEA session, you can:</span></span>

1. <span data-ttu-id="f6fbe-108">Engedélyezze az "over-the-váll" átiratok a JEA-végpont, és tekintse meg a szöveges könyvtár minden egyes felhasználói műveletek teljes naplók</span><span class="sxs-lookup"><span data-stu-id="f6fbe-108">Enable the "over-the-shoulder" transcripts for that JEA endpoint and consult the transcript directory for a full log of each user's actions</span></span>
2. <span data-ttu-id="f6fbe-109">Kapcsolja be a PowerShell-modul naplózást, és vizsgálja meg a PowerShell eseménynaplóit.</span><span class="sxs-lookup"><span data-stu-id="f6fbe-109">Turn on PowerShell module logging and inspect the PowerShell event logs.</span></span>