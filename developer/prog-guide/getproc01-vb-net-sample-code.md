---
title: GetProc01 (VB.NET) mintakód |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 3ee87f67-6d2c-48cc-b300-3ae917c6dc88
caps.latest.revision: 5
ms.openlocfilehash: 2411642c39737e7dc03bd0bb4ea753ed27783732
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62081801"
---
# <a name="getproc01-vbnet-sample-code"></a><span data-ttu-id="3f258-102">GetProc01 (VB.NET) Sample Code – mintakód</span><span class="sxs-lookup"><span data-stu-id="3f258-102">GetProc01 (VB.NET) Sample Code</span></span>

<span data-ttu-id="3f258-103">A következő kódot a GetProc01 parancsmagra megvalósítását mutatja be.</span><span class="sxs-lookup"><span data-stu-id="3f258-103">The following code shows the implementation of the GetProc01 sample cmdlet.</span></span> <span data-ttu-id="3f258-104">Figyelje meg, hogy a parancsmag egyszerűsödött, ha a folyamat lekéréséhez a tényleges munkát a [System.Diagnostics.Process.Getprocesses\*](/dotnet/api/System.Diagnostics.Process.GetProcesses) metódust.</span><span class="sxs-lookup"><span data-stu-id="3f258-104">Notice that the cmdlet is simplified by leaving the actual work of process retrieval to the [System.Diagnostics.Process.Getprocesses\*](/dotnet/api/System.Diagnostics.Process.GetProcesses) method.</span></span>

> [!NOTE]
> <span data-ttu-id="3f258-105">Letöltheti a C# forrásfájl (getproc01.cs) a Get-Proc parancsmag használatával a Microsoft Windows szoftverek fejlesztési Kit for Windows Vista és a .NET Framework 3.0 futtatási összetevői.</span><span class="sxs-lookup"><span data-stu-id="3f258-105">You can download the C# source file (getproc01.cs) for this Get-Proc cmdlet using the Microsoft Windows Software Development Kit for Windows Vista and .NET Framework 3.0 Runtime Components.</span></span> <span data-ttu-id="3f258-106">Letöltési útmutatás: [Windows PowerShell telepítése és a Windows PowerShell SDK letöltési](/powershell/developer/installing-the-windows-powershell-sdk).</span><span class="sxs-lookup"><span data-stu-id="3f258-106">For download instructions, see [How to Install Windows PowerShell and Download the Windows PowerShell SDK](/powershell/developer/installing-the-windows-powershell-sdk).</span></span>
>
> <span data-ttu-id="3f258-107">A letöltött forrásfájlok érhetők el a  **\<PowerShell-minták >** könyvtár.</span><span class="sxs-lookup"><span data-stu-id="3f258-107">The downloaded source files are available in the **\<PowerShell Samples>** directory.</span></span>

## <a name="code-sample"></a><span data-ttu-id="3f258-108">Kódminta</span><span class="sxs-lookup"><span data-stu-id="3f258-108">Code Sample</span></span>

<!-- TODO!!!: review snippet reference  [!CODE [msh_samplesgetproc01#getproc01vball](msh_samplesgetproc01#getproc01vball)]  -->

## <a name="see-also"></a><span data-ttu-id="3f258-109">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="3f258-109">See Also</span></span>

[<span data-ttu-id="3f258-110">Windows PowerShell programozói útmutató</span><span class="sxs-lookup"><span data-stu-id="3f258-110">Windows PowerShell Programmer's Guide</span></span>](./windows-powershell-programmer-s-guide.md)

[<span data-ttu-id="3f258-111">Windows PowerShell SDK</span><span class="sxs-lookup"><span data-stu-id="3f258-111">Windows PowerShell SDK</span></span>](../windows-powershell-reference.md)