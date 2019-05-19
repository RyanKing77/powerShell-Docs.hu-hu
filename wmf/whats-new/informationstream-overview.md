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
# <a name="information-stream"></a>Információfolyam

PowerShell 5.0 hozzáad egy új strukturált **információk** adatfolyam továbbítására a strukturált adatok között egy parancsfájlt és a gazdagép. `Write-Host` kimenete kibocsátható is frissítettük a **információk** stream, most rögzítése és csend azt. Az új `Write-Information` használt parancsmag **InformationVariable** és **InformationAction** általános paraméterek lehetővé teszi, hogy nagyobb rugalmasságot és képességet.

A következő függvényt használja, amelyek kihasználják az új parancsmagok **információk** stream.

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

Az alábbi példák bemutatják, ez a függvény futtatásának eredményét.

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

A `$r` változó rendelkezik rögzíteni a Folyamatadatok a parancsfájl változóban `$p`.

```powershell
$r.Id
4008
```

Ellentétben a `Write-Host` parancsmag használatával a **InformationVariable** paraméterében `Write-Information` lehetővé teszi a kimeneti változóként rögzítését. Használatával a **címke**, az küldött üzenetek külön-külön csatornákat hozhat létre a **információk** stream.

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

Ha az üzenet küldése a **információk** stream, egy, az üzenet nem jelenik meg a gazdaalkalmazást, de lehet lekérni a címke neve. Például:

```powershell
$iv | where Tags -eq 'LogHigh'
```

```Output
Some important logging information
```