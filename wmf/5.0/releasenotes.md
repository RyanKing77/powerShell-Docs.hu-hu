---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "WMF, a powershell, a beállítása"
ms.openlocfilehash: e88ce2d6956a10ec18daf4cd53927385854f9b55
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2017
---
# <a name="windows-management-framework-wmf-50-rtm-release-notes-overview"></a><span data-ttu-id="84db8-102">A Windows Management Framework (WMF) 5.0 RTM kibocsátási megjegyzések áttekintése</span><span class="sxs-lookup"><span data-stu-id="84db8-102">Windows Management Framework (WMF) 5.0 RTM Release Notes Overview</span></span>

<span data-ttu-id="84db8-103">Windows Management Framework (WMF) 5.0 RTM frissítve lett működésének során a WMF 4.0-s-ből.</span><span class="sxs-lookup"><span data-stu-id="84db8-103">Windows Management Framework (WMF) 5.0 RTM brings functionality that has been updated from WMF 4.0.</span></span> <span data-ttu-id="84db8-104">WMF 5.0 RTM érhető el a telepítés csak **Windows Server 2012 R2**, **Windows Server 2012**, **Windows Server 2008 R2**, **Windows 8.1**, és **Windows 7 SP1** és frissített verziója vagy bemutatása a következő szolgáltatásokat tartalmazza:</span><span class="sxs-lookup"><span data-stu-id="84db8-104">WMF 5.0 RTM is available for installation only on **Windows Server 2012 R2**, **Windows Server 2012**, **Windows Server 2008 R2**, **Windows 8.1**, and **Windows 7 SP1** and contains updated versions or introduction of the following features:</span></span>

- <span data-ttu-id="84db8-105">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="84db8-105">Windows PowerShell</span></span>
- <span data-ttu-id="84db8-106">Éppen elég felügyelettel (JEA)</span><span class="sxs-lookup"><span data-stu-id="84db8-106">Just Enough Administration (JEA)</span></span>
- <span data-ttu-id="84db8-107">Windows PowerShell célállapot konfiguráló szolgáltatása (DSC)</span><span class="sxs-lookup"><span data-stu-id="84db8-107">Windows PowerShell Desired State Configuration (DSC)</span></span>
- <span data-ttu-id="84db8-108">Windows PowerShell integrált parancsfájlkezelési környezet (ISE)</span><span class="sxs-lookup"><span data-stu-id="84db8-108">Windows PowerShell Integrated Scripting Environment (ISE)</span></span>
- <span data-ttu-id="84db8-109">A Windows PowerShell webszolgáltatások (felügyeleti OData IIS kiterjesztés)</span><span class="sxs-lookup"><span data-stu-id="84db8-109">Windows PowerShell Web Services (Management OData IIS Extension)</span></span> 
- <span data-ttu-id="84db8-110">Rendszerfelügyeleti webszolgáltatások (WinRM)</span><span class="sxs-lookup"><span data-stu-id="84db8-110">Windows Remote Management (WinRM)</span></span>
- <span data-ttu-id="84db8-111">Windows Management Instrumentation (WMI)</span><span class="sxs-lookup"><span data-stu-id="84db8-111">Windows Management Instrumentation (WMI)</span></span> 

<span data-ttu-id="84db8-112">WMF 5.0 RTM-re a felváltja a [WMF 5.0 éles előzetes](http://blogs.msdn.com/b/powershell/archive/2015/08/31/windows-management-framework-5-0-production-preview-is-now-available.aspx).</span><span class="sxs-lookup"><span data-stu-id="84db8-112">WMF 5.0 RTM replaces the [WMF 5.0 Production Preview](http://blogs.msdn.com/b/powershell/archive/2015/08/31/windows-management-framework-5-0-production-preview-is-now-available.aspx).</span></span> <span data-ttu-id="84db8-113">WMF 5.0 éles Preview eltávolítása nélkül WMF 5.0 RTM telepíthető, de a WMF 5.0 RTM telepítése előtt el kell távolítania minden régebbi kiadásai a WMF 5.0 az előzetes verziójú funkciók.</span><span class="sxs-lookup"><span data-stu-id="84db8-113">You can install WMF 5.0 RTM without uninstalling WMF 5.0 Production Preview, but you must uninstall all other older releases of WMF 5.0 previews before installing the WMF 5.0 RTM.</span></span>

<span data-ttu-id="84db8-114">*Megjegyzés:* Ha futtatja a Windows 10, kaphat ugyanazokat a funkció érhető el a WMF 5.0 RTM November frissítése a Windows 10 (1511-es verzió) frissítése.</span><span class="sxs-lookup"><span data-stu-id="84db8-114">*Note:* If you are running Windows 10, you can get the same set of functionality available in WMF 5.0 RTM by updating to the November update of Windows 10 (Version 1511).</span></span> <span data-ttu-id="84db8-115">Ha már nincs frissítve a Windows 10 rendszert, kattintson a Start gombra, majd válassza a beállítások > Frissítés és Biztonság > Windows Update > frissítések keresése.</span><span class="sxs-lookup"><span data-stu-id="84db8-115">If you have not already updated your Windows 10 system, select the Start button, then select Settings > Update & security > Windows Update > Check for updates.</span></span> 

