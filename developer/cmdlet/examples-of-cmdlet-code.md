---
title: Példák a parancsmag kód |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 6fed2f68-ce6d-4a8f-bf21-f94f27a155c2
caps.latest.revision: 9
ms.openlocfilehash: 936728d64f30a08fb9e2fa9ccef103683594aa3e
ms.sourcegitcommit: caac7d098a448232304c9d6728e7340ec7517a71
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/16/2019
ms.locfileid: "58056260"
---
# <a name="examples-of-cmdlet-code"></a><span data-ttu-id="47df9-102">Példák parancsmagkódokra</span><span class="sxs-lookup"><span data-stu-id="47df9-102">Examples of Cmdlet Code</span></span>

<span data-ttu-id="47df9-103">Ez a szakasz példákat mutatnak parancsmag, amelyek segítségével írhat saját parancsmagok tartalmaz.</span><span class="sxs-lookup"><span data-stu-id="47df9-103">This section contains examples of cmdlet code that you can use to start writing your own cmdlets.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="47df9-104">Ha azt szeretné, hogy a parancsmagok írása lépésről lépésre ismerteti, lásd: [írása parancsmagok oktatóanyagok](./tutorials-for-writing-cmdlets.md).</span><span class="sxs-lookup"><span data-stu-id="47df9-104">If you want step-by-step instructions for writing cmdlets, see [Tutorials for Writing Cmdlets](./tutorials-for-writing-cmdlets.md).</span></span>

## <a name="in-this-section"></a><span data-ttu-id="47df9-105">A szakasz tartalma</span><span class="sxs-lookup"><span data-stu-id="47df9-105">In This Section</span></span>

<span data-ttu-id="47df9-106">[Hogyan írhat egy egyszerű parancsmag](./how-to-write-a-simple-cmdlet.md) ebben a példában a parancsmag kód alapvető szerkezete látható.</span><span class="sxs-lookup"><span data-stu-id="47df9-106">[How to Write a Simple Cmdlet](./how-to-write-a-simple-cmdlet.md) This example shows the basic structure of cmdlet code.</span></span>

<span data-ttu-id="47df9-107">[Parancsmag-paraméterek deklarálja hogyan](./how-to-declare-cmdlet-parameters.md) Ez a példa bemutatja, hogyan deklarálja a különböző típusú paramétereket.</span><span class="sxs-lookup"><span data-stu-id="47df9-107">[How to Declare Cmdlet Parameters](./how-to-declare-cmdlet-parameters.md) This example shows how to declare the different types of parameters.</span></span>

<span data-ttu-id="47df9-108">[Deklarálja a paraméter állítja be, hogyan](./how-to-declare-parameter-sets.md) Ez a példa bemutatja, hogyan deklarálja a csoportok paraméterek, amelyek változhatnak, a parancsmag végrehajtja a műveletet.</span><span class="sxs-lookup"><span data-stu-id="47df9-108">[How to Declare Parameter Sets](./how-to-declare-parameter-sets.md) This example shows how to declare sets of parameters that can change the action a cmdlet performs.</span></span>

<span data-ttu-id="47df9-109">[A paraméter bemeneti ellenőrzése annak](./how-to-validate-parameter-input.md) ezek a példák szemléltetik a paraméter bemeneti ellenőrzése.</span><span class="sxs-lookup"><span data-stu-id="47df9-109">[How to Validate Parameter Input](./how-to-validate-parameter-input.md) These examples show how to validate parameter input.</span></span>

<span data-ttu-id="47df9-110">[Deklarálja a dinamikus paraméterek hogyan](./how-to-declare-dynamic-parameters.md) Ez a példa bemutatja, hogyan deklarovat parametr futásidőben hozzáadott.</span><span class="sxs-lookup"><span data-stu-id="47df9-110">[How to Declare Dynamic Parameters](./how-to-declare-dynamic-parameters.md) This example shows how to declare a parameter that is added at runtime.</span></span>

