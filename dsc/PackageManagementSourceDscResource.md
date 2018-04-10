---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: DSC PackageManagementSource Resource
ms.openlocfilehash: 8c0cb5a3b0a019ddb5ed995406f499298103b07c
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="dsc-packagemanagementsource-resource"></a><span data-ttu-id="b227e-103">DSC PackageManagementSource Resource</span><span class="sxs-lookup"><span data-stu-id="b227e-103">DSC PackageManagementSource Resource</span></span>

> <span data-ttu-id="b227e-104">Vonatkozik: A Windows PowerShell 4.0-s verzióját, a Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="b227e-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="b227e-105">A **PackageManagementSource** erőforrás a Windows PowerShell szükséges konfiguráló (DSC) regisztrálni vagy regisztrációt törölni egy célcsomóponttal Package Management források mechanizmust biztosít.</span><span class="sxs-lookup"><span data-stu-id="b227e-105">The **PackageManagementSource** resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to register or unregister Package Management sources on a target node.</span></span> <span data-ttu-id="b227e-106">**Ily módon regisztrált csomag felügyeleti adatforrások regisztrálva van a rendszer környezetben, a rendszer fiók vagy a DSC-motor használható.**</span><span class="sxs-lookup"><span data-stu-id="b227e-106">**Package Management sources registered in this way are registered under the System context, usable by the System account or by the DSC engine.**</span></span> <span data-ttu-id="b227e-107">Ehhez az erőforráshoz van szükség a **PackageManagement** modul, a rendelkezésre álló http://PowerShellGallery.com.</span><span class="sxs-lookup"><span data-stu-id="b227e-107">This resource requires the **PackageManagement** module, available from http://PowerShellGallery.com.</span></span>

## <a name="syntax"></a><span data-ttu-id="b227e-108">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="b227e-108">Syntax</span></span>

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

## <a name="properties"></a><span data-ttu-id="b227e-109">Tulajdonságok</span><span class="sxs-lookup"><span data-stu-id="b227e-109">Properties</span></span>
|  <span data-ttu-id="b227e-110">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="b227e-110">Property</span></span>  |  <span data-ttu-id="b227e-111">Leírás</span><span class="sxs-lookup"><span data-stu-id="b227e-111">Description</span></span>   |
|---|---|
| <span data-ttu-id="b227e-112">Név</span><span class="sxs-lookup"><span data-stu-id="b227e-112">Name</span></span>| <span data-ttu-id="b227e-113">Megadja a nevét, a csomag forrás-regisztrálva vagy nem regisztrált a rendszeren.</span><span class="sxs-lookup"><span data-stu-id="b227e-113">Specifies the name of the package source to be registered or unregistered on your system.</span></span>|
| <span data-ttu-id="b227e-114">Győződjön meg arról</span><span class="sxs-lookup"><span data-stu-id="b227e-114">Ensure</span></span>| <span data-ttu-id="b227e-115">Meghatározza, hogy a csomag forrásához regisztrálva vagy nem regisztrált.</span><span class="sxs-lookup"><span data-stu-id="b227e-115">Determines whether the package source is to be registered or unregistered.</span></span>|
| <span data-ttu-id="b227e-116">InstallationPolicy</span><span class="sxs-lookup"><span data-stu-id="b227e-116">InstallationPolicy</span></span>| <span data-ttu-id="b227e-117">Meghatározza, hogy megbízható-e a csomag forrásához.</span><span class="sxs-lookup"><span data-stu-id="b227e-117">Determines whether you trust the package source.</span></span> <span data-ttu-id="b227e-118">One of: "Untrusted", "Trusted".</span><span class="sxs-lookup"><span data-stu-id="b227e-118">One of: "Untrusted", "Trusted".</span></span>|
| <span data-ttu-id="b227e-119">ProviderName</span><span class="sxs-lookup"><span data-stu-id="b227e-119">ProviderName</span></span>| <span data-ttu-id="b227e-120">Megadja a OneGet szolgáltató, amelyen keresztül a csomag forrás együttműködési is nevét.</span><span class="sxs-lookup"><span data-stu-id="b227e-120">Specifies the name of the OneGet provider through which you can interop with the package source.</span></span>|
| <span data-ttu-id="b227e-121">SourceUri</span><span class="sxs-lookup"><span data-stu-id="b227e-121">SourceUri</span></span>| <span data-ttu-id="b227e-122">Adja meg a csomag forrás URI.</span><span class="sxs-lookup"><span data-stu-id="b227e-122">Specifies the URI of the package source.</span></span>|
| <span data-ttu-id="b227e-123">SourceCredential</span><span class="sxs-lookup"><span data-stu-id="b227e-123">SourceCredential</span></span>| <span data-ttu-id="b227e-124">A csomag hozzáférést biztosít a távoli adatforráson.</span><span class="sxs-lookup"><span data-stu-id="b227e-124">Provides access to the package on a remote source.</span></span>|

## <a name="example"></a><span data-ttu-id="b227e-125">Példa</span><span class="sxs-lookup"><span data-stu-id="b227e-125">Example</span></span>

<span data-ttu-id="b227e-126">Ez a példa a http://nuget.org forrás használatával a **PackageManagementSource** DSC-erőforrás.</span><span class="sxs-lookup"><span data-stu-id="b227e-126">This example registers the http://nuget.org package source using the **PackageManagementSource** DSC resource.</span></span>

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