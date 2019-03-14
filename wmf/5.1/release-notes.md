---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: WMF, powershell, beállítás
title: A WMF 5.1 kibocsátási megjegyzései
ms.openlocfilehash: 61ca854cf8f26a9e96c6c5b5c06f6b54d08fb4ea
ms.sourcegitcommit: 5990f04b8042ef2d8e571bec6d5b051e64c9921c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/12/2019
ms.locfileid: "57795011"
---
# <a name="windows-management-framework-wmf-51-release-notes"></a><span data-ttu-id="37fd3-103">Windows Management Framework (WMF) 5.1 kibocsátási megjegyzései</span><span class="sxs-lookup"><span data-stu-id="37fd3-103">Windows Management Framework (WMF) 5.1 Release Notes</span></span>

<span data-ttu-id="37fd3-104">A WMF 5.1 összetevői a PowerShell, a WMI, a Rendszerfelügyeleti webszolgáltatások és a szoftverleltár-naplózási (SIL) kiadott – Windows Server 2016-ban.</span><span class="sxs-lookup"><span data-stu-id="37fd3-104">WMF 5.1 includes the PowerShell, WMI, WinRM, and Software Inventory Logging (SIL) components that were released with Windows Server 2016.</span></span>
<span data-ttu-id="37fd3-105">A WMF 5.1 Windows 7, Windows 8.1, Windows Server 2008 R2, 2012 és 2012 R2 rendszerre telepíthető, és számos javítást tartalmaz a WMF 5.0 RTM-hez képest, melyek többek között a következők:</span><span class="sxs-lookup"><span data-stu-id="37fd3-105">WMF 5.1 can be installed on Windows 7, Windows 8.1, Windows Server 2008 R2, 2012, and 2012 R2, and provides a number of improvements over WMF 5.0 RTM including:</span></span>

- <span data-ttu-id="37fd3-106">Új parancsmagok: helyi felhasználók és csoportok; Get-ComputerInfo</span><span class="sxs-lookup"><span data-stu-id="37fd3-106">New cmdlets: local users and groups; Get-ComputerInfo</span></span>
- <span data-ttu-id="37fd3-107">A PowerShellGet javításai, többek között az aláírt modulok használatának kényszerítése és a JEA-modulok telepítése</span><span class="sxs-lookup"><span data-stu-id="37fd3-107">PowerShellGet improvements include enforcing signed modules, and installing JEA modules</span></span>
- <span data-ttu-id="37fd3-108">A PackageManagement mostantól támogatja a Containers szolgáltatást, a CBS-beállítást, az EXE-alapú beállítást és a CAB-csomagokat</span><span class="sxs-lookup"><span data-stu-id="37fd3-108">PackageManagement added support for Containers, CBS Setup, EXE-based setup, CAB packages</span></span>
- <span data-ttu-id="37fd3-109">DSC- és PowerShell-osztályok hibakeresési javításai</span><span class="sxs-lookup"><span data-stu-id="37fd3-109">Debugging improvements for DSC and PowerShell classes</span></span>
- <span data-ttu-id="37fd3-110">Biztonsági fejlesztések: katalógus által aláírt modulok használatának kényszerítése a lekérési kiszolgálóról érkező modulok, illetve PowerShellGet-parancsmagok használata esetén</span><span class="sxs-lookup"><span data-stu-id="37fd3-110">Security enhancements including enforcement of catalog-signed modules coming from the Pull Server and when using PowerShellGet cmdlets</span></span>
- <span data-ttu-id="37fd3-111">Válaszok néhány felhasználói kérésre és problémára</span><span class="sxs-lookup"><span data-stu-id="37fd3-111">Responses to a number of user requests and issues</span></span>

<span data-ttu-id="37fd3-112">**Fontos megjegyzések:**</span><span class="sxs-lookup"><span data-stu-id="37fd3-112">**Important notes:**</span></span>

- <span data-ttu-id="37fd3-113">**A WMF 5.1 szükséges a .NET-keretrendszer 4.5.2-es** (vagy újabb).</span><span class="sxs-lookup"><span data-stu-id="37fd3-113">**WMF 5.1 requires the .NET Framework 4.5.2** (or above).</span></span> <span data-ttu-id="37fd3-114">Telepítés sikeres lesz, de a legfontosabb jellemzők sikertelen lesz, ha a .NET 4.5.2-es (vagy újabb) nincs telepítve.</span><span class="sxs-lookup"><span data-stu-id="37fd3-114">Installation will succeed, but key features will fail if .NET 4.5.2 (or above) is not installed.</span></span> <span data-ttu-id="37fd3-115">Útmutatást a [telepítése és konfigurálása a WMF 5.1-es](https://msdn.microsoft.com/powershell/wmf/5.1/install-configure) témakör.</span><span class="sxs-lookup"><span data-stu-id="37fd3-115">Instructions are available in the [Install and Configure WMF 5.1](https://msdn.microsoft.com/powershell/wmf/5.1/install-configure) topic.</span></span>
- <span data-ttu-id="37fd3-116">A WMF 5.1-es előzetes verzió a WMF 5.1 RTM telepítése előtt el kell távolítani.</span><span class="sxs-lookup"><span data-stu-id="37fd3-116">WMF 5.1 Preview must be uninstalled before installing WMF 5.1 RTM.</span></span>
- <span data-ttu-id="37fd3-117">A WMF 5.1 közvetlenül a WMF 5.0 vagy a WMF 4.0 keresztül lehet telepíteni.</span><span class="sxs-lookup"><span data-stu-id="37fd3-117">WMF 5.1 may be installed directly over WMF 5.0 or WMF 4.0.</span></span>
- <span data-ttu-id="37fd3-118">Ez __nem szükséges__ WMF 4.0 telepítése a WMF 5.1 Windows 7 és Windows Server 2008 R2 telepítése előtt.</span><span class="sxs-lookup"><span data-stu-id="37fd3-118">It is __not required__ to install WMF 4.0 prior to installing WMF 5.1 on Windows 7 and Windows Server 2008 R2.</span></span> <span data-ttu-id="37fd3-119">Amely a WMF 5.1-es előzetes kiadásban történt, és lett feloldva.</span><span class="sxs-lookup"><span data-stu-id="37fd3-119">That was an issue for the WMF 5.1 Preview release, and has been resolved.</span></span>
