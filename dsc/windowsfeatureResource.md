---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: A DSC-WindowsFeature erőforrás
ms.openlocfilehash: e22f40d5a30b470bc322bd7fa3a065e6806d5cd5
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="dsc-windowsfeature-resource"></a><span data-ttu-id="665db-103">A DSC-WindowsFeature erőforrás</span><span class="sxs-lookup"><span data-stu-id="665db-103">DSC WindowsFeature Resource</span></span>

> <span data-ttu-id="665db-104">Vonatkozik: A Windows PowerShell 4.0-s verzióját, a Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="665db-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="665db-105">A **WindowsFeature** erőforrás a Windows PowerShell szükséges konfiguráló (DSC) Győződjön meg arról, hogy szerepkörök és szolgáltatások hozzáadása vagy eltávolítása egy célcsomóponttal mechanizmust biztosít.</span><span class="sxs-lookup"><span data-stu-id="665db-105">The **WindowsFeature** resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to ensure that roles and features are added or removed on a target node.</span></span>

## <a name="syntax"></a><span data-ttu-id="665db-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="665db-106">Syntax</span></span>

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

## <a name="properties"></a><span data-ttu-id="665db-107">Tulajdonságok</span><span class="sxs-lookup"><span data-stu-id="665db-107">Properties</span></span>

|  <span data-ttu-id="665db-108">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="665db-108">Property</span></span>  |  <span data-ttu-id="665db-109">Leírás</span><span class="sxs-lookup"><span data-stu-id="665db-109">Description</span></span>   |
|---|---|
| <span data-ttu-id="665db-110">Név</span><span class="sxs-lookup"><span data-stu-id="665db-110">Name</span></span>| <span data-ttu-id="665db-111">Azt jelzi, biztosítani kívánt szerepkör vagy szolgáltatás neve hozzáadni vagy eltávolítani.</span><span class="sxs-lookup"><span data-stu-id="665db-111">Indicates the name of the role or feature that you want to ensure is added or removed.</span></span> <span data-ttu-id="665db-112">Megegyezik a a __neve__ tulajdonságot a [Get-WindowsFeature](/powershell/module/servermanager/Get-WindowsFeature) parancsmagot, és nem a szerepkör vagy szolgáltatás megjelenített nevét.</span><span class="sxs-lookup"><span data-stu-id="665db-112">This is the same as the __Name__ property from the [Get-WindowsFeature](/powershell/module/servermanager/Get-WindowsFeature) cmdlet, and not the display name of the role or feature.</span></span>|
| <span data-ttu-id="665db-113">hitelesítő adatok</span><span class="sxs-lookup"><span data-stu-id="665db-113">Credential</span></span>| <span data-ttu-id="665db-114">Azt jelzi, hogy a hitelesítő adatok hozzáadása vagy eltávolítása a szerepkör vagy szolgáltatás használata.</span><span class="sxs-lookup"><span data-stu-id="665db-114">Indicates the credentials to use to add or remove the role or feature.</span></span>|
| <span data-ttu-id="665db-115">Győződjön meg arról</span><span class="sxs-lookup"><span data-stu-id="665db-115">Ensure</span></span>| <span data-ttu-id="665db-116">Azt jelzi, ha a szerepkör vagy szolgáltatás kerül.</span><span class="sxs-lookup"><span data-stu-id="665db-116">Indicates if the role or feature is added.</span></span> <span data-ttu-id="665db-117">Annak biztosításához, hogy a szerepkör vagy szolgáltatás hozzá, állítsa be ezt a tulajdonságot "Elérhető" Győződjön meg arról, hogy a szerepkör vagy szolgáltatás eltávolítása a tulajdonság értéke "Hiányzik".</span><span class="sxs-lookup"><span data-stu-id="665db-117">To ensure that the role or feature is added, set this property to "Present" To ensure that the role or feature is removed, set the property to "Absent".</span></span>|
| <span data-ttu-id="665db-118">IncludeAllSubFeature</span><span class="sxs-lookup"><span data-stu-id="665db-118">IncludeAllSubFeature</span></span>| <span data-ttu-id="665db-119">Ez a tulajdonság beállítása __$true__ adja meg, ha az összes szükséges alfunkció és a szolgáltatás állapotának állapotának biztosításához a __neve__ tulajdonság.</span><span class="sxs-lookup"><span data-stu-id="665db-119">Set this property to __$true__ to ensure the state of all required subfeatures with the state of the feature you specify with the __Name__ property.</span></span>|
| <span data-ttu-id="665db-120">LogPath</span><span class="sxs-lookup"><span data-stu-id="665db-120">LogPath</span></span>| <span data-ttu-id="665db-121">Azt jelzi, hogy a naplófájl elérési útja a kívánt való bejelentkezéshez a műveletet az erőforrás-szolgáltató.</span><span class="sxs-lookup"><span data-stu-id="665db-121">Indicates the path to a log file where you want the resource provider to log the operation.</span></span>|
| <span data-ttu-id="665db-122">dependsOn</span><span class="sxs-lookup"><span data-stu-id="665db-122">DependsOn</span></span>| <span data-ttu-id="665db-123">Azt jelzi, hogy egy másik erőforrás konfigurációjának kell futtatni, mielőtt ehhez az erőforráshoz van konfigurálva.</span><span class="sxs-lookup"><span data-stu-id="665db-123">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="665db-124">Például, ha az erőforrás-konfiguráció azonosítója blokk futtatni kívánt parancsfájl első az __ResourceName__ és annak típusa __ResourceType__, az e tulajdonság használatával szintaxisa a következő `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="665db-124">For example, if the ID of the resource configuration script block that you want to run first is __ResourceName__ and its type is __ResourceType__, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|
| <span data-ttu-id="665db-125">Forrás</span><span class="sxs-lookup"><span data-stu-id="665db-125">Source</span></span>| <span data-ttu-id="665db-126">Azt jelzi, használható a telepítéshez, a forrás-fájl helyét, ha szükséges.</span><span class="sxs-lookup"><span data-stu-id="665db-126">Indicates the location of the source file to use for installation, if necessary.</span></span>|

## <a name="example"></a><span data-ttu-id="665db-127">Példa</span><span class="sxs-lookup"><span data-stu-id="665db-127">Example</span></span>
```powershell
WindowsFeature RoleExample
{
    Ensure = "Present"
    # Alternatively, to ensure the role is uninstalled, set Ensure to "Absent"
    Name = "Web-Server" # Use the Name property from Get-WindowsFeature
}
```