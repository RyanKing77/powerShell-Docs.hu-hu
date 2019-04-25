---
title: GetProc02 (VB.NET) mintakód |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: f3497546-5b3a-4e29-84ba-cd9747be64b3
caps.latest.revision: 6
ms.openlocfilehash: 821d0dd327529614322e446bfb30d128d1b6a7f3
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62081594"
---
# <a name="getproc02-vbnet-sample-code"></a><span data-ttu-id="76251-102">GetProc02 (VB.NET) Sample Code – mintakód</span><span class="sxs-lookup"><span data-stu-id="76251-102">GetProc02 (VB.NET) Sample Code</span></span>

<span data-ttu-id="76251-103">Az alábbi kód megvalósítását mutatja be egy `Get-Process` parancsmagot, amely elfogadja a parancssori bemenet.</span><span class="sxs-lookup"><span data-stu-id="76251-103">The following code shows the implementation of a `Get-Process` cmdlet that accepts command-line input.</span></span> <span data-ttu-id="76251-104">Figyelje meg, hogy ez a megvalósítás meghatározása egy `Name` paraméter lehetővé teszik a parancssori bemenet, és használja a [System.Management.Automation.Cmdlet.WriteObject%28System.Object%2CSystem.Boolean%29](/dotnet/api/System.Management.Automation.Cmdlet.WriteObject%28System.Object%2CSystem.Boolean%29) kimenetként, metódus a folyamat küld kimeneti mechanizmus objektumokat.</span><span class="sxs-lookup"><span data-stu-id="76251-104">Notice that this implementation defines a `Name` parameter to allow command-line input, and it uses the [System.Management.Automation.Cmdlet.WriteObject%28System.Object%2CSystem.Boolean%29](/dotnet/api/System.Management.Automation.Cmdlet.WriteObject%28System.Object%2CSystem.Boolean%29) method as the output mechanism for sending output objects to the pipeline.</span></span>

## <a name="code-sample"></a><span data-ttu-id="76251-105">Kódminta</span><span class="sxs-lookup"><span data-stu-id="76251-105">Code Sample</span></span>

<!-- TODO!!!: review snippet reference  [!CODE [Msh_samplesgetproc02#getproc02vball](Msh_samplesgetproc02#getproc02vball)]  -->

## <a name="see-also"></a><span data-ttu-id="76251-106">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="76251-106">See Also</span></span>

[<span data-ttu-id="76251-107">Windows PowerShell SDK</span><span class="sxs-lookup"><span data-stu-id="76251-107">Windows PowerShell SDK</span></span>](../windows-powershell-reference.md)