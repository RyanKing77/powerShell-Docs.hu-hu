---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: DSC lekérési ügyfél beállítása
ms.openlocfilehash: b7cd6dc0087eb8368c5467df4c3c7266ed704451
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/14/2018
ms.locfileid: "53404149"
---
# <a name="setting-up-a-dsc-pull-client"></a><span data-ttu-id="1a53a-103">DSC lekérési ügyfél beállítása</span><span class="sxs-lookup"><span data-stu-id="1a53a-103">Setting up a DSC pull client</span></span>

> <span data-ttu-id="1a53a-104">Érvényes: Windows PowerShell 4.0-s, a Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="1a53a-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1a53a-105">A lekéréses kiszolgálón (Windows-szolgáltatás *DSC-szolgáltatás*), a Windows Server támogatott összetevője létezik azonban tervekben sem funkciókat és képességeket kínálnak.</span><span class="sxs-lookup"><span data-stu-id="1a53a-105">The Pull Server (Windows Feature *DSC-Service*) is a supported component of Windows Server however there are no plans to offer new features or capabilities.</span></span> <span data-ttu-id="1a53a-106">Javasoljuk, hogy helyeződnek felügyelt ügyfelek [Azure Automation DSC](/azure/automation/automation-dsc-getting-started) (beleértve a lekéréses kiszolgálón a Windows Server csomagban) vagy a közösségi megoldások felsorolt [Itt](pullserver.md#community-solutions-for-pull-service).</span><span class="sxs-lookup"><span data-stu-id="1a53a-106">It is recommended to begin transitioning managed clients to [Azure Automation DSC](/azure/automation/automation-dsc-getting-started) (includes features beyond Pull Server on Windows Server) or one of the community solutions listed [here](pullserver.md#community-solutions-for-pull-service).</span></span>

<span data-ttu-id="1a53a-107">Minden egyes célcsomóponttal le kell lekéréses mód használatára, hogy rendelkezik, és megadott URL-cím vagy a fájl helyét, ahol ezt a kapcsolatot a lekéréses kiszolgálón beolvasni a konfigurációkat és erőforrásokat, és ha kell adatokat küldhessen a azt.</span><span class="sxs-lookup"><span data-stu-id="1a53a-107">Each target node has to be told to use pull mode and given the URL or file location where it can contact the pull server to get configurations and resources, and where it should send report data.</span></span>

<span data-ttu-id="1a53a-108">A következő témakörök azt ismertetik, hogyan állítsa be a pull-ügyfelek:</span><span class="sxs-lookup"><span data-stu-id="1a53a-108">The following topics explain how to set up pull clients:</span></span>

* [<span data-ttu-id="1a53a-109">Lekérési ügyfél beállítása konfigurációs nevekkel</span><span class="sxs-lookup"><span data-stu-id="1a53a-109">Setting up a pull client using configuration names</span></span>](pullClientConfigNames.md)
* [<span data-ttu-id="1a53a-110">Lekérési ügyfél beállítása konfigurációs azonosítóval</span><span class="sxs-lookup"><span data-stu-id="1a53a-110">Setting up a pull client using configuration ID</span></span>](pullClientConfigID.md)

> <span data-ttu-id="1a53a-111">**Megjegyzés:**: Ezek a témakörök a PowerShell 5.0-s vonatkozik.</span><span class="sxs-lookup"><span data-stu-id="1a53a-111">**Note**: These topics apply to PowerShell 5.0.</span></span> <span data-ttu-id="1a53a-112">A PowerShell 4.0-s lekérési ügyfél beállítása, lásd: [egy lekérési ügyfél beállítása konfigurációs Azonosítóval a PowerShell 4.0-s](pullClientConfigID4.md).</span><span class="sxs-lookup"><span data-stu-id="1a53a-112">To set up a pull client in PowerShell 4.0, see [Setting up a pull client using configuration ID in PowerShell 4.0](pullClientConfigID4.md).</span></span>