---
ms.date: 08/23/2018
keywords: PowerShell, a parancsmag
title: PowerShell-folyamatok ismertetése
ms.openlocfilehash: 3033a4fe1a704fbbfa76e6d38662c8b22c3dbd9b
ms.sourcegitcommit: a6f13c16a535acea279c0ddeca72f1f0d8a8ce4c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2019
ms.locfileid: "67030392"
---
# <a name="understanding-pipelines"></a><span data-ttu-id="09a91-103">A folyamatok ismertetése</span><span class="sxs-lookup"><span data-stu-id="09a91-103">Understanding pipelines</span></span>

<span data-ttu-id="09a91-104">A folyamatok cső csatlakoztatott szegmenseinek sorozata úgy működik.</span><span class="sxs-lookup"><span data-stu-id="09a91-104">Pipelines act like a series of connected segments of pipe.</span></span> <span data-ttu-id="09a91-105">Elemek áthelyezése során a folyamat minden egyes szegmens halad át.</span><span class="sxs-lookup"><span data-stu-id="09a91-105">Items moving along the pipeline pass through each segment.</span></span> <span data-ttu-id="09a91-106">Folyamat létrehozása a PowerShell, a függőleges vonal operátor együtt parancsok csatlakozás "|}".</span><span class="sxs-lookup"><span data-stu-id="09a91-106">To create a pipeline in PowerShell, you connect commands together with the pipe operator "|".</span></span> <span data-ttu-id="09a91-107">Minden parancs kimenete a következő parancs bemenetként szolgál.</span><span class="sxs-lookup"><span data-stu-id="09a91-107">The output of each command is used as input to the next command.</span></span>

<span data-ttu-id="09a91-108">A folyamatokhoz használt jelölés más parancskörnyezet használt jelölés hasonlít.</span><span class="sxs-lookup"><span data-stu-id="09a91-108">The notation used for pipelines is similar to the notation used in other shells.</span></span> <span data-ttu-id="09a91-109">Első ránézésre nem lehet nyilvánvaló hogyan folyamatok különböznek a PowerShellben.</span><span class="sxs-lookup"><span data-stu-id="09a91-109">At first glance, it may not be apparent how pipelines are different in PowerShell.</span></span> <span data-ttu-id="09a91-110">A képernyőn látható szöveg, bár a PowerShell csövek objektumokat, nem szöveg parancsok között.</span><span class="sxs-lookup"><span data-stu-id="09a91-110">Although you see text on the screen, PowerShell pipes objects, not text, between commands.</span></span>

## <a name="the-powershell-pipeline"></a><span data-ttu-id="09a91-111">A PowerShell-adatcsatorna</span><span class="sxs-lookup"><span data-stu-id="09a91-111">The PowerShell pipeline</span></span>

<span data-ttu-id="09a91-112">A folyamatok olyan tartják a legértékesebb fogalma a parancssori felületen használt.</span><span class="sxs-lookup"><span data-stu-id="09a91-112">Pipelines are arguably the most valuable concept used in command-line interfaces.</span></span> <span data-ttu-id="09a91-113">Ha megfelelően használja, a folyamatok egyszerűsíteni az összetett parancsokkal, és könnyebben tekintse meg a parancsok a munkafolyamat.</span><span class="sxs-lookup"><span data-stu-id="09a91-113">When used properly, pipelines reduce the effort of using complex commands and make it easier to see the flow of work for the commands.</span></span> <span data-ttu-id="09a91-114">Egy folyamat (nevezett folyamat prvek) lévő összes parancs a következő parancsot a folyamat továbbítja a kimenetét-elemenként.</span><span class="sxs-lookup"><span data-stu-id="09a91-114">Each command in a pipeline (called a pipeline element) passes its output to the next command in the pipeline, item-by-item.</span></span> <span data-ttu-id="09a91-115">Parancsok nem kell egyszerre egynél több elem kezelni.</span><span class="sxs-lookup"><span data-stu-id="09a91-115">Commands don't have to handle more than one item at a time.</span></span> <span data-ttu-id="09a91-116">Csökkentett erőforrás-használat és a kimenet első azonnali megkezdéséhez képességét jön létre.</span><span class="sxs-lookup"><span data-stu-id="09a91-116">The result is reduced resource consumption and the ability to begin getting the output immediately.</span></span>

