---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "WMF, a powershell, a beállítása"
title: "A WMF 5.1 konzoljának fejlesztései"
ms.openlocfilehash: b0859191ea310c9b73fe9f255d7f256a1cc1af1f
ms.sourcegitcommit: fee03bb9802222078c8d5f6c8efb0698024406ed
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/27/2017
---
# <a name="console-improvements-in-wmf-51"></a><span data-ttu-id="a2f5d-103">A WMF 5.1# konzoljának fejlesztései</span><span class="sxs-lookup"><span data-stu-id="a2f5d-103">Console Improvements in WMF 5.1#</span></span>

## <a name="powershell-console-improvements"></a><span data-ttu-id="a2f5d-104">PowerShell konzoljának fejlesztései</span><span class="sxs-lookup"><span data-stu-id="a2f5d-104">PowerShell console improvements</span></span>

<span data-ttu-id="a2f5d-105">A következő módosítások lettek bevezetve a WMF 5.1 PowerShell.exe konzol élményének növelése érdekében:</span><span class="sxs-lookup"><span data-stu-id="a2f5d-105">The following changes have been made to powershell.exe in WMF 5.1 to improve the console experience:</span></span>

###<a name="vt100-support"></a><span data-ttu-id="a2f5d-106">VT100 támogatása</span><span class="sxs-lookup"><span data-stu-id="a2f5d-106">VT100 support</span></span>

<span data-ttu-id="a2f5d-107">Windows 10 támogatása az [VT100 escape-karaktersorozatokat](https://msdn.microsoft.com/en-us/library/windows/desktop/mt638032(v=vs.85).aspx).</span><span class="sxs-lookup"><span data-stu-id="a2f5d-107">Windows 10 added support for [VT100 escape sequences](https://msdn.microsoft.com/en-us/library/windows/desktop/mt638032(v=vs.85).aspx).</span></span>
<span data-ttu-id="a2f5d-108">PowerShell figyelmen kívül hagyja majd bizonyos VT100 formázási escape-karaktersorozatokat tábla vastagságok számításakor.</span><span class="sxs-lookup"><span data-stu-id="a2f5d-108">PowerShell will ignore certain VT100 formatting escape sequences when calculating table widths.</span></span>

<span data-ttu-id="a2f5d-109">PowerShell szintén hozzáadott egy olyan új API, amely használható a formázáshoz kódot, hogy ha VT100 támogatja-e.</span><span class="sxs-lookup"><span data-stu-id="a2f5d-109">PowerShell also added a new API that can be used in formatting code to determine if VT100 is supported.</span></span> <span data-ttu-id="a2f5d-110">Például:</span><span class="sxs-lookup"><span data-stu-id="a2f5d-110">For example:</span></span>

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
<span data-ttu-id="a2f5d-111">Ez egy teljes [példa](https://gist.github.com/lzybkr/dcb973dccd54900b67783c48083c28f7) , amely megfelel a kiemeléséhez használható Select karakterláncból.</span><span class="sxs-lookup"><span data-stu-id="a2f5d-111">Here is a complete [example](https://gist.github.com/lzybkr/dcb973dccd54900b67783c48083c28f7) that can be used to highlight matches from Select-String.</span></span>
<span data-ttu-id="a2f5d-112">A példa nevű fájlba mentése `MatchInfo.format.ps1xml`, majd, a profil vagy máshol futtatni `Update-FormatData -Prepend MatchInfo.format.ps1xml`.</span><span class="sxs-lookup"><span data-stu-id="a2f5d-112">Save the example in a file named `MatchInfo.format.ps1xml`, then to use it, in your profile or elsewhere, run `Update-FormatData -Prepend MatchInfo.format.ps1xml`.</span></span>

<span data-ttu-id="a2f5d-113">Vegye figyelembe, hogy VT100 escape-karaktersorozatokat csak támogatott kezdődő, és a Windows 10 évforduló frissítés; Ezek nem támogatottak a korábbi rendszereken.</span><span class="sxs-lookup"><span data-stu-id="a2f5d-113">Note that VT100 escape sequences are only supported starting with the Windows 10 Anniversary update; they are not supported on earlier systems.</span></span>   

### <a name="vi-mode-support-in-psreadline"></a><span data-ttu-id="a2f5d-114">A PSReadline VI mód támogatása</span><span class="sxs-lookup"><span data-stu-id="a2f5d-114">Vi mode support in PSReadline</span></span>

<span data-ttu-id="a2f5d-115">[PSReadline](https://github.com/lzybkr/PSReadLine) vi módot támogat.</span><span class="sxs-lookup"><span data-stu-id="a2f5d-115">[PSReadline](https://github.com/lzybkr/PSReadLine) adds support for vi mode.</span></span> <span data-ttu-id="a2f5d-116">Vi módban kell futtatni `Set-PSReadlineOption -EditMode Vi`.</span><span class="sxs-lookup"><span data-stu-id="a2f5d-116">To use vi mode, run `Set-PSReadlineOption -EditMode Vi`.</span></span>

### <a name="redirected-stdin-with-interactive-input"></a><span data-ttu-id="a2f5d-117">Interaktív bevitellel átirányított stdin</span><span class="sxs-lookup"><span data-stu-id="a2f5d-117">Redirected stdin with interactive input</span></span> 

<span data-ttu-id="a2f5d-118">A korábbi verziókban a PowerShell indítása `powershell -File -` volt szükség, amikor stdin át lett irányítva, és adja meg interaktív módon parancsok szeretne.</span><span class="sxs-lookup"><span data-stu-id="a2f5d-118">In earlier versions, starting PowerShell with `powershell -File -` was required when stdin was redirected and you wanted to enter commands interactively.</span></span>

<span data-ttu-id="a2f5d-119">A WMF 5.1, ezen nehéz felderíteni a beállítás már nem szükséges.</span><span class="sxs-lookup"><span data-stu-id="a2f5d-119">With WMF 5.1, this hard to discover option is no longer necessary.</span></span> <span data-ttu-id="a2f5d-120">Megkezdheti PowerShell pl. kapcsolók nélkül `powershell`.</span><span class="sxs-lookup"><span data-stu-id="a2f5d-120">You can start PowerShell without any options, e.g. `powershell`.</span></span>

<span data-ttu-id="a2f5d-121">Vegye figyelembe, hogy PSReadline jelenleg nem támogatja a átirányítva stdin, és átirányított stdin a beépített parancssori szerkesztési élményt rendkívül korlátozott, például a nyílbillentyűk nem működnek.</span><span class="sxs-lookup"><span data-stu-id="a2f5d-121">Note that PSReadline does not currently support redirected stdin, and the built-in command-line editing experience with redirected stdin is extremely limited, for example, arrow keys don't work.</span></span> <span data-ttu-id="a2f5d-122">Egy későbbi kiadásban az PSReadline eleget kell tennie a probléma.</span><span class="sxs-lookup"><span data-stu-id="a2f5d-122">A future release of PSReadline should address this issue.</span></span>   

