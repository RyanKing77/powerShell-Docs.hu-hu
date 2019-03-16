---
ms.date: 06/12/2017
contributor: JKeithB
keywords: katalógus, a powershell, a parancsmag, a psgallery
title: Katalógus ScriptAnalyzer szabály profil
ms.openlocfilehash: 939f01dece56b283dbe6e03c888f42ff866707af
ms.sourcegitcommit: caac7d098a448232304c9d6728e7340ec7517a71
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/16/2019
ms.locfileid: "58059592"
---
# <a name="scriptanalyzer-rule-profile-for-gallery"></a><span data-ttu-id="dcfcc-103">Katalógus ScriptAnalyzer szabály profil</span><span class="sxs-lookup"><span data-stu-id="dcfcc-103">ScriptAnalyzer rule profile for Gallery</span></span>

<span data-ttu-id="dcfcc-104">A futtatott PowerShell-galériában közzétett csomagokat a minőség biztosítása érdekében [PSScriptAnalyzer](https://github.com/PowerShell/PSScriptAnalyzer) szabályok használatával határozza meg, hogy vannak-e a szkriptekben elküldött kapcsolatban felmerülő szabálysértéseket.</span><span class="sxs-lookup"><span data-stu-id="dcfcc-104">To ensure the quality of packages published to PowerShell Gallery, we run [PSScriptAnalyzer](https://github.com/PowerShell/PSScriptAnalyzer) rules to determine if there are any violations in the scripts submitted.</span></span>

<span data-ttu-id="dcfcc-105">Annak a ScriptAnalyzer futtatjuk szabályok listáján [GitHub-oldalon](https://github.com/PowerShell/PSScriptAnalyzer/blob/development/Engine/Settings/PSGallery.psd1).</span><span class="sxs-lookup"><span data-stu-id="dcfcc-105">You can find the list of rules we are running on ScriptAnalyzer [GitHub page](https://github.com/PowerShell/PSScriptAnalyzer/blob/development/Engine/Settings/PSGallery.psd1).</span></span>
<span data-ttu-id="dcfcc-106">Ha bármely aggály szabályok futtatjuk, lépjen kapcsolatba a PowerShell-galéria rendszergazdák, vagy nyissa meg a problémát a ScriptAnalyzer.</span><span class="sxs-lookup"><span data-stu-id="dcfcc-106">If you have any concerns regarding the rules we are running, please contact PowerShell Gallery Administrators, or open an issue for ScriptAnalyzer.</span></span>

<span data-ttu-id="dcfcc-107">ScriptAnalyzer eredményeket a minden egyes csomag lapon katalógus a következő kiadásban jelennek meg.</span><span class="sxs-lookup"><span data-stu-id="dcfcc-107">ScriptAnalyzer results will be displayed on each individual package page in Gallery in the coming release.</span></span> <span data-ttu-id="dcfcc-108">Azt javasoljuk, hogy a csomag tulajdonosok csomagjaikat, hogy nincsenek közzétett csomag súlyos hibák ellenőrzéséhez.</span><span class="sxs-lookup"><span data-stu-id="dcfcc-108">We encourage package owners to check their packages to make sure there are no severe errors in published packages.</span></span>
