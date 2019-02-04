---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: 46a278b83edb9d8e3d75b0874603710d416be3b5
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55684653"
---
# <a name="import-dscresource-keyword-supports--moduleversion-parameter"></a><span data-ttu-id="1fb53-102">Az import-DscResource kulcsszó támogatja a - ModuleVersion paramétert</span><span class="sxs-lookup"><span data-stu-id="1fb53-102">Import-DscResource keyword supports -ModuleVersion parameter</span></span>

<span data-ttu-id="1fb53-103">Új paraméter hozzáadtuk a `Import-DscResource` dinamikus kulcsszó szerzői DSC-konfigurációk esetén érhető el.</span><span class="sxs-lookup"><span data-stu-id="1fb53-103">We have added a new parameter to the `Import-DscResource` dynamic keyword available when authoring DSC configurations.</span></span> <span data-ttu-id="1fb53-104">Konfigurációs szerzők megadhatja pontosan melyik verziója betölteni a DSC-erőforrásait.</span><span class="sxs-lookup"><span data-stu-id="1fb53-104">Configuration authors can now specify exactly which module version to load the DSC resources from.</span></span> <span data-ttu-id="1fb53-105">Új kulcsszó szintaxisa:</span><span class="sxs-lookup"><span data-stu-id="1fb53-105">The new syntax of the keyword is:</span></span>

```powershell
Import-DscResource [-Name <ResourceName(s)>] [-ModuleName <ModuleName(s)>] [-ModuleVersion <ModuleVersion>]
```

* <span data-ttu-id="1fb53-106">**Név**: Egy vagy több erőforrás importálása nevei.</span><span class="sxs-lookup"><span data-stu-id="1fb53-106">**Name**: Names of one or more resources to import.</span></span>
* <span data-ttu-id="1fb53-107">**ModuleName**: A modul nevét vagy ModuleSpecification objektumok importálása egy vagy több modulja.</span><span class="sxs-lookup"><span data-stu-id="1fb53-107">**ModuleName**: Module names or ModuleSpecification objects of one or more modules to import.</span></span>
* <span data-ttu-id="1fb53-108">**ModuleVersion**: Modul importálása verzióját.</span><span class="sxs-lookup"><span data-stu-id="1fb53-108">**ModuleVersion**: Version of module to import.</span></span> <span data-ttu-id="1fb53-109">Ha használta, modulename: csak egy modult kell meghatároznia név alapján.</span><span class="sxs-lookup"><span data-stu-id="1fb53-109">If used, ModuleName must represent only one module by name.</span></span>

<span data-ttu-id="1fb53-110">A Windows PowerShell ISE-ben az megjelenik az IntelliSense használatával:</span><span class="sxs-lookup"><span data-stu-id="1fb53-110">In the Windows PowerShell ISE, it shows up with IntelliSense:</span></span>

![](../images/Import-DscResource-Modversion.jpg)

<span data-ttu-id="1fb53-111">**Megjegyzés:**: a `–ModuleVersion` paraméter csak akkor használható együtt a `–ModuleName` paraméter.</span><span class="sxs-lookup"><span data-stu-id="1fb53-111">**Note**: the `–ModuleVersion` parameter can only be used in combination with the `–ModuleName` parameter.</span></span> <span data-ttu-id="1fb53-112">Az erőforrás-nevek használatával csak nem használható a `–Name` paraméter.</span><span class="sxs-lookup"><span data-stu-id="1fb53-112">It cannot be used with resource names using only the `–Name` parameter.</span></span>

<span data-ttu-id="1fb53-113">Korábban az adja meg a modul verzióját, DSC-erőforrások betöltése során csak úgy lett pl. specification modul objektum segítségével: `–ModuleName @{ModuleName="UserConfigProvider";ModuleVersion="3.0"}`</span><span class="sxs-lookup"><span data-stu-id="1fb53-113">Before this, the only way to specify the module version when loading DSC resources was by using the Module specification object e.g.: `–ModuleName @{ModuleName="UserConfigProvider";ModuleVersion="3.0"}`</span></span>
