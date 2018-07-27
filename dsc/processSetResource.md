---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: DSC ProcessSet erőforrás
ms.openlocfilehash: 33000786a9e17e11168b5e08c3bcfcacf3af2611
ms.sourcegitcommit: c3f1a83b59484651119630f3089aa51b6e7d4c3c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/26/2018
ms.locfileid: "39268017"
---
# <a name="dsc-windowsprocess-resource"></a><span data-ttu-id="70d51-103">DSC WindowsProcess erőforrás</span><span class="sxs-lookup"><span data-stu-id="70d51-103">DSC WindowsProcess Resource</span></span>

<span data-ttu-id="70d51-104">_A következőkre vonatkozik: Windows PowerShell 5.0_</span><span class="sxs-lookup"><span data-stu-id="70d51-104">_Applies To: Windows PowerShell 5.0_</span></span>

<span data-ttu-id="70d51-105">A **ProcessSet** erőforrás a Windows PowerShell Desired State Configuration (DSC) cél csomóponton folyamatok konfigurálása mechanizmust biztosít.</span><span class="sxs-lookup"><span data-stu-id="70d51-105">The **ProcessSet** resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to configure processes on a target node.</span></span> <span data-ttu-id="70d51-106">Ez az erőforrás egy [összetett erőforrás](authoringResourceComposite.md) , amely meghívja a [WindowsProcess erőforrás](windowsProcessResource.md) minden egyes megadott csoport számára a `GroupName` paraméter.</span><span class="sxs-lookup"><span data-stu-id="70d51-106">This resource is a [composite resource](authoringResourceComposite.md) that calls the [WindowsProcess resource](windowsProcessResource.md) for each group specified in the `GroupName` parameter.</span></span>

## <a name="syntax"></a><span data-ttu-id="70d51-107">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="70d51-107">Syntax</span></span>

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

## <a name="properties"></a><span data-ttu-id="70d51-108">Tulajdonságok</span><span class="sxs-lookup"><span data-stu-id="70d51-108">Properties</span></span>

