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
ms.openlocfilehash: b6fdad90f7339e941d77646936b1b5952cd65500
ms.sourcegitcommit: 46bebe692689ebedfe65ff2c828fe666b443198d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/10/2019
ms.locfileid: "67734931"
---
# <a name="runspace06-code-sample"></a><span data-ttu-id="fca96-102">Runspace06 – Kódminta</span><span class="sxs-lookup"><span data-stu-id="fca96-102">RunSpace06 Code Sample</span></span>

<span data-ttu-id="fca96-103">Itt van a forráskódot a Runspace06 minta ismertetett [konfigurálása egy futási teret egy Windows PowerShell beépülő modullal](https://msdn.microsoft.com/en-us/a7289ee8-9732-49ee-91c7-d533e9538b83).</span><span class="sxs-lookup"><span data-stu-id="fca96-103">Here is the source code for the Runspace06 sample described in [Configuring a Runspace Using a Windows PowerShell Snap-in](https://msdn.microsoft.com/en-us/a7289ee8-9732-49ee-91c7-d533e9538b83).</span></span> <span data-ttu-id="fca96-104">Ez a mintaalkalmazás egy futási teret egy Windows PowerShell beépülő modul, amely majd használható egy folyamat futtatása egyetlen paranccsal alapján hoz létre.</span><span class="sxs-lookup"><span data-stu-id="fca96-104">This sample application creates a runspace based on a Windows PowerShell snap-in, which is then used to run a pipeline with a single command.</span></span> <span data-ttu-id="fca96-105">Ehhez az alkalmazás a futási térben konfigurációs adatokat hoz létre, létrehoz egy futási teret, létrehoz egy folyamatot egyetlen paranccsal és a folyamat végrehajtja.</span><span class="sxs-lookup"><span data-stu-id="fca96-105">To do this, the application creates the runspace configuration information, creates a runspace, creates a pipeline with a single command, and then executes the pipeline.</span></span>

> [!NOTE]
> <span data-ttu-id="fca96-106">Letöltheti a C# forrásfájl (runspace06.cs) a Windows szoftverek fejlesztési Kit for Windows Vista és a Microsoft .NET Framework 3.0 futtatási összetevői.</span><span class="sxs-lookup"><span data-stu-id="fca96-106">You can download the C# source file (runspace06.cs) by using the Windows Software Development Kit for Windows Vista and Microsoft .NET Framework 3.0 Runtime Components.</span></span> <span data-ttu-id="fca96-107">Letöltési útmutatás: [Windows PowerShell telepítése és a Windows PowerShell SDK letöltési](/powershell/developer/installing-the-windows-powershell-sdk).</span><span class="sxs-lookup"><span data-stu-id="fca96-107">For download instructions, see [How to Install Windows PowerShell and Download the Windows PowerShell SDK](/powershell/developer/installing-the-windows-powershell-sdk).</span></span>
>
> <span data-ttu-id="fca96-108">A letöltött forrásfájlok érhetők el a  **\<PowerShell-minták >** könyvtár.</span><span class="sxs-lookup"><span data-stu-id="fca96-108">The downloaded source files are available in the **\<PowerShell Samples>** directory.</span></span>

## <a name="code-sample"></a><span data-ttu-id="fca96-109">Kódminta</span><span class="sxs-lookup"><span data-stu-id="fca96-109">Code Sample</span></span>

[!code-csharp[Runspace06.cs](../../powershell-sdk-samples/SDK-2.0/csharp/Runspace06/Runspace06.cs#L11-L85 "Runspace06.cs")]

## <a name="see-also"></a><span data-ttu-id="fca96-110">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="fca96-110">See Also</span></span>

[<span data-ttu-id="fca96-111">Windows PowerShell programozói útmutató</span><span class="sxs-lookup"><span data-stu-id="fca96-111">Windows PowerShell Programmer's Guide</span></span>](./windows-powershell-programmer-s-guide.md)

[<span data-ttu-id="fca96-112">Windows PowerShell SDK</span><span class="sxs-lookup"><span data-stu-id="fca96-112">Windows PowerShell SDK</span></span>](../windows-powershell-reference.md)