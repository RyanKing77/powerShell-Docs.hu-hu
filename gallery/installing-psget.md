---
ms.date: 06/12/2017
contributor: manikb
keywords: katalógus, powershell, a parancsmag, psget
title: A PowerShellGet telepítése
ms.openlocfilehash: 23a53a9117c9f6a7ad157b635cd7ff4b3b3444c5
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62075273"
---
# <a name="installing-powershellget"></a><span data-ttu-id="52038-103">A PowerShellGet telepítése</span><span class="sxs-lookup"><span data-stu-id="52038-103">Installing PowerShellGet</span></span>

## <a name="powershellget-is-an-in-box-module-in-the-following-releases"></a><span data-ttu-id="52038-104">A PowerShellGet a következő kiadásokban a beépített modul létrehozása</span><span class="sxs-lookup"><span data-stu-id="52038-104">PowerShellGet is an in-box module in the following releases</span></span>

- <span data-ttu-id="52038-105">[Windows 10-es](https://www.microsoft.com/windows) vagy újabb</span><span class="sxs-lookup"><span data-stu-id="52038-105">[Windows 10](https://www.microsoft.com/windows) or newer</span></span>
- <span data-ttu-id="52038-106">[A Windows Server 2016](/windows-server/windows-server) vagy újabb</span><span class="sxs-lookup"><span data-stu-id="52038-106">[Windows Server 2016](/windows-server/windows-server) or newer</span></span>
- <span data-ttu-id="52038-107">[Windows Management Framework (WMF) 5.0](https://www.microsoft.com/download/details.aspx?id=50395) vagy újabb</span><span class="sxs-lookup"><span data-stu-id="52038-107">[Windows Management Framework (WMF) 5.0](https://www.microsoft.com/download/details.aspx?id=50395) or newer</span></span>
- [<span data-ttu-id="52038-108">PowerShell 6</span><span class="sxs-lookup"><span data-stu-id="52038-108">PowerShell 6</span></span>](https://github.com/PowerShell/PowerShell/releases)

## <a name="get-powershellget-module-for-powershell-versions-30-and-40"></a><span data-ttu-id="52038-109">PowerShell-verziók 3.0 és 4.0-s verzióját a PowerShellGet modul beolvasása</span><span class="sxs-lookup"><span data-stu-id="52038-109">Get PowerShellGet module for PowerShell versions 3.0 and 4.0</span></span>

- [<span data-ttu-id="52038-110">PackageManagement MSI</span><span class="sxs-lookup"><span data-stu-id="52038-110">PackageManagement MSI</span></span>](https://www.microsoft.com/download/details.aspx?id=51451)

## <a name="get-the-latest-version-from-powershell-gallery"></a><span data-ttu-id="52038-111">PowerShell-galériából a legújabb verzió letöltése</span><span class="sxs-lookup"><span data-stu-id="52038-111">Get the latest version from PowerShell Gallery</span></span>

- <span data-ttu-id="52038-112">A PowerShellGet-frissítése előtt mindig a legújabb Nuget-szolgáltató kell telepítenie.</span><span class="sxs-lookup"><span data-stu-id="52038-112">Before updating PowerShellGet, you should always install the latest Nuget provider.</span></span> <span data-ttu-id="52038-113">Ehhez futtassa a következőt egy emelt szintű PowerShell-munkamenetet.</span><span class="sxs-lookup"><span data-stu-id="52038-113">To do that, run the following in an elevated PowerShell session.</span></span>

  ```powershell
  Install-PackageProvider Nuget –Force
  Exit
  ```

### <a name="for-systems-with-powershell-50-or-newer-you-can-install-the-latest-powershellget"></a><span data-ttu-id="52038-114">A legújabb PowerShellGet telepítése a PowerShell 5.0-s (vagy újabb) rendszerekhez</span><span class="sxs-lookup"><span data-stu-id="52038-114">For systems with PowerShell 5.0 (or newer) you can install the latest PowerShellGet</span></span>

- <span data-ttu-id="52038-115">Ehhez a Windows 10, Windows Server 2016, bármilyen rendszer WMF 5.0-s vagy 5.1 telepítve vagy bármely PowerShell 6-os, a rendszer a következő parancsokat egy emelt szintű PowerShell-munkamenetből.</span><span class="sxs-lookup"><span data-stu-id="52038-115">To do this on Windows 10, Windows Server 2016, any system with WMF 5.0 or 5.1 installed, or any system with PowerShell 6, run the following commands from an elevated PowerShell session.</span></span>

  ```powershell
  Install-Module –Name PowerShellGet –Force
  Exit
  ```

- <span data-ttu-id="52038-116">Használat `Update-Module` beolvasni az újabb verziók.</span><span class="sxs-lookup"><span data-stu-id="52038-116">Use `Update-Module` to get newer versions.</span></span>

  ```powershell
  Update-Module -Name PowerShellGet
  Exit
  ```

### <a name="for-systems-running-powershell-3-or-powershell-4-that-have-installed-the-packagemanagement-msihttpswwwmicrosoftcomdownloaddetailsaspxid51451"></a><span data-ttu-id="52038-117">PowerShell 3 vagy 4 operációs rendszer, hogy telepítette a [PackageManagement MSI](https://www.microsoft.com/download/details.aspx?id=51451)</span><span class="sxs-lookup"><span data-stu-id="52038-117">For systems running PowerShell 3 or PowerShell 4, that have installed the [PackageManagement MSI](https://www.microsoft.com/download/details.aspx?id=51451)</span></span>

- <span data-ttu-id="52038-118">Használja a PowerShellGet parancsmagot egy emelt szintű PowerShell-munkamenetből a modulok egy helyi könyvtárba menteni</span><span class="sxs-lookup"><span data-stu-id="52038-118">Use below PowerShellGet cmdlet from an elevated PowerShell session to save the modules to a local directory</span></span>

  ```powershell
  Save-Module PowerShellGet -Path C:\LocalFolder
  Exit
  ```

- <span data-ttu-id="52038-119">Győződjön meg arról, hogy a PowerShellGet és a PackageManagement-modulok nem töltődnek be más folyamatokban.</span><span class="sxs-lookup"><span data-stu-id="52038-119">Ensure that PowerShellGet and PackageManagement modules are not loaded in any other processes.</span></span>
- <span data-ttu-id="52038-120">Törli a tartalmát `$env:ProgramFiles\WindowsPowerShell\Modules\PowerShellGet\` és `$env:ProgramFiles\WindowsPowerShell\Modules\PackageManagement\` mappákat.</span><span class="sxs-lookup"><span data-stu-id="52038-120">Delete contents of `$env:ProgramFiles\WindowsPowerShell\Modules\PowerShellGet\` and  `$env:ProgramFiles\WindowsPowerShell\Modules\PackageManagement\` folders.</span></span>
- <span data-ttu-id="52038-121">Nyissa meg újra a PS-konzol emelt szintű engedélyekkel, majd futtassa a következő parancsokat.</span><span class="sxs-lookup"><span data-stu-id="52038-121">Re-open the PS Console with elevated permissions then run the following commands.</span></span>

  ```powershell
  Copy-Item "C:\LocalFolder\PowerShellGet\*" "$env:ProgramFiles\WindowsPowerShell\Modules\PowerShellGet\" -Recurse -Force
  Copy-Item "C:\LocalFolder\PackageManagement\*" "$env:ProgramFiles\WindowsPowerShell\Modules\PackageManagement\" -Recurse -Force
  ```
