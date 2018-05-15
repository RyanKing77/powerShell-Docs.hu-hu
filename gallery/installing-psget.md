---
ms.date: 06/12/2017
contributor: manikb
ms.topic: reference
keywords: gyűjtemény, a powershell, a parancsmag, a psget
title: PowerShellGet telepítése
ms.openlocfilehash: 6190c7caee61b43e70073ff7b30f867a901d3042
ms.sourcegitcommit: e9ad4d85fd7eb72fb5bc37f6ca3ae1282ae3c6d7
ms.contentlocale: hu-HU
ms.lasthandoff: 05/10/2018
---
# <a name="get-powershellget-module"></a><span data-ttu-id="68bf0-103">PowerShellGet modul beolvasása</span><span class="sxs-lookup"><span data-stu-id="68bf0-103">Get PowerShellGet module</span></span>

## <a name="powershellget-is-an-in-box-module-in-the-following-releases"></a><span data-ttu-id="68bf0-104">PowerShellGet az egy beépített modul, a következő kiadásokban</span><span class="sxs-lookup"><span data-stu-id="68bf0-104">PowerShellGet is an in-box module in the following releases</span></span>

- <span data-ttu-id="68bf0-105">[Windows 10](https://www.microsoft.com/windows/get-windows-10) vagy újabb verzió</span><span class="sxs-lookup"><span data-stu-id="68bf0-105">[Windows 10](https://www.microsoft.com/windows/get-windows-10) or newer</span></span>
- <span data-ttu-id="68bf0-106">[Windows Server 2016](https://technet.microsoft.com/windows-server-docs/get-started/windows-server-2016) vagy újabb verzió</span><span class="sxs-lookup"><span data-stu-id="68bf0-106">[Windows Server 2016](https://technet.microsoft.com/windows-server-docs/get-started/windows-server-2016) or newer</span></span>
- <span data-ttu-id="68bf0-107">[A Windows Management Framework (WMF) 5.0](https://www.microsoft.com/download/details.aspx?id=50395) vagy újabb verzió</span><span class="sxs-lookup"><span data-stu-id="68bf0-107">[Windows Management Framework (WMF) 5.0](https://www.microsoft.com/download/details.aspx?id=50395) or newer</span></span>
- [<span data-ttu-id="68bf0-108">PowerShell 6</span><span class="sxs-lookup"><span data-stu-id="68bf0-108">PowerShell 6</span></span>](https://github.com/PowerShell/PowerShell/releases)

## <a name="get-powershellget-module-for-powershell-versions-30-and-40"></a><span data-ttu-id="68bf0-109">PowerShell-verziók 3.0 és 4.0 PowerShellGet modul beolvasása</span><span class="sxs-lookup"><span data-stu-id="68bf0-109">Get PowerShellGet module for PowerShell versions 3.0 and 4.0</span></span>

- [<span data-ttu-id="68bf0-110">PackageManagement MSI</span><span class="sxs-lookup"><span data-stu-id="68bf0-110">PackageManagement MSI</span></span>](http://go.microsoft.com/fwlink/?LinkID=746217&clcid=0x409)

## <a name="get-the-latest-version-from-powershell-gallery"></a><span data-ttu-id="68bf0-111">A legújabb verzió letöltéséhez a PowerShell-galériából</span><span class="sxs-lookup"><span data-stu-id="68bf0-111">Get the latest version from PowerShell Gallery</span></span>

- <span data-ttu-id="68bf0-112">PowerShellGet frissítés előtti mindig telepítse a legújabb Nuget-szolgáltató.</span><span class="sxs-lookup"><span data-stu-id="68bf0-112">Before updating PowerShellGet, you should always install the latest Nuget provider.</span></span> <span data-ttu-id="68bf0-113">Ehhez futtassa a következő egy rendszergazda jogú PowerShell-munkamenetben.</span><span class="sxs-lookup"><span data-stu-id="68bf0-113">To do that, run the following in an elevated PowerShell session.</span></span>

```powershell
Install-PackageProvider Nuget –Force
Exit
```

### <a name="for-systems-with-powershell-50-or-newer-you-can-install-the-latest-powershellget"></a><span data-ttu-id="68bf0-114">A legújabb PowerShellGet telepítése rendszerekhez PowerShell 5.0 (vagy újabb)</span><span class="sxs-lookup"><span data-stu-id="68bf0-114">For systems with PowerShell 5.0 (or newer) you can install the latest PowerShellGet</span></span>

- <span data-ttu-id="68bf0-115">Ehhez a Windows 10, Windows Server 2016, a rendszer WMF 5.0 vagy telepített 5.1 vagy 6-os PowerShell, a rendszer a következő parancsokat egy rendszergazda jogú PowerShell-munkamenetben.</span><span class="sxs-lookup"><span data-stu-id="68bf0-115">To do this on Windows 10, Windows Server 2016, any system with WMF 5.0 or 5.1 installed, or any system with PowerShell 6, run the following commands from an elevated PowerShell session.</span></span>

```powershell
Install-Module –Name PowerShellGet –Force
Exit
```

- <span data-ttu-id="68bf0-116">Újabb verziókra frissítés-modul használható.</span><span class="sxs-lookup"><span data-stu-id="68bf0-116">Use Update-Module to get newer versions.</span></span>

```powershell
Update-Module -Name PowerShellGet
Exit
```

### <a name="for-systems-running-powershell-3-or-powershell-4-that-have-installed-the-packagemanagement-msihttpgomicrosoftcomfwlinklinkid746217clcid0x409"></a><span data-ttu-id="68bf0-117">PowerShell 3 vagy PowerShell 4 operációs rendszer, hogy telepítette a [PackageManagement MSI](http://go.microsoft.com/fwlink/?LinkID=746217&clcid=0x409)</span><span class="sxs-lookup"><span data-stu-id="68bf0-117">For systems running PowerShell 3 or PowerShell 4, that have installed the [PackageManagement MSI](http://go.microsoft.com/fwlink/?LinkID=746217&clcid=0x409)</span></span>

- <span data-ttu-id="68bf0-118">Alább PowerShellGet parancsmagot egy rendszergazda jogú PowerShell-munkamenetben egy helyi könyvtárba menti a modulok használata</span><span class="sxs-lookup"><span data-stu-id="68bf0-118">Use below PowerShellGet cmdlet from an elevated PowerShell session to save the modules to a local directory</span></span>

```powershell
Save-Module PowerShellGet -Path C:\LocalFolder
Exit
```

- <span data-ttu-id="68bf0-119">Győződjön meg arról, hogy PowerShellGet és PackageManagment modulok nem töltődnek egyéb folyamatok.</span><span class="sxs-lookup"><span data-stu-id="68bf0-119">Ensure that PowerShellGet and PackageManagment modules are not loaded in any other processes.</span></span>
- <span data-ttu-id="68bf0-120">Törli a tartalmát `$env:ProgramFiles\WindowsPowerShell\Modules\PowerShellGet\` és `$env:ProgramFiles\WindowsPowerShell\Modules\PackageManagement\` mappák.</span><span class="sxs-lookup"><span data-stu-id="68bf0-120">Delete contents of `$env:ProgramFiles\WindowsPowerShell\Modules\PowerShellGet\` and  `$env:ProgramFiles\WindowsPowerShell\Modules\PackageManagement\` folders.</span></span>
- <span data-ttu-id="68bf0-121">Nyissa meg újra a PS-konzolt emelt szintű engedélyekkel, majd futtassa a következő parancsokat.</span><span class="sxs-lookup"><span data-stu-id="68bf0-121">Re-open the PS Console with elevated permissions then run the following commands.</span></span>

```powershell
Copy-Item "C:\LocalFolder\PowerShellGet\*" "$env:ProgramFiles\WindowsPowerShell\Modules\PowerShellGet\" -Recurse -Force
Copy-Item "C:\LocalFolder\PackageManagement\*" "$env:ProgramFiles\WindowsPowerShell\Modules\PackageManagement\" -Recurse -Force
```