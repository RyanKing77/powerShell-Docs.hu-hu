---
ms.date: 06/20/2018
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: A DSC PackageManagementSource erőforrás
ms.openlocfilehash: 5d049b05c387cafe27edb202d569852b10852dce
ms.sourcegitcommit: 01d6985ed190a222e9da1da41596f524f607a5bc
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/04/2018
ms.locfileid: "34753770"
---
# <a name="dsc-packagemanagementsource-resource"></a><span data-ttu-id="8ed9c-103">A DSC PackageManagementSource erőforrás</span><span class="sxs-lookup"><span data-stu-id="8ed9c-103">DSC PackageManagementSource Resource</span></span>

> <span data-ttu-id="8ed9c-104">Vonatkozik: A Windows PowerShell 4.0-s verzióját, a Windows PowerShell 5.0, 5.1 Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="8ed9c-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0, Windows PowerShell 5.1</span></span>

<span data-ttu-id="8ed9c-105">A **PackageManagementSource** erőforrás a Windows PowerShell szükséges konfiguráló (DSC) regisztrálni vagy regisztrációt törölni egy célcsomóponttal Package Management források mechanizmust biztosít.</span><span class="sxs-lookup"><span data-stu-id="8ed9c-105">The **PackageManagementSource** resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to register or unregister Package Management sources on a target node.</span></span> <span data-ttu-id="8ed9c-106">**Ily módon regisztrált csomag felügyeleti adatforrások regisztrálva van a rendszer környezetben, a rendszer fiók vagy a DSC-motor használható.**</span><span class="sxs-lookup"><span data-stu-id="8ed9c-106">**Package Management sources registered in this way are registered under the System context, usable by the System account or by the DSC engine.**</span></span> <span data-ttu-id="8ed9c-107">Ehhez az erőforráshoz van szükség a **PackageManagement** modul, a rendelkezésre álló http://PowerShellGallery.com.</span><span class="sxs-lookup"><span data-stu-id="8ed9c-107">This resource requires the **PackageManagement** module, available from http://PowerShellGallery.com.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8ed9c-108">A **PackageManagement** modul kell lennie, mint a következő tulajdonság információk csak akkor lehet helyes 1.1.7.0 verziója.</span><span class="sxs-lookup"><span data-stu-id="8ed9c-108">The **PackageManagement** module should be at least version 1.1.7.0 for the following property information to be correct.</span></span>

## <a name="syntax"></a><span data-ttu-id="8ed9c-109">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="8ed9c-109">Syntax</span></span>

```
PackageManagementSource [String] #ResourceName
{
    Name = [string]
    ProviderName = [string]
    SourceLocation = [string]
    [DependsOn = [string[]]]
    [Ensure = [string]{ Absent | Present }]
    [InstallationPolicy = [string]{ Trusted | Untrusted }]
    [PsDscRunAsCredential = [PSCredential]]
    [SourceCredential = [PSCredential]]
}
```

## <a name="properties"></a><span data-ttu-id="8ed9c-110">Tulajdonságok</span><span class="sxs-lookup"><span data-stu-id="8ed9c-110">Properties</span></span>

|  <span data-ttu-id="8ed9c-111">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="8ed9c-111">Property</span></span>  |  <span data-ttu-id="8ed9c-112">Leírás</span><span class="sxs-lookup"><span data-stu-id="8ed9c-112">Description</span></span>   |
|---|---|
| <span data-ttu-id="8ed9c-113">Név</span><span class="sxs-lookup"><span data-stu-id="8ed9c-113">Name</span></span>| <span data-ttu-id="8ed9c-114">Megadja a nevét, a csomag forrás-regisztrálva vagy nem regisztrált a rendszeren.</span><span class="sxs-lookup"><span data-stu-id="8ed9c-114">Specifies the name of the package source to be registered or unregistered on your system.</span></span>|
| <span data-ttu-id="8ed9c-115">ProviderName</span><span class="sxs-lookup"><span data-stu-id="8ed9c-115">ProviderName</span></span>| <span data-ttu-id="8ed9c-116">Megadja a OneGet szolgáltató, amelyen keresztül a csomag forrás együttműködési is nevét.</span><span class="sxs-lookup"><span data-stu-id="8ed9c-116">Specifies the name of the OneGet provider through which you can interop with the package source.</span></span>|
| <span data-ttu-id="8ed9c-117">SourceLocation</span><span class="sxs-lookup"><span data-stu-id="8ed9c-117">SourceLocation</span></span>| <span data-ttu-id="8ed9c-118">Adja meg a csomag forrás URI.</span><span class="sxs-lookup"><span data-stu-id="8ed9c-118">Specifies the URI of the package source.</span></span>|
| <span data-ttu-id="8ed9c-119">Győződjön meg arról</span><span class="sxs-lookup"><span data-stu-id="8ed9c-119">Ensure</span></span>| <span data-ttu-id="8ed9c-120">Meghatározza, hogy a csomag forrásához regisztrálva vagy nem regisztrált.</span><span class="sxs-lookup"><span data-stu-id="8ed9c-120">Determines whether the package source is to be registered or unregistered.</span></span>|
| <span data-ttu-id="8ed9c-121">InstallationPolicy</span><span class="sxs-lookup"><span data-stu-id="8ed9c-121">InstallationPolicy</span></span>| <span data-ttu-id="8ed9c-122">Például a beépített Nuget-szolgáltatót a szolgáltatók használják.</span><span class="sxs-lookup"><span data-stu-id="8ed9c-122">Used by providers such as the built-in Nuget Provider.</span></span> <span data-ttu-id="8ed9c-123">Meghatározza, hogy megbízható-e a csomag forrásához.</span><span class="sxs-lookup"><span data-stu-id="8ed9c-123">Determines whether you trust the package's source.</span></span> <span data-ttu-id="8ed9c-124">Egyik: "Nem megbízható", "Megbízható".</span><span class="sxs-lookup"><span data-stu-id="8ed9c-124">One of: "Untrusted", "Trusted".</span></span>|
| <span data-ttu-id="8ed9c-125">SourceCredential</span><span class="sxs-lookup"><span data-stu-id="8ed9c-125">SourceCredential</span></span>| <span data-ttu-id="8ed9c-126">A csomag hozzáférést biztosít a távoli adatforráson.</span><span class="sxs-lookup"><span data-stu-id="8ed9c-126">Provides access to the package on a remote source.</span></span>|

## <a name="example"></a><span data-ttu-id="8ed9c-127">Példa</span><span class="sxs-lookup"><span data-stu-id="8ed9c-127">Example</span></span>

<span data-ttu-id="8ed9c-128">Ez a példa a http://nuget.org forrás használatával a **PackageManagementSource** DSC-erőforrás.</span><span class="sxs-lookup"><span data-stu-id="8ed9c-128">This example registers the http://nuget.org package source using the **PackageManagementSource** DSC resource.</span></span>

```powershell
Configuration PackageManagementSourceTest
{
    PackageManagementSource SourceRepository
    {
        Ensure      = "Present"
        Name        = "MyNuget"
        ProviderName= "Nuget"
        SourceLocation   = "http://nuget.org/api/v2/"
        InstallationPolicy ="Trusted"
    }
}
```