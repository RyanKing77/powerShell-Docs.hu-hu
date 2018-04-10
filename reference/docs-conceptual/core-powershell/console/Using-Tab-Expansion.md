---
ms.date: 06/05/2017
keywords: PowerShell parancsmag
title: A parancssorbővítés használata
ms.assetid: c8730471-bf6a-43b8-ab1d-f9ef5a74f04e
ms.openlocfilehash: 3d047bf0691c8a304d7637aa50fba6ae99709a82
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="using-tab-expansion"></a><span data-ttu-id="76a7e-103">A parancssorbővítés használata</span><span class="sxs-lookup"><span data-stu-id="76a7e-103">Using Tab Expansion</span></span>

<span data-ttu-id="76a7e-104">Parancssori ismertetése gyakran hardvermódosításainak végezze el automatikusan, a hosszú fájlok és parancsok nevében parancs bejegyzés felgyorsítása és kezeléséről.</span><span class="sxs-lookup"><span data-stu-id="76a7e-104">Command-line shells often provide a way to complete the names of long files or commands automatically, speeding up command entry and providing .</span></span> <span data-ttu-id="76a7e-105">Windows PowerShell lehetővé teszi a fájlok és parancsmag nevének billentyűkombináció lenyomásával töltse ki a **lapon** kulcs.</span><span class="sxs-lookup"><span data-stu-id="76a7e-105">Windows PowerShell allows you to fill in file names and cmdlet names by pressing the **Tab** key.</span></span>

> [!NOTE]
> <span data-ttu-id="76a7e-106">A belső függvény TabExpansion vagy TabExpansion2 lapon bővítése szabályozza.</span><span class="sxs-lookup"><span data-stu-id="76a7e-106">Tab expansion is controlled by the internal function TabExpansion or TabExpansion2.</span></span> <span data-ttu-id="76a7e-107">Mivel ez a funkció módosíthatják vagy felül, ismertető az alapértelmezett PowerShell konfiguráció viselkedésének útmutatóját.</span><span class="sxs-lookup"><span data-stu-id="76a7e-107">Since this function can be modified or overridden, this discussion is a guide to the behavior of the default PowerShell configuration.</span></span>

<span data-ttu-id="76a7e-108">A fájlnév vagy az elérési út, a rendelkezésre álló lehetőségek automatikusan kitölti, írja be a nevet, majd kattintson a részét a **lapon** kulcs.</span><span class="sxs-lookup"><span data-stu-id="76a7e-108">To fill in a filename or path from the available choices automatically, type part of the name and press the **Tab** key.</span></span> <span data-ttu-id="76a7e-109">PowerShell lesz automatikusan bontsa ki a nevét az első találatra talált.</span><span class="sxs-lookup"><span data-stu-id="76a7e-109">PowerShell will automatically expand the name to the first match that it finds.</span></span> <span data-ttu-id="76a7e-110">Nyomja le az **lapon** kulcs ismételten értéke között fog minden a választható.</span><span class="sxs-lookup"><span data-stu-id="76a7e-110">Pressing the **Tab** key repeatedly will cycle through all of the available choices.</span></span>

<span data-ttu-id="76a7e-111">A parancsmagok neve lap bővítése kis mértékben eltér.</span><span class="sxs-lookup"><span data-stu-id="76a7e-111">The tab expansion of cmdlet names is slightly different.</span></span> <span data-ttu-id="76a7e-112">A parancsmag neve lap bővítése használatához írja be a teljes első részét a nevét (művelet) és az azt követő kötőjelet.</span><span class="sxs-lookup"><span data-stu-id="76a7e-112">To use tab expansion on a cmdlet name, type the entire first part of the name (the verb) and the hyphen that follows it.</span></span> <span data-ttu-id="76a7e-113">Kitöltése több részleges egyezéssel a nevét.</span><span class="sxs-lookup"><span data-stu-id="76a7e-113">You can fill in more of the name for a partial match.</span></span> <span data-ttu-id="76a7e-114">Például, ha beírja **get-co** és nyomja le az **lapon** kulcs, PowerShell lesz automatikusan bontsa ki a a **Get-Command** parancsmag (értesítés is módosítja az eset a betűk a szabványos formában).</span><span class="sxs-lookup"><span data-stu-id="76a7e-114">For example, if you type **get-co** and then press the **Tab** key, PowerShell will automatically expand this to the **Get-Command** cmdlet (notice that it also changes the case of letters to their standard form).</span></span> <span data-ttu-id="76a7e-115">Ha lenyomja az **lapon** kulcs újra, PowerShell váltja fel a csak más névvel megegyező nevű parancsmag, **Get-tartalom**.</span><span class="sxs-lookup"><span data-stu-id="76a7e-115">If you press **Tab** key again, PowerShell replaces this with the only other matching cmdlet name, **Get-Content**.</span></span>

<span data-ttu-id="76a7e-116">Lapon bővítése ismételten használható ugyanabban a sorban.</span><span class="sxs-lookup"><span data-stu-id="76a7e-116">You can use tab expansion repeatedly on the same line.</span></span> <span data-ttu-id="76a7e-117">Például használhatja lapon bővítése nevét a **Get-tartalom** parancsmag megadásával:</span><span class="sxs-lookup"><span data-stu-id="76a7e-117">For example, you can use tab expansion on the name of the **Get-Content** cmdlet by entering:</span></span>

```
PS> Get-Con<Tab>
```

<span data-ttu-id="76a7e-118">Amikor lenyomja az a **lapon** kulcs, a parancs bontja ki:</span><span class="sxs-lookup"><span data-stu-id="76a7e-118">When you press the **Tab** key, the command expands to:</span></span>

```
PS> Get-Content
```

<span data-ttu-id="76a7e-119">Ezután részben adja meg a naplófájl elérési útja a telepítő aktív, és újra lapon bővítése használja:</span><span class="sxs-lookup"><span data-stu-id="76a7e-119">You can then partially specify the path to the Active Setup log file and use tab expansion again:</span></span>

```
PS> Get-Content c:\windows\acts<Tab>
```

<span data-ttu-id="76a7e-120">Amikor lenyomja az a **lapon** kulcs, a parancs bontja ki:</span><span class="sxs-lookup"><span data-stu-id="76a7e-120">When you press the **Tab** key, the command expands to:</span></span>

```
PS> Get-Content C:\windows\actsetup.log
```

> [!NOTE]
> <span data-ttu-id="76a7e-121">A lap bővítése folyamat egy korlátozása, hogy lapok értelmezi szót befejezése megkísérli.</span><span class="sxs-lookup"><span data-stu-id="76a7e-121">One limitation of the tab expansion process is that tabs are always interpreted as attempts to complete a word.</span></span> <span data-ttu-id="76a7e-122">Ha másolja, és parancspéldákban illessze be a PowerShell-konzolban, győződjön meg arról, hogy a minta nem tartalmaz-e lapok; Ha igen, az eredmények előre nem látható lesz, és szinte biztosan nem lesz szándékainak.</span><span class="sxs-lookup"><span data-stu-id="76a7e-122">If you copy and paste command examples into a PowerShell console, make sure that the sample does not contain tabs; if it does, the results will be unpredictable and will almost certainly not be what you intended.</span></span>