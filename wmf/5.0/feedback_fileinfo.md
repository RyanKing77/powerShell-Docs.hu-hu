---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: 5280ef5ff95679dc8721be8f5f81031a4ffe796f
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55687068"
---
# <a name="updates-to-fileinfo-object"></a><span data-ttu-id="a5946-102">A FileInfo objektum frissítései</span><span class="sxs-lookup"><span data-stu-id="a5946-102">Updates to FileInfo object</span></span>
<span data-ttu-id="a5946-103">Fájlverzió-információkat is félrevezető lehet, különösen olyan esetekben, ahol a fájl javítva lett.</span><span class="sxs-lookup"><span data-stu-id="a5946-103">File version information can be misleading, particularly in cases where the file was patched.</span></span> <span data-ttu-id="a5946-104">Ebben a kiadásban a WMF 5.0 ad hozzá új **FileVersionRaw** és **ProductVersionRaw** parancsfájl FileInfo objektum tulajdonságait.</span><span class="sxs-lookup"><span data-stu-id="a5946-104">This release of WMF 5.0 adds new **FileVersionRaw** and **ProductVersionRaw** script properties to FileInfo objects.</span></span> <span data-ttu-id="a5946-105">A powershell.exe (feltéve, hogy $pid a PowerShell-folyamat azonosítója) jelenik meg az alábbiakban a tulajdonságai:</span><span class="sxs-lookup"><span data-stu-id="a5946-105">Here are the properties as displayed for powershell.exe (assuming $pid is the ID of the PowerShell process):</span></span>

```powershell
PS C:\> Get-Process -Id $pid -FileVersionInfo | fl *version* -Force


FileVersionRaw    : 10.0.10586.117
ProductVersionRaw : 10.0.10586.117
FileVersion       : 10.0.10586.117 (th2_release.160212-2359)
ProductVersion    : 10.0.10586.117
