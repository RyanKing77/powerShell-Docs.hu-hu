---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: DSC WindowsProcess erőforrás
ms.openlocfilehash: cee93ab283ded407d6e032161125aa6d6ac98827
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 01/04/2019
ms.locfileid: "54048465"
---
# <a name="dsc-windowsprocess-resource"></a><span data-ttu-id="9f84a-103">DSC WindowsProcess erőforrás</span><span class="sxs-lookup"><span data-stu-id="9f84a-103">DSC WindowsProcess Resource</span></span>

<span data-ttu-id="9f84a-104">_A következőkre vonatkozik: Windows PowerShell 4.0-s, a Windows PowerShell 5.0_</span><span class="sxs-lookup"><span data-stu-id="9f84a-104">_Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0_</span></span>

<span data-ttu-id="9f84a-105">A **WindowsProcess** erőforrás a Windows PowerShell Desired State Configuration (DSC) cél csomóponton folyamatok konfigurálása mechanizmust biztosít.</span><span class="sxs-lookup"><span data-stu-id="9f84a-105">The **WindowsProcess** resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to configure processes on a target node.</span></span>

## <a name="syntax"></a><span data-ttu-id="9f84a-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="9f84a-106">Syntax</span></span>

```
WindowsProcess [string] #ResourceName
{
    Arguments = [string]
    Path = [string]
    [ Credential = [PSCredential] ]
    [ Ensure = [string] { Absent | Present }  ]
    [ DependsOn = [string[]] ]
    [ StandardErrorPath = [string] ]
    [ StandardInputPath = [string] ]
    [ StandardOutputPath = [string] ]
    [ WorkingDirectory = [string] ]
}
```

## <a name="properties"></a><span data-ttu-id="9f84a-107">Tulajdonságok</span><span class="sxs-lookup"><span data-stu-id="9f84a-107">Properties</span></span>

