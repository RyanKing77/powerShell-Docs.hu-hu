---
ms.date: 06/20/2018
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: A DSC PackageManagement erőforrás
ms.openlocfilehash: 3d52934b130d59acee4d7f8a92da2c743c1eb305
ms.sourcegitcommit: 01d6985ed190a222e9da1da41596f524f607a5bc
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/04/2018
ms.locfileid: "34753787"
---
# <a name="dsc-packagemanagement-resource"></a><span data-ttu-id="6fe85-103">A DSC PackageManagement erőforrás</span><span class="sxs-lookup"><span data-stu-id="6fe85-103">DSC PackageManagement Resource</span></span>

> <span data-ttu-id="6fe85-104">Vonatkozik: A Windows PowerShell 4.0-s verzióját, a Windows PowerShell 5.0, 5.1 Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="6fe85-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0, Windows PowerShell 5.1</span></span>

<span data-ttu-id="6fe85-105">A **PackageManagement** erőforrás a Windows PowerShell szükséges konfiguráló (DSC) telepítéséhez vagy eltávolításához egy célcsomóponttal csomag felügyeleti csomagok mechanizmust biztosít.</span><span class="sxs-lookup"><span data-stu-id="6fe85-105">The **PackageManagement** resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to install or uninstall Package Management packages on a target node.</span></span> <span data-ttu-id="6fe85-106">Ehhez az erőforráshoz van szükség a **PackageManagement** modul, a rendelkezésre álló http://PowerShellGallery.com.</span><span class="sxs-lookup"><span data-stu-id="6fe85-106">This resource requires the **PackageManagement** module, available from http://PowerShellGallery.com.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6fe85-107">A **PackageManagement** modul kell lennie, mint a következő tulajdonság információk csak akkor lehet helyes 1.1.7.0 verziója.</span><span class="sxs-lookup"><span data-stu-id="6fe85-107">The **PackageManagement** module should be at least version 1.1.7.0 for the following property information to be correct.</span></span>

## <a name="syntax"></a><span data-ttu-id="6fe85-108">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="6fe85-108">Syntax</span></span>

```
PackageManagement [string] #ResourceName
{
    Name = [string]
    [AdditionalParameters = [HashTable]]
    [DependsOn = [string[]]]
    [Ensure = [string]{ Absent | Present }]
    [MaximumVersion = [string]]
    [MinimumVersion = [string]]
    [ProviderName = [string]]
    [PsDscRunAsCredential = [PSCredential]]
    [RequiredVersion = [string]]
    [Source = [string]]
    [SourceCredential = [PSCredential]]
}
```

## <a name="properties"></a><span data-ttu-id="6fe85-109">Tulajdonságok</span><span class="sxs-lookup"><span data-stu-id="6fe85-109">Properties</span></span>

