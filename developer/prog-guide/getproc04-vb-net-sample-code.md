---
title: GetProc04 (VB.NET) mintakód |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 5d22f47b-3679-4587-a559-94454415d2dd
caps.latest.revision: 5
ms.openlocfilehash: 0d0d1a3f82bc2cee025139d69fee02eb601fa563
ms.sourcegitcommit: caac7d098a448232304c9d6728e7340ec7517a71
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/16/2019
ms.locfileid: "58055461"
---
# <a name="getproc04-vbnet-sample-code"></a><span data-ttu-id="55592-102">GetProc04 (VB.NET) Sample Code – mintakód</span><span class="sxs-lookup"><span data-stu-id="55592-102">GetProc04 (VB.NET) Sample Code</span></span>

<span data-ttu-id="55592-103">Az alábbi kód megvalósítását mutatja be egy `Get-Process` parancsmagot, amely nonterminating hibát jelez.</span><span class="sxs-lookup"><span data-stu-id="55592-103">The following code shows the implementation of a `Get-Process` cmdlet that reports nonterminating errors.</span></span> <span data-ttu-id="55592-104">Ez a megvalósítás meghívja a [System.Management.Automation.Cmdlet.WriteError](/dotnet/api/System.Management.Automation.Cmdlet.WriteError) metódus nonterminating hibák jelentéséhez.</span><span class="sxs-lookup"><span data-stu-id="55592-104">This implementation calls the [System.Management.Automation.Cmdlet.WriteError](/dotnet/api/System.Management.Automation.Cmdlet.WriteError) method to report nonterminating errors.</span></span>

> [!NOTE]
> <span data-ttu-id="55592-105">Letöltheti a C# forrásfájl (getprov04.cs) a Get-Proc parancsmag használatával a Microsoft Windows szoftverek fejlesztési Kit for Windows Vista és a .NET Framework 3.0 futtatási összetevői.</span><span class="sxs-lookup"><span data-stu-id="55592-105">You can download the C# source file (getprov04.cs) for this Get-Proc cmdlet using the Microsoft Windows Software Development Kit for Windows Vista and .NET Framework 3.0 Runtime Components.</span></span> <span data-ttu-id="55592-106">Letöltési útmutatás: [Windows PowerShell telepítése és a Windows PowerShell SDK letöltési](/powershell/developer/installing-the-windows-powershell-sdk).</span><span class="sxs-lookup"><span data-stu-id="55592-106">For download instructions, see [How to Install Windows PowerShell and Download the Windows PowerShell SDK](/powershell/developer/installing-the-windows-powershell-sdk).</span></span>
>
> <span data-ttu-id="55592-107">A letöltött forrásfájlok érhetők el a  **\<PowerShell-minták >** könyvtár.</span><span class="sxs-lookup"><span data-stu-id="55592-107">The downloaded source files are available in the **\<PowerShell Samples>** directory.</span></span>

## <a name="code-sample"></a><span data-ttu-id="55592-108">Kódminta</span><span class="sxs-lookup"><span data-stu-id="55592-108">Code Sample</span></span>

<!-- TODO!!!: review snippet reference  [!CODE [Msh_samplesgetproc04#GetProc04vball](Msh_samplesgetproc04#GetProc04vball)]  -->

## <a name="see-also"></a><span data-ttu-id="55592-109">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="55592-109">See Also</span></span>

[<span data-ttu-id="55592-110">Windows PowerShell programozói útmutató</span><span class="sxs-lookup"><span data-stu-id="55592-110">Windows PowerShell Programmer's Guide</span></span>](./windows-powershell-programmer-s-guide.md)

[<span data-ttu-id="55592-111">Windows PowerShell SDK</span><span class="sxs-lookup"><span data-stu-id="55592-111">Windows PowerShell SDK</span></span>](../windows-powershell-reference.md)