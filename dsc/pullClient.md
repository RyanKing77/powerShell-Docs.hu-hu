---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "A DSC lekérési ügyfél beállítása"
ms.openlocfilehash: d2d1bab7ba2b482b2a66ce59b5f80ea32c242c47
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2017
---
# <a name="setting-up-a-dsc-pull-client"></a><span data-ttu-id="3b3a1-103">A DSC lekérési ügyfél beállítása</span><span class="sxs-lookup"><span data-stu-id="3b3a1-103">Setting up a DSC pull client</span></span>

> <span data-ttu-id="3b3a1-104">Vonatkozik: A Windows PowerShell 4.0-s verzióját, a Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="3b3a1-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="3b3a1-105">Minden cél fürtcsomópont lekéréses módban a rendszergazda és megadott URL-cím vagy a fájl helyét, akkor vegye fel a kapcsolatot a lekérési kiszolgálójával, hogy konfigurációk és erőforrások helyével, valamint azt kell jelentésadatok küldése.</span><span class="sxs-lookup"><span data-stu-id="3b3a1-105">Each target node has to be told to use pull mode and given the URL or file location where it can contact the pull server to get configurations and resources, and where it should send report data.</span></span>


<span data-ttu-id="3b3a1-106">Az alábbi témakörök ismertetik a lekéréses ügyfelek beállítása:</span><span class="sxs-lookup"><span data-stu-id="3b3a1-106">The following topics explain how to set up pull clients:</span></span>

* [<span data-ttu-id="3b3a1-107">Konfigurációs nevek használatával lekéréses ügyfél beállítása</span><span class="sxs-lookup"><span data-stu-id="3b3a1-107">Setting up a pull client using configuration names</span></span>](pullClientConfigNames.md)
* [<span data-ttu-id="3b3a1-108">Konfigurációs azonosítójával lekéréses ügyfél beállítása</span><span class="sxs-lookup"><span data-stu-id="3b3a1-108">Setting up a pull client using configuration ID</span></span>](pullClientConfigID.md)

> <span data-ttu-id="3b3a1-109">**Megjegyzés:**: ezek a témakörök PowerShell 5.0 vonatkozik.</span><span class="sxs-lookup"><span data-stu-id="3b3a1-109">**Note**: These topics apply to PowerShell 5.0.</span></span> <span data-ttu-id="3b3a1-110">A PowerShell 4.0 lekéréses ügyfél beállításához tekintse meg a [ügyféltelepítéshez lekéréses konfigurációs azonosítójával PowerShell 4.0](pullClientConfigID4.md).</span><span class="sxs-lookup"><span data-stu-id="3b3a1-110">To set up a pull client in PowerShell 4.0, see [Setting up a pull client using configuration ID in PowerShell 4.0](pullClientConfigID4.md).</span></span>

