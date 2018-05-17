---
ms.date: 06/12/2017
contributor: manikb
keywords: gyűjtemény, a powershell, a parancsmag, a psget
title: A PowerShellGet telepítése
ms.openlocfilehash: 35be7d02ea856ea39218f05d32b43c60fa1bd53e
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/17/2018
---
# <a name="installing-powershellget"></a>A PowerShellGet telepítése

## <a name="powershellget-is-an-in-box-module-in-the-following-releases"></a>PowerShellGet az egy beépített modul, a következő kiadásokban

- [Windows 10](https://www.microsoft.com/windows/get-windows-10) vagy újabb verzió
- [Windows Server 2016](https://technet.microsoft.com/windows-server-docs/get-started/windows-server-2016) vagy újabb verzió
- [A Windows Management Framework (WMF) 5.0](https://www.microsoft.com/download/details.aspx?id=50395) vagy újabb verzió
- [PowerShell 6](https://github.com/PowerShell/PowerShell/releases)

## <a name="get-powershellget-module-for-powershell-versions-30-and-40"></a>PowerShell-verziók 3.0 és 4.0 PowerShellGet modul beolvasása

- [PackageManagement MSI](http://go.microsoft.com/fwlink/?LinkID=746217&clcid=0x409)

## <a name="get-the-latest-version-from-powershell-gallery"></a>A legújabb verzió letöltéséhez a PowerShell-galériából

- PowerShellGet frissítés előtti mindig telepítse a legújabb Nuget-szolgáltató. Ehhez futtassa a következő egy rendszergazda jogú PowerShell-munkamenetben.

```powershell
Install-PackageProvider Nuget –Force
Exit
```

### <a name="for-systems-with-powershell-50-or-newer-you-can-install-the-latest-powershellget"></a>A legújabb PowerShellGet telepítése rendszerekhez PowerShell 5.0 (vagy újabb)

- Ehhez a Windows 10, Windows Server 2016, a rendszer WMF 5.0 vagy telepített 5.1 vagy 6-os PowerShell, a rendszer a következő parancsokat egy rendszergazda jogú PowerShell-munkamenetben.

```powershell
Install-Module –Name PowerShellGet –Force
Exit
```

- Újabb verziókra frissítés-modul használható.

```powershell
Update-Module -Name PowerShellGet
Exit
```

### <a name="for-systems-running-powershell-3-or-powershell-4-that-have-installed-the-packagemanagement-msihttpgomicrosoftcomfwlinklinkid746217clcid0x409"></a>PowerShell 3 vagy PowerShell 4 operációs rendszer, hogy telepítette a [PackageManagement MSI](http://go.microsoft.com/fwlink/?LinkID=746217&clcid=0x409)

- Alább PowerShellGet parancsmagot egy rendszergazda jogú PowerShell-munkamenetben egy helyi könyvtárba menti a modulok használata

```powershell
Save-Module PowerShellGet -Path C:\LocalFolder
Exit
```

- Győződjön meg arról, hogy PowerShellGet és PackageManagment modulok nem töltődnek egyéb folyamatok.
- Törli a tartalmát `$env:ProgramFiles\WindowsPowerShell\Modules\PowerShellGet\` és `$env:ProgramFiles\WindowsPowerShell\Modules\PackageManagement\` mappák.
- Nyissa meg újra a PS-konzolt emelt szintű engedélyekkel, majd futtassa a következő parancsokat.

```powershell
Copy-Item "C:\LocalFolder\PowerShellGet\*" "$env:ProgramFiles\WindowsPowerShell\Modules\PowerShellGet\" -Recurse -Force
Copy-Item "C:\LocalFolder\PackageManagement\*" "$env:ProgramFiles\WindowsPowerShell\Modules\PackageManagement\" -Recurse -Force
```