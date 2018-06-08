---
ms.date: 06/05/2017
keywords: PowerShell parancsmag
title: Információk kérése a parancsokról
ms.assetid: 56f8e5b4-d97c-4e59-abbe-bf13e464eb0d
ms.openlocfilehash: c51579fe2cdf4f2a0d3248d1aaf3f1f9cac83868
ms.sourcegitcommit: 01d6985ed190a222e9da1da41596f524f607a5bc
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/07/2018
ms.locfileid: "34482726"
---
# <a name="getting-information-about-commands"></a><span data-ttu-id="60d2f-103">Információk kérése a parancsokról</span><span class="sxs-lookup"><span data-stu-id="60d2f-103">Getting Information About Commands</span></span>
<span data-ttu-id="60d2f-104">A Windows PowerShell `Get-Command` parancsmag lekéri az aktuális munkamenetben rendelkezésre álló összes parancsot.</span><span class="sxs-lookup"><span data-stu-id="60d2f-104">The Windows PowerShell `Get-Command` cmdlet gets all commands that are available in your current session.</span></span> <span data-ttu-id="60d2f-105">Amikor beírja `Get-Command` egy PowerShell-parancssorba, a következőhöz hasonló kimenetet fog látni:</span><span class="sxs-lookup"><span data-stu-id="60d2f-105">When you type `Get-Command` at a PowerShell prompt, you will see output similar to the following:</span></span>

```
PS> Get-Command
CommandType     Name                            Definition
-----------     ----                            ----------
Cmdlet          Add-Content                     Add-Content [-Path] <String[...
Cmdlet          Add-History                     Add-History [[-InputObject] ...
Cmdlet          Add-Member                      Add-Member [-MemberType] <PS...
...
```

<span data-ttu-id="60d2f-106">Ez a kimeneti keres sokkal például a Cmd.exe súgó kimenete: belső parancsok táblázatos összegzését.</span><span class="sxs-lookup"><span data-stu-id="60d2f-106">This output looks a lot like the Help output of Cmd.exe: a tabular summary of internal commands.</span></span> <span data-ttu-id="60d2f-107">A kivonat a a **Get-Command** a fent látható minden parancs látható kimeneti rendelkezik egy parancsmag CommandType parancsot.</span><span class="sxs-lookup"><span data-stu-id="60d2f-107">In the excerpt of the **Get-Command** command output shown above, every command shown has a CommandType of Cmdlet.</span></span> <span data-ttu-id="60d2f-108">A parancsmag típus Windows PowerShell belső parancs - olyan típusú, amely a nagyjából megfelel a **dir** és **cd** Cmd.exe, valamint a UNIX ismertetése, például a BASH built-ins parancsok.</span><span class="sxs-lookup"><span data-stu-id="60d2f-108">A cmdlet is Windows PowerShell's intrinsic command type - a type that corresponds roughly to the **dir** and **cd** commands of Cmd.exe and to built-ins in UNIX shells such as BASH.</span></span>

<span data-ttu-id="60d2f-109">A kimenet a `Get-Command` parancsot, a definíciók végződhet folytatást jelző pontokra (...), annak jelzésére, hogy a PowerShell nem tudja megjeleníteni a tartalmat a rendelkezésre álló területet.</span><span class="sxs-lookup"><span data-stu-id="60d2f-109">In the output of the `Get-Command` command, all the definitions end with ellipses (...) to indicate that PowerShell cannot display all the content in the available space.</span></span> <span data-ttu-id="60d2f-110">Windows PowerShell kimenet megjelenítése, ha a kimeneti szövegként formázza, és azt, hogy az adatok szabályszerűen felelnek meg az ablak majd elrendezése.</span><span class="sxs-lookup"><span data-stu-id="60d2f-110">When Windows PowerShell displays output, it formats the output as text and then arranges it to make the data fit cleanly into the window.</span></span> <span data-ttu-id="60d2f-111">Előadás a későbbi szakaszában a is.</span><span class="sxs-lookup"><span data-stu-id="60d2f-111">We will talk about this later in the section on formatters.</span></span>

