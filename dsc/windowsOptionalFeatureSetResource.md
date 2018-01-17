---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "A DSC WindowsOptionalFeatureSet erőforrás"
ms.openlocfilehash: 6912e5cf92f23058342bc566bd66dc4be3357a30
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 01/17/2018
---
# <a name="dsc-windowsoptionalfeatureset-resource"></a><span data-ttu-id="6d4d8-103">A DSC WindowsOptionalFeatureSet erőforrás</span><span class="sxs-lookup"><span data-stu-id="6d4d8-103">DSC WindowsOptionalFeatureSet Resource</span></span>

> <span data-ttu-id="6d4d8-104">Vonatkozik: A Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="6d4d8-104">Applies To: Windows PowerShell 5.0</span></span>

<span data-ttu-id="6d4d8-105">A **WindowsOptionalFeatureSet** erőforrás a Windows PowerShell szükséges konfiguráló (DSC) lehetővé teszi annak érdekében, hogy az választható szolgáltatások engedélyezve vannak-e a célcsomóponton.</span><span class="sxs-lookup"><span data-stu-id="6d4d8-105">The **WindowsOptionalFeatureSet** resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to ensure that optional features are enabled on a target node.</span></span> <span data-ttu-id="6d4d8-106">Az erőforrás egy [összetett erőforrás](authoringResourceComposite.md) , amely meghívja a [WindowsOptionalFeature erőforrás](windowsOptionalFeatureResource.md) az egyes szolgáltatásokhoz megadott a `Name` tulajdonság.</span><span class="sxs-lookup"><span data-stu-id="6d4d8-106">This resource is a [composite resource](authoringResourceComposite.md) that calls the [WindowsOptionalFeature resource](windowsOptionalFeatureResource.md) for each feature specified in the `Name` property.</span></span>

<span data-ttu-id="6d4d8-107">Ehhez az erőforráshoz akkor használja, ha a Windows választható szolgáltatások állapot számos konfigurálni szeretné.</span><span class="sxs-lookup"><span data-stu-id="6d4d8-107">Use this resource when you want to configure a number of Windows optional features to the same state.</span></span>

## <a name="syntax"></a><span data-ttu-id="6d4d8-108">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="6d4d8-108">Syntax</span></span>

```
WindowsOptionalFeature [string] #ResourceName
{
    Name = [string[]]
    [ Ensure = [string] { Enable | Disable }  ]
    [ Source = [string] ] 
    [ RemoveFilesOnDisable = [bool] ]  
    [ LogPath = [string] ]
    [ NoWindowsUpdateCheck = [bool] ]
    [ LogLevel = [string] { ErrorsOnly | ErrorsAndWarning | ErrorsAndWarningAndInformation }  ]
    [ DependsOn = [string[]] ]
    
}
```

## <a name="properties"></a><span data-ttu-id="6d4d8-109">Tulajdonságok</span><span class="sxs-lookup"><span data-stu-id="6d4d8-109">Properties</span></span>

