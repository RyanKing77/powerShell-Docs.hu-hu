---
title: Kódminta RunSpace07 |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 8ad306d9-45c2-4d55-8e64-fdcba43402c5
caps.latest.revision: 6
ms.openlocfilehash: 064e7d7ea2ee173bbcdd75a9f3a6c12582afe17b
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62081291"
---
# <a name="runspace07-code-sample"></a><span data-ttu-id="159f8-102">Runspace07 – Kódminta</span><span class="sxs-lookup"><span data-stu-id="159f8-102">RunSpace07 Code Sample</span></span>

<span data-ttu-id="159f8-103">Itt van a forráskódot a Runspace07 minta ismertetett [egy alkalmazást, hogy hozzáadja konzolparancsok egy folyamat létrehozása](http://msdn.microsoft.com/en-us/01eb7808-e97b-4905-80be-9e2fa38c262e).</span><span class="sxs-lookup"><span data-stu-id="159f8-103">Here is the source code for the Runspace07 sample described in [Creating a Console Application That Adds Commands to a Pipeline](http://msdn.microsoft.com/en-us/01eb7808-e97b-4905-80be-9e2fa38c262e).</span></span> <span data-ttu-id="159f8-104">Ez a mintaalkalmazás egy futási teret hoz létre, létrehoz egy folyamatot, két parancsot ad hozzá a folyamat és a folyamat végrehajtja.</span><span class="sxs-lookup"><span data-stu-id="159f8-104">This sample application creates a runspace, creates a pipeline, adds two commands to the pipeline, and then executes the pipeline.</span></span> <span data-ttu-id="159f8-105">A folyamat hozzáadott parancsai a `Get-Process` és `Measure-Object` parancsmagok.</span><span class="sxs-lookup"><span data-stu-id="159f8-105">The commands added to the pipeline are the `Get-Process` and `Measure-Object` cmdlets.</span></span>

> [!NOTE]
> <span data-ttu-id="159f8-106">Letöltheti a C# forrásfájl (runspace07.cs) a Microsoft Windows szoftverek fejlesztési Kit for Windows Vista és a Microsoft .NET Framework 3.0 futtatási összetevői.</span><span class="sxs-lookup"><span data-stu-id="159f8-106">You can download the C# source file (runspace07.cs) using the Microsoft Windows Software Development Kit for Windows Vista and Microsoft .NET Framework 3.0 Runtime Components.</span></span> <span data-ttu-id="159f8-107">Letöltési útmutatás: [Windows PowerShell telepítése és a Windows PowerShell SDK letöltési](/powershell/developer/installing-the-windows-powershell-sdk).</span><span class="sxs-lookup"><span data-stu-id="159f8-107">For download instructions, see [How to Install Windows PowerShell and Download the Windows PowerShell SDK](/powershell/developer/installing-the-windows-powershell-sdk).</span></span>
>
> <span data-ttu-id="159f8-108">A letöltött forrásfájlok érhetők el a  **\<PowerShell-minták >** könyvtár.</span><span class="sxs-lookup"><span data-stu-id="159f8-108">The downloaded source files are available in the **\<PowerShell Samples>** directory.</span></span>

## <a name="code-sample"></a><span data-ttu-id="159f8-109">Kódminta</span><span class="sxs-lookup"><span data-stu-id="159f8-109">Code Sample</span></span>

[!code-csharp[Runspace07.cs](../../powershell-sdk-samples/SDK-2.0/csharp/Runspace07/Runspace07.cs#L11-L108 "Runspace07.cs")]

## <a name="see-also"></a><span data-ttu-id="159f8-110">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="159f8-110">See Also</span></span>

[<span data-ttu-id="159f8-111">Windows PowerShell programozói útmutató</span><span class="sxs-lookup"><span data-stu-id="159f8-111">Windows PowerShell Programmer's Guide</span></span>](./windows-powershell-programmer-s-guide.md)

[<span data-ttu-id="159f8-112">Windows PowerShell SDK</span><span class="sxs-lookup"><span data-stu-id="159f8-112">Windows PowerShell SDK</span></span>](../windows-powershell-reference.md)