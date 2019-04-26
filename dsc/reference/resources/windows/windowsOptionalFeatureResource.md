---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: DSC-WindowsOptionalFeature erőforrás
ms.openlocfilehash: 390caefd2ad190afc651b22ed1beb5cf1d604527
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62076758"
---
# <a name="dsc-windowsoptionalfeature-resource"></a><span data-ttu-id="6cadb-103">DSC-WindowsOptionalFeature erőforrás</span><span class="sxs-lookup"><span data-stu-id="6cadb-103">DSC WindowsOptionalFeature Resource</span></span>

> <span data-ttu-id="6cadb-104">A következőkre vonatkozik: Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="6cadb-104">Applies To: Windows PowerShell 5.0</span></span>

<span data-ttu-id="6cadb-105">A **WindowsOptionalFeature** erőforrás a Windows PowerShell Desired State Configuration (DSC), győződjön meg arról, hogy választható szolgáltatások engedélyezve vannak-e a cél csomópont mechanizmust biztosít.</span><span class="sxs-lookup"><span data-stu-id="6cadb-105">The **WindowsOptionalFeature** resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to ensure that optional features are enabled on a target node.</span></span>

## <a name="syntax"></a><span data-ttu-id="6cadb-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="6cadb-106">Syntax</span></span>

```
WindowsOptionalFeature [string] #ResourceName
{
    Name = [string]
    [ Ensure = [string] { Enable | Disable }  ]
    [ Source = [string] ]
    [ NoWindowsUpdateCheck = [bool] ]
    [ RemoveFilesOnDisable = [bool] ]
    [ LogLevel = [string] { ErrorsOnly | ErrorsAndWarning | ErrorsAndWarningAndInformation }  ]
    [ LogPath = [string] ]
    [ DependsOn = [string[]] ]

}
```

## <a name="properties"></a><span data-ttu-id="6cadb-107">Tulajdonságok</span><span class="sxs-lookup"><span data-stu-id="6cadb-107">Properties</span></span>

|  <span data-ttu-id="6cadb-108">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="6cadb-108">Property</span></span>  |  <span data-ttu-id="6cadb-109">Leírás</span><span class="sxs-lookup"><span data-stu-id="6cadb-109">Description</span></span>   |
|---|---|
| <span data-ttu-id="6cadb-110">Név</span><span class="sxs-lookup"><span data-stu-id="6cadb-110">Name</span></span>| <span data-ttu-id="6cadb-111">Azt jelzi, hogy azt szeretné, a szolgáltatás neve engedélyezve van, vagy le van tiltva.</span><span class="sxs-lookup"><span data-stu-id="6cadb-111">Indicates the name of the feature that you want to ensure is enabled or disabled.</span></span>|
| <span data-ttu-id="6cadb-112">Győződjön meg, hogy</span><span class="sxs-lookup"><span data-stu-id="6cadb-112">Ensure</span></span>| <span data-ttu-id="6cadb-113">Itt adhatja meg, hogy engedélyezve van-e a szolgáltatás.</span><span class="sxs-lookup"><span data-stu-id="6cadb-113">Specifies whether the feature is enabled.</span></span> <span data-ttu-id="6cadb-114">Annak érdekében, hogy a funkció engedélyezve van, állítsa be ezt a tulajdonságot az "Engedélyezés" annak érdekében, hogy a szolgáltatás le van tiltva, a tulajdonság értéke "Letiltás".</span><span class="sxs-lookup"><span data-stu-id="6cadb-114">To ensure that the feature is enabled, set this property to "Enable" To ensure that the feature is disabled, set the property to "Disable".</span></span>|
| <span data-ttu-id="6cadb-115">Forrás</span><span class="sxs-lookup"><span data-stu-id="6cadb-115">Source</span></span>| <span data-ttu-id="6cadb-116">Není implementována.</span><span class="sxs-lookup"><span data-stu-id="6cadb-116">Not implemented.</span></span>|
| <span data-ttu-id="6cadb-117">NoWindowsUpdateCheck</span><span class="sxs-lookup"><span data-stu-id="6cadb-117">NoWindowsUpdateCheck</span></span>| <span data-ttu-id="6cadb-118">Itt adhatja meg, e DISM csatlakozik-e a Windows Update (WU), a funkció engedélyezéséhez a forrásfájlok keresésekor.</span><span class="sxs-lookup"><span data-stu-id="6cadb-118">Specifies whether DISM contacts Windows Update (WU) when searching for the source files to enable a feature.</span></span> <span data-ttu-id="6cadb-119">Ha $true, DISM nem lép kapcsolatba a WU-hoz.</span><span class="sxs-lookup"><span data-stu-id="6cadb-119">If $true, DISM does not contact WU.</span></span>|
| <span data-ttu-id="6cadb-120">RemoveFilesOnDisable</span><span class="sxs-lookup"><span data-stu-id="6cadb-120">RemoveFilesOnDisable</span></span>| <span data-ttu-id="6cadb-121">Állítsa **$true** eltávolítja, ha le van tiltva a szolgáltatás kapcsolódó fájlok (azt jelenti, amikor **ellenőrizze, hogy** van beállítva a "Hiányzó").</span><span class="sxs-lookup"><span data-stu-id="6cadb-121">Set to **$true** to remove all files associated with the feature when it is disabled (that is, when **Ensure** is set to "Absent").</span></span>|
| <span data-ttu-id="6cadb-122">Naplózási szint</span><span class="sxs-lookup"><span data-stu-id="6cadb-122">LogLevel</span></span>| <span data-ttu-id="6cadb-123">A naplókban megjelenő legnagyobb kimeneti szintet.</span><span class="sxs-lookup"><span data-stu-id="6cadb-123">The maximum output level shown in the logs.</span></span> <span data-ttu-id="6cadb-124">Az elfogadott értékek a következők: (Csak a hibák naplózása) "ErrorsOnly", "ErrorsAndWarning" (hibák és figyelmeztetések naplózása van), és a "ErrorsAndWarningAndInformation" (hibák figyelmeztetések és hibakeresési információkat naplózza).</span><span class="sxs-lookup"><span data-stu-id="6cadb-124">The accepted values are: "ErrorsOnly" (only errors are logged), "ErrorsAndWarning" (errors and warnings are logged), and "ErrorsAndWarningAndInformation" (errors, warnings, and debug information are logged).</span></span>|
| <span data-ttu-id="6cadb-125">LogPath</span><span class="sxs-lookup"><span data-stu-id="6cadb-125">LogPath</span></span>| <span data-ttu-id="6cadb-126">Ha szeretne bejelentkezni a műveletet az erőforrás-szolgáltató naplófájl elérési útja.</span><span class="sxs-lookup"><span data-stu-id="6cadb-126">The path to a log file where you want the resource provider to log the operation.</span></span>|
| <span data-ttu-id="6cadb-127">DependsOn</span><span class="sxs-lookup"><span data-stu-id="6cadb-127">DependsOn</span></span>| <span data-ttu-id="6cadb-128">Itt adhatja meg, hogy a konfigurációt egy másik erőforrás futtatnia kell, mielőtt az erőforrás konfigurálva van.</span><span class="sxs-lookup"><span data-stu-id="6cadb-128">Specifies that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="6cadb-129">Például, ha az erőforrás-konfiguráció azonosítója letiltása, a futtatni kívánt parancsfájl először van __ResourceName__ és a típusa __ResourceType__, ez a tulajdonság használata esetén `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="6cadb-129">For example, if the ID of the resource configuration script block that you want to run first is __ResourceName__ and its type is __ResourceType__, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|