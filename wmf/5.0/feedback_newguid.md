---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: 90fd26f9f27d2398da839b309c17b921bb3b8521
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62085326"
---
# <a name="new-guid"></a><span data-ttu-id="87351-102">New-Guid</span><span class="sxs-lookup"><span data-stu-id="87351-102">New-Guid</span></span>
<span data-ttu-id="87351-103">Gyakran a parancsfájl (vagy akár a DSC-erőforrás írása), nincs szüksége az egyedi azonosítója.</span><span class="sxs-lookup"><span data-stu-id="87351-103">Often script (or perhaps writing a DSC resource), you have the need for a unique identifier.</span></span> <span data-ttu-id="87351-104">GUID-azonosítói megfelelően működjön, és hívja meg a .NET-keretrendszer Guid osztályt hozhat létre egy egyszerű, de kellene parancsmag segítségével könnyebben felfedezhetővé teheti a végfelhasználók számára, akik még nem ismeri a .NET-keretrendszer osztály:</span><span class="sxs-lookup"><span data-stu-id="87351-104">GUIDs work well, and it is easy to call the .NET Framework Guid class to generate one, but having a cmdlet makes this more discoverable for end users who are not already familiar with the .NET Framework class:</span></span>

<span data-ttu-id="87351-105">PS C:\\&gt; New-Guid</span><span class="sxs-lookup"><span data-stu-id="87351-105">PS C:\\&gt; New-Guid</span></span>

<span data-ttu-id="87351-106">Guid</span><span class="sxs-lookup"><span data-stu-id="87351-106">Guid</span></span>

----

<span data-ttu-id="87351-107">e19d6ea5-3cc2-4db9-8095-0cdaed5a703d</span><span class="sxs-lookup"><span data-stu-id="87351-107">e19d6ea5-3cc2-4db9-8095-0cdaed5a703d</span></span>
