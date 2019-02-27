---
title: GetProc03 Kódminták |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 8ad39c7d-2f64-49d1-9be0-d2295e4302b3
caps.latest.revision: 5
ms.openlocfilehash: 8cb02b9f2510b90f405651deaf551e9622f5a298
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56847725"
---
# <a name="getproc03-code-samples"></a><span data-ttu-id="b56f1-102">GetProc03 – Kódminták</span><span class="sxs-lookup"><span data-stu-id="b56f1-102">GetProc03 Code Samples</span></span>

<span data-ttu-id="b56f1-103">Az alábbiakban a GetProc03 minta parancsmag Kódminták.</span><span class="sxs-lookup"><span data-stu-id="b56f1-103">Here are the code samples for the GetProc03 sample cmdlet.</span></span> <span data-ttu-id="b56f1-104">Ez a `Get-Process` parancsmag minta ismertetett [a folyamat folyamat bemeneti paramétereket adunk hozzá](../cmdlet/adding-parameters-that-process-pipeline-input.md).</span><span class="sxs-lookup"><span data-stu-id="b56f1-104">This is the `Get-Process` cmdlet sample described in [Adding Parameters that Process Pipeline Input](../cmdlet/adding-parameters-that-process-pipeline-input.md).</span></span> <span data-ttu-id="b56f1-105">Ez `Get-Process` parancsmagot használja egy `Name` paraméter, amely egy folyamat objektumot a bemenetet elfogadja folyamat adatait kérdezi le a helyi számítógép megadott neve alapján, és ezután megjeleníti a folyamatok adatait a parancssorban.</span><span class="sxs-lookup"><span data-stu-id="b56f1-105">This `Get-Process` cmdlet uses a `Name` parameter that accepts input from a pipeline object, retrieves process information from the local computer based on the supplied names, and then displays information about the processes at the command line.</span></span>

> [!NOTE]
> <span data-ttu-id="b56f1-106">Letöltheti a C# forrásfájl (getprov03.cs) a Get-Proc parancsmag használatával a Microsoft Windows szoftverek fejlesztési Kit for Windows Vista és a .NET Framework 3.0 futtatási összetevői.</span><span class="sxs-lookup"><span data-stu-id="b56f1-106">You can download the C# source file (getprov03.cs) for this Get-Proc cmdlet using the Microsoft Windows Software Development Kit for Windows Vista and .NET Framework 3.0 Runtime Components.</span></span> <span data-ttu-id="b56f1-107">Letöltési útmutatás: [Windows PowerShell telepítése és a Windows PowerShell SDK letöltési](/powershell/developer/installing-the-windows-powershell-sdk).</span><span class="sxs-lookup"><span data-stu-id="b56f1-107">For download instructions, see [How to Install Windows PowerShell and Download the Windows PowerShell SDK](/powershell/developer/installing-the-windows-powershell-sdk).</span></span>
> <span data-ttu-id="b56f1-108">Letöltheti a C# forrásfájl (getprov03.cs) a Get-Proc parancsmag használatával a Microsoft Windows szoftverek fejlesztési Kit for Windows Vista és a .NET Framework 3.0 futtatási összetevői.</span><span class="sxs-lookup"><span data-stu-id="b56f1-108">You can download the C# source file (getprov03.cs) for this Get-Proc cmdlet using the Microsoft Windows Software Development Kit for Windows Vista and .NET Framework 3.0 Runtime Components.</span></span> <span data-ttu-id="b56f1-109">Letöltési útmutatás: [Windows PowerShell telepítése és a Windows PowerShell SDK letöltési](/powershell/developer/installing-the-windows-powershell-sdk).</span><span class="sxs-lookup"><span data-stu-id="b56f1-109">For download instructions, see [How to Install Windows PowerShell and Download the Windows PowerShell SDK](/powershell/developer/installing-the-windows-powershell-sdk).</span></span>
>
> <span data-ttu-id="b56f1-110">A letöltött forrásfájlok érhetők el a  **\<PowerShell-minták >** könyvtár.</span><span class="sxs-lookup"><span data-stu-id="b56f1-110">The downloaded source files are available in the **\<PowerShell Samples>** directory.</span></span>

<span data-ttu-id="b56f1-111">Teljes minta kódot a következő témakörökben talál.</span><span class="sxs-lookup"><span data-stu-id="b56f1-111">For complete sample code, see the following topics.</span></span>

|<span data-ttu-id="b56f1-112">Nyelv</span><span class="sxs-lookup"><span data-stu-id="b56f1-112">Language</span></span>|<span data-ttu-id="b56f1-113">Témakör</span><span class="sxs-lookup"><span data-stu-id="b56f1-113">Topic</span></span>|
|--------------|-----------|
|<span data-ttu-id="b56f1-114">C#</span><span class="sxs-lookup"><span data-stu-id="b56f1-114">C#</span></span>|[<span data-ttu-id="b56f1-115">GetProc03 (C#) mintakód</span><span class="sxs-lookup"><span data-stu-id="b56f1-115">GetProc03 (C#) Sample Code</span></span>](./getproc03-csharp-sample-code.md)|
|<span data-ttu-id="b56f1-116">VB.NET</span><span class="sxs-lookup"><span data-stu-id="b56f1-116">VB.NET</span></span>|[<span data-ttu-id="b56f1-117">GetProc03 (VB.NET) mintakód</span><span class="sxs-lookup"><span data-stu-id="b56f1-117">GetProc03 (VB.NET) Sample Code</span></span>](./getproc03-vb-net-sample-code.md)|

## <a name="see-also"></a><span data-ttu-id="b56f1-118">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="b56f1-118">See Also</span></span>

[<span data-ttu-id="b56f1-119">Windows PowerShell programozói útmutató</span><span class="sxs-lookup"><span data-stu-id="b56f1-119">Windows PowerShell Programmer's Guide</span></span>](./windows-powershell-programmer-s-guide.md)

[<span data-ttu-id="b56f1-120">Windows PowerShell SDK</span><span class="sxs-lookup"><span data-stu-id="b56f1-120">Windows PowerShell SDK</span></span>](../windows-powershell-reference.md)