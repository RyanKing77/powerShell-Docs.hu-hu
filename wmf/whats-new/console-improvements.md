---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
title: A WMF 5.1 konzoljának fejlesztései
ms.openlocfilehash: d0dd8e3c31dc0ddebab1bb899468b77a9292954d
ms.sourcegitcommit: 01b81317029b28dd9b61d167045fd31f1ec7bc06
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/17/2019
ms.locfileid: "65856216"
---
# <a name="console-improvements-in-wmf-51"></a>A WMF 5.1 konzoljának fejlesztései

## <a name="powershell-console-improvements"></a>PowerShell-konzol fejlesztései

A következő módosításokat végzett változtatások a WMF 5.1 PowerShell.exe a konzol élmény javítása érdekében:

### <a name="vt100-support"></a>VT100 támogatása

Windows 10-es támogatása [VT100 escape-karaktersorozatokat](/windows/console/console-virtual-terminal-sequences).
PowerShell bizonyos formázási escape-karaktersorozatokat VT100 figyelmen kívül tábla vastagságok kiszámítása során.

PowerShell is hozzá egy új API-t, amely segítségével a formázáshoz meghatározza, hogy VT100 támogatott. Például:

```powershell
if ($host.UI.SupportsVirtualTerminal)
{
    $esc = [char]0x1b
    "A yellow ${esc}[93mhello${esc}[0m"
}
else
{
    "A default hello"
}
```

Íme egy teljes [példa](https://gist.github.com/lzybkr/dcb973dccd54900b67783c48083c28f7) találatok kiemelése, amely használható a `Select-String`. A példában mentse egy nevű fájl `MatchInfo.format.ps1xml`, majd, a profilban vagy máshol kell futtatni `Update-FormatData -Prepend MatchInfo.format.ps1xml`.

Vegye figyelembe, hogy VT100 escape-karaktersorozatokat csak akkor támogatottak a Windows 10 Évfordulós frissítéssel történő indítása.
Ezek nem támogatottak a korábbi rendszerek.

### <a name="vi-mode-support-in-psreadline"></a>A PSReadline VI mód támogatása

[PSReadline](https://github.com/PowerShell/PSReadLine) vi módot támogat. Vi módot használja, futtassa `Set-PSReadlineOption -EditMode Vi`.

### <a name="redirected-stdin-with-interactive-input"></a>Interaktív bemenettel átirányított stdin

A korábbi verziókban a PowerShell indítása `powershell -File -` volt szükség, amikor stdin át lett irányítva, és adja meg a parancsok interaktív módon szeretne.

A WMF 5.1, ezen nehéz felderíteni, a beállítás már nem szükséges. PowerShell kapcsolók nélkül is elindítható.

Vegye figyelembe, hogy nem támogatja a PSReadline átirányítja stdin, és a beépített parancssori Profilszerkesztési élmény az átirányított stdin rendkívül korlátozott, például a nyíl billentyűk nem működnek. PSReadline egy jövőbeli verziójában meg a probléma megoldására.