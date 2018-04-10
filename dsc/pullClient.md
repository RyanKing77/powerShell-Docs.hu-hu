---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: A DSC lekérési ügyfél beállítása
ms.openlocfilehash: e6d73187566db2756ae24dabe0a825fffb5ecce0
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="setting-up-a-dsc-pull-client"></a><span data-ttu-id="0857c-103">A DSC lekérési ügyfél beállítása</span><span class="sxs-lookup"><span data-stu-id="0857c-103">Setting up a DSC pull client</span></span>

> <span data-ttu-id="0857c-104">Vonatkozik: A Windows PowerShell 4.0-s verzióját, a Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="0857c-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="0857c-105">Minden cél fürtcsomópont lekéréses módban a rendszergazda és megadott URL-cím vagy a fájl helyét, akkor vegye fel a kapcsolatot a lekérési kiszolgálójával, hogy konfigurációk és erőforrások helyével, valamint azt kell jelentésadatok küldése.</span><span class="sxs-lookup"><span data-stu-id="0857c-105">Each target node has to be told to use pull mode and given the URL or file location where it can contact the pull server to get configurations and resources, and where it should send report data.</span></span>


<span data-ttu-id="0857c-106">Az alábbi témakörök ismertetik a lekéréses ügyfelek beállítása:</span><span class="sxs-lookup"><span data-stu-id="0857c-106">The following topics explain how to set up pull clients:</span></span>

* [<span data-ttu-id="0857c-107">Lekérési ügyfél beállítása konfigurációs nevekkel</span><span class="sxs-lookup"><span data-stu-id="0857c-107">Setting up a pull client using configuration names</span></span>](pullClientConfigNames.md)
* [<span data-ttu-id="0857c-108">Lekérési ügyfél beállítása konfigurációs azonosítóval</span><span class="sxs-lookup"><span data-stu-id="0857c-108">Setting up a pull client using configuration ID</span></span>](pullClientConfigID.md)

> <span data-ttu-id="0857c-109">**Megjegyzés:**: ezek a témakörök PowerShell 5.0 vonatkozik.</span><span class="sxs-lookup"><span data-stu-id="0857c-109">**Note**: These topics apply to PowerShell 5.0.</span></span> <span data-ttu-id="0857c-110">A PowerShell 4.0 lekéréses ügyfél beállításához tekintse meg a [ügyféltelepítéshez lekéréses konfigurációs azonosítójával PowerShell 4.0](pullClientConfigID4.md).</span><span class="sxs-lookup"><span data-stu-id="0857c-110">To set up a pull client in PowerShell 4.0, see [Setting up a pull client using configuration ID in PowerShell 4.0](pullClientConfigID4.md).</span></span>