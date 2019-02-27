---
title: StopProcessSample04 Kódminták |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: dc68af2b-f622-47c4-964f-b07f3d5bdf14
caps.latest.revision: 5
ms.openlocfilehash: fdb78ac93befba66041c4e45834f8a857e3670b6
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56851092"
---
# <a name="stopprocesssample04-code-samples"></a><span data-ttu-id="39362-102">StopProcessSample04 – kódminták</span><span class="sxs-lookup"><span data-stu-id="39362-102">StopProcessSample04 Code Samples</span></span>

<span data-ttu-id="39362-103">Az alábbiakban a StopProc00 minta parancsmag Kódminták.</span><span class="sxs-lookup"><span data-stu-id="39362-103">Here are the code samples for the StopProc00 sample cmdlet.</span></span> <span data-ttu-id="39362-104">Ez a `Stop-Process` parancsmag minta ismertetett [paraméterkészlettel hozzáadása egy parancsmag](../cmdlet/adding-parameter-sets-to-a-cmdlet.md).</span><span class="sxs-lookup"><span data-stu-id="39362-104">This is the `Stop-Process` cmdlet sample described in [Adding Parameter Sets to a Cmdlet](../cmdlet/adding-parameter-sets-to-a-cmdlet.md).</span></span> <span data-ttu-id="39362-105">A `Stop-Process` parancsmag úgy tervezték, hogy állítsa le a folyamatokat, amelyek a Get-Proc parancsmaggal olvassa be (ismertetett [létrehozásához az első parancsmag](../cmdlet/creating-a-cmdlet-without-parameters.md)).</span><span class="sxs-lookup"><span data-stu-id="39362-105">The `Stop-Process` cmdlet is designed to stop processes that are retrieved using the Get-Proc cmdlet (described in [Creating Your First Cmdlet](../cmdlet/creating-a-cmdlet-without-parameters.md)).</span></span>

> [!NOTE]
> <span data-ttu-id="39362-106">Letöltheti a C# (stopprocesssample04.cs) és a Microsoft Windows szoftverek fejlesztési Kit for Windows Vista és a .NET Framework 3.0 futtatási összetevői használatával állítsa le a folyamaton parancsmag (stopprocesssample04.vb) VB.NET.</span><span class="sxs-lookup"><span data-stu-id="39362-106">You can download the C# (stopprocesssample04.cs) and VB.NET (stopprocesssample04.vb) for this Stop-Proc cmdlet using the Microsoft Windows Software Development Kit for Windows Vista and .NET Framework 3.0 Runtime Components.</span></span> <span data-ttu-id="39362-107">Letöltési útmutatás: [Windows PowerShell telepítése és a Windows PowerShell SDK letöltési](/powershell/developer/installing-the-windows-powershell-sdk).</span><span class="sxs-lookup"><span data-stu-id="39362-107">For download instructions, see [How to Install Windows PowerShell and Download the Windows PowerShell SDK](/powershell/developer/installing-the-windows-powershell-sdk).</span></span>
> <span data-ttu-id="39362-108">Letöltheti a C# (stopprocesssample04.cs) és a Microsoft Windows szoftverek fejlesztési Kit for Windows Vista és a .NET Framework 3.0 futtatási összetevői használatával állítsa le a folyamaton parancsmag (stopprocesssample04.vb) VB.NET.</span><span class="sxs-lookup"><span data-stu-id="39362-108">You can download the C# (stopprocesssample04.cs) and VB.NET (stopprocesssample04.vb) for this Stop-Proc cmdlet using the Microsoft Windows Software Development Kit for Windows Vista and .NET Framework 3.0 Runtime Components.</span></span> <span data-ttu-id="39362-109">Letöltési útmutatás: [Windows PowerShell telepítése és a Windows PowerShell SDK letöltési](/powershell/developer/installing-the-windows-powershell-sdk).</span><span class="sxs-lookup"><span data-stu-id="39362-109">For download instructions, see [How to Install Windows PowerShell and Download the Windows PowerShell SDK](/powershell/developer/installing-the-windows-powershell-sdk).</span></span>
>
> <span data-ttu-id="39362-110">A letöltött forrásfájlok érhetők el a  **\<PowerShell-minták >** könyvtár.</span><span class="sxs-lookup"><span data-stu-id="39362-110">The downloaded source files are available in the **\<PowerShell Samples>** directory.</span></span>

<span data-ttu-id="39362-111">Teljes minta kódot a következő témakörökben talál.</span><span class="sxs-lookup"><span data-stu-id="39362-111">For complete sample code, see the following topics.</span></span>

|<span data-ttu-id="39362-112">Nyelv</span><span class="sxs-lookup"><span data-stu-id="39362-112">Language</span></span>|<span data-ttu-id="39362-113">Témakör</span><span class="sxs-lookup"><span data-stu-id="39362-113">Topic</span></span>|
|--------------|-----------|
|<span data-ttu-id="39362-114">C#</span><span class="sxs-lookup"><span data-stu-id="39362-114">C#</span></span>|[<span data-ttu-id="39362-115">StopProc04 (C#) mintakód</span><span class="sxs-lookup"><span data-stu-id="39362-115">StopProc04 (C#) Sample Code</span></span>](./stopprocesssample04-csharp-sample-code.md)|
|<span data-ttu-id="39362-116">VB.NET</span><span class="sxs-lookup"><span data-stu-id="39362-116">VB.NET</span></span>|[<span data-ttu-id="39362-117">StopProc04 (VB.NET) Sample Code</span><span class="sxs-lookup"><span data-stu-id="39362-117">StopProc04 (VB.NET) Sample Code</span></span>](./stopprocesssample04-vb-net-sample-code.md)|

## <a name="see-also"></a><span data-ttu-id="39362-118">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="39362-118">See Also</span></span>

[<span data-ttu-id="39362-119">Windows PowerShell programozói útmutató</span><span class="sxs-lookup"><span data-stu-id="39362-119">Windows PowerShell Programmer's Guide</span></span>](./windows-powershell-programmer-s-guide.md)

[<span data-ttu-id="39362-120">Windows PowerShell SDK</span><span class="sxs-lookup"><span data-stu-id="39362-120">Windows PowerShell SDK</span></span>](../windows-powershell-reference.md)