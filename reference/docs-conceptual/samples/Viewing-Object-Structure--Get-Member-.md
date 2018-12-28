---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: Megtekintés objektum struktúra Get-Member
ms.assetid: a1819ed2-2ef3-453a-b2b0-f3589c550481
ms.openlocfilehash: cc93e45e4306b3d623c1d3d1096dd20c1afc59c8
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/14/2018
ms.locfileid: "53404499"
---
# <a name="viewing-object-structure-get-member"></a><span data-ttu-id="b68e8-103">Az objektumstruktúra (Get-Member)</span><span class="sxs-lookup"><span data-stu-id="b68e8-103">Viewing Object Structure (Get-Member)</span></span>

<span data-ttu-id="b68e8-104">Objektumok ilyen központi szerepet játszik a Windows PowerShell, mert nincsenek több natív parancsok tetszőleges objektumtípusok való használatra készült.</span><span class="sxs-lookup"><span data-stu-id="b68e8-104">Because objects play such a central role in Windows PowerShell, there are several native commands designed to work with arbitrary object types.</span></span> <span data-ttu-id="b68e8-105">A legfontosabb az egyik a **Get-Member** parancsot.</span><span class="sxs-lookup"><span data-stu-id="b68e8-105">The most important one is the **Get-Member** command.</span></span>

<span data-ttu-id="b68e8-106">A legegyszerűbb módszer, amely a parancs visszaadja az objektumok elemzése, hogy a kimenetet, hogy a parancs a **Get-Member** parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="b68e8-106">The simplest technique for analyzing the objects that a command returns is to pipe the output of that command to the **Get-Member** cmdlet.</span></span> <span data-ttu-id="b68e8-107">A **Get-Member** parancsmag megjeleníti az objektumtípus formális nevét és a tagjai teljes listáját.</span><span class="sxs-lookup"><span data-stu-id="b68e8-107">The **Get-Member** cmdlet shows you the formal name of the object type and a complete listing of its members.</span></span> <span data-ttu-id="b68e8-108">A visszaadott elemek száma néha elsöprő is lehet.</span><span class="sxs-lookup"><span data-stu-id="b68e8-108">The number of elements that are returned can sometimes be overwhelming.</span></span> <span data-ttu-id="b68e8-109">Ha például egy folyamat objektumot rendelkezhet több mint 100 tag.</span><span class="sxs-lookup"><span data-stu-id="b68e8-109">For example, a process object can have over 100 members.</span></span>

<span data-ttu-id="b68e8-110">Egy folyamat objektumot és a kimeneti oldal összes tagját jelenik meg, hogy minden adatot meg tudja tekinteni, írja be:</span><span class="sxs-lookup"><span data-stu-id="b68e8-110">To see all the members of a Process object and page the output so you can view all of it, type:</span></span>

```powershell
Get-Process | Get-Member | Out-Host -Paging
```

<span data-ttu-id="b68e8-111">Ez a parancs kimenete ehhez hasonló fog kinézni:</span><span class="sxs-lookup"><span data-stu-id="b68e8-111">The output from this command will look something like this:</span></span>

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

<span data-ttu-id="b68e8-112">Azt is, hogy információk hosszú listája használhatóbbá szeretnénk megnézni elemek szűrése.</span><span class="sxs-lookup"><span data-stu-id="b68e8-112">We can make this long list of information more usable by filtering for elements we want to see.</span></span> <span data-ttu-id="b68e8-113">A **Get-Member** listában csak a tagok, amelyek a Tulajdonságok parancs segítségével.</span><span class="sxs-lookup"><span data-stu-id="b68e8-113">The **Get-Member** command lets you list only members that are properties.</span></span> <span data-ttu-id="b68e8-114">Nincsenek tulajdonságok több formáját.</span><span class="sxs-lookup"><span data-stu-id="b68e8-114">There are several forms of properties.</span></span> <span data-ttu-id="b68e8-115">A parancsmag bármilyen típusú tulajdonságokat jeleníti meg, ha be van állítva a **Get-Member MemberType** paraméter értékére **tulajdonságok**.</span><span class="sxs-lookup"><span data-stu-id="b68e8-115">The cmdlet displays properties of any type if we set the **Get-Member MemberType** parameter to the value **Properties**.</span></span> <span data-ttu-id="b68e8-116">Az eredményül kapott bejegyzéslista még mindig nagyon hosszú, de egy kicsit jobban kezelhető:</span><span class="sxs-lookup"><span data-stu-id="b68e8-116">The resulting list is still very long, but a bit more manageable:</span></span>

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
> <span data-ttu-id="b68e8-117">Az engedélyezett értékek a MemberType: AliasProperty, CodeProperty, tulajdonságot, NoteProperty, ScriptProperty, tulajdonságok, PropertySet, metódus, CodeMethod, ScriptMethod, módszerek, ParameterizedProperty, MemberSet és az összes.</span><span class="sxs-lookup"><span data-stu-id="b68e8-117">The allowed values of MemberType are AliasProperty, CodeProperty, Property, NoteProperty, ScriptProperty, Properties, PropertySet, Method, CodeMethod, ScriptMethod, Methods, ParameterizedProperty, MemberSet, and All.</span></span>

<span data-ttu-id="b68e8-118">Nincsenek a folyamat több mint 60 tulajdonságait.</span><span class="sxs-lookup"><span data-stu-id="b68e8-118">There are over 60 properties for a process.</span></span> <span data-ttu-id="b68e8-119">A Windows PowerShell gyakran látható csak néhány rekordra minden olyan jól ismert objektum tulajdonságait, hogy ezek mindegyike megjelenítő OK akkor az eredmény egy Kezelhetetlen mennyiségű olyan információt.</span><span class="sxs-lookup"><span data-stu-id="b68e8-119">The reason Windows PowerShell often shows only a handful of properties for any well-known object is that showing all of them would produce an unmanageable amount of information.</span></span>

> [!NOTE]
> <span data-ttu-id="b68e8-120">Windows PowerShell egy objektum típusának megjelenítése végződésű névvel rendelkező XML-fájlokban tárolt információk alapján határozza meg. format.ps1xml.</span><span class="sxs-lookup"><span data-stu-id="b68e8-120">Windows PowerShell determines how to display an object type by using information stored in XML files that have names ending in .format.ps1xml.</span></span> <span data-ttu-id="b68e8-121">A folyamat objektumok, amelyek .NET System.Diagnostics.Process objektumok, adatok formázása DotNetTypes.format.ps1xml van tárolva.</span><span class="sxs-lookup"><span data-stu-id="b68e8-121">The formatting data for process objects, which are .NET System.Diagnostics.Process objects, is stored in DotNetTypes.format.ps1xml.</span></span>

<span data-ttu-id="b68e8-122">Ha kivételével, amelyek a Windows PowerShell alapértelmezés szerint megjeleníti a tulajdonságainak megjelenítéséhez szüksége, szüksége lesz a kimeneti adatok formázásához, saját magának.</span><span class="sxs-lookup"><span data-stu-id="b68e8-122">If you need to look at properties other than those that Windows PowerShell displays by default, you will need to format the output data yourself.</span></span> <span data-ttu-id="b68e8-123">Ez a formátum parancsmagok segítségével teheti meg.</span><span class="sxs-lookup"><span data-stu-id="b68e8-123">This can be done by using the format cmdlets.</span></span>