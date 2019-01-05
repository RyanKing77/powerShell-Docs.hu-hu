---
ms.date: 06/20/2018
keywords: DSC, powershell, a konfigurációt, a beállítása
title: DSC PackageManagement erőforrás
ms.openlocfilehash: 18cbbfe0715c82dcfdf4a5fb6ee36ee814e43d3b
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 01/04/2019
ms.locfileid: "54048486"
---
# <a name="dsc-packagemanagement-resource"></a><span data-ttu-id="a5730-103">DSC PackageManagement erőforrás</span><span class="sxs-lookup"><span data-stu-id="a5730-103">DSC PackageManagement Resource</span></span>

<span data-ttu-id="a5730-104">Érvényes: Windows PowerShell 4.0-s, Windows PowerShell 5.0, 5.1 Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="a5730-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0, Windows PowerShell 5.1</span></span>

<span data-ttu-id="a5730-105">A **PackageManagement** erőforrás a Windows PowerShell Desired State Configuration (DSC) telepítéséhez, vagy távolítsa el a felügyeleti csomagban csomagokat a egy célcsomóponttal mechanizmust biztosít.</span><span class="sxs-lookup"><span data-stu-id="a5730-105">The **PackageManagement** resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to install or uninstall Package Management packages on a target node.</span></span> <span data-ttu-id="a5730-106">Ezt az erőforrást igényel a **PackageManagement** modulban elérhető [ http://PowerShellGallery.com ](http://PowerShellGallery.com).</span><span class="sxs-lookup"><span data-stu-id="a5730-106">This resource requires the **PackageManagement** module, available from [http://PowerShellGallery.com](http://PowerShellGallery.com).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a5730-107">A **PackageManagement** modul kell lennie, mint a következő tulajdonság információkat csak akkor lehet helyes 1.1.7.0 verzió.</span><span class="sxs-lookup"><span data-stu-id="a5730-107">The **PackageManagement** module should be at least version 1.1.7.0 for the following property information to be correct.</span></span>

## <a name="syntax"></a><span data-ttu-id="a5730-108">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="a5730-108">Syntax</span></span>

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

## <a name="properties"></a><span data-ttu-id="a5730-109">Tulajdonságok</span><span class="sxs-lookup"><span data-stu-id="a5730-109">Properties</span></span>

| <span data-ttu-id="a5730-110">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="a5730-110">Property</span></span> | <span data-ttu-id="a5730-111">Leírás</span><span class="sxs-lookup"><span data-stu-id="a5730-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a5730-112">Név</span><span class="sxs-lookup"><span data-stu-id="a5730-112">Name</span></span>| <span data-ttu-id="a5730-113">Megadja a telepítendő vagy eltávolítandó-csomag neve.</span><span class="sxs-lookup"><span data-stu-id="a5730-113">Specifies the name of the Package to be installed or uninstalled.</span></span>|
| <span data-ttu-id="a5730-114">AdditionalParameters</span><span class="sxs-lookup"><span data-stu-id="a5730-114">AdditionalParameters</span></span>| <span data-ttu-id="a5730-115">Szolgáltató paramétereket, amelyek számára az adott szórótábla `Get-Package -AdditionalArguments`.</span><span class="sxs-lookup"><span data-stu-id="a5730-115">Provider specific hashtable of parameters that would be passed to `Get-Package -AdditionalArguments`.</span></span> <span data-ttu-id="a5730-116">Például a NuGet-szolgáltató adhat át további paraméterek, például a DestinationPath.</span><span class="sxs-lookup"><span data-stu-id="a5730-116">For example, for NuGet provider you can pass additional parameters like DestinationPath.</span></span>|
| <span data-ttu-id="a5730-117">Győződjön meg, hogy</span><span class="sxs-lookup"><span data-stu-id="a5730-117">Ensure</span></span>| <span data-ttu-id="a5730-118">Meghatározza, hogy a csomag telepítése vagy eltávolítása.</span><span class="sxs-lookup"><span data-stu-id="a5730-118">Determines whether the package is to be installed or uninstalled.</span></span>|
| <span data-ttu-id="a5730-119">MaximumVersion</span><span class="sxs-lookup"><span data-stu-id="a5730-119">MaximumVersion</span></span>|<span data-ttu-id="a5730-120">Adja meg a megengedett maximális verziója a csomagot, amelyet meg szeretne keresni.</span><span class="sxs-lookup"><span data-stu-id="a5730-120">Specifies the maximum allowed version of the package that you want to find.</span></span> <span data-ttu-id="a5730-121">Ha nem adja hozzá ezt a paramétert, az erőforrás megkeresése a csomag legmagasabb rendelkezésre álló verziója.</span><span class="sxs-lookup"><span data-stu-id="a5730-121">If you do not add this parameter, the resource finds the highest available version of the package.</span></span>|
| <span data-ttu-id="a5730-122">MinimumVersion</span><span class="sxs-lookup"><span data-stu-id="a5730-122">MinimumVersion</span></span>|<span data-ttu-id="a5730-123">Adja meg a minimális verziója a csomagot, amelyet meg szeretne keresni.</span><span class="sxs-lookup"><span data-stu-id="a5730-123">Specifies the minimum allowed version of the package that you want to find.</span></span> <span data-ttu-id="a5730-124">Ha nem adja hozzá ezt a paramétert, az erőforrás megkeresi a legmagasabb elérhető verziója a csomagot, amely bármely által megadott maximális megadott verziója is megfelel a _MaximumVersion_ paraméter.</span><span class="sxs-lookup"><span data-stu-id="a5730-124">If you do not add this parameter, the resource finds the highest available version of the package that also satisfies any maximum specified version specified by the _MaximumVersion_ parameter.</span></span>|
| <span data-ttu-id="a5730-125">ProviderName</span><span class="sxs-lookup"><span data-stu-id="a5730-125">ProviderName</span></span>| <span data-ttu-id="a5730-126">Adja meg, amelyhez a csomag keresést, egy szolgáltató nevét.</span><span class="sxs-lookup"><span data-stu-id="a5730-126">Specifies a package provider name to which to scope your package search.</span></span> <span data-ttu-id="a5730-127">Alkalmazáscsomagok szolgáltató nevének lekéréséhez futtassa a `Get-PackageProvider` parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="a5730-127">You can get package provider names by running the `Get-PackageProvider` cmdlet.</span></span>|
| <span data-ttu-id="a5730-128">RequiredVersion</span><span class="sxs-lookup"><span data-stu-id="a5730-128">RequiredVersion</span></span>| <span data-ttu-id="a5730-129">Adja meg a telepíteni kívánt csomag pontos verziójának.</span><span class="sxs-lookup"><span data-stu-id="a5730-129">Specifies the exact version of the package that you want to install.</span></span> <span data-ttu-id="a5730-130">Ez a paraméter nincs megadva, a DSC-erőforrás telepíti a csomagot, amely bármely által megadott maximális verziója is megfelel a legújabb elérhető verziója a _MaximumVersion_ paraméter.</span><span class="sxs-lookup"><span data-stu-id="a5730-130">If you do not specify this parameter, this DSC resource installs the newest available version of the package that also satisfies any maximum version specified by the _MaximumVersion_ parameter.</span></span>|
| <span data-ttu-id="a5730-131">Forrás</span><span class="sxs-lookup"><span data-stu-id="a5730-131">Source</span></span>| <span data-ttu-id="a5730-132">A neve, a csomag forrásához, ahol a csomag található.</span><span class="sxs-lookup"><span data-stu-id="a5730-132">Specifies the name of the package source where the package can be found.</span></span> <span data-ttu-id="a5730-133">Ez lehet egy URI-t, vagy egy adatforrás regisztrálva `Register-PackageSource` vagy PackageManagementSource DSC-erőforrás.</span><span class="sxs-lookup"><span data-stu-id="a5730-133">This can either be a URI or a source registered with `Register-PackageSource` or PackageManagementSource DSC resource.</span></span>|
| <span data-ttu-id="a5730-134">SourceCredential</span><span class="sxs-lookup"><span data-stu-id="a5730-134">SourceCredential</span></span> | <span data-ttu-id="a5730-135">Itt adható meg egy felhasználói fiókot, amely rendelkezik jogosultságokkal a megadott csomag szolgáltató vagy a forrás csomag telepítéséhez.</span><span class="sxs-lookup"><span data-stu-id="a5730-135">Specifies a user account that has rights to install a package for a specified package provider or source.</span></span>|

## <a name="additional-parameters"></a><span data-ttu-id="a5730-136">További paraméterek</span><span class="sxs-lookup"><span data-stu-id="a5730-136">Additional Parameters</span></span>

<span data-ttu-id="a5730-137">A következő táblázat felsorolja a AdditionalParameters tulajdonság lehetőségeit.</span><span class="sxs-lookup"><span data-stu-id="a5730-137">The following table lists options for the AdditionalParameters property.</span></span>

| <span data-ttu-id="a5730-138">Paraméter</span><span class="sxs-lookup"><span data-stu-id="a5730-138">Parameter</span></span> | <span data-ttu-id="a5730-139">Leírás</span><span class="sxs-lookup"><span data-stu-id="a5730-139">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a5730-140">DestinationPath</span><span class="sxs-lookup"><span data-stu-id="a5730-140">DestinationPath</span></span>| <span data-ttu-id="a5730-141">Szolgáltatók, például a beépített Nuget-szolgáltató által használt.</span><span class="sxs-lookup"><span data-stu-id="a5730-141">Used by providers such as the built-in Nuget Provider.</span></span> <span data-ttu-id="a5730-142">A csomagot a telepíteni kívánt fájl helyének megadása.</span><span class="sxs-lookup"><span data-stu-id="a5730-142">Specifies a file location where you want the package to be installed.</span></span>|
| <span data-ttu-id="a5730-143">InstallationPolicy</span><span class="sxs-lookup"><span data-stu-id="a5730-143">InstallationPolicy</span></span>| <span data-ttu-id="a5730-144">Szolgáltatók, például a beépített Nuget-szolgáltató által használt.</span><span class="sxs-lookup"><span data-stu-id="a5730-144">Used by providers such as the built-in Nuget Provider.</span></span> <span data-ttu-id="a5730-145">Azt határozza meg, hogy megbízható-e a csomag forrásához.</span><span class="sxs-lookup"><span data-stu-id="a5730-145">Determines whether you trust the package's source.</span></span> <span data-ttu-id="a5730-146">Egyik: `Untrusted`, `Trusted`.</span><span class="sxs-lookup"><span data-stu-id="a5730-146">One of: `Untrusted`, `Trusted`.</span></span>|

## <a name="example"></a><span data-ttu-id="a5730-147">Példa</span><span class="sxs-lookup"><span data-stu-id="a5730-147">Example</span></span>

<span data-ttu-id="a5730-148">Ez a példa telepíti a **JQuery** NuGet-csomagot és **GistProvider** PowerShell modul használatával a **PackageManagement** DSC-erőforrás.</span><span class="sxs-lookup"><span data-stu-id="a5730-148">This example installs the **JQuery** NuGet package and **GistProvider** PowerShell module using the **PackageManagement** DSC resource.</span></span> <span data-ttu-id="a5730-149">Ebben a példában először biztosítja a szükséges csomag adatforrások érhetők el, majd határozza meg a várható állapotát a **JQuery** és **GistProvider** packages (NuGet és a PowerShell, jelölik).</span><span class="sxs-lookup"><span data-stu-id="a5730-149">This example first ensures the required package sources are available then defines the expected state of the **JQuery** and **GistProvider** packages (NuGet and PowerShell, respectively).</span></span>

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