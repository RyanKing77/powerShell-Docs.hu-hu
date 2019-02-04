---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: 61c5df1b64cb9c54f9c7372a56e77abf319658dd
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55683764"
---
# <a name="network-switch-management-with-powershell"></a>Hálózati kapcsolók kezelése a PowerShell-lel

A **Get-NetworkSwitchEthernetPort** parancsmag mostantól osztályt a következő kiegészítő információkat ad vissza:

- IP-cím – a porthoz társított IP-cím
- PortMode – a port mód: hozzáférés, útvonal vagy hálózati trönk
- AccessVLAN – a VLAN Azonosítóját társított ezt a portot, a hozzáférési mód
- Ehhez a porthoz trönk módban társított azonosítók a VLAN-ok listáját TrunkedVLANList –

## <a name="fundamental-network-switch-management-with-windows-powershell"></a>Alapvető hálózati kapcsolók kezelése a Windows PowerShell-lel

A hálózati kapcsoló, a WMF 5.0-s-ben bevezetett parancsmagjaival kapcsoló, a virtuális LAN (VLAN) és az alapszintű 2. rétegbeli hálózati kapcsoló port konfigurációja alkalmazhat a Windows Server 2012 R2-emblémával hitelesített hálózati kapcsolók. A Microsoft továbbra is fontos, hogy támogató a [adatközpont-absztrakciós](http://technet.microsoft.com/cloud/dal.aspx) réteg (DAL) vision, és a megjelenítendő érték ügyfeleink és partnereink számára ezen a helyen. Ezek a parancsmagok használatával hajthatja végre:

- Globális váltson konfigurációs, például:
    - Gazdagép nevének beállítása
    - Set kapcsoló szalagcím
    - Konfigurációs megőrzése
    - Engedélyezi vagy letiltja a szolgáltatás

- VLAN-konfiguráció:
    - Hozzon létre vagy VLAN eltávolítása
    - Engedélyezheti vagy tilthatja le a VLAN
    - VLAN számbavétele
    - Rövid név beállítása egy VLAN-hoz

- 2. rétegbeli port konfigurációja:
    - Portok számbavétele
    - Engedélyezheti vagy tilthatja le a portok
    - Beállított port módok és tulajdonságai
    - Adja hozzá, vagy VLAN-Trönk vagy a hozzáférés a porton társítása

Indítsa el a NetworkSwitch parancsmagok mindegyikét keres vizsgálatát!

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

További információ a WMF 5.0-s előzetes bejelentés ebben a blogbejegyzésben Jeffrey Snover érhető el: <http://blogs.technet.com/b/windowsserver/archive/2014/04/03/windows-management-framework-v5-preview.aspx>
