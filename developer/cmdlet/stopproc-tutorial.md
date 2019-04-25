---
title: Az oktatóanyag StopProc |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: a142aeb6-9c11-44a0-b34f-1f9470fa347b
caps.latest.revision: 5
ms.openlocfilehash: 27c8e2c7525aba38e69e50b2b7fd3b18b8e54989
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62067311"
---
# <a name="stopproc-tutorial"></a><span data-ttu-id="5a436-102">StopProc-oktatóanyag</span><span class="sxs-lookup"><span data-stu-id="5a436-102">StopProc Tutorial</span></span>

<span data-ttu-id="5a436-103">Ez a szakasz tartalmazza a Stop-Proc parancsmagot, amely nagyon hasonlít a létrehozására vonatkozó oktatóanyag a [Stop-Process](/powershell/module/Microsoft.PowerShell.Management/Stop-Process) biztosítja a Windows PowerShell parancsmaggal.</span><span class="sxs-lookup"><span data-stu-id="5a436-103">This section provides a tutorial for creating the Stop-Proc cmdlet, which is very similar to the [Stop-Process](/powershell/module/Microsoft.PowerShell.Management/Stop-Process) cmdlet provided by Windows PowerShell.</span></span> <span data-ttu-id="5a436-104">Ez az oktatóanyag ismerteti, töredék mutatnak, amelyek bemutatják, hogyan parancsmagok vannak megvalósítva, és annak magyarázatát, a kódot.</span><span class="sxs-lookup"><span data-stu-id="5a436-104">This tutorial provides fragments of code that illustrate how cmdlets are implemented, and an explanation of the code.</span></span>

## <a name="topics-in-this-tutorial"></a><span data-ttu-id="5a436-105">Ebben az oktatóanyagban kapcsolatos témakörök</span><span class="sxs-lookup"><span data-stu-id="5a436-105">Topics in this Tutorial</span></span>

<span data-ttu-id="5a436-106">Ebben az oktatóanyagban a témakörök a megadott sorrendben kell olvasni az egyes kialakításához a mi volt az előző témakörben tárgyalt témakörök tervezték.</span><span class="sxs-lookup"><span data-stu-id="5a436-106">The topics in this tutorial are designed to be read sequentially, with each topic building on what was discussed in the previous topic.</span></span>

<span data-ttu-id="5a436-107">[A parancsmag létrehozása, amely módosítja a rendszer](./creating-a-cmdlet-that-modifies-the-system.md) Ez a szakasz ismerteti, hogyan hozhat létre olyan parancsmagot, amely támogatja a rendszer a módosítások, például a számítógépen futó folyamat leállítása.</span><span class="sxs-lookup"><span data-stu-id="5a436-107">[Creating a Cmdlet that Modifies the System](./creating-a-cmdlet-that-modifies-the-system.md) This section describes how to create a cmdlet that supports system modifications, such as stopping a process running on the computer.</span></span>

<span data-ttu-id="5a436-108">[Felhasználói üzeneteket ad hozzá a parancsmag](./adding-user-messages-to-your-cmdlet.md) Ez a szakasz ismerteti, hogyan adhat hozzá felhasználói üzenetek, hibakeresési üzeneteket, figyelmeztető üzeneteket és állapotadatokat írni a parancsmaghoz.</span><span class="sxs-lookup"><span data-stu-id="5a436-108">[Adding User Messages to Your Cmdlet](./adding-user-messages-to-your-cmdlet.md) This section describes how to add the ability to write user messages, debug messages, warning messages, and progress information to your cmdlet.</span></span>

<span data-ttu-id="5a436-109">[Aliasok, helyettesítő bővítése, hozzáadását és parancsmag-paraméterek segítségével](./adding-aliases-wildcard-expansion-and-help-to-cmdlet-parameters.md) Ez a szakasz ismerteti, hogyan hozhat létre olyan parancsmagot, amely támogatja a paraméter-aliasok, Súgó és helyettesítő bővítése.</span><span class="sxs-lookup"><span data-stu-id="5a436-109">[Adding Aliases, Wildcard Expansion, and Help to Cmdlet Parameters](./adding-aliases-wildcard-expansion-and-help-to-cmdlet-parameters.md) This section describes how to create a cmdlet that supports parameter aliases, Help, and wildcard expansion.</span></span>

<span data-ttu-id="5a436-110">[Parancsmagok hozzáadása a paraméterkészletek](./adding-parameter-sets-to-a-cmdlet.md) Ez a szakasz ismerteti, hogyan lehet paraméter állítja be, a parancsmag hozzáadása.</span><span class="sxs-lookup"><span data-stu-id="5a436-110">[Adding Parameter Sets to Cmdlets](./adding-parameter-sets-to-a-cmdlet.md) This section describes how to add parameter sets to a cmdlet.</span></span> <span data-ttu-id="5a436-111">Paraméterkészlettel lehetővé teszik a parancsmag működését menübeállításoktól függően a felhasználó által megadott paramétereket.</span><span class="sxs-lookup"><span data-stu-id="5a436-111">Parameter sets allow the cmdlet to operate differently based on what parameters are specified by the user.</span></span>

## <a name="see-also"></a><span data-ttu-id="5a436-112">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="5a436-112">See Also</span></span>

[<span data-ttu-id="5a436-113">A parancsmag létrehozása, amely módosítja a rendszer</span><span class="sxs-lookup"><span data-stu-id="5a436-113">Creating a Cmdlet that Modifies the System</span></span>](./creating-a-cmdlet-that-modifies-the-system.md)

[<span data-ttu-id="5a436-114">Felhasználói üzenetek hozzáadása a parancsmaghoz</span><span class="sxs-lookup"><span data-stu-id="5a436-114">Adding User Messages to Your Cmdlet</span></span>](./adding-user-messages-to-your-cmdlet.md)

[<span data-ttu-id="5a436-115">Aliasok, helyettesítő bővítése, hozzáadását és parancsmag-paraméterek segítségével</span><span class="sxs-lookup"><span data-stu-id="5a436-115">Adding Aliases, Wildcard Expansion, and Help to Cmdlet Parameters</span></span>](./adding-aliases-wildcard-expansion-and-help-to-cmdlet-parameters.md)

[<span data-ttu-id="5a436-116">Beállítja a parancsmagok paraméter hozzáadása</span><span class="sxs-lookup"><span data-stu-id="5a436-116">Adding Parameter Sets to Cmdlets</span></span>](./adding-parameter-sets-to-a-cmdlet.md)

[<span data-ttu-id="5a436-117">Windows PowerShell SDK</span><span class="sxs-lookup"><span data-stu-id="5a436-117">Windows PowerShell SDK</span></span>](../windows-powershell-reference.md)
