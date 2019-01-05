---
ms.date: 06/20/2018
keywords: DSC, powershell, a konfigurációt, a beállítása
title: DSC PackageManagementSource erőforrás
ms.openlocfilehash: e51b5318288bef458567dd4b58d17caaea3ed69b
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 01/04/2019
ms.locfileid: "54048239"
---
# <a name="dsc-packagemanagementsource-resource"></a><span data-ttu-id="27d9e-103">DSC PackageManagementSource erőforrás</span><span class="sxs-lookup"><span data-stu-id="27d9e-103">DSC PackageManagementSource Resource</span></span>

> <span data-ttu-id="27d9e-104">Érvényes: Windows PowerShell 4.0-s, Windows PowerShell 5.0, 5.1 Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="27d9e-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0, Windows PowerShell 5.1</span></span>

<span data-ttu-id="27d9e-105">A **PackageManagementSource** erőforrás a Windows PowerShell Desired State Configuration (DSC) regisztrálásához vagy regisztrációjának törlése a csomagkezelés forrásból a célként megadott csomóponton mechanizmust biztosít.</span><span class="sxs-lookup"><span data-stu-id="27d9e-105">The **PackageManagementSource** resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to register or unregister Package Management sources on a target node.</span></span> <span data-ttu-id="27d9e-106">**Ezzel a módszerrel regisztrált felügyeleti csomagforrások rendszer környezetében, a rendszer fiók vagy a DSC motor által használható vannak regisztrálva.**</span><span class="sxs-lookup"><span data-stu-id="27d9e-106">**Package Management sources registered in this way are registered under the System context, usable by the System account or by the DSC engine.**</span></span> <span data-ttu-id="27d9e-107">Ezt az erőforrást igényel a **PackageManagement** modulban elérhető http://PowerShellGallery.com.</span><span class="sxs-lookup"><span data-stu-id="27d9e-107">This resource requires the **PackageManagement** module, available from http://PowerShellGallery.com.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="27d9e-108">A **PackageManagement** modul kell lennie, mint a következő tulajdonság információkat csak akkor lehet helyes 1.1.7.0 verzió.</span><span class="sxs-lookup"><span data-stu-id="27d9e-108">The **PackageManagement** module should be at least version 1.1.7.0 for the following property information to be correct.</span></span>

## <a name="syntax"></a><span data-ttu-id="27d9e-109">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="27d9e-109">Syntax</span></span>

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

## <a name="properties"></a><span data-ttu-id="27d9e-110">Tulajdonságok</span><span class="sxs-lookup"><span data-stu-id="27d9e-110">Properties</span></span>

|  <span data-ttu-id="27d9e-111">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="27d9e-111">Property</span></span>  |  <span data-ttu-id="27d9e-112">Leírás</span><span class="sxs-lookup"><span data-stu-id="27d9e-112">Description</span></span>   |
|---|---|
| <span data-ttu-id="27d9e-113">Név</span><span class="sxs-lookup"><span data-stu-id="27d9e-113">Name</span></span>| <span data-ttu-id="27d9e-114">A neve, a csomag forrásához – regisztrálva vagy nem regisztrált a rendszeren.</span><span class="sxs-lookup"><span data-stu-id="27d9e-114">Specifies the name of the package source to be registered or unregistered on your system.</span></span>|
| <span data-ttu-id="27d9e-115">ProviderName</span><span class="sxs-lookup"><span data-stu-id="27d9e-115">ProviderName</span></span>| <span data-ttu-id="27d9e-116">Megadja a OneGet szolgáltatója, amelyen keresztül a csomag forrás-mel is nevét.</span><span class="sxs-lookup"><span data-stu-id="27d9e-116">Specifies the name of the OneGet provider through which you can interop with the package source.</span></span>|
| <span data-ttu-id="27d9e-117">SourceLocation</span><span class="sxs-lookup"><span data-stu-id="27d9e-117">SourceLocation</span></span>| <span data-ttu-id="27d9e-118">Adja meg az URI-ját a csomag forrásához.</span><span class="sxs-lookup"><span data-stu-id="27d9e-118">Specifies the URI of the package source.</span></span>|
| <span data-ttu-id="27d9e-119">Győződjön meg, hogy</span><span class="sxs-lookup"><span data-stu-id="27d9e-119">Ensure</span></span>| <span data-ttu-id="27d9e-120">Meghatározza, hogy a csomag forrásához regisztrálva vagy nem regisztrált.</span><span class="sxs-lookup"><span data-stu-id="27d9e-120">Determines whether the package source is to be registered or unregistered.</span></span>|
| <span data-ttu-id="27d9e-121">InstallationPolicy</span><span class="sxs-lookup"><span data-stu-id="27d9e-121">InstallationPolicy</span></span>| <span data-ttu-id="27d9e-122">Szolgáltatók, például a beépített Nuget-szolgáltató által használt.</span><span class="sxs-lookup"><span data-stu-id="27d9e-122">Used by providers such as the built-in Nuget Provider.</span></span> <span data-ttu-id="27d9e-123">Azt határozza meg, hogy megbízható-e a csomag forrásához.</span><span class="sxs-lookup"><span data-stu-id="27d9e-123">Determines whether you trust the package's source.</span></span> <span data-ttu-id="27d9e-124">Egyike: "Nem megbízható", "megbízható".</span><span class="sxs-lookup"><span data-stu-id="27d9e-124">One of: "Untrusted", "Trusted".</span></span>|
| <span data-ttu-id="27d9e-125">SourceCredential</span><span class="sxs-lookup"><span data-stu-id="27d9e-125">SourceCredential</span></span>| <span data-ttu-id="27d9e-126">A csomag hozzáférést biztosít a távoli forrás.</span><span class="sxs-lookup"><span data-stu-id="27d9e-126">Provides access to the package on a remote source.</span></span>|

## <a name="example"></a><span data-ttu-id="27d9e-127">Példa</span><span class="sxs-lookup"><span data-stu-id="27d9e-127">Example</span></span>

<span data-ttu-id="27d9e-128">Ebben a példában regisztrálja a http://nuget.org forrás használatával a **PackageManagementSource** DSC-erőforrás.</span><span class="sxs-lookup"><span data-stu-id="27d9e-128">This example registers the http://nuget.org package source using the **PackageManagementSource** DSC resource.</span></span>

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