---
title: Oktatóanyagok a parancsmagok írására |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: d0b548aa-febf-45dd-bf71-2077730b9b73
caps.latest.revision: 6
ms.openlocfilehash: 767b392bd1603e83d80bad5b3fd9cb42ff142ce6
ms.sourcegitcommit: 10c347a8c3dcbf8962295601834f5ba85342a87b
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/07/2019
ms.locfileid: "56852135"
---
# <a name="tutorials-for-writing-cmdlets"></a><span data-ttu-id="93fba-102">Parancsmagok írása – oktatóanyagok</span><span class="sxs-lookup"><span data-stu-id="93fba-102">Tutorials for Writing Cmdlets</span></span>

<span data-ttu-id="93fba-103">Ez a szakasz tartalmazza kapcsolatos parancsmagok írása.</span><span class="sxs-lookup"><span data-stu-id="93fba-103">This section contains tutorials for writing cmdlets.</span></span> <span data-ttu-id="93fba-104">Ezekben az oktatóanyagokban közé tartozik a parancsmagok, és annak magyarázatát, hogy miért van szükség a kód írása szükséges kódot.</span><span class="sxs-lookup"><span data-stu-id="93fba-104">These tutorials include the code needed to write the cmdlets, plus an explanation of why the code is needed.</span></span> <span data-ttu-id="93fba-105">Ezek a témakörök azok számára, akik most használja először írása parancsmagok nagyon hasznos lesz.</span><span class="sxs-lookup"><span data-stu-id="93fba-105">These topics will be very helpful for those who are just starting to write cmdlets.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="93fba-106">Azok számára, akik hitelesítésikód-példák a kisebb leírással kívánja, tekintse meg a [parancsmag minták](./cmdlet-samples.md).</span><span class="sxs-lookup"><span data-stu-id="93fba-106">For those who want code examples with less description, see [Cmdlet Samples](./cmdlet-samples.md).</span></span>

## <a name="in-this-section"></a><span data-ttu-id="93fba-107">A szakasz tartalma</span><span class="sxs-lookup"><span data-stu-id="93fba-107">In This Section</span></span>

<span data-ttu-id="93fba-108">[Az oktatóanyag GetProc](./getproc-tutorial.md) – Ez az oktatóanyag ismerteti, hogyan lehet egy parancsmag osztály meghatározását és hozzáadását alapvető funkciókat, például-paramétereket adunk hozzá, és hibát jelentett.</span><span class="sxs-lookup"><span data-stu-id="93fba-108">[GetProc Tutorial](./getproc-tutorial.md) - This tutorial describes how to define a cmdlet class and add basic functionality such as adding parameters and reporting errors.</span></span> <span data-ttu-id="93fba-109">A parancsmag ebben az oktatóanyagban ismertetett nagyon hasonlít a [Get-Process](/powershell/module/Microsoft.PowerShell.Management/Get-Process) biztosítja a Windows PowerShell parancsmaggal.</span><span class="sxs-lookup"><span data-stu-id="93fba-109">The cmdlet described in this tutorial is very similar to the [Get-Process](/powershell/module/Microsoft.PowerShell.Management/Get-Process) cmdlet provided by Windows PowerShell.</span></span>

<span data-ttu-id="93fba-110">[Az oktatóanyag StopProc](./stopproc-tutorial.md) – Ez az oktatóanyag bemutatja, hogyan határozza meg a parancsmag, és adja hozzá a Funkciók, például a felhasználói utasításokat, helyettesítő karakterek használatát, és beállítja a paraméter használatát.</span><span class="sxs-lookup"><span data-stu-id="93fba-110">[StopProc Tutorial](./stopproc-tutorial.md) - This tutorial describes how to define a cmdlet and add functionality such as user prompts, wildcard support, and the use of parameter sets.</span></span> <span data-ttu-id="93fba-111">Az itt leírtak szerint a parancsmag végrehajtja ugyanazt a feladatot, mint a [Stop-Process](/powershell/module/Microsoft.PowerShell.Management/Stop-Process) biztosítja a Windows PowerShell parancsmaggal.</span><span class="sxs-lookup"><span data-stu-id="93fba-111">The cmdlet described here performs the same task as the [Stop-Process](/powershell/module/Microsoft.PowerShell.Management/Stop-Process) cmdlet provided by Windows PowerShell.</span></span>

<span data-ttu-id="93fba-112">[Az oktatóanyag SelectStr](./selectstr-tutorial.md) – Ez az oktatóanyag bemutatja, hogyan határozza meg, amely hozzáfér az adattár parancsmag.</span><span class="sxs-lookup"><span data-stu-id="93fba-112">[SelectStr Tutorial](./selectstr-tutorial.md) - This tutorial describes how to define a cmdlet that accesses a data store.</span></span> <span data-ttu-id="93fba-113">Az itt leírtak szerint a parancsmag végrehajtja ugyanazt a feladatot, mint a [Select-karakterlánc](/powershell/module/microsoft.powershell.utility/select-string) biztosítja a Windows PowerShell parancsmaggal.</span><span class="sxs-lookup"><span data-stu-id="93fba-113">The cmdlet described here performs the same task as the [Select-String](/powershell/module/microsoft.powershell.utility/select-string) cmdlet provided by Windows PowerShell.</span></span>

## <a name="see-also"></a><span data-ttu-id="93fba-114">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="93fba-114">See Also</span></span>

[<span data-ttu-id="93fba-115">GetProc oktatóanyag</span><span class="sxs-lookup"><span data-stu-id="93fba-115">GetProc Tutorial</span></span>](./getproc-tutorial.md)

[<span data-ttu-id="93fba-116">StopProc oktatóanyag</span><span class="sxs-lookup"><span data-stu-id="93fba-116">StopProc Tutorial</span></span>](./stopproc-tutorial.md)

[<span data-ttu-id="93fba-117">SelectStr oktatóanyag</span><span class="sxs-lookup"><span data-stu-id="93fba-117">SelectStr Tutorial</span></span>](./selectstr-tutorial.md)

[<span data-ttu-id="93fba-118">Windows PowerShell SDK</span><span class="sxs-lookup"><span data-stu-id="93fba-118">Windows PowerShell SDK</span></span>](../windows-powershell-reference.md)
