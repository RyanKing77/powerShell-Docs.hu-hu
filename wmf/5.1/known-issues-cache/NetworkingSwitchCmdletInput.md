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
# <a name="network-switch-manager-cmdlets-failure"></a>Hálózati kapcsolók kezelője parancsmagok hiba

A hálózati kapcsolók kezelője parancsmagok segítségével hálózati kapcsolók kezelése a wsman által használt keresztül.
Ez a modul parancsmagjai néhány képesek a folyamatok értékek elfogadásával.
A WMF 5.1-es előzetes verzióban elérhető parancsmagjainak is fogadja el a folyamat nem hajtható végre, ha az értékek nem továbbítódnak a folyamatok.

"InputObject" paraméter nem használatos, ha a parancsmag végrehajtása nélkül hibák továbbra is.

Itt látható a listában érintett parancsmagok, azaz ezeket a parancsmagokat elfogadhatja adatcsatornából "InputObject" paraméter értéke.
Ha ezt az értéket nem ad át a folyamat a parancsmag végrehajtása sikertelen lesz.

- Disable-NetworkSwitchEthernetPort
- Enable-NetworkSwitchEthernetPort
- Remove-NetworkSwitchEthernetPortIPAddress
- Set-NetworkSwitchEthernetPortIPAddress
- Set-NetworkSwitchPortMode
- Set-NetworkSwitchPortProperty
- Disable-NetworkSwitchFeature
- Enable-NetworkSwitchFeature
- Remove-NetworkSwitchVlan
- Set-NetworkSwitchVlanProperty

## <a name="resolution"></a>Felbontás

A parancsmagok munka gondot, ha InputObject paraméter értékének továbbítja a rendszer bele folyamat. Néhány példa, amelyek a fenti parancsmagok a következők:

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