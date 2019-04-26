---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: DSC, a Linux nxEnvironment erőforrás
ms.openlocfilehash: 763ec560faa6adaf42aef3c21c9045be95f780bc
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62078010"
---
# <a name="dsc-for-linux-nxenvironment-resource"></a><span data-ttu-id="4fb51-103">DSC, a Linux nxEnvironment erőforrás</span><span class="sxs-lookup"><span data-stu-id="4fb51-103">DSC for Linux nxEnvironment Resource</span></span>

<span data-ttu-id="4fb51-104">A **nxEnvironment** erőforrás a PowerShell Desired State Configuration (DSC) kezelése a Linux csomópont rendszerszintű környezeti változókat mechanizmust biztosít.</span><span class="sxs-lookup"><span data-stu-id="4fb51-104">The **nxEnvironment** resource in PowerShell Desired State Configuration (DSC) provides a mechanism to manage system environment variables on a Linux node.</span></span>

## <a name="syntax"></a><span data-ttu-id="4fb51-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="4fb51-105">Syntax</span></span>

```
nxEnvironment <string> #ResourceName
{
    Name = <string>
    [ Value = <string>
    [ Ensure = <string> { Absent | Present }  ]
    [ Path = <bool> }
    [ DependsOn = <string[]> ]

}
```

## <a name="properties"></a><span data-ttu-id="4fb51-106">Tulajdonságok</span><span class="sxs-lookup"><span data-stu-id="4fb51-106">Properties</span></span>

