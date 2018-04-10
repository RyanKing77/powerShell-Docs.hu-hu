---
ms.date: 06/05/2017
keywords: PowerShell parancsmag
title: Megtekintés objektum struktúra Get tag
ms.assetid: a1819ed2-2ef3-453a-b2b0-f3589c550481
ms.openlocfilehash: cc93e45e4306b3d623c1d3d1096dd20c1afc59c8
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="viewing-object-structure-get-member"></a><span data-ttu-id="9970b-103">Objektum struktúra (Get-tag) megtekintése</span><span class="sxs-lookup"><span data-stu-id="9970b-103">Viewing Object Structure (Get-Member)</span></span>

<span data-ttu-id="9970b-104">Objektumok ilyen központi szerepet játszik a Windows PowerShell, mert nincsenek több natív parancsok tetszőleges objektumtípusokat működik.</span><span class="sxs-lookup"><span data-stu-id="9970b-104">Because objects play such a central role in Windows PowerShell, there are several native commands designed to work with arbitrary object types.</span></span> <span data-ttu-id="9970b-105">A legfontosabb az egyik a **Get-tag** parancsot.</span><span class="sxs-lookup"><span data-stu-id="9970b-105">The most important one is the **Get-Member** command.</span></span>

<span data-ttu-id="9970b-106">A legegyszerűbb módszer a parancs visszaadja az objektumok elemzéséhez, hogy irányítsa a kimenetét a parancsnak a **Get-tag** parancsmag.</span><span class="sxs-lookup"><span data-stu-id="9970b-106">The simplest technique for analyzing the objects that a command returns is to pipe the output of that command to the **Get-Member** cmdlet.</span></span> <span data-ttu-id="9970b-107">A **Get-tag** parancsmag elsajátíthatja, hogy az objektum típusának formális nevét és annak tagjait teljes listáját.</span><span class="sxs-lookup"><span data-stu-id="9970b-107">The **Get-Member** cmdlet shows you the formal name of the object type and a complete listing of its members.</span></span> <span data-ttu-id="9970b-108">Visszaadott elemek száma néha túlságosan is lehet.</span><span class="sxs-lookup"><span data-stu-id="9970b-108">The number of elements that are returned can sometimes be overwhelming.</span></span> <span data-ttu-id="9970b-109">Például egy folyamat objektumot rendelkezhet több mint 100 tagokat.</span><span class="sxs-lookup"><span data-stu-id="9970b-109">For example, a process object can have over 100 members.</span></span>

<span data-ttu-id="9970b-110">A Process objektum és a kimeneti oldal összes tagját szeretné megjeleníteni az összes parancsot kell beírnia:</span><span class="sxs-lookup"><span data-stu-id="9970b-110">To see all the members of a Process object and page the output so you can view all of it, type:</span></span>

```powershell
Get-Process | Get-Member | Out-Host -Paging
```

<span data-ttu-id="9970b-111">A parancs kimenete következőhöz hasonlóan fog kinézni:</span><span class="sxs-lookup"><span data-stu-id="9970b-111">The output from this command will look something like this:</span></span>

```output
TypeName: System.Diagnostics.Process

Name                           MemberType     Definition
----                           ----------     ----------
Handles                        AliasProperty  Handles = Handlecount
Name                           AliasProperty  Name = ProcessName
NPM                            AliasProperty  NPM = NonpagedSystemMemorySize
PM                             AliasProperty  PM = PagedMemorySize
VM                             AliasProperty  VM = VirtualMemorySize
WS                             AliasProperty  WS = WorkingSet
add_Disposed                   Method         System.Void add_Disposed(Event...
...
```

