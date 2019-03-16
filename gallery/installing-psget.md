---
ms.date: 06/12/2017
contributor: manikb
keywords: katalógus, powershell, a parancsmag, psget
title: A PowerShellGet telepítése
ms.openlocfilehash: 23a53a9117c9f6a7ad157b635cd7ff4b3b3444c5
ms.sourcegitcommit: caac7d098a448232304c9d6728e7340ec7517a71
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/16/2019
ms.locfileid: "58054824"
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

- Győződjön meg arról, hogy a PowerShellGet és a PackageManagement-modulok nem töltődnek be más folyamatokban.
- Törli a tartalmát `$env:ProgramFiles\WindowsPowerShell\Modules\PowerShellGet\` és `$env:ProgramFiles\WindowsPowerShell\Modules\PackageManagement\` mappákat.
- Nyissa meg újra a PS-konzol emelt szintű engedélyekkel, majd futtassa a következő parancsokat.

  ```powershell
  Copy-Item "C:\LocalFolder\PowerShellGet\*" "$env:ProgramFiles\WindowsPowerShell\Modules\PowerShellGet\" -Recurse -Force
  Copy-Item "C:\LocalFolder\PackageManagement\*" "$env:ProgramFiles\WindowsPowerShell\Modules\PackageManagement\" -Recurse -Force
  ```
