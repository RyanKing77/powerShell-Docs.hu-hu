---
title: Helyezi el a Megjegyzés-alapú súgó parancsfájlok |} A Microsoft Docs
ms.custom: ''
ms.date: 09/12/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 49f8267c-d887-4d7d-b9b7-80dc624b1261
caps.latest.revision: 4
ms.openlocfilehash: d199c53a748ac57bb2a5f998b5056e39d3e80c0d
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56850147"
---
# <a name="placing-comment-based-help-in-scripts"></a><span data-ttu-id="c1404-102">Megjegyzésalapú súgótémakörök elhelyezése szkriptekben</span><span class="sxs-lookup"><span data-stu-id="c1404-102">Placing Comment-Based Help in Scripts</span></span>

<span data-ttu-id="c1404-103">Ez a témakör ismerteti a Megjegyzés-alapú súgó parancsfájl helyét, hogy a `Get-Help` parancsmag társítja a Megjegyzés-alapú súgó-témakör szkriptekkel és nem lehet, a parancsfájl funkciók.</span><span class="sxs-lookup"><span data-stu-id="c1404-103">This topic explains where to place comment-based help for a script so that the `Get-Help` cmdlet associates the comment-based help topic with scripts and not with any functions that might be in the script.</span></span>

## <a name="where-to-place-comment-based-help-for-a-script"></a><span data-ttu-id="c1404-104">Megjegyzés-alapú súgó parancsfájl helye</span><span class="sxs-lookup"><span data-stu-id="c1404-104">Where to Place Comment-Based Help for a Script</span></span>

- <span data-ttu-id="c1404-105">A parancsfájl elején.</span><span class="sxs-lookup"><span data-stu-id="c1404-105">At the beginning of the script file.</span></span> <span data-ttu-id="c1404-106">Parancsfájl segítséget is megelőzi a szkriptben csak megjegyzésekkel és az üres sorok.</span><span class="sxs-lookup"><span data-stu-id="c1404-106">Script Help can be preceded in the script only by comments and blank lines.</span></span>

- <span data-ttu-id="c1404-107">A parancsfájl végén.</span><span class="sxs-lookup"><span data-stu-id="c1404-107">At the end of the script file.</span></span>

  <span data-ttu-id="c1404-108">Ha a parancsfájl törzsének (után a Súgó) első elemében függvény határozza meg, legalább két üres sorok Súgó-szkript és a függvény deklarációjában között lehet.</span><span class="sxs-lookup"><span data-stu-id="c1404-108">If the first item in the script body (after the Help) is a function declaration, there must be at least two blank lines between the end of the script Help and the function declaration.</span></span> <span data-ttu-id="c1404-109">Ellenkező esetben a Súgó értelmezi, hogy a Súgó a függvény esetében a szkript nem súgója.</span><span class="sxs-lookup"><span data-stu-id="c1404-109">Otherwise, the Help is interpreted as being Help for the function, not Help for the script.</span></span>

## <a name="examples-of-help-placement-in-a-script"></a><span data-ttu-id="c1404-110">Súgó az Elhelyezés a parancsfájl példái</span><span class="sxs-lookup"><span data-stu-id="c1404-110">Examples of Help Placement in a Script</span></span>

 <span data-ttu-id="c1404-111">Az alábbi példák bemutatják az elhelyezési lehetőségek Megjegyzés-alapú segítségét az parancsprogramok.</span><span class="sxs-lookup"><span data-stu-id="c1404-111">The following examples show each of the placement options for comment-based help for a script.</span></span>

### <a name="help-at-the-beginning-of-a-script"></a><span data-ttu-id="c1404-112">A parancsfájl elején Súgó</span><span class="sxs-lookup"><span data-stu-id="c1404-112">Help at the Beginning of a Script</span></span>

 <span data-ttu-id="c1404-113">Az alábbi példa bemutatja a Megjegyzés-alapú, a parancsfájl elején.</span><span class="sxs-lookup"><span data-stu-id="c1404-113">The following example shows comment-based at the beginning of a script.</span></span>

```
<#
.Description
This script performs a series of network connection tests.
#>

param [string]$ComputerName
...
```

### <a name="help-at-the-end-of-a-script"></a><span data-ttu-id="c1404-114">A szkript végén található Súgó</span><span class="sxs-lookup"><span data-stu-id="c1404-114">Help at the End of a Script</span></span>

 <span data-ttu-id="c1404-115">Az alábbi példa bemutatja, hogy a parancsfájl végén található megjegyzés-alapú.</span><span class="sxs-lookup"><span data-stu-id="c1404-115">The following example shows comment-based at the end of a script.</span></span>

```powershell
...
function Ping { Test-Connection -ComputerName $ComputerName }

<#
.Description
This script performs a series of network connection tests.
#>

```