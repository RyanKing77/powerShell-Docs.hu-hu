---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: A DSC ProcessSet erőforrás
ms.openlocfilehash: d3c7383da5fd10580612527465ab621004ee7269
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="dsc-windowsprocess-resource"></a><span data-ttu-id="7fcd6-103">A DSC WindowsProcess erőforrás</span><span class="sxs-lookup"><span data-stu-id="7fcd6-103">DSC WindowsProcess Resource</span></span>

> <span data-ttu-id="7fcd6-104">Vonatkozik: A Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="7fcd6-104">Applies To: Windows PowerShell 5.0</span></span>

<span data-ttu-id="7fcd6-105">A **ProcessSet** erőforrás a Windows PowerShell szükséges konfiguráló (DSC) folyamatok konfigurálása egy célcsomóponttal mechanizmust biztosít.</span><span class="sxs-lookup"><span data-stu-id="7fcd6-105">The **ProcessSet** resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to configure processes on a target node.</span></span> <span data-ttu-id="7fcd6-106">Az erőforrás egy [összetett erőforrás](authoringResourceComposite.md) , amely meghívja a [WindowsProcess erőforrás](windowsProcessResource.md) minden egyes megadott csoport számára a `GroupName` paraméter.</span><span class="sxs-lookup"><span data-stu-id="7fcd6-106">This resource is a [composite resource](authoringResourceComposite.md) that calls the [WindowsProcess resource](windowsProcessResource.md) for each group specified in the `GroupName` parameter.</span></span>

## <a name="syntax"></a><span data-ttu-id="7fcd6-107">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="7fcd6-107">Syntax</span></span>

```
WindowsProcess [string] #ResourceName
{
    Arguments = [string]
    Path = [string]
    [ Credential = [PSCredential] ]
    [ Ensure = [string] { Absent | Present }  ]
    [ StandardOutputPath = [string] ]
    [ StandardErrorPath = [string] ]
    [ StandardInputPath = [string] ]
    [ WorkingDirectory = [string] ]
    [ DependsOn = [string[]] ]
}
```

