---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "A DSC-környezet erőforrás"
ms.openlocfilehash: 7c98798fa0e8fc865798ea30530e41ac87b2dadc
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2017
---
# <a name="dsc-environment-resource"></a><span data-ttu-id="c5455-103">A DSC-környezet erőforrás</span><span class="sxs-lookup"><span data-stu-id="c5455-103">DSC Environment Resource</span></span>

> <span data-ttu-id="c5455-104">Vonatkozik: A Windows PowerShell 4.0-s verzióját, a Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="c5455-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="c5455-105">A __környezet__ erőforrás a Windows PowerShell szükséges konfiguráló (DSC) lehetővé teszi a rendszerszintű környezeti változókat kezeléséhez.</span><span class="sxs-lookup"><span data-stu-id="c5455-105">The __Environment__ resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to manage system environment variables.</span></span>

## <a name="syntax"></a><span data-ttu-id="c5455-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="c5455-106">Syntax</span></span>
``` mof
Environment [string] #ResourceName
{
    Name = [string]
    [ Ensure = [string] { Absent | Present }  ]
    [ Path = [bool] ]
    [ DependsOn = [string[]] ]
    [ Value = [string] ]
}
```

## <a name="properties"></a><span data-ttu-id="c5455-107">Tulajdonságok</span><span class="sxs-lookup"><span data-stu-id="c5455-107">Properties</span></span>

|  <span data-ttu-id="c5455-108">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="c5455-108">Property</span></span>  |  <span data-ttu-id="c5455-109">Leírás</span><span class="sxs-lookup"><span data-stu-id="c5455-109">Description</span></span>   | 
|---|---| 
| <span data-ttu-id="c5455-110">Név</span><span class="sxs-lookup"><span data-stu-id="c5455-110">Name</span></span>| <span data-ttu-id="c5455-111">A környezeti változó, amelyekhez egy adott állapot biztosításához nevét jelöli.</span><span class="sxs-lookup"><span data-stu-id="c5455-111">Indicates the name of the environment variable for which you want to ensure a specific state.</span></span>| 
| <span data-ttu-id="c5455-112">Győződjön meg arról</span><span class="sxs-lookup"><span data-stu-id="c5455-112">Ensure</span></span>| <span data-ttu-id="c5455-113">Azt jelzi, hogy létezik-e egy változót.</span><span class="sxs-lookup"><span data-stu-id="c5455-113">Indicates if a variable exists.</span></span> <span data-ttu-id="c5455-114">Ez a tulajdonság beállítása __jelen__ a környezeti változó létrehozása, ha nem létezik, vagy győződjön meg arról, hogy annak értéke megegyezik-e a keresztül elérhető a __érték__ tulajdonságot, ha a változó már létezik.</span><span class="sxs-lookup"><span data-stu-id="c5455-114">Set this property to __Present__ to create the environment variable if it does not exist or to ensure that its value matches what is provided through the __Value__ property if the variable already exists.</span></span> <span data-ttu-id="c5455-115">Állítsa az értékét __távol__ törli a változót, ha van ilyen.</span><span class="sxs-lookup"><span data-stu-id="c5455-115">Set it to __Absent__ to delete the variable if it exists.</span></span>| 
| <span data-ttu-id="c5455-116">Elérési út</span><span class="sxs-lookup"><span data-stu-id="c5455-116">Path</span></span>| <span data-ttu-id="c5455-117">Határozza meg a konfigurálni kívánt környezeti változó.</span><span class="sxs-lookup"><span data-stu-id="c5455-117">Defines the environment variable that is being configured.</span></span> <span data-ttu-id="c5455-118">Ez a tulajdonság beállítása __$true__ Ha a változó a __elérési__ változó; ellenkező esetben állítsa __$false__.</span><span class="sxs-lookup"><span data-stu-id="c5455-118">Set this property to __$true__ if the variable is the __Path__ variable; otherwise, set it to __$false__.</span></span> <span data-ttu-id="c5455-119">Az alapértelmezett érték __$false__.</span><span class="sxs-lookup"><span data-stu-id="c5455-119">The default is __$false__.</span></span> <span data-ttu-id="c5455-120">Ha a konfigurálni kívánt változó a __elérési__ változó, a megadott érték keresztül a __érték__ tulajdonság hozzáfűzi a meglévő értéket.</span><span class="sxs-lookup"><span data-stu-id="c5455-120">If the variable being configured is the __Path__ variable, the value provided through the __Value__ property will be appended to the existing value.</span></span>| 
| <span data-ttu-id="c5455-121">dependsOn</span><span class="sxs-lookup"><span data-stu-id="c5455-121">DependsOn</span></span> | <span data-ttu-id="c5455-122">Azt jelzi, hogy egy másik erőforrás konfigurációjának kell futtatni, mielőtt ehhez az erőforráshoz van konfigurálva.</span><span class="sxs-lookup"><span data-stu-id="c5455-122">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="c5455-123">Például, ha az erőforrás-konfiguráció azonosítója blokk futtatni kívánt parancsfájl első az __ResourceName__ és annak típusa __ResourceType__, az e tulajdonság használatával szintaxisa a következő `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="c5455-123">For example, if the ID of the resource configuration script block that you want to run first is __ResourceName__ and its type is __ResourceType__, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>| 
| <span data-ttu-id="c5455-124">Érték</span><span class="sxs-lookup"><span data-stu-id="c5455-124">Value</span></span>| <span data-ttu-id="c5455-125">A környezeti változóhoz rendelhető érték.</span><span class="sxs-lookup"><span data-stu-id="c5455-125">The value to assign to the environment variable.</span></span>| 

## <a name="example"></a><span data-ttu-id="c5455-126">Példa</span><span class="sxs-lookup"><span data-stu-id="c5455-126">Example</span></span>

<span data-ttu-id="c5455-127">Az alábbi példa biztosítja, hogy __TestEnvironmentVariable__ található és értéke __TestValue__.</span><span class="sxs-lookup"><span data-stu-id="c5455-127">The following example ensures that __TestEnvironmentVariable__ is present and it has the value __TestValue__.</span></span> <span data-ttu-id="c5455-128">Ha nincs jelen, létrehozza azt.</span><span class="sxs-lookup"><span data-stu-id="c5455-128">If it is not present, it creates it.</span></span>

```powershell
Environment EnvironmentExample
{
    Ensure = "Present"  # You can also set Ensure to "Absent"
    Name = "TestEnvironmentVariable"
    Value = "TestValue"
}
```

