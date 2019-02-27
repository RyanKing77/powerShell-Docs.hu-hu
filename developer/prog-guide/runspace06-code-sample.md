---
title: Kódminta RunSpace06 |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: d71f86d5-eb62-4b16-aa95-5fd3f314ffd3
caps.latest.revision: 6
ms.openlocfilehash: 2874f9df3f5166fbe14deb5b128674540c0d6701
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56845436"
---
# <a name="runspace06-code-sample"></a><span data-ttu-id="59b93-102">Runspace06 – Kódminta</span><span class="sxs-lookup"><span data-stu-id="59b93-102">RunSpace06 Code Sample</span></span>

<span data-ttu-id="59b93-103">Itt van a forráskódot a Runspace06 minta ismertetett [konfigurálása egy futási teret egy Windows PowerShell beépülő modullal](http://msdn.microsoft.com/en-us/a7289ee8-9732-49ee-91c7-d533e9538b83).</span><span class="sxs-lookup"><span data-stu-id="59b93-103">Here is the source code for the Runspace06 sample described in [Configuring a Runspace Using a Windows PowerShell Snap-in](http://msdn.microsoft.com/en-us/a7289ee8-9732-49ee-91c7-d533e9538b83).</span></span> <span data-ttu-id="59b93-104">Ez a mintaalkalmazás egy futási teret egy Windows PowerShell beépülő modul, amely majd használható egy folyamat futtatása egyetlen paranccsal alapján hoz létre.</span><span class="sxs-lookup"><span data-stu-id="59b93-104">This sample application creates a runspace based on a Windows PowerShell snap-in, which is then used to run a pipeline with a single command.</span></span> <span data-ttu-id="59b93-105">Ehhez az alkalmazás a futási térben konfigurációs adatokat hoz létre, létrehoz egy futási teret, létrehoz egy folyamatot egyetlen paranccsal és a folyamat végrehajtja.</span><span class="sxs-lookup"><span data-stu-id="59b93-105">To do this, the application creates the runspace configuration information, creates a runspace, creates a pipeline with a single command, and then executes the pipeline.</span></span>

> [!NOTE]
> <span data-ttu-id="59b93-106">Letöltheti a C# forrásfájl (runspace06.cs) a Windows szoftverek fejlesztési Kit for Windows Vista és a Microsoft .NET Framework 3.0 futtatási összetevői.</span><span class="sxs-lookup"><span data-stu-id="59b93-106">You can download the C# source file (runspace06.cs) by using the Windows Software Development Kit for Windows Vista and Microsoft .NET Framework 3.0 Runtime Components.</span></span> <span data-ttu-id="59b93-107">Letöltési útmutatás: [Windows PowerShell telepítése és a Windows PowerShell SDK letöltési](/powershell/developer/installing-the-windows-powershell-sdk).</span><span class="sxs-lookup"><span data-stu-id="59b93-107">For download instructions, see [How to Install Windows PowerShell and Download the Windows PowerShell SDK](/powershell/developer/installing-the-windows-powershell-sdk).</span></span>
> <span data-ttu-id="59b93-108">Letöltheti a C# forrásfájl (runspace06.cs) a Windows szoftverek fejlesztési Kit for Windows Vista és a Microsoft .NET Framework 3.0 futtatási összetevői.</span><span class="sxs-lookup"><span data-stu-id="59b93-108">You can download the C# source file (runspace06.cs) by using the Windows Software Development Kit for Windows Vista and Microsoft .NET Framework 3.0 Runtime Components.</span></span> <span data-ttu-id="59b93-109">Letöltési útmutatás: [Windows PowerShell telepítése és a Windows PowerShell SDK letöltési](/powershell/developer/installing-the-windows-powershell-sdk).</span><span class="sxs-lookup"><span data-stu-id="59b93-109">For download instructions, see [How to Install Windows PowerShell and Download the Windows PowerShell SDK](/powershell/developer/installing-the-windows-powershell-sdk).</span></span>
>
> <span data-ttu-id="59b93-110">A letöltött forrásfájlok érhetők el a  **\<PowerShell-minták >** könyvtár.</span><span class="sxs-lookup"><span data-stu-id="59b93-110">The downloaded source files are available in the **\<PowerShell Samples>** directory.</span></span>

## <a name="code-sample"></a><span data-ttu-id="59b93-111">Kódminta</span><span class="sxs-lookup"><span data-stu-id="59b93-111">Code Sample</span></span>

[!code-csharp[Runspace06.cs](../../powershell-sdk-samples/SDK-2.0/csharp/Runspace06/Runspace06.cs#L11-L85 "Runspace06.cs")]

## <a name="see-also"></a><span data-ttu-id="59b93-112">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="59b93-112">See Also</span></span>

[<span data-ttu-id="59b93-113">Windows PowerShell programozói útmutató</span><span class="sxs-lookup"><span data-stu-id="59b93-113">Windows PowerShell Programmer's Guide</span></span>](./windows-powershell-programmer-s-guide.md)

[<span data-ttu-id="59b93-114">Windows PowerShell SDK</span><span class="sxs-lookup"><span data-stu-id="59b93-114">Windows PowerShell SDK</span></span>](../windows-powershell-reference.md)