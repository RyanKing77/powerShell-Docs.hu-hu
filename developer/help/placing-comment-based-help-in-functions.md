---
title: A függvények helyezi el a Megjegyzés-alapú súgó |} A Microsoft Docs
ms.custom: ''
ms.date: 09/12/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 5ec7159e-e4e9-4b21-95df-94244432f679
caps.latest.revision: 5
ms.openlocfilehash: a663bd69be7825b1685f64ff8d3068bdd8ca3265
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56848173"
---
# <a name="placing-comment-based-help-in-functions"></a><span data-ttu-id="0705c-102">Megjegyzésalapú súgótémakörök elhelyezése függvényekben</span><span class="sxs-lookup"><span data-stu-id="0705c-102">Placing Comment-Based Help in Functions</span></span>

<span data-ttu-id="0705c-103">Ez a témakör ismerteti a Megjegyzés-alapú súgó-függvény elhelyezése, hogy a `Get-Help` parancsmag hozzárendeli a megfelelő függvény Megjegyzés-alapú súgó-témakör.</span><span class="sxs-lookup"><span data-stu-id="0705c-103">This topic explains where to place comment-based help for a function so that the `Get-Help` cmdlet associates the comment-based help topic with the correct function.</span></span>

## <a name="where-to-place-comment-based-help-for-a-function"></a><span data-ttu-id="0705c-104">Megjegyzés-alapú súgó-függvény elhelyezése</span><span class="sxs-lookup"><span data-stu-id="0705c-104">Where to Place Comment-Based Help for a Function</span></span>

- <span data-ttu-id="0705c-105">A függvény törzsében elején.</span><span class="sxs-lookup"><span data-stu-id="0705c-105">At the beginning of the function body.</span></span>

- <span data-ttu-id="0705c-106">A függvény törzsében végén.</span><span class="sxs-lookup"><span data-stu-id="0705c-106">At the end of the function body.</span></span>

- <span data-ttu-id="0705c-107">Mielőtt a `Function` kulcsszót.</span><span class="sxs-lookup"><span data-stu-id="0705c-107">Before the `Function` keyword.</span></span> <span data-ttu-id="0705c-108">A funkciót, ha van olyan parancsfájl vagy a modul skriptu nem szerepelhet egynél több üres sor utolsó sora a Megjegyzés-alapú súgó között, és a `Function` kulcsszót.</span><span class="sxs-lookup"><span data-stu-id="0705c-108">When the function is in a script or script module, there cannot be more than one blank line between the last line of the comment-based help and the `Function` keyword.</span></span> <span data-ttu-id="0705c-109">Ellenkező esetben `Get-Help` társítja a Súgó a szkriptet, és nem az a függvény.</span><span class="sxs-lookup"><span data-stu-id="0705c-109">Otherwise, `Get-Help` associates the help with the script, not with the function.</span></span>

## <a name="examples-of-help-placement-in-a-function"></a><span data-ttu-id="0705c-110">Súgó az Elhelyezés a függvény példái</span><span class="sxs-lookup"><span data-stu-id="0705c-110">Examples of Help Placement in a Function</span></span>

 <span data-ttu-id="0705c-111">Az alábbi példák bemutatják az egyes Megjegyzés-alapú súgó-függvény három elhelyezési beállításait.</span><span class="sxs-lookup"><span data-stu-id="0705c-111">The following examples show each of the three placement options for comment-based help for a function.</span></span>

### <a name="help-at-the-beginning-of-a-function-body"></a><span data-ttu-id="0705c-112">A függvény törzséhez elején Súgó</span><span class="sxs-lookup"><span data-stu-id="0705c-112">Help at the Beginning of a Function Body</span></span>

 <span data-ttu-id="0705c-113">Az alábbi példa bemutatja a Megjegyzés-alapú, a függvény törzséhez elején.</span><span class="sxs-lookup"><span data-stu-id="0705c-113">The following example shows comment-based at the beginning of a function body.</span></span>

```powershell

function MyProcess
{
    <#
       .Description
       The MyProcess function gets the Windows PowerShell process.
    #>

    Get-Process powershell
}

```

### <a name="help-at-the-end-of-a-function-body"></a><span data-ttu-id="0705c-114">A függvény törzséhez végén található Súgó</span><span class="sxs-lookup"><span data-stu-id="0705c-114">Help at the End of a Function Body</span></span>

 <span data-ttu-id="0705c-115">Az alábbi példa bemutatja, hogy a függvény törzséhez végén található megjegyzés-alapú.</span><span class="sxs-lookup"><span data-stu-id="0705c-115">The following example shows comment-based at the end of a function body.</span></span>

```powershell

function MyFunction
{
    Get-Process powershell

    <#
       .Description
       The MyProcess function gets the Windows PowerShell process.
    #>
}

```

### <a name="help-before-the-function-keyword"></a><span data-ttu-id="0705c-116">A függvény kulcsszó előtt Súgó</span><span class="sxs-lookup"><span data-stu-id="0705c-116">Help Before the Function Keyword</span></span>

 <span data-ttu-id="0705c-117">A következő példákban Megjegyzés-alapú előtt a függvény kulcsszó a sorban.</span><span class="sxs-lookup"><span data-stu-id="0705c-117">The following examples shows comment-based on the line before the function keyword.</span></span>

```powershell

<#
    .Description
    The MyProcess function gets the Windows PowerShell process.
#>
function MyFunction { Get-Process powershell}

```