|  <span data-ttu-id="6d4d8-110">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="6d4d8-110">Property</span></span>  |  <span data-ttu-id="6d4d8-111">Leírás</span><span class="sxs-lookup"><span data-stu-id="6d4d8-111">Description</span></span>   | 
|---|---| 
| <span data-ttu-id="6d4d8-112">Név</span><span class="sxs-lookup"><span data-stu-id="6d4d8-112">Name</span></span>| <span data-ttu-id="6d4d8-113">Azt jelzi, a funkciókat, amelyeket szeretne biztosítani a neve engedélyezésekor vagy letiltásakor.</span><span class="sxs-lookup"><span data-stu-id="6d4d8-113">Indicates the name of the features that you want to ensure are enabled or disabled.</span></span>| 
| <span data-ttu-id="6d4d8-114">Győződjön meg arról</span><span class="sxs-lookup"><span data-stu-id="6d4d8-114">Ensure</span></span>| <span data-ttu-id="6d4d8-115">Meghatározza, hogy engedélyezett-e a szolgáltatásokat.</span><span class="sxs-lookup"><span data-stu-id="6d4d8-115">Specifies whether the features are enabled.</span></span> <span data-ttu-id="6d4d8-116">Ezzel biztosíthatja, hogy a szolgáltatások engedélyezett, állítsa be ezt a tulajdonságot "Engedélyezés" Győződjön meg arról, hogy a szolgáltatások le vannak tiltva, a tulajdonság értéke "Letiltás".</span><span class="sxs-lookup"><span data-stu-id="6d4d8-116">To ensure that the features are enabled, set this property to "Enable" To ensure that the features are disabled, set the property to "Disable".</span></span>|
| <span data-ttu-id="6d4d8-117">Forrás</span><span class="sxs-lookup"><span data-stu-id="6d4d8-117">Source</span></span>| <span data-ttu-id="6d4d8-118">Nincs megvalósítva.</span><span class="sxs-lookup"><span data-stu-id="6d4d8-118">Not implemented.</span></span>|
| <span data-ttu-id="6d4d8-119">NoWindowsUpdateCheck</span><span class="sxs-lookup"><span data-stu-id="6d4d8-119">NoWindowsUpdateCheck</span></span>| <span data-ttu-id="6d4d8-120">Meghatározza, hogy DISM kapcsolódik-e a Windows Update (WU), a funkciók engedélyezésére forrásfájlok keresésekor.</span><span class="sxs-lookup"><span data-stu-id="6d4d8-120">Specifies whether DISM contacts Windows Update (WU) when searching for the source files to enable features.</span></span> <span data-ttu-id="6d4d8-121">Ha $true, DISM nem tud kapcsolódni a WU.</span><span class="sxs-lookup"><span data-stu-id="6d4d8-121">If $true, DISM does not contact WU.</span></span>|
| <span data-ttu-id="6d4d8-122">RemoveFilesOnDisable</span><span class="sxs-lookup"><span data-stu-id="6d4d8-122">RemoveFilesOnDisable</span></span>| <span data-ttu-id="6d4d8-123">Beállítása **$true** eltávolítja, ha le vannak tiltva, a szolgáltatások társított összes fájlt (Ez azt jelenti, hogy ha **ellenőrizze, hogy** be van állítva a "Hiányzik").</span><span class="sxs-lookup"><span data-stu-id="6d4d8-123">Set to **$true** to remove all files associated with the features when they are disabled (that is, when **Ensure** is set to "Absent").</span></span>|
| <span data-ttu-id="6d4d8-124">Naplózási szint</span><span class="sxs-lookup"><span data-stu-id="6d4d8-124">LogLevel</span></span>| <span data-ttu-id="6d4d8-125">A naplókban megjelenő legnagyobb kimeneti szintet.</span><span class="sxs-lookup"><span data-stu-id="6d4d8-125">The maximum output level shown in the logs.</span></span> <span data-ttu-id="6d4d8-126">Az elfogadott értékei: "ErrorsOnly" (csak a hibák naplózása), "ErrorsAndWarning" (hibák és figyelmeztetések naplózása van), és a "ErrorsAndWarningAndInformation" (hibák figyelmeztetések és hibakeresési információ bejelentkezett).</span><span class="sxs-lookup"><span data-stu-id="6d4d8-126">The accepted values are: "ErrorsOnly" (only errors are logged), "ErrorsAndWarning" (errors and warnings are logged), and "ErrorsAndWarningAndInformation" (errors, warnings, and debug information are logged).</span></span>|
| <span data-ttu-id="6d4d8-127">LogPath</span><span class="sxs-lookup"><span data-stu-id="6d4d8-127">LogPath</span></span>| <span data-ttu-id="6d4d8-128">A naplófájl elérési útja a kívánt való bejelentkezéshez a műveletet az erőforrás-szolgáltató.</span><span class="sxs-lookup"><span data-stu-id="6d4d8-128">The path to a log file where you want the resource provider to log the operation.</span></span>| 
| <span data-ttu-id="6d4d8-129">dependsOn</span><span class="sxs-lookup"><span data-stu-id="6d4d8-129">DependsOn</span></span>| <span data-ttu-id="6d4d8-130">Meghatározza, hogy egy másik erőforrás konfigurációjának kell futtatni, mielőtt ehhez az erőforráshoz van konfigurálva.</span><span class="sxs-lookup"><span data-stu-id="6d4d8-130">Specifies that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="6d4d8-131">Például, ha az erőforrás-konfiguráció azonosítója blokk futtatni kívánt parancsfájl első az __ResourceName__ és annak típusa __ResourceType__, az e tulajdonság használatával szintaxisa a következő `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="6d4d8-131">For example, if the ID of the resource configuration script block that you want to run first is __ResourceName__ and its type is __ResourceType__, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>| 
 



