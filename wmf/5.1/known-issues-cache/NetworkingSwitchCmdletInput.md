---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.topic: conceptual
contributor: vaibch
title: Hálózati kapcsolók kezelője parancsmagok hiba
ms.openlocfilehash: a0f84c35974b6674faba4b0f19a28bd6e2490a96
ms.sourcegitcommit: 8b076ebde7ef971d7465bab834a3c2a32471ef6f
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/06/2018
ms.locfileid: "37893154"
---
# <a name="network-switch-manager-cmdlets-failure"></a><span data-ttu-id="b547d-103">Hálózati kapcsolók kezelője parancsmagok hiba</span><span class="sxs-lookup"><span data-stu-id="b547d-103">Network Switch Manager Cmdlets Failure</span></span>

<span data-ttu-id="b547d-104">A hálózati kapcsolók kezelője parancsmagok segítségével hálózati kapcsolók kezelése a wsman által használt keresztül.</span><span class="sxs-lookup"><span data-stu-id="b547d-104">The Network Switch Manager cmdlets can be used to manage network switches over WSMAN.</span></span>
<span data-ttu-id="b547d-105">Ez a modul parancsmagjai néhány képesek a folyamatok értékek elfogadásával.</span><span class="sxs-lookup"><span data-stu-id="b547d-105">A few cmdlets of this module are capable of accepting values from pipelines.</span></span>
<span data-ttu-id="b547d-106">A WMF 5.1-es előzetes verzióban elérhető parancsmagjainak is fogadja el a folyamat nem hajtható végre, ha az értékek nem továbbítódnak a folyamatok.</span><span class="sxs-lookup"><span data-stu-id="b547d-106">In WMF 5.1 Preview, the cmdlets that can accept value from pipeline fail to execute when the values are not passed through pipelines.</span></span>

<span data-ttu-id="b547d-107">"InputObject" paraméter nem használatos, ha a parancsmag végrehajtása nélkül hibák továbbra is.</span><span class="sxs-lookup"><span data-stu-id="b547d-107">If "InputObject" parameter is not used, the cmdlet should continue to execute without failures.</span></span>

<span data-ttu-id="b547d-108">Itt látható a listában érintett parancsmagok, azaz ezeket a parancsmagokat elfogadhatja adatcsatornából "InputObject" paraméter értéke.</span><span class="sxs-lookup"><span data-stu-id="b547d-108">Here is the list of affected cmdlets i.e. these cmdlets can accept value for "InputObject" parameter from pipeline.</span></span>
<span data-ttu-id="b547d-109">Ha ezt az értéket nem ad át a folyamat a parancsmag végrehajtása sikertelen lesz.</span><span class="sxs-lookup"><span data-stu-id="b547d-109">If this value is not passed from pipeline the execution of cmdlet will fail.</span></span>

- <span data-ttu-id="b547d-110">Disable-NetworkSwitchEthernetPort</span><span class="sxs-lookup"><span data-stu-id="b547d-110">Disable-NetworkSwitchEthernetPort</span></span>
- <span data-ttu-id="b547d-111">Enable-NetworkSwitchEthernetPort</span><span class="sxs-lookup"><span data-stu-id="b547d-111">Enable-NetworkSwitchEthernetPort</span></span>
- <span data-ttu-id="b547d-112">Remove-NetworkSwitchEthernetPortIPAddress</span><span class="sxs-lookup"><span data-stu-id="b547d-112">Remove-NetworkSwitchEthernetPortIPAddress</span></span>
- <span data-ttu-id="b547d-113">Set-NetworkSwitchEthernetPortIPAddress</span><span class="sxs-lookup"><span data-stu-id="b547d-113">Set-NetworkSwitchEthernetPortIPAddress</span></span>
- <span data-ttu-id="b547d-114">Set-NetworkSwitchPortMode</span><span class="sxs-lookup"><span data-stu-id="b547d-114">Set-NetworkSwitchPortMode</span></span>
- <span data-ttu-id="b547d-115">Set-NetworkSwitchPortProperty</span><span class="sxs-lookup"><span data-stu-id="b547d-115">Set-NetworkSwitchPortProperty</span></span>
- <span data-ttu-id="b547d-116">Disable-NetworkSwitchFeature</span><span class="sxs-lookup"><span data-stu-id="b547d-116">Disable-NetworkSwitchFeature</span></span>
- <span data-ttu-id="b547d-117">Enable-NetworkSwitchFeature</span><span class="sxs-lookup"><span data-stu-id="b547d-117">Enable-NetworkSwitchFeature</span></span>
- <span data-ttu-id="b547d-118">Remove-NetworkSwitchVlan</span><span class="sxs-lookup"><span data-stu-id="b547d-118">Remove-NetworkSwitchVlan</span></span>
- <span data-ttu-id="b547d-119">Set-NetworkSwitchVlanProperty</span><span class="sxs-lookup"><span data-stu-id="b547d-119">Set-NetworkSwitchVlanProperty</span></span>

