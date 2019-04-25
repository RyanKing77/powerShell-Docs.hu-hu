---
title: Hibával kapcsolatos információk megjelenítése |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 76fcc0c1-9795-45d3-a564-40f822b657b5
caps.latest.revision: 8
ms.openlocfilehash: 4bc8666ee9053eb368402c8644558f4fe2dcc9ee
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62068283"
---
# <a name="displaying-error-information"></a><span data-ttu-id="5921e-102">Hibaadatok megjelenítése</span><span class="sxs-lookup"><span data-stu-id="5921e-102">Displaying Error Information</span></span>

<span data-ttu-id="5921e-103">Ez a témakör ismerteti a módszereket, amelyben a felhasználók megjeleníthetik a hibával kapcsolatos információk.</span><span class="sxs-lookup"><span data-stu-id="5921e-103">This topic discusses the ways in which users can display error information.</span></span>

<span data-ttu-id="5921e-104">A parancsmag hibát észlel, ha a hiba adatait bemutatása, alapértelmezés szerint hasonló a következő hibakimenet.</span><span class="sxs-lookup"><span data-stu-id="5921e-104">When your cmdlet encounters an error, the presentation of the error information will, by default, resemble the following error output.</span></span>

```powershell
$ stop-service lanmanworkstation
You do not have sufficient permissions to stop the service Workstation.
```

<span data-ttu-id="5921e-105">Azonban felhasználók megtekinthetik hibák kategória szerint beállításával a `$ErrorView` változó `"CategoryView"`.</span><span class="sxs-lookup"><span data-stu-id="5921e-105">However, users can view errors by category by setting the `$ErrorView` variable to `"CategoryView"`.</span></span> <span data-ttu-id="5921e-106">Kategória nézet hibaüzenet helyett a hiba szabad szöveges leírása származó azon információkat jeleníti meg.</span><span class="sxs-lookup"><span data-stu-id="5921e-106">Category view displays specific information from the error record rather than a free-text description of the error.</span></span> <span data-ttu-id="5921e-107">Ez a nézet lehet hasznos, ha hibák vizsgálata hosszú listáját.</span><span class="sxs-lookup"><span data-stu-id="5921e-107">This view can be useful if you have a long list of errors to scan.</span></span> <span data-ttu-id="5921e-108">Kategória nézetben az előző hibaüzenet jelenik meg a következő.</span><span class="sxs-lookup"><span data-stu-id="5921e-108">In category view, the previous error message is displayed as follows.</span></span>

```powershell
$ $ErrorView = "CategoryView"
$ stop-service lanmanworkstation
CloseError: (System.ServiceProcess.ServiceController:ServiceController) [stop-service], ServiceCommandException
```

<span data-ttu-id="5921e-109">Hiba történt a kategóriák kapcsolatos további információkért lásd: [Windows PowerShell Hibarekordjainak](./windows-powershell-error-records.md).</span><span class="sxs-lookup"><span data-stu-id="5921e-109">For more information about error categories, see [Windows PowerShell Error Records](./windows-powershell-error-records.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="5921e-110">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="5921e-110">See Also</span></span>

[<span data-ttu-id="5921e-111">Windows PowerShell Hibarekordjainak</span><span class="sxs-lookup"><span data-stu-id="5921e-111">Windows PowerShell Error Records</span></span>](./windows-powershell-error-records.md)

[<span data-ttu-id="5921e-112">Egy Windows PowerShell-parancsmag írása</span><span class="sxs-lookup"><span data-stu-id="5921e-112">Writing a Windows PowerShell Cmdlet</span></span>](./writing-a-windows-powershell-cmdlet.md)
