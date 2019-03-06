---
title: GetProc03 (C#) mintakód |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: ebc0d538-69ac-43d5-837d-b6f47344fc6a
caps.latest.revision: 5
ms.openlocfilehash: 328f4eeea27243102679ab5d139181a878165ad6
ms.sourcegitcommit: 69abc5ad16e5dd29ddfb1853e266a4bfd1d59d59
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/05/2019
ms.locfileid: "57429754"
---
# <a name="getproc03-c-sample-code"></a><span data-ttu-id="33f95-102">GetProc03 (C#) – mintakód</span><span class="sxs-lookup"><span data-stu-id="33f95-102">GetProc03 (C#) Sample Code</span></span>

<span data-ttu-id="33f95-103">Az alábbi kód megvalósítását mutatja be egy `Get-Process` parancsmag, amely elfogadja a bemeneti vagyok.</span><span class="sxs-lookup"><span data-stu-id="33f95-103">The following code shows the implementation of a `Get-Process` cmdlet that can accept pipelined input.</span></span> <span data-ttu-id="33f95-104">Ez a megvalósítás meghatározása egy `Name` paraméter, amely elfogadja a folyamat bemeneti, folyamat adatait kérdezi le a helyi számítógép megadott neve alapján, és ezután a [System.Management.Automation.Cmdlet.Writeobject% 28System.Object%2Csystem.Boolean%29](/dotnet/api/System.Management.Automation.Cmdlet.WriteObject%28System.Object%2CSystem.Boolean%29) metódus objektumok küld el a folyamat a kimeneti mechanizmusként.</span><span class="sxs-lookup"><span data-stu-id="33f95-104">This implementation defines a `Name` parameter that accepts pipeline input, retrieves process information from the local computer based on the supplied names, and then uses the [System.Management.Automation.Cmdlet.Writeobject%28System.Object%2Csystem.Boolean%29](/dotnet/api/System.Management.Automation.Cmdlet.WriteObject%28System.Object%2CSystem.Boolean%29) method as the output mechanism for sending objects to the pipeline.</span></span>

> [!NOTE]
> <span data-ttu-id="33f95-105">Letöltheti a C# forrásfájl (getprov03.cs) a Get-Proc parancsmag használatával a Microsoft Windows szoftverek fejlesztési Kit for Windows Vista és a .NET Framework 3.0 futtatási összetevői.</span><span class="sxs-lookup"><span data-stu-id="33f95-105">You can download the C# source file (getprov03.cs) for this Get-Proc cmdlet using the Microsoft Windows Software Development Kit for Windows Vista and .NET Framework 3.0 Runtime Components.</span></span> <span data-ttu-id="33f95-106">Letöltési útmutatás: [Windows PowerShell telepítése és a Windows PowerShell SDK letöltési](/powershell/developer/installing-the-windows-powershell-sdk).</span><span class="sxs-lookup"><span data-stu-id="33f95-106">For download instructions, see [How to Install Windows PowerShell and Download the Windows PowerShell SDK](/powershell/developer/installing-the-windows-powershell-sdk).</span></span>
>
> <span data-ttu-id="33f95-107">A letöltött forrásfájlok érhetők el a  **\<PowerShell-minták >** könyvtár.</span><span class="sxs-lookup"><span data-stu-id="33f95-107">The downloaded source files are available in the **\<PowerShell Samples>** directory.</span></span>

## <a name="code-sample"></a><span data-ttu-id="33f95-108">Kódminta</span><span class="sxs-lookup"><span data-stu-id="33f95-108">Code Sample</span></span>

[!code-csharp[GetProcessSample03.cs](../../powershell-sdk-samples/SDK-2.0/csharp/GetProcessSample03/GetProcessSample03.cs#L11-L78 "GetProcessSample03.cs")]

## <a name="see-also"></a><span data-ttu-id="33f95-109">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="33f95-109">See Also</span></span>

[<span data-ttu-id="33f95-110">Windows PowerShell programozói útmutató</span><span class="sxs-lookup"><span data-stu-id="33f95-110">Windows PowerShell Programmer's Guide</span></span>](./windows-powershell-programmer-s-guide.md)

[<span data-ttu-id="33f95-111">Windows PowerShell SDK</span><span class="sxs-lookup"><span data-stu-id="33f95-111">Windows PowerShell SDK</span></span>](../windows-powershell-reference.md)