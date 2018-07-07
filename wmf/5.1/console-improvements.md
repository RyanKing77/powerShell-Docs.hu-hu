---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
title: A WMF 5.1 konzoljának fejlesztései
ms.openlocfilehash: a8e82e2f973916c2ed5007eba90ee6f2b7a9a769
ms.sourcegitcommit: 8b076ebde7ef971d7465bab834a3c2a32471ef6f
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/06/2018
ms.locfileid: "37892926"
---
# <a name="console-improvements-in-wmf-51"></a>A WMF 5.1 konzoljának fejlesztései

## <a name="powershell-console-improvements"></a>PowerShell-konzol fejlesztései

A következő módosításokat végzett változtatások a WMF 5.1 PowerShell.exe a konzol élmény javítása érdekében:

### <a name="vt100-support"></a>VT100 támogatása

Windows 10-es támogatása [VT100 escape-karaktersorozatokat](/windows/console/console-virtual-terminal-sequences).
PowerShell bizonyos formázási escape-karaktersorozatokat VT100 figyelmen kívül tábla vastagságok kiszámítása során.

PowerShell is hozzá egy új API-t, amely segítségével a formázáshoz meghatározza, hogy VT100 támogatott.
Például:

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

Íme egy teljes [példa](https://gist.github.com/lzybkr/dcb973dccd54900b67783c48083c28f7) találatok kiemelése, amely használható a `Select-String`.
A példában mentse egy nevű fájl `MatchInfo.format.ps1xml`, majd, a profilban vagy máshol kell futtatni `Update-FormatData -Prepend MatchInfo.format.ps1xml`.

Vegye figyelembe, hogy VT100 escape-karaktersorozatokat csak a Windows 10 Évfordulós frissítés; kezdve támogatott Ezek nem támogatottak a korábbi rendszerek.

### <a name="vi-mode-support-in-psreadline"></a>A PSReadline VI mód támogatása

[PSReadline](https://github.com/lzybkr/PSReadLine) vi módot támogat. Vi módot használja, futtassa `Set-PSReadlineOption -EditMode Vi`.

### <a name="redirected-stdin-with-interactive-input"></a>Interaktív bemenettel átirányított stdin

A korábbi verziókban a PowerShell indítása `powershell -File -` volt szükség, amikor stdin át lett irányítva, és adja meg a parancsok interaktív módon szeretne.

A WMF 5.1, ezen nehéz felderíteni, a beállítás már nem szükséges.
Elkezdheti PowerShell például kapcsolók nélkül `powershell`.

Vegye figyelembe, hogy PSReadline jelenleg nem támogatja az átirányított stdin, és a beépített parancssori Profilszerkesztési élmény az átirányított stdin rendkívül korlátozott, például a nyíl billentyűk nem működnek.
PSReadline egy jövőbeli verziójában meg a probléma megoldására.