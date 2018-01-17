---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "A Linux nxEnvironment erőforrás DSC"
ms.openlocfilehash: 61e0c7e77e486cea878351f1929d73f1f80710d8
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 01/17/2018
---
# <a name="dsc-for-linux-nxenvironment-resource"></a><span data-ttu-id="d832a-103">A Linux nxEnvironment erőforrás DSC</span><span class="sxs-lookup"><span data-stu-id="d832a-103">DSC for Linux nxEnvironment Resource</span></span>

<span data-ttu-id="d832a-104">A **nxEnvironment** erőforrás a PowerShell kívánt állapot konfigurációs szolgáltatása (DSC) gombra a rendszerszintű környezeti változókat a Linux csomópont kezelése mechanizmust biztosít.</span><span class="sxs-lookup"><span data-stu-id="d832a-104">The **nxEnvironment** resource in PowerShell Desired State Configuration (DSC) provides a mechanism to to manage system environment variables on a Linux node.</span></span>

## <a name="syntax"></a><span data-ttu-id="d832a-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="d832a-105">Syntax</span></span>

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

## <a name="properties"></a><span data-ttu-id="d832a-106">Tulajdonságok</span><span class="sxs-lookup"><span data-stu-id="d832a-106">Properties</span></span>

|  <span data-ttu-id="d832a-107">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="d832a-107">Property</span></span> |  <span data-ttu-id="d832a-108">Leírás</span><span class="sxs-lookup"><span data-stu-id="d832a-108">Description</span></span> | 
|---|---|
| <span data-ttu-id="d832a-109">Név</span><span class="sxs-lookup"><span data-stu-id="d832a-109">Name</span></span>| <span data-ttu-id="d832a-110">A környezeti változó, amelyekhez egy adott állapot biztosításához nevét jelöli.</span><span class="sxs-lookup"><span data-stu-id="d832a-110">Indicates the name of the environment variable for which you want to ensure a specific state.</span></span>| 
| <span data-ttu-id="d832a-111">Érték</span><span class="sxs-lookup"><span data-stu-id="d832a-111">Value</span></span>| <span data-ttu-id="d832a-112">A környezeti változóhoz rendelhető érték.</span><span class="sxs-lookup"><span data-stu-id="d832a-112">The value to assign to the environment variable.</span></span>| 
| <span data-ttu-id="d832a-113">Győződjön meg arról</span><span class="sxs-lookup"><span data-stu-id="d832a-113">Ensure</span></span>| <span data-ttu-id="d832a-114">Ellenőrizze, hogy létezik-e a változó határozza meg.</span><span class="sxs-lookup"><span data-stu-id="d832a-114">Determines whether to check if the variable exists.</span></span> <span data-ttu-id="d832a-115">A tulajdonság "Elérhető" annak érdekében, hogy létezik-e a változó értéke.</span><span class="sxs-lookup"><span data-stu-id="d832a-115">Set this property to "Present" to ensure the variable exists.</span></span> <span data-ttu-id="d832a-116">Állítsa az értékét "Hiányzik", annak érdekében, a változó nem létezik.</span><span class="sxs-lookup"><span data-stu-id="d832a-116">Set it to "Absent" to ensure the variable does not exist.</span></span> <span data-ttu-id="d832a-117">Az alapértelmezett érték: "Elérhető".</span><span class="sxs-lookup"><span data-stu-id="d832a-117">The default value is "Present".</span></span>| 
| <span data-ttu-id="d832a-118">Elérési út</span><span class="sxs-lookup"><span data-stu-id="d832a-118">Path</span></span>| <span data-ttu-id="d832a-119">Határozza meg a konfigurálni kívánt környezeti változó.</span><span class="sxs-lookup"><span data-stu-id="d832a-119">Defines the environment variable that is being configured.</span></span> <span data-ttu-id="d832a-120">Ez a tulajdonság beállítása **$true** Ha a változó a **elérési** változó; ellenkező esetben állítsa **$false**.</span><span class="sxs-lookup"><span data-stu-id="d832a-120">Set this property to **$true** if the variable is the **Path** variable; otherwise, set it to **$false**.</span></span> <span data-ttu-id="d832a-121">Az alapértelmezett érték **$false**.</span><span class="sxs-lookup"><span data-stu-id="d832a-121">The default is **$false**.</span></span> <span data-ttu-id="d832a-122">Ha a konfigurálni kívánt változó a **elérési** változó, a megadott érték keresztül a **érték** tulajdonság hozzáfűzi a meglévő értéket.</span><span class="sxs-lookup"><span data-stu-id="d832a-122">If the variable being configured is the **Path** variable, the value provided through the **Value** property will be appended to the existing value.</span></span>| 
| <span data-ttu-id="d832a-123">dependsOn</span><span class="sxs-lookup"><span data-stu-id="d832a-123">DependsOn</span></span> | <span data-ttu-id="d832a-124">Azt jelzi, hogy egy másik erőforrás konfigurációjának kell futtatni, mielőtt ehhez az erőforráshoz van konfigurálva.</span><span class="sxs-lookup"><span data-stu-id="d832a-124">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="d832a-125">Például ha a **azonosító** az erőforrás konfigurációs futtatni kívánt először parancsprogramblokkja **ResourceName** és annak típusa **ResourceType**, ez a szintaxis a tulajdonság `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="d832a-125">For example, if the **ID** of the resource configuration script block that you want to run first is **ResourceName** and its type is **ResourceType**, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>| 

## <a name="additional-information"></a><span data-ttu-id="d832a-126">További információ</span><span class="sxs-lookup"><span data-stu-id="d832a-126">Additional Information</span></span>

* <span data-ttu-id="d832a-127">Ha **elérési** hiányzik, vagy állítsa be **$false**, a környezeti változók felügyelete `/etc/environment`.</span><span class="sxs-lookup"><span data-stu-id="d832a-127">If **Path** is absent or set to **$false**, environment variables are managed in `/etc/environment`.</span></span> <span data-ttu-id="d832a-128">A programok vagy parancsfájlok forrás konfigurálásra lehet szükség a `/etc/environment` fájl a felügyelt környezeti változók elérésére.</span><span class="sxs-lookup"><span data-stu-id="d832a-128">Your programs or scripts may require configuration to source the `/etc/environment` file to access the managed environment variables.</span></span>
* <span data-ttu-id="d832a-129">Ha **elérési** értéke **$true**, a fájlban a következő környezeti változó felügyelt `/etc/profile.d/DSCenvironment.sh`.</span><span class="sxs-lookup"><span data-stu-id="d832a-129">If **Path** is set to **$true**, the environment variable is managed in the file `/etc/profile.d/DSCenvironment.sh`.</span></span> <span data-ttu-id="d832a-130">Ha még nem létezik. létrehozza ezt a fájlt.</span><span class="sxs-lookup"><span data-stu-id="d832a-130">This file will be created if it does not exist.</span></span> <span data-ttu-id="d832a-131">Ha **ellenőrizze, hogy** van beállítva a "Hiányzik" és **elérési** értékre van állítva **$true**, környezeti változó csak törlődnek a `/etc/profile.d/DSCenvironment.sh` és más fájlok nem a.</span><span class="sxs-lookup"><span data-stu-id="d832a-131">If **Ensure** is set to "Absent" and **Path** is set to **$true**, an existing environment variable will only be removed from `/etc/profile.d/DSCenvironment.sh` and not from other files.</span></span>

## <a name="example"></a><span data-ttu-id="d832a-132">Példa</span><span class="sxs-lookup"><span data-stu-id="d832a-132">Example</span></span>

<span data-ttu-id="d832a-133">A következő példa bemutatja, hogyan használható a **nxEnvironment** annak érdekében, hogy erőforrás **TestEnvironmentVariable** jelen, és a "Test-érték" értékkel rendelkezik.</span><span class="sxs-lookup"><span data-stu-id="d832a-133">The following example shows how to use the **nxEnvironment** resource to ensure that **TestEnvironmentVariable** is present and has the value "Test-Value".</span></span> <span data-ttu-id="d832a-134">Ha **TestEnvironmentVariable** van nincs jelen, a rendszer automatikusan létrehozza.</span><span class="sxs-lookup"><span data-stu-id="d832a-134">If **TestEnvironmentVariable** is not present, it will be created.</span></span>

```
Import-DSCResource -Module nx 


nxEnvironment EnvironmentExample
{
    Ensure = “Present”
    Name = “TestEnvironmentVariable”
    Value = “TestValue”
}
```