| <span data-ttu-id="9f84a-108">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="9f84a-108">Property</span></span> | <span data-ttu-id="9f84a-109">Leírás</span><span class="sxs-lookup"><span data-stu-id="9f84a-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="9f84a-110">Argumentumok</span><span class="sxs-lookup"><span data-stu-id="9f84a-110">Arguments</span></span>| <span data-ttu-id="9f84a-111">Azt jelzi, hogy egy karakterlánc, a folyamat argumentumokat-van.</span><span class="sxs-lookup"><span data-stu-id="9f84a-111">Indicates a string of arguments to pass to the process as-is.</span></span> <span data-ttu-id="9f84a-112">Ha több argumentumokat át van szüksége, helyezi őket az ezt a karakterláncot.</span><span class="sxs-lookup"><span data-stu-id="9f84a-112">If you need to pass several arguments, put them all in this string.</span></span>|
| <span data-ttu-id="9f84a-113">Elérési út</span><span class="sxs-lookup"><span data-stu-id="9f84a-113">Path</span></span>| <span data-ttu-id="9f84a-114">A folyamat végrehajtható fájl elérési útja.</span><span class="sxs-lookup"><span data-stu-id="9f84a-114">The path to the process executable.</span></span> <span data-ttu-id="9f84a-115">Ha ez a végrehajtható fájl (nem teljes elérési útja), a DSC-erőforrás neve fog keresni a környezet **elérési** változó (`$env:Path`) található a végrehajtható fájl.</span><span class="sxs-lookup"><span data-stu-id="9f84a-115">If this the file name of the executable (not the fully qualified path), the DSC resource will search the environment **Path** variable (`$env:Path`) to find the executable file.</span></span> <span data-ttu-id="9f84a-116">Ha ez a tulajdonság értéke teljes elérési útja, DSC nem fogja használni a **elérési út** környezeti változót, keresse meg a fájlt, és hibát váltja, ha az elérési út nem létezik.</span><span class="sxs-lookup"><span data-stu-id="9f84a-116">If the value of this property is a fully qualified path, DSC will not use the **Path** environment variable to find the file, and will throw an error if the path does not exist.</span></span> <span data-ttu-id="9f84a-117">Relatív elérési utakat nem engedélyezettek.</span><span class="sxs-lookup"><span data-stu-id="9f84a-117">Relative paths are not allowed.</span></span>|
| <span data-ttu-id="9f84a-118">Hitelesítő adatok</span><span class="sxs-lookup"><span data-stu-id="9f84a-118">Credential</span></span>| <span data-ttu-id="9f84a-119">Azt jelzi, hogy a hitelesítő adatokat a folyamat indításához.</span><span class="sxs-lookup"><span data-stu-id="9f84a-119">Indicates the credentials for starting the process.</span></span>|
| <span data-ttu-id="9f84a-120">Győződjön meg, hogy</span><span class="sxs-lookup"><span data-stu-id="9f84a-120">Ensure</span></span>| <span data-ttu-id="9f84a-121">Azt jelzi, hogy létezik-e a folyamat.</span><span class="sxs-lookup"><span data-stu-id="9f84a-121">Indicates if the process exists.</span></span> <span data-ttu-id="9f84a-122">Ezzel a tulajdonsággal, "E" Győződjön meg arról, hogy létezik-e a folyamat.</span><span class="sxs-lookup"><span data-stu-id="9f84a-122">Set this property to "Present" to ensure that the process exists.</span></span> <span data-ttu-id="9f84a-123">Ellenkező esetben állítsa "Hiányzik".</span><span class="sxs-lookup"><span data-stu-id="9f84a-123">Otherwise, set it to "Absent".</span></span> <span data-ttu-id="9f84a-124">Az alapértelmezett érték "E".</span><span class="sxs-lookup"><span data-stu-id="9f84a-124">The default is "Present".</span></span>|
| <span data-ttu-id="9f84a-125">DependsOn</span><span class="sxs-lookup"><span data-stu-id="9f84a-125">DependsOn</span></span> | <span data-ttu-id="9f84a-126">Azt jelzi, hogy a konfigurációt egy másik erőforrás futtatnia kell, mielőtt az erőforrás konfigurálva van.</span><span class="sxs-lookup"><span data-stu-id="9f84a-126">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="9f84a-127">Például, ha az erőforrás-konfiguráció azonosítója letiltása, a futtatni kívánt parancsfájl először van **ResourceName** és a típusa **ResourceType**, ez a tulajdonság használata esetén `DependsOn = "[ResourceType]ResourceName"` .</span><span class="sxs-lookup"><span data-stu-id="9f84a-127">For example, if the ID of the resource configuration script block that you want to run first is **ResourceName** and its type is **ResourceType**, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"` .</span></span>|
| <span data-ttu-id="9f84a-128">StandardErrorPath</span><span class="sxs-lookup"><span data-stu-id="9f84a-128">StandardErrorPath</span></span>| <span data-ttu-id="9f84a-129">Azt jelzi, hogy a könyvtár elérési útja a normál hiba írni.</span><span class="sxs-lookup"><span data-stu-id="9f84a-129">Indicates the directory path to write the standard error.</span></span> <span data-ttu-id="9f84a-130">Minden olyan meglévő fájl felül lesznek írva.</span><span class="sxs-lookup"><span data-stu-id="9f84a-130">Any existing file there will be overwritten.</span></span>|
| <span data-ttu-id="9f84a-131">StandardInputPath</span><span class="sxs-lookup"><span data-stu-id="9f84a-131">StandardInputPath</span></span>| <span data-ttu-id="9f84a-132">A szabványos bemeneti helyét jelöli.</span><span class="sxs-lookup"><span data-stu-id="9f84a-132">Indicates the standard input location.</span></span>|
| <span data-ttu-id="9f84a-133">StandardOutputPath</span><span class="sxs-lookup"><span data-stu-id="9f84a-133">StandardOutputPath</span></span>| <span data-ttu-id="9f84a-134">Azt jelzi, hogy a hely a normál a kimenetbe írhat.</span><span class="sxs-lookup"><span data-stu-id="9f84a-134">Indicates the location to write the standard output.</span></span> <span data-ttu-id="9f84a-135">Minden olyan meglévő fájl felül lesznek írva.</span><span class="sxs-lookup"><span data-stu-id="9f84a-135">Any existing file there will be overwritten.</span></span>|
| <span data-ttu-id="9f84a-136">WorkingDirectory</span><span class="sxs-lookup"><span data-stu-id="9f84a-136">WorkingDirectory</span></span>| <span data-ttu-id="9f84a-137">Azt jelzi, hogy a helyre, amely a folyamat az aktuális munkakönyvtár lesz.</span><span class="sxs-lookup"><span data-stu-id="9f84a-137">Indicates the location that will be used as the current working directory for the process.</span></span>|