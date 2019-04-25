---
title: Windows PowerShell API-minták |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 82df2cde-ba12-46d2-b6ec-da5455fd9b57
caps.latest.revision: 8
ms.openlocfilehash: a472f07cb24b0de8e5dcdfcaddd2802575318d7a
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62082583"
---
# <a name="windows-powershell-api-samples"></a><span data-ttu-id="6d55b-102">Windows PowerSheles API-minták</span><span class="sxs-lookup"><span data-stu-id="6d55b-102">Windows PowerShell API Samples</span></span>

<span data-ttu-id="6d55b-103">Ez a szakasz tartalmazza, amely bemutatja, hogyan hozhat létre, amelyek korlátozzák a funkciók futási terek, és hogyan aszinkron módon futtathat parancsokat a futási térben készlet használatával adja meg a futási terek mintakódot.</span><span class="sxs-lookup"><span data-stu-id="6d55b-103">This section includes sample code that shows how to create runspaces that restrict functionality, and how to asynchronously run commands by using a runspace pool to supply the runspaces.</span></span> <span data-ttu-id="6d55b-104">Microsoft Visual Studio segítségével hozzon létre egy konzolalkalmazást, majd a kódot bemásolhatja a témakörei ebben a szakaszban a gazdaalkalmazást.</span><span class="sxs-lookup"><span data-stu-id="6d55b-104">You can use Microsoft Visual Studio to create a console application and then copy the code from the topics in this section into your host application.</span></span>

## <a name="in-this-section"></a><span data-ttu-id="6d55b-105">A szakasz tartalma</span><span class="sxs-lookup"><span data-stu-id="6d55b-105">In This Section</span></span>

<span data-ttu-id="6d55b-106">[PowerShell01 minta](./windows-powershell01-sample.md) Ez a példa bemutatja, hogyan használhatja egy [System.Management.Automation.Runspaces.Initialsessionstate](/dotnet/api/System.Management.Automation.Runspaces.InitialSessionState) egy futási teret funkcióinak objektumot.</span><span class="sxs-lookup"><span data-stu-id="6d55b-106">[PowerShell01 Sample](./windows-powershell01-sample.md) This sample shows how to use an [System.Management.Automation.Runspaces.Initialsessionstate](/dotnet/api/System.Management.Automation.Runspaces.InitialSessionState) object to limit the functionality of a runspace.</span></span> <span data-ttu-id="6d55b-107">Ez a minta kimenete bemutatja, hogyan korlátozhatja a nyelvmód futási térben személyes parancsmag megjelölni, hozzáadása és eltávolítása parancsmagok és szolgáltatók, a proxy parancsot, és további hozzáadása.</span><span class="sxs-lookup"><span data-stu-id="6d55b-107">The output of this sample demonstrates how to restrict the language mode of the runspace, how to mark a cmdlet as private, how to add and remove cmdlets and providers, how to add a proxy command, and more.</span></span>

<span data-ttu-id="6d55b-108">[PowerShell02 minta](./windows-powershell02-sample.md) Ez a példa bemutatja, hogyan futtathat parancsokat aszinkron módon történik a futási terek futási térben készlet használatával.</span><span class="sxs-lookup"><span data-stu-id="6d55b-108">[PowerShell02 Sample](./windows-powershell02-sample.md) This sample shows how to run commands asynchronously by using the runspaces of a runspace pool.</span></span> <span data-ttu-id="6d55b-109">A minta parancsok álló listát hoz létre, és majd futtatja azokat a parancsokat, amíg a Windows PowerShell motor megnyílik egy futási teret a készletből, szükség esetén.</span><span class="sxs-lookup"><span data-stu-id="6d55b-109">The sample generates a list of commands, and then runs those commands while the Windows PowerShell engine opens a runspace from the pool when it is needed.</span></span>