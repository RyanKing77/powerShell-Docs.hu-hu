---
title: Kódminta RunSpace09 |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 136e451f-767b-42e0-bd6f-6486693abd5e
caps.latest.revision: 6
ms.openlocfilehash: e21ef8685598db9a1ae0fcd86051386af526f2a5
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62081223"
---
# <a name="runspace09-code-sample"></a><span data-ttu-id="5d704-102">Runspace09 – Kódminta</span><span class="sxs-lookup"><span data-stu-id="5d704-102">RunSpace09 Code Sample</span></span>

<span data-ttu-id="5d704-103">Itt van a forráskódot a Runspace09 minta ismertetett [egy Console Application, hogy meghívja a folyamat aszinkron módon létrehozása](http://msdn.microsoft.com/en-us/198c1c94-2a06-457e-93ce-c0d910618e47).</span><span class="sxs-lookup"><span data-stu-id="5d704-103">Here is the source code for the Runspace09 sample described in [Creating a Console Application That Invokes a Pipeline Asynchronously](http://msdn.microsoft.com/en-us/198c1c94-2a06-457e-93ce-c0d910618e47).</span></span> <span data-ttu-id="5d704-104">Ez a mintaalkalmazás hoz létre, és megnyílik egy futási teret, létrehozása és aszinkron módon hív meg egy folyamatot, és ezután használt folyamat-események a parancsfájl műveletek aszinkron feldolgozásához.</span><span class="sxs-lookup"><span data-stu-id="5d704-104">This sample application creates and opens a runspace, creates and asynchronously invokes a pipeline, and then uses pipeline events to process the script asynchronously.</span></span> <span data-ttu-id="5d704-105">A jelen alkalmazás által futtatott parancsfájl 0,5 másodperces időközönként (500 ms) hoz létre az egész számok 1 és 10 közötti.</span><span class="sxs-lookup"><span data-stu-id="5d704-105">The script that is run by this application creates the integers 1 through 10 in 0.5-second intervals (500 ms).</span></span>

## <a name="code-sample"></a><span data-ttu-id="5d704-106">Kódminta</span><span class="sxs-lookup"><span data-stu-id="5d704-106">Code Sample</span></span>

[!code-csharp[Runspace09.cs](../../powershell-sdk-samples/SDK-2.0/csharp/Runspace09/Runspace09.cs#L11-L113 "Runspace09.cs")]

## <a name="see-also"></a><span data-ttu-id="5d704-107">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="5d704-107">See Also</span></span>

[<span data-ttu-id="5d704-108">Windows PowerShell SDK</span><span class="sxs-lookup"><span data-stu-id="5d704-108">Windows PowerShell SDK</span></span>](../windows-powershell-reference.md)