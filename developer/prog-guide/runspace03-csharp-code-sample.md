---
title: RunSpace03 (C#) kód minta | Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 9ac8ab99-1856-4d6f-b30d-c0a18b8dd1fc
caps.latest.revision: 6
ms.openlocfilehash: 9afdb97b8ae2919f091ca5bacccedbe37c2e1584
ms.sourcegitcommit: 00083f07b13c73b86936e7d7307397df27c63c04
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/10/2019
ms.locfileid: "70848026"
---
# <a name="runspace03-c-code-sample"></a><span data-ttu-id="33a21-102">Runspace03 (C#) – Kódminta</span><span class="sxs-lookup"><span data-stu-id="33a21-102">RunSpace03 (C#) Code Sample</span></span>

<span data-ttu-id="33a21-103">Itt látható a C# "megadott parancsfájlt futtató konzolszoftver létrehozása" című témakörben ismertetett konzolos alkalmazás forráskódja.</span><span class="sxs-lookup"><span data-stu-id="33a21-103">Here is the C# source code for the console application described in "Creating a Console Application That Runs a Specified Script".</span></span> <span data-ttu-id="33a21-104">Ez a példa a [System. Management. Automation. Runspaceinvoke](/dotnet/api/System.Management.Automation.RunspaceInvoke) osztályt használja egy olyan parancsfájl végrehajtásához, amely lekéri a folyamat adatait a parancsfájlba átadott folyamat-nevek listájának használatával.</span><span class="sxs-lookup"><span data-stu-id="33a21-104">This sample uses the [System.Management.Automation.Runspaceinvoke](/dotnet/api/System.Management.Automation.RunspaceInvoke) class to execute a script that retrieves process information by using the list of process names passed into the script.</span></span> <span data-ttu-id="33a21-105">Bemutatja, hogyan adhatók át bemeneti objektumok egy parancsfájlnak, valamint hogyan lehet lekérdezni a hibákat, valamint a kimeneti objektumokat.</span><span class="sxs-lookup"><span data-stu-id="33a21-105">It shows how to pass input objects to a script and how to retrieve error objects as well as the output objects.</span></span>

> [!NOTE]
> <span data-ttu-id="33a21-106">A minta C# forrásfájljait (runspace03.cs) a Microsoft Windows szoftverfejlesztői készlettel töltheti le a Windows Vista és Microsoft .NET Framework 3,0 Runtime Components szolgáltatáshoz.</span><span class="sxs-lookup"><span data-stu-id="33a21-106">You can download the C# source file (runspace03.cs) for this sample using the Microsoft Windows Software Development Kit for Windows Vista and Microsoft .NET Framework 3.0 Runtime Components.</span></span> <span data-ttu-id="33a21-107">A letöltési utasításokért lásd: a [Windows PowerShell telepítése és a Windows POWERSHELL SDK letöltése](/powershell/developer/installing-the-windows-powershell-sdk).</span><span class="sxs-lookup"><span data-stu-id="33a21-107">For download instructions, see [How to Install Windows PowerShell and Download the Windows PowerShell SDK](/powershell/developer/installing-the-windows-powershell-sdk).</span></span>
> <span data-ttu-id="33a21-108">A letöltött forrásfájlok a  **\<PowerShell-minták >** könyvtárban érhetők el.</span><span class="sxs-lookup"><span data-stu-id="33a21-108">The downloaded source files are available in the **\<PowerShell Samples>** directory.</span></span>

## <a name="code-sample"></a><span data-ttu-id="33a21-109">Mintakód</span><span class="sxs-lookup"><span data-stu-id="33a21-109">Code Sample</span></span>

[!code-csharp[Runspace03.cs](../../powershell-sdk-samples/SDK-2.0/csharp/Runspace03/Runspace03.cs#L11-L88 "Runspace03.cs")]

## <a name="see-also"></a><span data-ttu-id="33a21-110">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="33a21-110">See Also</span></span>

[<span data-ttu-id="33a21-111">A Windows PowerShell programozói útmutatója</span><span class="sxs-lookup"><span data-stu-id="33a21-111">Windows PowerShell Programmer's Guide</span></span>](./windows-powershell-programmer-s-guide.md)

[<span data-ttu-id="33a21-112">Windows PowerShell SDK</span><span class="sxs-lookup"><span data-stu-id="33a21-112">Windows PowerShell SDK</span></span>](../windows-powershell-reference.md)