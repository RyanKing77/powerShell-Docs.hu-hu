---
ms.date: 06/12/2017
contributor: JKeithB
ms.topic: conceptual
keywords: gyűjtemény, a powershell, a parancsmag, a psgallery
title: ScriptAnazlyer szabály profil galéria
ms.openlocfilehash: 74eab49e4c4a546655451ef21b30cfcafaeb9584
ms.sourcegitcommit: e9ad4d85fd7eb72fb5bc37f6ca3ae1282ae3c6d7
ms.contentlocale: hu-HU
ms.lasthandoff: 05/10/2018
---
# <a name="scriptanazlyer-rule-profile-for-gallery"></a><span data-ttu-id="1c832-103">ScriptAnazlyer szabály profil galéria</span><span class="sxs-lookup"><span data-stu-id="1c832-103">ScriptAnazlyer rule profile for Gallery</span></span>

<span data-ttu-id="1c832-104">PowerShell-galériában közzétett cikkek minőségének biztosítása érdekében Futtatás [PSScriptAnalyzer](https://github.com/PowerShell/PSScriptAnalyzer) szabályok használatával határozza meg, hogy van-e elküldve parancsfájlokban felmerülő szabálysértéseket.</span><span class="sxs-lookup"><span data-stu-id="1c832-104">To ensure the quality of items published to PowerShell Gallery, we run [PSScriptAnalyzer](https://github.com/PowerShell/PSScriptAnalyzer) rules to determine if there are any violations in the scripts submitted.</span></span>

<span data-ttu-id="1c832-105">ScriptAnalyzer futtatja azt szabályok listáján található [GitHub-oldalon](https://github.com/PowerShell/PSScriptAnalyzer/blob/development/Engine/Settings/PSGallery.psd1).</span><span class="sxs-lookup"><span data-stu-id="1c832-105">You can find the list of rules we are running on ScriptAnalyzer [GitHub page](https://github.com/PowerShell/PSScriptAnalyzer/blob/development/Engine/Settings/PSGallery.psd1).</span></span>
<span data-ttu-id="1c832-106">Ha bármilyen probléma merül fel kapcsolatos szabályok azt futnak, forduljon a PowerShell-Galériabeli rendszergazdák, vagy nyissa meg a problémát a ScriptAnalzyer.</span><span class="sxs-lookup"><span data-stu-id="1c832-106">If you have any concerns regarding the rules we are running, please contact PowerShell Gallery Administrators, or open an issue for ScriptAnalzyer.</span></span>

<span data-ttu-id="1c832-107">ScriptAnalyzer eredmények minden oldalon egyedi elem gyűjteményben a következő kiadásban jelennek meg.</span><span class="sxs-lookup"><span data-stu-id="1c832-107">ScriptAnalyzer results will be displayed on each individual item page in Gallery in the coming release.</span></span> <span data-ttu-id="1c832-108">Javasoljuk a cikk tulajdonosok ellenőrizze, hogy nincsenek a közzétett cikkek súlyos hibák az elemek kereséséhez.</span><span class="sxs-lookup"><span data-stu-id="1c832-108">We encourage item owners to check their items to make sure there are no severe errors in published items.</span></span>