| <span data-ttu-id="70d51-109">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="70d51-109">Property</span></span> | <span data-ttu-id="70d51-110">Leírás</span><span class="sxs-lookup"><span data-stu-id="70d51-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="70d51-111">Argumentumok</span><span class="sxs-lookup"><span data-stu-id="70d51-111">Arguments</span></span>| <span data-ttu-id="70d51-112">A folyamat, argumentumokat tartalmazó karakterlánc-van.</span><span class="sxs-lookup"><span data-stu-id="70d51-112">A string that contains arguments to pass to the process as-is.</span></span> <span data-ttu-id="70d51-113">Ha több argumentumokat át van szüksége, helyezi őket az ezt a karakterláncot.</span><span class="sxs-lookup"><span data-stu-id="70d51-113">If you need to pass several arguments, put them all in this string.</span></span>|
| <span data-ttu-id="70d51-114">Elérési út</span><span class="sxs-lookup"><span data-stu-id="70d51-114">Path</span></span>| <span data-ttu-id="70d51-115">A folyamat végrehajtható fájlok elérési útja.</span><span class="sxs-lookup"><span data-stu-id="70d51-115">The paths to the process executables.</span></span> <span data-ttu-id="70d51-116">Ha tartoznak a végrehajtható fájlok (teljesen minősített elérési út) nevét, a DSC-erőforrás fog keresni a környezet **elérési útja** változó (`$env:Path`) található fájlokat.</span><span class="sxs-lookup"><span data-stu-id="70d51-116">If these are the names of the executable files (not fully qualified paths), the DSC resource will search the environment **Path** variable (`$env:Path`) to find the files.</span></span> <span data-ttu-id="70d51-117">Ha ez a tulajdonság értékét teljesen minősített elérési utak, DSC nem fogja használni a **elérési útja** környezeti változót, keresse meg a fájlokat, és hibát váltja, ha bármely, az elérési utak nem léteznek.</span><span class="sxs-lookup"><span data-stu-id="70d51-117">If the values of this property are fully qualified paths, DSC will not use the **Path** environment variable to find the files, and will throw an error if any of the paths do not exist.</span></span> <span data-ttu-id="70d51-118">Relatív elérési utakat nem engedélyezettek.</span><span class="sxs-lookup"><span data-stu-id="70d51-118">Relative paths are not allowed.</span></span>|
| <span data-ttu-id="70d51-119">Hitelesítő adatok</span><span class="sxs-lookup"><span data-stu-id="70d51-119">Credential</span></span>| <span data-ttu-id="70d51-120">Azt jelzi, hogy a hitelesítő adatokat a folyamat indításához.</span><span class="sxs-lookup"><span data-stu-id="70d51-120">Indicates the credentials for starting the process.</span></span>|
| <span data-ttu-id="70d51-121">Győződjön meg, hogy</span><span class="sxs-lookup"><span data-stu-id="70d51-121">Ensure</span></span>| <span data-ttu-id="70d51-122">Itt adhatja meg, hogy létezik-e a folyamatokat.</span><span class="sxs-lookup"><span data-stu-id="70d51-122">Specifies whether the processes exists.</span></span> <span data-ttu-id="70d51-123">Ezzel a tulajdonsággal, "E" Győződjön meg arról, hogy létezik-e a folyamat.</span><span class="sxs-lookup"><span data-stu-id="70d51-123">Set this property to "Present" to ensure that the process exists.</span></span> <span data-ttu-id="70d51-124">Ellenkező esetben állítsa "Hiányzik".</span><span class="sxs-lookup"><span data-stu-id="70d51-124">Otherwise, set it to "Absent".</span></span> <span data-ttu-id="70d51-125">Az alapértelmezett érték "E".</span><span class="sxs-lookup"><span data-stu-id="70d51-125">The default is "Present".</span></span>|
| <span data-ttu-id="70d51-126">StandardErrorPath</span><span class="sxs-lookup"><span data-stu-id="70d51-126">StandardErrorPath</span></span>| <span data-ttu-id="70d51-127">Az elérési út, amelyre a folyamatok írási standard hiba.</span><span class="sxs-lookup"><span data-stu-id="70d51-127">The path to which the processes write standard error.</span></span> <span data-ttu-id="70d51-128">Minden olyan meglévő fájl felül lesznek írva.</span><span class="sxs-lookup"><span data-stu-id="70d51-128">Any existing file there will be overwritten.</span></span>|
| <span data-ttu-id="70d51-129">StandardInputPath</span><span class="sxs-lookup"><span data-stu-id="70d51-129">StandardInputPath</span></span>| <span data-ttu-id="70d51-130">A streamet, amelyből a folyamat megkapja a standard bemenetet.</span><span class="sxs-lookup"><span data-stu-id="70d51-130">The stream from which the process receives standard input.</span></span>|
| <span data-ttu-id="70d51-131">StandardOutputPath</span><span class="sxs-lookup"><span data-stu-id="70d51-131">StandardOutputPath</span></span>| <span data-ttu-id="70d51-132">A fájl, amelyre a folyamatok írási standard kimenet elérési útja.</span><span class="sxs-lookup"><span data-stu-id="70d51-132">The path of the file to which the processes write standard output.</span></span> <span data-ttu-id="70d51-133">Minden olyan meglévő fájl felül lesznek írva.</span><span class="sxs-lookup"><span data-stu-id="70d51-133">Any existing file there will be overwritten.</span></span>|
| <span data-ttu-id="70d51-134">WorkingDirectory</span><span class="sxs-lookup"><span data-stu-id="70d51-134">WorkingDirectory</span></span>| <span data-ttu-id="70d51-135">A folyamatok, az aktuális munkakönyvtárban használt helyet.</span><span class="sxs-lookup"><span data-stu-id="70d51-135">The location used as the current working directory for the processes.</span></span>|
| <span data-ttu-id="70d51-136">DependsOn</span><span class="sxs-lookup"><span data-stu-id="70d51-136">DependsOn</span></span> | <span data-ttu-id="70d51-137">Azt jelzi, hogy a konfigurációt egy másik erőforrás futtatnia kell, mielőtt az erőforrás konfigurálva van.</span><span class="sxs-lookup"><span data-stu-id="70d51-137">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="70d51-138">Például, ha az erőforrás-konfiguráció azonosítója letiltása, a futtatni kívánt parancsfájl először van **ResourceName** és a típusa **_ResourceType**, ez a tulajdonság használata esetén `DependsOn = "[ResourceType]ResourceName"` .</span><span class="sxs-lookup"><span data-stu-id="70d51-138">For example, if the ID of the resource configuration script block that you want to run first is **ResourceName** and its type is **_ResourceType**, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"` .</span></span>|