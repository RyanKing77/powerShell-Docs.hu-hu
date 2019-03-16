---
title: GetProc02 (C#) mintakód |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: e4e1eee3-316b-43a4-8a60-313391619be6
caps.latest.revision: 6
ms.openlocfilehash: 2ac4aea2fdefdfe86349c14fe9b87cd8c41db090
ms.sourcegitcommit: caac7d098a448232304c9d6728e7340ec7517a71
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/16/2019
ms.locfileid: "58054560"
---
# <a name="getproc02-c-sample-code"></a><span data-ttu-id="00a65-102">GetProc02 (C#) – mintakód</span><span class="sxs-lookup"><span data-stu-id="00a65-102">GetProc02 (C#) Sample Code</span></span>

<span data-ttu-id="00a65-103">Az alábbi kód megvalósítását mutatja be egy `Get-Process` parancsmagot, amely elfogadja a parancssori bemenet.</span><span class="sxs-lookup"><span data-stu-id="00a65-103">The following code shows the implementation of a `Get-Process` cmdlet that accepts command-line input.</span></span> <span data-ttu-id="00a65-104">Figyelje meg, hogy ez a megvalósítás meghatározása egy `Name` paraméter lehetővé teszik a parancssori bemenet, és használja a [System.Management.Automation.Cmdlet.WriteObject%28System.Object%2CSystem.Boolean%29](/dotnet/api/System.Management.Automation.Cmdlet.WriteObject%28System.Object%2CSystem.Boolean%29) kimenetként, metódus a folyamat küld kimeneti mechanizmus objektumokat.</span><span class="sxs-lookup"><span data-stu-id="00a65-104">Notice that this implementation defines a `Name` parameter to allow command-line input, and it uses the [System.Management.Automation.Cmdlet.WriteObject%28System.Object%2CSystem.Boolean%29](/dotnet/api/System.Management.Automation.Cmdlet.WriteObject%28System.Object%2CSystem.Boolean%29) method as the output mechanism for sending output objects to the pipeline.</span></span>

## <a name="code-sample"></a><span data-ttu-id="00a65-105">Kódminta</span><span class="sxs-lookup"><span data-stu-id="00a65-105">Code Sample</span></span>

[!code-csharp[GetProcessSample02.cs](../../powershell-sdk-samples/SDK-2.0/csharp/GetProcessSample02/GetProcessSample02.cs#L11-L76 "GetProcessSample02.cs")]

## <a name="see-also"></a><span data-ttu-id="00a65-106">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="00a65-106">See Also</span></span>

[<span data-ttu-id="00a65-107">Windows PowerShell SDK</span><span class="sxs-lookup"><span data-stu-id="00a65-107">Windows PowerShell SDK</span></span>](../windows-powershell-reference.md)