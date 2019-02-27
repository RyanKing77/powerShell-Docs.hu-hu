---
title: RunSpace04 Kódminták |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: cb6fcc47-cf89-43e7-b686-3d60934ce3e7
caps.latest.revision: 6
ms.openlocfilehash: 10f236b201920d2d456af41328c7a62a9e14b571
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56850378"
---
# <a name="runspace04-code-samples"></a><span data-ttu-id="2cb43-102">Runspace04 – Kódminták</span><span class="sxs-lookup"><span data-stu-id="2cb43-102">RunSpace04 Code Samples</span></span>

<span data-ttu-id="2cb43-103">Íme egy kódminta egy futási teret használ, a [System.Management.Automation.Runspaceinvoke](/dotnet/api/System.Management.Automation.RunspaceInvoke) osztály egy parancsfájlt, amely a leállítási hibát generál végrehajtásához.</span><span class="sxs-lookup"><span data-stu-id="2cb43-103">Here is a code sample for a runspace that uses the [System.Management.Automation.Runspaceinvoke](/dotnet/api/System.Management.Automation.RunspaceInvoke) class to execute a script that generates a terminating error.</span></span> <span data-ttu-id="2cb43-104">A hiba kölcsönhatásai és hibarekord értelmezése felelős a gazdaalkalmazást.</span><span class="sxs-lookup"><span data-stu-id="2cb43-104">The host application is responsible for catching the error and interpreting the error record.</span></span>

> [!NOTE]
> <span data-ttu-id="2cb43-105">Ez a Windows szoftverek fejlesztési Kit for Windows Vista és a Microsoft .NET Framework 3.0 futtatási összetevői futási térben lehet letölteni a VB.NET forrásfájl (Runspace04.vb).</span><span class="sxs-lookup"><span data-stu-id="2cb43-105">You can download the VB.NET source file (Runspace04.vb) for this runspace using the Windows Software Development Kit for Windows Vista and Microsoft .NET Framework 3.0 Runtime Components.</span></span> <span data-ttu-id="2cb43-106">Letöltési útmutatás: [Windows PowerShell telepítése és a Windows PowerShell SDK letöltési](/powershell/developer/installing-the-windows-powershell-sdk).</span><span class="sxs-lookup"><span data-stu-id="2cb43-106">For download instructions, see [How to Install Windows PowerShell and Download the Windows PowerShell SDK](/powershell/developer/installing-the-windows-powershell-sdk).</span></span>
> <span data-ttu-id="2cb43-107">Ez a Windows szoftverek fejlesztési Kit for Windows Vista és a Microsoft .NET Framework 3.0 futtatási összetevői futási térben lehet letölteni a VB.NET forrásfájl (Runspace04.vb).</span><span class="sxs-lookup"><span data-stu-id="2cb43-107">You can download the VB.NET source file (Runspace04.vb) for this runspace using the Windows Software Development Kit for Windows Vista and Microsoft .NET Framework 3.0 Runtime Components.</span></span> <span data-ttu-id="2cb43-108">Letöltési útmutatás: [Windows PowerShell telepítése és a Windows PowerShell SDK letöltési](/powershell/developer/installing-the-windows-powershell-sdk).</span><span class="sxs-lookup"><span data-stu-id="2cb43-108">For download instructions, see [How to Install Windows PowerShell and Download the Windows PowerShell SDK](/powershell/developer/installing-the-windows-powershell-sdk).</span></span>
>
> <span data-ttu-id="2cb43-109">A letöltött forrásfájlok érhetők el a  **\<PowerShell-minták >** könyvtár.</span><span class="sxs-lookup"><span data-stu-id="2cb43-109">The downloaded source files are available in the **\<PowerShell Samples>** directory.</span></span>

<span data-ttu-id="2cb43-110">Teljes minta kódot a következő témakörökben talál.</span><span class="sxs-lookup"><span data-stu-id="2cb43-110">For complete sample code, see the following topics.</span></span>

|<span data-ttu-id="2cb43-111">Nyelv</span><span class="sxs-lookup"><span data-stu-id="2cb43-111">Language</span></span>|<span data-ttu-id="2cb43-112">Témakör</span><span class="sxs-lookup"><span data-stu-id="2cb43-112">Topic</span></span>|
|--------------|-----------|
|<span data-ttu-id="2cb43-113">VB.NET</span><span class="sxs-lookup"><span data-stu-id="2cb43-113">VB.NET</span></span>|[<span data-ttu-id="2cb43-114">Runspace01 (VB.NET) kódminta</span><span class="sxs-lookup"><span data-stu-id="2cb43-114">Runspace01 (VB.NET) Code Sample</span></span>](./runspace01-vb-net-code-sample.md)|

## <a name="see-also"></a><span data-ttu-id="2cb43-115">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="2cb43-115">See Also</span></span>

[<span data-ttu-id="2cb43-116">Windows PowerShell programozói útmutató</span><span class="sxs-lookup"><span data-stu-id="2cb43-116">Windows PowerShell Programmer's Guide</span></span>](./windows-powershell-programmer-s-guide.md)

[<span data-ttu-id="2cb43-117">Windows PowerShell SDK</span><span class="sxs-lookup"><span data-stu-id="2cb43-117">Windows PowerShell SDK</span></span>](../windows-powershell-reference.md)