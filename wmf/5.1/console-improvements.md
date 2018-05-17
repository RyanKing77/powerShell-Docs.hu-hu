---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
title: A WMF 5.1 konzoljának fejlesztései
ms.openlocfilehash: fb689002caf42203d760f11acc64e52cfa681069
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/16/2018
---
# <a name="console-improvements-in-wmf-51"></a>A WMF 5.1# konzoljának fejlesztései

## <a name="powershell-console-improvements"></a>PowerShell konzoljának fejlesztései

A következő módosítások lettek bevezetve a WMF 5.1 PowerShell.exe konzol élményének növelése érdekében:

###<a name="vt100-support"></a>VT100 támogatása

Windows 10 támogatása az [VT100 escape-karaktersorozatokat](https://msdn.microsoft.com/en-us/library/windows/desktop/mt638032(v=vs.85).aspx).
PowerShell figyelmen kívül hagyja majd bizonyos VT100 formázási escape-karaktersorozatokat tábla vastagságok számításakor.

PowerShell szintén hozzáadott egy olyan új API, amely használható a formázáshoz kódot, hogy ha VT100 támogatja-e.
Például:

```
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
Ez egy teljes [példa](https://gist.github.com/lzybkr/dcb973dccd54900b67783c48083c28f7) , amely megfelel a kiemeléséhez használható Select karakterláncból.
A példa nevű fájlba mentése `MatchInfo.format.ps1xml`, majd, a profil vagy máshol futtatni `Update-FormatData -Prepend MatchInfo.format.ps1xml`.

Vegye figyelembe, hogy VT100 escape-karaktersorozatokat csak támogatott kezdődő, és a Windows 10 évforduló frissítés; Ezek nem támogatottak a korábbi rendszereken.

### <a name="vi-mode-support-in-psreadline"></a>A PSReadline VI mód támogatása

[PSReadline](https://github.com/lzybkr/PSReadLine) vi módot támogat. Vi módban kell futtatni `Set-PSReadlineOption -EditMode Vi`.

### <a name="redirected-stdin-with-interactive-input"></a>Interaktív bevitellel átirányított stdin

A korábbi verziókban a PowerShell indítása `powershell -File -` volt szükség, amikor stdin át lett irányítva, és adja meg interaktív módon parancsok szeretne.

A WMF 5.1, ezen nehéz felderíteni a beállítás már nem szükséges.
Megkezdheti PowerShell pl. kapcsolók nélkül `powershell`.

Vegye figyelembe, hogy PSReadline jelenleg nem támogatja a átirányítva stdin, és átirányított stdin a beépített parancssori szerkesztési élményt rendkívül korlátozott, például a nyílbillentyűk nem működnek.
Egy későbbi kiadásban az PSReadline eleget kell tennie a probléma.
