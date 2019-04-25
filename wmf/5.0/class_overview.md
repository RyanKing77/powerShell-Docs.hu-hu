---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: 5919a68c87ae8827a1b97befc653bb74713f33fe
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62085779"
---
# <a name="creating-custom-types-using-powershell-classes"></a><span data-ttu-id="85402-102">Egyéni típusok létrehozása PowerShell-osztályokkal</span><span class="sxs-lookup"><span data-stu-id="85402-102">Creating Custom Types using PowerShell Classes</span></span>

<span data-ttu-id="85402-103">Továbbfejlesztettük a PowerShell nyelv osztályok és a többi felhasználó által meghatározott típusok definiálása formális szintaxist és a hasonló más objektumorientált programozási nyelveket szemantika használatával.</span><span class="sxs-lookup"><span data-stu-id="85402-103">We’ve improved the PowerShell language for defining classes and other user-defined types by using formal syntax and semantics that are similar to other object-oriented programming languages.</span></span> <span data-ttu-id="85402-104">A cél, hogy a fejlesztők és informatikai szakemberek PowerShell kihasználni a használati esetek szélesebb köre, leegyszerűsítheti a fejlesztést az PowerShell-összetevők (például a DSC-erőforrások) és gyorsítsa fel a felügyeleti felületek lefedettség engedélyezése.</span><span class="sxs-lookup"><span data-stu-id="85402-104">The goal is to enable developers and IT professionals to embrace PowerShell for a wider range of use cases, simplify development of PowerShell artifacts (such as DSC resources), and accelerate coverage of management surfaces.</span></span>

## <a name="supported-scenarios-in-this-release"></a><span data-ttu-id="85402-105">Ebben a kiadásban támogatott helyzetek</span><span class="sxs-lookup"><span data-stu-id="85402-105">Supported scenarios in this release</span></span>

-   <span data-ttu-id="85402-106">DSC-erőforrások és az azokhoz társított típusokat megadása a PowerShell nyelv segítségével</span><span class="sxs-lookup"><span data-stu-id="85402-106">Define DSC resources and their associated types by using the PowerShell language</span></span>
-   <span data-ttu-id="85402-107">Egyéni típusok definiálása a PowerShellben a jól ismert objektumorientált programozási módszerek, például az osztályokat, tulajdonságokat, módszerek használatával.</span><span class="sxs-lookup"><span data-stu-id="85402-107">Define custom types in PowerShell by using familiar object-oriented programming constructs, such as classes, properties, methods, etc.</span></span>
-   <span data-ttu-id="85402-108">Öröklés támogatására az osztály a PowerShell és az osztály base DSC-erőforrás</span><span class="sxs-lookup"><span data-stu-id="85402-108">Inheritance support with class in PowerShell and class base DSC resource</span></span>
-   <span data-ttu-id="85402-109">Típusok hibakeresés a PowerShell nyelv használatával</span><span class="sxs-lookup"><span data-stu-id="85402-109">Debug types by using the PowerShell language</span></span>
-   <span data-ttu-id="85402-110">Hozzon létre, és a kivételek kezelésére, formális mechanizmusok használatával, és a megfelelő szinten</span><span class="sxs-lookup"><span data-stu-id="85402-110">Generate and handle exceptions by using formal mechanisms, and at the right level</span></span>
