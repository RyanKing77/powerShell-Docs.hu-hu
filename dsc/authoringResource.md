---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "Egyéni Windows PowerShell kívánt állapot konfigurációs erőforrások létrehozása"
ms.openlocfilehash: 4751bcaab1996ee3164bd2a2f430c3b188712860
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 01/17/2018
---
# <a name="build-custom-windows-powershell-desired-state-configuration-resources"></a><span data-ttu-id="89461-103">Egyéni Windows PowerShell kívánt állapot konfigurációs erőforrások létrehozása</span><span class="sxs-lookup"><span data-stu-id="89461-103">Build Custom Windows PowerShell Desired State Configuration Resources</span></span>

> <span data-ttu-id="89461-104">Vonatkozik: A Windows PowerShell 4.0-s verzióját, a Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="89461-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="89461-105">Windows PowerShell kívánt állapot konfigurációs szolgáltatása (DSC) rendelkezik, amelyek segítségével konfigurálhatja a környezetében beépített erőforrások.</span><span class="sxs-lookup"><span data-stu-id="89461-105">Windows PowerShell Desired State Configuration (DSC) has built-in resources that you can use to configure your environment.</span></span> <span data-ttu-id="89461-106">(További információkért lásd: [beépített Windows PowerShell kívánt állapot konfigurációs erőforrások](builtInResource.md).) Ez a témakör áttekintést a szükséges erőforrások és az adott útmutatást és példákat témakörökre mutató hivatkozásokat tartalmaz.</span><span class="sxs-lookup"><span data-stu-id="89461-106">(For more information, see [Built-In Windows PowerShell Desired State Configuration Resources](builtInResource.md).) This topic provides an overview of developing resources and links to topics with specific information and examples.</span></span>

## <a name="dsc-resource-components"></a><span data-ttu-id="89461-107">A DSC-erőforrás összetevők</span><span class="sxs-lookup"><span data-stu-id="89461-107">DSC resource components</span></span>

<span data-ttu-id="89461-108">A DSC-erőforrás egy Windows PowerShell-modul.</span><span class="sxs-lookup"><span data-stu-id="89461-108">A DSC resource is a Windows PowerShell module.</span></span> <span data-ttu-id="89461-109">A modul az erőforrás a séma (a beállítható tulajdonságok definíciója) és a megvalósítás (a kódot, amely a tényleges munkát konfiguráció által meghatározott) is tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="89461-109">The module contains both the schema (the definition of the configurable properties) and the implementation (the code that does the actual work specified by a configuration) for the resource.</span></span> <span data-ttu-id="89461-110">A DSC-erőforrás séma meghatározása a MOF-fájlt, és végrehajtása egy szkriptmodulba hajtja végre.</span><span class="sxs-lookup"><span data-stu-id="89461-110">A DSC resource schema can be defined in a MOF file, and the implementation is performed by a script module.</span></span> <span data-ttu-id="89461-111">Kezdődő 5-ös verzió osztályokat PowerShell-támogatása, a séma és a megvalósítását is definiálható osztályban található.</span><span class="sxs-lookup"><span data-stu-id="89461-111">Beginning with the support of PowerShell classes in version 5, the schema and implementation can both be defined in a class.</span></span> <span data-ttu-id="89461-112">Az alábbi témakörök ismertetik részletesebben DSC erőforrások létrehozásához.</span><span class="sxs-lookup"><span data-stu-id="89461-112">The following topics describe in more detail how to create DSC resources.</span></span>

* [<span data-ttu-id="89461-113">Egyéni DSC-erőforrás MOF írása</span><span class="sxs-lookup"><span data-stu-id="89461-113">Writing a custom DSC resource with MOF</span></span>](authoringResourceMOF.md)
* [<span data-ttu-id="89461-114">A DSC-erőforrás végrehajtási C#</span><span class="sxs-lookup"><span data-stu-id="89461-114">Implementing a DSC resource in C#</span></span>](authoringResourceMofCS.md)
* [<span data-ttu-id="89461-115">A PowerShell osztályok egyéni DSC-erőforrás írása</span><span class="sxs-lookup"><span data-stu-id="89461-115">Writing a custom DSC resource with PowerShell classes</span></span>](authoringResourceClass.md)
* [<span data-ttu-id="89461-116">Összetett erőforrások: erőforrásként a DSC-konfiguráció használata</span><span class="sxs-lookup"><span data-stu-id="89461-116">Composite resources: Using a DSC configuration as a resource</span></span>](authoringResourceComposite.md)
* [<span data-ttu-id="89461-117">Az erőforrás-tervező eszközzel</span><span class="sxs-lookup"><span data-stu-id="89461-117">Using the Resource Designer tool</span></span>](authoringResourceMofDesigner.md)

