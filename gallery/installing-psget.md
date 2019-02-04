---
ms.date: 06/12/2017
contributor: manikb
keywords: katalógus, powershell, a parancsmag, psget
title: A PowerShellGet telepítése
ms.openlocfilehash: 5c51cb1c7ea2538cc5f8503ce6c5d80edda70e15
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55683876"
---
# <a name="installing-powershellget"></a>A PowerShellGet telepítése

## <a name="powershellget-is-an-in-box-module-in-the-following-releases"></a>A PowerShellGet a következő kiadásokban a beépített modul létrehozása

- [Windows 10-es](https://www.microsoft.com/windows) vagy újabb
- [A Windows Server 2016](/windows-server/windows-server) vagy újabb
- [Windows Management Framework (WMF) 5.0](https://www.microsoft.com/download/details.aspx?id=50395) vagy újabb
- [PowerShell 6](https://github.com/PowerShell/PowerShell/releases)

## <a name="get-powershellget-module-for-powershell-versions-30-and-40"></a>PowerShell-verziók 3.0 és 4.0-s verzióját a PowerShellGet modul beolvasása

- [PackageManagement MSI](https://www.microsoft.com/download/details.aspx?id=51451)

## <a name="get-the-latest-version-from-powershell-gallery"></a>PowerShell-galériából a legújabb verzió letöltése

- A PowerShellGet-frissítése előtt mindig a legújabb Nuget-szolgáltató kell telepítenie. Ehhez futtassa a következőt egy emelt szintű PowerShell-munkamenetet.

  ```powershell
  Install-PackageProvider Nuget –Force
  Exit
  ```

### <a name="for-systems-with-powershell-50-or-newer-you-can-install-the-latest-powershellget"></a>A legújabb PowerShellGet telepítése a PowerShell 5.0-s (vagy újabb) rendszerekhez

- Ehhez a Windows 10, Windows Server 2016, bármilyen rendszer WMF 5.0-s vagy 5.1 telepítve vagy bármely PowerShell 6-os, a rendszer a következő parancsokat egy emelt szintű PowerShell-munkamenetből.

  ```powershell
  Install-Module –Name PowerShellGet –Force
  Exit
  ```

- Használat `Update-Module` beolvasni az újabb verziók.

  ```powershell
  Update-Module -Name PowerShellGet
  Exit
  ```

### <a name="for-systems-running-powershell-3-or-powershell-4-that-have-installed-the-packagemanagement-msihttpswwwmicrosoftcomdownloaddetailsaspxid51451"></a>PowerShell 3 vagy 4 operációs rendszer, hogy telepítette a [PackageManagement MSI](https://www.microsoft.com/download/details.aspx?id=51451)

- Használja a PowerShellGet parancsmagot egy emelt szintű PowerShell-munkamenetből a modulok egy helyi könyvtárba menteni

  ```powershell
  Save-Module PowerShellGet -Path C:\LocalFolder
  Exit
  ```

- Győződjön meg arról, hogy a PowerShellGet és PackageManagment modulok nem töltődnek be más folyamatokban.
- Törli a tartalmát `$env:ProgramFiles\WindowsPowerShell\Modules\PowerShellGet\` és `$env:ProgramFiles\WindowsPowerShell\Modules\PackageManagement\` mappákat.
- Nyissa meg újra a PS-konzol emelt szintű engedélyekkel, majd futtassa a következő parancsokat.

  ```powershell
  Copy-Item "C:\LocalFolder\PowerShellGet\*" "$env:ProgramFiles\WindowsPowerShell\Modules\PowerShellGet\" -Recurse -Force
  Copy-Item "C:\LocalFolder\PackageManagement\*" "$env:ProgramFiles\WindowsPowerShell\Modules\PackageManagement\" -Recurse -Force
  ```
