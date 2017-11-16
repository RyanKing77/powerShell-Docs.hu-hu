---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "WMF, a powershell, a beállítása"
ms.openlocfilehash: 80852bf750700d549de24e150ffd89ac55b7bf88
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2017
---
# <a name="network-switch-management-with-powershell"></a>Hálózati kapcsoló kezelése a PowerShell használatával

A **Get-NetworkSwitchEthernetPort** parancsmag most osztályt a következő kiegészítő információkat ad vissza:

- IP-cím – az a port társított IP-cím
- PortMode – a port mód: hozzáférés, útvonal vagy trönk
- AccessVLAN – a VLAN Azonosítóját társított ezt a portot, a hozzáférési mód
- TrunkedVLANList – Ez a port trönk módban tartozó azonosítók a VLAN hálózatok listája

## <a name="fundamental-network-switch-management-with-windows-powershell"></a>Alapvető hálózati kapcsoló kezelése a Windows PowerShell használatával

A Hálózatikapcsoló-parancsmagjai, a WMF 5.0-ben bevezetett lehetővé teszik a Windows Server 2012 R2 embléma hitelesített hálózati kapcsolók kapcsoló, a virtuális LAN (VLAN) és a 2. rétegbeli hálózati kapcsoló port alapkonfiguráció alkalmazandó. Microsoft továbbra is támogató véglegesíteni a [adatközpont-absztrakciós](http://technet.microsoft.com/en-us/cloud/dal.aspx) réteg (DAL) stratégiai, és az érték szerepel, az ügyfelek és a partnerek ezen a helyen. Ezek a parancsmagok használatával hajthatja végre:

- Globális konfigurációs, például a kapcsolóhoz:
    - Gazdagép neve
    - Set kapcsoló szalagcím
    - Konfigurációs megőrzése
    - Engedélyezheti vagy tilthatja le a szolgáltatást

- VLAN-konfiguráció:
    - Hozzon létre, vagy távolítsa el a VLAN
    - Engedélyezheti vagy tilthatja le a VLAN
    - VLAN számbavétele
    - Állítsa be a rövid nevet a VLAN-hoz

- 2. réteg port konfigurálása:
    - Portok számbavétele
    - Engedélyezheti vagy tilthatja le a portok
    - Set port módok és tulajdonságai
    - Adja hozzá, vagy VLAN-Trönk vagy a hozzáférés a porton társítása

Fedezze fel az összes NetworkSwitch!

```powershell
PS> Get-Command *-NetworkSwitch*

| CommandType | Name                                      | Source        |
|-------------|-------------------------------------------|---------------|
|             |                                           |               |
| Function    | Disable-NetworkSwitchEthernetPort         | NetworkSwitch |
| Function    | Disable-NetworkSwitchFeature              | NetworkSwitch |
| Function    | Disable-NetworkSwitchVlan                 | NetworkSwitch |
| Function    | Enable-NetworkSwitchEthernetPort          | NetworkSwitch |
| Function    | Enable-NetworkSwitchFeature               | NetworkSwitch |
| Function    | Enable-NetworkSwitchVlan                  | NetworkSwitch |
| Function    | Get-NetworkSwitchEthernetPort             | NetworkSwitch |
| Function    | Get-NetworkSwitchFeature                  | NetworkSwitch |
| Function    | Get-NetworkSwitchGlobalData               | NetworkSwitch |
| Function    | Get-NetworkSwitchVlan                     | NetworkSwitch |
| Function    | New-NetworkSwitchVlan                     | NetworkSwitch |
| Function    | Remove-NetworkSwitchEthernetPortIPAddress | NetworkSwitch |
| Function    | Remove-NetworkSwitchVlan                  | NetworkSwitch |
| Function    | Restore-NetworkSwitchConfiguration        | NetworkSwitch |
| Function    | Save-NetworkSwitchConfiguration           | NetworkSwitch |
| Function    | Set-NetworkSwitchEthernetPortIPAddress    | NetworkSwitch |
| Function    | Set-NetworkSwitchPortMode                 | NetworkSwitch |
| Function    | Set-NetworkSwitchPortProperty             | NetworkSwitch |
| Function    | Set-NetworkSwitchVlanProperty             | NetworkSwitch |
```

További információ a Jeffrey Snover WMF 5.0 előzetes bejelentés blogbejegyzésben érhető el: <http://blogs.technet.com/b/windowsserver/archive/2014/04/03/windows-management-framework-v5-preview.aspx>

