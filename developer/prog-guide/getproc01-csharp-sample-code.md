---
title: GetProc01 (C#) mintakód |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 65094bb7-1972-44b3-b8b0-5f639860b58c
caps.latest.revision: 5
ms.openlocfilehash: 32c8214935a8c9f455426b76966d8c7fb33353d4
ms.sourcegitcommit: 69abc5ad16e5dd29ddfb1853e266a4bfd1d59d59
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/05/2019
ms.locfileid: "57430077"
---
# <a name="getproc01-c-sample-code"></a><span data-ttu-id="65495-102">GetProc01 (C#) – mintakód</span><span class="sxs-lookup"><span data-stu-id="65495-102">GetProc01 (C#) Sample Code</span></span>

<span data-ttu-id="65495-103">A következő kódot a GetProc01 parancsmagra megvalósítását mutatja be.</span><span class="sxs-lookup"><span data-stu-id="65495-103">The following code shows the implementation of the GetProc01 sample cmdlet.</span></span> <span data-ttu-id="65495-104">Figyelje meg, hogy a parancsmag egyszerűsödött, ha a folyamat lekéréséhez a tényleges munkát a [System.Diagnostics.Process.Getprocesses\*](/dotnet/api/System.Diagnostics.Process.GetProcesses) metódust.</span><span class="sxs-lookup"><span data-stu-id="65495-104">Notice that the cmdlet is simplified by leaving the actual work of process retrieval to the [System.Diagnostics.Process.Getprocesses\*](/dotnet/api/System.Diagnostics.Process.GetProcesses) method.</span></span>

> [!NOTE]
> <span data-ttu-id="65495-105">Letöltheti a C# forrásfájl (getproc01.cs) a Get-Proc parancsmag használatával a Microsoft Windows szoftverek fejlesztési Kit for Windows Vista és a .NET Framework 3.0 futtatási összetevői.</span><span class="sxs-lookup"><span data-stu-id="65495-105">You can download the C# source file (getproc01.cs) for this Get-Proc cmdlet using the Microsoft Windows Software Development Kit for Windows Vista and .NET Framework 3.0 Runtime Components.</span></span> <span data-ttu-id="65495-106">Letöltési útmutatás: [Windows PowerShell telepítése és a Windows PowerShell SDK letöltési](/powershell/developer/installing-the-windows-powershell-sdk).</span><span class="sxs-lookup"><span data-stu-id="65495-106">For download instructions, see [How to Install Windows PowerShell and Download the Windows PowerShell SDK](/powershell/developer/installing-the-windows-powershell-sdk).</span></span>
>
> <span data-ttu-id="65495-107">A letöltött forrásfájlok érhetők el a  **\<PowerShell-minták >** könyvtár.</span><span class="sxs-lookup"><span data-stu-id="65495-107">The downloaded source files are available in the **\<PowerShell Samples>** directory.</span></span>

## <a name="code-sample"></a><span data-ttu-id="65495-108">Kódminta</span><span class="sxs-lookup"><span data-stu-id="65495-108">Code Sample</span></span>

[!code-csharp[GetProcessSample01.cs](../../powershell-sdk-samples/SDK-2.0/csharp/GetProcessSample01/GetProcessSample01.cs#L11-L126 "GetProcessSample01.cs")]

## <a name="see-also"></a><span data-ttu-id="65495-109">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="65495-109">See Also</span></span>

[<span data-ttu-id="65495-110">Windows PowerShell programozói útmutató</span><span class="sxs-lookup"><span data-stu-id="65495-110">Windows PowerShell Programmer's Guide</span></span>](./windows-powershell-programmer-s-guide.md)

[<span data-ttu-id="65495-111">Windows PowerShell SDK</span><span class="sxs-lookup"><span data-stu-id="65495-111">Windows PowerShell SDK</span></span>](../windows-powershell-reference.md)