<span data-ttu-id="60d2f-112">A `Get-Command` parancsmagja rendelkezik egy **szintaxis** paraméter, amely minden parancsmag szintaxisa a következő lekérdezi.</span><span class="sxs-lookup"><span data-stu-id="60d2f-112">The `Get-Command` cmdlet has a **Syntax** parameter that gets the syntax of each cmdlet.</span></span> <span data-ttu-id="60d2f-113">Ahhoz, hogy a Get-Help parancsmag szintaxisa a következő, a következő paranccsal:</span><span class="sxs-lookup"><span data-stu-id="60d2f-113">To get the syntax of the Get-Help cmdlet, use the following command:</span></span>

```
Get-Command Get-Help -Syntax

Get-Help [[-Name] <String>] [-Path <String>] [-Category <String[]>] [-Component <String[]>] [-Functionality <String[]>]
 [-Role <String[]>] [-Full] [-Online] [-Verbose] [-Debug] [-ErrorAction <ActionPreference>] [-WarningAction <ActionPreference>] [-ErrorVariable <String>] [-WarningVariable <String>] [-OutVariable <String>] [-OutBuffer <Int32>]

Get-Help [[-Name] <String>] [-Path <String>] [-Category <String[]>] [-Component <String[]>] [-Functionality <String[]>]
 [-Role <String[]>] [-Detailed] [-Online] [-Verbose] [-Debug] [-ErrorAction <ActionPreference>] [-WarningAction <ActionPreference>] [-ErrorVariable <String>] [-WarningVariable <String>] [-OutVariable <String>] [-OutBuffer <Int32>]

Get-Help [[-Name] <String>] [-Path <String>] [-Category <String[]>] [-Component <String[]>] [-Functionality <String[]>]
 [-Role <String[]>] [-Examples] [-Online] [-Verbose] [-Debug] [-ErrorAction <ActionPreference>] [-WarningAction <ActionPreference>] [-ErrorVariable <String>] [-WarningVariable <String>] [-OutVariable <String>] [-OutBuffer <Int32>]

Get-Help [[-Name] <String>] [-Path <String>] [-Category <String[]>] [-Component <String[]>] [-Functionality <String[]>]
 [-Role <String[]>] [-Parameter <String>] [-Online] [-Verbose] [-Debug] [-ErrorAction <ActionPreference>] [-WarningAction <ActionPreference>] [-ErrorVariable <String>] [-WarningVariable <String>] [-OutVariable <String>] [-OutBuffer <Int32>]
```

### <a name="displaying-available-command-types"></a><span data-ttu-id="60d2f-114">Elérhető parancstípusok megjelenítése</span><span class="sxs-lookup"><span data-stu-id="60d2f-114">Displaying Available Command Types</span></span>
<span data-ttu-id="60d2f-115">A **Get-Command** parancs nem szerepel minden elérhető Windows PowerShell parancsot.</span><span class="sxs-lookup"><span data-stu-id="60d2f-115">The **Get-Command** command does not list every command that is available in Windows PowerShell.</span></span> <span data-ttu-id="60d2f-116">Ehelyett a **Get-Command** parancs csak a parancsmagokat a jelenlegi munkamenet jeleníti meg.</span><span class="sxs-lookup"><span data-stu-id="60d2f-116">Instead, the **Get-Command** command lists only the cmdlets in the current session.</span></span> <span data-ttu-id="60d2f-117">A Windows PowerShell ténylegesen támogatja több más típusú parancsokat.</span><span class="sxs-lookup"><span data-stu-id="60d2f-117">Windows PowerShell actually supports several other types of commands.</span></span> <span data-ttu-id="60d2f-118">Aliasok, függvények és parancsfájlok egyaránt Windows PowerShell-parancsok, bár a nem a Windows PowerShell felhasználói útmutatója részletes ismertetése.</span><span class="sxs-lookup"><span data-stu-id="60d2f-118">Aliases, functions, and scripts are also Windows PowerShell commands, although they are not discussed in detail in the Windows PowerShell User's Guide.</span></span> <span data-ttu-id="60d2f-119">Külső fájlok, amelyeknek is végrehajtható, vagy egy regisztrált típus kezelőjének is besorolt parancsok.</span><span class="sxs-lookup"><span data-stu-id="60d2f-119">External files that are executable, or have a registered file type handler, are also classified as commands.</span></span>

