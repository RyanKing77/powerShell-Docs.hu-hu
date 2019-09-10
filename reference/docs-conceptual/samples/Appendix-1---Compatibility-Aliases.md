---
ms.date: 09/09/2019
keywords: PowerShell, parancsmag
title: '1\. függelék: Kompatibilitási aliasok'
ms.openlocfilehash: 2351fdf23711fe1417f7e3fc3cca5b642d5a59fc
ms.sourcegitcommit: 00083f07b13c73b86936e7d7307397df27c63c04
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/10/2019
ms.locfileid: "70848160"
---
# <a name="appendix-1---compatibility-aliases"></a>1\. függelék – kompatibilitási aliasok

A PowerShell több aliast is tartalmaz, amelyek lehetővé teszik a **UNIX** és a **cmd. exe** felhasználók számára ismerős parancsok használatát.
A parancsok és a hozzájuk kapcsolódó PowerShell-parancsmagok és PowerShell-aliasok az alábbi táblázatban láthatók:

|cmd. exe parancs|UNIX-parancs|PowerShell-parancsmag|PowerShell-alias|
|---------------|----------------|--------------|------------|
|**CLS**|**egyértelmű**|`Clear-Host`függvény|`cls`|
|**másolja**|**CP**|`Copy-Item`|`cpi`|
|**dir**|**ls**|`Get-ChildItem`|`gci`|
|**type**|**cat**|`Get-Content`|`gc`|
|**áthelyezése**|**MV**|`Move-Item`|`mi`|
|**MD**|**mkdir**|`New-Item`|`ni`|
|**pushd**|**pushd**|`Push-Location`|`pushd`|
|**popd**|**popd**|`Pop-Location`|`popd`|
|**del**, **Törlés**, **Rd**, **rmdir**|**RM**|`Remove-Item`|`ri`|
|**Ren**|**MV**|`Rename-Item`|`rni`|
|**CD**, **chdir**|**CD**|`Set-Location`|`sl`|

A PowerShell-aliasok megkereséséhez használja a [Get-alias](/powershell/module/Microsoft.PowerShell.Utility/Get-Alias) parancsmagot. Egy parancsmag aliasnevének megjelenítéséhez használja a **definition** paramétert, és adja meg a parancsmag nevét.
Vagy az alias parancsmag nevének megkereséséhez használja a **Name** paramétert, és adja meg az aliast.

```powershell
Get-Alias -Definition Get-ChildItem
```

```Output
CommandType     Name
-----------     ----
Alias           dir -> Get-ChildItem
Alias           gci -> Get-ChildItem
Alias           ls -> Get-ChildItem
```

```powershell
Get-Alias -Name gci
```

```Output
CommandType     Name
-----------     ----
Alias           gci -> Get-ChildItem
```
