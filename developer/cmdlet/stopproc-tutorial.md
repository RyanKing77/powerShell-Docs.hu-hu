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
ms.openlocfilehash: 6e1c8a4709988adfa59bda14eb3af52b0a79f1df
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56847060"
---
# <a name="stopproc-tutorial"></a><span data-ttu-id="4b192-102">StopProc-oktatóanyag</span><span class="sxs-lookup"><span data-stu-id="4b192-102">StopProc Tutorial</span></span>

<span data-ttu-id="4b192-103">Ez a szakasz tartalmazza a Stop-Proc parancsmagot, amely nagyon hasonlít a létrehozására vonatkozó oktatóanyag a [Stop-Process](/powershell/module/Microsoft.PowerShell.Management/Stop-Process) biztosítja a Windows PowerShell parancsmaggal.</span><span class="sxs-lookup"><span data-stu-id="4b192-103">This section provides a tutorial for creating the Stop-Proc cmdlet, which is very similar to the [Stop-Process](/powershell/module/Microsoft.PowerShell.Management/Stop-Process) cmdlet provided by Windows PowerShell.</span></span> <span data-ttu-id="4b192-104">Ez az oktatóanyag ismerteti, töredék mutatnak, amelyek bemutatják, hogyan parancsmagok vannak megvalósítva, és annak magyarázatát, a kódot.</span><span class="sxs-lookup"><span data-stu-id="4b192-104">This tutorial provides fragments of code that illustrate how cmdlets are implemented, and an explanation of the code.</span></span>
<span data-ttu-id="4b192-105">Ez a szakasz tartalmazza a Stop-Proc parancsmagot, amely nagyon hasonlít a létrehozására vonatkozó oktatóanyag a [Stop-Process](/powershell/module/Microsoft.PowerShell.Management/Stop-Process) biztosítja a Windows PowerShell parancsmaggal.</span><span class="sxs-lookup"><span data-stu-id="4b192-105">This section provides a tutorial for creating the Stop-Proc cmdlet, which is very similar to the [Stop-Process](/powershell/module/Microsoft.PowerShell.Management/Stop-Process) cmdlet provided by Windows PowerShell.</span></span> <span data-ttu-id="4b192-106">Ez az oktatóanyag ismerteti, töredék mutatnak, amelyek bemutatják, hogyan parancsmagok vannak megvalósítva, és annak magyarázatát, a kódot.</span><span class="sxs-lookup"><span data-stu-id="4b192-106">This tutorial provides fragments of code that illustrate how cmdlets are implemented, and an explanation of the code.</span></span>

## <a name="topics-in-this-tutorial"></a><span data-ttu-id="4b192-107">Ebben az oktatóanyagban kapcsolatos témakörök</span><span class="sxs-lookup"><span data-stu-id="4b192-107">Topics in this Tutorial</span></span>

<span data-ttu-id="4b192-108">Ebben az oktatóanyagban a témakörök a megadott sorrendben kell olvasni az egyes kialakításához a mi volt az előző témakörben tárgyalt témakörök tervezték.</span><span class="sxs-lookup"><span data-stu-id="4b192-108">The topics in this tutorial are designed to be read sequentially, with each topic building on what was discussed in the previous topic.</span></span>

<span data-ttu-id="4b192-109">[A parancsmag létrehozása, amely módosítja a rendszer](./creating-a-cmdlet-that-modifies-the-system.md) Ez a szakasz ismerteti, hogyan hozhat létre olyan parancsmagot, amely támogatja a rendszer a módosítások, például a számítógépen futó folyamat leállítása.</span><span class="sxs-lookup"><span data-stu-id="4b192-109">[Creating a Cmdlet that Modifies the System](./creating-a-cmdlet-that-modifies-the-system.md) This section describes how to create a cmdlet that supports system modifications, such as stopping a process running on the computer.</span></span>

<span data-ttu-id="4b192-110">[Felhasználói üzeneteket ad hozzá a parancsmag](./adding-user-messages-to-your-cmdlet.md) Ez a szakasz ismerteti, hogyan adhat hozzá felhasználói üzenetek, hibakeresési üzeneteket, figyelmeztető üzeneteket és állapotadatokat írni a parancsmaghoz.</span><span class="sxs-lookup"><span data-stu-id="4b192-110">[Adding User Messages to Your Cmdlet](./adding-user-messages-to-your-cmdlet.md) This section describes how to add the ability to write user messages, debug messages, warning messages, and progress information to your cmdlet.</span></span>

<span data-ttu-id="4b192-111">[Aliasok, helyettesítő bővítése, hozzáadását és parancsmag-paraméterek segítségével](./adding-aliases-wildcard-expansion-and-help-to-cmdlet-parameters.md) Ez a szakasz ismerteti, hogyan hozhat létre olyan parancsmagot, amely támogatja a paraméter-aliasok, Súgó és helyettesítő bővítése.</span><span class="sxs-lookup"><span data-stu-id="4b192-111">[Adding Aliases, Wildcard Expansion, and Help to Cmdlet Parameters](./adding-aliases-wildcard-expansion-and-help-to-cmdlet-parameters.md) This section describes how to create a cmdlet that supports parameter aliases, Help, and wildcard expansion.</span></span>

<span data-ttu-id="4b192-112">[Parancsmagok hozzáadása a paraméterkészletek](./adding-parameter-sets-to-a-cmdlet.md) Ez a szakasz ismerteti, hogyan lehet paraméter állítja be, a parancsmag hozzáadása.</span><span class="sxs-lookup"><span data-stu-id="4b192-112">[Adding Parameter Sets to Cmdlets](./adding-parameter-sets-to-a-cmdlet.md) This section describes how to add parameter sets to a cmdlet.</span></span> <span data-ttu-id="4b192-113">Paraméterkészlettel lehetővé teszik a parancsmag működését menübeállításoktól függően a felhasználó által megadott paramétereket.</span><span class="sxs-lookup"><span data-stu-id="4b192-113">Parameter sets allow the cmdlet to operate differently based on what parameters are specified by the user.</span></span>

## <a name="see-also"></a><span data-ttu-id="4b192-114">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="4b192-114">See Also</span></span>

[<span data-ttu-id="4b192-115">A parancsmag létrehozása, amely módosítja a rendszer</span><span class="sxs-lookup"><span data-stu-id="4b192-115">Creating a Cmdlet that Modifies the System</span></span>](./creating-a-cmdlet-that-modifies-the-system.md)

[<span data-ttu-id="4b192-116">Felhasználói üzenetek hozzáadása a parancsmaghoz</span><span class="sxs-lookup"><span data-stu-id="4b192-116">Adding User Messages to Your Cmdlet</span></span>](./adding-user-messages-to-your-cmdlet.md)

[<span data-ttu-id="4b192-117">Aliasok, helyettesítő bővítése, hozzáadását és parancsmag-paraméterek segítségével</span><span class="sxs-lookup"><span data-stu-id="4b192-117">Adding Aliases, Wildcard Expansion, and Help to Cmdlet Parameters</span></span>](./adding-aliases-wildcard-expansion-and-help-to-cmdlet-parameters.md)

[<span data-ttu-id="4b192-118">Beállítja a parancsmagok paraméter hozzáadása</span><span class="sxs-lookup"><span data-stu-id="4b192-118">Adding Parameter Sets to Cmdlets</span></span>](./adding-parameter-sets-to-a-cmdlet.md)

[<span data-ttu-id="4b192-119">Windows PowerShell SDK</span><span class="sxs-lookup"><span data-stu-id="4b192-119">Windows PowerShell SDK</span></span>](../windows-powershell-reference.md)