<span data-ttu-id="09a91-117">Ha például a `Out-Host` parancsmag a lap-lapon megjeleníti a kimenetet egy másik parancsba, a kimeneti úgy tűnik, csak a normál, lapok felosztani, a képernyőn megjelenő szöveg, például:</span><span class="sxs-lookup"><span data-stu-id="09a91-117">For example, if you use the `Out-Host` cmdlet to force a page-by-page display of output from another command, the output looks just like the normal text displayed on the screen, broken up into pages:</span></span>

```powershell
Get-ChildItem -Path C:\WINDOWS\System32 | Out-Host -Paging
```

```Output
    Directory: C:\WINDOWS\system32

Mode                LastWriteTime         Length Name
----                -------------         ------ ----
d-----        4/12/2018   2:15 AM                0409
d-----        5/13/2018  11:31 PM                1033
d-----        4/11/2018   4:38 PM                AdvancedInstallers
d-----        5/13/2018  11:13 PM                af-ZA
d-----        5/13/2018  11:13 PM                am-et
d-----        4/11/2018   4:38 PM                AppLocker
d-----        5/13/2018  11:31 PM                appmgmt
d-----        7/11/2018   2:05 AM                appraiser
d---s-        4/12/2018   2:20 AM                AppV
d-----        5/13/2018  11:10 PM                ar-SA
d-----        5/13/2018  11:13 PM                as-IN
d-----        8/14/2018   9:03 PM                az-Latn-AZ
d-----        5/13/2018  11:13 PM                be-BY
d-----        5/13/2018  11:10 PM                BestPractices
d-----        5/13/2018  11:10 PM                bg-BG
d-----        5/13/2018  11:13 PM                bn-BD
d-----        5/13/2018  11:13 PM                bn-IN
d-----        8/14/2018   9:03 PM                Boot
d-----        8/14/2018   9:03 PM                bs-Latn-BA
d-----        4/11/2018   4:38 PM                Bthprops
d-----        4/12/2018   2:19 AM                ca-ES
d-----        8/14/2018   9:03 PM                ca-ES-valencia
d-----        5/13/2018  10:46 PM                CatRoot
d-----        8/23/2018   5:07 PM                catroot2
<SPACE> next page; <CR> next line; Q quit
...
```

<span data-ttu-id="09a91-118">CPU-kihasználtság lapozást is csökkenti, mert a feldolgozás továbbítja a `Out-Host` megjelenítésére készen álló teljes oldal, ha a parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="09a91-118">Paging also reduces CPU utilization because processing transfers to the `Out-Host` cmdlet when it has a complete page ready to display.</span></span> <span data-ttu-id="09a91-119">A parancsmagok, a folyamat az azt megelőző végrehajtási szüneteltetése, amíg a kimenet a következő lapra érhető el.</span><span class="sxs-lookup"><span data-stu-id="09a91-119">The cmdlets that precede it in the pipeline pause execution until the next page of output is available.</span></span>

<span data-ttu-id="09a91-120">Láthatja, hogy milyen hatással van a átirányítását a CPU és memória kihasználtsága a Windows Feladatkezelő, összehasonlítása az alábbi parancsokat:</span><span class="sxs-lookup"><span data-stu-id="09a91-120">You can see how piping impacts CPU and memory usage in the Windows Task Manager by comparing the following commands:</span></span>

- `Get-ChildItem C:\Windows -Recurse`
- `Get-ChildItem C:\Windows -Recurse | Out-Host -Paging`

