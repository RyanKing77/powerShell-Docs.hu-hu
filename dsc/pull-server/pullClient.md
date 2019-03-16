---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: DSC lekérési ügyfél beállítása
ms.openlocfilehash: 54c68ac26e5388260e252ce01418170e26ddecde
ms.sourcegitcommit: caac7d098a448232304c9d6728e7340ec7517a71
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/16/2019
ms.locfileid: "58054254"
---
# <a name="setting-up-a-dsc-pull-client"></a><span data-ttu-id="21c63-103">DSC lekérési ügyfél beállítása</span><span class="sxs-lookup"><span data-stu-id="21c63-103">Setting up a DSC pull client</span></span>

> <span data-ttu-id="21c63-104">Érvényes: Windows PowerShell 4.0-s, a Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="21c63-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

> [!IMPORTANT]
> <span data-ttu-id="21c63-105">A lekéréses kiszolgálón (Windows-szolgáltatás *DSC-szolgáltatás*), a Windows Server támogatott összetevője létezik azonban tervekben sem funkciókat és képességeket kínálnak.</span><span class="sxs-lookup"><span data-stu-id="21c63-105">The Pull Server (Windows Feature *DSC-Service*) is a supported component of Windows Server however there are no plans to offer new features or capabilities.</span></span> <span data-ttu-id="21c63-106">Javasoljuk, hogy helyeződnek felügyelt ügyfelek [Azure Automation DSC](/azure/automation/automation-dsc-getting-started) (beleértve a lekéréses kiszolgálón a Windows Server csomagban) vagy a közösségi megoldások felsorolt [Itt](pullserver.md#community-solutions-for-pull-service).</span><span class="sxs-lookup"><span data-stu-id="21c63-106">It is recommended to begin transitioning managed clients to [Azure Automation DSC](/azure/automation/automation-dsc-getting-started) (includes features beyond Pull Server on Windows Server) or one of the community solutions listed [here](pullserver.md#community-solutions-for-pull-service).</span></span>

<span data-ttu-id="21c63-107">Minden egyes célcsomóponttal le kell lekéréses mód használatára, hogy rendelkezik, és megadott URL-cím vagy a fájl helyét, ahol ezt a kapcsolatot a lekéréses kiszolgálón beolvasni a konfigurációkat és erőforrásokat, és ha kell adatokat küldhessen a azt.</span><span class="sxs-lookup"><span data-stu-id="21c63-107">Each target node has to be told to use pull mode and given the URL or file location where it can contact the pull server to get configurations and resources, and where it should send report data.</span></span>

<span data-ttu-id="21c63-108">A következő témakörök azt ismertetik, hogyan állítsa be a pull-ügyfelek:</span><span class="sxs-lookup"><span data-stu-id="21c63-108">The following topics explain how to set up pull clients:</span></span>

* [<span data-ttu-id="21c63-109">Lekérési ügyfél beállítása konfigurációs nevekkel</span><span class="sxs-lookup"><span data-stu-id="21c63-109">Setting up a pull client using configuration names</span></span>](pullClientConfigNames.md)
* [<span data-ttu-id="21c63-110">Lekérési ügyfél beállítása konfigurációs azonosítóval</span><span class="sxs-lookup"><span data-stu-id="21c63-110">Setting up a pull client using configuration ID</span></span>](pullClientConfigID.md)

> [!NOTE]
> <span data-ttu-id="21c63-111">Ezek a témakörök a PowerShell 5.0-s vonatkozik.</span><span class="sxs-lookup"><span data-stu-id="21c63-111">These topics apply to PowerShell 5.0.</span></span> <span data-ttu-id="21c63-112">A PowerShell 4.0-s lekérési ügyfél beállítása, lásd: [egy lekérési ügyfél beállítása konfigurációs Azonosítóval a PowerShell 4.0-s](pullClientConfigID4.md).</span><span class="sxs-lookup"><span data-stu-id="21c63-112">To set up a pull client in PowerShell 4.0, see [Setting up a pull client using configuration ID in PowerShell 4.0](pullClientConfigID4.md).</span></span>