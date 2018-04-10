---
ms.date: 08/12/2017
author: JKeithB
ms.topic: reference
keywords: WMF, powershell, beállítás
title: A WMF 5.1 kibocsátási megjegyzései
ms.openlocfilehash: 9df21afe52e79dc248871b999afead21f8678d52
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="windows-management-framework-wmf-51"></a><span data-ttu-id="34628-103">Windows Management Framework (WMF) 5.1</span><span class="sxs-lookup"><span data-stu-id="34628-103">Windows Management Framework (WMF) 5.1</span></span> #

<span data-ttu-id="34628-104">A WMF-fel a felhasználók frissíthetik meglévő Windowsos rendszereiket a PowerShell-, a WMI-, a WinRM- és a Szoftverleltár-naplózási (SIL) összetevő a Windows Server 2016-ban kiadott verzióira.</span><span class="sxs-lookup"><span data-stu-id="34628-104">WMF provides users with the ability to update existing Windows systems to the versions of PowerShell, WMI, WinRM, and Software Inventory Logging (SIL) components that were released with Windows Server 2016.</span></span>

<span data-ttu-id="34628-105">A WMF 5.1 Windows 7, Windows 8.1, Windows Server 2008 R2, 2012 és 2012 R2 rendszerre telepíthető, és számos javítást tartalmaz a WMF 5.0 RTM-hez képest, melyek többek között a következők:</span><span class="sxs-lookup"><span data-stu-id="34628-105">WMF 5.1 can be installed on Windows 7, Windows 8.1, Windows Server 2008 R2, 2012, and 2012 R2, and provides a number of improvements over WMF 5.0 RTM including:</span></span>

- <span data-ttu-id="34628-106">Új parancsmagok: helyi felhasználók és csoportok; Get-ComputerInfo</span><span class="sxs-lookup"><span data-stu-id="34628-106">New cmdlets: local users and groups; Get-ComputerInfo</span></span>
- <span data-ttu-id="34628-107">A PowerShellGet javításai, többek között az aláírt modulok használatának kényszerítése és a JEA-modulok telepítése</span><span class="sxs-lookup"><span data-stu-id="34628-107">PowerShellGet improvements include enforcing signed modules, and installing JEA modules</span></span>
- <span data-ttu-id="34628-108">A PackageManagement mostantól támogatja a Containers szolgáltatást, a CBS-beállítást, az EXE-alapú beállítást és a CAB-csomagokat</span><span class="sxs-lookup"><span data-stu-id="34628-108">PackageManagement added support for Containers, CBS Setup, EXE-based setup, CAB packages</span></span>
- <span data-ttu-id="34628-109">DSC- és PowerShell-osztályok hibakeresési javításai</span><span class="sxs-lookup"><span data-stu-id="34628-109">Debugging improvements for DSC and PowerShell classes</span></span>
- <span data-ttu-id="34628-110">Biztonsági fejlesztések: katalógus által aláírt modulok használatának kényszerítése a lekérési kiszolgálóról érkező modulok, illetve PowerShellGet-parancsmagok használata esetén</span><span class="sxs-lookup"><span data-stu-id="34628-110">Security enhancements including enforcement of catalog-signed modules coming from the Pull Server and when using PowerShellGet cmdlets</span></span>
- <span data-ttu-id="34628-111">Válaszok néhány felhasználói kérésre és problémára</span><span class="sxs-lookup"><span data-stu-id="34628-111">Responses to a number of user requests and issues</span></span>

<span data-ttu-id="34628-112">Ha többet szeretne megtudni a kiadás újdonságairól, tekintse meg az [Új forgatókönyvek és funkciók](https://docs.microsoft.com/en-us/powershell/wmf/5.1/scenarios-features) szakasz témaköreit.</span><span class="sxs-lookup"><span data-stu-id="34628-112">To learn about what is new in this release, browse the topics listed under [New Scenarios and Features](https://docs.microsoft.com/en-us/powershell/wmf/5.1/scenarios-features).</span></span>

<span data-ttu-id="34628-113">A [Telepítés és konfigurálás](https://docs.microsoft.com/en-us/powershell/wmf/5.1/install-configure) témakör a WMF követelményeit és telepítési utasításait ismerteti.</span><span class="sxs-lookup"><span data-stu-id="34628-113">The [Install and Configure](https://docs.microsoft.com/en-us/powershell/wmf/5.1/install-configure) topic lists the requirements and provides installation instructions for WMF.</span></span>

<span data-ttu-id="34628-114">A [Kompatibilitás](https://docs.microsoft.com/en-us/powershell/wmf/5.1/compatibility) témakör ismerteti, mely WMF-verziók mely Windows-kiadásokon telepíthetők.</span><span class="sxs-lookup"><span data-stu-id="34628-114">The [Compatibility](https://docs.microsoft.com/en-us/powershell/wmf/5.1/compatibility) topic lists which versions of WMF may be installed on which Windows releases.</span></span>

<span data-ttu-id="34628-115">A [Termékkompatibilitás](https://docs.microsoft.com/en-us/powershell/wmf/5.1/productincompat) témakör azokat a Microsoft-alkalmazásokat sorolja fel, amelyek még nem támogatják a WMF 5.1 szolgáltatást.</span><span class="sxs-lookup"><span data-stu-id="34628-115">[Product Compatibility](https://docs.microsoft.com/en-us/powershell/wmf/5.1/productincompat) lists the Microsoft applications that have not approved WMF 5.1 for use at this time.</span></span>

<span data-ttu-id="34628-116">A WMF összetevőiről részletes információt az MSDN-dokumentációban találhat:</span><span class="sxs-lookup"><span data-stu-id="34628-116">Details for the components of WMF will be found in MSDN documentation:</span></span>

- [<span data-ttu-id="34628-117">PowerShell 5.1</span><span class="sxs-lookup"><span data-stu-id="34628-117">PowerShell 5.1</span></span>](https://docs.microsoft.com/en-us/powershell/)
- <span data-ttu-id="34628-118">[WMI](https://msdn.microsoft.com/en-us/library/jj152383(v=vs.85).aspx)</span><span class="sxs-lookup"><span data-stu-id="34628-118">[WMI](https://msdn.microsoft.com/en-us/library/jj152383(v=vs.85).aspx)</span></span>
- <span data-ttu-id="34628-119">[WinRM](https://msdn.microsoft.com/en-us/library/aa384426(v=vs.85).aspx)</span><span class="sxs-lookup"><span data-stu-id="34628-119">[WinRM](https://msdn.microsoft.com/en-us/library/aa384426(v=vs.85).aspx)</span></span>
- <span data-ttu-id="34628-120">[Szoftverleltár-naplózás](https://technet.microsoft.com/en-us/library/dn383584(v=ws.11).aspx)</span><span class="sxs-lookup"><span data-stu-id="34628-120">[Software Inventory Logging](https://technet.microsoft.com/en-us/library/dn383584(v=ws.11).aspx)</span></span>