---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: 07ebcfd37cc3e1f38a9434ffa8d86f479b89ee0f
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55685535"
---
# <a name="windows-management-framework-wmf-50-rtm-release-notes-overview"></a><span data-ttu-id="0ed92-102">Windows Management Framework (WMF) 5.0 RTM kibocsátási megjegyzések – áttekintés</span><span class="sxs-lookup"><span data-stu-id="0ed92-102">Windows Management Framework (WMF) 5.0 RTM Release Notes Overview</span></span>

<span data-ttu-id="0ed92-103">**A WMF 5.0 a WMF 5.1 helyettesít. A WMF 5.0-s felhasználók szeretne támogatást kapni a WMF 5.1 kell frissítenie. Kérjük, kövesse a [telepítési intructions a WMF 5.1](../5.1/install-configure.md)**</span><span class="sxs-lookup"><span data-stu-id="0ed92-103">**WMF 5.0 is superseded by WMF 5.1. Users with WMF 5.0 must upgrade to WMF 5.1 to receive support. Please follow the [installation intructions of WMF 5.1](../5.1/install-configure.md)**</span></span>

<span data-ttu-id="0ed92-104">Windows Management Framework (WMF) 5.0 RTM elérhetővé teszi a Funkciók, amelyek frissítve lett a WMF 4.0-s verzióját.</span><span class="sxs-lookup"><span data-stu-id="0ed92-104">Windows Management Framework (WMF) 5.0 RTM brings functionality that has been updated from WMF 4.0.</span></span> <span data-ttu-id="0ed92-105">A WMF 5.0 RTM-re érhető el a telepítést csak **Windows Server 2012 R2**, **Windows Server 2012**, **Windows Server 2008 R2**, **Windows 8.1**, és **Windows 7 SP1** , és tartalmazza a frissített verziója vagy a következő funkciók bevezetése:</span><span class="sxs-lookup"><span data-stu-id="0ed92-105">WMF 5.0 RTM is available for installation only on **Windows Server 2012 R2**, **Windows Server 2012**, **Windows Server 2008 R2**, **Windows 8.1**, and **Windows 7 SP1** and contains updated versions or introduction of the following features:</span></span>

- <span data-ttu-id="0ed92-106">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="0ed92-106">Windows PowerShell</span></span>
- <span data-ttu-id="0ed92-107">Just Enough Administration (JEA)</span><span class="sxs-lookup"><span data-stu-id="0ed92-107">Just Enough Administration (JEA)</span></span>
- <span data-ttu-id="0ed92-108">Windows PowerShell célállapot konfiguráló szolgáltatása (DSC)</span><span class="sxs-lookup"><span data-stu-id="0ed92-108">Windows PowerShell Desired State Configuration (DSC)</span></span>
- <span data-ttu-id="0ed92-109">Windows PowerShell integrált parancsfájlkezelési környezet (ISE)</span><span class="sxs-lookup"><span data-stu-id="0ed92-109">Windows PowerShell Integrated Scripting Environment (ISE)</span></span>
- <span data-ttu-id="0ed92-110">Windows PowerShell webszolgáltatások (felügyeleti OData IIS kiterjesztés)</span><span class="sxs-lookup"><span data-stu-id="0ed92-110">Windows PowerShell Web Services (Management OData IIS Extension)</span></span>
- <span data-ttu-id="0ed92-111">Rendszerfelügyeleti webszolgáltatások (WinRM)</span><span class="sxs-lookup"><span data-stu-id="0ed92-111">Windows Remote Management (WinRM)</span></span>
- <span data-ttu-id="0ed92-112">Windows Management Instrumentation (WMI)</span><span class="sxs-lookup"><span data-stu-id="0ed92-112">Windows Management Instrumentation (WMI)</span></span>

<span data-ttu-id="0ed92-113">A WMF 5.0 RTM-re váltja fel a [WMF 5.0 éles előzetes](http://blogs.msdn.com/b/powershell/archive/2015/08/31/windows-management-framework-5-0-production-preview-is-now-available.aspx).</span><span class="sxs-lookup"><span data-stu-id="0ed92-113">WMF 5.0 RTM replaces the [WMF 5.0 Production Preview](http://blogs.msdn.com/b/powershell/archive/2015/08/31/windows-management-framework-5-0-production-preview-is-now-available.aspx).</span></span> <span data-ttu-id="0ed92-114">Telepítheti a WMF 5.0 RTM-re a WMF 5.0 éles előzetes eltávolítása nélkül, de a WMF 5.0 RTM telepítése előtt el kell távolítania minden régebbi kiadásokban a WMF 5.0 előnézetek.</span><span class="sxs-lookup"><span data-stu-id="0ed92-114">You can install WMF 5.0 RTM without uninstalling WMF 5.0 Production Preview, but you must uninstall all other older releases of WMF 5.0 previews before installing the WMF 5.0 RTM.</span></span>

<span data-ttu-id="0ed92-115">*Megjegyzés:* Ha futtatja a Windows 10-es, ugyanazokat a funkciókat a WMF 5.0 RTM-hez elérhető megkaphassa a novemberi frissítésben Windows 10-es (1511-es verzióra) frissítése.</span><span class="sxs-lookup"><span data-stu-id="0ed92-115">*Note:* If you are running Windows 10, you can get the same set of functionality available in WMF 5.0 RTM by updating to the November update of Windows 10 (Version 1511).</span></span> <span data-ttu-id="0ed92-116">Ha még nem frissített a Windows 10 rendszert, kattintson a Start gombra, majd válassza a beállítások > Frissítés és Biztonság > Windows Update > frissítések keresése.</span><span class="sxs-lookup"><span data-stu-id="0ed92-116">If you have not already updated your Windows 10 system, select the Start button, then select Settings > Update & security > Windows Update > Check for updates.</span></span>
