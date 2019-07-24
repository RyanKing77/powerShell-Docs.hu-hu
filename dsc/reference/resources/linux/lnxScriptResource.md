---
ms.date: 06/12/2017
keywords: DSC, PowerShell, konfigurálás, beállítás
title: DSC Linux nxScript-erőforráshoz
ms.openlocfilehash: 0ad0530f1de7b86ff48c4eb1f79870f6682894a1
ms.sourcegitcommit: 118eb294d5a84a772e6449d42a9d9324e18ef6b9
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/22/2019
ms.locfileid: "68372166"
---
# <a name="dsc-for-linux-nxscript-resource"></a><span data-ttu-id="7e80d-103">DSC Linux nxScript-erőforráshoz</span><span class="sxs-lookup"><span data-stu-id="7e80d-103">DSC for Linux nxScript Resource</span></span>

<span data-ttu-id="7e80d-104">A **nxScript** -erőforrás a PowerShell desired State CONFIGURATION (DSC) szolgáltatásban a Linux-parancsfájlok Linux-csomóponton való futtatására szolgáló mechanizmust biztosít.</span><span class="sxs-lookup"><span data-stu-id="7e80d-104">The **nxScript** resource in PowerShell Desired State Configuration (DSC) provides a mechanism to run Linux scripts on a Linux node.</span></span>

## <a name="syntax"></a><span data-ttu-id="7e80d-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="7e80d-105">Syntax</span></span>

```
nxScript <string> #ResourceName
{
    GetScript = <string>
    SetScript = <string>
    TestScript = <string>
    [ User = <string> ]
    [ Group = <string> ]
    [ DependsOn = <string[]> ]

}
```

## <a name="properties"></a><span data-ttu-id="7e80d-106">Tulajdonságok</span><span class="sxs-lookup"><span data-stu-id="7e80d-106">Properties</span></span>

