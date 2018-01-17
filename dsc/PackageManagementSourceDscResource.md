---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: DSC PackageManagementSource Resource
ms.openlocfilehash: 1c904c70369a75802484c3c0520df63602760361
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 01/17/2018
---
# <a name="dsc-packagemanagementsource-resource"></a><span data-ttu-id="8f43d-103">DSC PackageManagementSource Resource</span><span class="sxs-lookup"><span data-stu-id="8f43d-103">DSC PackageManagementSource Resource</span></span>

> <span data-ttu-id="8f43d-104">Vonatkozik: A Windows PowerShell 4.0-s verzióját, a Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="8f43d-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="8f43d-105">A **PackageManagementSource** erőforrás a Windows PowerShell szükséges konfiguráló (DSC) regisztrálni vagy regisztrációt törölni egy célcsomóponttal Package Management források mechanizmust biztosít.</span><span class="sxs-lookup"><span data-stu-id="8f43d-105">The **PackageManagementSource** resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to register or unregister Package Management sources on a target node.</span></span> <span data-ttu-id="8f43d-106">**Ily módon regisztrált csomag felügyeleti adatforrások regisztrálva van a rendszer környezetben, a rendszer fiók vagy a DSC-motor használható.**</span><span class="sxs-lookup"><span data-stu-id="8f43d-106">**Package Management sources registered in this way are registered under the System context, usable by the System account or by the DSC engine.**</span></span> <span data-ttu-id="8f43d-107">Ehhez az erőforráshoz van szükség a **PackageManagement** modul http://PowerShellGallery.com elérhető.</span><span class="sxs-lookup"><span data-stu-id="8f43d-107">This resource requires the **PackageManagement** module, available from http://PowerShellGallery.com.</span></span>

## <a name="syntax"></a><span data-ttu-id="8f43d-108">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="8f43d-108">Syntax</span></span>

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

## <a name="properties"></a><span data-ttu-id="8f43d-109">Tulajdonságok</span><span class="sxs-lookup"><span data-stu-id="8f43d-109">Properties</span></span>
|  <span data-ttu-id="8f43d-110">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="8f43d-110">Property</span></span>  |  <span data-ttu-id="8f43d-111">Leírás</span><span class="sxs-lookup"><span data-stu-id="8f43d-111">Description</span></span>   | 
|---|---| 
| <span data-ttu-id="8f43d-112">Név</span><span class="sxs-lookup"><span data-stu-id="8f43d-112">Name</span></span>| <span data-ttu-id="8f43d-113">Megadja a nevét, a csomag forrás-regisztrálva vagy nem regisztrált a rendszeren.</span><span class="sxs-lookup"><span data-stu-id="8f43d-113">Specifies the name of the package source to be registered or unregistered on your system.</span></span>| 
| <span data-ttu-id="8f43d-114">Győződjön meg arról</span><span class="sxs-lookup"><span data-stu-id="8f43d-114">Ensure</span></span>| <span data-ttu-id="8f43d-115">Meghatározza, hogy a csomag forrásához regisztrálva vagy nem regisztrált.</span><span class="sxs-lookup"><span data-stu-id="8f43d-115">Determines whether the package source is to be registered or unregistered.</span></span>| 
| <span data-ttu-id="8f43d-116">InstallationPolicy</span><span class="sxs-lookup"><span data-stu-id="8f43d-116">InstallationPolicy</span></span>| <span data-ttu-id="8f43d-117">Meghatározza, hogy megbízható-e a csomag forrásához.</span><span class="sxs-lookup"><span data-stu-id="8f43d-117">Determines whether you trust the package source.</span></span> <span data-ttu-id="8f43d-118">One of: "Untrusted", "Trusted".</span><span class="sxs-lookup"><span data-stu-id="8f43d-118">One of: "Untrusted", "Trusted".</span></span>| 
| <span data-ttu-id="8f43d-119">ProviderName</span><span class="sxs-lookup"><span data-stu-id="8f43d-119">ProviderName</span></span>| <span data-ttu-id="8f43d-120">Megadja a OneGet szolgáltató, amelyen keresztül a csomag forrás együttműködési is nevét.</span><span class="sxs-lookup"><span data-stu-id="8f43d-120">Specifies the name of the OneGet provider through which you can interop with the package source.</span></span>| 
| <span data-ttu-id="8f43d-121">SourceUri</span><span class="sxs-lookup"><span data-stu-id="8f43d-121">SourceUri</span></span>| <span data-ttu-id="8f43d-122">Adja meg a csomag forrás URI.</span><span class="sxs-lookup"><span data-stu-id="8f43d-122">Specifies the URI of the package source.</span></span>| 
| <span data-ttu-id="8f43d-123">SourceCredential</span><span class="sxs-lookup"><span data-stu-id="8f43d-123">SourceCredential</span></span>| <span data-ttu-id="8f43d-124">A csomag hozzáférést biztosít a távoli adatforráson.</span><span class="sxs-lookup"><span data-stu-id="8f43d-124">Provides access to the package on a remote source.</span></span>| 

## <a name="example"></a><span data-ttu-id="8f43d-125">Példa</span><span class="sxs-lookup"><span data-stu-id="8f43d-125">Example</span></span>

<span data-ttu-id="8f43d-126">Ez a példa regisztrálja a http://nuget.org csomag forrás használ a **PackageManagementSource** DSC-erőforrás.</span><span class="sxs-lookup"><span data-stu-id="8f43d-126">This example registers the http://nuget.org package source using the **PackageManagementSource** DSC resource.</span></span>

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

