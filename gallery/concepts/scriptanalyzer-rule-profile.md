---
ms.date: 06/12/2017
contributor: JKeithB
keywords: katalógus, a powershell, a parancsmag, a psgallery
title: Katalógus ScriptAnalyzer szabály profil
ms.openlocfilehash: d91a88981cc2f3269a1f8b6ee864f8333a2f097c
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55683855"
---
# <a name="scriptanalyzer-rule-profile-for-gallery"></a><span data-ttu-id="68c75-103">Katalógus ScriptAnalyzer szabály profil</span><span class="sxs-lookup"><span data-stu-id="68c75-103">ScriptAnalyzer rule profile for Gallery</span></span>

<span data-ttu-id="68c75-104">A futtatott PowerShell-galériában közzétett csomagokat a minőség biztosítása érdekében [PSScriptAnalyzer](https://github.com/PowerShell/PSScriptAnalyzer) szabályok használatával határozza meg, hogy vannak-e a szkriptekben elküldött kapcsolatban felmerülő szabálysértéseket.</span><span class="sxs-lookup"><span data-stu-id="68c75-104">To ensure the quality of packages published to PowerShell Gallery, we run [PSScriptAnalyzer](https://github.com/PowerShell/PSScriptAnalyzer) rules to determine if there are any violations in the scripts submitted.</span></span>

<span data-ttu-id="68c75-105">Annak a ScriptAnalyzer futtatjuk szabályok listáján [GitHub-oldalon](https://github.com/PowerShell/PSScriptAnalyzer/blob/development/Engine/Settings/PSGallery.psd1).</span><span class="sxs-lookup"><span data-stu-id="68c75-105">You can find the list of rules we are running on ScriptAnalyzer [GitHub page](https://github.com/PowerShell/PSScriptAnalyzer/blob/development/Engine/Settings/PSGallery.psd1).</span></span>
<span data-ttu-id="68c75-106">Ha bármely aggály szabályok futtatjuk, lépjen kapcsolatba a PowerShell-galéria rendszergazdák, vagy nyissa meg a problémát a ScriptAnalzyer.</span><span class="sxs-lookup"><span data-stu-id="68c75-106">If you have any concerns regarding the rules we are running, please contact PowerShell Gallery Administrators, or open an issue for ScriptAnalzyer.</span></span>

<span data-ttu-id="68c75-107">ScriptAnalyzer eredményeket a minden egyes csomag lapon katalógus a következő kiadásban jelennek meg.</span><span class="sxs-lookup"><span data-stu-id="68c75-107">ScriptAnalyzer results will be displayed on each individual package page in Gallery in the coming release.</span></span> <span data-ttu-id="68c75-108">Azt javasoljuk, hogy a csomag tulajdonosok csomagjaikat, hogy nincsenek közzétett csomag súlyos hibák ellenőrzéséhez.</span><span class="sxs-lookup"><span data-stu-id="68c75-108">We encourage package owners to check their packages to make sure there are no severe errors in published packages.</span></span>