|  <span data-ttu-id="7e80d-107">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="7e80d-107">Property</span></span> |  <span data-ttu-id="7e80d-108">Leírás</span><span class="sxs-lookup"><span data-stu-id="7e80d-108">Description</span></span> |
|---|---|
| <span data-ttu-id="7e80d-109">GetScript</span><span class="sxs-lookup"><span data-stu-id="7e80d-109">GetScript</span></span>| <span data-ttu-id="7e80d-110">Parancsfájlt biztosít a gép aktuális állapotának visszaküldéséhez.</span><span class="sxs-lookup"><span data-stu-id="7e80d-110">Provides a script to return current status of the machine.</span></span>  <span data-ttu-id="7e80d-111">Ez a szkript a [GetDscConfiguration.py](https://github.com/Microsoft/PowerShell-DSC-for-Linux#performing-dsc-operations-from-the-linux-computer) parancsfájl meghívásakor fut.</span><span class="sxs-lookup"><span data-stu-id="7e80d-111">This script runs when you invoke the [GetDscConfiguration.py](https://github.com/Microsoft/PowerShell-DSC-for-Linux#performing-dsc-operations-from-the-linux-computer) script.</span></span> <span data-ttu-id="7e80d-112">A szkriptnek egy shebangje kell kezdődnie, például #!/bin/bash.</span><span class="sxs-lookup"><span data-stu-id="7e80d-112">The script must begin with a shebang, such as #!/bin/bash.</span></span>|
| <span data-ttu-id="7e80d-113">SetScript</span><span class="sxs-lookup"><span data-stu-id="7e80d-113">SetScript</span></span>| <span data-ttu-id="7e80d-114">Egy olyan parancsfájlt biztosít, amely megfelelő állapotba helyezi a gépet.</span><span class="sxs-lookup"><span data-stu-id="7e80d-114">Provides a script that puts the machine in the correct state.</span></span> <span data-ttu-id="7e80d-115">A [StartDscConfiguration.py](https://github.com/Microsoft/PowerShell-DSC-for-Linux#performing-dsc-operations-from-the-linux-computer) parancsfájl meghívásakor a **TestScript** először fut.</span><span class="sxs-lookup"><span data-stu-id="7e80d-115">When you invoke the [StartDscConfiguration.py](https://github.com/Microsoft/PowerShell-DSC-for-Linux#performing-dsc-operations-from-the-linux-computer) script, the **TestScript** runs first.</span></span> <span data-ttu-id="7e80d-116">Ha a **TestScript** blokk a 0-tól eltérő kilépési kódot ad vissza, akkor a **SetScript** -blokk fut.</span><span class="sxs-lookup"><span data-stu-id="7e80d-116">If the **TestScript** block returns an exit code other than 0, the **SetScript** block will run.</span></span> <span data-ttu-id="7e80d-117">Ha a **TestScript** 0 kilépési kódot ad vissza, a **SetScript** nem fog futni.</span><span class="sxs-lookup"><span data-stu-id="7e80d-117">If the **TestScript** returns an exit code of 0, the **SetScript** will not run.</span></span> <span data-ttu-id="7e80d-118">A szkriptnek egy shebangje kell kezdődnie, például `#!/bin/bash`:.</span><span class="sxs-lookup"><span data-stu-id="7e80d-118">The script must begin with a shebang, such as `#!/bin/bash`.</span></span>|
| <span data-ttu-id="7e80d-119">TestScript</span><span class="sxs-lookup"><span data-stu-id="7e80d-119">TestScript</span></span>| <span data-ttu-id="7e80d-120">Egy olyan parancsfájlt biztosít, amely kiértékeli, hogy a csomópont jelenleg megfelelő állapotban van-e.</span><span class="sxs-lookup"><span data-stu-id="7e80d-120">Provides a script that evaluates whether the node is currently in the correct state.</span></span> <span data-ttu-id="7e80d-121">A [StartDscConfiguration.py](https://github.com/Microsoft/PowerShell-DSC-for-Linux#performing-dsc-operations-from-the-linux-computer) parancsfájl meghívásakor ez a szkript fut.</span><span class="sxs-lookup"><span data-stu-id="7e80d-121">When you invoke the [StartDscConfiguration.py](https://github.com/Microsoft/PowerShell-DSC-for-Linux#performing-dsc-operations-from-the-linux-computer) script, this script runs.</span></span> <span data-ttu-id="7e80d-122">Ha nullától eltérő kilépési kódot ad vissza, a SetScript futni fog.</span><span class="sxs-lookup"><span data-stu-id="7e80d-122">If it returns an exit code other than 0, the SetScript will run.</span></span> <span data-ttu-id="7e80d-123">Ha 0 kilépési kódot ad vissza, a **SetScript** nem fog futni.</span><span class="sxs-lookup"><span data-stu-id="7e80d-123">If it returns an exit code of 0, the **SetScript** will not run.</span></span> <span data-ttu-id="7e80d-124">A **TestScript** a [TestDscConfiguration](https://github.com/Microsoft/PowerShell-DSC-for-Linux#performing-dsc-operations-from-the-linux-computer) parancsfájl meghívásakor is fut.</span><span class="sxs-lookup"><span data-stu-id="7e80d-124">The **TestScript** also runs when you invoke the [TestDscConfiguration](https://github.com/Microsoft/PowerShell-DSC-for-Linux#performing-dsc-operations-from-the-linux-computer) script.</span></span> <span data-ttu-id="7e80d-125">Ebben az esetben azonban a **SetScript** nem fog futni, függetlenül attól, hogy milyen kilépési kódot ad vissza a **TestScript**.</span><span class="sxs-lookup"><span data-stu-id="7e80d-125">However, in this case, the **SetScript** will not run, no matter what exit code is returned from the **TestScript**.</span></span> <span data-ttu-id="7e80d-126">A **TestScript** tartalmaznia kell a tartalmat, és 0 kilépési kódot kell visszaadnia, ha a tényleges konfiguráció megegyezik a jelenlegi kívánt állapot-konfigurációval, és a kilépési kód nullától eltérő, ha nem egyezik.</span><span class="sxs-lookup"><span data-stu-id="7e80d-126">The **TestScript** must contain content and must return an exit code of 0 if the actual configuration matches the current desired state configuration, and an exit code other than 0 if it does not match.</span></span> <span data-ttu-id="7e80d-127">(A jelenlegi kívánt állapot-konfiguráció a DSC-t használó csomópont utolsó konfigurációja.</span><span class="sxs-lookup"><span data-stu-id="7e80d-127">(The current desired state configuration is the last configuration enacted on the node that is using DSC).</span></span> <span data-ttu-id="7e80d-128">A szkriptnek egy shebangje kell kezdődnie, például 1 #!/bin/bash.1</span><span class="sxs-lookup"><span data-stu-id="7e80d-128">The script must begin with a shebang, such as 1#!/bin/bash.1</span></span>|
| <span data-ttu-id="7e80d-129">Felhasználó</span><span class="sxs-lookup"><span data-stu-id="7e80d-129">User</span></span>| <span data-ttu-id="7e80d-130">A felhasználó, aki a parancsfájlt futtatja.</span><span class="sxs-lookup"><span data-stu-id="7e80d-130">The user to run the script as.</span></span>|
| <span data-ttu-id="7e80d-131">Csoport</span><span class="sxs-lookup"><span data-stu-id="7e80d-131">Group</span></span>| <span data-ttu-id="7e80d-132">A parancsfájl futtatására szolgáló csoport.</span><span class="sxs-lookup"><span data-stu-id="7e80d-132">The group to run the script as.</span></span>|
| <span data-ttu-id="7e80d-133">DependsOn</span><span class="sxs-lookup"><span data-stu-id="7e80d-133">DependsOn</span></span> | <span data-ttu-id="7e80d-134">Azt jelzi, hogy egy másik erőforrás konfigurációjának futnia kell az erőforrás konfigurálása előtt.</span><span class="sxs-lookup"><span data-stu-id="7e80d-134">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="7e80d-135">Ha például az az erőforrás  -konfigurációs parancsfájl blokkja, amelyet először szeretne futtatni, **resourcename** , és a típusa **resourcetype**, a tulajdonság `DependsOn = "[ResourceType]ResourceName"`használatának szintaxisa a következő:.</span><span class="sxs-lookup"><span data-stu-id="7e80d-135">For example, if the **ID** of the resource configuration script block that you want to run first is **ResourceName** and its type is **ResourceType**, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|

## <a name="example"></a><span data-ttu-id="7e80d-136">Példa</span><span class="sxs-lookup"><span data-stu-id="7e80d-136">Example</span></span>

<span data-ttu-id="7e80d-137">Az alábbi példa bemutatja, hogyan használhatja a **nxScript** -erőforrást további konfigurálási műveletek végrehajtásához.</span><span class="sxs-lookup"><span data-stu-id="7e80d-137">The following example demonstrates the use of the **nxScript** resource to perform additional configuration management.</span></span>

```
Import-DSCResource -Module nx

Node $node {
nxScript KeepDirEmpty{

    GetScript = @"
#!/bin/bash
ls /tmp/mydir/ | wc -l
"@

    SetScript = @"
#!/bin/bash
rm -rf /tmp/mydir/*
"@

    TestScript = @'
#!/bin/bash
filecount=`ls /tmp/mydir | wc -l`
if [ $filecount -gt 0 ]
then
    exit 1
else
    exit 0
fi
'@
}
}
```
