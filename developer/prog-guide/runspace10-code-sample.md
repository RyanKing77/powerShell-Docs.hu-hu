---
title: Kódminta RunSpace10 |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 5337dc40-c56e-458b-aedc-5f5d401dfd28
caps.latest.revision: 6
ms.openlocfilehash: 77c0675b45bf4ff6f8c6a85ff9a090c13c199c6d
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62081240"
---
# <a name="runspace10-code-sample"></a><span data-ttu-id="8c7a7-102">Runspace10 – Kódminta</span><span class="sxs-lookup"><span data-stu-id="8c7a7-102">RunSpace10 Code Sample</span></span>

<span data-ttu-id="8c7a7-103">Íme a forráskódot a Runspace10 minta.</span><span class="sxs-lookup"><span data-stu-id="8c7a7-103">Here is the source code for the Runspace10 sample.</span></span> <span data-ttu-id="8c7a7-104">Ez a mintaalkalmazás egy parancsmag hozzáadja [System.Management.Automation.Runspaces.Runspaceconfiguration](/dotnet/api/System.Management.Automation.Runspaces.RunspaceConfiguration) és a módosított konfigurációs információk segítségével a futási térben létrehozása.</span><span class="sxs-lookup"><span data-stu-id="8c7a7-104">This sample application adds a cmdlet to [System.Management.Automation.Runspaces.Runspaceconfiguration](/dotnet/api/System.Management.Automation.Runspaces.RunspaceConfiguration) and then uses the modified configuration information to create the runspace.</span></span>

> [!NOTE]
> <span data-ttu-id="8c7a7-105">Letöltheti a C# forrásfájl (runspace10.cs) a Windows szoftverek fejlesztési Kit for Windows Vista és a Microsoft .NET Framework 3.0 futtatási összetevői.</span><span class="sxs-lookup"><span data-stu-id="8c7a7-105">You can download the C# source file (runspace10.cs) by using the Windows Software Development Kit for Windows Vista and Microsoft .NET Framework 3.0 Runtime Components.</span></span> <span data-ttu-id="8c7a7-106">Letöltési útmutatás: [Windows PowerShell telepítése és a Windows PowerShell SDK letöltési](/powershell/developer/installing-the-windows-powershell-sdk).</span><span class="sxs-lookup"><span data-stu-id="8c7a7-106">For download instructions, see [How to Install Windows PowerShell and Download the Windows PowerShell SDK](/powershell/developer/installing-the-windows-powershell-sdk).</span></span>
>
> <span data-ttu-id="8c7a7-107">A letöltött forrásfájlok érhetők el a  **\<PowerShell-minták >** könyvtár.</span><span class="sxs-lookup"><span data-stu-id="8c7a7-107">The downloaded source files are available in the **\<PowerShell Samples>** directory.</span></span>

## <a name="code-sample"></a><span data-ttu-id="8c7a7-108">Kódminta</span><span class="sxs-lookup"><span data-stu-id="8c7a7-108">Code Sample</span></span>

[!code-csharp[Runspace10.cs](../../powershell-sdk-samples/SDK-2.0/csharp/Runspace10/Runspace10.cs#L11-L118 "Runspace10.cs")]

## <a name="see-also"></a><span data-ttu-id="8c7a7-109">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="8c7a7-109">See Also</span></span>

[<span data-ttu-id="8c7a7-110">Windows PowerShell programozói útmutató</span><span class="sxs-lookup"><span data-stu-id="8c7a7-110">Windows PowerShell Programmer's Guide</span></span>](./windows-powershell-programmer-s-guide.md)

[<span data-ttu-id="8c7a7-111">Windows PowerShell SDK</span><span class="sxs-lookup"><span data-stu-id="8c7a7-111">Windows PowerShell SDK</span></span>](../windows-powershell-reference.md)