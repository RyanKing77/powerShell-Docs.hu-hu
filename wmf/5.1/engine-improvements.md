---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "WMF, a powershell, a beállítása"
title: "A WMF 5.1 PowerShell motor fejlesztései"
ms.openlocfilehash: 6c8000ccfc59ab46de95dc4f67161e12a5a41199
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2017
---
#<a name="powershell-engine-improvements"></a><span data-ttu-id="6193e-103">PowerShell-motor fejlesztései</span><span class="sxs-lookup"><span data-stu-id="6193e-103">PowerShell Engine Improvements</span></span>

<span data-ttu-id="6193e-104">A core PowerShell motor az alábbi fejlesztések történtek WMF 5.1:</span><span class="sxs-lookup"><span data-stu-id="6193e-104">The following improvements to the core PowerShell engine have been implemented in WMF 5.1:</span></span>


## <a name="performance"></a><span data-ttu-id="6193e-105">Teljesítmény</span><span class="sxs-lookup"><span data-stu-id="6193e-105">Performance</span></span> ##

<span data-ttu-id="6193e-106">Jobb teljesítmény, néhány fontos területeken:</span><span class="sxs-lookup"><span data-stu-id="6193e-106">Performance has improved in some important areas:</span></span>

- <span data-ttu-id="6193e-107">Indítás</span><span class="sxs-lookup"><span data-stu-id="6193e-107">Startup</span></span>
- <span data-ttu-id="6193e-108">Például a ForEach-Object és a Where-Object-parancsmagjainak futószalagos körülbelül 50 %-kal gyorsabb</span><span class="sxs-lookup"><span data-stu-id="6193e-108">Pipelining to cmdlets like ForEach-Object and Where-Object is approximately 50% faster</span></span> 

<span data-ttu-id="6193e-109">Néhány példa fejlesztései (az eltérő attól függően, hogy a hardver):</span><span class="sxs-lookup"><span data-stu-id="6193e-109">Some example improvements (your results may vary depending on your hardware):</span></span> 

| <span data-ttu-id="6193e-110">Forgatókönyv</span><span class="sxs-lookup"><span data-stu-id="6193e-110">Scenario</span></span> | <span data-ttu-id="6193e-111">5.0 idő (ms)</span><span class="sxs-lookup"><span data-stu-id="6193e-111">5.0 Time (ms)</span></span> | <span data-ttu-id="6193e-112">5.1 idő (ms)</span><span class="sxs-lookup"><span data-stu-id="6193e-112">5.1 Time (ms)</span></span> |
| -------- | :---------------: | :---------------: |
| `powershell -command "echo 1"` | <span data-ttu-id="6193e-113">900</span><span class="sxs-lookup"><span data-stu-id="6193e-113">900</span></span> | <span data-ttu-id="6193e-114">250</span><span class="sxs-lookup"><span data-stu-id="6193e-114">250</span></span> |
| <span data-ttu-id="6193e-115">Első legalább egyszer PowerShell futtatása:`powershell -command "Unknown-Command"`</span><span class="sxs-lookup"><span data-stu-id="6193e-115">First ever PowerShell run: `powershell -command "Unknown-Command"`</span></span> | <span data-ttu-id="6193e-116">30000</span><span class="sxs-lookup"><span data-stu-id="6193e-116">30000</span></span> | <span data-ttu-id="6193e-117">13000</span><span class="sxs-lookup"><span data-stu-id="6193e-117">13000</span></span> |
| <span data-ttu-id="6193e-118">A parancs elemzési gyorsítótár beépített:`powershell -command "Unknown-Command"`</span><span class="sxs-lookup"><span data-stu-id="6193e-118">Command analysis cache built: `powershell -command "Unknown-Command"`</span></span> | <span data-ttu-id="6193e-119">7000</span><span class="sxs-lookup"><span data-stu-id="6193e-119">7000</span></span> | <span data-ttu-id="6193e-120">520</span><span class="sxs-lookup"><span data-stu-id="6193e-120">520</span></span> |
| <code>1..1000000 &#124; % { }</code> | <span data-ttu-id="6193e-121">1400</span><span class="sxs-lookup"><span data-stu-id="6193e-121">1400</span></span> | <span data-ttu-id="6193e-122">750</span><span class="sxs-lookup"><span data-stu-id="6193e-122">750</span></span> |
  
> <span data-ttu-id="6193e-123">Megjegyzés: indítási kapcsolódik egy módosítása hatással lehet egyes forgatókönyvek nem támogatott.</span><span class="sxs-lookup"><span data-stu-id="6193e-123">Note One change related to startup might impact some unsupported scenarios.</span></span> 
> <span data-ttu-id="6193e-124">PowerShell már nem olvassa a fájlokat `$pshome\*.ps1xml` – ezek a fájlok konvertált C# elkerülése érdekében néhány fájlt, és a CPU-terhelés az XML feldolgozási fájlokat.</span><span class="sxs-lookup"><span data-stu-id="6193e-124">PowerShell no longer reads the files `$pshome\*.ps1xml` -- these files have been converted to C# to avoid some file and CPU overhead of processing the XML files.</span></span> 
<span data-ttu-id="6193e-125">A fájlok még mindig léteznek támogatásához V2-mellé, ha módosítja a fájl tartalmát, azt fogja nincs hatása V5, csak V2.</span><span class="sxs-lookup"><span data-stu-id="6193e-125">The files still exist to support V2 side-by-side, so if you change the file contents, it will not have any effect to V5, only V2.</span></span> 
<span data-ttu-id="6193e-126">Vegye figyelembe, hogy ezek a fájlok tartalmának módosítása nem támogatott.</span><span class="sxs-lookup"><span data-stu-id="6193e-126">Note that changing the contents of these files was never a supported scenario.</span></span>

<span data-ttu-id="6193e-127">Egy másik látható változást, hogy milyen módon gyorsítótárazza a PowerShell az exportált parancsokat és egyéb adatait, amely a rendszerre telepített modulok.</span><span class="sxs-lookup"><span data-stu-id="6193e-127">Another visible change is how PowerShell caches the exported commands and other information for modules that are installed on a system.</span></span> <span data-ttu-id="6193e-128">Korábban, a gyorsítótárban tárolta a címtárban `$env:LOCALAPPDATA\Microsoft\Windows\PowerShell\CommandAnalysis`.</span><span class="sxs-lookup"><span data-stu-id="6193e-128">Previously, this cache was stored in the directory `$env:LOCALAPPDATA\Microsoft\Windows\PowerShell\CommandAnalysis`.</span></span> <span data-ttu-id="6193e-129">WMF 5.1, a gyorsítótár egy olyan egyetlen fájl `$env:LOCALAPPDATA\Microsoft\Windows\PowerShell\ModuleAnalysisCache`.</span><span class="sxs-lookup"><span data-stu-id="6193e-129">In WMF 5.1, the cache is a single file `$env:LOCALAPPDATA\Microsoft\Windows\PowerShell\ModuleAnalysisCache`.</span></span>
<span data-ttu-id="6193e-130">Lásd: [modul elemzés gyorsítótár](scenarios-features.md#module-analysis-cache) további részleteket.</span><span class="sxs-lookup"><span data-stu-id="6193e-130">See [Module Analysis Cache](scenarios-features.md#module-analysis-cache) for more details.</span></span>

