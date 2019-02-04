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
# <a name="scriptanalyzer-rule-profile-for-gallery"></a>Katalógus ScriptAnalyzer szabály profil

A futtatott PowerShell-galériában közzétett csomagokat a minőség biztosítása érdekében [PSScriptAnalyzer](https://github.com/PowerShell/PSScriptAnalyzer) szabályok használatával határozza meg, hogy vannak-e a szkriptekben elküldött kapcsolatban felmerülő szabálysértéseket.

Annak a ScriptAnalyzer futtatjuk szabályok listáján [GitHub-oldalon](https://github.com/PowerShell/PSScriptAnalyzer/blob/development/Engine/Settings/PSGallery.psd1).
Ha bármely aggály szabályok futtatjuk, lépjen kapcsolatba a PowerShell-galéria rendszergazdák, vagy nyissa meg a problémát a ScriptAnalzyer.

ScriptAnalyzer eredményeket a minden egyes csomag lapon katalógus a következő kiadásban jelennek meg. Azt javasoljuk, hogy a csomag tulajdonosok csomagjaikat, hogy nincsenek közzétett csomag súlyos hibák ellenőrzéséhez.
