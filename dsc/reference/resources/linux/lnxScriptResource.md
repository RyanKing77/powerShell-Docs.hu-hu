---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: DSC Linux nxScript erőforrás számára
ms.openlocfilehash: 339968512ab1c16c4c3785a3a19b00c3fbbf9ea1
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 01/04/2019
ms.locfileid: "54048259"
---
# <a name="dsc-for-linux-nxscript-resource"></a><span data-ttu-id="12bbc-103">DSC Linux nxScript erőforrás számára</span><span class="sxs-lookup"><span data-stu-id="12bbc-103">DSC for Linux nxScript Resource</span></span>

<span data-ttu-id="12bbc-104">A **nxScript** erőforrás a PowerShell Desired State Configuration (DSC) Linux parancsfájlok futtatása egy Linux-csomóponton mechanizmust biztosít.</span><span class="sxs-lookup"><span data-stu-id="12bbc-104">The **nxScript** resource in PowerShell Desired State Configuration (DSC) provides a mechanism to run Linux scripts on a Linux node.</span></span>

## <a name="syntax"></a><span data-ttu-id="12bbc-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="12bbc-105">Syntax</span></span>

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

## <a name="properties"></a><span data-ttu-id="12bbc-106">Tulajdonságok</span><span class="sxs-lookup"><span data-stu-id="12bbc-106">Properties</span></span>

