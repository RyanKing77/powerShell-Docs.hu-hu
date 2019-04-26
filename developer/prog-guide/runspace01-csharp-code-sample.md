---
title: Runspace01 (C#) kódminta |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: d59f8b7c-e800-4633-aa5b-74d4c57e2706
caps.latest.revision: 6
ms.openlocfilehash: 59320365c4a35c3d71af10273eb21b1ce01e5c0c
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62081461"
---
# <a name="runspace01-c-code-sample"></a><span data-ttu-id="22479-102">Runspace01 (C#) – Kódminta</span><span class="sxs-lookup"><span data-stu-id="22479-102">Runspace01 (C#) Code Sample</span></span>

<span data-ttu-id="22479-103">Íme a mintakódokat, a futási térben ismertetett [létrehozása egy Console Application, hogy fut a megadott parancs](http://msdn.microsoft.com/en-us/793a6570-a072-4799-840b-172f28ce620e).</span><span class="sxs-lookup"><span data-stu-id="22479-103">Here are the code samples for the runspace described in [Creating a Console Application That Runs a Specified Command](http://msdn.microsoft.com/en-us/793a6570-a072-4799-840b-172f28ce620e).</span></span> <span data-ttu-id="22479-104">Ehhez az alkalmazás hív meg egy futási teret, és ezután meghívja a parancsot.</span><span class="sxs-lookup"><span data-stu-id="22479-104">To do this, the application invokes a runspace, and then invokes a command.</span></span> <span data-ttu-id="22479-105">(Vegye figyelembe, hogy az alkalmazás nem ad meg futási térben konfigurációs adatokat, és nem, explicit módon hozza létre folyamat).</span><span class="sxs-lookup"><span data-stu-id="22479-105">(Note that this application does not specify runspace configuration information, nor does it explicitly create a pipeline).</span></span> <span data-ttu-id="22479-106">A parancs, amely meghívja a `Get-Process` parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="22479-106">The command that is invoked is the `Get-Process` cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="22479-107">Letöltheti a C# a futási teret a Microsoft Windows szoftverek fejlesztési Kit for Windows Vista és a Microsoft .NET Framework 3.0 futtatási összetevői forrásfájl (runspace01.cs).</span><span class="sxs-lookup"><span data-stu-id="22479-107">You can download the C# source file (runspace01.cs) for this runspace using the Microsoft Windows Software Development Kit for Windows Vista and Microsoft .NET Framework 3.0 Runtime Components.</span></span> <span data-ttu-id="22479-108">Letöltési útmutatás: [Windows PowerShell telepítése és a Windows PowerShell SDK letöltési](/powershell/developer/installing-the-windows-powershell-sdk).</span><span class="sxs-lookup"><span data-stu-id="22479-108">For download instructions, see [How to Install Windows PowerShell and Download the Windows PowerShell SDK](/powershell/developer/installing-the-windows-powershell-sdk).</span></span>
>
> <span data-ttu-id="22479-109">A letöltött forrásfájlok érhetők el a  **\<PowerShell-minták >** könyvtár.</span><span class="sxs-lookup"><span data-stu-id="22479-109">The downloaded source files are available in the **\<PowerShell Samples>** directory.</span></span>

## <a name="code-sample"></a><span data-ttu-id="22479-110">Kódminta</span><span class="sxs-lookup"><span data-stu-id="22479-110">Code Sample</span></span>

[!code-csharp[Runspace01.cs](../../powershell-sdk-samples/SDK-2.0/csharp/Runspace01/Runspace01.cs#L11-L62 "Runspace01.cs")]

## <a name="see-also"></a><span data-ttu-id="22479-111">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="22479-111">See Also</span></span>

[<span data-ttu-id="22479-112">Windows PowerShell programozói útmutató</span><span class="sxs-lookup"><span data-stu-id="22479-112">Windows PowerShell Programmer's Guide</span></span>](./windows-powershell-programmer-s-guide.md)

[<span data-ttu-id="22479-113">Windows PowerShell SDK</span><span class="sxs-lookup"><span data-stu-id="22479-113">Windows PowerShell SDK</span></span>](../windows-powershell-reference.md)