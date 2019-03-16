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
# <a name="scriptanalyzer-rule-profile-for-gallery"></a>Katalógus ScriptAnalyzer szabály profil

A futtatott PowerShell-galériában közzétett csomagokat a minőség biztosítása érdekében [PSScriptAnalyzer](https://github.com/PowerShell/PSScriptAnalyzer) szabályok használatával határozza meg, hogy vannak-e a szkriptekben elküldött kapcsolatban felmerülő szabálysértéseket.

Annak a ScriptAnalyzer futtatjuk szabályok listáján [GitHub-oldalon](https://github.com/PowerShell/PSScriptAnalyzer/blob/development/Engine/Settings/PSGallery.psd1).
Ha bármely aggály szabályok futtatjuk, lépjen kapcsolatba a PowerShell-galéria rendszergazdák, vagy nyissa meg a problémát a ScriptAnalyzer.

ScriptAnalyzer eredményeket a minden egyes csomag lapon katalógus a következő kiadásban jelennek meg. Azt javasoljuk, hogy a csomag tulajdonosok csomagjaikat, hogy nincsenek közzétett csomag súlyos hibák ellenőrzéséhez.
