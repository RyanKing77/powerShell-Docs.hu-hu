---
title: A parancsmag kimenete |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 1362f4cd-4e05-4ace-ade6-7128da8ad86c
caps.latest.revision: 10
ms.openlocfilehash: 4c6aacd49b0a87bca6806ba5f08a1b4d48a90959
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56845282"
---
# <a name="cmdlet-output"></a><span data-ttu-id="a9658-102">Parancsmagkimenet</span><span class="sxs-lookup"><span data-stu-id="a9658-102">Cmdlet Output</span></span>

<span data-ttu-id="a9658-103">Ez a szakasz bemutatja, milyen parancsmag kimenete és a módszereket, a parancsmagok segítségével meghívhatja a kimenet például a hibaüzeneteket és objektumok létrehozásához.</span><span class="sxs-lookup"><span data-stu-id="a9658-103">This section discusses the types of cmdlet output and the methods that cmdlets can call to generate output such as error messages and objects.</span></span> <span data-ttu-id="a9658-104">A szakasz emellett ismerteti, hogyan adhat meg a .NET-keretrendszer típusok, a parancsmag által visszaadott, és hogyan jelennek meg ezek az objektumok.</span><span class="sxs-lookup"><span data-stu-id="a9658-104">This section also describes how to define the .NET Framework types that are returned by your cmdlets and how those objects are displayed.</span></span>

## <a name="in-this-section"></a><span data-ttu-id="a9658-105">A szakasz tartalma</span><span class="sxs-lookup"><span data-stu-id="a9658-105">In This Section</span></span>

<span data-ttu-id="a9658-106">[A parancsmag kimenete típusú](./types-of-cmdlet-output.md) típusok és kimenete a parancsmagok hozhat létre és a parancsmagok hívja a kimenet előállítása módszereket ismerteti.</span><span class="sxs-lookup"><span data-stu-id="a9658-106">[Types of Cmdlet Output](./types-of-cmdlet-output.md) Describes the types and output that cmdlets can generate and the methods that cmdlets call to generate the output.</span></span>

<span data-ttu-id="a9658-107">[A parancsmag hibajelentés](./cmdlet-error-reporting.md) parancsmag hibajelentést küldő, a parancsmag kimenete egy részét tárgyalja.</span><span class="sxs-lookup"><span data-stu-id="a9658-107">[Cmdlet Error Reporting](./cmdlet-error-reporting.md) Discusses cmdlet error reporting, a subset of cmdlet output.</span></span>

<span data-ttu-id="a9658-108">[Kimeneti objektumok kiterjesztése](./extending-output-objects.md) parancsmagok, függvények és parancsfájlok a típusok fájlok (.ps1xml) segítségével kiterjesztheti a .NET keretrendszer objektumait visszaadott ismerteti.</span><span class="sxs-lookup"><span data-stu-id="a9658-108">[Extending Output Objects](./extending-output-objects.md) Discusses how to use the types files (.ps1xml) to extend the .NET Framework objects that are returned by cmdlets, functions, and scripts.</span></span>

<span data-ttu-id="a9658-109">[PowerShell formázás fájlok](../format/powershell-formatting-files.md) formázási fájlokat ismerteti (. format.ps1xml) fájlok, amelyek meghatározzák az alapértelmezett jeleníti meg a Windows PowerShellben .NET-keretrendszer objektumok egy adott készletét.</span><span class="sxs-lookup"><span data-stu-id="a9658-109">[PowerShell Formatting Files](../format/powershell-formatting-files.md) Describes the formatting files (.format.ps1xml) files that define the default display for a specific set of .NET Framework objects in Windows PowerShell.</span></span>

<span data-ttu-id="a9658-110">[Egyéni formázás fájlok](./custom-formatting-files.md) ismerteti, hogyan hozhat létre saját egyéni formázás felülírja az alapértelmezett fájlok megjelenítése a formátumok, illetve a saját parancsok által visszaadott objektumok megjelenítéséhez meghatározásához.</span><span class="sxs-lookup"><span data-stu-id="a9658-110">[Custom Formatting Files](./custom-formatting-files.md) Describes how to create your own custom formatting files to overwrite the default display formats or to define the display of objects returned by your own commands.</span></span>

## <a name="see-also"></a><span data-ttu-id="a9658-111">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="a9658-111">See Also</span></span>

[<span data-ttu-id="a9658-112">Egy Windows PowerShell-parancsmag írása</span><span class="sxs-lookup"><span data-stu-id="a9658-112">Writing a Windows PowerShell Cmdlet</span></span>](./writing-a-windows-powershell-cmdlet.md)
