---
title: Megjegyzés-alapú súgó szintaxisát |} A Microsoft Docs
ms.custom: ''
ms.date: 09/12/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: e8adc997-1a71-48e9-9383-513ef13da7cf
caps.latest.revision: 4
ms.openlocfilehash: 584e5923008e8369a83c699478844f0e0c295adc
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62083212"
---
# <a name="syntax-of-comment-based-help"></a><span data-ttu-id="dae3d-102">Megjegyzésalapú súgótémakörök szintaxisa</span><span class="sxs-lookup"><span data-stu-id="dae3d-102">Syntax of Comment-Based Help</span></span>

<span data-ttu-id="dae3d-103">Ez a szakasz ismerteti a Megjegyzés-alapú súgó szintaxisát.</span><span class="sxs-lookup"><span data-stu-id="dae3d-103">This section describes the syntax of comment-based help.</span></span>

## <a name="syntax-diagram"></a><span data-ttu-id="dae3d-104">Szintaxisdiagramja</span><span class="sxs-lookup"><span data-stu-id="dae3d-104">Syntax Diagram</span></span>

 <span data-ttu-id="dae3d-105">A Megjegyzés-alapú súgó szintaxisa a következő:</span><span class="sxs-lookup"><span data-stu-id="dae3d-105">The syntax for comment-based Help is as follows:</span></span>

```
# .< help keyword>
# <help content>

-or -

<#
.< help keyword>
< help content>
#>
```

## <a name="syntax-description"></a><span data-ttu-id="dae3d-106">Szintaxis leírása</span><span class="sxs-lookup"><span data-stu-id="dae3d-106">Syntax Description</span></span>

 <span data-ttu-id="dae3d-107">Megjegyzés-alapú súgó írt megjegyzések sorozataként.</span><span class="sxs-lookup"><span data-stu-id="dae3d-107">Comment-based Help is written as a series of comments.</span></span> <span data-ttu-id="dae3d-108">Megjegyzések minden egyes sora elé is írja be a Megjegyzés szimbólumát (#), vagy használhatja a "\<#" és "#>" hozhat létre egy megjegyzésblokkot szimbólumok.</span><span class="sxs-lookup"><span data-stu-id="dae3d-108">You can type a comment symbol (#) before each line of comments, or you can use the "\<#" and "#>" symbols to create a comment block.</span></span> <span data-ttu-id="dae3d-109">A Megjegyzés blokkon belül a sorok megjegyzésként értelmezi.</span><span class="sxs-lookup"><span data-stu-id="dae3d-109">All the lines within the comment block are interpreted as comments.</span></span>

 <span data-ttu-id="dae3d-110">Megjegyzés-alapú súgó minden szakasza határozza meg egy kulcsszót, és minden kulcsszó előzi meg egy pontot (.).</span><span class="sxs-lookup"><span data-stu-id="dae3d-110">Each section of comment-based Help is defined by a keyword and each keyword is preceded by a dot (.).</span></span> <span data-ttu-id="dae3d-111">A kulcsszavak bármilyen sorrendben is megjelenhetnek.</span><span class="sxs-lookup"><span data-stu-id="dae3d-111">The keywords can appear in any order.</span></span> <span data-ttu-id="dae3d-112">A kulcsszó nevében a rendszer nem kis-és nagybetűket.</span><span class="sxs-lookup"><span data-stu-id="dae3d-112">The keyword names are not case-sensitive.</span></span>

 <span data-ttu-id="dae3d-113">A megjegyzésblokkot tartalmaznia kell legalább egy Súgó kulcsszót.</span><span class="sxs-lookup"><span data-stu-id="dae3d-113">A comment block must contain at least one help keyword.</span></span> <span data-ttu-id="dae3d-114">Néhány kulcsszóra, mint PÉLDÁUL az azonos megjegyzésblokkot sokszor szerepelhetnek.</span><span class="sxs-lookup"><span data-stu-id="dae3d-114">Some of the keywords, such as EXAMPLE, can appear many times in the same comment block.</span></span> <span data-ttu-id="dae3d-115">Minden kulcsszó súgója kulcsszó után a sor kezdődik, és több sort is kiterjedhetnek.</span><span class="sxs-lookup"><span data-stu-id="dae3d-115">The Help content for each keyword begins on the line after the keyword and can span multiple lines.</span></span>

 <span data-ttu-id="dae3d-116">Az összes megjegyzés-alapú súgótémakör sorok összefüggőeknek kell lenniük.</span><span class="sxs-lookup"><span data-stu-id="dae3d-116">All of the lines in a comment-based Help topic must be contiguous.</span></span> <span data-ttu-id="dae3d-117">A Megjegyzés-alapú súgó-témakör egy megjegyzés, amely nem része a Súgó-témakör követi, ha legalább egy üres sor utolsó sora nem súgó Megjegyzés és a Megjegyzés-alapú súgó kezdete közötti lehet.</span><span class="sxs-lookup"><span data-stu-id="dae3d-117">If a comment-based Help topic follows a comment that is not part of the Help topic, there must be at least one blank line between the last non-Help comment line and the beginning of the comment-based Help.</span></span>

 <span data-ttu-id="dae3d-118">Például a következő megjegyzés-alapú témakör tartalmazza a. Leírás kulcsszó és a hozzá tartozó értéket, amely egy függvény vagy parancsfájl leírása.</span><span class="sxs-lookup"><span data-stu-id="dae3d-118">For example, the following comment-based help topic contains the .Description keyword and its value, which is a description of a function or script.</span></span>

```powershell
<#
    .Description
    The Get-Function function displays the name and syntax of all functions in the session.
#>
```