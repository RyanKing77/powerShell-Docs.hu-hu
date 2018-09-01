---
ms.date: 08/27/2018
keywords: PowerShell, a parancsmag
title: A parancsokkal kapcsolatos információk lekérése
ms.assetid: 56f8e5b4-d97c-4e59-abbe-bf13e464eb0d
ms.openlocfilehash: 7af83e3a0e776d96e580b442430357b4ea063a72
ms.sourcegitcommit: c170a1608d20d3c925d79c35fa208f650d014146
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/31/2018
ms.locfileid: "43353170"
---
# <a name="getting-information-about-commands"></a><span data-ttu-id="d46c8-103">A parancsokkal kapcsolatos információk lekérése</span><span class="sxs-lookup"><span data-stu-id="d46c8-103">Getting information about commands</span></span>

<span data-ttu-id="d46c8-104">A PowerShell `Get-Command` jeleníti meg a parancsok, amelyek használhatók az aktuális munkamenetben.</span><span class="sxs-lookup"><span data-stu-id="d46c8-104">The PowerShell `Get-Command` displays commands that are available in your current session.</span></span>
<span data-ttu-id="d46c8-105">Ha futtatja a `Get-Command` parancsmagot, tekintse meg a következő kimenethez hasonló:</span><span class="sxs-lookup"><span data-stu-id="d46c8-105">When you run the `Get-Command` cmdlet, you see something similar to the following output:</span></span>

```output
CommandType     Name                    Version    Source
-----------     ----                    -------    ------
Cmdlet          Add-Computer            3.1.0.0    Microsoft.PowerShell.Management
Cmdlet          Add-Content             3.1.0.0    Microsoft.PowerShell.Management
Cmdlet          Add-History             3.0.0.0    Microsoft.PowerShell.Core
Cmdlet          Add-JobTrigger          1.1.0.0    PSScheduledJob
Cmdlet          Add-LocalGroupMember    1.0.0.0    Microsoft.PowerShell.LocalAccounts
Cmdlet          Add-Member              3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Add-PSSnapin            3.0.0.0    Microsoft.PowerShell.Core
Cmdlet          Add-Type                3.1.0.0    Microsoft.PowerShell.Utility
...
```

<span data-ttu-id="d46c8-106">A kimeneti keresi sokkal például annak a súgónak **cmd.exe**: belső parancsok táblázatos összegzését.</span><span class="sxs-lookup"><span data-stu-id="d46c8-106">This output looks a lot like the Help output of **cmd.exe**: a tabular summary of internal commands.</span></span> <span data-ttu-id="d46c8-107">Az a kivonat a `Get-Command` a fent látható minden parancs kimenete tartalmaz egy parancsmag CommandType parancsot.</span><span class="sxs-lookup"><span data-stu-id="d46c8-107">In the excerpt of the `Get-Command` command output shown above, every command shown has a CommandType of Cmdlet.</span></span> <span data-ttu-id="d46c8-108">Egy parancsmag PowerShell belső parancs típusa.</span><span class="sxs-lookup"><span data-stu-id="d46c8-108">A cmdlet is PowerShell's intrinsic command type.</span></span> <span data-ttu-id="d46c8-109">Ez a típus nagyjából megfelel, mint `dir` és `cd` a **cmd.exe** vagy a Unix-rendszerhéjjal beépített parancsok, például a bash.</span><span class="sxs-lookup"><span data-stu-id="d46c8-109">This type corresponds roughly to commands like `dir` and `cd` in **cmd.exe** or the built-in commands of Unix shells like bash.</span></span>

<span data-ttu-id="d46c8-110">A `Get-Command` parancsmag rendelkezik egy **szintaxis** paraméter, amely egyes parancsmagok szintaxisát adja vissza.</span><span class="sxs-lookup"><span data-stu-id="d46c8-110">The `Get-Command` cmdlet has a **Syntax** parameter that returns syntax of each cmdlet.</span></span> <span data-ttu-id="d46c8-111">Az alábbi példa bemutatja, hogyan szintaxisának lekérése a `Get-Help` parancsmagot:</span><span class="sxs-lookup"><span data-stu-id="d46c8-111">The following example shows how to get the syntax of the `Get-Help` cmdlet:</span></span>

```powershell
Get-Command Get-Help -Syntax
```

```output
Get-Help [[-Name] <String>] [-Path <String>] [-Category <String[]>] [-Component <String[]>] [-Functionality <String[]>]
 [-Role <String[]>] [-Full] [-Online] [-Verbose] [-Debug] [-ErrorAction <ActionPreference>] [-WarningAction <ActionPreference>] [-ErrorVariable <String>] [-WarningVariable <String>] [-OutVariable <String>] [-OutBuffer <Int32>]

Get-Help [[-Name] <String>] [-Path <String>] [-Category <String[]>] [-Component <String[]>] [-Functionality <String[]>]
 [-Role <String[]>] [-Detailed] [-Online] [-Verbose] [-Debug] [-ErrorAction <ActionPreference>] [-WarningAction <ActionPreference>] [-ErrorVariable <String>] [-WarningVariable <String>] [-OutVariable <String>] [-OutBuffer <Int32>]

Get-Help [[-Name] <String>] [-Path <String>] [-Category <String[]>] [-Component <String[]>] [-Functionality <String[]>]
 [-Role <String[]>] [-Examples] [-Online] [-Verbose] [-Debug] [-ErrorAction <ActionPreference>] [-WarningAction <ActionPreference>] [-ErrorVariable <String>] [-WarningVariable <String>] [-OutVariable <String>] [-OutBuffer <Int32>]

Get-Help [[-Name] <String>] [-Path <String>] [-Category <String[]>] [-Component <String[]>] [-Functionality <String[]>]
 [-Role <String[]>] [-Parameter <String>] [-Online] [-Verbose] [-Debug] [-ErrorAction <ActionPreference>] [-WarningAction <ActionPreference>] [-ErrorVariable <String>] [-WarningVariable <String>] [-OutVariable <String>] [-OutBuffer <Int32>]
```