## <a name="properties"></a><span data-ttu-id="7fcd6-108">Tulajdonságok</span><span class="sxs-lookup"><span data-stu-id="7fcd6-108">Properties</span></span>
|  <span data-ttu-id="7fcd6-109">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="7fcd6-109">Property</span></span>  |  <span data-ttu-id="7fcd6-110">Leírás</span><span class="sxs-lookup"><span data-stu-id="7fcd6-110">Description</span></span>   |
|---|---|
| <span data-ttu-id="7fcd6-111">Argumentumok</span><span class="sxs-lookup"><span data-stu-id="7fcd6-111">Arguments</span></span>| <span data-ttu-id="7fcd6-112">A folyamat, argumentumokat tartalmazó karakterlánc-értéke.</span><span class="sxs-lookup"><span data-stu-id="7fcd6-112">A string that contains arguments to pass to the process as-is.</span></span> <span data-ttu-id="7fcd6-113">Ha több argumentumot továbbítani kell, helyezze őket az összes ezt a karakterláncot.</span><span class="sxs-lookup"><span data-stu-id="7fcd6-113">If you need to pass several arguments, put them all in this string.</span></span>|
| <span data-ttu-id="7fcd6-114">Elérési út</span><span class="sxs-lookup"><span data-stu-id="7fcd6-114">Path</span></span>| <span data-ttu-id="7fcd6-115">A folyamat végrehajtható fájlok elérési útjait.</span><span class="sxs-lookup"><span data-stu-id="7fcd6-115">The paths to the process executables.</span></span> <span data-ttu-id="7fcd6-116">Ha a végrehajtható fájlok (teljesen minősített elérési utak) nevét, a DSC-erőforrás keressen-e a környezet **elérési** változó (`$env:Path`) található a fájl.</span><span class="sxs-lookup"><span data-stu-id="7fcd6-116">If these are the names of the executable files (not fully qualified paths), the DSC resource will search the environment **Path** variable (`$env:Path`) to find the files.</span></span> <span data-ttu-id="7fcd6-117">Ha ez a tulajdonság értékének teljesen minősített elérési utak, DSC nem fogja használni a **elérési** környezeti változó található a fájl, és kivételhibát hiba történt az elérési utak közül bármelyik nem léteznek.</span><span class="sxs-lookup"><span data-stu-id="7fcd6-117">If the values of this property are fully qualified paths, DSC will not use the **Path** environment variable to find the files, and will throw an error if any of the paths do not exist.</span></span> <span data-ttu-id="7fcd6-118">Relatív útvonalak nem engedélyezettek.</span><span class="sxs-lookup"><span data-stu-id="7fcd6-118">Relative paths are not allowed.</span></span>|
| <span data-ttu-id="7fcd6-119">hitelesítő adatok</span><span class="sxs-lookup"><span data-stu-id="7fcd6-119">Credential</span></span>| <span data-ttu-id="7fcd6-120">Azt jelzi, hogy a hitelesítő adatokat kell elindítania a telepítést.</span><span class="sxs-lookup"><span data-stu-id="7fcd6-120">Indicates the credentials for starting the process.</span></span>|
| <span data-ttu-id="7fcd6-121">Győződjön meg arról</span><span class="sxs-lookup"><span data-stu-id="7fcd6-121">Ensure</span></span>| <span data-ttu-id="7fcd6-122">Meghatározza, hogy létezik-e a folyamatokat.</span><span class="sxs-lookup"><span data-stu-id="7fcd6-122">Specifies whether the processes exists.</span></span> <span data-ttu-id="7fcd6-123">Állítsa be ezt a tulajdonságot "Elérhető" Győződjön meg arról, hogy létezik-e a folyamat.</span><span class="sxs-lookup"><span data-stu-id="7fcd6-123">Set this property to "Present" to ensure that the process exists.</span></span> <span data-ttu-id="7fcd6-124">Egyéb esetben állítsa "Hiányzik".</span><span class="sxs-lookup"><span data-stu-id="7fcd6-124">Otherwise, set it to "Absent".</span></span> <span data-ttu-id="7fcd6-125">Az alapértelmezett érték az "Elérhető".</span><span class="sxs-lookup"><span data-stu-id="7fcd6-125">The default is "Present".</span></span>|
| <span data-ttu-id="7fcd6-126">StandardErrorPath</span><span class="sxs-lookup"><span data-stu-id="7fcd6-126">StandardErrorPath</span></span>| <span data-ttu-id="7fcd6-127">Az elérési utat, amelyhez a folyamatok írási standard hiba.</span><span class="sxs-lookup"><span data-stu-id="7fcd6-127">The path to which the processes write standard error.</span></span> <span data-ttu-id="7fcd6-128">Felülírja a meglévő fájlt.</span><span class="sxs-lookup"><span data-stu-id="7fcd6-128">Any existing file there will be overwritten.</span></span>|
| <span data-ttu-id="7fcd6-129">StandardInputPath</span><span class="sxs-lookup"><span data-stu-id="7fcd6-129">StandardInputPath</span></span>| <span data-ttu-id="7fcd6-130">Az adatfolyam, ahonnan a folyamat szabványos bemeneti kapja.</span><span class="sxs-lookup"><span data-stu-id="7fcd6-130">The stream from which the process receives standard input.</span></span>|
| <span data-ttu-id="7fcd6-131">StandardOutputPath</span><span class="sxs-lookup"><span data-stu-id="7fcd6-131">StandardOutputPath</span></span>| <span data-ttu-id="7fcd6-132">A fájl elérési útját a, amelyhez a folyamat szabványos kimeneti írása.</span><span class="sxs-lookup"><span data-stu-id="7fcd6-132">The path of the file to which the processes write standard output.</span></span> <span data-ttu-id="7fcd6-133">Felülírja a meglévő fájlt.</span><span class="sxs-lookup"><span data-stu-id="7fcd6-133">Any existing file there will be overwritten.</span></span>|
| <span data-ttu-id="7fcd6-134">WorkingDirectory</span><span class="sxs-lookup"><span data-stu-id="7fcd6-134">WorkingDirectory</span></span>| <span data-ttu-id="7fcd6-135">A folyamatok, az aktuális munkakönyvtárban használt helyet.</span><span class="sxs-lookup"><span data-stu-id="7fcd6-135">The location used as the current working directory for the processes.</span></span>|
| <span data-ttu-id="7fcd6-136">dependsOn</span><span class="sxs-lookup"><span data-stu-id="7fcd6-136">DependsOn</span></span> | <span data-ttu-id="7fcd6-137">Azt jelzi, hogy egy másik erőforrás konfigurációjának kell futtatni, mielőtt ehhez az erőforráshoz van konfigurálva.</span><span class="sxs-lookup"><span data-stu-id="7fcd6-137">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="7fcd6-138">Például, ha az erőforrás-konfiguráció azonosítója blokk futtatni kívánt parancsfájl első az **ResourceName** és annak típusa **_ResourceType**, szintaxisa a következő e tulajdonság használatával "DependsOn ="[ A ResourceType] ResourceName"".</span><span class="sxs-lookup"><span data-stu-id="7fcd6-138">For example, if the ID of the resource configuration script block that you want to run first is **ResourceName** and its type is **_ResourceType**, the syntax for using this property is \`DependsOn = "[ResourceType]ResourceName"\`\` .</span></span>|