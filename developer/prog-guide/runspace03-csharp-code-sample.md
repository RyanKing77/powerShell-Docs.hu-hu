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
ms.openlocfilehash: 0e80f4d850a7c6dc044526a56b92f16eea4040b5
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62081376"
---
# <a name="runspace03-c-code-sample"></a><span data-ttu-id="e34b6-102">Runspace03 (C#) – Kódminta</span><span class="sxs-lookup"><span data-stu-id="e34b6-102">RunSpace03 (C#) Code Sample</span></span>

<span data-ttu-id="e34b6-103">Íme a C# forráskódját el a konzolalkalmazást ismertetett [létrehozása egy Console Application, hogy fut a megadott parancsfájl](http://msdn.microsoft.com/en-us/a93e6006-36db-4bcc-b9da-c5bebf4ffd68).</span><span class="sxs-lookup"><span data-stu-id="e34b6-103">Here is the C# source code for the console application described in [Creating a Console Application That Runs a Specified Script](http://msdn.microsoft.com/en-us/a93e6006-36db-4bcc-b9da-c5bebf4ffd68).</span></span> <span data-ttu-id="e34b6-104">Ebben a példában a [System.Management.Automation.Runspaceinvoke](/dotnet/api/System.Management.Automation.RunspaceInvoke) osztály végrehajtani egy parancsfájlt, amely lekéri a szkriptbe folyamat Névlista használatával dolgozza fel adatokat.</span><span class="sxs-lookup"><span data-stu-id="e34b6-104">This sample uses the [System.Management.Automation.Runspaceinvoke](/dotnet/api/System.Management.Automation.RunspaceInvoke) class to execute a script that retrieves process information by using the list of process names passed into the script.</span></span> <span data-ttu-id="e34b6-105">Bemutatja, hogyan adhatók át a bemeneti objektumok egy parancsfájlt, és hogyan kérheti le a hiba objektumokat, valamint a kimeneti objektumok.</span><span class="sxs-lookup"><span data-stu-id="e34b6-105">It shows how to pass input objects to a script and how to retrieve error objects as well as the output objects.</span></span>

> [!NOTE]
> <span data-ttu-id="e34b6-106">Letöltheti a C# forrásfájl (runspace03.cs) ehhez a mintához a Microsoft Windows szoftverek fejlesztési Kit for Windows Vista és a Microsoft .NET Framework 3.0 futtatási összetevői.</span><span class="sxs-lookup"><span data-stu-id="e34b6-106">You can download the C# source file (runspace03.cs) for this sample using the Microsoft Windows Software Development Kit for Windows Vista and Microsoft .NET Framework 3.0 Runtime Components.</span></span> <span data-ttu-id="e34b6-107">Letöltési útmutatás: [Windows PowerShell telepítése és a Windows PowerShell SDK letöltési](/powershell/developer/installing-the-windows-powershell-sdk).</span><span class="sxs-lookup"><span data-stu-id="e34b6-107">For download instructions, see [How to Install Windows PowerShell and Download the Windows PowerShell SDK](/powershell/developer/installing-the-windows-powershell-sdk).</span></span>
>
> <span data-ttu-id="e34b6-108">A letöltött forrásfájlok érhetők el a  **\<PowerShell-minták >** könyvtár.</span><span class="sxs-lookup"><span data-stu-id="e34b6-108">The downloaded source files are available in the **\<PowerShell Samples>** directory.</span></span>

## <a name="code-sample"></a><span data-ttu-id="e34b6-109">Kódminta</span><span class="sxs-lookup"><span data-stu-id="e34b6-109">Code Sample</span></span>

[!code-csharp[Runspace03.cs](../../powershell-sdk-samples/SDK-2.0/csharp/Runspace03/Runspace03.cs#L11-L88 "Runspace03.cs")]

## <a name="see-also"></a><span data-ttu-id="e34b6-110">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="e34b6-110">See Also</span></span>

[<span data-ttu-id="e34b6-111">Windows PowerShell programozói útmutató</span><span class="sxs-lookup"><span data-stu-id="e34b6-111">Windows PowerShell Programmer's Guide</span></span>](./windows-powershell-programmer-s-guide.md)

[<span data-ttu-id="e34b6-112">Windows PowerShell SDK</span><span class="sxs-lookup"><span data-stu-id="e34b6-112">Windows PowerShell SDK</span></span>](../windows-powershell-reference.md)