---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "A Linux nxScript erőforrás DSC"
ms.openlocfilehash: c12fb3b405d84eedd13e4cbebf2b2bf0d7cfb4d3
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 01/17/2018
---
# <a name="dsc-for-linux-nxscript-resource"></a><span data-ttu-id="df941-103">A Linux nxScript erőforrás DSC</span><span class="sxs-lookup"><span data-stu-id="df941-103">DSC for Linux nxScript Resource</span></span>

<span data-ttu-id="df941-104">A **nxScript** erőforrás a PowerShell kívánt állapot konfigurációs szolgáltatása (DSC) lehetővé teszi a Linux-parancsfájlok futtatása egy Linux-csomóponton.</span><span class="sxs-lookup"><span data-stu-id="df941-104">The **nxScript** resource in PowerShell Desired State Configuration (DSC) provides a mechanism to run Linux scripts on a Linux node.</span></span>

## <a name="syntax"></a><span data-ttu-id="df941-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="df941-105">Syntax</span></span>

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

## <a name="properties"></a><span data-ttu-id="df941-106">Tulajdonságok</span><span class="sxs-lookup"><span data-stu-id="df941-106">Properties</span></span>

|  <span data-ttu-id="df941-107">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="df941-107">Property</span></span> |  <span data-ttu-id="df941-108">Leírás</span><span class="sxs-lookup"><span data-stu-id="df941-108">Description</span></span> | 
|---|---|
| <span data-ttu-id="df941-109">GetScript</span><span class="sxs-lookup"><span data-stu-id="df941-109">GetScript</span></span>| <span data-ttu-id="df941-110">Egy parancsfájl, amely indításakor fut a [Get-DscConfiguration](https://technet.microsoft.com/en-us/library/dn521625.aspx) parancsmag.</span><span class="sxs-lookup"><span data-stu-id="df941-110">Provides a script that runs when you invoke the [Get-DscConfiguration](https://technet.microsoft.com/en-us/library/dn521625.aspx) cmdlet.</span></span> <span data-ttu-id="df941-111">A parancsfájl egy shebang, például # kell kezdődnie! / bin/bash.</span><span class="sxs-lookup"><span data-stu-id="df941-111">The script must begin with a shebang, such as #!/bin/bash.</span></span>| 
| <span data-ttu-id="df941-112">SetScript</span><span class="sxs-lookup"><span data-stu-id="df941-112">SetScript</span></span>| <span data-ttu-id="df941-113">Egy parancsfájlt tartalmaz.</span><span class="sxs-lookup"><span data-stu-id="df941-113">Provides a script.</span></span> <span data-ttu-id="df941-114">Ha meghívása a [Start-DscConfiguration](https://technet.microsoft.com/en-us/library/dn521623.aspx) parancsmag, a **TestScript** első futtatja.</span><span class="sxs-lookup"><span data-stu-id="df941-114">When you invoke the [Start-DscConfiguration](https://technet.microsoft.com/en-us/library/dn521623.aspx) cmdlet, the **TestScript** runs first.</span></span> <span data-ttu-id="df941-115">Ha a **TestScript** blokk eltérő 0, kilépési kódot ad vissza a **SetScript** blokk fog futni.</span><span class="sxs-lookup"><span data-stu-id="df941-115">If the **TestScript** block returns an exit code other than 0, the **SetScript** block will run.</span></span> <span data-ttu-id="df941-116">Ha a **TestScript** , a 0 kilépési kódot ad vissza a **SetScript** nem fog futni.</span><span class="sxs-lookup"><span data-stu-id="df941-116">If the **TestScript** returns an exit code of 0, the **SetScript** will not run.</span></span> <span data-ttu-id="df941-117">A parancsfájl például a egy shebang kell kezdődnie `#!/bin/bash`.</span><span class="sxs-lookup"><span data-stu-id="df941-117">The script must begin with a shebang, such as `#!/bin/bash`.</span></span>| 
| <span data-ttu-id="df941-118">TestScript</span><span class="sxs-lookup"><span data-stu-id="df941-118">TestScript</span></span>| <span data-ttu-id="df941-119">Egy parancsfájlt tartalmaz.</span><span class="sxs-lookup"><span data-stu-id="df941-119">Provides a script.</span></span> <span data-ttu-id="df941-120">Ha meghívása a [Start-DscConfiguration](https://technet.microsoft.com/en-us/library/dn521623.aspx) parancsmag, ez a parancsfájl futtatása.</span><span class="sxs-lookup"><span data-stu-id="df941-120">When you invoke the [Start-DscConfiguration](https://technet.microsoft.com/en-us/library/dn521623.aspx) cmdlet, this script runs.</span></span> <span data-ttu-id="df941-121">Eltérő 0 kilépési kódot adja vissza, ha a SetScript fog futni.</span><span class="sxs-lookup"><span data-stu-id="df941-121">If it returns an exit code other than 0, the SetScript will run.</span></span> <span data-ttu-id="df941-122">Ha a 0 kilépési kódot adja vissza a **SetScript** nem fog futni.</span><span class="sxs-lookup"><span data-stu-id="df941-122">If it returns an exit code of 0, the **SetScript** will not run.</span></span> <span data-ttu-id="df941-123">A **TestScript** indításakor fut a [teszt-DscConfiguration](https://technet.microsoft.com/en-us/library/dn407382.aspx) parancsmag.</span><span class="sxs-lookup"><span data-stu-id="df941-123">The **TestScript** also runs when you invoke the [Test-DscConfiguration](https://technet.microsoft.com/en-us/library/dn407382.aspx) cmdlet.</span></span> <span data-ttu-id="df941-124">Azonban ebben az esetben az a **SetScript** nem fog futni, függetlenül attól, milyen kilépési kódot küld vissza a **TestScript**.</span><span class="sxs-lookup"><span data-stu-id="df941-124">However, in this case, the **SetScript** will not run, no matter what exit code is returned from the **TestScript**.</span></span> <span data-ttu-id="df941-125">A **TestScript** 0 kilépési kódot kell visszaadnia, ha a tényleges konfigurációja megegyezik az aktuális kívánt állapot konfigurációs, és egy kilépési kód más, mint 0, ha nem felel meg.</span><span class="sxs-lookup"><span data-stu-id="df941-125">The **TestScript** must return an exit code of 0 if the actual configuration matches the current desired state configuration, and an exit code other than 0 if it does not match.</span></span> <span data-ttu-id="df941-126">(Az aktuális kívánt állapot konfigurációs a csomópont által használt DSC helyeztek utolsó konfiguráció).</span><span class="sxs-lookup"><span data-stu-id="df941-126">(The current desired state configuration is the last configuration enacted on the node that is using DSC).</span></span> <span data-ttu-id="df941-127">A parancsfájl egy shebang, például a 1#!/bin/bash.1 kell kezdődnie.</span><span class="sxs-lookup"><span data-stu-id="df941-127">The script must begin with a shebang, such as 1#!/bin/bash.1</span></span>| 
| <span data-ttu-id="df941-128">Felhasználó</span><span class="sxs-lookup"><span data-stu-id="df941-128">User</span></span>| <span data-ttu-id="df941-129">A felhasználó, a parancsfájl futtatásához.</span><span class="sxs-lookup"><span data-stu-id="df941-129">The user to run the script as.</span></span>| 
| <span data-ttu-id="df941-130">Group</span><span class="sxs-lookup"><span data-stu-id="df941-130">Group</span></span>| <span data-ttu-id="df941-131">A csoport, a parancsfájl futtatásához.</span><span class="sxs-lookup"><span data-stu-id="df941-131">The group to run the script as.</span></span>| 
| <span data-ttu-id="df941-132">dependsOn</span><span class="sxs-lookup"><span data-stu-id="df941-132">DependsOn</span></span> | <span data-ttu-id="df941-133">Azt jelzi, hogy egy másik erőforrás konfigurációjának kell futtatni, mielőtt ehhez az erőforráshoz van konfigurálva.</span><span class="sxs-lookup"><span data-stu-id="df941-133">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="df941-134">Például ha a **azonosító** az erőforrás konfigurációs futtatni kívánt először parancsprogramblokkja **ResourceName** és annak típusa **ResourceType**, ez a szintaxis a tulajdonság `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="df941-134">For example, if the **ID** of the resource configuration script block that you want to run first is **ResourceName** and its type is **ResourceType**, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>| 

## <a name="example"></a><span data-ttu-id="df941-135">Példa</span><span class="sxs-lookup"><span data-stu-id="df941-135">Example</span></span>

<span data-ttu-id="df941-136">A következő példa bemutatja, hogy a **nxScript** erőforrás további kezelési végrehajtásához.</span><span class="sxs-lookup"><span data-stu-id="df941-136">The following example demonstrates the use of the **nxScript** resource to perform additional configuration management.</span></span>

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

