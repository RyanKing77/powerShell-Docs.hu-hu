---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: DSC-WindowsFeature erőforrás
ms.openlocfilehash: 7a57f4b2797ab3bb202aea8b2543d1e3f14074e9
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55685969"
---
# <a name="dsc-windowsfeature-resource"></a><span data-ttu-id="18218-103">DSC-WindowsFeature erőforrás</span><span class="sxs-lookup"><span data-stu-id="18218-103">DSC WindowsFeature Resource</span></span>

> <span data-ttu-id="18218-104">Érvényes: Windows PowerShell 4.0-s, a Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="18218-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="18218-105">A **WindowsFeature** erőforrás a Windows PowerShell Desired State Configuration (DSC), győződjön meg arról, hogy szerepkörök és funkciók hozzáadásakor vagy eltávolításakor a cél csomópont mechanizmust biztosít.</span><span class="sxs-lookup"><span data-stu-id="18218-105">The **WindowsFeature** resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to ensure that roles and features are added or removed on a target node.</span></span>

## <a name="syntax"></a><span data-ttu-id="18218-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="18218-106">Syntax</span></span>

```
WindowsFeature [string] #ResourceName
{
    Name = [string]
    [ Credential = [PSCredential] ]
    [ Ensure = [string] { Absent | Present }  ]
    [ IncludeAllSubFeature = [bool] ]
    [ LogPath = [string] ]
    [ DependsOn = [string[]] ]
    [ Source = [string] ]
}
```

## <a name="properties"></a><span data-ttu-id="18218-107">Tulajdonságok</span><span class="sxs-lookup"><span data-stu-id="18218-107">Properties</span></span>

|  <span data-ttu-id="18218-108">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="18218-108">Property</span></span>  |  <span data-ttu-id="18218-109">Leírás</span><span class="sxs-lookup"><span data-stu-id="18218-109">Description</span></span>   |
|---|---|
| <span data-ttu-id="18218-110">Név</span><span class="sxs-lookup"><span data-stu-id="18218-110">Name</span></span>| <span data-ttu-id="18218-111">Azt jelzi, hogy biztosítani kívánt szerepkör vagy szolgáltatás neve hozzáadva vagy eltávolítva.</span><span class="sxs-lookup"><span data-stu-id="18218-111">Indicates the name of the role or feature that you want to ensure is added or removed.</span></span> <span data-ttu-id="18218-112">Ez ugyanaz, mint az a __neve__ tulajdonságot a [Get-WindowsFeature](/powershell/module/servermanager/Get-WindowsFeature) parancsmagot, és nem a szerepkör vagy szolgáltatás megjelenített nevét.</span><span class="sxs-lookup"><span data-stu-id="18218-112">This is the same as the __Name__ property from the [Get-WindowsFeature](/powershell/module/servermanager/Get-WindowsFeature) cmdlet, and not the display name of the role or feature.</span></span>|
| <span data-ttu-id="18218-113">Hitelesítő adatok</span><span class="sxs-lookup"><span data-stu-id="18218-113">Credential</span></span>| <span data-ttu-id="18218-114">Azt jelzi, hogy a hitelesítő adatok hozzáadása vagy eltávolítása a szerepkör vagy szolgáltatás használatára.</span><span class="sxs-lookup"><span data-stu-id="18218-114">Indicates the credentials to use to add or remove the role or feature.</span></span>|
| <span data-ttu-id="18218-115">Győződjön meg, hogy</span><span class="sxs-lookup"><span data-stu-id="18218-115">Ensure</span></span>| <span data-ttu-id="18218-116">Azt jelzi, ha a szerepkör vagy szolgáltatás kerül.</span><span class="sxs-lookup"><span data-stu-id="18218-116">Indicates if the role or feature is added.</span></span> <span data-ttu-id="18218-117">Annak érdekében, hogy a szerepkör vagy szolgáltatás hozzá, állítsa be ezt a tulajdonságot a "E" annak érdekében, hogy a szerepkör vagy szolgáltatás eltávolítása a tulajdonság értéke "Hiányzik".</span><span class="sxs-lookup"><span data-stu-id="18218-117">To ensure that the role or feature is added, set this property to "Present" To ensure that the role or feature is removed, set the property to "Absent".</span></span>|
| <span data-ttu-id="18218-118">IncludeAllSubFeature</span><span class="sxs-lookup"><span data-stu-id="18218-118">IncludeAllSubFeature</span></span>| <span data-ttu-id="18218-119">Ez a tulajdonság beállítása __$true__ adja meg a szolgáltatás állapotával minden szükséges alfunkció állapotának biztosítása érdekében a __neve__ tulajdonság.</span><span class="sxs-lookup"><span data-stu-id="18218-119">Set this property to __$true__ to ensure the state of all required subfeatures with the state of the feature you specify with the __Name__ property.</span></span>|
| <span data-ttu-id="18218-120">LogPath</span><span class="sxs-lookup"><span data-stu-id="18218-120">LogPath</span></span>| <span data-ttu-id="18218-121">Azt jelzi, ha szeretne bejelentkezni a műveletet az erőforrás-szolgáltató naplófájl elérési útja.</span><span class="sxs-lookup"><span data-stu-id="18218-121">Indicates the path to a log file where you want the resource provider to log the operation.</span></span>|
| <span data-ttu-id="18218-122">DependsOn</span><span class="sxs-lookup"><span data-stu-id="18218-122">DependsOn</span></span>| <span data-ttu-id="18218-123">Azt jelzi, hogy a konfigurációt egy másik erőforrás futtatnia kell, mielőtt az erőforrás konfigurálva van.</span><span class="sxs-lookup"><span data-stu-id="18218-123">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="18218-124">Például, ha az erőforrás-konfiguráció azonosítója letiltása, a futtatni kívánt parancsfájl először van __ResourceName__ és a típusa __ResourceType__, ez a tulajdonság használata esetén `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="18218-124">For example, if the ID of the resource configuration script block that you want to run first is __ResourceName__ and its type is __ResourceType__, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|
| <span data-ttu-id="18218-125">Forrás</span><span class="sxs-lookup"><span data-stu-id="18218-125">Source</span></span>| <span data-ttu-id="18218-126">Azt jelzi, használható a telepítéshez, a forrás-fájl helyét, ha szükséges.</span><span class="sxs-lookup"><span data-stu-id="18218-126">Indicates the location of the source file to use for installation, if necessary.</span></span>|

## <a name="example"></a><span data-ttu-id="18218-127">Példa</span><span class="sxs-lookup"><span data-stu-id="18218-127">Example</span></span>
```powershell
WindowsFeature RoleExample
{
    Ensure = "Present"
    # Alternatively, to ensure the role is uninstalled, set Ensure to "Absent"
    Name = "Web-Server" # Use the Name property from Get-WindowsFeature
}
```