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
# <a name="network-switch-management-with-powershell"></a><span data-ttu-id="faf7d-102">Hálózati kapcsolók kezelése a PowerShell-lel</span><span class="sxs-lookup"><span data-stu-id="faf7d-102">Network Switch Management with PowerShell</span></span>

<span data-ttu-id="faf7d-103">A **Get-NetworkSwitchEthernetPort** parancsmag mostantól osztályt a következő kiegészítő információkat ad vissza:</span><span class="sxs-lookup"><span data-stu-id="faf7d-103">The **Get-NetworkSwitchEthernetPort** cmdlet now returns the following additional information with instances:</span></span>

- <span data-ttu-id="faf7d-104">IP-cím – a porthoz társított IP-cím</span><span class="sxs-lookup"><span data-stu-id="faf7d-104">IPAddress – the IP address associated with the port</span></span>
- <span data-ttu-id="faf7d-105">PortMode – a port mód: hozzáférés, útvonal vagy hálózati trönk</span><span class="sxs-lookup"><span data-stu-id="faf7d-105">PortMode – the port mode: access, route, or trunk</span></span>
- <span data-ttu-id="faf7d-106">AccessVLAN – a VLAN Azonosítóját társított ezt a portot, a hozzáférési mód</span><span class="sxs-lookup"><span data-stu-id="faf7d-106">AccessVLAN – the ID of the VLAN associated with this port in access mode</span></span>
- <span data-ttu-id="faf7d-107">Ehhez a porthoz trönk módban társított azonosítók a VLAN-ok listáját TrunkedVLANList –</span><span class="sxs-lookup"><span data-stu-id="faf7d-107">TrunkedVLANList – a list of IDs of VLANs associated with this port in trunk mode</span></span>

## <a name="fundamental-network-switch-management-with-windows-powershell"></a><span data-ttu-id="faf7d-108">Alapvető hálózati kapcsolók kezelése a Windows PowerShell-lel</span><span class="sxs-lookup"><span data-stu-id="faf7d-108">Fundamental network switch management with Windows PowerShell</span></span>

<span data-ttu-id="faf7d-109">A hálózati kapcsoló, a WMF 5.0-s-ben bevezetett parancsmagjaival kapcsoló, a virtuális LAN (VLAN) és az alapszintű 2. rétegbeli hálózati kapcsoló port konfigurációja alkalmazhat a Windows Server 2012 R2-emblémával hitelesített hálózati kapcsolók.</span><span class="sxs-lookup"><span data-stu-id="faf7d-109">The Network Switch cmdlets, introduced in WMF 5.0, enable you to apply switch, virtual LAN (VLAN), and basic Layer 2 network switch port configuration to Windows Server 2012 R2 logo-certified network switches.</span></span> <span data-ttu-id="faf7d-110">A Microsoft továbbra is fontos, hogy támogató a [adatközpont-absztrakciós](http://technet.microsoft.com/cloud/dal.aspx) réteg (DAL) vision, és a megjelenítendő érték ügyfeleink és partnereink számára ezen a helyen.</span><span class="sxs-lookup"><span data-stu-id="faf7d-110">Microsoft remains committed to supporting the [Datacenter Abstraction](http://technet.microsoft.com/cloud/dal.aspx) Layer (DAL) vision, and to show value for our customers and partners in this space.</span></span> <span data-ttu-id="faf7d-111">Ezek a parancsmagok használatával hajthatja végre:</span><span class="sxs-lookup"><span data-stu-id="faf7d-111">Using these cmdlets you can perform:</span></span>

- <span data-ttu-id="faf7d-112">Globális váltson konfigurációs, például:</span><span class="sxs-lookup"><span data-stu-id="faf7d-112">Global switch configuration, such as:</span></span>
    - <span data-ttu-id="faf7d-113">Gazdagép nevének beállítása</span><span class="sxs-lookup"><span data-stu-id="faf7d-113">Set host name</span></span>
    - <span data-ttu-id="faf7d-114">Set kapcsoló szalagcím</span><span class="sxs-lookup"><span data-stu-id="faf7d-114">Set switch banner</span></span>
    - <span data-ttu-id="faf7d-115">Konfigurációs megőrzése</span><span class="sxs-lookup"><span data-stu-id="faf7d-115">Persist configuration</span></span>
    - <span data-ttu-id="faf7d-116">Engedélyezi vagy letiltja a szolgáltatás</span><span class="sxs-lookup"><span data-stu-id="faf7d-116">Enable or disable feature</span></span>

- <span data-ttu-id="faf7d-117">VLAN-konfiguráció:</span><span class="sxs-lookup"><span data-stu-id="faf7d-117">VLAN configuration:</span></span>
    - <span data-ttu-id="faf7d-118">Hozzon létre vagy VLAN eltávolítása</span><span class="sxs-lookup"><span data-stu-id="faf7d-118">Create or remove VLAN</span></span>
    - <span data-ttu-id="faf7d-119">Engedélyezheti vagy tilthatja le a VLAN</span><span class="sxs-lookup"><span data-stu-id="faf7d-119">Enable or disable VLAN</span></span>
    - <span data-ttu-id="faf7d-120">VLAN számbavétele</span><span class="sxs-lookup"><span data-stu-id="faf7d-120">Enumerate VLAN</span></span>
    - <span data-ttu-id="faf7d-121">Rövid név beállítása egy VLAN-hoz</span><span class="sxs-lookup"><span data-stu-id="faf7d-121">Set friendly name to a VLAN</span></span>

- <span data-ttu-id="faf7d-122">2. rétegbeli port konfigurációja:</span><span class="sxs-lookup"><span data-stu-id="faf7d-122">Layer 2 port configuration:</span></span>
    - <span data-ttu-id="faf7d-123">Portok számbavétele</span><span class="sxs-lookup"><span data-stu-id="faf7d-123">Enumerate ports</span></span>
    - <span data-ttu-id="faf7d-124">Engedélyezheti vagy tilthatja le a portok</span><span class="sxs-lookup"><span data-stu-id="faf7d-124">Enable or disable ports</span></span>
    - <span data-ttu-id="faf7d-125">Beállított port módok és tulajdonságai</span><span class="sxs-lookup"><span data-stu-id="faf7d-125">Set port modes and properties</span></span>
    - <span data-ttu-id="faf7d-126">Adja hozzá, vagy VLAN-Trönk vagy a hozzáférés a porton társítása</span><span class="sxs-lookup"><span data-stu-id="faf7d-126">Add or associate VLAN to Trunk or Access on the port</span></span>

<span data-ttu-id="faf7d-127">Indítsa el a NetworkSwitch parancsmagok mindegyikét keres vizsgálatát!</span><span class="sxs-lookup"><span data-stu-id="faf7d-127">Start exploring by looking for all of the NetworkSwitch cmdlets!</span></span>

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

<span data-ttu-id="faf7d-128">További információ a WMF 5.0-s előzetes bejelentés ebben a blogbejegyzésben Jeffrey Snover érhető el: <http://blogs.technet.com/b/windowsserver/archive/2014/04/03/windows-management-framework-v5-preview.aspx></span><span class="sxs-lookup"><span data-stu-id="faf7d-128">More information is available in Jeffrey Snover’s WMF 5.0 Preview announcement blog post: <http://blogs.technet.com/b/windowsserver/archive/2014/04/03/windows-management-framework-v5-preview.aspx></span></span>