|  <span data-ttu-id="6fe85-110">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="6fe85-110">Property</span></span>  |  <span data-ttu-id="6fe85-111">Leírás</span><span class="sxs-lookup"><span data-stu-id="6fe85-111">Description</span></span>   |
|---|---|
| <span data-ttu-id="6fe85-112">Név</span><span class="sxs-lookup"><span data-stu-id="6fe85-112">Name</span></span>| <span data-ttu-id="6fe85-113">Megadja a telepítendő vagy eltávolítandó-csomag nevét.</span><span class="sxs-lookup"><span data-stu-id="6fe85-113">Specifies the name of the Package to be installed or uninstalled.</span></span>|
| <span data-ttu-id="6fe85-114">AdditionalParameters</span><span class="sxs-lookup"><span data-stu-id="6fe85-114">AdditionalParameters</span></span>| <span data-ttu-id="6fe85-115">Szolgáltató adott kivonattábla, amely átadandó paraméterek `Get-Package -AdditionalArguments`.</span><span class="sxs-lookup"><span data-stu-id="6fe85-115">Provider specific hashtable of parameters that would be passed to `Get-Package -AdditionalArguments`.</span></span> <span data-ttu-id="6fe85-116">Például NuGet-szolgáltató is át további paraméterek, például a DestinationPath.</span><span class="sxs-lookup"><span data-stu-id="6fe85-116">For example, for NuGet provider you can pass additional parameters like DestinationPath.</span></span>|
| <span data-ttu-id="6fe85-117">Győződjön meg arról</span><span class="sxs-lookup"><span data-stu-id="6fe85-117">Ensure</span></span>| <span data-ttu-id="6fe85-118">Meghatározza, hogy a csomag telepítendő vagy eltávolítandó.</span><span class="sxs-lookup"><span data-stu-id="6fe85-118">Determines whether the package is to be installed or uninstalled.</span></span>|
| <span data-ttu-id="6fe85-119">MaximumVersion</span><span class="sxs-lookup"><span data-stu-id="6fe85-119">MaximumVersion</span></span>|<span data-ttu-id="6fe85-120">Adja meg a megengedett a csomagot, amely a keresett verzióját.</span><span class="sxs-lookup"><span data-stu-id="6fe85-120">Specifies the maximum allowed version of the package that you want to find.</span></span> <span data-ttu-id="6fe85-121">Ha nem adja hozzá ezt a paramétert, az erőforrás megkeresése a csomag legmagasabb rendelkezésre álló verziója.</span><span class="sxs-lookup"><span data-stu-id="6fe85-121">If you do not add this parameter, the resource finds the highest available version of the package.</span></span>|
| <span data-ttu-id="6fe85-122">MinimumVersion</span><span class="sxs-lookup"><span data-stu-id="6fe85-122">MinimumVersion</span></span>|<span data-ttu-id="6fe85-123">Adja meg a minimális verziója a csomagot, amely a keresett engedélyezett.</span><span class="sxs-lookup"><span data-stu-id="6fe85-123">Specifies the minimum allowed version of the package that you want to find.</span></span> <span data-ttu-id="6fe85-124">Ha nem adja hozzá ezt a paramétert, az erőforrás megkeresése a csomagot, amely megfelel minden maximális megadott verziója által megadott legmagasabb rendelkezésre álló verziója a _MaximumVersion_ paraméter.</span><span class="sxs-lookup"><span data-stu-id="6fe85-124">If you do not add this parameter, the resource finds the highest available version of the package that also satisfies any maximum specified version specified by the _MaximumVersion_ parameter.</span></span>|
| <span data-ttu-id="6fe85-125">ProviderName</span><span class="sxs-lookup"><span data-stu-id="6fe85-125">ProviderName</span></span>| <span data-ttu-id="6fe85-126">A csomag szolgáltató nevét, amelyhez a csomag keresés hatókörének megadása</span><span class="sxs-lookup"><span data-stu-id="6fe85-126">Specifies a package provider name to which to scope your package search.</span></span> <span data-ttu-id="6fe85-127">Csomag a szolgáltatói nevet lekéréséhez futtassa a `Get-PackageProvider` parancsmag.</span><span class="sxs-lookup"><span data-stu-id="6fe85-127">You can get package provider names by running the `Get-PackageProvider` cmdlet.</span></span>|
| <span data-ttu-id="6fe85-128">RequiredVersion</span><span class="sxs-lookup"><span data-stu-id="6fe85-128">RequiredVersion</span></span>| <span data-ttu-id="6fe85-129">Adja meg a telepíteni kívánt csomag pontos verziójának.</span><span class="sxs-lookup"><span data-stu-id="6fe85-129">Specifies the exact version of the package that you want to install.</span></span> <span data-ttu-id="6fe85-130">Ha ez a paraméter nincs megadva, a DSC-erőforrás telepíti-e a csomagot, amely megfelel a megadott maximális verziója elérhető legújabb verzióját a _MaximumVersion_ paraméter.</span><span class="sxs-lookup"><span data-stu-id="6fe85-130">If you do not specify this parameter, this DSC resource installs the newest available version of the package that also satisfies any maximum version specified by the _MaximumVersion_ parameter.</span></span>|
| <span data-ttu-id="6fe85-131">Forrás</span><span class="sxs-lookup"><span data-stu-id="6fe85-131">Source</span></span>| <span data-ttu-id="6fe85-132">Megadja a nevét, a csomag forrás, ahol a csomag található.</span><span class="sxs-lookup"><span data-stu-id="6fe85-132">Specifies the name of the package source where the package can be found.</span></span> <span data-ttu-id="6fe85-133">Ez lehet egy URI-t, vagy egy adatforrás regisztrálva a `Register-PackageSource` vagy PackageManagementSource DSC-erőforrást.</span><span class="sxs-lookup"><span data-stu-id="6fe85-133">This can either be a URI or a source registered with `Register-PackageSource` or PackageManagementSource DSC resource.</span></span>|
| <span data-ttu-id="6fe85-134">SourceCredential</span><span class="sxs-lookup"><span data-stu-id="6fe85-134">SourceCredential</span></span> | <span data-ttu-id="6fe85-135">Adja meg egy felhasználói fiókot, amely a megadott csomag szolgáltató vagy a forrás csomag telepítéséhez jogosultsággal rendelkezik.</span><span class="sxs-lookup"><span data-stu-id="6fe85-135">Specifies a user account that has rights to install a package for a specified package provider or source.</span></span>|

