---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: DSC WindowsFeatureSet erőforrás
ms.openlocfilehash: 8a64168d9ad0d6a6c40eb0398cc734fa93a247dc
ms.sourcegitcommit: 46bebe692689ebedfe65ff2c828fe666b443198d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/10/2019
ms.locfileid: "67726791"
---
# <a name="dsc-windowsfeatureset-resource"></a><span data-ttu-id="39d4e-103">DSC WindowsFeatureSet erőforrás</span><span class="sxs-lookup"><span data-stu-id="39d4e-103">DSC WindowsFeatureSet Resource</span></span>

> <span data-ttu-id="39d4e-104">Érvényes: Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="39d4e-104">Applies To: Windows PowerShell 5.0</span></span>

<span data-ttu-id="39d4e-105">A **WindowsFeatureSet** erőforrás a Windows PowerShell Desired State Configuration (DSC), győződjön meg arról, hogy szerepkörök és funkciók hozzáadásakor vagy eltávolításakor a cél csomópont mechanizmust biztosít.</span><span class="sxs-lookup"><span data-stu-id="39d4e-105">The **WindowsFeatureSet** resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to ensure that roles and features are added or removed on a target node.</span></span>
<span data-ttu-id="39d4e-106">Ez az erőforrás egy [összetett erőforrás](../../../resources/authoringResourceComposite.md) , amely meghívja a [WindowsFeature erőforrás](windowsfeatureResource.md) az egyes szolgáltatásokhoz, megadva a `Name` tulajdonság.</span><span class="sxs-lookup"><span data-stu-id="39d4e-106">This resource is a [composite resource](../../../resources/authoringResourceComposite.md) that calls the [WindowsFeature resource](windowsfeatureResource.md) for each feature specified in the `Name` property.</span></span>

<span data-ttu-id="39d4e-107">Akkor használja ezt az erőforrást, ha szeretne konfigurálni egy Windows-szolgáltatások állapot számát.</span><span class="sxs-lookup"><span data-stu-id="39d4e-107">Use this resource when you want to configure a number of Windows Features to the same state.</span></span>

## <a name="syntax"></a><span data-ttu-id="39d4e-108">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="39d4e-108">Syntax</span></span>

```
WindowsFeatureSet [string] #ResourceName
{
    Name = [string[]]
    [ Ensure = [string] { Absent | Present }  ]
    [ Source = [string] ]
    [ IncludeAllSubFeature = [bool] ]
    [ Credential = [PSCredential] ]
    [ LogPath = [string] ]
    [ DependsOn = [string[]] ]

}
```

## <a name="properties"></a><span data-ttu-id="39d4e-109">Tulajdonságok</span><span class="sxs-lookup"><span data-stu-id="39d4e-109">Properties</span></span>

