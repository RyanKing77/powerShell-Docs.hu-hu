---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "A DSC PackageManagement erőforrás"
ms.openlocfilehash: a984fbf5db561a696d89b60dde8b92096c6e4924
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2017
---
# <a name="dsc-packagemanagement-resource"></a><span data-ttu-id="20ada-103">A DSC PackageManagement erőforrás</span><span class="sxs-lookup"><span data-stu-id="20ada-103">DSC PackageManagement Resource</span></span>

> <span data-ttu-id="20ada-104">Vonatkozik: A Windows PowerShell 4.0-s verzióját, a Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="20ada-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="20ada-105">A **PackageManagement** erőforrás a Windows PowerShell szükséges konfiguráló (DSC) telepítéséhez vagy eltávolításához egy célcsomóponttal csomag felügyeleti csomagok mechanizmust biztosít.</span><span class="sxs-lookup"><span data-stu-id="20ada-105">The **PackageManagement** resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to install or uninstall Package Management packages on a target node.</span></span> <span data-ttu-id="20ada-106">Ehhez az erőforráshoz van szükség a **PackageManagement** modul http://PowerShellGallery.com elérhető.</span><span class="sxs-lookup"><span data-stu-id="20ada-106">This resource requires the **PackageManagement** module, available from http://PowerShellGallery.com.</span></span>

## <a name="syntax"></a><span data-ttu-id="20ada-107">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="20ada-107">Syntax</span></span>

```
PackageManagement [string] #ResourceName
{
    Name = [string]
    [ Source = [string] ]
    [ Ensure = [string] { Absent | Present }  ]
    [ RequiredVersion = [string] ]
    [ MinimumVersion = [string] ]
    [ MaximumVersion = [string] ]
    [ SourceCredential = [PSCredential] ]
    [ ProviderName = [string] ]
    [ AdditionalParameters = [Microsoft.Management.Infrastructure.CimInstance[]] ]
}
```

