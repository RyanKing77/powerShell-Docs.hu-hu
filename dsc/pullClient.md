---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "A DSC lekérési ügyfél beállítása"
ms.openlocfilehash: 98a67b8d27eeb445bb70f75253ca31e12207d5bd
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 01/17/2018
---
# <a name="setting-up-a-dsc-pull-client"></a><span data-ttu-id="10e60-103">A DSC lekérési ügyfél beállítása</span><span class="sxs-lookup"><span data-stu-id="10e60-103">Setting up a DSC pull client</span></span>

> <span data-ttu-id="10e60-104">Vonatkozik: A Windows PowerShell 4.0-s verzióját, a Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="10e60-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="10e60-105">Minden cél fürtcsomópont lekéréses módban a rendszergazda és megadott URL-cím vagy a fájl helyét, akkor vegye fel a kapcsolatot a lekérési kiszolgálójával, hogy konfigurációk és erőforrások helyével, valamint azt kell jelentésadatok küldése.</span><span class="sxs-lookup"><span data-stu-id="10e60-105">Each target node has to be told to use pull mode and given the URL or file location where it can contact the pull server to get configurations and resources, and where it should send report data.</span></span>


<span data-ttu-id="10e60-106">Az alábbi témakörök ismertetik a lekéréses ügyfelek beállítása:</span><span class="sxs-lookup"><span data-stu-id="10e60-106">The following topics explain how to set up pull clients:</span></span>

* [<span data-ttu-id="10e60-107">Lekérési ügyfél beállítása konfigurációs nevekkel</span><span class="sxs-lookup"><span data-stu-id="10e60-107">Setting up a pull client using configuration names</span></span>](pullClientConfigNames.md)
* [<span data-ttu-id="10e60-108">Lekérési ügyfél beállítása konfigurációs azonosítóval</span><span class="sxs-lookup"><span data-stu-id="10e60-108">Setting up a pull client using configuration ID</span></span>](pullClientConfigID.md)

> <span data-ttu-id="10e60-109">**Megjegyzés:**: ezek a témakörök PowerShell 5.0 vonatkozik.</span><span class="sxs-lookup"><span data-stu-id="10e60-109">**Note**: These topics apply to PowerShell 5.0.</span></span> <span data-ttu-id="10e60-110">A PowerShell 4.0 lekéréses ügyfél beállításához tekintse meg a [ügyféltelepítéshez lekéréses konfigurációs azonosítójával PowerShell 4.0](pullClientConfigID4.md).</span><span class="sxs-lookup"><span data-stu-id="10e60-110">To set up a pull client in PowerShell 4.0, see [Setting up a pull client using configuration ID in PowerShell 4.0](pullClientConfigID4.md).</span></span>

