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
ms.openlocfilehash: a0a88ca517347a94fc81534caace6efa0f13fdd7
ms.sourcegitcommit: f60fa420bdc81db174e6168d3aeb11371e483162
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/20/2019
ms.locfileid: "67301573"
---
# <a name="getproc03-vbnet-sample-code"></a><span data-ttu-id="7e6c2-102">GetProc03 (VB.NET) Sample Code – mintakód</span><span class="sxs-lookup"><span data-stu-id="7e6c2-102">GetProc03 (VB.NET) Sample Code</span></span>

<span data-ttu-id="7e6c2-103">Az alábbi kód megvalósítását mutatja be egy `Get-Process` parancsmag, amely elfogadja a bemeneti vagyok.</span><span class="sxs-lookup"><span data-stu-id="7e6c2-103">The following code shows the implementation of a `Get-Process` cmdlet that can accept pipelined input.</span></span> <span data-ttu-id="7e6c2-104">Ez a megvalósítás meghatározása egy `Name` paraméter, amely elfogadja a folyamat bemeneti, folyamat adatait kérdezi le a helyi számítógép megadott neve alapján, és ezután a [WriteObject(System.Object,System.Boolean)](/dotnet/api/system.management.automation.cmdlet.writeobject?view=pscore-6.2.0#System_Management_Automation_Cmdlet_WriteObject_System_Object_System_Boolean_)metódus objektumok küld el a folyamat a kimeneti mechanizmusként.</span><span class="sxs-lookup"><span data-stu-id="7e6c2-104">This implementation defines a `Name` parameter that accepts pipeline input, retrieves process information from the local computer based on the supplied names, and then uses the [WriteObject(System.Object,System.Boolean)](/dotnet/api/system.management.automation.cmdlet.writeobject?view=pscore-6.2.0#System_Management_Automation_Cmdlet_WriteObject_System_Object_System_Boolean_) method as the output mechanism for sending objects to the pipeline.</span></span>

## <a name="code-sample"></a><span data-ttu-id="7e6c2-105">Kódminta</span><span class="sxs-lookup"><span data-stu-id="7e6c2-105">Code Sample</span></span>

<!-- TODO!!!: review snippet reference  [!CODE [Msh_samplesgetproc03#getproc03vbAll](Msh_samplesgetproc03#getproc03vbAll)]  -->
