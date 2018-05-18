---
ms.date: 06/12/2017
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: A DSC WindowsFeatureSet erőforrás
ms.openlocfilehash: 582f9b1f439056118680f6f814d2c202d0e823be
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/16/2018
---
# <a name="dsc-windowsfeatureset-resource"></a><span data-ttu-id="28adf-103">A DSC WindowsFeatureSet erőforrás</span><span class="sxs-lookup"><span data-stu-id="28adf-103">DSC WindowsFeatureSet Resource</span></span>

> <span data-ttu-id="28adf-104">Vonatkozik: A Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="28adf-104">Applies To: Windows PowerShell 5.0</span></span>

<span data-ttu-id="28adf-105">A **WindowsFeatureSet** erőforrás a Windows PowerShell szükséges konfiguráló (DSC) Győződjön meg arról, hogy szerepkörök és szolgáltatások hozzáadása vagy eltávolítása egy célcsomóponttal mechanizmust biztosít.</span><span class="sxs-lookup"><span data-stu-id="28adf-105">The **WindowsFeatureSet** resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to ensure that roles and features are added or removed on a target node.</span></span>
<span data-ttu-id="28adf-106">Az erőforrás egy [összetett erőforrás](authoringResourceComposite.md) , amely meghívja a [WindowsFeature erőforrás](windowsfeatureResource.md) az egyes szolgáltatásokhoz megadott a `Name` tulajdonság.</span><span class="sxs-lookup"><span data-stu-id="28adf-106">This resource is a [composite resource](authoringResourceComposite.md) that calls the [WindowsFeature resource](windowsfeatureResource.md) for each feature specified in the `Name` property.</span></span>

<span data-ttu-id="28adf-107">Ehhez az erőforráshoz akkor használja, ha a Windows-szolgáltatások számos állapot konfigurálni szeretné.</span><span class="sxs-lookup"><span data-stu-id="28adf-107">Use this resource when you want to configure a number of Windows Features to the same state.</span></span>

## <a name="syntax"></a><span data-ttu-id="28adf-108">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="28adf-108">Syntax</span></span>

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

## <a name="properties"></a><span data-ttu-id="28adf-109">Tulajdonságok</span><span class="sxs-lookup"><span data-stu-id="28adf-109">Properties</span></span>

|  <span data-ttu-id="28adf-110">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="28adf-110">Property</span></span>  |  <span data-ttu-id="28adf-111">Leírás</span><span class="sxs-lookup"><span data-stu-id="28adf-111">Description</span></span>   |
|---|---|
| <span data-ttu-id="28adf-112">Név</span><span class="sxs-lookup"><span data-stu-id="28adf-112">Name</span></span>| <span data-ttu-id="28adf-113">A szerepkörök vagy szolgáltatások biztosítása kívánt nevét hozzáadásakor vagy eltávolításakor.</span><span class="sxs-lookup"><span data-stu-id="28adf-113">The names of the roles or features that you want to ensure are added or removed.</span></span> <span data-ttu-id="28adf-114">Ez megegyezik a **neve** tulajdonsága a [Get-WindowsFeature](https://technet.microsoft.com/en-us/library/jj205469.aspx) parancsmag, és nem a megjelenített név a szerepkörök vagy szolgáltatások.</span><span class="sxs-lookup"><span data-stu-id="28adf-114">This is the same as the **Name** property of the [Get-WindowsFeature](https://technet.microsoft.com/en-us/library/jj205469.aspx) cmdlet, and not the display name of the roles or features.</span></span>|
| <span data-ttu-id="28adf-115">hitelesítő adatok</span><span class="sxs-lookup"><span data-stu-id="28adf-115">Credential</span></span>| <span data-ttu-id="28adf-116">A hitelesítő adatok hozzáadása vagy eltávolítása a szerepkörök vagy szolgáltatások használatára.</span><span class="sxs-lookup"><span data-stu-id="28adf-116">The credentials to use to add or remove the roles or features.</span></span>|
| <span data-ttu-id="28adf-117">Győződjön meg arról</span><span class="sxs-lookup"><span data-stu-id="28adf-117">Ensure</span></span>| <span data-ttu-id="28adf-118">Azt jelzi, hogy a szerepkörök vagy szolgáltatások kerülnek.</span><span class="sxs-lookup"><span data-stu-id="28adf-118">Indicates whether the roles or features are added.</span></span> <span data-ttu-id="28adf-119">Ezzel biztosíthatja, hogy a szerepkörök vagy szolgáltatások hozzáadott, állítsa be ezt a tulajdonságot "Elérhető" Győződjön meg arról, hogy eltávolítja a szerepkörök vagy szolgáltatások, a tulajdonság értéke "Hiányzik".</span><span class="sxs-lookup"><span data-stu-id="28adf-119">To ensure that the roles or features are added, set this property to "Present" To ensure that the roles or features are removed, set the property to "Absent".</span></span>|
| <span data-ttu-id="28adf-120">IncludeAllSubFeature</span><span class="sxs-lookup"><span data-stu-id="28adf-120">IncludeAllSubFeature</span></span>| <span data-ttu-id="28adf-121">Ez a tulajdonság beállítása **$true** tartalmazza a Funkciók, adja meg az összes szükséges alfunkció a **neve** tulajdonság.</span><span class="sxs-lookup"><span data-stu-id="28adf-121">Set this property to **$true** to include all required subfeatures with of the features you specify with the **Name** property.</span></span>|
| <span data-ttu-id="28adf-122">LogPath</span><span class="sxs-lookup"><span data-stu-id="28adf-122">LogPath</span></span>| <span data-ttu-id="28adf-123">A naplófájl elérési útja a kívánt való bejelentkezéshez a műveletet az erőforrás-szolgáltató.</span><span class="sxs-lookup"><span data-stu-id="28adf-123">The path to a log file where you want the resource provider to log the operation.</span></span>|
| <span data-ttu-id="28adf-124">dependsOn</span><span class="sxs-lookup"><span data-stu-id="28adf-124">DependsOn</span></span>| <span data-ttu-id="28adf-125">Azt jelzi, hogy egy másik erőforrás konfigurációjának kell futtatni, mielőtt ehhez az erőforráshoz van konfigurálva.</span><span class="sxs-lookup"><span data-stu-id="28adf-125">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="28adf-126">Például, ha az erőforrás-konfiguráció azonosítója blokk futtatni kívánt parancsfájl első az __ResourceName__ és annak típusa __ResourceType__, az e tulajdonság használatával szintaxisa a következő `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="28adf-126">For example, if the ID of the resource configuration script block that you want to run first is __ResourceName__ and its type is __ResourceType__, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|
| <span data-ttu-id="28adf-127">Forrás</span><span class="sxs-lookup"><span data-stu-id="28adf-127">Source</span></span>| <span data-ttu-id="28adf-128">Azt jelzi, használható a telepítéshez, a forrás-fájl helyét, ha szükséges.</span><span class="sxs-lookup"><span data-stu-id="28adf-128">Indicates the location of the source file to use for installation, if necessary.</span></span>|

## <a name="example"></a><span data-ttu-id="28adf-129">Példa</span><span class="sxs-lookup"><span data-stu-id="28adf-129">Example</span></span>

<span data-ttu-id="28adf-130">A következő konfigurációs biztosítja, hogy a **webkiszolgáló** (IIS) és **SMTP-kiszolgáló** funkciók és összes részszolgáltatása, is települnek.</span><span class="sxs-lookup"><span data-stu-id="28adf-130">The following configuration ensures that the **Web-Server** (IIS) and **SMTP Server** features, and all subfeatures of each, are installed.</span></span>

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