<span data-ttu-id="47df9-111">[Egy parancsmag belül szkriptek Invoke hogyan](./how-to-invoke-scripts-within-a-cmdlet.md) Ez a példa bemutatja, hogyan meghívni egy parancsmaghoz megadott parancsfájlt.</span><span class="sxs-lookup"><span data-stu-id="47df9-111">[How to Invoke Scripts Within a Cmdlet](./how-to-invoke-scripts-within-a-cmdlet.md) This example shows how to invoke a script that is supplied to a cmdlet.</span></span>

<span data-ttu-id="47df9-112">[Bemeneti feldolgozási metódusok felülbírálása](./how-to-override-input-processing-methods.md) a példákból látható, felül az BeginProcessing ProcessRecord és EndProcessing módszerek alapszintű struktúrát.</span><span class="sxs-lookup"><span data-stu-id="47df9-112">[How To Override Input Processing Methods](./how-to-override-input-processing-methods.md) These examples show the basic structure used to override the BeginProcessing, ProcessRecord, and EndProcessing methods.</span></span>

<span data-ttu-id="47df9-113">[Hogyan ShouldProcess hívások](./how-to-request-confirmations.md) a példa bemutatja, hogyan a [System.Management.Automation.Cmdlet.ShouldProcess](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) és [System.Management.Automation.Cmdlet.ShouldContinue](/dotnet/api/System.Management.Automation.Cmdlet.ShouldContinue) módszerek a parancsmag belül kell megnyitni.</span><span class="sxs-lookup"><span data-stu-id="47df9-113">[How to Support ShouldProcess Calls](./how-to-request-confirmations.md) This example shows how the [System.Management.Automation.Cmdlet.ShouldProcess](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) and [System.Management.Automation.Cmdlet.ShouldContinue](/dotnet/api/System.Management.Automation.Cmdlet.ShouldContinue) methods should be called from within a cmdlet.</span></span>

<span data-ttu-id="47df9-114">[A támogatási tranzakciók hogyan](./how-to-support-transactions.md) Ez a példa bemutatja, hogyan azt jelzik, hogy a parancsmag támogatja a tranzakciókat és megvalósítása a parancsmag tranzakción belüli használata esetén végrehajtandó műveletet.</span><span class="sxs-lookup"><span data-stu-id="47df9-114">[How to Support Transactions](./how-to-support-transactions.md) This example shows how to indicate that the cmdlet supports transactions and how to implement the action that is taken when the cmdlet is used within a transaction.</span></span>

<span data-ttu-id="47df9-115">[Hogyan támogatja a feladatok](./how-to-support-jobs.md) Ez a példa bemutatja, hogyan támogatja a feladatok parancsmagok írásakor.</span><span class="sxs-lookup"><span data-stu-id="47df9-115">[How to Support Jobs](./how-to-support-jobs.md) This example shows how to support jobs when you write cmdlets.</span></span>

<span data-ttu-id="47df9-116">[A parancsmag a belül egy parancsmag meghívása hogyan](./how-to-invoke-a-cmdlet-from-within-a-cmdlet.md) Ez a példa bemutatja, hogyan belül egy másik parancsmagot, amely lehetővé teszi, hogy az a funkciók a meghívott parancsmag hozzáadása a parancsmag fejleszt, parancsmag meghívása.</span><span class="sxs-lookup"><span data-stu-id="47df9-116">[How to Invoke a Cmdlet From Within a Cmdlet](./how-to-invoke-a-cmdlet-from-within-a-cmdlet.md) This example shows how to invoke a cmdlet from within another cmdlet, which allows you to add the functionality of the invoked cmdlet to the cmdlet you are developing.</span></span>

## <a name="see-also"></a><span data-ttu-id="47df9-117">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="47df9-117">See Also</span></span>

[<span data-ttu-id="47df9-118">Egy Windows PowerShell-parancsmag írása</span><span class="sxs-lookup"><span data-stu-id="47df9-118">Writing a Windows PowerShell Cmdlet</span></span>](./writing-a-windows-powershell-cmdlet.md)
