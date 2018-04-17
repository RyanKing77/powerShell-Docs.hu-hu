---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: A DSC lekérési ügyfél beállítása
ms.openlocfilehash: 4c56671313b93cc12ce9460ce41e1710e0d6a526
ms.sourcegitcommit: ece1794c94be4880a2af5a2605ed4721593643b6
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/16/2018
---
# <a name="setting-up-a-dsc-pull-client"></a><span data-ttu-id="238b0-103">A DSC lekérési ügyfél beállítása</span><span class="sxs-lookup"><span data-stu-id="238b0-103">Setting up a DSC pull client</span></span>

> <span data-ttu-id="238b0-104">Vonatkozik: A Windows PowerShell 4.0-s verzióját, a Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="238b0-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

> [!IMPORTANT]
> <span data-ttu-id="238b0-105">A lekéréses kiszolgáló (Windows-szolgáltatás *DSC-szolgáltatás*), Windows Server támogatott összetevője létezik azonban a következők: nem tervezi, hogy új funkciók és képességek kínálnak.</span><span class="sxs-lookup"><span data-stu-id="238b0-105">The Pull Server (Windows Feature *DSC-Service*) is a supported component of Windows Server however there are no plans to offer new features or capabilities.</span></span> <span data-ttu-id="238b0-106">Javasoljuk, hogy kezdje a Váltás felügyelt ügyfelek [Azure Automation DSC](/azure/automation/automation-dsc-getting-started) (tartalmazza a Windows Server-kiszolgáló lekéréses is) vagy a közösségi megoldásoknak a valamelyikét felsorolt [Itt](pullserver.md#community-solutions-for-pull-service).</span><span class="sxs-lookup"><span data-stu-id="238b0-106">It is recommended to begin transitioning managed clients to [Azure Automation DSC](/azure/automation/automation-dsc-getting-started) (includes features beyond Pull Server on Windows Server) or one of the community solutions listed [here](pullserver.md#community-solutions-for-pull-service).</span></span>

<span data-ttu-id="238b0-107">Minden cél fürtcsomópont lekéréses módban a rendszergazda és megadott URL-cím vagy a fájl helyét, akkor vegye fel a kapcsolatot a lekérési kiszolgálójával, hogy konfigurációk és erőforrások helyével, valamint azt kell jelentésadatok küldése.</span><span class="sxs-lookup"><span data-stu-id="238b0-107">Each target node has to be told to use pull mode and given the URL or file location where it can contact the pull server to get configurations and resources, and where it should send report data.</span></span>

<span data-ttu-id="238b0-108">Az alábbi témakörök ismertetik a lekéréses ügyfelek beállítása:</span><span class="sxs-lookup"><span data-stu-id="238b0-108">The following topics explain how to set up pull clients:</span></span>

* [<span data-ttu-id="238b0-109">Lekérési ügyfél beállítása konfigurációs nevekkel</span><span class="sxs-lookup"><span data-stu-id="238b0-109">Setting up a pull client using configuration names</span></span>](pullClientConfigNames.md)
* [<span data-ttu-id="238b0-110">Lekérési ügyfél beállítása konfigurációs azonosítóval</span><span class="sxs-lookup"><span data-stu-id="238b0-110">Setting up a pull client using configuration ID</span></span>](pullClientConfigID.md)

> <span data-ttu-id="238b0-111">**Megjegyzés:**: ezek a témakörök PowerShell 5.0 vonatkozik.</span><span class="sxs-lookup"><span data-stu-id="238b0-111">**Note**: These topics apply to PowerShell 5.0.</span></span> <span data-ttu-id="238b0-112">A PowerShell 4.0 lekéréses ügyfél beállításához tekintse meg a [ügyféltelepítéshez lekéréses konfigurációs azonosítójával PowerShell 4.0](pullClientConfigID4.md).</span><span class="sxs-lookup"><span data-stu-id="238b0-112">To set up a pull client in PowerShell 4.0, see [Setting up a pull client using configuration ID in PowerShell 4.0](pullClientConfigID4.md).</span></span>