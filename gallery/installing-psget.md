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
# <a name="installing-powershellget"></a><span data-ttu-id="b686f-103">A PowerShellGet telepítése</span><span class="sxs-lookup"><span data-stu-id="b686f-103">Installing PowerShellGet</span></span>

## <a name="powershellget-is-an-in-box-module-in-the-following-releases"></a><span data-ttu-id="b686f-104">A PowerShellGet egy beépített modul a következő kiadásokban</span><span class="sxs-lookup"><span data-stu-id="b686f-104">PowerShellGet is an in-box module in the following releases</span></span>

- <span data-ttu-id="b686f-105">[Windows 10](https://www.microsoft.com/windows) vagy újabb</span><span class="sxs-lookup"><span data-stu-id="b686f-105">[Windows 10](https://www.microsoft.com/windows) or newer</span></span>
- <span data-ttu-id="b686f-106">[Windows Server 2016](/windows-server/windows-server) vagy újabb</span><span class="sxs-lookup"><span data-stu-id="b686f-106">[Windows Server 2016](/windows-server/windows-server) or newer</span></span>
- <span data-ttu-id="b686f-107">[Windows Management Framework (WMF) 5,0](https://www.microsoft.com/download/details.aspx?id=50395) vagy újabb</span><span class="sxs-lookup"><span data-stu-id="b686f-107">[Windows Management Framework (WMF) 5.0](https://www.microsoft.com/download/details.aspx?id=50395) or newer</span></span>
- [<span data-ttu-id="b686f-108">PowerShell 6</span><span class="sxs-lookup"><span data-stu-id="b686f-108">PowerShell 6</span></span>](https://github.com/PowerShell/PowerShell/releases)

## <a name="get-powershellget-module-for-powershell-versions-30-and-40"></a><span data-ttu-id="b686f-109">PowerShellGet-modul beszerzése a PowerShell 3,0-es és 4,0-es verzióihoz</span><span class="sxs-lookup"><span data-stu-id="b686f-109">Get PowerShellGet module for PowerShell versions 3.0 and 4.0</span></span>

- [<span data-ttu-id="b686f-110">PackageManagement MSI</span><span class="sxs-lookup"><span data-stu-id="b686f-110">PackageManagement MSI</span></span>](https://www.microsoft.com/download/details.aspx?id=51451)

## <a name="get-the-latest-version-from-powershell-gallery"></a><span data-ttu-id="b686f-111">A legújabb verzió letöltése PowerShell-galéria</span><span class="sxs-lookup"><span data-stu-id="b686f-111">Get the latest version from PowerShell Gallery</span></span>

- <span data-ttu-id="b686f-112">A PowerShellGet frissítése előtt mindig telepítse a legújabb Nuget-szolgáltatót.</span><span class="sxs-lookup"><span data-stu-id="b686f-112">Before updating PowerShellGet, you should always install the latest Nuget provider.</span></span> <span data-ttu-id="b686f-113">Ehhez futtassa a következőt egy emelt szintű PowerShell-munkamenetben.</span><span class="sxs-lookup"><span data-stu-id="b686f-113">To do that, run the following in an elevated PowerShell session.</span></span>

  ```powershell
  Install-PackageProvider Nuget -Force
  Exit
  ```

### <a name="for-systems-with-powershell-50-or-newer-you-can-install-the-latest-powershellget"></a><span data-ttu-id="b686f-114">A PowerShell 5,0 (vagy újabb) rendszerekkel rendelkező rendszerek esetében telepítheti a legújabb PowerShellGet</span><span class="sxs-lookup"><span data-stu-id="b686f-114">For systems with PowerShell 5.0 (or newer) you can install the latest PowerShellGet</span></span>

- <span data-ttu-id="b686f-115">Ezt a Windows 10, a Windows Server 2016, a WMF 5,0 vagy 5,1 rendszerű, illetve a PowerShell 6-os verzióval rendelkező rendszerek esetén futtassa a következő parancsokat egy emelt szintű PowerShell-munkamenetből.</span><span class="sxs-lookup"><span data-stu-id="b686f-115">To do this on Windows 10, Windows Server 2016, any system with WMF 5.0 or 5.1 installed, or any system with PowerShell 6, run the following commands from an elevated PowerShell session.</span></span>

  ```powershell
  Install-Module -Name PowerShellGet -Force
  Exit
  ```

- <span data-ttu-id="b686f-116">Újabb `Update-Module` verziók beszerzéséhez használja a következőt:.</span><span class="sxs-lookup"><span data-stu-id="b686f-116">Use `Update-Module` to get newer versions.</span></span>

  ```powershell
  Update-Module -Name PowerShellGet
  Exit
  ```

### <a name="for-systems-running-powershell-3-or-powershell-4-that-have-installed-the-packagemanagement-msihttpswwwmicrosoftcomdownloaddetailsaspxid51451"></a><span data-ttu-id="b686f-117">A PowerShell 3 vagy PowerShell 4 rendszert futtató rendszerek esetében, amelyek telepítették a [PACKAGEMANAGEMENT MSI](https://www.microsoft.com/download/details.aspx?id=51451) -t</span><span class="sxs-lookup"><span data-stu-id="b686f-117">For systems running PowerShell 3 or PowerShell 4, that have installed the [PackageManagement MSI](https://www.microsoft.com/download/details.aspx?id=51451)</span></span>

- <span data-ttu-id="b686f-118">Az alábbi PowerShellGet-parancsmagot egy emelt szintű PowerShell-munkamenetből használva mentse a modulokat egy helyi könyvtárba.</span><span class="sxs-lookup"><span data-stu-id="b686f-118">Use below PowerShellGet cmdlet from an elevated PowerShell session to save the modules to a local directory</span></span>

  ```powershell
  Save-Module PowerShellGet -Path C:\LocalFolder
  Exit
  ```

- <span data-ttu-id="b686f-119">Győződjön meg arról, hogy a PowerShellGet és a PackageManagement modulok nincsenek betöltve más folyamatokban.</span><span class="sxs-lookup"><span data-stu-id="b686f-119">Ensure that PowerShellGet and PackageManagement modules are not loaded in any other processes.</span></span>
- <span data-ttu-id="b686f-120">A és `$env:ProgramFiles\WindowsPowerShell\Modules\PowerShellGet\` `$env:ProgramFiles\WindowsPowerShell\Modules\PackageManagement\` a mappák tartalmának törlése.</span><span class="sxs-lookup"><span data-stu-id="b686f-120">Delete contents of `$env:ProgramFiles\WindowsPowerShell\Modules\PowerShellGet\` and  `$env:ProgramFiles\WindowsPowerShell\Modules\PackageManagement\` folders.</span></span>
- <span data-ttu-id="b686f-121">Nyissa meg újra a PS-konzolt emelt szintű engedélyekkel, majd futtassa a következő parancsokat.</span><span class="sxs-lookup"><span data-stu-id="b686f-121">Re-open the PS Console with elevated permissions then run the following commands.</span></span>

  ```powershell
  Copy-Item "C:\LocalFolder\PowerShellGet\*" "$env:ProgramFiles\WindowsPowerShell\Modules\PowerShellGet\" -Recurse -Force
  Copy-Item "C:\LocalFolder\PackageManagement\*" "$env:ProgramFiles\WindowsPowerShell\Modules\PackageManagement\" -Recurse -Force
  ```
