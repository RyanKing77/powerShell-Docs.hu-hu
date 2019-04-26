---
title: Az oktatóanyag GetProc |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 4663905f-560a-4e39-9b03-6db2c315c322
caps.latest.revision: 6
ms.openlocfilehash: bbd07a0d0abd30742b7e02482adedae3af43aca4
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62068096"
---
# <a name="getproc-tutorial"></a><span data-ttu-id="4e006-102">GetProc-oktatóanyag</span><span class="sxs-lookup"><span data-stu-id="4e006-102">GetProc Tutorial</span></span>

<span data-ttu-id="4e006-103">Ez a szakasz tartalmazza az oktatóanyagot, a Get-Proc parancsmag létrehozása, amely nagyon hasonlít a [Get-Process](/powershell/module/Microsoft.PowerShell.Management/Get-Process) biztosítja a Windows PowerShell parancsmaggal.</span><span class="sxs-lookup"><span data-stu-id="4e006-103">This section provides a tutorial for creating a Get-Proc cmdlet that is very similar to the [Get-Process](/powershell/module/Microsoft.PowerShell.Management/Get-Process) cmdlet provided by Windows PowerShell.</span></span> <span data-ttu-id="4e006-104">Ez az oktatóanyag ismerteti, töredék mutatnak, amelyek bemutatják, hogyan parancsmagok vannak megvalósítva, és annak magyarázatát, a kódot.</span><span class="sxs-lookup"><span data-stu-id="4e006-104">This tutorial provides fragments of code that illustrate how cmdlets are implemented, and an explanation of the code.</span></span>

## <a name="topics-in-this-tutorial"></a><span data-ttu-id="4e006-105">Ebben az oktatóanyagban kapcsolatos témakörök</span><span class="sxs-lookup"><span data-stu-id="4e006-105">Topics in this Tutorial</span></span>

<span data-ttu-id="4e006-106">Ebben az oktatóanyagban a témakörök a megadott sorrendben kell olvasni az egyes kialakításához a mi volt az előző témakörben tárgyalt témakörök tervezték.</span><span class="sxs-lookup"><span data-stu-id="4e006-106">The topics in this tutorial are designed to be read sequentially, with each topic building on what was discussed in the previous topic.</span></span>

<span data-ttu-id="4e006-107">[Paraméterek nélkül a parancsmag létrehozása](./creating-a-cmdlet-without-parameters.md) Ez a szakasz ismerteti, hogyan hozhat létre olyan parancsmagot, amely adatait kérdezi le a helyi számítógépen, a paraméterek nélkül, és a folyamat ezután beírja az információkat.</span><span class="sxs-lookup"><span data-stu-id="4e006-107">[Creating a Cmdlet without Parameters](./creating-a-cmdlet-without-parameters.md) This section describes how to create a cmdlet that retrieves information from the local computer without the use of parameters, and then writes the information to the pipeline.</span></span>

<span data-ttu-id="4e006-108">[A folyamat parancssori bemeneti paramétereket adunk hozzá](./adding-parameters-that-process-command-line-input.md) Ez a szakasz ismerteti, hogy a parancsmag képes feldolgozni a parancsmagnak átadott explicit objektumokat alapján bemeneti paraméter hozzáadása a Get-Proc parancsmag.</span><span class="sxs-lookup"><span data-stu-id="4e006-108">[Adding Parameters that Process Command-Line Input](./adding-parameters-that-process-command-line-input.md) This section describes how to add a parameter to the Get-Proc cmdlet so that the cmdlet can process input based on explicit objects passed to the cmdlet.</span></span> <span data-ttu-id="4e006-109">Leírt végrehajtása itt lekéri a nevük alapján folyamatokat, és ezután beírja az információkat a folyamat.</span><span class="sxs-lookup"><span data-stu-id="4e006-109">The implementation described here retrieves processes based on their name, and then writes the information to the pipeline.</span></span>

<span data-ttu-id="4e006-110">[A folyamat folyamat bemeneti paramétereket adunk hozzá](./adding-parameters-that-process-pipeline-input.md) Ez a szakasz ismerteti, hogyan lehet egy paraméter hozzáadása a Get-Proc parancsmagot úgy, hogy a parancsmagnak átadni az folyamat objektumok tud feldolgozni.</span><span class="sxs-lookup"><span data-stu-id="4e006-110">[Adding Parameters that Process Pipeline Input](./adding-parameters-that-process-pipeline-input.md) This section describes how to add a parameter to the Get-Proc cmdlet so that the cmdlet can process objects passed to it through the pipeline.</span></span> <span data-ttu-id="4e006-111">Az ismertetett megvalósítási parancsmag itt lekérdezi az objektumot a parancsmagnak átadott alapuló folyamatok, és a folyamat ezután beírja az információkat.</span><span class="sxs-lookup"><span data-stu-id="4e006-111">The implementation cmdlet described here retrieves processes based on objects passed to the cmdlet, and then writes the information to the pipeline.</span></span>

<span data-ttu-id="4e006-112">[A parancsmag Nonterminating hibajelentés hozzáadása](./adding-non-terminating-error-reporting-to-your-cmdlet.md) Ez a szakasz ismerteti a parancsmag nonterminating hibajelentési hozzáadása.</span><span class="sxs-lookup"><span data-stu-id="4e006-112">[Adding Nonterminating Error Reporting to Your Cmdlet](./adding-non-terminating-error-reporting-to-your-cmdlet.md) This section describes how to add nonterminating error reporting to a cmdlet.</span></span> <span data-ttu-id="4e006-113">Az itt ismertetett megvalósítási észleli a bemeneti feldolgozásakor fordulhat elő, és a egy hiba rekordot ír a hibafolyam nonterminating hibákat.</span><span class="sxs-lookup"><span data-stu-id="4e006-113">The implementation described here detects nonterminating errors that occur when processing input, and writes an error record to the error stream.</span></span>

## <a name="see-also"></a><span data-ttu-id="4e006-114">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="4e006-114">See Also</span></span>

[<span data-ttu-id="4e006-115">Paraméterek nélkül a parancsmag létrehozása</span><span class="sxs-lookup"><span data-stu-id="4e006-115">Creating a Cmdlet without Parameters</span></span>](./creating-a-cmdlet-without-parameters.md)

[<span data-ttu-id="4e006-116">Parancssori bemenet feldolgozása paraméterek hozzáadása</span><span class="sxs-lookup"><span data-stu-id="4e006-116">Adding Parameters that Process Command-Line Input</span></span>](./adding-parameters-that-process-command-line-input.md)

[<span data-ttu-id="4e006-117">Folyamat folyamat bemeneti paraméterek hozzáadása</span><span class="sxs-lookup"><span data-stu-id="4e006-117">Adding Parameters that Process Pipeline Input</span></span>](./adding-parameters-that-process-pipeline-input.md)

[<span data-ttu-id="4e006-118">A parancsmaghoz Nonterminating hibajelentési hozzáadása</span><span class="sxs-lookup"><span data-stu-id="4e006-118">Adding Nonterminating Error Reporting to Your Cmdlet</span></span>](./adding-non-terminating-error-reporting-to-your-cmdlet.md)

[<span data-ttu-id="4e006-119">Windows PowerShell SDK</span><span class="sxs-lookup"><span data-stu-id="4e006-119">Windows PowerShell SDK</span></span>](../windows-powershell-reference.md)
