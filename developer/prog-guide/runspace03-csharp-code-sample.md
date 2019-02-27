---
title: RunSpace03 (C#) kódminta |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 9ac8ab99-1856-4d6f-b30d-c0a18b8dd1fc
caps.latest.revision: 6
ms.openlocfilehash: d2e5b8c0a7622481bfca21d5c5b46afa01c02d2c
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56852079"
---
# <a name="runspace03-c-code-sample"></a><span data-ttu-id="4cca3-102">Runspace03 (C#) – Kódminta</span><span class="sxs-lookup"><span data-stu-id="4cca3-102">RunSpace03 (C#) Code Sample</span></span>

<span data-ttu-id="4cca3-103">Íme a C# forráskódját el a konzolalkalmazást ismertetett [létrehozása egy Console Application, hogy fut a megadott parancsfájl](http://msdn.microsoft.com/en-us/a93e6006-36db-4bcc-b9da-c5bebf4ffd68).</span><span class="sxs-lookup"><span data-stu-id="4cca3-103">Here is the C# source code for the console application described in [Creating a Console Application That Runs a Specified Script](http://msdn.microsoft.com/en-us/a93e6006-36db-4bcc-b9da-c5bebf4ffd68).</span></span> <span data-ttu-id="4cca3-104">Ebben a példában a [System.Management.Automation.Runspaceinvoke](/dotnet/api/System.Management.Automation.RunspaceInvoke) osztály végrehajtani egy parancsfájlt, amely lekéri a szkriptbe folyamat Névlista használatával dolgozza fel adatokat.</span><span class="sxs-lookup"><span data-stu-id="4cca3-104">This sample uses the [System.Management.Automation.Runspaceinvoke](/dotnet/api/System.Management.Automation.RunspaceInvoke) class to execute a script that retrieves process information by using the list of process names passed into the script.</span></span> <span data-ttu-id="4cca3-105">Bemutatja, hogyan adhatók át a bemeneti objektumok egy parancsfájlt, és hogyan kérheti le a hiba objektumokat, valamint a kimeneti objektumok.</span><span class="sxs-lookup"><span data-stu-id="4cca3-105">It shows how to pass input objects to a script and how to retrieve error objects as well as the output objects.</span></span>

> [!NOTE]
> <span data-ttu-id="4cca3-106">Letöltheti a C# forrásfájl (runspace03.cs) ehhez a mintához a Microsoft Windows szoftverek fejlesztési Kit for Windows Vista és a Microsoft .NET Framework 3.0 futtatási összetevői.</span><span class="sxs-lookup"><span data-stu-id="4cca3-106">You can download the C# source file (runspace03.cs) for this sample using the Microsoft Windows Software Development Kit for Windows Vista and Microsoft .NET Framework 3.0 Runtime Components.</span></span> <span data-ttu-id="4cca3-107">Letöltési útmutatás: [Windows PowerShell telepítése és a Windows PowerShell SDK letöltési](/powershell/developer/installing-the-windows-powershell-sdk).</span><span class="sxs-lookup"><span data-stu-id="4cca3-107">For download instructions, see [How to Install Windows PowerShell and Download the Windows PowerShell SDK](/powershell/developer/installing-the-windows-powershell-sdk).</span></span>
> <span data-ttu-id="4cca3-108">Letöltheti a C# forrásfájl (runspace03.cs) ehhez a mintához a Microsoft Windows szoftverek fejlesztési Kit for Windows Vista és a Microsoft .NET Framework 3.0 futtatási összetevői.</span><span class="sxs-lookup"><span data-stu-id="4cca3-108">You can download the C# source file (runspace03.cs) for this sample using the Microsoft Windows Software Development Kit for Windows Vista and Microsoft .NET Framework 3.0 Runtime Components.</span></span> <span data-ttu-id="4cca3-109">Letöltési útmutatás: [Windows PowerShell telepítése és a Windows PowerShell SDK letöltési](/powershell/developer/installing-the-windows-powershell-sdk).</span><span class="sxs-lookup"><span data-stu-id="4cca3-109">For download instructions, see [How to Install Windows PowerShell and Download the Windows PowerShell SDK](/powershell/developer/installing-the-windows-powershell-sdk).</span></span>
>
> <span data-ttu-id="4cca3-110">A letöltött forrásfájlok érhetők el a  **\<PowerShell-minták >** könyvtár.</span><span class="sxs-lookup"><span data-stu-id="4cca3-110">The downloaded source files are available in the **\<PowerShell Samples>** directory.</span></span>

## <a name="code-sample"></a><span data-ttu-id="4cca3-111">Kódminta</span><span class="sxs-lookup"><span data-stu-id="4cca3-111">Code Sample</span></span>

[!code-csharp[Runspace03.cs](../../powershell-sdk-samples/SDK-2.0/csharp/Runspace03/Runspace03.cs#L11-L88 "Runspace03.cs")]

## <a name="see-also"></a><span data-ttu-id="4cca3-112">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="4cca3-112">See Also</span></span>

[<span data-ttu-id="4cca3-113">Windows PowerShell programozói útmutató</span><span class="sxs-lookup"><span data-stu-id="4cca3-113">Windows PowerShell Programmer's Guide</span></span>](./windows-powershell-programmer-s-guide.md)

[<span data-ttu-id="4cca3-114">Windows PowerShell SDK</span><span class="sxs-lookup"><span data-stu-id="4cca3-114">Windows PowerShell SDK</span></span>](../windows-powershell-reference.md)