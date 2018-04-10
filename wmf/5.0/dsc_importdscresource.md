---
ms.date: 06/12/2017
author: JKeithB
ms.topic: reference
keywords: WMF, powershell, beállítás
ms.openlocfilehash: a3b176101bebf7081febd8629bddcfa0ae1e7540
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="import-dscresource-keyword-supports--moduleversion-parameter"></a><span data-ttu-id="2a02f-102">Importálás – DscResource kulcsszó - ModuleVersion paraméter támogatja</span><span class="sxs-lookup"><span data-stu-id="2a02f-102">Import-DscResource keyword supports -ModuleVersion parameter</span></span>

<span data-ttu-id="2a02f-103">Egy új paraméter jelentek meg a `Import-DscResource` érhető el, ha a DSC-konfigurációk szerzői dinamikus kulcsszó.</span><span class="sxs-lookup"><span data-stu-id="2a02f-103">We have added a new parameter to the `Import-DscResource` dynamic keyword available when authoring DSC configurations.</span></span> <span data-ttu-id="2a02f-104">Konfigurációs szerzők mostantól megadhatja, hogy pontosan melyik verziója a DSC-erőforrások betöltése.</span><span class="sxs-lookup"><span data-stu-id="2a02f-104">Configuration authors can now specify exactly which module version to load the DSC resources from.</span></span> <span data-ttu-id="2a02f-105">A kulcsszó új szintaxisa:</span><span class="sxs-lookup"><span data-stu-id="2a02f-105">The new syntax of the keyword is:</span></span>

```powershell
Import-DscResource [-Name <ResourceName(s)>] [-ModuleName <ModuleName(s)>] [-ModuleVersion <ModuleVersion>]
```

* <span data-ttu-id="2a02f-106">**Név**: egy vagy több erőforrás importálása nevét.</span><span class="sxs-lookup"><span data-stu-id="2a02f-106">**Name**: Names of one or more resources to import.</span></span>
* <span data-ttu-id="2a02f-107">**Modulnév**: modulneveket vagy ModuleSpecification objektumok importálása egy vagy több modulja.</span><span class="sxs-lookup"><span data-stu-id="2a02f-107">**ModuleName**: Module names or ModuleSpecification objects of one or more modules to import.</span></span>
* <span data-ttu-id="2a02f-108">**ModuleVersion**: Soha importálás verzióját.</span><span class="sxs-lookup"><span data-stu-id="2a02f-108">**ModuleVersion**: Version of module ot import.</span></span> <span data-ttu-id="2a02f-109">Ha használ, modulename: csak egy modul kell meghatároznia név szerint.</span><span class="sxs-lookup"><span data-stu-id="2a02f-109">If used, ModuleName must represent only one module by name.</span></span>

<span data-ttu-id="2a02f-110">A Windows PowerShell ISE azt mutatja az IntelliSense:</span><span class="sxs-lookup"><span data-stu-id="2a02f-110">In the Windows PowerShell ISE, it shows up with IntelliSense:</span></span>

![](../images/Import-DscResource-Modversion.jpg)

<span data-ttu-id="2a02f-111">**Megjegyzés:**: a `–ModuleVersion` paraméter csak akkor használható együtt a `–ModuleName` paraméter.</span><span class="sxs-lookup"><span data-stu-id="2a02f-111">**Note**: the `–ModuleVersion` parameter can only be used in combination with the `–ModuleName` parameter.</span></span> <span data-ttu-id="2a02f-112">Az erőforrás nevét, csak a nem használható a `–Name` paraméter.</span><span class="sxs-lookup"><span data-stu-id="2a02f-112">It cannot be used with resource names using only the `–Name` parameter.</span></span>

<span data-ttu-id="2a02f-113">Ez csak úgy lehet megadni a modul verzióját, ha a DSC-erőforrások betöltése volt a modul specification objektum pl.: `–ModuleName @{ModuleName="UserConfigProvider";ModuleVersion="3.0"}`</span><span class="sxs-lookup"><span data-stu-id="2a02f-113">Before this, the only way to specify the module version when loading DSC resources was by using the Module specification object e.g.: `–ModuleName @{ModuleName="UserConfigProvider";ModuleVersion="3.0"}`</span></span>