## <a name="properties"></a><span data-ttu-id="20ada-108">Tulajdonságok</span><span class="sxs-lookup"><span data-stu-id="20ada-108">Properties</span></span>
|  <span data-ttu-id="20ada-109">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="20ada-109">Property</span></span>  |  <span data-ttu-id="20ada-110">Leírás</span><span class="sxs-lookup"><span data-stu-id="20ada-110">Description</span></span>   | 
|---|---| 
| <span data-ttu-id="20ada-111">Név</span><span class="sxs-lookup"><span data-stu-id="20ada-111">Name</span></span>| <span data-ttu-id="20ada-112">Megadja a telepítendő vagy eltávolítandó-csomag nevét.</span><span class="sxs-lookup"><span data-stu-id="20ada-112">Specifies the name of the Package to be installed or uninstalled.</span></span>| 
| <span data-ttu-id="20ada-113">Forrás</span><span class="sxs-lookup"><span data-stu-id="20ada-113">Source</span></span>| <span data-ttu-id="20ada-114">Megadja a nevét, a csomag forrás, ahol a csomag található.</span><span class="sxs-lookup"><span data-stu-id="20ada-114">Specifies the name of the package source where the package can be found.</span></span> <span data-ttu-id="20ada-115">Ez lehet egy URI-t, vagy egy adatforrás regisztrálva a Register-PackageSource vagy PackageManagementSource DSC erőforrás.</span><span class="sxs-lookup"><span data-stu-id="20ada-115">This can either be a URI or a source registered with Register-PackageSource or PackageManagementSource DSC resource.</span></span> <span data-ttu-id="20ada-116">A DSC-erőforrás MSFT_PackageManagementSource is regisztrálhatja a csomag forrásához.</span><span class="sxs-lookup"><span data-stu-id="20ada-116">The DSC resource MSFT_PackageManagementSource can also register a package source.</span></span>| 
| <span data-ttu-id="20ada-117">Győződjön meg arról</span><span class="sxs-lookup"><span data-stu-id="20ada-117">Ensure</span></span>| <span data-ttu-id="20ada-118">Meghatározza, hogy a csomag telepítendő vagy eltávolítandó.</span><span class="sxs-lookup"><span data-stu-id="20ada-118">Determines whether the package is to be installed or uninstalled.</span></span>| 
| <span data-ttu-id="20ada-119">RequiredVersion</span><span class="sxs-lookup"><span data-stu-id="20ada-119">RequiredVersion</span></span>| <span data-ttu-id="20ada-120">Adja meg a telepíteni kívánt csomag pontos verziójának.</span><span class="sxs-lookup"><span data-stu-id="20ada-120">Specifies the exact version of the package that you want to install.</span></span> <span data-ttu-id="20ada-121">Ez a paraméter nincs megadva, a DSC-erőforrás a csomagot, amely megfelel a MaximumVersion paraméter által megadott maximális bármilyen elérhető legújabb verzióját telepíti.</span><span class="sxs-lookup"><span data-stu-id="20ada-121">If you do not specify this parameter, this DSC resource installs the newest available version of the package that also satisfies any maximum version specified by the MaximumVersion parameter.</span></span>| 
| <span data-ttu-id="20ada-122">MinimumVersion</span><span class="sxs-lookup"><span data-stu-id="20ada-122">MinimumVersion</span></span>| <span data-ttu-id="20ada-123">Adja meg a munkaszálak a telepíteni kívánt csomag verzióját.</span><span class="sxs-lookup"><span data-stu-id="20ada-123">Specifies the minimum allowed version of the package that you want to install.</span></span> <span data-ttu-id="20ada-124">Ha nem adja hozzá ezt a paramétert, a DSC-erőforrás intalls a csomagot, amely megfelel a megadott maximális verziója elérhető legmagasabb verzióját a MaximumVersion paraméterrel megadott.</span><span class="sxs-lookup"><span data-stu-id="20ada-124">If you do not add this parameter, this DSC resource intalls the highest available version of the package that also satisfies any maximum specified version specified by the MaximumVersion parameter.</span></span>| 
| <span data-ttu-id="20ada-125">MaximumVersion</span><span class="sxs-lookup"><span data-stu-id="20ada-125">MaximumVersion</span></span>| <span data-ttu-id="20ada-126">Adja meg a megengedett a telepíteni kívánt csomag verzióját.</span><span class="sxs-lookup"><span data-stu-id="20ada-126">Specifies the maximum allowed version of the package that you want to install.</span></span> <span data-ttu-id="20ada-127">Ha ez a paraméter nincs megadva, a DSC-erőforrás a legmagasabb számú elérhető verzióját telepíti a csomag.</span><span class="sxs-lookup"><span data-stu-id="20ada-127">If you do not specify this parameter, this DSC resource installs the highest-numbered available version of the package.</span></span>| 
| <span data-ttu-id="20ada-128">SourceCredential</span><span class="sxs-lookup"><span data-stu-id="20ada-128">SourceCredential</span></span> | <span data-ttu-id="20ada-129">Adja meg egy felhasználói fiókot, amely a megadott csomag szolgáltató vagy a forrás csomag telepítéséhez jogosultsággal rendelkezik.</span><span class="sxs-lookup"><span data-stu-id="20ada-129">Specifies a user account that has rights to install a package for a specified package provider or source.</span></span>| 
| <span data-ttu-id="20ada-130">ProviderName</span><span class="sxs-lookup"><span data-stu-id="20ada-130">ProviderName</span></span>| <span data-ttu-id="20ada-131">A csomag szolgáltató nevét, amelyhez a csomag keresés hatókörének megadása</span><span class="sxs-lookup"><span data-stu-id="20ada-131">Specifies a package provider name to which to scope your package search.</span></span> <span data-ttu-id="20ada-132">A Get-PackageProvider parancsmag futtatásával kaphat a csomag a szolgáltatói nevet.</span><span class="sxs-lookup"><span data-stu-id="20ada-132">You can get package provider names by running the Get-PackageProvider cmdlet.</span></span>| 
| <span data-ttu-id="20ada-133">AdditionalParameters</span><span class="sxs-lookup"><span data-stu-id="20ada-133">AdditionalParameters</span></span>| <span data-ttu-id="20ada-134">Szolgáltató adott paraméterek átadása pedig egy kivonattáblát.</span><span class="sxs-lookup"><span data-stu-id="20ada-134">Provider specific parameters that are passed as an Hashtable.</span></span> <span data-ttu-id="20ada-135">Például NuGet-szolgáltató is át további paraméterek, például a DestinationPath.</span><span class="sxs-lookup"><span data-stu-id="20ada-135">For example, for NuGet provider you can pass additional parameters like DestinationPath.</span></span>| 

