---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: WMF, powershell, beállítás
title: A WMF 5.1 kibocsátási megjegyzései
ms.openlocfilehash: 5c3075eda5482cc6a43bd237fe4fca0064136753
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/17/2018
ms.locfileid: "34219436"
---
# <a name="windows-management-framework-wmf-51-release-notes"></a><span data-ttu-id="ad25e-103">A Windows Management Framework (WMF) 5.1 kibocsátási megjegyzések</span><span class="sxs-lookup"><span data-stu-id="ad25e-103">Windows Management Framework (WMF) 5.1 Release Notes</span></span> #

<span data-ttu-id="ad25e-104">WMF 5.1 összetevői a PowerShell, a WMI, a Rendszerfelügyeleti webszolgáltatások és a szoftverleltár-naplózási (SIL) a Windows Server 2016 kiadott.</span><span class="sxs-lookup"><span data-stu-id="ad25e-104">WMF 5.1 includes the PowerShell, WMI, WinRM, and Software Inventory Logging (SIL) components that were released with Windows Server 2016.</span></span>
<span data-ttu-id="ad25e-105">A WMF 5.1 Windows 7, Windows 8.1, Windows Server 2008 R2, 2012 és 2012 R2 rendszerre telepíthető, és számos javítást tartalmaz a WMF 5.0 RTM-hez képest, melyek többek között a következők:</span><span class="sxs-lookup"><span data-stu-id="ad25e-105">WMF 5.1 can be installed on Windows 7, Windows 8.1, Windows Server 2008 R2, 2012, and 2012 R2, and provides a number of improvements over WMF 5.0 RTM including:</span></span>

- <span data-ttu-id="ad25e-106">Új parancsmagok: helyi felhasználók és csoportok; Get-ComputerInfo</span><span class="sxs-lookup"><span data-stu-id="ad25e-106">New cmdlets: local users and groups; Get-ComputerInfo</span></span>
- <span data-ttu-id="ad25e-107">A PowerShellGet javításai, többek között az aláírt modulok használatának kényszerítése és a JEA-modulok telepítése</span><span class="sxs-lookup"><span data-stu-id="ad25e-107">PowerShellGet improvements include enforcing signed modules, and installing JEA modules</span></span>
- <span data-ttu-id="ad25e-108">A PackageManagement mostantól támogatja a Containers szolgáltatást, a CBS-beállítást, az EXE-alapú beállítást és a CAB-csomagokat</span><span class="sxs-lookup"><span data-stu-id="ad25e-108">PackageManagement added support for Containers, CBS Setup, EXE-based setup, CAB packages</span></span>
- <span data-ttu-id="ad25e-109">DSC- és PowerShell-osztályok hibakeresési javításai</span><span class="sxs-lookup"><span data-stu-id="ad25e-109">Debugging improvements for DSC and PowerShell classes</span></span>
- <span data-ttu-id="ad25e-110">Biztonsági fejlesztések: katalógus által aláírt modulok használatának kényszerítése a lekérési kiszolgálóról érkező modulok, illetve PowerShellGet-parancsmagok használata esetén</span><span class="sxs-lookup"><span data-stu-id="ad25e-110">Security enhancements including enforcement of catalog-signed modules coming from the Pull Server and when using PowerShellGet cmdlets</span></span>
- <span data-ttu-id="ad25e-111">Válaszok néhány felhasználói kérésre és problémára</span><span class="sxs-lookup"><span data-stu-id="ad25e-111">Responses to a number of user requests and issues</span></span>

<span data-ttu-id="ad25e-112">**Fontos megjegyzések:**</span><span class="sxs-lookup"><span data-stu-id="ad25e-112">**Important notes:**</span></span>

- <span data-ttu-id="ad25e-113">**WMF 5.1 a .NET-keretrendszer 4.5.2-es szükséges** (vagy újabb).</span><span class="sxs-lookup"><span data-stu-id="ad25e-113">**WMF 5.1 requires the .NET Framework 4.5.2** (or above).</span></span> <span data-ttu-id="ad25e-114">Telepítés sikeres lesz, azonban a legfontosabb jellemzők sikertelen lesz, ha a .NET 4.5.2 (vagy újabb) nincs telepítve.</span><span class="sxs-lookup"><span data-stu-id="ad25e-114">Installation will succeed, but key features will fail if .NET 4.5.2 (or above) is not installed.</span></span> <span data-ttu-id="ad25e-115">Útmutatás a érhető el a [telepítése és konfigurálása a WMF 5.1 ](https://msdn.microsoft.com/powershell/wmf/5.1/install-configure) témakör.</span><span class="sxs-lookup"><span data-stu-id="ad25e-115">Instructions are available in the [Install and Configure WMF 5.1 ](https://msdn.microsoft.com/powershell/wmf/5.1/install-configure) topic.</span></span>
- <span data-ttu-id="ad25e-116">WMF 5.1 Preview WMF 5.1 RTM telepítése előtt el kell távolítani.</span><span class="sxs-lookup"><span data-stu-id="ad25e-116">WMF 5.1 Preview must be uninstalled before installing WMF 5.1 RTM.</span></span>
- <span data-ttu-id="ad25e-117">WMF 5.1 WMF 5.0 vagy a WMF 4.0 keresztül közvetlenül is telepíthető.</span><span class="sxs-lookup"><span data-stu-id="ad25e-117">WMF 5.1 may be installed directly over WMF 5.0 or WMF 4.0.</span></span>
- <span data-ttu-id="ad25e-118">Az __nem szükséges__ WMF 4.0 telepítése WMF 5.1 a Windows 7 és Windows Server 2008 R2 telepítése előtt.</span><span class="sxs-lookup"><span data-stu-id="ad25e-118">It is __not required__ to install WMF 4.0 prior to installing WMF 5.1 on Windows 7 and Windows Server 2008 R2.</span></span> <span data-ttu-id="ad25e-119">Amely WMF 5.1 előzetes problémát, és lett feloldva.</span><span class="sxs-lookup"><span data-stu-id="ad25e-119">That was an issue for the WMF 5.1 Preview release, and has been resolved.</span></span>