## <a name="additional-parameters"></a><span data-ttu-id="6fe85-136">További paraméterek</span><span class="sxs-lookup"><span data-stu-id="6fe85-136">Additional Parameters</span></span>

<span data-ttu-id="6fe85-137">A következő táblázat felsorolja a AdditionalParameters tulajdonság lehetőségeit.</span><span class="sxs-lookup"><span data-stu-id="6fe85-137">The following table lists options for the AdditionalParameters property.</span></span>
|  <span data-ttu-id="6fe85-138">Paraméter</span><span class="sxs-lookup"><span data-stu-id="6fe85-138">Parameter</span></span>  | <span data-ttu-id="6fe85-139">Leírás</span><span class="sxs-lookup"><span data-stu-id="6fe85-139">Description</span></span>   |
|---|---|
| <span data-ttu-id="6fe85-140">DestinationPath</span><span class="sxs-lookup"><span data-stu-id="6fe85-140">DestinationPath</span></span>| <span data-ttu-id="6fe85-141">Például a beépített Nuget-szolgáltatót a szolgáltatók használják.</span><span class="sxs-lookup"><span data-stu-id="6fe85-141">Used by providers such as the built-in Nuget Provider.</span></span> <span data-ttu-id="6fe85-142">A csomagot a telepíteni kívánt fájl helyének megadása.</span><span class="sxs-lookup"><span data-stu-id="6fe85-142">Specifies a file location where you want the package to be installed.</span></span>|
| <span data-ttu-id="6fe85-143">InstallationPolicy</span><span class="sxs-lookup"><span data-stu-id="6fe85-143">InstallationPolicy</span></span>| <span data-ttu-id="6fe85-144">Például a beépített Nuget-szolgáltatót a szolgáltatók használják.</span><span class="sxs-lookup"><span data-stu-id="6fe85-144">Used by providers such as the built-in Nuget Provider.</span></span> <span data-ttu-id="6fe85-145">Meghatározza, hogy megbízható-e a csomag forrásához.</span><span class="sxs-lookup"><span data-stu-id="6fe85-145">Determines whether you trust the package's source.</span></span> <span data-ttu-id="6fe85-146">Egyik: "Nem megbízható", "Megbízható".</span><span class="sxs-lookup"><span data-stu-id="6fe85-146">One of: "Untrusted", "Trusted".</span></span>|

## <a name="example"></a><span data-ttu-id="6fe85-147">Példa</span><span class="sxs-lookup"><span data-stu-id="6fe85-147">Example</span></span>

<span data-ttu-id="6fe85-148">Ez a példa telepíti a **JQuery** NuGet-csomagot és **GistProvider** PowerShell modul használatával a **PackageManagement** DSC-erőforrás.</span><span class="sxs-lookup"><span data-stu-id="6fe85-148">This example installs the **JQuery** NuGet package and **GistProvider** PowerShell module using the **PackageManagement** DSC resource.</span></span> <span data-ttu-id="6fe85-149">Ez a példa első biztosítja a szükséges csomag források érhetők el, majd határozza meg a várt állapota a **JQuery** és **GistProvider** csomagok (NuGet és a PowerShell használatával, illetve).</span><span class="sxs-lookup"><span data-stu-id="6fe85-149">This example first ensures the required package sources are available then defines the expected state of the **JQuery** and **GistProvider** packages (NuGet and PowerShell, respectively).</span></span>

```powershell
Configuration PackageTest
{
    PackageManagementSource SourceRepository
    {
        Ensure      = "Present"
        Name        = "MyNuget"
        ProviderName= "Nuget"
        SourceLocation   = "http://nuget.org/api/v2/"
        InstallationPolicy ="Trusted"
    }

    PackageManagementSource PSGallery
    {
        Ensure      = "Present"
        Name        = "psgallery"
        ProviderName= "PowerShellGet"
        SourceLocation   = "https://www.powershellgallery.com/api/v2/"
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