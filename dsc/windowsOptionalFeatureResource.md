---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: A DSC-WindowsOptionalFeature erőforrás
ms.openlocfilehash: 4cb59151d69adb2a01b7c4bdcaf0e961c24b29a6
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="dsc-windowsoptionalfeature-resource"></a><span data-ttu-id="3c713-103">A DSC-WindowsOptionalFeature erőforrás</span><span class="sxs-lookup"><span data-stu-id="3c713-103">DSC WindowsOptionalFeature Resource</span></span>

> <span data-ttu-id="3c713-104">Vonatkozik: A Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="3c713-104">Applies To: Windows PowerShell 5.0</span></span>

<span data-ttu-id="3c713-105">A **WindowsOptionalFeature** erőforrás a Windows PowerShell szükséges konfiguráló (DSC) lehetővé teszi annak érdekében, hogy az választható szolgáltatások engedélyezve vannak-e a célcsomóponton.</span><span class="sxs-lookup"><span data-stu-id="3c713-105">The **WindowsOptionalFeature** resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to ensure that optional features are enabled on a target node.</span></span>

## <a name="syntax"></a><span data-ttu-id="3c713-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="3c713-106">Syntax</span></span>

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

## <a name="properties"></a><span data-ttu-id="3c713-107">Tulajdonságok</span><span class="sxs-lookup"><span data-stu-id="3c713-107">Properties</span></span>

|  <span data-ttu-id="3c713-108">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="3c713-108">Property</span></span>  |  <span data-ttu-id="3c713-109">Leírás</span><span class="sxs-lookup"><span data-stu-id="3c713-109">Description</span></span>   |
|---|---|
| <span data-ttu-id="3c713-110">Név</span><span class="sxs-lookup"><span data-stu-id="3c713-110">Name</span></span>| <span data-ttu-id="3c713-111">Azt jelzi, hogy biztos szeretne lenni abban a szolgáltatás neve engedélyezve vagy letiltva.</span><span class="sxs-lookup"><span data-stu-id="3c713-111">Indicates the name of the feature that you want to ensure is enabled or disabled.</span></span>|
| <span data-ttu-id="3c713-112">Győződjön meg arról</span><span class="sxs-lookup"><span data-stu-id="3c713-112">Ensure</span></span>| <span data-ttu-id="3c713-113">Meghatározza, hogy engedélyezve van-e a szolgáltatás.</span><span class="sxs-lookup"><span data-stu-id="3c713-113">Specifies whether the feature is enabled.</span></span> <span data-ttu-id="3c713-114">Annak biztosításához, hogy a szolgáltatás engedélyezve van, állítsa be ezt a tulajdonságot "Engedélyezés" Győződjön meg arról, hogy a szolgáltatás le van tiltva, a tulajdonság értéke "Letiltás".</span><span class="sxs-lookup"><span data-stu-id="3c713-114">To ensure that the feature is enabled, set this property to "Enable" To ensure that the feature is disabled, set the property to "Disable".</span></span>|
| <span data-ttu-id="3c713-115">Forrás</span><span class="sxs-lookup"><span data-stu-id="3c713-115">Source</span></span>| <span data-ttu-id="3c713-116">Nincs megvalósítva.</span><span class="sxs-lookup"><span data-stu-id="3c713-116">Not implemented.</span></span>|
| <span data-ttu-id="3c713-117">NoWindowsUpdateCheck</span><span class="sxs-lookup"><span data-stu-id="3c713-117">NoWindowsUpdateCheck</span></span>| <span data-ttu-id="3c713-118">Meghatározza, hogy DISM kapcsolódik-e a Windows Update (WU), a funkció engedélyezéséhez a forrásfájlok keresésekor.</span><span class="sxs-lookup"><span data-stu-id="3c713-118">Specifies whether DISM contacts Windows Update (WU) when searching for the source files to enable a feature.</span></span> <span data-ttu-id="3c713-119">Ha $true, DISM nem tud kapcsolódni a WU.</span><span class="sxs-lookup"><span data-stu-id="3c713-119">If $true, DISM does not contact WU.</span></span>|
| <span data-ttu-id="3c713-120">RemoveFilesOnDisable</span><span class="sxs-lookup"><span data-stu-id="3c713-120">RemoveFilesOnDisable</span></span>| <span data-ttu-id="3c713-121">Beállítása **$true** eltávolítja, ha le van tiltva, a szolgáltatás társított összes fájlt (Ez azt jelenti, hogy ha **ellenőrizze, hogy** be van állítva a "Hiányzik").</span><span class="sxs-lookup"><span data-stu-id="3c713-121">Set to **$true** to remove all files associated with the feature when it is disabled (that is, when **Ensure** is set to "Absent").</span></span>|
| <span data-ttu-id="3c713-122">Naplózási szint</span><span class="sxs-lookup"><span data-stu-id="3c713-122">LogLevel</span></span>| <span data-ttu-id="3c713-123">A naplókban megjelenő legnagyobb kimeneti szintet.</span><span class="sxs-lookup"><span data-stu-id="3c713-123">The maximum output level shown in the logs.</span></span> <span data-ttu-id="3c713-124">Az elfogadott értékei: "ErrorsOnly" (csak a hibák naplózása), "ErrorsAndWarning" (hibák és figyelmeztetések naplózása van), és a "ErrorsAndWarningAndInformation" (hibák figyelmeztetések és hibakeresési információ bejelentkezett).</span><span class="sxs-lookup"><span data-stu-id="3c713-124">The accepted values are: "ErrorsOnly" (only errors are logged), "ErrorsAndWarning" (errors and warnings are logged), and "ErrorsAndWarningAndInformation" (errors, warnings, and debug information are logged).</span></span>|
| <span data-ttu-id="3c713-125">LogPath</span><span class="sxs-lookup"><span data-stu-id="3c713-125">LogPath</span></span>| <span data-ttu-id="3c713-126">A naplófájl elérési útja a kívánt való bejelentkezéshez a műveletet az erőforrás-szolgáltató.</span><span class="sxs-lookup"><span data-stu-id="3c713-126">The path to a log file where you want the resource provider to log the operation.</span></span>|
| <span data-ttu-id="3c713-127">dependsOn</span><span class="sxs-lookup"><span data-stu-id="3c713-127">DependsOn</span></span>| <span data-ttu-id="3c713-128">Meghatározza, hogy egy másik erőforrás konfigurációjának kell futtatni, mielőtt ehhez az erőforráshoz van konfigurálva.</span><span class="sxs-lookup"><span data-stu-id="3c713-128">Specifies that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="3c713-129">Például, ha az erőforrás-konfiguráció azonosítója blokk futtatni kívánt parancsfájl első az __ResourceName__ és annak típusa __ResourceType__, az e tulajdonság használatával szintaxisa a következő `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="3c713-129">For example, if the ID of the resource configuration script block that you want to run first is __ResourceName__ and its type is __ResourceType__, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|