## <a name="resolution"></a><span data-ttu-id="b547d-120">Felbontás</span><span class="sxs-lookup"><span data-stu-id="b547d-120">Resolution</span></span>

<span data-ttu-id="b547d-121">A parancsmagok munka gondot, ha InputObject paraméter értékének továbbítja a rendszer bele folyamat.</span><span class="sxs-lookup"><span data-stu-id="b547d-121">The cmdlets work fine when the value of InputObject parameter are passed into it through pipeline.</span></span> <span data-ttu-id="b547d-122">Néhány példa, amelyek a fenti parancsmagok a következők:</span><span class="sxs-lookup"><span data-stu-id="b547d-122">A few examples that work for the above cmdlets are:</span></span>

- `Disable-NetworkSwitchEthernetPort`

  ```powershell
  $port = Get-CimInstance -Namespace root/interop -ClassName CIM_EthernetPort -CimSession $cimSession | Select-Object -First 1
  $port | Disable-NetworkSwitchEthernetPort -CimSession $cimSession
  ```

- `Enable-NetworkSwitchEthernetPort`

  ```powershell
  $port = Get-CimInstance -Namespace root/interop -ClassName CIM_EthernetPort -CimSession $cimSession | Select-Object -First 1
  $port | Enable-NetworkSwitchEthernetPort -CimSession $cimSession
  ```

- `Remove-NetworkSwitchEthernetPortIPAddress`

  ```powershell
  $port = Get-CimInstance -Namespace root/interop -ClassName CIM_EthernetPort -CimSession $cimSession | Select-Object -First 1
  $port | Remove-NetworkSwitchEthernetPortIPAddress -CimSession $cimSession
  ```

- `Set-NetworkSwitchEthernetPortIPAddress`

  ```powershell
  $port = Get-CimInstance -Namespace root/interop -ClassName CIM_EthernetPort -CimSession $cimSession | Select-Object -First 1
  $ipAddress = "192.168.10.1"
  $subnetAddress = "255.255.255.0"
  $port | Set-NetworkSwitchEthernetPortIPAddress -IpAddress $ipAddress -SubnetAddress $subnetAddress -CimSession $cimSession
  ```

- `Set-NetworkSwitchPortProperty`

  ```powershell
  $portProperties = @{Caption = "New Caption"}
  $port = Get-CimInstance -Namespace root/interop -ClassName CIM_EthernetPort -CimSession $cimSession | Select-Object -First 1
  $port | Set-NetworkSwitchPortProperty -Property $portProperties -CimSession $cimSession
  ```

- `Disable-NetworkSwitchFeature`

  ```powershell
  $feature = Get-CimInstance -Namespace root/interop -ClassName MSFT_Feature -CimSession $cimSession | Select-Object -First 1
  $feature | Disable-NetworkSwitchFeature -CimSession $cimSession
  ```

- `Enable-NetworkSwitchFeature`

  ```powershell
  $feature = Get-CimInstance -Namespace root/interop -ClassName MSFT_Feature -CimSession $cimSession | Select-Object -First 1
  $feature | Enable-NetworkSwitchFeature -CimSession $cimSession
  ```

- `Set-NetworkSwitchVlanProperty`

  ```powershell
  $properties = @{Caption = "New Caption"}
  $vlan = Get-CimInstance -ClassName CIM_NetworkVlan -Namespace root/interop -CimSession $cimSession | Select-Object -First 1
  $vlan | Set-NetworkSwitchVlanProperty -Property $properties -CimSession $cimSession
  ```