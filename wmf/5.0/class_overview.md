---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "WMF, a powershell, a beállítása"
ms.openlocfilehash: 8b414331bbfb7dc71d960241a6bc83b0b22641db
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2017
---
# <a name="creating-custom-types-using-powershell-classes"></a><span data-ttu-id="633f5-102">Egyéni típusok PowerShell osztályokat létrehozása</span><span class="sxs-lookup"><span data-stu-id="633f5-102">Creating Custom Types using PowerShell Classes</span></span>

<span data-ttu-id="633f5-103">Azt is javult a PowerShell nyelvi osztályok és más felhasználó által definiált típusok meghatározásához formális szintaxisát és egyéb objektumorientált programozási nyelvek hasonló szemantika használatával.</span><span class="sxs-lookup"><span data-stu-id="633f5-103">We’ve improved the PowerShell language for defining classes and other user-defined types by using formal syntax and semantics that are similar to other object-oriented programming languages.</span></span> <span data-ttu-id="633f5-104">A cél, hogy engedélyezze a fejlesztők és informatikai szakemberek számára bevezetni a PowerShell szélesebb köre által használati esetek, fejlesztési PowerShell összetevők (például a DSC) egyszerűbbé és felgyorsítani felügyeleti felületek körét.</span><span class="sxs-lookup"><span data-stu-id="633f5-104">The goal is to enable developers and IT professionals to embrace PowerShell for a wider range of use cases, simplify development of PowerShell artifacts (such as DSC resources), and accelerate coverage of management surfaces.</span></span>

## <a name="supported-scenarios-in-this-release"></a><span data-ttu-id="633f5-105">Ez a kiadás támogatott helyzetek</span><span class="sxs-lookup"><span data-stu-id="633f5-105">Supported scenarios in this release</span></span>

-   <span data-ttu-id="633f5-106">Adja meg a DSC-erőforrások és a kapcsolódó típusukat a PowerShell nyelv használatával</span><span class="sxs-lookup"><span data-stu-id="633f5-106">Define DSC resources and their associated types by using the PowerShell language</span></span>
-   <span data-ttu-id="633f5-107">Egyéni típusainak definiálása a PowerShell használatával a megszokott objektumorientált programozási módszerek, például az osztályokat, tulajdonságokat, módszerek, stb.</span><span class="sxs-lookup"><span data-stu-id="633f5-107">Define custom types in PowerShell by using familiar object-oriented programming constructs, such as classes, properties, methods, etc.</span></span>
-   <span data-ttu-id="633f5-108">A PowerShell és az osztály base DSC erőforrás osztály öröklési támogatása</span><span class="sxs-lookup"><span data-stu-id="633f5-108">Inheritance support with class in PowerShell and class base DSC resource</span></span>
-   <span data-ttu-id="633f5-109">Debug típusok a PowerShell nyelv használatával</span><span class="sxs-lookup"><span data-stu-id="633f5-109">Debug types by using the PowerShell language</span></span>
-   <span data-ttu-id="633f5-110">Létrehozni és kezelni a kivételek formális mechanizmusok használatával, és a megfelelő szintű</span><span class="sxs-lookup"><span data-stu-id="633f5-110">Generate and handle exceptions by using formal mechanisms, and at the right level</span></span>