|  <span data-ttu-id="4fb51-107">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="4fb51-107">Property</span></span> |  <span data-ttu-id="4fb51-108">Leírás</span><span class="sxs-lookup"><span data-stu-id="4fb51-108">Description</span></span> |
|---|---|
| <span data-ttu-id="4fb51-109">Név</span><span class="sxs-lookup"><span data-stu-id="4fb51-109">Name</span></span>| <span data-ttu-id="4fb51-110">Azt jelzi, hogy a neve, amelyhez szeretne biztosítani adott állapotú környezeti változó.</span><span class="sxs-lookup"><span data-stu-id="4fb51-110">Indicates the name of the environment variable for which you want to ensure a specific state.</span></span>|
| <span data-ttu-id="4fb51-111">Érték</span><span class="sxs-lookup"><span data-stu-id="4fb51-111">Value</span></span>| <span data-ttu-id="4fb51-112">Rendelhet hozzá a környezeti változó értéke.</span><span class="sxs-lookup"><span data-stu-id="4fb51-112">The value to assign to the environment variable.</span></span>|
| <span data-ttu-id="4fb51-113">Győződjön meg, hogy</span><span class="sxs-lookup"><span data-stu-id="4fb51-113">Ensure</span></span>| <span data-ttu-id="4fb51-114">Ellenőrizze, hogy létezik-e a változó határozza meg.</span><span class="sxs-lookup"><span data-stu-id="4fb51-114">Determines whether to check if the variable exists.</span></span> <span data-ttu-id="4fb51-115">Ez annak érdekében, hogy létezik a változó "e" tulajdonság értéke.</span><span class="sxs-lookup"><span data-stu-id="4fb51-115">Set this property to "Present" to ensure the variable exists.</span></span> <span data-ttu-id="4fb51-116">Állítsa a "Hiányzó" annak biztosítására, a változó nem létezik.</span><span class="sxs-lookup"><span data-stu-id="4fb51-116">Set it to "Absent" to ensure the variable does not exist.</span></span> <span data-ttu-id="4fb51-117">Az alapértelmezett érték: "E".</span><span class="sxs-lookup"><span data-stu-id="4fb51-117">The default value is "Present".</span></span>|
| <span data-ttu-id="4fb51-118">Elérési út</span><span class="sxs-lookup"><span data-stu-id="4fb51-118">Path</span></span>| <span data-ttu-id="4fb51-119">A konfigurálni kívánt környezeti változó határozza meg.</span><span class="sxs-lookup"><span data-stu-id="4fb51-119">Defines the environment variable that is being configured.</span></span> <span data-ttu-id="4fb51-120">Ez a tulajdonság beállítása **$true** Ha a változó a **elérési** változó; ellenkező esetben beállíthatja azt a **$false**.</span><span class="sxs-lookup"><span data-stu-id="4fb51-120">Set this property to **$true** if the variable is the **Path** variable; otherwise, set it to **$false**.</span></span> <span data-ttu-id="4fb51-121">Az alapértelmezett érték **$false**.</span><span class="sxs-lookup"><span data-stu-id="4fb51-121">The default is **$false**.</span></span> <span data-ttu-id="4fb51-122">Ha a változó konfigurált a **elérési** változóhoz, a megadott érték keresztül a **érték** tulajdonság hozzá lesznek fűzve a meglévő értéket.</span><span class="sxs-lookup"><span data-stu-id="4fb51-122">If the variable being configured is the **Path** variable, the value provided through the **Value** property will be appended to the existing value.</span></span>|
| <span data-ttu-id="4fb51-123">DependsOn</span><span class="sxs-lookup"><span data-stu-id="4fb51-123">DependsOn</span></span> | <span data-ttu-id="4fb51-124">Azt jelzi, hogy a konfigurációt egy másik erőforrás futtatnia kell, mielőtt az erőforrás konfigurálva van.</span><span class="sxs-lookup"><span data-stu-id="4fb51-124">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="4fb51-125">Például ha a **azonosító** az erőforrás, amely a futtatni kívánt konfigurációs parancsprogram-blokkot első az **ResourceName** és a típusa **ResourceType**, ezzel esetén a tulajdonság `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="4fb51-125">For example, if the **ID** of the resource configuration script block that you want to run first is **ResourceName** and its type is **ResourceType**, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|

## <a name="additional-information"></a><span data-ttu-id="4fb51-126">További információ</span><span class="sxs-lookup"><span data-stu-id="4fb51-126">Additional Information</span></span>

* <span data-ttu-id="4fb51-127">Ha **elérési** hiányzik, vagy állítsa **$false**, felügyelete, a környezeti változók `/etc/environment`.</span><span class="sxs-lookup"><span data-stu-id="4fb51-127">If **Path** is absent or set to **$false**, environment variables are managed in `/etc/environment`.</span></span> <span data-ttu-id="4fb51-128">A programok vagy parancsfájlok forrás konfigurációt igényelhetnek a `/etc/environment` fájl eléréséhez a felügyelt környezeti változókat.</span><span class="sxs-lookup"><span data-stu-id="4fb51-128">Your programs or scripts may require configuration to source the `/etc/environment` file to access the managed environment variables.</span></span>
* <span data-ttu-id="4fb51-129">Ha **elérési** értékre van állítva **$true**, a környezeti változó kezelik a fájl `/etc/profile.d/DSCenvironment.sh`.</span><span class="sxs-lookup"><span data-stu-id="4fb51-129">If **Path** is set to **$true**, the environment variable is managed in the file `/etc/profile.d/DSCenvironment.sh`.</span></span> <span data-ttu-id="4fb51-130">Ez a fájl létrejön, ha még nem létezik.</span><span class="sxs-lookup"><span data-stu-id="4fb51-130">This file will be created if it does not exist.</span></span> <span data-ttu-id="4fb51-131">Ha **ellenőrizze, hogy** van beállítva a "Hiányzik" és **elérési** értékre van állítva **$true**, környezeti változó csak törlődni fog `/etc/profile.d/DSCenvironment.sh` és más fájlokból nem.</span><span class="sxs-lookup"><span data-stu-id="4fb51-131">If **Ensure** is set to "Absent" and **Path** is set to **$true**, an existing environment variable will only be removed from `/etc/profile.d/DSCenvironment.sh` and not from other files.</span></span>

## <a name="example"></a><span data-ttu-id="4fb51-132">Példa</span><span class="sxs-lookup"><span data-stu-id="4fb51-132">Example</span></span>

<span data-ttu-id="4fb51-133">Az alábbi példa bemutatja, hogyan használható a **nxEnvironment** annak érdekében, hogy erőforrás **TestEnvironmentVariable** létezik, és a "Test-Value" értékkel rendelkezik.</span><span class="sxs-lookup"><span data-stu-id="4fb51-133">The following example shows how to use the **nxEnvironment** resource to ensure that **TestEnvironmentVariable** is present and has the value "Test-Value".</span></span> <span data-ttu-id="4fb51-134">Ha **TestEnvironmentVariable** van nem található, a rendszer automatikusan létrehozza.</span><span class="sxs-lookup"><span data-stu-id="4fb51-134">If **TestEnvironmentVariable** is not present, it will be created.</span></span>

```
Import-DSCResource -Module nx


nxEnvironment EnvironmentExample
{
    Ensure = “Present”
    Name = “TestEnvironmentVariable”
    Value = “TestValue”
}
```