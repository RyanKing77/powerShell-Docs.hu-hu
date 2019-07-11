---
title: Kódminta RunSpace08 |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 0f286201-8a02-4b00-9a2c-1b833ccdbdbf
caps.latest.revision: 7
ms.openlocfilehash: ec6aae544eafea1dedc1379dab00beeed2c7c436
ms.sourcegitcommit: 46bebe692689ebedfe65ff2c828fe666b443198d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/10/2019
ms.locfileid: "67734916"
---
# <a name="runspace08-code-sample"></a><span data-ttu-id="2bc82-102">Runspace08 – Kódminta</span><span class="sxs-lookup"><span data-stu-id="2bc82-102">RunSpace08 Code Sample</span></span>

<span data-ttu-id="2bc82-103">Itt van a forráskódot a Runspace08 minta ismertetett [létrehozása egy Console Application, hogy hozzáadja a parancs paraméterei](https://msdn.microsoft.com/en-us/848b2b46-60f1-4a86-b448-cfc7c0cccfba).</span><span class="sxs-lookup"><span data-stu-id="2bc82-103">Here is the source code for the Runspace08 sample described in [Creating a Console Application That Adds Parameters to a Command](https://msdn.microsoft.com/en-us/848b2b46-60f1-4a86-b448-cfc7c0cccfba).</span></span> <span data-ttu-id="2bc82-104">Ez a mintaalkalmazás egy futási teret hoz létre, létrehoz egy folyamatot, két parancsot a folyamat hozzáadja, két paramétert ad hozzá a második parancs és a folyamat végrehajtja.</span><span class="sxs-lookup"><span data-stu-id="2bc82-104">This sample application creates a runspace, creates a pipeline, adds two commands to the pipeline, adds two parameters to the second command, and then executes the pipeline.</span></span> <span data-ttu-id="2bc82-105">A folyamat hozzáadott parancsai a `Get-Process` és `Sort-Object` parancsmagok.</span><span class="sxs-lookup"><span data-stu-id="2bc82-105">The commands that are added to the pipeline are the `Get-Process` and `Sort-Object` cmdlets.</span></span>

## <a name="code-sample"></a><span data-ttu-id="2bc82-106">Kódminta</span><span class="sxs-lookup"><span data-stu-id="2bc82-106">Code Sample</span></span>

[!code-csharp[Runspace08.cs](../../powershell-sdk-samples/SDK-2.0/csharp/Runspace08/Runspace08.cs#L11-L86 "Runspace08.cs")]

## <a name="see-also"></a><span data-ttu-id="2bc82-107">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="2bc82-107">See Also</span></span>

[<span data-ttu-id="2bc82-108">Windows PowerShell SDK</span><span class="sxs-lookup"><span data-stu-id="2bc82-108">Windows PowerShell SDK</span></span>](../windows-powershell-reference.md)