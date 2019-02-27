---
title: Runspace02 (C#) kódminta |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 59a7b8b9-f72e-43fd-9a10-77404441a3f2
caps.latest.revision: 6
ms.openlocfilehash: 0a8fc05db74529e2bfb88820b9cfd988245e0aeb
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56845842"
---
# <a name="runspace02-c-code-sample"></a><span data-ttu-id="8f931-102">Runspace02 (C#) – Kódminta</span><span class="sxs-lookup"><span data-stu-id="8f931-102">Runspace02 (C#) Code Sample</span></span>

<span data-ttu-id="8f931-103">Íme a C# forráskódját a Runspace02 minta.</span><span class="sxs-lookup"><span data-stu-id="8f931-103">Here is the C# source code for the Runspace02 sample.</span></span> <span data-ttu-id="8f931-104">Ebben a példában a [System.Management.Automation.Runspaceinvoke](/dotnet/api/System.Management.Automation.RunspaceInvoke) végrehajtásához az osztály a `Get-Process` parancsmag szinkron módon történik.</span><span class="sxs-lookup"><span data-stu-id="8f931-104">This sample uses the [System.Management.Automation.Runspaceinvoke](/dotnet/api/System.Management.Automation.RunspaceInvoke) class to execute the `Get-Process` cmdlet synchronously.</span></span> <span data-ttu-id="8f931-105">Windows Forms- és adatkötés majd használni az eredmények megjelennek egy vezérlő</span><span class="sxs-lookup"><span data-stu-id="8f931-105">Windows Forms and data binding are then used to display the results in a DataGridView control</span></span>

## <a name="code-sample"></a><span data-ttu-id="8f931-106">Kódminta</span><span class="sxs-lookup"><span data-stu-id="8f931-106">Code Sample</span></span>

[!code-csharp[Runspace02.cs](../../powershell-sdk-samples/SDK-2.0/csharp/Runspace02/Runspace02.cs#L11-L82 "Runspace02.cs")]

## <a name="see-also"></a><span data-ttu-id="8f931-107">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="8f931-107">See Also</span></span>

[<span data-ttu-id="8f931-108">Windows PowerShell SDK</span><span class="sxs-lookup"><span data-stu-id="8f931-108">Windows PowerShell SDK</span></span>](../windows-powershell-reference.md)