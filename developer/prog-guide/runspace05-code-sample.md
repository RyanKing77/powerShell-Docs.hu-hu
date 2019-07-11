---
title: Kódminta RunSpace05 |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 9688cd69-07ea-4ea0-8822-0a4850bcf86c
caps.latest.revision: 7
ms.openlocfilehash: abf19d848f6150d005c63bb0fc2ffbe1de405e2a
ms.sourcegitcommit: 46bebe692689ebedfe65ff2c828fe666b443198d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/10/2019
ms.locfileid: "67734971"
---
# <a name="runspace05-code-sample"></a><span data-ttu-id="d3ebc-102">Runspace05 – Kódminta</span><span class="sxs-lookup"><span data-stu-id="d3ebc-102">RunSpace05 Code Sample</span></span>

<span data-ttu-id="d3ebc-103">Íme a forráskódot a Runspace05 minta leírt [konfigurálása a futási teret használ RunspaceConfiguration](https://msdn.microsoft.com/en-us/42681d19-2d05-4975-befd-afb1990e79b2).</span><span class="sxs-lookup"><span data-stu-id="d3ebc-103">Here is the source code for the Runspace05 sample that is described in [Configuring a Runspace Using RunspaceConfiguration](https://msdn.microsoft.com/en-us/42681d19-2d05-4975-befd-afb1990e79b2).</span></span> <span data-ttu-id="d3ebc-104">Ez a példa bemutatja, hogyan létrehozása a futási térben konfigurációs adatokat, hozzon létre egy futási teret, hozzon létre egy folyamatot egyetlen paranccsal és ezután hajtsa végre a folyamat.</span><span class="sxs-lookup"><span data-stu-id="d3ebc-104">This sample shows how to create the runspace configuration information, create a runspace, create a pipeline with a single command, and then execute the pipeline.</span></span> <span data-ttu-id="d3ebc-105">A végrehajtott parancs a `Get-Process` parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="d3ebc-105">The command that is executed is the `Get-Process` cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="d3ebc-106">Letöltheti a C# forrásfájl (runspace05.cs) a Microsoft Windows szoftverek fejlesztési Kit for Windows Vista és a Microsoft .NET Framework 3.0 futtatási összetevői.</span><span class="sxs-lookup"><span data-stu-id="d3ebc-106">You can download the C# source file (runspace05.cs) by using the Microsoft Windows Software Development Kit for Windows Vista and Microsoft .NET Framework 3.0 Runtime Components.</span></span> <span data-ttu-id="d3ebc-107">Letöltési útmutatás: [Windows PowerShell telepítése és a Windows PowerShell SDK letöltési](/powershell/developer/installing-the-windows-powershell-sdk).</span><span class="sxs-lookup"><span data-stu-id="d3ebc-107">For download instructions, see [How to Install Windows PowerShell and Download the Windows PowerShell SDK](/powershell/developer/installing-the-windows-powershell-sdk).</span></span>
>
> <span data-ttu-id="d3ebc-108">A letöltött forrásfájlok érhetők el a  **\<PowerShell-minták >** könyvtár.</span><span class="sxs-lookup"><span data-stu-id="d3ebc-108">The downloaded source files are available in the **\<PowerShell Samples>** directory.</span></span>

## <a name="code-sample"></a><span data-ttu-id="d3ebc-109">Kódminta</span><span class="sxs-lookup"><span data-stu-id="d3ebc-109">Code Sample</span></span>

[!code-csharp[Runspace05.cs](../../powershell-sdk-samples/SDK-2.0/csharp/Runspace05/Runspace05.cs#L11-L86 "Runspace05.cs")]

## <a name="see-also"></a><span data-ttu-id="d3ebc-110">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="d3ebc-110">See Also</span></span>

[<span data-ttu-id="d3ebc-111">Windows PowerShell programozói útmutató</span><span class="sxs-lookup"><span data-stu-id="d3ebc-111">Windows PowerShell Programmer's Guide</span></span>](./windows-powershell-programmer-s-guide.md)

[<span data-ttu-id="d3ebc-112">Windows PowerShell SDK</span><span class="sxs-lookup"><span data-stu-id="d3ebc-112">Windows PowerShell SDK</span></span>](../windows-powershell-reference.md)