<span data-ttu-id="60d2f-120">Ahhoz, hogy minden parancs a munkamenetben, írja be:</span><span class="sxs-lookup"><span data-stu-id="60d2f-120">To get all commands in the session, type:</span></span>

```powershell
Get-Command *
```

<span data-ttu-id="60d2f-121">Mivel ebben a listában a keresési elérési út külső fájlokat tartalmazza, ezrei között válogathat tartalmazhat.</span><span class="sxs-lookup"><span data-stu-id="60d2f-121">Because this list includes external files in your search path, it may contain thousands of items.</span></span> <span data-ttu-id="60d2f-122">Több célszerű egy meghatározott parancsok közül.</span><span class="sxs-lookup"><span data-stu-id="60d2f-122">It is more useful to look at a reduced set of commands.</span></span>

<span data-ttu-id="60d2f-123">Más típusú natív parancsok használatához a **CommandType** paramétere a `Get-Command` parancsmag.</span><span class="sxs-lookup"><span data-stu-id="60d2f-123">To get native commands of other types, use the **CommandType** parameter of the `Get-Command` cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="60d2f-124">A csillag (\*) helyettesítő karakterek használata a Windows PowerShell parancssori argumentumok szolgál.</span><span class="sxs-lookup"><span data-stu-id="60d2f-124">The asterisk (\*) is used for wildcard matching in Windows PowerShell command arguments.</span></span> <span data-ttu-id="60d2f-125">A \* azt jelenti, hogy "egyezik egy vagy több szereplő olyan karakterek".</span><span class="sxs-lookup"><span data-stu-id="60d2f-125">The \* means "match one or more of any characters".</span></span> <span data-ttu-id="60d2f-126">Beírhatja `Get-Command a*` található a betűvel kezdődő minden parancs "a".</span><span class="sxs-lookup"><span data-stu-id="60d2f-126">You can type `Get-Command a*` to find all commands that begin with the letter "a".</span></span> <span data-ttu-id="60d2f-127">Ellentétben a Cmd.exe megfelelő helyettesítő a Windows PowerShell helyettesítő is fog egyezni időtartamra.</span><span class="sxs-lookup"><span data-stu-id="60d2f-127">Unlike wildcard matching in Cmd.exe, Windows PowerShell's wildcard will also match a period.</span></span>

<span data-ttu-id="60d2f-128">Get parancs aliasok, amelyek a hozzárendelt becenevet parancsokat, írja be:</span><span class="sxs-lookup"><span data-stu-id="60d2f-128">To get command aliases, which are the assigned nicknames of commands, type:</span></span>

```powershell
Get-Command -CommandType Alias
```

<span data-ttu-id="60d2f-129">A funkciók eléréséhez a jelenlegi munkamenet, írja be:</span><span class="sxs-lookup"><span data-stu-id="60d2f-129">To get the functions in the current session, type:</span></span>

```powershell
Get-Command -CommandType Function
```

<span data-ttu-id="60d2f-130">A Windows PowerShell keresési út parancsfájlok megjelenítéséhez írja be:</span><span class="sxs-lookup"><span data-stu-id="60d2f-130">To display scripts in Windows PowerShell's search path, type:</span></span>

```powershell
Get-Command -CommandType Script
```
