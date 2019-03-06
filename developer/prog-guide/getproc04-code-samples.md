---
title: GetProc04 Kódminták |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: c00afd46-758a-4aec-b865-2c9d8f6a17ad
caps.latest.revision: 5
ms.openlocfilehash: b9b42c818981090496f7b14a1cb8bdec14a5d5bb
ms.sourcegitcommit: 69abc5ad16e5dd29ddfb1853e266a4bfd1d59d59
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/05/2019
ms.locfileid: "57429720"
---
# <a name="getproc04-code-samples"></a><span data-ttu-id="18368-102">GetProc04 – Kódminták</span><span class="sxs-lookup"><span data-stu-id="18368-102">GetProc04 Code Samples</span></span>

<span data-ttu-id="18368-103">Az alábbiakban a GetProc04 minta parancsmag Kódminták.</span><span class="sxs-lookup"><span data-stu-id="18368-103">Here are the code samples for the GetProc04 sample cmdlet.</span></span> <span data-ttu-id="18368-104">Ez a `Get-Process` parancsmag minta ismertetett [hozzáadása Nonterminating hibajelentés a parancsmaghoz](../cmdlet/adding-non-terminating-error-reporting-to-your-cmdlet.md).</span><span class="sxs-lookup"><span data-stu-id="18368-104">This is the `Get-Process` cmdlet sample described in [Adding Nonterminating Error Reporting to Your Cmdlet](../cmdlet/adding-non-terminating-error-reporting-to-your-cmdlet.md).</span></span> <span data-ttu-id="18368-105">Ez `Get-Process` parancsmag hívások a [System.Management.Automation.Cmdlet.Writeerror\*](/dotnet/api/System.Management.Automation.Cmdlet.WriteError) metódus, amikor a program érvénytelen művelet kivételt vált ki, folyamat-adatok beolvasása során.</span><span class="sxs-lookup"><span data-stu-id="18368-105">This `Get-Process` cmdlet calls the [System.Management.Automation.Cmdlet.Writeerror\*](/dotnet/api/System.Management.Automation.Cmdlet.WriteError) method whenever an invalid operation exception is thrown while retrieving process information.</span></span>

> [!NOTE]
> <span data-ttu-id="18368-106">Letöltheti a C# forrásfájl (getprov04.cs) a Get-Proc parancsmag használatával a Microsoft Windows szoftverek fejlesztési Kit for Windows Vista és a .NET Framework 3.0 futtatási összetevői.</span><span class="sxs-lookup"><span data-stu-id="18368-106">You can download the C# source file (getprov04.cs) for this Get-Proc cmdlet using the Microsoft Windows Software Development Kit for Windows Vista and .NET Framework 3.0 Runtime Components.</span></span> <span data-ttu-id="18368-107">Letöltési útmutatás: [Windows PowerShell telepítése és a Windows PowerShell SDK letöltési](/powershell/developer/installing-the-windows-powershell-sdk).</span><span class="sxs-lookup"><span data-stu-id="18368-107">For download instructions, see [How to Install Windows PowerShell and Download the Windows PowerShell SDK](/powershell/developer/installing-the-windows-powershell-sdk).</span></span>
>
> <span data-ttu-id="18368-108">A letöltött forrásfájlok érhetők el a  **\<PowerShell-minták >** könyvtár.</span><span class="sxs-lookup"><span data-stu-id="18368-108">The downloaded source files are available in the **\<PowerShell Samples>** directory.</span></span>

<span data-ttu-id="18368-109">Teljes minta kódot a következő témakörökben talál.</span><span class="sxs-lookup"><span data-stu-id="18368-109">For complete sample code, see the following topics.</span></span>

|<span data-ttu-id="18368-110">Nyelv</span><span class="sxs-lookup"><span data-stu-id="18368-110">Language</span></span>|<span data-ttu-id="18368-111">Témakör</span><span class="sxs-lookup"><span data-stu-id="18368-111">Topic</span></span>|
|--------------|-----------|
|<span data-ttu-id="18368-112">C#</span><span class="sxs-lookup"><span data-stu-id="18368-112">C#</span></span>|[<span data-ttu-id="18368-113">GetProc04 (C#) mintakód</span><span class="sxs-lookup"><span data-stu-id="18368-113">GetProc04 (C#) Sample Code</span></span>](./getproc04-csharp-sample-code.md)|
|<span data-ttu-id="18368-114">VB.NET</span><span class="sxs-lookup"><span data-stu-id="18368-114">VB.NET</span></span>|[<span data-ttu-id="18368-115">GetProc04 (VB.NET) mintakód</span><span class="sxs-lookup"><span data-stu-id="18368-115">GetProc04 (VB.NET) Sample Code</span></span>](./getproc04-vb-net-sample-code.md)|

## <a name="see-also"></a><span data-ttu-id="18368-116">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="18368-116">See Also</span></span>

[<span data-ttu-id="18368-117">Windows PowerShell programozói útmutató</span><span class="sxs-lookup"><span data-stu-id="18368-117">Windows PowerShell Programmer's Guide</span></span>](./windows-powershell-programmer-s-guide.md)

[<span data-ttu-id="18368-118">Windows PowerShell SDK</span><span class="sxs-lookup"><span data-stu-id="18368-118">Windows PowerShell SDK</span></span>](../windows-powershell-reference.md)