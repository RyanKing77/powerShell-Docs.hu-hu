---
ms.date: 06/12/2017
author: JKeithB
ms.topic: reference
keywords: WMF, powershell, beállítás
ms.openlocfilehash: 91c115c7f0553cd5edf7fecf04e6a5c71c0a1aa2
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="new-guid"></a><span data-ttu-id="cb805-102">New-Guid</span><span class="sxs-lookup"><span data-stu-id="cb805-102">New-Guid</span></span>
<span data-ttu-id="cb805-103">Gyakran parancsfájl (vagy lehet, hogy a DSC-erőforrás írása), az egyedi azonosító szükséges.</span><span class="sxs-lookup"><span data-stu-id="cb805-103">Often script (or perhaps writing a DSC resource), you have the need for a unique identifier.</span></span> <span data-ttu-id="cb805-104">GUID azonosítók működőképesek, és hívni a .NET-keretrendszer Guid osztályt hozhat létre egy egyszerű, de munkája parancsmag válik, ez több felderíthető végfelhasználók számára, akik még nem ismeri a .NET-keretrendszer osztály:</span><span class="sxs-lookup"><span data-stu-id="cb805-104">GUIDs work well, and it is easy to call the .NET Framework Guid class to generate one, but having a cmdlet makes this more discoverable for end users who are not already familiar with the .NET Framework class:</span></span>

<span data-ttu-id="cb805-105">PS C:\\ &gt; új Guid</span><span class="sxs-lookup"><span data-stu-id="cb805-105">PS C:\\&gt; New-Guid</span></span>

<span data-ttu-id="cb805-106">GUID</span><span class="sxs-lookup"><span data-stu-id="cb805-106">Guid</span></span>

----

<span data-ttu-id="cb805-107">e19d6ea5-3cc2-4db9-8095-0cdaed5a703d</span><span class="sxs-lookup"><span data-stu-id="cb805-107">e19d6ea5-3cc2-4db9-8095-0cdaed5a703d</span></span>