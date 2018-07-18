---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: DSC WindowsProcess erőforrás
ms.openlocfilehash: 3c4e6d8377c3dcbf4f1db87a603d5483b8caafb8
ms.sourcegitcommit: 77f62a55cac8c13d69d51eef5fade18f71d66955
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/17/2018
ms.locfileid: "39093735"
---
# <a name="dsc-windowsprocess-resource"></a><span data-ttu-id="c0fc3-103">DSC WindowsProcess erőforrás</span><span class="sxs-lookup"><span data-stu-id="c0fc3-103">DSC WindowsProcess Resource</span></span>

> <span data-ttu-id="c0fc3-104">A következőkre vonatkozik: Windows PowerShell 4.0-s, a Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="c0fc3-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="c0fc3-105">A **WindowsProcess** erőforrás a Windows PowerShell Desired State Configuration (DSC) cél csomóponton folyamatok konfigurálása mechanizmust biztosít.</span><span class="sxs-lookup"><span data-stu-id="c0fc3-105">The **WindowsProcess** resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to configure processes on a target node.</span></span>

## <a name="syntax"></a><span data-ttu-id="c0fc3-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="c0fc3-106">Syntax</span></span>

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

## <a name="properties"></a><span data-ttu-id="c0fc3-107">Tulajdonságok</span><span class="sxs-lookup"><span data-stu-id="c0fc3-107">Properties</span></span>

