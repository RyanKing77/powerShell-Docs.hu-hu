---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: Egyéni Windows PowerShell Desired State Configuration erőforrások létrehozása
ms.openlocfilehash: 882b6efed4564d2354183d7472b301e1e1758335
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/14/2018
ms.locfileid: "53404165"
---
# <a name="build-custom-windows-powershell-desired-state-configuration-resources"></a><span data-ttu-id="92600-103">Egyéni Windows PowerShell Desired State Configuration erőforrások létrehozása</span><span class="sxs-lookup"><span data-stu-id="92600-103">Build Custom Windows PowerShell Desired State Configuration Resources</span></span>

> <span data-ttu-id="92600-104">Érvényes: Windows PowerShell 4.0-s, a Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="92600-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="92600-105">Windows PowerShell Desired State Configuration (DSC) rendelkezik beépített erőforrások, amelyek segítségével konfigurálja a környezetet.</span><span class="sxs-lookup"><span data-stu-id="92600-105">Windows PowerShell Desired State Configuration (DSC) has built-in resources that you can use to configure your environment.</span></span> <span data-ttu-id="92600-106">Ez a témakör áttekintést erőforrások és a konkrét információk és példák témakörökre mutató hivatkozásokat.</span><span class="sxs-lookup"><span data-stu-id="92600-106">This topic provides an overview of developing resources and links to topics with specific information and examples.</span></span>

## <a name="dsc-resource-components"></a><span data-ttu-id="92600-107">DSC-erőforrás összetevők</span><span class="sxs-lookup"><span data-stu-id="92600-107">DSC resource components</span></span>

<span data-ttu-id="92600-108">A DSC-erőforrás egy Windows PowerShell-modul.</span><span class="sxs-lookup"><span data-stu-id="92600-108">A DSC resource is a Windows PowerShell module.</span></span> <span data-ttu-id="92600-109">A modul tartalmazza a séma (a Tulajdonságok gyűjteményével-definíció) és a (a kódot, amely a megadott konfiguráció szerint a tényleges munkát) végrehajtása az erőforrás.</span><span class="sxs-lookup"><span data-stu-id="92600-109">The module contains both the schema (the definition of the configurable properties) and the implementation (the code that does the actual work specified by a configuration) for the resource.</span></span> <span data-ttu-id="92600-110">A DSC-erőforrás séma MOF-fájl lehet definiálni, és a egy szkriptmodulba végzi a megvalósítás.</span><span class="sxs-lookup"><span data-stu-id="92600-110">A DSC resource schema can be defined in a MOF file, and the implementation is performed by a script module.</span></span> <span data-ttu-id="92600-111">Verziótól kezdve a PowerShell-osztályok az 5-ös verzió támogatása, a séma és a megvalósítás is lehet definiálni egy osztályt.</span><span class="sxs-lookup"><span data-stu-id="92600-111">Beginning with the support of PowerShell classes in version 5, the schema and implementation can both be defined in a class.</span></span> <span data-ttu-id="92600-112">Az alábbi témakörök részletesen ismertetik a DSC-erőforrások létrehozása.</span><span class="sxs-lookup"><span data-stu-id="92600-112">The following topics describe in more detail how to create DSC resources.</span></span>

* [<span data-ttu-id="92600-113">MOF-egyéni DSC-erőforrás írása</span><span class="sxs-lookup"><span data-stu-id="92600-113">Writing a custom DSC resource with MOF</span></span>](authoringResourceMOF.md)
* [<span data-ttu-id="92600-114">A DSC erőforrás megvalósításaC#</span><span class="sxs-lookup"><span data-stu-id="92600-114">Implementing a DSC resource in C#</span></span>](authoringResourceMofCS.md)
* [<span data-ttu-id="92600-115">A PowerShell-osztályok egyéni DSC-erőforrás írása</span><span class="sxs-lookup"><span data-stu-id="92600-115">Writing a custom DSC resource with PowerShell classes</span></span>](authoringResourceClass.md)
* [<span data-ttu-id="92600-116">Összetett erőforrások: A DSC-konfiguráció használata erőforrásként</span><span class="sxs-lookup"><span data-stu-id="92600-116">Composite resources: Using a DSC configuration as a resource</span></span>](authoringResourceComposite.md)
* [<span data-ttu-id="92600-117">Az erőforrás-tervező eszköz használata</span><span class="sxs-lookup"><span data-stu-id="92600-117">Using the Resource Designer tool</span></span>](../authoringResourceMofDesigner.md)
