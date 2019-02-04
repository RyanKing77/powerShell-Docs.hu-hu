---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: WMF, powershell, beállítás
title: A WMF 5.1 PowerShell motor fejlesztései
ms.openlocfilehash: 738f72b910de7d44f48309013237d523d0dd40a4
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55687446"
---
# <a name="powershell-engine-improvements"></a><span data-ttu-id="cb982-103">PowerShell motor fejlesztései</span><span class="sxs-lookup"><span data-stu-id="cb982-103">PowerShell Engine Improvements</span></span>

<span data-ttu-id="cb982-104">A core PowerShell motor a következő fejlesztések történtek a WMF 5.1:</span><span class="sxs-lookup"><span data-stu-id="cb982-104">The following improvements to the core PowerShell engine have been implemented in WMF 5.1:</span></span>

## <a name="performance"></a><span data-ttu-id="cb982-105">Teljesítmény</span><span class="sxs-lookup"><span data-stu-id="cb982-105">Performance</span></span>

<span data-ttu-id="cb982-106">Teljesítmény javulását néhány fontos területeken:</span><span class="sxs-lookup"><span data-stu-id="cb982-106">Performance has improved in some important areas:</span></span>

- <span data-ttu-id="cb982-107">Indítás</span><span class="sxs-lookup"><span data-stu-id="cb982-107">Startup</span></span>
- <span data-ttu-id="cb982-108">Az adatcsatornás feldolgozás parancsmagokhoz hasonlóan `ForEach-Object` és `Where-Object` körülbelül 50 %-kal gyorsabb van</span><span class="sxs-lookup"><span data-stu-id="cb982-108">Pipelining to cmdlets like `ForEach-Object` and `Where-Object` is approximately 50% faster</span></span>

<span data-ttu-id="cb982-109">Néhány példa fejlesztései (a az eredményeket a hardverektől függően változhat):</span><span class="sxs-lookup"><span data-stu-id="cb982-109">Some example improvements (your results may vary depending on your hardware):</span></span>

| <span data-ttu-id="cb982-110">Forgatókönyv</span><span class="sxs-lookup"><span data-stu-id="cb982-110">Scenario</span></span> | <span data-ttu-id="cb982-111">5.0-s idő (ms)</span><span class="sxs-lookup"><span data-stu-id="cb982-111">5.0 Time (ms)</span></span> | <span data-ttu-id="cb982-112">5.1 idő (ms)</span><span class="sxs-lookup"><span data-stu-id="cb982-112">5.1 Time (ms)</span></span> |
| -------- | :---------------: | :---------------: |
| `powershell -command "echo 1"` | <span data-ttu-id="cb982-113">900</span><span class="sxs-lookup"><span data-stu-id="cb982-113">900</span></span> | <span data-ttu-id="cb982-114">250</span><span class="sxs-lookup"><span data-stu-id="cb982-114">250</span></span> |
| <span data-ttu-id="cb982-115">Először minden eddiginél PowerShell futtatása: `powershell -command "Unknown-Command"`</span><span class="sxs-lookup"><span data-stu-id="cb982-115">First ever PowerShell run: `powershell -command "Unknown-Command"`</span></span> | <span data-ttu-id="cb982-116">30000</span><span class="sxs-lookup"><span data-stu-id="cb982-116">30000</span></span> | <span data-ttu-id="cb982-117">13000</span><span class="sxs-lookup"><span data-stu-id="cb982-117">13000</span></span> |
| <span data-ttu-id="cb982-118">Parancs a beépített elemzési gyorsítótár: `powershell -command "Unknown-Command"`</span><span class="sxs-lookup"><span data-stu-id="cb982-118">Command analysis cache built: `powershell -command "Unknown-Command"`</span></span> | <span data-ttu-id="cb982-119">7000</span><span class="sxs-lookup"><span data-stu-id="cb982-119">7000</span></span> | <span data-ttu-id="cb982-120">520</span><span class="sxs-lookup"><span data-stu-id="cb982-120">520</span></span> |
| <code>1..1000000 &#124; % { }</code> | <span data-ttu-id="cb982-121">1400</span><span class="sxs-lookup"><span data-stu-id="cb982-121">1400</span></span> | <span data-ttu-id="cb982-122">750</span><span class="sxs-lookup"><span data-stu-id="cb982-122">750</span></span> |

> [!Note]
> <span data-ttu-id="cb982-123">Indítási kapcsolatos egy módosítása hatással lehet a bizonyos nem támogatott forgatókönyveket.</span><span class="sxs-lookup"><span data-stu-id="cb982-123">One change related to startup might impact some unsupported scenarios.</span></span>
> <span data-ttu-id="cb982-124">PowerShell már nem olvassa a fájlokat `$pshome\*.ps1xml` – ezek a fájlok lett konvertálva a C# elkerülése érdekében néhány fájlt, és a CPU-terhelés az XML feldolgozási fájlokat.</span><span class="sxs-lookup"><span data-stu-id="cb982-124">PowerShell no longer reads the files `$pshome\*.ps1xml` -- these files have been converted to C# to avoid some file and CPU overhead of processing the XML files.</span></span>
> <span data-ttu-id="cb982-125">A fájlok továbbra is léteznek támogatási V2 egymás mellett, így a fájl tartalmának módosítása esetén ez nem lesz bármilyen hatása V5 verzióra, csak V2.</span><span class="sxs-lookup"><span data-stu-id="cb982-125">The files still exist to support V2 side-by-side, so if you change the file contents, it will not have any effect to V5, only V2.</span></span>
> <span data-ttu-id="cb982-126">Vegye figyelembe, hogy ezek a fájlok tartalmának módosítása soha nem volt támogatott.</span><span class="sxs-lookup"><span data-stu-id="cb982-126">Note that changing the contents of these files was never a supported scenario.</span></span>

<span data-ttu-id="cb982-127">Egy másik látható változást, hogy hogyan gyorsítótárazza a PowerShell, az exportált parancsokat és más információkat rendszerre telepített modulok.</span><span class="sxs-lookup"><span data-stu-id="cb982-127">Another visible change is how PowerShell caches the exported commands and other information for modules that are installed on a system.</span></span>
<span data-ttu-id="cb982-128">Korábban, a gyorsítótár a könyvtár a tárolt `$env:LOCALAPPDATA\Microsoft\Windows\PowerShell\CommandAnalysis`.</span><span class="sxs-lookup"><span data-stu-id="cb982-128">Previously, this cache was stored in the directory `$env:LOCALAPPDATA\Microsoft\Windows\PowerShell\CommandAnalysis`.</span></span>
<span data-ttu-id="cb982-129">A WMF 5.1-es, a gyorsítótár nem egyetlen fájl `$env:LOCALAPPDATA\Microsoft\Windows\PowerShell\ModuleAnalysisCache`.</span><span class="sxs-lookup"><span data-stu-id="cb982-129">In WMF 5.1, the cache is a single file `$env:LOCALAPPDATA\Microsoft\Windows\PowerShell\ModuleAnalysisCache`.</span></span>
<span data-ttu-id="cb982-130">Lásd: [modul elemzési gyorsítótár](scenarios-features.md#module-analysis-cache) további részletekért.</span><span class="sxs-lookup"><span data-stu-id="cb982-130">See [Module Analysis Cache](scenarios-features.md#module-analysis-cache) for more details.</span></span>