## <a name="additional-parameters"></a><span data-ttu-id="20ada-136">További paraméterek</span><span class="sxs-lookup"><span data-stu-id="20ada-136">Additional Parameters</span></span>
<span data-ttu-id="20ada-137">A következő táblázat felsorolja a AdditionalParameters tulajdonság lehetőségeit.</span><span class="sxs-lookup"><span data-stu-id="20ada-137">The following table lists options for the AdditionalParameters property.</span></span>
|  <span data-ttu-id="20ada-138">Paraméter</span><span class="sxs-lookup"><span data-stu-id="20ada-138">Parameter</span></span>  | <span data-ttu-id="20ada-139">Leírás</span><span class="sxs-lookup"><span data-stu-id="20ada-139">Description</span></span>   | 
|---|---|
| <span data-ttu-id="20ada-140">DestinationPath</span><span class="sxs-lookup"><span data-stu-id="20ada-140">DestinationPath</span></span>| <span data-ttu-id="20ada-141">Például a beépített Nuget-szolgáltatót a szolgáltatók használják.</span><span class="sxs-lookup"><span data-stu-id="20ada-141">Used by providers such as the built-in Nuget Provider.</span></span> <span data-ttu-id="20ada-142">A csomagot a telepíteni kívánt fájl helyének megadása.</span><span class="sxs-lookup"><span data-stu-id="20ada-142">Specifies a file location where you want the package to be installed.</span></span>|
| <span data-ttu-id="20ada-143">InstallationPolicy</span><span class="sxs-lookup"><span data-stu-id="20ada-143">InstallationPolicy</span></span>| <span data-ttu-id="20ada-144">Például a beépített Nuget-szolgáltatót a szolgáltatók használják.</span><span class="sxs-lookup"><span data-stu-id="20ada-144">Used by providers such as the built-in Nuget Provider.</span></span> <span data-ttu-id="20ada-145">Meghatározza, hogy megbízható-e a csomag forrásához.</span><span class="sxs-lookup"><span data-stu-id="20ada-145">Determines whether you trust the package's source.</span></span> <span data-ttu-id="20ada-146">Egyik: "Nem megbízható", "Megbízható".</span><span class="sxs-lookup"><span data-stu-id="20ada-146">One of: "Untrusted", "Trusted".</span></span>|

## <a name="example"></a><span data-ttu-id="20ada-147">Példa</span><span class="sxs-lookup"><span data-stu-id="20ada-147">Example</span></span>

<span data-ttu-id="20ada-148">Ez a példa telepíti a **JQuery** NuGet-csomagot és **GistProvider** PowerShell modul használatával a **PackageManagement** DSC-erőforrás.</span><span class="sxs-lookup"><span data-stu-id="20ada-148">This example installs the **JQuery** NuGet package and **GistProvider** PowerShell module using the **PackageManagement** DSC resource.</span></span> <span data-ttu-id="20ada-149">Ez a példa első biztosítja a szükséges csomag források érhetők el, majd határozza meg a várt állapota a **JQuery** és **GistProvider** csomagok (NuGet és a PowerShell használatával, illetve).</span><span class="sxs-lookup"><span data-stu-id="20ada-149">This example first ensures the required package sources are available then defines the expected state of the **JQuery** and **GistProvider** packages (NuGet and PowerShell, respectively).</span></span>

```powershell
Configuration PackageTest
{    
    PackageManagementSource SourceRepository 
    { 
        Ensure      = "Present" 
        Name        = "MyNuget" 
        ProviderName= "Nuget" 
        SourceUri   = "http://nuget.org/api/v2/"   
        InstallationPolicy ="Trusted" 
    }    
    
    PackageManagementSource PSGallery 
    { 
        Ensure      = "Present" 
        Name        = "psgallery" 
        ProviderName= "PowerShellGet" 
        SourceUri   = "https://www.powershellgallery.com/api/v2/"   
        InstallationPolicy ="Trusted" 
    } 
          
    PackageManagement NugetPackage 
    { 
        Ensure               = "Present"  
        Name                 = "JQuery"
        AdditionalParameters = "$env:HomeDrive\nuget"
        RequiredVersion      = "2.0.1" 
        DependsOn            = "[PackageManagementSource]SourceRepository" 
    }
    
    PackageManagement PSModule 
    { 
        Ensure               = "Present"  
        Name                 = "gistprovider"
        Source               = "PSGallery"
        DependsOn            = "[PackageManagementSource]PSGallery" 
    }
}
```

