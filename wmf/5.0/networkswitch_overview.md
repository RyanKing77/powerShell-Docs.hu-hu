---
ms.date: 06/12/2017
author: JKeithB
ms.topic: reference
keywords: WMF, powershell, beállítás
ms.openlocfilehash: 2b6b81d250c3d745f3ab21ebadb9a657583638b0
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="network-switch-management-with-powershell"></a><span data-ttu-id="35e3f-102">Hálózati kapcsolók kezelése a PowerShell-lel</span><span class="sxs-lookup"><span data-stu-id="35e3f-102">Network Switch Management with PowerShell</span></span>

<span data-ttu-id="35e3f-103">A **Get-NetworkSwitchEthernetPort** parancsmag most osztályt a következő kiegészítő információkat ad vissza:</span><span class="sxs-lookup"><span data-stu-id="35e3f-103">The **Get-NetworkSwitchEthernetPort** cmdlet now returns the following additional information with instances:</span></span>

- <span data-ttu-id="35e3f-104">IP-cím – az a port társított IP-cím</span><span class="sxs-lookup"><span data-stu-id="35e3f-104">IPAddress – the IP address associated with the port</span></span>
- <span data-ttu-id="35e3f-105">PortMode – a port mód: hozzáférés, útvonal vagy trönk</span><span class="sxs-lookup"><span data-stu-id="35e3f-105">PortMode – the port mode: access, route, or trunk</span></span>
- <span data-ttu-id="35e3f-106">AccessVLAN – a VLAN Azonosítóját társított ezt a portot, a hozzáférési mód</span><span class="sxs-lookup"><span data-stu-id="35e3f-106">AccessVLAN – the ID of the VLAN associated with this port in access mode</span></span>
- <span data-ttu-id="35e3f-107">TrunkedVLANList – Ez a port trönk módban tartozó azonosítók a VLAN hálózatok listája</span><span class="sxs-lookup"><span data-stu-id="35e3f-107">TrunkedVLANList – a list of IDs of VLANs associated with this port in trunk mode</span></span>

## <a name="fundamental-network-switch-management-with-windows-powershell"></a><span data-ttu-id="35e3f-108">Alapvető hálózati kapcsoló kezelése a Windows PowerShell használatával</span><span class="sxs-lookup"><span data-stu-id="35e3f-108">Fundamental network switch management with Windows PowerShell</span></span>

<span data-ttu-id="35e3f-109">A Hálózatikapcsoló-parancsmagjai, a WMF 5.0-ben bevezetett lehetővé teszik a Windows Server 2012 R2 embléma hitelesített hálózati kapcsolók kapcsoló, a virtuális LAN (VLAN) és a 2. rétegbeli hálózati kapcsoló port alapkonfiguráció alkalmazandó.</span><span class="sxs-lookup"><span data-stu-id="35e3f-109">The Network Switch cmdlets, introduced in WMF 5.0, enable you to apply switch, virtual LAN (VLAN), and basic Layer 2 network switch port configuration to Windows Server 2012 R2 logo-certified network switches.</span></span> <span data-ttu-id="35e3f-110">Microsoft továbbra is támogató véglegesíteni a [adatközpont-absztrakciós](http://technet.microsoft.com/cloud/dal.aspx) réteg (DAL) stratégiai, és az érték szerepel, az ügyfelek és a partnerek ezen a helyen.</span><span class="sxs-lookup"><span data-stu-id="35e3f-110">Microsoft remains committed to supporting the [Datacenter Abstraction](http://technet.microsoft.com/cloud/dal.aspx) Layer (DAL) vision, and to show value for our customers and partners in this space.</span></span> <span data-ttu-id="35e3f-111">Ezek a parancsmagok használatával hajthatja végre:</span><span class="sxs-lookup"><span data-stu-id="35e3f-111">Using these cmdlets you can perform:</span></span>

- <span data-ttu-id="35e3f-112">Globális konfigurációs, például a kapcsolóhoz:</span><span class="sxs-lookup"><span data-stu-id="35e3f-112">Global switch configuration, such as:</span></span>
    - <span data-ttu-id="35e3f-113">Gazdagép neve</span><span class="sxs-lookup"><span data-stu-id="35e3f-113">Set host name</span></span>
    - <span data-ttu-id="35e3f-114">Set kapcsoló szalagcím</span><span class="sxs-lookup"><span data-stu-id="35e3f-114">Set switch banner</span></span>
    - <span data-ttu-id="35e3f-115">Konfigurációs megőrzése</span><span class="sxs-lookup"><span data-stu-id="35e3f-115">Persist configuration</span></span>
    - <span data-ttu-id="35e3f-116">Engedélyezheti vagy tilthatja le a szolgáltatást</span><span class="sxs-lookup"><span data-stu-id="35e3f-116">Enable or disable feature</span></span>

- <span data-ttu-id="35e3f-117">VLAN-konfiguráció:</span><span class="sxs-lookup"><span data-stu-id="35e3f-117">VLAN configuration:</span></span>
    - <span data-ttu-id="35e3f-118">Hozzon létre, vagy távolítsa el a VLAN</span><span class="sxs-lookup"><span data-stu-id="35e3f-118">Create or remove VLAN</span></span>
    - <span data-ttu-id="35e3f-119">Engedélyezheti vagy tilthatja le a VLAN</span><span class="sxs-lookup"><span data-stu-id="35e3f-119">Enable or disable VLAN</span></span>
    - <span data-ttu-id="35e3f-120">VLAN számbavétele</span><span class="sxs-lookup"><span data-stu-id="35e3f-120">Enumerate VLAN</span></span>
    - <span data-ttu-id="35e3f-121">Állítsa be a rövid nevet a VLAN-hoz</span><span class="sxs-lookup"><span data-stu-id="35e3f-121">Set friendly name to a VLAN</span></span>

- <span data-ttu-id="35e3f-122">2. réteg port konfigurálása:</span><span class="sxs-lookup"><span data-stu-id="35e3f-122">Layer 2 port configuration:</span></span>
    - <span data-ttu-id="35e3f-123">Portok számbavétele</span><span class="sxs-lookup"><span data-stu-id="35e3f-123">Enumerate ports</span></span>
    - <span data-ttu-id="35e3f-124">Engedélyezheti vagy tilthatja le a portok</span><span class="sxs-lookup"><span data-stu-id="35e3f-124">Enable or disable ports</span></span>
    - <span data-ttu-id="35e3f-125">Set port módok és tulajdonságai</span><span class="sxs-lookup"><span data-stu-id="35e3f-125">Set port modes and properties</span></span>
    - <span data-ttu-id="35e3f-126">Adja hozzá, vagy VLAN-Trönk vagy a hozzáférés a porton társítása</span><span class="sxs-lookup"><span data-stu-id="35e3f-126">Add or associate VLAN to Trunk or Access on the port</span></span>

<span data-ttu-id="35e3f-127">Fedezze fel az összes NetworkSwitch!</span><span class="sxs-lookup"><span data-stu-id="35e3f-127">Start exploring by looking for all of the NetworkSwitch cmdlets!</span></span>

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

<span data-ttu-id="35e3f-128">További információ a Jeffrey Snover WMF 5.0 előzetes bejelentés blogbejegyzésben érhető el: <http://blogs.technet.com/b/windowsserver/archive/2014/04/03/windows-management-framework-v5-preview.aspx></span><span class="sxs-lookup"><span data-stu-id="35e3f-128">More information is available in Jeffrey Snover’s WMF 5.0 Preview announcement blog post: <http://blogs.technet.com/b/windowsserver/archive/2014/04/03/windows-management-framework-v5-preview.aspx></span></span>