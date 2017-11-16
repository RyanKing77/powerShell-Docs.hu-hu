---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "A DSC WindowsProcess erőforrás"
ms.openlocfilehash: c34d3cb1d4d9b899b45fba7b4b148a7c977f5365
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2017
---
# <a name="dsc-windowsprocess-resource"></a><span data-ttu-id="8d15f-103">A DSC WindowsProcess erőforrás</span><span class="sxs-lookup"><span data-stu-id="8d15f-103">DSC WindowsProcess Resource</span></span>

> <span data-ttu-id="8d15f-104">Vonatkozik: A Windows PowerShell 4.0-s verzióját, a Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="8d15f-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="8d15f-105">A **WindowsProcess** erőforrás a Windows PowerShell szükséges konfiguráló (DSC) folyamatok konfigurálása egy célcsomóponttal mechanizmust biztosít.</span><span class="sxs-lookup"><span data-stu-id="8d15f-105">The **WindowsProcess** resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to configure processes on a target node.</span></span>

## <a name="syntax"></a><span data-ttu-id="8d15f-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="8d15f-106">Syntax</span></span>

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

## <a name="properties"></a><span data-ttu-id="8d15f-107">Tulajdonságok</span><span class="sxs-lookup"><span data-stu-id="8d15f-107">Properties</span></span>
|  <span data-ttu-id="8d15f-108">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="8d15f-108">Property</span></span>  |  <span data-ttu-id="8d15f-109">Leírás</span><span class="sxs-lookup"><span data-stu-id="8d15f-109">Description</span></span>   | 
|---|---| 
| <span data-ttu-id="8d15f-110">Argumentumok</span><span class="sxs-lookup"><span data-stu-id="8d15f-110">Arguments</span></span>| <span data-ttu-id="8d15f-111">Azt jelzi, a folyamat argumentumokat karakterlánc-értéke.</span><span class="sxs-lookup"><span data-stu-id="8d15f-111">Indicates a string of arguments to pass to the process as-is.</span></span> <span data-ttu-id="8d15f-112">Ha több argumentumot továbbítani kell, helyezze őket az összes ezt a karakterláncot.</span><span class="sxs-lookup"><span data-stu-id="8d15f-112">If you need to pass several arguments, put them all in this string.</span></span>| 
| <span data-ttu-id="8d15f-113">Elérési út</span><span class="sxs-lookup"><span data-stu-id="8d15f-113">Path</span></span>| <span data-ttu-id="8d15f-114">A folyamat végrehajtható fájl elérési útja.</span><span class="sxs-lookup"><span data-stu-id="8d15f-114">The path to the process executable.</span></span> <span data-ttu-id="8d15f-115">Ha ez a végrehajtható fájl (nem a teljes elérési útja), a DSC-erőforrás nevét átvizsgálja a környezet **elérési** változó (`$env:Path`) található a végrehajtható fájl.</span><span class="sxs-lookup"><span data-stu-id="8d15f-115">If this the file name of the executable (not the fully qualified path), the DSC resource will search the environment **Path** variable (`$env:Path`) to find the executable file.</span></span> <span data-ttu-id="8d15f-116">Ha ez a tulajdonság értéke egy teljesen minősített elérési útja, DSC nem fogja használni a **elérési** környezeti változót megtalálják a fájlt, és a rendszer hibaüzenetet küldjön, ha az elérési út nem létezik.</span><span class="sxs-lookup"><span data-stu-id="8d15f-116">If the value of this property is a fully qualified path, DSC will not use the **Path** environment variable to find the file, and will throw an error if the path does not exist.</span></span> <span data-ttu-id="8d15f-117">Relatív útvonalak nem engedélyezettek.</span><span class="sxs-lookup"><span data-stu-id="8d15f-117">Relative paths are not allowed.</span></span>| 
| <span data-ttu-id="8d15f-118">hitelesítő adatok</span><span class="sxs-lookup"><span data-stu-id="8d15f-118">Credential</span></span>| <span data-ttu-id="8d15f-119">Azt jelzi, hogy a hitelesítő adatokat kell elindítania a telepítést.</span><span class="sxs-lookup"><span data-stu-id="8d15f-119">Indicates the credentials for starting the process.</span></span>| 
| <span data-ttu-id="8d15f-120">Győződjön meg arról</span><span class="sxs-lookup"><span data-stu-id="8d15f-120">Ensure</span></span>| <span data-ttu-id="8d15f-121">Azt jelzi, hogy létezik-e a folyamat.</span><span class="sxs-lookup"><span data-stu-id="8d15f-121">Indicates if the process exists.</span></span> <span data-ttu-id="8d15f-122">Állítsa be ezt a tulajdonságot "Elérhető" Győződjön meg arról, hogy létezik-e a folyamat.</span><span class="sxs-lookup"><span data-stu-id="8d15f-122">Set this property to "Present" to ensure that the process exists.</span></span> <span data-ttu-id="8d15f-123">Egyéb esetben állítsa "Hiányzik".</span><span class="sxs-lookup"><span data-stu-id="8d15f-123">Otherwise, set it to "Absent".</span></span> <span data-ttu-id="8d15f-124">Az alapértelmezett érték az "Elérhető".</span><span class="sxs-lookup"><span data-stu-id="8d15f-124">The default is "Present".</span></span>| 
| <span data-ttu-id="8d15f-125">dependsOn</span><span class="sxs-lookup"><span data-stu-id="8d15f-125">DependsOn</span></span> | <span data-ttu-id="8d15f-126">Azt jelzi, hogy egy másik erőforrás konfigurációjának kell futtatni, mielőtt ehhez az erőforráshoz van konfigurálva.</span><span class="sxs-lookup"><span data-stu-id="8d15f-126">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="8d15f-127">Például, ha az erőforrás-konfiguráció azonosítója blokk futtatni kívánt parancsfájl első az __ResourceName__ és annak típusa __ResourceType__, szintaxisa a következő e tulajdonság használatával "DependsOn ="[ A ResourceType] ResourceName"".</span><span class="sxs-lookup"><span data-stu-id="8d15f-127">For example, if the ID of the resource configuration script block that you want to run first is __ResourceName__ and its type is __ResourceType__, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`\` .</span></span>| 
| <span data-ttu-id="8d15f-128">StandardErrorPath</span><span class="sxs-lookup"><span data-stu-id="8d15f-128">StandardErrorPath</span></span>| <span data-ttu-id="8d15f-129">Azt jelzi, hogy a könyvtár elérési útja a normál hiba írni.</span><span class="sxs-lookup"><span data-stu-id="8d15f-129">Indicates the directory path to write the standard error.</span></span> <span data-ttu-id="8d15f-130">Felülírja a meglévő fájlt.</span><span class="sxs-lookup"><span data-stu-id="8d15f-130">Any existing file there will be overwritten.</span></span>| 
| <span data-ttu-id="8d15f-131">StandardInputPath</span><span class="sxs-lookup"><span data-stu-id="8d15f-131">StandardInputPath</span></span>| <span data-ttu-id="8d15f-132">A szabványos bemeneti helyét jelöli.</span><span class="sxs-lookup"><span data-stu-id="8d15f-132">Indicates the standard input location.</span></span>| 
| <span data-ttu-id="8d15f-133">StandardOutputPath</span><span class="sxs-lookup"><span data-stu-id="8d15f-133">StandardOutputPath</span></span>| <span data-ttu-id="8d15f-134">Azt jelzi, hogy a helyet, ahova kiírhatná a normál a kimenetbe.</span><span class="sxs-lookup"><span data-stu-id="8d15f-134">Indicates the location to write the standard output.</span></span> <span data-ttu-id="8d15f-135">Felülírja a meglévő fájlt.</span><span class="sxs-lookup"><span data-stu-id="8d15f-135">Any existing file there will be overwritten.</span></span>| 
| <span data-ttu-id="8d15f-136">WorkingDirectory</span><span class="sxs-lookup"><span data-stu-id="8d15f-136">WorkingDirectory</span></span>| <span data-ttu-id="8d15f-137">Azt jelzi, hogy a helyet, a folyamat az aktuális munkakönyvtárban lesz.</span><span class="sxs-lookup"><span data-stu-id="8d15f-137">Indicates the location that will be used as the current working directory for the process.</span></span>| 

