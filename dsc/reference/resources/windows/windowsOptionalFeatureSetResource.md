---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: DSC WindowsOptionalFeatureSet erőforrás
ms.openlocfilehash: c27d026e01bbb443a82112e37f1d199fb3482e49
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55683946"
---
# <a name="dsc-windowsoptionalfeatureset-resource"></a><span data-ttu-id="9c9fa-103">DSC WindowsOptionalFeatureSet erőforrás</span><span class="sxs-lookup"><span data-stu-id="9c9fa-103">DSC WindowsOptionalFeatureSet Resource</span></span>

> <span data-ttu-id="9c9fa-104">Érvényes: Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="9c9fa-104">Applies To: Windows PowerShell 5.0</span></span>

<span data-ttu-id="9c9fa-105">A **WindowsOptionalFeatureSet** erőforrás a Windows PowerShell Desired State Configuration (DSC), győződjön meg arról, hogy választható szolgáltatások engedélyezve vannak-e a cél csomópont mechanizmust biztosít.</span><span class="sxs-lookup"><span data-stu-id="9c9fa-105">The **WindowsOptionalFeatureSet** resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to ensure that optional features are enabled on a target node.</span></span>
<span data-ttu-id="9c9fa-106">Ez az erőforrás egy [összetett erőforrás](../../../resources/authoringResourceComposite.md) , amely meghívja a [WindowsOptionalFeature erőforrás](windowsOptionalFeatureResource.md) az egyes szolgáltatásokhoz, megadva a `Name` tulajdonság.</span><span class="sxs-lookup"><span data-stu-id="9c9fa-106">This resource is a [composite resource](../../../resources/authoringResourceComposite.md) that calls the [WindowsOptionalFeature resource](windowsOptionalFeatureResource.md) for each feature specified in the `Name` property.</span></span>

<span data-ttu-id="9c9fa-107">Akkor használja ezt az erőforrást, ha szeretne konfigurálni egy választható funkciók Windows állapot számát.</span><span class="sxs-lookup"><span data-stu-id="9c9fa-107">Use this resource when you want to configure a number of Windows optional features to the same state.</span></span>

## <a name="syntax"></a><span data-ttu-id="9c9fa-108">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="9c9fa-108">Syntax</span></span>

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

## <a name="properties"></a><span data-ttu-id="9c9fa-109">Tulajdonságok</span><span class="sxs-lookup"><span data-stu-id="9c9fa-109">Properties</span></span>