|  <span data-ttu-id="39d4e-110">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="39d4e-110">Property</span></span>  |  <span data-ttu-id="39d4e-111">Description</span><span class="sxs-lookup"><span data-stu-id="39d4e-111">Description</span></span>   |
|---|---|
| <span data-ttu-id="39d4e-112">Név</span><span class="sxs-lookup"><span data-stu-id="39d4e-112">Name</span></span>| <span data-ttu-id="39d4e-113">A szerepkörök vagy szolgáltatások biztosítására kívánt nevei hozzáadásakor vagy eltávolításakor.</span><span class="sxs-lookup"><span data-stu-id="39d4e-113">The names of the roles or features that you want to ensure are added or removed.</span></span> <span data-ttu-id="39d4e-114">Ez ugyanaz, mint az a **neve** tulajdonsága a [Get-WindowsFeature](/powershell/module/servermanager/get-windowsfeature?view=winserver2012r2-ps) parancsmagot, és nem a megjelenített nevet a szerepkörök vagy funkciók.</span><span class="sxs-lookup"><span data-stu-id="39d4e-114">This is the same as the **Name** property of the [Get-WindowsFeature](/powershell/module/servermanager/get-windowsfeature?view=winserver2012r2-ps) cmdlet, and not the display name of the roles or features.</span></span>|
| <span data-ttu-id="39d4e-115">Hitelesítő adatok</span><span class="sxs-lookup"><span data-stu-id="39d4e-115">Credential</span></span>| <span data-ttu-id="39d4e-116">A hitelesítő adatok hozzáadása vagy eltávolítása a szerepkörök vagy szolgáltatások használata.</span><span class="sxs-lookup"><span data-stu-id="39d4e-116">The credentials to use to add or remove the roles or features.</span></span>|
| <span data-ttu-id="39d4e-117">Győződjön meg, hogy</span><span class="sxs-lookup"><span data-stu-id="39d4e-117">Ensure</span></span>| <span data-ttu-id="39d4e-118">Azt jelzi-e a szerepkörök vagy szolgáltatások kerülnek.</span><span class="sxs-lookup"><span data-stu-id="39d4e-118">Indicates whether the roles or features are added.</span></span> <span data-ttu-id="39d4e-119">Annak érdekében, hogy a szerepkörök vagy szolgáltatások hozzá, állítsa be ezt a tulajdonságot a "E" annak érdekében, hogy eltávolítja a szerepkörök vagy szolgáltatások, a tulajdonság értéke "Hiányzik".</span><span class="sxs-lookup"><span data-stu-id="39d4e-119">To ensure that the roles or features are added, set this property to "Present" To ensure that the roles or features are removed, set the property to "Absent".</span></span>|
| <span data-ttu-id="39d4e-120">IncludeAllSubFeature</span><span class="sxs-lookup"><span data-stu-id="39d4e-120">IncludeAllSubFeature</span></span>| <span data-ttu-id="39d4e-121">Ez a tulajdonság beállítása **$true** adja meg, ha a szolgáltatásokat az összes szükséges alfunkció tartalmazza a **neve** tulajdonság.</span><span class="sxs-lookup"><span data-stu-id="39d4e-121">Set this property to **$true** to include all required subfeatures with of the features you specify with the **Name** property.</span></span>|
| <span data-ttu-id="39d4e-122">LogPath</span><span class="sxs-lookup"><span data-stu-id="39d4e-122">LogPath</span></span>| <span data-ttu-id="39d4e-123">Ha szeretne bejelentkezni a műveletet az erőforrás-szolgáltató naplófájl elérési útja.</span><span class="sxs-lookup"><span data-stu-id="39d4e-123">The path to a log file where you want the resource provider to log the operation.</span></span>|
| <span data-ttu-id="39d4e-124">DependsOn</span><span class="sxs-lookup"><span data-stu-id="39d4e-124">DependsOn</span></span>| <span data-ttu-id="39d4e-125">Azt jelzi, hogy a konfigurációt egy másik erőforrás futtatnia kell, mielőtt az erőforrás konfigurálva van.</span><span class="sxs-lookup"><span data-stu-id="39d4e-125">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="39d4e-126">Például, ha az erőforrás-konfiguráció azonosítója letiltása, a futtatni kívánt parancsfájl először van __ResourceName__ és a típusa __ResourceType__, ez a tulajdonság használata esetén `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="39d4e-126">For example, if the ID of the resource configuration script block that you want to run first is __ResourceName__ and its type is __ResourceType__, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|
| <span data-ttu-id="39d4e-127">Forrás</span><span class="sxs-lookup"><span data-stu-id="39d4e-127">Source</span></span>| <span data-ttu-id="39d4e-128">Azt jelzi, használható a telepítéshez, a forrás-fájl helyét, ha szükséges.</span><span class="sxs-lookup"><span data-stu-id="39d4e-128">Indicates the location of the source file to use for installation, if necessary.</span></span>|

## <a name="example"></a><span data-ttu-id="39d4e-129">Példa</span><span class="sxs-lookup"><span data-stu-id="39d4e-129">Example</span></span>

<span data-ttu-id="39d4e-130">A következő konfiguráció biztosítja, hogy a **webkiszolgálón** (IIS) és **SMTP-kiszolgáló** funkciók és az egyes, az összes alfunkció telepítve vannak.</span><span class="sxs-lookup"><span data-stu-id="39d4e-130">The following configuration ensures that the **Web-Server** (IIS) and **SMTP Server** features, and all subfeatures of each, are installed.</span></span>

```powershell
configuration FeatureSetTest
{
    Import-DscResource -ModuleName PSDesiredStateConfiguration
    Node localhost
    {

        WindowsFeatureSet WindowsFeatureSetExample
        {
            Name                    = @("SMTP-Server", "Web-Server")
            Ensure                  = 'Present'
            IncludeAllSubFeature    = $true
        }
    }
}
```