|  <span data-ttu-id="c0fc3-108">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="c0fc3-108">Property</span></span>  |  <span data-ttu-id="c0fc3-109">Leírás</span><span class="sxs-lookup"><span data-stu-id="c0fc3-109">Description</span></span>   |
|---|---|
| <span data-ttu-id="c0fc3-110">Argumentumok</span><span class="sxs-lookup"><span data-stu-id="c0fc3-110">Arguments</span></span>| <span data-ttu-id="c0fc3-111">Azt jelzi, hogy egy karakterlánc, a folyamat argumentumokat-van.</span><span class="sxs-lookup"><span data-stu-id="c0fc3-111">Indicates a string of arguments to pass to the process as-is.</span></span> <span data-ttu-id="c0fc3-112">Ha több argumentumokat át van szüksége, helyezi őket az ezt a karakterláncot.</span><span class="sxs-lookup"><span data-stu-id="c0fc3-112">If you need to pass several arguments, put them all in this string.</span></span>|
| <span data-ttu-id="c0fc3-113">Elérési út</span><span class="sxs-lookup"><span data-stu-id="c0fc3-113">Path</span></span>| <span data-ttu-id="c0fc3-114">A folyamat végrehajtható fájl elérési útja.</span><span class="sxs-lookup"><span data-stu-id="c0fc3-114">The path to the process executable.</span></span> <span data-ttu-id="c0fc3-115">Ha ez a végrehajtható fájl (nem teljes elérési útja), a DSC-erőforrás neve fog keresni a környezet **elérési** változó (`$env:Path`) található a végrehajtható fájl.</span><span class="sxs-lookup"><span data-stu-id="c0fc3-115">If this the file name of the executable (not the fully qualified path), the DSC resource will search the environment **Path** variable (`$env:Path`) to find the executable file.</span></span> <span data-ttu-id="c0fc3-116">Ha ez a tulajdonság értéke teljes elérési útja, DSC nem fogja használni a **elérési út** környezeti változót, keresse meg a fájlt, és hibát váltja, ha az elérési út nem létezik.</span><span class="sxs-lookup"><span data-stu-id="c0fc3-116">If the value of this property is a fully qualified path, DSC will not use the **Path** environment variable to find the file, and will throw an error if the path does not exist.</span></span> <span data-ttu-id="c0fc3-117">Relatív elérési utakat nem engedélyezettek.</span><span class="sxs-lookup"><span data-stu-id="c0fc3-117">Relative paths are not allowed.</span></span>|
| <span data-ttu-id="c0fc3-118">Hitelesítő adatok</span><span class="sxs-lookup"><span data-stu-id="c0fc3-118">Credential</span></span>| <span data-ttu-id="c0fc3-119">Azt jelzi, hogy a hitelesítő adatokat a folyamat indításához.</span><span class="sxs-lookup"><span data-stu-id="c0fc3-119">Indicates the credentials for starting the process.</span></span>|
| <span data-ttu-id="c0fc3-120">Győződjön meg, hogy</span><span class="sxs-lookup"><span data-stu-id="c0fc3-120">Ensure</span></span>| <span data-ttu-id="c0fc3-121">Azt jelzi, hogy létezik-e a folyamat.</span><span class="sxs-lookup"><span data-stu-id="c0fc3-121">Indicates if the process exists.</span></span> <span data-ttu-id="c0fc3-122">Ezzel a tulajdonsággal, "E" Győződjön meg arról, hogy létezik-e a folyamat.</span><span class="sxs-lookup"><span data-stu-id="c0fc3-122">Set this property to "Present" to ensure that the process exists.</span></span> <span data-ttu-id="c0fc3-123">Ellenkező esetben állítsa "Hiányzik".</span><span class="sxs-lookup"><span data-stu-id="c0fc3-123">Otherwise, set it to "Absent".</span></span> <span data-ttu-id="c0fc3-124">Az alapértelmezett érték "E".</span><span class="sxs-lookup"><span data-stu-id="c0fc3-124">The default is "Present".</span></span>|
| <span data-ttu-id="c0fc3-125">DependsOn</span><span class="sxs-lookup"><span data-stu-id="c0fc3-125">DependsOn</span></span> | <span data-ttu-id="c0fc3-126">Azt jelzi, hogy a konfigurációt egy másik erőforrás futtatnia kell, mielőtt az erőforrás konfigurálva van.</span><span class="sxs-lookup"><span data-stu-id="c0fc3-126">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="c0fc3-127">Például, ha az erőforrás-konfiguráció azonosítója parancsfájl-blokk futtatni kívánt első az **ResourceName** és a típusa **ResourceType**, esetén ez a tulajdonság használatával "DependsOn"[a = Erőforrástípus] ResourceName"s".</span><span class="sxs-lookup"><span data-stu-id="c0fc3-127">For example, if the ID of the resource configuration script block that you want to run first is **ResourceName** and its type is **ResourceType**, the syntax for using this property is \`DependsOn = "[ResourceType]ResourceName"\`\` .</span></span>|
| <span data-ttu-id="c0fc3-128">StandardErrorPath</span><span class="sxs-lookup"><span data-stu-id="c0fc3-128">StandardErrorPath</span></span>| <span data-ttu-id="c0fc3-129">Azt jelzi, hogy a könyvtár elérési útja a normál hiba írni.</span><span class="sxs-lookup"><span data-stu-id="c0fc3-129">Indicates the directory path to write the standard error.</span></span> <span data-ttu-id="c0fc3-130">Minden olyan meglévő fájl felül lesznek írva.</span><span class="sxs-lookup"><span data-stu-id="c0fc3-130">Any existing file there will be overwritten.</span></span>|
| <span data-ttu-id="c0fc3-131">StandardInputPath</span><span class="sxs-lookup"><span data-stu-id="c0fc3-131">StandardInputPath</span></span>| <span data-ttu-id="c0fc3-132">A szabványos bemeneti helyét jelöli.</span><span class="sxs-lookup"><span data-stu-id="c0fc3-132">Indicates the standard input location.</span></span>|
| <span data-ttu-id="c0fc3-133">StandardOutputPath</span><span class="sxs-lookup"><span data-stu-id="c0fc3-133">StandardOutputPath</span></span>| <span data-ttu-id="c0fc3-134">Azt jelzi, hogy a hely a normál a kimenetbe írhat.</span><span class="sxs-lookup"><span data-stu-id="c0fc3-134">Indicates the location to write the standard output.</span></span> <span data-ttu-id="c0fc3-135">Minden olyan meglévő fájl felül lesznek írva.</span><span class="sxs-lookup"><span data-stu-id="c0fc3-135">Any existing file there will be overwritten.</span></span>|
| <span data-ttu-id="c0fc3-136">WorkingDirectory</span><span class="sxs-lookup"><span data-stu-id="c0fc3-136">WorkingDirectory</span></span>| <span data-ttu-id="c0fc3-137">Azt jelzi, hogy a helyre, amely a folyamat az aktuális munkakönyvtár lesz.</span><span class="sxs-lookup"><span data-stu-id="c0fc3-137">Indicates the location that will be used as the current working directory for the process.</span></span>|