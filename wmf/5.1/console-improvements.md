---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
title: A WMF 5.1 konzoljának fejlesztései
ms.openlocfilehash: a8e82e2f973916c2ed5007eba90ee6f2b7a9a769
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62085137"
---
# <a name="console-improvements-in-wmf-51"></a><span data-ttu-id="f8e94-103">A WMF 5.1 konzoljának fejlesztései</span><span class="sxs-lookup"><span data-stu-id="f8e94-103">Console Improvements in WMF 5.1</span></span>

## <a name="powershell-console-improvements"></a><span data-ttu-id="f8e94-104">PowerShell-konzol fejlesztései</span><span class="sxs-lookup"><span data-stu-id="f8e94-104">PowerShell console improvements</span></span>

<span data-ttu-id="f8e94-105">A következő módosításokat végzett változtatások a WMF 5.1 PowerShell.exe a konzol élmény javítása érdekében:</span><span class="sxs-lookup"><span data-stu-id="f8e94-105">The following changes have been made to powershell.exe in WMF 5.1 to improve the console experience:</span></span>

### <a name="vt100-support"></a><span data-ttu-id="f8e94-106">VT100 támogatása</span><span class="sxs-lookup"><span data-stu-id="f8e94-106">VT100 support</span></span>

<span data-ttu-id="f8e94-107">Windows 10-es támogatása [VT100 escape-karaktersorozatokat](/windows/console/console-virtual-terminal-sequences).</span><span class="sxs-lookup"><span data-stu-id="f8e94-107">Windows 10 added support for [VT100 escape sequences](/windows/console/console-virtual-terminal-sequences).</span></span>
<span data-ttu-id="f8e94-108">PowerShell bizonyos formázási escape-karaktersorozatokat VT100 figyelmen kívül tábla vastagságok kiszámítása során.</span><span class="sxs-lookup"><span data-stu-id="f8e94-108">PowerShell will ignore certain VT100 formatting escape sequences when calculating table widths.</span></span>

<span data-ttu-id="f8e94-109">PowerShell is hozzá egy új API-t, amely segítségével a formázáshoz meghatározza, hogy VT100 támogatott.</span><span class="sxs-lookup"><span data-stu-id="f8e94-109">PowerShell also added a new API that can be used in formatting code to determine if VT100 is supported.</span></span>
<span data-ttu-id="f8e94-110">Például:</span><span class="sxs-lookup"><span data-stu-id="f8e94-110">For example:</span></span>

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

<span data-ttu-id="f8e94-111">Íme egy teljes [példa](https://gist.github.com/lzybkr/dcb973dccd54900b67783c48083c28f7) találatok kiemelése, amely használható a `Select-String`.</span><span class="sxs-lookup"><span data-stu-id="f8e94-111">Here is a complete [example](https://gist.github.com/lzybkr/dcb973dccd54900b67783c48083c28f7) that can be used to highlight matches from `Select-String`.</span></span>
<span data-ttu-id="f8e94-112">A példában mentse egy nevű fájl `MatchInfo.format.ps1xml`, majd, a profilban vagy máshol kell futtatni `Update-FormatData -Prepend MatchInfo.format.ps1xml`.</span><span class="sxs-lookup"><span data-stu-id="f8e94-112">Save the example in a file named `MatchInfo.format.ps1xml`, then to use it, in your profile or elsewhere, run `Update-FormatData -Prepend MatchInfo.format.ps1xml`.</span></span>

<span data-ttu-id="f8e94-113">Vegye figyelembe, hogy VT100 escape-karaktersorozatokat csak a Windows 10 Évfordulós frissítés; kezdve támogatott Ezek nem támogatottak a korábbi rendszerek.</span><span class="sxs-lookup"><span data-stu-id="f8e94-113">Note that VT100 escape sequences are only supported starting with the Windows 10 Anniversary update; they are not supported on earlier systems.</span></span>

### <a name="vi-mode-support-in-psreadline"></a><span data-ttu-id="f8e94-114">A PSReadline VI mód támogatása</span><span class="sxs-lookup"><span data-stu-id="f8e94-114">Vi mode support in PSReadline</span></span>

<span data-ttu-id="f8e94-115">[PSReadline](https://github.com/lzybkr/PSReadLine) vi módot támogat.</span><span class="sxs-lookup"><span data-stu-id="f8e94-115">[PSReadline](https://github.com/lzybkr/PSReadLine) adds support for vi mode.</span></span> <span data-ttu-id="f8e94-116">Vi módot használja, futtassa `Set-PSReadlineOption -EditMode Vi`.</span><span class="sxs-lookup"><span data-stu-id="f8e94-116">To use vi mode, run `Set-PSReadlineOption -EditMode Vi`.</span></span>

### <a name="redirected-stdin-with-interactive-input"></a><span data-ttu-id="f8e94-117">Interaktív bemenettel átirányított stdin</span><span class="sxs-lookup"><span data-stu-id="f8e94-117">Redirected stdin with interactive input</span></span>

<span data-ttu-id="f8e94-118">A korábbi verziókban a PowerShell indítása `powershell -File -` volt szükség, amikor stdin át lett irányítva, és adja meg a parancsok interaktív módon szeretne.</span><span class="sxs-lookup"><span data-stu-id="f8e94-118">In earlier versions, starting PowerShell with `powershell -File -` was required when stdin was redirected and you wanted to enter commands interactively.</span></span>

<span data-ttu-id="f8e94-119">A WMF 5.1, ezen nehéz felderíteni, a beállítás már nem szükséges.</span><span class="sxs-lookup"><span data-stu-id="f8e94-119">With WMF 5.1, this hard to discover option is no longer necessary.</span></span>
<span data-ttu-id="f8e94-120">Elkezdheti PowerShell például kapcsolók nélkül `powershell`.</span><span class="sxs-lookup"><span data-stu-id="f8e94-120">You can start PowerShell without any options, e.g. `powershell`.</span></span>

<span data-ttu-id="f8e94-121">Vegye figyelembe, hogy PSReadline jelenleg nem támogatja az átirányított stdin, és a beépített parancssori Profilszerkesztési élmény az átirányított stdin rendkívül korlátozott, például a nyíl billentyűk nem működnek.</span><span class="sxs-lookup"><span data-stu-id="f8e94-121">Note that PSReadline does not currently support redirected stdin, and the built-in command-line editing experience with redirected stdin is extremely limited, for example, arrow keys don't work.</span></span>
<span data-ttu-id="f8e94-122">PSReadline egy jövőbeli verziójában meg a probléma megoldására.</span><span class="sxs-lookup"><span data-stu-id="f8e94-122">A future release of PSReadline should address this issue.</span></span>