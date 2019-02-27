---
title: Windows PowerShell02 minta |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 92492a7e-257d-47d3-b119-89df3c5545e8
caps.latest.revision: 9
ms.openlocfilehash: 89ad17257ebac56105a93672317a149515e80d32
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56850357"
---
# <a name="windows-powershell02-sample"></a><span data-ttu-id="0e8aa-102">Windows PowerShell02 – minta</span><span class="sxs-lookup"><span data-stu-id="0e8aa-102">Windows PowerShell02 Sample</span></span>

<span data-ttu-id="0e8aa-103">Ez a példa bemutatja, hogyan futtathat parancsokat aszinkron módon történik a futási terek futási térben készlet használatával.</span><span class="sxs-lookup"><span data-stu-id="0e8aa-103">This sample shows how to run commands asynchronously by using the runspaces of a runspace pool.</span></span> <span data-ttu-id="0e8aa-104">A minta parancsok álló listát hoz létre, és majd futtatja azokat a parancsokat, amíg a Windows PowerShell motor megnyílik egy futási teret a készletből, szükség esetén.</span><span class="sxs-lookup"><span data-stu-id="0e8aa-104">The sample generates a list of commands, and then runs those commands while the Windows PowerShell engine opens a runspace from the pool when it is needed.</span></span>

## <a name="requirements"></a><span data-ttu-id="0e8aa-105">Követelmények</span><span class="sxs-lookup"><span data-stu-id="0e8aa-105">Requirements</span></span>

- <span data-ttu-id="0e8aa-106">Ez a minta Windows PowerShell 2.0 szükséges.</span><span class="sxs-lookup"><span data-stu-id="0e8aa-106">This sample requires Windows PowerShell 2.0.</span></span>

## <a name="demonstrates"></a><span data-ttu-id="0e8aa-107">Bemutatók</span><span class="sxs-lookup"><span data-stu-id="0e8aa-107">Demonstrates</span></span>

<span data-ttu-id="0e8aa-108">Ez a minta bemutatja a következőket:</span><span class="sxs-lookup"><span data-stu-id="0e8aa-108">This sample demonstrates the following:</span></span>

- <span data-ttu-id="0e8aa-109">Egy RunspacePool objektum létrehozása a futási terek nyitható meg egyszerre engedélyezett minimális és maximális számát.</span><span class="sxs-lookup"><span data-stu-id="0e8aa-109">Creating a RunspacePool object with a minimum and maximum number of runspaces allowed to be open at the same time.</span></span>

- <span data-ttu-id="0e8aa-110">Létrehoz egy listát az parancsokat.</span><span class="sxs-lookup"><span data-stu-id="0e8aa-110">Creating a list of commands.</span></span>

- <span data-ttu-id="0e8aa-111">A parancsok aszinkron módon fut.</span><span class="sxs-lookup"><span data-stu-id="0e8aa-111">Running the commands asynchronously.</span></span>

- <span data-ttu-id="0e8aa-112">Hívása a [System.Management.Automation.Runspaces.Runspacepool.Getavailablerunspaces\*](/dotnet/api/System.Management.Automation.Runspaces.RunspacePool.GetAvailableRunspaces) metódus ingyenes hány futási terek megtekintéséhez.</span><span class="sxs-lookup"><span data-stu-id="0e8aa-112">Calling the [System.Management.Automation.Runspaces.Runspacepool.Getavailablerunspaces\*](/dotnet/api/System.Management.Automation.Runspaces.RunspacePool.GetAvailableRunspaces) method to see how many runspaces are free.</span></span>

- <span data-ttu-id="0e8aa-113">A parancs kimenete a rögzítés a [System.Management.Automation.Powershell.Endinvoke\*](/dotnet/api/System.Management.Automation.PowerShell.EndInvoke) metódust.</span><span class="sxs-lookup"><span data-stu-id="0e8aa-113">Capturing the command output with the [System.Management.Automation.Powershell.Endinvoke\*](/dotnet/api/System.Management.Automation.PowerShell.EndInvoke) method.</span></span>

## <a name="example"></a><span data-ttu-id="0e8aa-114">Példa</span><span class="sxs-lookup"><span data-stu-id="0e8aa-114">Example</span></span>

<span data-ttu-id="0e8aa-115">Ez a példa bemutatja, hogyan lehet megnyitni a futási terek futási térben készlet, és hogyan aszinkron módon futtathat parancsokat a ezeket futási terek.</span><span class="sxs-lookup"><span data-stu-id="0e8aa-115">This sample shows how to open the runspaces of a runspace pool, and how to asynchronously run commands in those runspaces.</span></span>

[!code-csharp[PowerShell02.cs](../../powershell-sdk-samples/SDK-2.0/csharp/PowerShell02/PowerShell02.cs#L11-L96 "PowerShell02.cs")]

## <a name="see-also"></a><span data-ttu-id="0e8aa-116">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="0e8aa-116">See Also</span></span>

[<span data-ttu-id="0e8aa-117">A Windows PowerShell-gazdagépet alkalmazás írása</span><span class="sxs-lookup"><span data-stu-id="0e8aa-117">Writing a Windows PowerShell Host Application</span></span>](./writing-a-windows-powershell-host-application.md)