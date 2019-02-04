---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: DSC-környezeti erőforrás
ms.openlocfilehash: 2bc1600a9df32538d59efa712569b12fa9e3beee
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55685983"
---
# <a name="dsc-environment-resource"></a><span data-ttu-id="8fbf6-103">DSC-környezeti erőforrás</span><span class="sxs-lookup"><span data-stu-id="8fbf6-103">DSC Environment Resource</span></span>

> <span data-ttu-id="8fbf6-104">Érvényes: Windows PowerShell 4.0-s, a Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="8fbf6-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="8fbf6-105">A __környezet__ erőforrás a Windows PowerShell Desired State Configuration (DSC) kezeléséhez rendszerszintű környezeti változókat mechanizmust biztosít.</span><span class="sxs-lookup"><span data-stu-id="8fbf6-105">The __Environment__ resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to manage system environment variables.</span></span>

## <a name="syntax"></a><span data-ttu-id="8fbf6-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="8fbf6-106">Syntax</span></span>
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

## <a name="properties"></a><span data-ttu-id="8fbf6-107">Tulajdonságok</span><span class="sxs-lookup"><span data-stu-id="8fbf6-107">Properties</span></span>

|  <span data-ttu-id="8fbf6-108">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="8fbf6-108">Property</span></span>  |  <span data-ttu-id="8fbf6-109">Leírás</span><span class="sxs-lookup"><span data-stu-id="8fbf6-109">Description</span></span>   |
|---|---|
| <span data-ttu-id="8fbf6-110">Név</span><span class="sxs-lookup"><span data-stu-id="8fbf6-110">Name</span></span>| <span data-ttu-id="8fbf6-111">Azt jelzi, hogy a neve, amelyhez szeretne biztosítani adott állapotú környezeti változó.</span><span class="sxs-lookup"><span data-stu-id="8fbf6-111">Indicates the name of the environment variable for which you want to ensure a specific state.</span></span>|
| <span data-ttu-id="8fbf6-112">Győződjön meg, hogy</span><span class="sxs-lookup"><span data-stu-id="8fbf6-112">Ensure</span></span>| <span data-ttu-id="8fbf6-113">Azt jelzi, hogy létezik-e egy változóban.</span><span class="sxs-lookup"><span data-stu-id="8fbf6-113">Indicates if a variable exists.</span></span> <span data-ttu-id="8fbf6-114">Ez a tulajdonság beállítása __jelen__ a környezeti változó létrehozásához, ha még nem létezik, vagy győződjön meg arról, hogy az érték megegyezik-e a keresztül biztosított a __érték__ tulajdonságot, ha a változó már létezik.</span><span class="sxs-lookup"><span data-stu-id="8fbf6-114">Set this property to __Present__ to create the environment variable if it does not exist or to ensure that its value matches what is provided through the __Value__ property if the variable already exists.</span></span> <span data-ttu-id="8fbf6-115">Állítsa be __távol__ , ha létezik, törölje a változót.</span><span class="sxs-lookup"><span data-stu-id="8fbf6-115">Set it to __Absent__ to delete the variable if it exists.</span></span>|
| <span data-ttu-id="8fbf6-116">Elérési út</span><span class="sxs-lookup"><span data-stu-id="8fbf6-116">Path</span></span>| <span data-ttu-id="8fbf6-117">A konfigurálni kívánt környezeti változó határozza meg.</span><span class="sxs-lookup"><span data-stu-id="8fbf6-117">Defines the environment variable that is being configured.</span></span> <span data-ttu-id="8fbf6-118">Ez a tulajdonság beállítása __$true__ Ha a változó a __elérési__ változó; ellenkező esetben beállíthatja azt a __$false__.</span><span class="sxs-lookup"><span data-stu-id="8fbf6-118">Set this property to __$true__ if the variable is the __Path__ variable; otherwise, set it to __$false__.</span></span> <span data-ttu-id="8fbf6-119">Az alapértelmezett érték __$false__.</span><span class="sxs-lookup"><span data-stu-id="8fbf6-119">The default is __$false__.</span></span> <span data-ttu-id="8fbf6-120">Ha a változó konfigurált a __elérési__ változóhoz, a megadott érték keresztül a __érték__ tulajdonság hozzá lesznek fűzve a meglévő értéket.</span><span class="sxs-lookup"><span data-stu-id="8fbf6-120">If the variable being configured is the __Path__ variable, the value provided through the __Value__ property will be appended to the existing value.</span></span>|
| <span data-ttu-id="8fbf6-121">DependsOn</span><span class="sxs-lookup"><span data-stu-id="8fbf6-121">DependsOn</span></span> | <span data-ttu-id="8fbf6-122">Azt jelzi, hogy a konfigurációt egy másik erőforrás futtatnia kell, mielőtt az erőforrás konfigurálva van.</span><span class="sxs-lookup"><span data-stu-id="8fbf6-122">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="8fbf6-123">Például, ha az erőforrás-konfiguráció azonosítója letiltása, a futtatni kívánt parancsfájl először van __ResourceName__ és a típusa __ResourceType__, ez a tulajdonság használata esetén `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="8fbf6-123">For example, if the ID of the resource configuration script block that you want to run first is __ResourceName__ and its type is __ResourceType__, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|
| <span data-ttu-id="8fbf6-124">Érték</span><span class="sxs-lookup"><span data-stu-id="8fbf6-124">Value</span></span>| <span data-ttu-id="8fbf6-125">Rendelhet hozzá a környezeti változó értéke.</span><span class="sxs-lookup"><span data-stu-id="8fbf6-125">The value to assign to the environment variable.</span></span>|

## <a name="example"></a><span data-ttu-id="8fbf6-126">Példa</span><span class="sxs-lookup"><span data-stu-id="8fbf6-126">Example</span></span>

<span data-ttu-id="8fbf6-127">Az alábbi példa biztosítja, hogy __TestEnvironmentVariable__ található és értéke __TestValue__.</span><span class="sxs-lookup"><span data-stu-id="8fbf6-127">The following example ensures that __TestEnvironmentVariable__ is present and it has the value __TestValue__.</span></span> <span data-ttu-id="8fbf6-128">Ha nem található, létrehozza azt.</span><span class="sxs-lookup"><span data-stu-id="8fbf6-128">If it is not present, it creates it.</span></span>

```powershell
Environment EnvironmentExample
{
    Ensure = "Present"  # You can also set Ensure to "Absent"
    Name = "TestEnvironmentVariable"
    Value = "TestValue"
}
```