## <a name="displaying-available-command-by-type"></a><span data-ttu-id="d46c8-112">Rendelkezésre álló parancssori megjelenítése típus szerint</span><span class="sxs-lookup"><span data-stu-id="d46c8-112">Displaying available command by type</span></span>

<span data-ttu-id="d46c8-113">A `Get-Command` parancs felsorolja a parancsmagok csak az aktuális munkamenetben.</span><span class="sxs-lookup"><span data-stu-id="d46c8-113">The `Get-Command` command lists only the cmdlets in the current session.</span></span> <span data-ttu-id="d46c8-114">PowerShell ténylegesen parancsok számos egyéb típusú támogatja:</span><span class="sxs-lookup"><span data-stu-id="d46c8-114">PowerShell actually supports several other types of commands:</span></span>

- <span data-ttu-id="d46c8-115">Aliasok</span><span class="sxs-lookup"><span data-stu-id="d46c8-115">Aliases</span></span>
- <span data-ttu-id="d46c8-116">Funkciók</span><span class="sxs-lookup"><span data-stu-id="d46c8-116">Functions</span></span>
- <span data-ttu-id="d46c8-117">Parancsfájlok</span><span class="sxs-lookup"><span data-stu-id="d46c8-117">Scripts</span></span>

<span data-ttu-id="d46c8-118">Külső végrehajtható fájlok, vagy egy regisztrált típus kezelőjének rendelkező fájlokat is besorolt parancsokat.</span><span class="sxs-lookup"><span data-stu-id="d46c8-118">External executable files, or files that have a registered file type handler, are also classified as commands.</span></span>

<span data-ttu-id="d46c8-119">A munkamenet összes parancs kérni, írja be:</span><span class="sxs-lookup"><span data-stu-id="d46c8-119">To get all commands in the session, type:</span></span>

```powershell
Get-Command *
```

<span data-ttu-id="d46c8-120">Ez a lista tartalmazza a keresési útvonalat a külső parancsok, így tartalmazhat, ezer elem.</span><span class="sxs-lookup"><span data-stu-id="d46c8-120">This list includes external commands in your search path so it can contain thousands of items.</span></span>
<span data-ttu-id="d46c8-121">Több hasznos, és tekintse meg a parancsok csökkentett készletét.</span><span class="sxs-lookup"><span data-stu-id="d46c8-121">It is more useful to look at a reduced set of commands.</span></span>

> [!NOTE]
> <span data-ttu-id="d46c8-122">A csillag (\*) helyettesítő karakterek használata a PowerShell-parancs argumentumainak szolgál.</span><span class="sxs-lookup"><span data-stu-id="d46c8-122">The asterisk (\*) is used for wildcard matching in PowerShell command arguments.</span></span> <span data-ttu-id="d46c8-123">A \* azt jelenti, hogy egyezik"egy vagy több bármilyen karaktert".</span><span class="sxs-lookup"><span data-stu-id="d46c8-123">The \* means "match one or more of any characters".</span></span> <span data-ttu-id="d46c8-124">Beírhatja `Get-Command a*` található betűvel kezdődő összes parancs "a".</span><span class="sxs-lookup"><span data-stu-id="d46c8-124">You can type `Get-Command a*` to find all commands that begin with the letter "a".</span></span> <span data-ttu-id="d46c8-125">Ellentétben a helyettesítő karakterek megfeleltetése **cmd.exe**, a PowerShell a helyettesítő karakter is egyezni fog a egy ideig.</span><span class="sxs-lookup"><span data-stu-id="d46c8-125">Unlike wildcard matching in **cmd.exe**, PowerShell's wildcard will also match a period.</span></span>

<span data-ttu-id="d46c8-126">Használja a **CommandType** paraméterében `Get-Command` beolvasni a más típusú natív parancsokat.</span><span class="sxs-lookup"><span data-stu-id="d46c8-126">Use the **CommandType** parameter of `Get-Command` to get native commands of other types.</span></span>
<span data-ttu-id="d46c8-127">-parancsmag futtatási eredményei között.</span><span class="sxs-lookup"><span data-stu-id="d46c8-127">cmdlet.</span></span>

<span data-ttu-id="d46c8-128">Első parancsaliasok, amelyek a hozzárendelt beceneveinek parancsokat, írja be:</span><span class="sxs-lookup"><span data-stu-id="d46c8-128">To get command aliases, which are the assigned nicknames of commands, type:</span></span>

```powershell
Get-Command -CommandType Alias
```

<span data-ttu-id="d46c8-129">A függvények az aktuális munkamenet kérni, írja be:</span><span class="sxs-lookup"><span data-stu-id="d46c8-129">To get the functions in the current session, type:</span></span>

```powershell
Get-Command -CommandType Function
```

<span data-ttu-id="d46c8-130">A PowerShell a keresési útvonalat szkriptek jelennek meg, írja be:</span><span class="sxs-lookup"><span data-stu-id="d46c8-130">To display scripts in PowerShell's search path, type:</span></span>

```powershell
Get-Command -CommandType Script
```