> [!NOTE]
> <span data-ttu-id="09a91-121">A **lapozás** paraméter minden PowerShell-gazdagép nem támogatja.</span><span class="sxs-lookup"><span data-stu-id="09a91-121">The **Paging** parameter is not supported by all PowerShell hosts.</span></span> <span data-ttu-id="09a91-122">Például, amikor a próbálja használni a **lapozás** paramétert a PowerShell ISE-ben, az alábbi hibát látja:</span><span class="sxs-lookup"><span data-stu-id="09a91-122">For example, when you try to use the **Paging** parameter in the PowerShell ISE, you see the following error:</span></span>
>
> ```Output
> out-lineoutput : The method or operation is not implemented.
> At line:1 char:1
> + Get-ChildItem C:\Windows -Recurse | Out-Host -Paging
> + ~~~~~~~~~~~~~~~~~~~~~~~~~~~
>     + CategoryInfo          : NotSpecified: (:) [out-lineoutput], NotImplementedException
>     + FullyQualifiedErrorId : System.NotImplementedException,Microsoft.PowerShell.Commands.OutLineOutputCommand
> ```

## <a name="objects-in-the-pipeline"></a><span data-ttu-id="09a91-123">A folyamat objektumok</span><span class="sxs-lookup"><span data-stu-id="09a91-123">Objects in the pipeline</span></span>

<span data-ttu-id="09a91-124">A PowerShell-parancsmag futtatásakor a szöveges kimenet látja, mert a szükséges objektumokat képviseli a konzolablakban szövegként.</span><span class="sxs-lookup"><span data-stu-id="09a91-124">When you run a cmdlet in PowerShell, you see text output because it is necessary to represent objects as text in a console window.</span></span> <span data-ttu-id="09a91-125">A szöveges kimenet előfordulhat, hogy nem jeleníthető meg az összes, a kimeneti objektum tulajdonságait.</span><span class="sxs-lookup"><span data-stu-id="09a91-125">The text output may not display all of the properties of the object being output.</span></span>

<span data-ttu-id="09a91-126">Vegyük példaként a `Get-Location` parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="09a91-126">For example, consider the `Get-Location` cmdlet.</span></span> <span data-ttu-id="09a91-127">Ha `Get-Location` közben az aktuális tartózkodási helyét a C meghajtó gyökérkönyvtárában, a következő eredmény látható:</span><span class="sxs-lookup"><span data-stu-id="09a91-127">If you run `Get-Location` while your current location is the root of the C drive, you see the following output:</span></span>

```
PS> Get-Location

Path
----
C:\
```

<span data-ttu-id="09a91-128">A szöveges kimenet található egy összefoglaló az információ nem teljes reprezentációját által visszaadott objektum `Get-Location`.</span><span class="sxs-lookup"><span data-stu-id="09a91-128">The text output is a summary of information, not a complete representation of the object returned by `Get-Location`.</span></span> <span data-ttu-id="09a91-129">A címsor a kimenetben, a folyamat, amely formázza az adatokat a képernyőn megjelenítendő egészül ki.</span><span class="sxs-lookup"><span data-stu-id="09a91-129">The heading in the output is added by the process that formats the data for onscreen display.</span></span>

<span data-ttu-id="09a91-130">Amikor irányítsa a kimenetét a `Get-Member` parancsmag által visszaadott objektumra vonatkozó információ első `Get-Location`.</span><span class="sxs-lookup"><span data-stu-id="09a91-130">When you pipe the output to the `Get-Member` cmdlet you get information about the object returned by `Get-Location`.</span></span>

```powershell
Get-Location | Get-Member
```

```Output
   TypeName: System.Management.Automation.PathInfo

Name         MemberType Definition
----         ---------- ----------
Equals       Method     bool Equals(System.Object obj)
GetHashCode  Method     int GetHashCode()
GetType      Method     type GetType()
ToString     Method     string ToString()
Drive        Property   System.Management.Automation.PSDriveInfo Drive {get;}
Path         Property   string Path {get;}
Provider     Property   System.Management.Automation.ProviderInfo Provider {get;}
ProviderPath Property   string ProviderPath {get;}
```

<span data-ttu-id="09a91-131">`Get-Location` Visszaadja egy **PathInfo** objektum, amely tartalmazza az aktuális elérés úton és egyéb információkat.</span><span class="sxs-lookup"><span data-stu-id="09a91-131">`Get-Location` returns a **PathInfo** object that contains the current path and other information.</span></span>