<span data-ttu-id="9970b-112">Tökéletesíthetjük információk listája túl hosszú több használható szűréssel szeretnénk megnézni elemeknél használatos.</span><span class="sxs-lookup"><span data-stu-id="9970b-112">We can make this long list of information more usable by filtering for elements we want to see.</span></span> <span data-ttu-id="9970b-113">A **Get-tag** parancs segítségével felsorolja, amelyek a tulajdonságok csak tagokat.</span><span class="sxs-lookup"><span data-stu-id="9970b-113">The **Get-Member** command lets you list only members that are properties.</span></span> <span data-ttu-id="9970b-114">Nincsenek több űrlap tulajdonságai.</span><span class="sxs-lookup"><span data-stu-id="9970b-114">There are several forms of properties.</span></span> <span data-ttu-id="9970b-115">A parancsmag bármilyen típusú tulajdonságokat jeleníti meg, ha be van állítva a **Get-tag MemberType** paraméter értéke a **tulajdonságok**.</span><span class="sxs-lookup"><span data-stu-id="9970b-115">The cmdlet displays properties of any type if we set the **Get-Member MemberType** parameter to the value **Properties**.</span></span> <span data-ttu-id="9970b-116">A megjelenő listában még nagyon hosszú, de egy kicsit könnyebben kezelhető:</span><span class="sxs-lookup"><span data-stu-id="9970b-116">The resulting list is still very long, but a bit more manageable:</span></span>

```
PS> Get-Process | Get-Member -MemberType Properties

   TypeName: System.Diagnostics.Process

Name                       MemberType     Definition
----                       ----------     ----------
Handles                    AliasProperty  Handles = Handlecount
Name                       AliasProperty  Name = ProcessName
...
ExitCode                   Property       System.Int32 ExitCode {get;}
...
Handle                     Property       System.IntPtr Handle {get;}
...
CPU                        ScriptProperty System.Object CPU {get=$this.Total...
...
Path                       ScriptProperty System.Object Path {get=$this.Main...
...
```

> [!NOTE]
> <span data-ttu-id="9970b-117">Az engedélyezett értékek MemberType: AliasProperty, CodeProperty, tulajdonság, NoteProperty, ScriptProperty, tulajdonságok, tulajdonsághalmaz, módszer, CodeMethod, ScriptMethod, módszerek, ParameterizedProperty, MemberSet és az összes.</span><span class="sxs-lookup"><span data-stu-id="9970b-117">The allowed values of MemberType are AliasProperty, CodeProperty, Property, NoteProperty, ScriptProperty, Properties, PropertySet, Method, CodeMethod, ScriptMethod, Methods, ParameterizedProperty, MemberSet, and All.</span></span>

<span data-ttu-id="9970b-118">A folyamat több mint 60 tulajdonságok van.</span><span class="sxs-lookup"><span data-stu-id="9970b-118">There are over 60 properties for a process.</span></span> <span data-ttu-id="9970b-119">A Windows PowerShell gyakran látható, csak kevés a jól ismert objektum tulajdonságait, amely megjeleníti az összes OK Kezelhetetlen mennyiségű információ eredményezne.</span><span class="sxs-lookup"><span data-stu-id="9970b-119">The reason Windows PowerShell often shows only a handful of properties for any well-known object is that showing all of them would produce an unmanageable amount of information.</span></span>

> [!NOTE]
> <span data-ttu-id="9970b-120">A Windows PowerShell egy objektum típusának megjelenítése a végződése nevű XML-fájlokban tárolt információk segítségével határozza meg. format.ps1xml.</span><span class="sxs-lookup"><span data-stu-id="9970b-120">Windows PowerShell determines how to display an object type by using information stored in XML files that have names ending in .format.ps1xml.</span></span> <span data-ttu-id="9970b-121">A folyamat objektumok, amelyek .NET System.Diagnostics.Process objektumok, formázási adatai DotNetTypes.format.ps1xml tárolja.</span><span class="sxs-lookup"><span data-stu-id="9970b-121">The formatting data for process objects, which are .NET System.Diagnostics.Process objects, is stored in DotNetTypes.format.ps1xml.</span></span>

<span data-ttu-id="9970b-122">Alapértelmezés szerint megjeleníti a Windows PowerShell tulajdonságokat meg kell, ha szüksége lesz a kimeneti adatok formázásához saját maga.</span><span class="sxs-lookup"><span data-stu-id="9970b-122">If you need to look at properties other than those that Windows PowerShell displays by default, you will need to format the output data yourself.</span></span> <span data-ttu-id="9970b-123">Ezt megteheti a formátum-parancsmagok használatával.</span><span class="sxs-lookup"><span data-stu-id="9970b-123">This can be done by using the format cmdlets.</span></span>