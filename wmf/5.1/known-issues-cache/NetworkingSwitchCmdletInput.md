---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.topic: conceptual
contributor: vaibch
title: Hálózati kapcsolók kezelője parancsmagok hiba
ms.openlocfilehash: 197a25411a82e5d256a9420706535d5411991f1b
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/16/2018
ms.locfileid: "34188683"
---
<span data-ttu-id="848ec-103">A hálózati kapcsolók kezelője parancsmagok segítségével kezelheti a hálózati kapcsolók WSMAN keresztül.</span><span class="sxs-lookup"><span data-stu-id="848ec-103">The Network Switch Manager cmdlets can be used to manage network switches over WSMAN.</span></span>
<span data-ttu-id="848ec-104">Ehhez a modul néhány parancsmagok képesek a folyamatok értékek elfogadásával.</span><span class="sxs-lookup"><span data-stu-id="848ec-104">A few cmdlets of this module are capable of accepting values from pipelines.</span></span>
<span data-ttu-id="848ec-105">WMF 5.1 Preview a parancsmagok láncból értéket fogad el nem hajtható végre, ha az értékek nem továbbítja a rendszer folyamatok.</span><span class="sxs-lookup"><span data-stu-id="848ec-105">In WMF 5.1 Preview, the cmdlets that can accept value from pipeline fail to execute when the values are not passed through pipelines.</span></span>

<span data-ttu-id="848ec-106">Ha nem használja a "InputObject" paramétert, a parancsmag továbbra is hibák nélkül.</span><span class="sxs-lookup"><span data-stu-id="848ec-106">If "InputObject" parameter is not used, the cmdlet should continue to execute without failures.</span></span>

<span data-ttu-id="848ec-107">Ez a lista érintett parancsmagok azaz ezeket a parancsmagokat fogadhat láncból "InputObject" paraméter értékét.</span><span class="sxs-lookup"><span data-stu-id="848ec-107">Here is the list of affected cmdlets i.e. these cmdlets can accept value for "InputObject" parameter from pipeline.</span></span>
<span data-ttu-id="848ec-108">Ha ez az érték nem kerül át, a csővezeték-parancsmag végrehajtása sikertelen lesz.</span><span class="sxs-lookup"><span data-stu-id="848ec-108">If this value is not passed from pipeline the execution of cmdlet will fail.</span></span>

- <span data-ttu-id="848ec-109">Disable-NetworkSwitchEthernetPort</span><span class="sxs-lookup"><span data-stu-id="848ec-109">Disable-NetworkSwitchEthernetPort</span></span>
- <span data-ttu-id="848ec-110">Enable-NetworkSwitchEthernetPort</span><span class="sxs-lookup"><span data-stu-id="848ec-110">Enable-NetworkSwitchEthernetPort</span></span>
- <span data-ttu-id="848ec-111">Remove-NetworkSwitchEthernetPortIPAddress</span><span class="sxs-lookup"><span data-stu-id="848ec-111">Remove-NetworkSwitchEthernetPortIPAddress</span></span>
- <span data-ttu-id="848ec-112">Set-NetworkSwitchEthernetPortIPAddress</span><span class="sxs-lookup"><span data-stu-id="848ec-112">Set-NetworkSwitchEthernetPortIPAddress</span></span>
- <span data-ttu-id="848ec-113">Set-NetworkSwitchPortMode</span><span class="sxs-lookup"><span data-stu-id="848ec-113">Set-NetworkSwitchPortMode</span></span>
- <span data-ttu-id="848ec-114">Set-NetworkSwitchPortProperty</span><span class="sxs-lookup"><span data-stu-id="848ec-114">Set-NetworkSwitchPortProperty</span></span>
- <span data-ttu-id="848ec-115">Disable-NetworkSwitchFeature</span><span class="sxs-lookup"><span data-stu-id="848ec-115">Disable-NetworkSwitchFeature</span></span>
- <span data-ttu-id="848ec-116">Enable-NetworkSwitchFeature</span><span class="sxs-lookup"><span data-stu-id="848ec-116">Enable-NetworkSwitchFeature</span></span>
- <span data-ttu-id="848ec-117">Remove-NetworkSwitchVlan</span><span class="sxs-lookup"><span data-stu-id="848ec-117">Remove-NetworkSwitchVlan</span></span>
- <span data-ttu-id="848ec-118">Set-NetworkSwitchVlanProperty</span><span class="sxs-lookup"><span data-stu-id="848ec-118">Set-NetworkSwitchVlanProperty</span></span>

