---
ms.date: 06/12/2017
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: A DSC PackageManagementSource erőforrás
ms.openlocfilehash: 3e67cec9058ecb0e43f882f98f5ec8b92e261a09
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/16/2018
---
# <a name="dsc-packagemanagementsource-resource"></a><span data-ttu-id="78f14-103">A DSC PackageManagementSource erőforrás</span><span class="sxs-lookup"><span data-stu-id="78f14-103">DSC PackageManagementSource Resource</span></span>

> <span data-ttu-id="78f14-104">Vonatkozik: A Windows PowerShell 4.0-s verzióját, a Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="78f14-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="78f14-105">A **PackageManagementSource** erőforrás a Windows PowerShell szükséges konfiguráló (DSC) regisztrálni vagy regisztrációt törölni egy célcsomóponttal Package Management források mechanizmust biztosít.</span><span class="sxs-lookup"><span data-stu-id="78f14-105">The **PackageManagementSource** resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to register or unregister Package Management sources on a target node.</span></span> <span data-ttu-id="78f14-106">**Ily módon regisztrált csomag felügyeleti adatforrások regisztrálva van a rendszer környezetben, a rendszer fiók vagy a DSC-motor használható.**</span><span class="sxs-lookup"><span data-stu-id="78f14-106">**Package Management sources registered in this way are registered under the System context, usable by the System account or by the DSC engine.**</span></span> <span data-ttu-id="78f14-107">Ehhez az erőforráshoz van szükség a **PackageManagement** modul, a rendelkezésre álló http://PowerShellGallery.com.</span><span class="sxs-lookup"><span data-stu-id="78f14-107">This resource requires the **PackageManagement** module, available from http://PowerShellGallery.com.</span></span>

## <a name="syntax"></a><span data-ttu-id="78f14-108">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="78f14-108">Syntax</span></span>

```
PSModule [string] #ResourceName
{
    Name = [string]
    [ Ensure = [string] { Absent | Present }  ]
    [ InstallationPolicy = [string] ]
    [ ProviderName = [string] ]
    [ SourceUri = [string] ]
    [ SourceCredential = [PSCredential] ]
}
```

## <a name="properties"></a><span data-ttu-id="78f14-109">Tulajdonságok</span><span class="sxs-lookup"><span data-stu-id="78f14-109">Properties</span></span>
|  <span data-ttu-id="78f14-110">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="78f14-110">Property</span></span>  |  <span data-ttu-id="78f14-111">Leírás</span><span class="sxs-lookup"><span data-stu-id="78f14-111">Description</span></span>   |
|---|---|
| <span data-ttu-id="78f14-112">Név</span><span class="sxs-lookup"><span data-stu-id="78f14-112">Name</span></span>| <span data-ttu-id="78f14-113">Megadja a nevét, a csomag forrás-regisztrálva vagy nem regisztrált a rendszeren.</span><span class="sxs-lookup"><span data-stu-id="78f14-113">Specifies the name of the package source to be registered or unregistered on your system.</span></span>|
| <span data-ttu-id="78f14-114">Győződjön meg arról</span><span class="sxs-lookup"><span data-stu-id="78f14-114">Ensure</span></span>| <span data-ttu-id="78f14-115">Meghatározza, hogy a csomag forrásához regisztrálva vagy nem regisztrált.</span><span class="sxs-lookup"><span data-stu-id="78f14-115">Determines whether the package source is to be registered or unregistered.</span></span>|
| <span data-ttu-id="78f14-116">InstallationPolicy</span><span class="sxs-lookup"><span data-stu-id="78f14-116">InstallationPolicy</span></span>| <span data-ttu-id="78f14-117">Meghatározza, hogy megbízható-e a csomag forrásához.</span><span class="sxs-lookup"><span data-stu-id="78f14-117">Determines whether you trust the package source.</span></span> <span data-ttu-id="78f14-118">Egyik: "Nem megbízható", "Megbízható".</span><span class="sxs-lookup"><span data-stu-id="78f14-118">One of: "Untrusted", "Trusted".</span></span>|
| <span data-ttu-id="78f14-119">ProviderName</span><span class="sxs-lookup"><span data-stu-id="78f14-119">ProviderName</span></span>| <span data-ttu-id="78f14-120">Megadja a OneGet szolgáltató, amelyen keresztül a csomag forrás együttműködési is nevét.</span><span class="sxs-lookup"><span data-stu-id="78f14-120">Specifies the name of the OneGet provider through which you can interop with the package source.</span></span>|
| <span data-ttu-id="78f14-121">SourceUri</span><span class="sxs-lookup"><span data-stu-id="78f14-121">SourceUri</span></span>| <span data-ttu-id="78f14-122">Adja meg a csomag forrás URI.</span><span class="sxs-lookup"><span data-stu-id="78f14-122">Specifies the URI of the package source.</span></span>|
| <span data-ttu-id="78f14-123">SourceCredential</span><span class="sxs-lookup"><span data-stu-id="78f14-123">SourceCredential</span></span>| <span data-ttu-id="78f14-124">A csomag hozzáférést biztosít a távoli adatforráson.</span><span class="sxs-lookup"><span data-stu-id="78f14-124">Provides access to the package on a remote source.</span></span>|

## <a name="example"></a><span data-ttu-id="78f14-125">Példa</span><span class="sxs-lookup"><span data-stu-id="78f14-125">Example</span></span>

<span data-ttu-id="78f14-126">Ez a példa a http://nuget.org forrás használatával a **PackageManagementSource** DSC-erőforrás.</span><span class="sxs-lookup"><span data-stu-id="78f14-126">This example registers the http://nuget.org package source using the **PackageManagementSource** DSC resource.</span></span>

```powershell
Configuration PackageManagementSourceTest
{
    PackageManagementSource SourceRepository
    {
        Ensure      = "Present"
        Name        = "MyNuget"
        ProviderName= "Nuget"
        SourceUri   = "http://nuget.org/api/v2/"
        InstallationPolicy ="Trusted"
    }
}
```