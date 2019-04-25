---
title: GetProc03 (VB.NET) mintakód |} A Microsoft Docs
ms.custom: ''
ms.date: 09/12/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: ff94c452-d4ec-4492-ac20-61ad52f8ae8c
caps.latest.revision: 7
ms.openlocfilehash: 0cfb5c203c97a4d20e7fadf8183e608e9e31b881
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62081648"
---
# <a name="getproc03-vbnet-sample-code"></a><span data-ttu-id="3ccad-102">GetProc03 (VB.NET) Sample Code – mintakód</span><span class="sxs-lookup"><span data-stu-id="3ccad-102">GetProc03 (VB.NET) Sample Code</span></span>

<span data-ttu-id="3ccad-103">Az alábbi kód megvalósítását mutatja be egy `Get-Process` parancsmag, amely elfogadja a bemeneti vagyok.</span><span class="sxs-lookup"><span data-stu-id="3ccad-103">The following code shows the implementation of a `Get-Process` cmdlet that can accept pipelined input.</span></span> <span data-ttu-id="3ccad-104">Ez a megvalósítás meghatározása egy `Name` paraméter, amely elfogadja a folyamat bemeneti, folyamat adatait kérdezi le a helyi számítógép megadott neve alapján, és ezután a [System.Management.Automation.Cmdlet.WriteObject% 28System.Object%2CSystem.Boolean%29](/dotnet/api/System.Management.Automation.Cmdlet.WriteObject%28System.Object%2CSystem.Boolean%29) metódus objektumok küld el a folyamat a kimeneti mechanizmusként.</span><span class="sxs-lookup"><span data-stu-id="3ccad-104">This implementation defines a `Name` parameter that accepts pipeline input, retrieves process information from the local computer based on the supplied names, and then uses the [System.Management.Automation.Cmdlet.WriteObject%28System.Object%2CSystem.Boolean%29](/dotnet/api/System.Management.Automation.Cmdlet.WriteObject%28System.Object%2CSystem.Boolean%29) method as the output mechanism for sending objects to the pipeline.</span></span>

## <a name="code-sample"></a><span data-ttu-id="3ccad-105">Kódminta</span><span class="sxs-lookup"><span data-stu-id="3ccad-105">Code Sample</span></span>

<!-- TODO!!!: review snippet reference  [!CODE [Msh_samplesgetproc03#getproc03vbAll](Msh_samplesgetproc03#getproc03vbAll)]  -->