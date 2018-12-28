---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: Egy lekéréses kiszolgálóról csomópontok frissítése
ms.openlocfilehash: 4333a5bf82ef45f22a062942ebe93409433623f5
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/14/2018
ms.locfileid: "53404134"
---
# <a name="update-nodes-from-a-pull-server"></a><span data-ttu-id="0c0a0-103">Egy lekéréses kiszolgálóról csomópontok frissítése</span><span class="sxs-lookup"><span data-stu-id="0c0a0-103">Update Nodes from a Pull Server</span></span>

<span data-ttu-id="0c0a0-104">Az alábbi szakaszok azt feltételezik, hogy Ön már beállított egy lekéréses kiszolgálón.</span><span class="sxs-lookup"><span data-stu-id="0c0a0-104">The sections below assume that you have already set up a Pull Server.</span></span> <span data-ttu-id="0c0a0-105">Ha nincs beállítva a lekéréses kiszolgálón, használhatja a következő útmutatókat:</span><span class="sxs-lookup"><span data-stu-id="0c0a0-105">If you have not set up your Pull Server, you can use the following guides:</span></span>

- [<span data-ttu-id="0c0a0-106">DSC SMB-lekérési kiszolgáló beállítása</span><span class="sxs-lookup"><span data-stu-id="0c0a0-106">Set up a DSC SMB Pull Server</span></span>](pullServerSmb.md)
- [<span data-ttu-id="0c0a0-107">A DSC HTTP-lekérési kiszolgáló beállítása</span><span class="sxs-lookup"><span data-stu-id="0c0a0-107">Set up a DSC HTTP Pull Server</span></span>](pullServer.md)

<span data-ttu-id="0c0a0-108">Minden egyes célcsomóponttal konfigurálható töltse le a konfigurációk, az erőforrásokat, és még jelentést annak állapotát.</span><span class="sxs-lookup"><span data-stu-id="0c0a0-108">Each target node can be configured to download configurations, resources, and even report its status.</span></span> <span data-ttu-id="0c0a0-109">Ebből a cikkből megtudhatja, hogyan tölthet fel erőforrásokat, így elérhetők tölthető le, és konfigurálja az ügyfeleket, automatikusan erőforrások letöltéséhez.</span><span class="sxs-lookup"><span data-stu-id="0c0a0-109">This article will show you how to upload resources so they are available to be downloaded, and configure clients to download resources automatically.</span></span> <span data-ttu-id="0c0a0-110">Amikor a csomópont kap keresztül egy hozzárendelt konfigurációs **lekéréses** vagy **leküldéses** (v5), automatikusan letölti az konfigurációjában megadott helyen található az LCM Konfigurálása a szükséges erőforrásokat.</span><span class="sxs-lookup"><span data-stu-id="0c0a0-110">When the Node's receives an assigned Configuration, through **Pull** or **Push** (v5), it automatically downloads any resources required by the Configuration from the location specified in the LCM.</span></span>

## <a name="using-the-update-dscconfiguration-cmdlet"></a><span data-ttu-id="0c0a0-111">Az Update-DSCConfiguration parancsmag használatával</span><span class="sxs-lookup"><span data-stu-id="0c0a0-111">Using the Update-DSCConfiguration cmdlet</span></span>

<span data-ttu-id="0c0a0-112">A PowerShell 5.0-, kezdve a [Update-DSCConfiguration](/powershell/module/psdesiredstateconfiguration/update-dscconfiguration) parancsmag frissíti a konfigurációját az LCM konfigurált lekérési kiszolgálóról egy csomópont kényszeríti.</span><span class="sxs-lookup"><span data-stu-id="0c0a0-112">Beginning in PowerShell 5.0, the [Update-DSCConfiguration](/powershell/module/psdesiredstateconfiguration/update-dscconfiguration) cmdlet, forces a Node to update its configuration from the Pull Server configured in the LCM.</span></span>

```powershell
Update-DSCConfiguration -ComputerName "Server01"
```

## <a name="using-invoke-cimmethod"></a><span data-ttu-id="0c0a0-113">Invoke-CIMMethod használatával</span><span class="sxs-lookup"><span data-stu-id="0c0a0-113">Using Invoke-CIMMethod</span></span>

<span data-ttu-id="0c0a0-114">A PowerShell 4.0-s, manuálisan is kényszerítheti, hogy a használt konfiguráció frissítése lekérési ügyfél [Invoke-CIMMethod](/powershell/module/cimcmdlets/invoke-cimmethod).</span><span class="sxs-lookup"><span data-stu-id="0c0a0-114">In PowerShell 4.0, you can still manually force a Pull Client to update its Configuration using [Invoke-CIMMethod](/powershell/module/cimcmdlets/invoke-cimmethod).</span></span> <span data-ttu-id="0c0a0-115">Az alábbi példa CIM-munkamenetet hoz létre a megadott hitelesítő adatokkal, a megfelelő CIM módszert hívja meg, és eltávolítja a munkamenetet.</span><span class="sxs-lookup"><span data-stu-id="0c0a0-115">The following example creates a CIM session with specified credentials, invokes the appropriate CIM method, and removes the session.</span></span>

```powershell
$cimSession = New-CimSession -ComputerName "Server01" -Credential $(Get-Credential)
Invoke-CimMethod -CimSession $cimSession -Namespace 'root/microsoft/windows/desiredstateconfiguration' -Class 'MSFT_DscLocalConfigurationManager' -MethodName 'PerformRequiredConfigurationChecks' -Arguments @{ 'Flags' = [uint32]1 } -Verbose
$cimSession | Remove-CimSession
```

## <a name="see-also"></a><span data-ttu-id="0c0a0-116">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="0c0a0-116">See Also</span></span>

[<span data-ttu-id="0c0a0-117">PerformRequiredConfigurationChecks</span><span class="sxs-lookup"><span data-stu-id="0c0a0-117">PerformRequiredConfigurationChecks</span></span>](/powershell/dsc/msft-dsclocalconfigurationmanager-performrequiredconfigurationchecks)
