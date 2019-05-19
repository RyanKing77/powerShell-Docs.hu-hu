---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
title: Információfolyam
ms.openlocfilehash: c54603cf0dd4f0b69f8147620130f9f29bc3e5ec
ms.sourcegitcommit: 01b81317029b28dd9b61d167045fd31f1ec7bc06
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/17/2019
ms.locfileid: "65856384"
---
# <a name="information-stream"></a><span data-ttu-id="6baff-103">Információfolyam</span><span class="sxs-lookup"><span data-stu-id="6baff-103">Information Stream</span></span>

<span data-ttu-id="6baff-104">PowerShell 5.0 hozzáad egy új strukturált **információk** adatfolyam továbbítására a strukturált adatok között egy parancsfájlt és a gazdagép.</span><span class="sxs-lookup"><span data-stu-id="6baff-104">PowerShell 5.0 adds a new structured **Information** stream to transmit structured data between a script and its host.</span></span> <span data-ttu-id="6baff-105">`Write-Host` kimenete kibocsátható is frissítettük a **információk** stream, most rögzítése és csend azt.</span><span class="sxs-lookup"><span data-stu-id="6baff-105">`Write-Host` has also been updated to emit its output to the **Information** stream where you can now capture or silence it.</span></span> <span data-ttu-id="6baff-106">Az új `Write-Information` használt parancsmag **InformationVariable** és **InformationAction** általános paraméterek lehetővé teszi, hogy nagyobb rugalmasságot és képességet.</span><span class="sxs-lookup"><span data-stu-id="6baff-106">The new `Write-Information` cmdlet used with **InformationVariable** and **InformationAction** common parameters enables more flexibility and capability.</span></span>

<span data-ttu-id="6baff-107">A következő függvényt használja, amelyek kihasználják az új parancsmagok **információk** stream.</span><span class="sxs-lookup"><span data-stu-id="6baff-107">The following function uses cmdlets that take advantage of the new **Information** stream.</span></span>

```powershell
function OutputGusher {
  [CmdletBinding()]
  param()
  Write-Host -ForegroundColor Green 'Preparing to give you output!'
  Write-Host '============================='
  Write-Host 'I ' -ForegroundColor White -NoNewline
  Write-Host '<3 ' -ForegroundColor Red -NoNewline
  Write-Host 'Output' -ForegroundColor White
  Write-Host '============================='

  $p = Get-Process -id $pid
  $p

  Write-Information $p -Tag Process
  Write-Information 'Some spammy logging information' -Tag LogLow
  Write-Information 'Some important logging information' -Tag LogHigh

  Write-Host
  Write-Host -ForegroundColor Green 'SCRIPT COMPLETE!!'
}
```

<span data-ttu-id="6baff-108">Az alábbi példák bemutatják, ez a függvény futtatásának eredményét.</span><span class="sxs-lookup"><span data-stu-id="6baff-108">The following examples show the results of running this function.</span></span>

```powershell
$r = c:\temp\OutputGusher
```

```Output
Preparing to give you output!
=============================
I <3 Output
=============================

SCRIPT COMPLETE!!
```

<span data-ttu-id="6baff-109">A `$r` változó rendelkezik rögzíteni a Folyamatadatok a parancsfájl változóban `$p`.</span><span class="sxs-lookup"><span data-stu-id="6baff-109">The `$r` variable has captured the process information in the script variable `$p`.</span></span>

```powershell
$r.Id
4008
```

<span data-ttu-id="6baff-110">Ellentétben a `Write-Host` parancsmag használatával a **InformationVariable** paraméterében `Write-Information` lehetővé teszi a kimeneti változóként rögzítését.</span><span class="sxs-lookup"><span data-stu-id="6baff-110">Unlike the `Write-Host` cmdlet, using the **InformationVariable** parameter of `Write-Information` allows you to capture the output in a variable.</span></span> <span data-ttu-id="6baff-111">Használatával a **címke**, az küldött üzenetek külön-külön csatornákat hozhat létre a **információk** stream.</span><span class="sxs-lookup"><span data-stu-id="6baff-111">Using the **Tag**, you can create separate channels for message sent to the **Information** stream.</span></span>

```powershell
$r = OutputGusher -InformationVariable iv
$ivOutput = $iv | Group-Object -AsHash { $_.Tags[0] } -AsString
$ivOutput
```

```Output
Preparing to give you output!
=============================
I <3 Output
=============================
SCRIPT COMPLETE!!

Name                 Value
----                 -----
LogLow               {Some spammy logging information}
LogHigh              {Some important logging information}
Process              {System.Diagnostics.Process (powershell)}
PSHOST               {Preparing to give you output!, =============================, I , <3 ...}
```

<span data-ttu-id="6baff-112">Ha az üzenet küldése a **információk** stream, egy, az üzenet nem jelenik meg a gazdaalkalmazást, de lehet lekérni a címke neve.</span><span class="sxs-lookup"><span data-stu-id="6baff-112">When you send a message to the **Information** stream with a tag, that message is not displayed in the host application but can be retrieved using the tag name.</span></span> <span data-ttu-id="6baff-113">Például:</span><span class="sxs-lookup"><span data-stu-id="6baff-113">For example:</span></span>

```powershell
$iv | where Tags -eq 'LogHigh'
```

```Output
Some important logging information
```