### <a name="resolution"></a><span data-ttu-id="848ec-119">Felbontás</span><span class="sxs-lookup"><span data-stu-id="848ec-119">Resolution</span></span>
<span data-ttu-id="848ec-120">A parancsmagok munkahelyi elfogadható, ha a InputObject paraméter értékének bele-feldolgozási folyamaton keresztül.</span><span class="sxs-lookup"><span data-stu-id="848ec-120">The cmdlets work fine when the value of InputObject parameter are passed into it through pipeline.</span></span> <span data-ttu-id="848ec-121">Néhány példa a fenti parancsmag használható a következők:</span><span class="sxs-lookup"><span data-stu-id="848ec-121">A few examples that work for the above cmdlets are:</span></span>

- <span data-ttu-id="848ec-122">Disable-NetworkSwitchEthernetPort</span><span class="sxs-lookup"><span data-stu-id="848ec-122">Disable-NetworkSwitchEthernetPort</span></span>
```powershell
$port = Get-CimInstance -Namespace root/interop -ClassName CIM_EthernetPort -CimSession $cimSession | Select-Object -First 1
$port | Disable-NetworkSwitchEthernetPort -CimSession $cimSession
```

- <span data-ttu-id="848ec-123">Enable-NetworkSwitchEthernetPort</span><span class="sxs-lookup"><span data-stu-id="848ec-123">Enable-NetworkSwitchEthernetPort</span></span>
```powershell
$port = Get-CimInstance -Namespace root/interop -ClassName CIM_EthernetPort -CimSession $cimSession | Select-Object -First 1
$port | Enable-NetworkSwitchEthernetPort -CimSession $cimSession
```

- <span data-ttu-id="848ec-124">Remove-NetworkSwitchEthernetPortIPAddress</span><span class="sxs-lookup"><span data-stu-id="848ec-124">Remove-NetworkSwitchEthernetPortIPAddress</span></span>
```powershell
$port = Get-CimInstance -Namespace root/interop -ClassName CIM_EthernetPort -CimSession $cimSession | Select-Object -First 1
$port | Remove-NetworkSwitchEthernetPortIPAddress -CimSession $cimSession
```

- <span data-ttu-id="848ec-125">Set-NetworkSwitchEthernetPortIPAddress</span><span class="sxs-lookup"><span data-stu-id="848ec-125">Set-NetworkSwitchEthernetPortIPAddress</span></span>
```powershell
$port = Get-CimInstance -Namespace root/interop -ClassName CIM_EthernetPort -CimSession $cimSession | Select-Object -First 1
$ipAddress = "192.168.10.1"
$subnetAddress = "255.255.255.0"
$port | Set-NetworkSwitchEthernetPortIPAddress -IpAddress $ipAddress -SubnetAddress $subnetAddress -CimSession $cimSession
```

- <span data-ttu-id="848ec-126">Set-NetworkSwitchPortProperty</span><span class="sxs-lookup"><span data-stu-id="848ec-126">Set-NetworkSwitchPortProperty</span></span>
```powershell
$portProperties = @{Caption = "New Caption"}
$port = Get-CimInstance -Namespace root/interop -ClassName CIM_EthernetPort -CimSession $cimSession | Select-Object -First 1
$port | Set-NetworkSwitchPortProperty -Property $portProperties -CimSession $cimSession
```

- <span data-ttu-id="848ec-127">Disable-NetworkSwitchFeature</span><span class="sxs-lookup"><span data-stu-id="848ec-127">Disable-NetworkSwitchFeature</span></span>
```powershell
$feature = Get-CimInstance -Namespace root/interop -ClassName MSFT_Feature -CimSession $cimSession | Select-Object -First 1
$feature | Disable-NetworkSwitchFeature -CimSession $cimSession
```

- <span data-ttu-id="848ec-128">Enable-NetworkSwitchFeature</span><span class="sxs-lookup"><span data-stu-id="848ec-128">Enable-NetworkSwitchFeature</span></span>
```powershell
$feature = Get-CimInstance -Namespace root/interop -ClassName MSFT_Feature -CimSession $cimSession | Select-Object -First 1
$feature | Enable-NetworkSwitchFeature -CimSession $cimSession
```

- <span data-ttu-id="848ec-129">Set-NetworkSwitchVlanProperty</span><span class="sxs-lookup"><span data-stu-id="848ec-129">Set-NetworkSwitchVlanProperty</span></span>
```powershell
$properties = @{Caption = "New Caption"}
$vlan = Get-CimInstance -ClassName CIM_NetworkVlan -Namespace root/interop -CimSession $cimSession | Select-Object -First 1
$vlan | Set-NetworkSwitchVlanProperty -Property $properties -CimSession $cimSession
```
