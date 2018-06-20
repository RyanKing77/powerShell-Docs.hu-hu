---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: 7982acc111e95b4167f948314f176d53f39d3620
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/17/2018
ms.locfileid: "34218722"
---
# <a name="reporting-on-jea"></a><span data-ttu-id="6da6f-102">JEA-jelentések</span><span class="sxs-lookup"><span data-stu-id="6da6f-102">Reporting on JEA</span></span>
<span data-ttu-id="6da6f-103">Ahhoz, hogy a jelentés a JEA konfigurációs állapotát, használhatja:</span><span class="sxs-lookup"><span data-stu-id="6da6f-103">In order to report on the state of your JEA configuration, you can use:</span></span>
1.  <span data-ttu-id="6da6f-104">**Get-PSSessionConfiguration** vissza az összes regisztrált végpontok az adott számítógépen.</span><span class="sxs-lookup"><span data-stu-id="6da6f-104">**Get-PSSessionConfiguration** to return a list of all registered endpoints on a given machine.</span></span>
2.  <span data-ttu-id="6da6f-105">**Get-PSSessionCapability** képességeit jelentés az adott felhasználó számára egy adott végpont.</span><span class="sxs-lookup"><span data-stu-id="6da6f-105">**Get-PSSessionCapability** to report on the capabilities any given user has on a specific endpoint.</span></span>

<span data-ttu-id="6da6f-106">Íme egy példa **Get-PSSessionCapability**:</span><span class="sxs-lookup"><span data-stu-id="6da6f-106">Here’s an example of **Get-PSSessionCapability**:</span></span>
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

<span data-ttu-id="6da6f-107">A jelentés a _műveletek_ felhasználók tartott JEA munkamenet során, akkor is:</span><span class="sxs-lookup"><span data-stu-id="6da6f-107">To report on the _actions_ users took during a JEA session, you can:</span></span>
1. <span data-ttu-id="6da6f-108">Engedélyezze az "over-az-a képernyőre pillant" ki, hogy JEA végpont, és tekintse át a Beszélgetés szövegének könyvtár az egyes felhasználói műveletek teljes naplók</span><span class="sxs-lookup"><span data-stu-id="6da6f-108">Enable the "over-the-shoulder" transcripts for that JEA endpoint and consult the transcript directory for a full log of each user's actions</span></span>
2. <span data-ttu-id="6da6f-109">PowerShell modul naplózás bekapcsolása, és vizsgálja meg a PowerShell eseménynaplóit.</span><span class="sxs-lookup"><span data-stu-id="6da6f-109">Turn on PowerShell module logging and inspect the PowerShell event logs.</span></span>
