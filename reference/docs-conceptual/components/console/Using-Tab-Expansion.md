---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: A parancssorbővítés használata
ms.openlocfilehash: d96cbf848f464aff29a7bed9b70d0b6a000aa808
ms.sourcegitcommit: a6f13c16a535acea279c0ddeca72f1f0d8a8ce4c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2019
ms.locfileid: "67031012"
---
# <a name="using-tab-expansion"></a><span data-ttu-id="6682b-103">A parancssorbővítés használata</span><span class="sxs-lookup"><span data-stu-id="6682b-103">Using Tab Expansion</span></span>

<span data-ttu-id="6682b-104">Parancssori parancskörnyezet gyakran hardvermódosításainak fejezze be a nevét, illetve hosszú fájlok vagy parancsok automatikusan, felgyorsítva a parancs bejegyzést, és biztosítják, hogy a mutatók.</span><span class="sxs-lookup"><span data-stu-id="6682b-104">Command-line shells often provide a way to complete the names of long files or commands automatically, speeding up command entry and providing hints.</span></span> <span data-ttu-id="6682b-105">PowerShell lehetővé teszi, hogy a fájlok és a parancsmag nevének lenyomásával töltse ki a <kbd>lapon</kbd> kulcsot.</span><span class="sxs-lookup"><span data-stu-id="6682b-105">PowerShell allows you to fill in file names and cmdlet names by pressing the <kbd>Tab</kbd> key.</span></span>

> [!NOTE]
> <span data-ttu-id="6682b-106">A parancssorbővítés a belső függvény TabExpansion vagy TabExpansion2 vezérli.</span><span class="sxs-lookup"><span data-stu-id="6682b-106">Tab expansion is controlled by the internal function TabExpansion or TabExpansion2.</span></span> <span data-ttu-id="6682b-107">Mivel ez a függvény módosíthatják vagy felülírni, az adott vitafórum egy útmutató, amellyel a PowerShell alapértelmezett konfiguráció viselkedésének.</span><span class="sxs-lookup"><span data-stu-id="6682b-107">Since this function can be modified or overridden, this discussion is a guide to the behavior of the default PowerShell configuration.</span></span>

<span data-ttu-id="6682b-108">A fájlnév vagy elérési útját a rendelkezésre álló lehetőségek közül automatikusan kitölti, írja be a nevét, majd nyomja le a részét a <kbd>lapon</kbd> kulcsot.</span><span class="sxs-lookup"><span data-stu-id="6682b-108">To fill in a filename or path from the available choices automatically, type part of the name and press the <kbd>Tab</kbd> key.</span></span> <span data-ttu-id="6682b-109">PowerShell lesz automatikusan bontsa ki a nevét az első egyezést talált.</span><span class="sxs-lookup"><span data-stu-id="6682b-109">PowerShell will automatically expand the name to the first match that it finds.</span></span> <span data-ttu-id="6682b-110">Nyomja le az <kbd>lapon</kbd> kulcs ismételt fog ciklus keresztül a rendelkezésre álló lehetőségek mindegyikét.</span><span class="sxs-lookup"><span data-stu-id="6682b-110">Pressing the <kbd>Tab</kbd> key repeatedly will cycle through all of the available choices.</span></span>

<span data-ttu-id="6682b-111">A parancssorbővítés parancsmag neve kismértékben eltér.</span><span class="sxs-lookup"><span data-stu-id="6682b-111">The tab expansion of cmdlet names is slightly different.</span></span> <span data-ttu-id="6682b-112">A parancssorbővítés használata a parancsmag neve, írja be a nevét (művelet) és az azt követő kötőjel teljes első részét.</span><span class="sxs-lookup"><span data-stu-id="6682b-112">To use tab expansion on a cmdlet name, type the entire first part of the name (the verb) and the hyphen that follows it.</span></span> <span data-ttu-id="6682b-113">Kitöltheti a további részleges nevét.</span><span class="sxs-lookup"><span data-stu-id="6682b-113">You can fill in more of the name for a partial match.</span></span> <span data-ttu-id="6682b-114">Például, ha beírja `get-co` és nyomja le az <kbd>lapon</kbd> kulcs PowerShell automatikusan ki ezt a a `Get-Command` parancsmag (figyelje meg, hogy azt is megváltozik a kis-és nagybetűket a szabványos formában).</span><span class="sxs-lookup"><span data-stu-id="6682b-114">For example, if you type `get-co` and then press the <kbd>Tab</kbd> key, PowerShell will automatically expand this to the `Get-Command` cmdlet (notice that it also changes the case of letters to their standard form).</span></span> <span data-ttu-id="6682b-115">Ha lenyomja <kbd>lapon</kbd> kulcs ismét PowerShell váltja fel a csak más névvel megegyező nevű parancsmagot, `Get-Content`.</span><span class="sxs-lookup"><span data-stu-id="6682b-115">If you press <kbd>Tab</kbd> key again, PowerShell replaces this with the only other matching cmdlet name, `Get-Content`.</span></span>

<span data-ttu-id="6682b-116">A parancssorbővítés többször használható ugyanabban a sorban.</span><span class="sxs-lookup"><span data-stu-id="6682b-116">You can use tab expansion repeatedly on the same line.</span></span> <span data-ttu-id="6682b-117">Például használhatja a parancssorbővítés nevére a `Get-Content` parancsmag megadásával:</span><span class="sxs-lookup"><span data-stu-id="6682b-117">For example, you can use tab expansion on the name of the `Get-Content` cmdlet by entering:</span></span>

```
PS> Get-Con<Tab>
```

<span data-ttu-id="6682b-118">Amikor lenyomja a <kbd>lapon</kbd> kulcs, a parancs kibontja a:</span><span class="sxs-lookup"><span data-stu-id="6682b-118">When you press the <kbd>Tab</kbd> key, the command expands to:</span></span>

```
PS> Get-Content
```

<span data-ttu-id="6682b-119">Ezután részben adja meg a naplófájl elérési útja a beállítás aktív, és újra a parancssorbővítés használata:</span><span class="sxs-lookup"><span data-stu-id="6682b-119">You can then partially specify the path to the Active Setup log file and use tab expansion again:</span></span>

```
PS> Get-Content c:\windows\acts<Tab>
```

<span data-ttu-id="6682b-120">Amikor lenyomja a <kbd>lapon</kbd> kulcs, a parancs kibontja a:</span><span class="sxs-lookup"><span data-stu-id="6682b-120">When you press the <kbd>Tab</kbd> key, the command expands to:</span></span>

```
PS> Get-Content C:\windows\actsetup.log
```

> [!NOTE]
> <span data-ttu-id="6682b-121">A lap csoportbővítési folyamatának egyik korlátozása, hogy lapok értelmezi kísérletek szó végrehajtásához.</span><span class="sxs-lookup"><span data-stu-id="6682b-121">One limitation of the tab expansion process is that tabs are always interpreted as attempts to complete a word.</span></span> <span data-ttu-id="6682b-122">Ha másolja és illessze be a PowerShell-konzolt parancspéldákban, győződjön meg róla, hogy a minta nesmí obsahovat tabulátory; Ha igen, az eredmények előre nem látható lesz, és szinte biztosan nem kívánt.</span><span class="sxs-lookup"><span data-stu-id="6682b-122">If you copy and paste command examples into a PowerShell console, make sure that the sample does not contain tabs; if it does, the results will be unpredictable and will almost certainly not be what you intended.</span></span>