|  <span data-ttu-id="12bbc-107">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="12bbc-107">Property</span></span> |  <span data-ttu-id="12bbc-108">Leírás</span><span class="sxs-lookup"><span data-stu-id="12bbc-108">Description</span></span> |
|---|---|
| <span data-ttu-id="12bbc-109">GetScript</span><span class="sxs-lookup"><span data-stu-id="12bbc-109">GetScript</span></span>| <span data-ttu-id="12bbc-110">Egy parancsfájl, amely akkor fut, amikor indít el a [Get-DscConfiguration](https://technet.microsoft.com/en-us/library/dn521625.aspx) parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="12bbc-110">Provides a script that runs when you invoke the [Get-DscConfiguration](https://technet.microsoft.com/en-us/library/dn521625.aspx) cmdlet.</span></span> <span data-ttu-id="12bbc-111">A szkript egy shebangje határoz meg, például # kell kezdődnie! / bin/bash.</span><span class="sxs-lookup"><span data-stu-id="12bbc-111">The script must begin with a shebang, such as #!/bin/bash.</span></span>|
| <span data-ttu-id="12bbc-112">SetScript</span><span class="sxs-lookup"><span data-stu-id="12bbc-112">SetScript</span></span>| <span data-ttu-id="12bbc-113">Egy parancsfájlt tartalmaz.</span><span class="sxs-lookup"><span data-stu-id="12bbc-113">Provides a script.</span></span> <span data-ttu-id="12bbc-114">Amikor meghívása a [Start-DscConfiguration](https://technet.microsoft.com/en-us/library/dn521623.aspx) parancsmagot, a **TestScript** első futtatja.</span><span class="sxs-lookup"><span data-stu-id="12bbc-114">When you invoke the [Start-DscConfiguration](https://technet.microsoft.com/en-us/library/dn521623.aspx) cmdlet, the **TestScript** runs first.</span></span> <span data-ttu-id="12bbc-115">Ha a **TestScript** blokk 0, eltérő kilépési kódot ad vissza a **SetScript** blokk fog futni.</span><span class="sxs-lookup"><span data-stu-id="12bbc-115">If the **TestScript** block returns an exit code other than 0, the **SetScript** block will run.</span></span> <span data-ttu-id="12bbc-116">Ha a **TestScript** , a 0 kilépési kódot ad vissza a **SetScript** nem fog futni.</span><span class="sxs-lookup"><span data-stu-id="12bbc-116">If the **TestScript** returns an exit code of 0, the **SetScript** will not run.</span></span> <span data-ttu-id="12bbc-117">A parancsfájl a következővel kell kezdődnie shebangje határoz meg, mint például `#!/bin/bash`.</span><span class="sxs-lookup"><span data-stu-id="12bbc-117">The script must begin with a shebang, such as `#!/bin/bash`.</span></span>|
| <span data-ttu-id="12bbc-118">TestScript</span><span class="sxs-lookup"><span data-stu-id="12bbc-118">TestScript</span></span>| <span data-ttu-id="12bbc-119">Egy parancsfájlt tartalmaz.</span><span class="sxs-lookup"><span data-stu-id="12bbc-119">Provides a script.</span></span> <span data-ttu-id="12bbc-120">Amikor meghívása a [Start-DscConfiguration](https://technet.microsoft.com/en-us/library/dn521623.aspx) parancsmag, ez a szkript futtatása.</span><span class="sxs-lookup"><span data-stu-id="12bbc-120">When you invoke the [Start-DscConfiguration](https://technet.microsoft.com/en-us/library/dn521623.aspx) cmdlet, this script runs.</span></span> <span data-ttu-id="12bbc-121">0-tól eltérő kilépési kódot ad vissza, ha a SetScript fog futni.</span><span class="sxs-lookup"><span data-stu-id="12bbc-121">If it returns an exit code other than 0, the SetScript will run.</span></span> <span data-ttu-id="12bbc-122">Ha a 0 kilépési kódot ad vissza a **SetScript** nem fog futni.</span><span class="sxs-lookup"><span data-stu-id="12bbc-122">If it returns an exit code of 0, the **SetScript** will not run.</span></span> <span data-ttu-id="12bbc-123">A **TestScript** is fut, amikor indít el a [a Test-DscConfiguration](https://technet.microsoft.com/en-us/library/dn407382.aspx) parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="12bbc-123">The **TestScript** also runs when you invoke the [Test-DscConfiguration](https://technet.microsoft.com/en-us/library/dn407382.aspx) cmdlet.</span></span> <span data-ttu-id="12bbc-124">Azonban ebben az esetben az a **SetScript** nem fog futni, függetlenül attól, hogy milyen kilépési kód érkezésekor a a **TestScript**.</span><span class="sxs-lookup"><span data-stu-id="12bbc-124">However, in this case, the **SetScript** will not run, no matter what exit code is returned from the **TestScript**.</span></span> <span data-ttu-id="12bbc-125">A **TestScript** kell a 0 kilépési kódot ad vissza, ha a tényleges konfigurációja megegyezik a jelenlegi állapotkonfigurációs, és a egy kilépési kód más, mint 0, ha nem felel meg.</span><span class="sxs-lookup"><span data-stu-id="12bbc-125">The **TestScript** must return an exit code of 0 if the actual configuration matches the current desired state configuration, and an exit code other than 0 if it does not match.</span></span> <span data-ttu-id="12bbc-126">(A jelenlegi kívánt állapot konfigurációs a csomópont által használt DSC gyakorlatokkal utolsó konfiguráció).</span><span class="sxs-lookup"><span data-stu-id="12bbc-126">(The current desired state configuration is the last configuration enacted on the node that is using DSC).</span></span> <span data-ttu-id="12bbc-127">A szkript egy shebangje határoz meg, például a 1#!/bin/bash.1 kell kezdődnie.</span><span class="sxs-lookup"><span data-stu-id="12bbc-127">The script must begin with a shebang, such as 1#!/bin/bash.1</span></span>|
| <span data-ttu-id="12bbc-128">Felhasználó</span><span class="sxs-lookup"><span data-stu-id="12bbc-128">User</span></span>| <span data-ttu-id="12bbc-129">A felhasználó, a parancsfájl futtatásához.</span><span class="sxs-lookup"><span data-stu-id="12bbc-129">The user to run the script as.</span></span>|
| <span data-ttu-id="12bbc-130">Csoport</span><span class="sxs-lookup"><span data-stu-id="12bbc-130">Group</span></span>| <span data-ttu-id="12bbc-131">A csoport, a parancsfájl futtatásához.</span><span class="sxs-lookup"><span data-stu-id="12bbc-131">The group to run the script as.</span></span>|
| <span data-ttu-id="12bbc-132">DependsOn</span><span class="sxs-lookup"><span data-stu-id="12bbc-132">DependsOn</span></span> | <span data-ttu-id="12bbc-133">Azt jelzi, hogy a konfigurációt egy másik erőforrás futtatnia kell, mielőtt az erőforrás konfigurálva van.</span><span class="sxs-lookup"><span data-stu-id="12bbc-133">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="12bbc-134">Például ha a **azonosító** az erőforrás, amely a futtatni kívánt konfigurációs parancsprogram-blokkot első az **ResourceName** és a típusa **ResourceType**, ezzel esetén a tulajdonság `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="12bbc-134">For example, if the **ID** of the resource configuration script block that you want to run first is **ResourceName** and its type is **ResourceType**, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|

## <a name="example"></a><span data-ttu-id="12bbc-135">Példa</span><span class="sxs-lookup"><span data-stu-id="12bbc-135">Example</span></span>

<span data-ttu-id="12bbc-136">Az alábbi példa bemutatja, hogy a **nxScript** erőforrás további konfigurációfelügyeleti végrehajtásához.</span><span class="sxs-lookup"><span data-stu-id="12bbc-136">The following example demonstrates the use of the **nxScript** resource to perform additional configuration management.</span></span>

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