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
# <a name="network-switch-management-with-powershell"></a><span data-ttu-id="f083a-102">Hálózati kapcsoló kezelése a PowerShell használatával</span><span class="sxs-lookup"><span data-stu-id="f083a-102">Network Switch Management with PowerShell</span></span>

<span data-ttu-id="f083a-103">A **Get-NetworkSwitchEthernetPort** parancsmag most osztályt a következő kiegészítő információkat ad vissza:</span><span class="sxs-lookup"><span data-stu-id="f083a-103">The **Get-NetworkSwitchEthernetPort** cmdlet now returns the following additional information with instances:</span></span>

- <span data-ttu-id="f083a-104">IP-cím – az a port társított IP-cím</span><span class="sxs-lookup"><span data-stu-id="f083a-104">IPAddress – the IP address associated with the port</span></span>
- <span data-ttu-id="f083a-105">PortMode – a port mód: hozzáférés, útvonal vagy trönk</span><span class="sxs-lookup"><span data-stu-id="f083a-105">PortMode – the port mode: access, route, or trunk</span></span>
- <span data-ttu-id="f083a-106">AccessVLAN – a VLAN Azonosítóját társított ezt a portot, a hozzáférési mód</span><span class="sxs-lookup"><span data-stu-id="f083a-106">AccessVLAN – the ID of the VLAN associated with this port in access mode</span></span>
- <span data-ttu-id="f083a-107">TrunkedVLANList – Ez a port trönk módban tartozó azonosítók a VLAN hálózatok listája</span><span class="sxs-lookup"><span data-stu-id="f083a-107">TrunkedVLANList – a list of IDs of VLANs associated with this port in trunk mode</span></span>

## <a name="fundamental-network-switch-management-with-windows-powershell"></a><span data-ttu-id="f083a-108">Alapvető hálózati kapcsoló kezelése a Windows PowerShell használatával</span><span class="sxs-lookup"><span data-stu-id="f083a-108">Fundamental network switch management with Windows PowerShell</span></span>

<span data-ttu-id="f083a-109">A Hálózatikapcsoló-parancsmagjai, a WMF 5.0-ben bevezetett lehetővé teszik a Windows Server 2012 R2 embléma hitelesített hálózati kapcsolók kapcsoló, a virtuális LAN (VLAN) és a 2. rétegbeli hálózati kapcsoló port alapkonfiguráció alkalmazandó.</span><span class="sxs-lookup"><span data-stu-id="f083a-109">The Network Switch cmdlets, introduced in WMF 5.0, enable you to apply switch, virtual LAN (VLAN), and basic Layer 2 network switch port configuration to Windows Server 2012 R2 logo-certified network switches.</span></span> <span data-ttu-id="f083a-110">Microsoft továbbra is támogató véglegesíteni a [adatközpont-absztrakciós](http://technet.microsoft.com/en-us/cloud/dal.aspx) réteg (DAL) stratégiai, és az érték szerepel, az ügyfelek és a partnerek ezen a helyen.</span><span class="sxs-lookup"><span data-stu-id="f083a-110">Microsoft remains committed to supporting the [Datacenter Abstraction](http://technet.microsoft.com/en-us/cloud/dal.aspx) Layer (DAL) vision, and to show value for our customers and partners in this space.</span></span> <span data-ttu-id="f083a-111">Ezek a parancsmagok használatával hajthatja végre:</span><span class="sxs-lookup"><span data-stu-id="f083a-111">Using these cmdlets you can perform:</span></span>

- <span data-ttu-id="f083a-112">Globális konfigurációs, például a kapcsolóhoz:</span><span class="sxs-lookup"><span data-stu-id="f083a-112">Global switch configuration, such as:</span></span>
    - <span data-ttu-id="f083a-113">Gazdagép neve</span><span class="sxs-lookup"><span data-stu-id="f083a-113">Set host name</span></span>
    - <span data-ttu-id="f083a-114">Set kapcsoló szalagcím</span><span class="sxs-lookup"><span data-stu-id="f083a-114">Set switch banner</span></span>
    - <span data-ttu-id="f083a-115">Konfigurációs megőrzése</span><span class="sxs-lookup"><span data-stu-id="f083a-115">Persist configuration</span></span>
    - <span data-ttu-id="f083a-116">Engedélyezheti vagy tilthatja le a szolgáltatást</span><span class="sxs-lookup"><span data-stu-id="f083a-116">Enable or disable feature</span></span>

- <span data-ttu-id="f083a-117">VLAN-konfiguráció:</span><span class="sxs-lookup"><span data-stu-id="f083a-117">VLAN configuration:</span></span>
    - <span data-ttu-id="f083a-118">Hozzon létre, vagy távolítsa el a VLAN</span><span class="sxs-lookup"><span data-stu-id="f083a-118">Create or remove VLAN</span></span>
    - <span data-ttu-id="f083a-119">Engedélyezheti vagy tilthatja le a VLAN</span><span class="sxs-lookup"><span data-stu-id="f083a-119">Enable or disable VLAN</span></span>
    - <span data-ttu-id="f083a-120">VLAN számbavétele</span><span class="sxs-lookup"><span data-stu-id="f083a-120">Enumerate VLAN</span></span>
    - <span data-ttu-id="f083a-121">Állítsa be a rövid nevet a VLAN-hoz</span><span class="sxs-lookup"><span data-stu-id="f083a-121">Set friendly name to a VLAN</span></span>

- <span data-ttu-id="f083a-122">2. réteg port konfigurálása:</span><span class="sxs-lookup"><span data-stu-id="f083a-122">Layer 2 port configuration:</span></span>
    - <span data-ttu-id="f083a-123">Portok számbavétele</span><span class="sxs-lookup"><span data-stu-id="f083a-123">Enumerate ports</span></span>
    - <span data-ttu-id="f083a-124">Engedélyezheti vagy tilthatja le a portok</span><span class="sxs-lookup"><span data-stu-id="f083a-124">Enable or disable ports</span></span>
    - <span data-ttu-id="f083a-125">Set port módok és tulajdonságai</span><span class="sxs-lookup"><span data-stu-id="f083a-125">Set port modes and properties</span></span>
    - <span data-ttu-id="f083a-126">Adja hozzá, vagy VLAN-Trönk vagy a hozzáférés a porton társítása</span><span class="sxs-lookup"><span data-stu-id="f083a-126">Add or associate VLAN to Trunk or Access on the port</span></span>

<span data-ttu-id="f083a-127">Fedezze fel az összes NetworkSwitch!</span><span class="sxs-lookup"><span data-stu-id="f083a-127">Start exploring by looking for all of the NetworkSwitch cmdlets!</span></span>

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

<span data-ttu-id="f083a-128">További információ a Jeffrey Snover WMF 5.0 előzetes bejelentés blogbejegyzésben érhető el: <http://blogs.technet.com/b/windowsserver/archive/2014/04/03/windows-management-framework-v5-preview.aspx></span><span class="sxs-lookup"><span data-stu-id="f083a-128">More information is available in Jeffrey Snover’s WMF 5.0 Preview announcement blog post: <http://blogs.technet.com/b/windowsserver/archive/2014/04/03/windows-management-framework-v5-preview.aspx></span></span>

