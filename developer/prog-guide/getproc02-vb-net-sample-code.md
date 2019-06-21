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
ms.openlocfilehash: 4ec63ed32bd2906f5b027523aa0f253b51a5d873
ms.sourcegitcommit: f60fa420bdc81db174e6168d3aeb11371e483162
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/20/2019
ms.locfileid: "67301348"
---
# <a name="getproc02-vbnet-sample-code"></a><span data-ttu-id="74e9d-102">GetProc02 (VB.NET) Sample Code – mintakód</span><span class="sxs-lookup"><span data-stu-id="74e9d-102">GetProc02 (VB.NET) Sample Code</span></span>

<span data-ttu-id="74e9d-103">Az alábbi kód megvalósítását mutatja be egy `Get-Process` parancsmagot, amely elfogadja a parancssori bemenet.</span><span class="sxs-lookup"><span data-stu-id="74e9d-103">The following code shows the implementation of a `Get-Process` cmdlet that accepts command-line input.</span></span> <span data-ttu-id="74e9d-104">Figyelje meg, hogy ez a megvalósítás meghatározása egy `Name` paraméter lehetővé teszik a parancssori bemenet, és használja a [WriteObject(System.Object,System.Boolean)](/dotnet/api/system.management.automation.cmdlet.writeobject?view=pscore-6.2.0#System_Management_Automation_Cmdlet_WriteObject_System_Object_System_Boolean_) objektumok kimenetet küld kimeneti mechanizmusként metódus az folyamat.</span><span class="sxs-lookup"><span data-stu-id="74e9d-104">Notice that this implementation defines a `Name` parameter to allow command-line input, and it uses the [WriteObject(System.Object,System.Boolean)](/dotnet/api/system.management.automation.cmdlet.writeobject?view=pscore-6.2.0#System_Management_Automation_Cmdlet_WriteObject_System_Object_System_Boolean_) method as the output mechanism for sending output objects to the pipeline.</span></span>

## <a name="code-sample"></a><span data-ttu-id="74e9d-105">Kódminta</span><span class="sxs-lookup"><span data-stu-id="74e9d-105">Code Sample</span></span>

<!-- TODO!!!: review snippet reference  [!CODE [Msh_samplesgetproc02#getproc02vball](Msh_samplesgetproc02#getproc02vball)]  -->

## <a name="see-also"></a><span data-ttu-id="74e9d-106">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="74e9d-106">See Also</span></span>

[<span data-ttu-id="74e9d-107">Windows PowerShell SDK</span><span class="sxs-lookup"><span data-stu-id="74e9d-107">Windows PowerShell SDK</span></span>](../windows-powershell-reference.md)
