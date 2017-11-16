---
ms.date: 2017-06-12
contributor: JKeithB
ms.topic: conceptual
keywords: "gyűjtemény, a powershell, a parancsmag, a psgallery"
title: psgallery_scriptanalyzer_rule_profile
ms.openlocfilehash: b178f198c9643fb39a6499d7e957cfd0d848c52d
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2017
---
# <a name="scriptanazlyer-rule-profile-for-gallery"></a><span data-ttu-id="c194f-103">A gyűjtemény ScriptAnazlyer szabály profil</span><span class="sxs-lookup"><span data-stu-id="c194f-103">ScriptAnazlyer Rule Profile for Gallery</span></span>
<span data-ttu-id="c194f-104">PowerShell-galériában közzétett cikkek minőségének biztosítása érdekében Futtatás [PSScriptAnalyzer](https://github.com/PowerShell/PSScriptAnalyzer) szabályok használatával határozza meg, hogy van-e elküldve parancsfájlokban felmerülő szabálysértéseket.</span><span class="sxs-lookup"><span data-stu-id="c194f-104">To ensure the quality of items published to PowerShell Gallery, we run [PSScriptAnalyzer](https://github.com/PowerShell/PSScriptAnalyzer) rules to determine if there are any violations in the scripts submitted.</span></span>

<span data-ttu-id="c194f-105">ScriptAnalyzer futtatja azt szabályok listáján található [GitHub-oldalon](https://github.com/PowerShell/PSScriptAnalyzer/blob/development/Engine/Settings/PSGallery.psd1).</span><span class="sxs-lookup"><span data-stu-id="c194f-105">You can find the list of rules we are running on ScriptAnalyzer [GitHub page](https://github.com/PowerShell/PSScriptAnalyzer/blob/development/Engine/Settings/PSGallery.psd1).</span></span>
<span data-ttu-id="c194f-106">Ha bármilyen probléma merül fel kapcsolatos szabályok azt futnak, forduljon a PowerShell-Galériabeli rendszergazdák, vagy nyissa meg a problémát a ScriptAnalzyer.</span><span class="sxs-lookup"><span data-stu-id="c194f-106">If you have any concerns regarding the rules we are running, please contact PowerShell Gallery Administrators, or open an issue for ScriptAnalzyer.</span></span>

<span data-ttu-id="c194f-107">ScriptAnalyzer eredmények minden oldalon egyedi elem gyűjteményben a következő kiadásban jelennek meg.</span><span class="sxs-lookup"><span data-stu-id="c194f-107">ScriptAnalyzer results will be displayed on each individual item page in Gallery in the coming release.</span></span> <span data-ttu-id="c194f-108">Javasoljuk a cikk tulajdonosok ellenőrizze, hogy nincsenek a közzétett cikkek súlyos hibák az elemek kereséséhez.</span><span class="sxs-lookup"><span data-stu-id="c194f-108">We encourage item owners to check their items to make sure there are no severe errors in published items.</span></span>