|  <span data-ttu-id="9c9fa-110">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="9c9fa-110">Property</span></span>  |  <span data-ttu-id="9c9fa-111">Leírás</span><span class="sxs-lookup"><span data-stu-id="9c9fa-111">Description</span></span>   |
|---|---|
| <span data-ttu-id="9c9fa-112">Név</span><span class="sxs-lookup"><span data-stu-id="9c9fa-112">Name</span></span>| <span data-ttu-id="9c9fa-113">Azt jelzi, hogy a biztosítani kívánt szolgáltatások nevére vannak engedélyezve vagy letiltva.</span><span class="sxs-lookup"><span data-stu-id="9c9fa-113">Indicates the name of the features that you want to ensure are enabled or disabled.</span></span>|
| <span data-ttu-id="9c9fa-114">Győződjön meg, hogy</span><span class="sxs-lookup"><span data-stu-id="9c9fa-114">Ensure</span></span>| <span data-ttu-id="9c9fa-115">Itt adhatja meg, hogy engedélyezve vannak-e az a funkciók.</span><span class="sxs-lookup"><span data-stu-id="9c9fa-115">Specifies whether the features are enabled.</span></span> <span data-ttu-id="9c9fa-116">Annak érdekében, hogy az funkciók engedélyezve van, állítsa be ezt a tulajdonságot az "Engedélyezés" annak érdekében, hogy a szolgáltatások le vannak tiltva, a tulajdonság értéke "Letiltás".</span><span class="sxs-lookup"><span data-stu-id="9c9fa-116">To ensure that the features are enabled, set this property to "Enable" To ensure that the features are disabled, set the property to "Disable".</span></span>|
| <span data-ttu-id="9c9fa-117">Forrás</span><span class="sxs-lookup"><span data-stu-id="9c9fa-117">Source</span></span>| <span data-ttu-id="9c9fa-118">Není implementována.</span><span class="sxs-lookup"><span data-stu-id="9c9fa-118">Not implemented.</span></span>|
| <span data-ttu-id="9c9fa-119">NoWindowsUpdateCheck</span><span class="sxs-lookup"><span data-stu-id="9c9fa-119">NoWindowsUpdateCheck</span></span>| <span data-ttu-id="9c9fa-120">Itt adhatja meg, e DISM csatlakozik-e a Windows Update (WU),-szolgáltatások engedélyezése a forrásfájlok keresése.</span><span class="sxs-lookup"><span data-stu-id="9c9fa-120">Specifies whether DISM contacts Windows Update (WU) when searching for the source files to enable features.</span></span> <span data-ttu-id="9c9fa-121">Ha $true, DISM nem lép kapcsolatba a WU-hoz.</span><span class="sxs-lookup"><span data-stu-id="9c9fa-121">If $true, DISM does not contact WU.</span></span>|
| <span data-ttu-id="9c9fa-122">RemoveFilesOnDisable</span><span class="sxs-lookup"><span data-stu-id="9c9fa-122">RemoveFilesOnDisable</span></span>| <span data-ttu-id="9c9fa-123">Beállítása **$true** eltávolítja, ha le vannak tiltva, az a funkciók az hozzárendelt összes fájl (azt jelenti, amikor **ellenőrizze, hogy** be van állítva a "Hiányzó").</span><span class="sxs-lookup"><span data-stu-id="9c9fa-123">Set to **$true** to remove all files associated with the features when they are disabled (that is, when **Ensure** is set to "Absent").</span></span>|
| <span data-ttu-id="9c9fa-124">Naplózási szint</span><span class="sxs-lookup"><span data-stu-id="9c9fa-124">LogLevel</span></span>| <span data-ttu-id="9c9fa-125">A naplókban megjelenő legnagyobb kimeneti szintet.</span><span class="sxs-lookup"><span data-stu-id="9c9fa-125">The maximum output level shown in the logs.</span></span> <span data-ttu-id="9c9fa-126">Az elfogadott értékek a következők: (Csak a hibák naplózása) "ErrorsOnly", "ErrorsAndWarning" (hibák és figyelmeztetések naplózása van), és a "ErrorsAndWarningAndInformation" (hibák figyelmeztetések és hibakeresési információkat naplózza).</span><span class="sxs-lookup"><span data-stu-id="9c9fa-126">The accepted values are: "ErrorsOnly" (only errors are logged), "ErrorsAndWarning" (errors and warnings are logged), and "ErrorsAndWarningAndInformation" (errors, warnings, and debug information are logged).</span></span>|
| <span data-ttu-id="9c9fa-127">LogPath</span><span class="sxs-lookup"><span data-stu-id="9c9fa-127">LogPath</span></span>| <span data-ttu-id="9c9fa-128">Ha szeretne bejelentkezni a műveletet az erőforrás-szolgáltató naplófájl elérési útja.</span><span class="sxs-lookup"><span data-stu-id="9c9fa-128">The path to a log file where you want the resource provider to log the operation.</span></span>|
| <span data-ttu-id="9c9fa-129">DependsOn</span><span class="sxs-lookup"><span data-stu-id="9c9fa-129">DependsOn</span></span>| <span data-ttu-id="9c9fa-130">Itt adhatja meg, hogy a konfigurációt egy másik erőforrás futtatnia kell, mielőtt az erőforrás konfigurálva van.</span><span class="sxs-lookup"><span data-stu-id="9c9fa-130">Specifies that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="9c9fa-131">Például, ha az erőforrás-konfiguráció azonosítója letiltása, a futtatni kívánt parancsfájl először van __ResourceName__ és a típusa __ResourceType__, ez a tulajdonság használata esetén `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="9c9fa-131">For example, if the ID of the resource configuration script block that you want to run first is __ResourceName__ and its type is __ResourceType__, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|
