---
ms.date: 06/12/2017
contributor: manikb
keywords: Galéria, PowerShell, parancsmag, psget
title: A PowerShellGet telepítése
ms.openlocfilehash: 2d3ba8c4d4d4c7ee023c7e6a948a29d8f47ea242
ms.sourcegitcommit: 8d47eb41445ffaf10fcd68874e397c9a1703d898
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/29/2019
ms.locfileid: "68601419"
---
# <a name="installing-powershellget"></a>A PowerShellGet telepítése

## <a name="powershellget-is-an-in-box-module-in-the-following-releases"></a>A PowerShellGet egy beépített modul a következő kiadásokban

- [Windows 10](https://www.microsoft.com/windows) vagy újabb
- [Windows Server 2016](/windows-server/windows-server) vagy újabb
- [Windows Management Framework (WMF) 5,0](https://www.microsoft.com/download/details.aspx?id=50395) vagy újabb
- [PowerShell 6](https://github.com/PowerShell/PowerShell/releases)

## <a name="get-powershellget-module-for-powershell-versions-30-and-40"></a>PowerShellGet-modul beszerzése a PowerShell 3,0-es és 4,0-es verzióihoz

- [PackageManagement MSI](https://www.microsoft.com/download/details.aspx?id=51451)

## <a name="get-the-latest-version-from-powershell-gallery"></a>A legújabb verzió letöltése PowerShell-galéria

- A PowerShellGet frissítése előtt mindig telepítse a legújabb Nuget-szolgáltatót. Ehhez futtassa a következőt egy emelt szintű PowerShell-munkamenetben.

  ```powershell
  Install-PackageProvider Nuget -Force
  Exit
  ```

### <a name="for-systems-with-powershell-50-or-newer-you-can-install-the-latest-powershellget"></a>A PowerShell 5,0 (vagy újabb) rendszerekkel rendelkező rendszerek esetében telepítheti a legújabb PowerShellGet

- Ezt a Windows 10, a Windows Server 2016, a WMF 5,0 vagy 5,1 rendszerű, illetve a PowerShell 6-os verzióval rendelkező rendszerek esetén futtassa a következő parancsokat egy emelt szintű PowerShell-munkamenetből.

  ```powershell
  Install-Module -Name PowerShellGet -Force
  Exit
  ```

- Újabb `Update-Module` verziók beszerzéséhez használja a következőt:.

  ```powershell
  Update-Module -Name PowerShellGet
  Exit
  ```

### <a name="for-systems-running-powershell-3-or-powershell-4-that-have-installed-the-packagemanagement-msihttpswwwmicrosoftcomdownloaddetailsaspxid51451"></a>A PowerShell 3 vagy PowerShell 4 rendszert futtató rendszerek esetében, amelyek telepítették a [PACKAGEMANAGEMENT MSI](https://www.microsoft.com/download/details.aspx?id=51451) -t

- Az alábbi PowerShellGet-parancsmagot egy emelt szintű PowerShell-munkamenetből használva mentse a modulokat egy helyi könyvtárba.

  ```powershell
  Save-Module PowerShellGet -Path C:\LocalFolder
  Exit
  ```

- Győződjön meg arról, hogy a PowerShellGet és a PackageManagement modulok nincsenek betöltve más folyamatokban.
- A és `$env:ProgramFiles\WindowsPowerShell\Modules\PowerShellGet\` `$env:ProgramFiles\WindowsPowerShell\Modules\PackageManagement\` a mappák tartalmának törlése.
- Nyissa meg újra a PS-konzolt emelt szintű engedélyekkel, majd futtassa a következő parancsokat.

  ```powershell
  Copy-Item "C:\LocalFolder\PowerShellGet\*" "$env:ProgramFiles\WindowsPowerShell\Modules\PowerShellGet\" -Recurse -Force
  Copy-Item "C:\LocalFolder\PackageManagement\*" "$env:ProgramFiles\WindowsPowerShell\Modules\PackageManagement\" -Recurse -Force
  ```
