---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: DSC, a Linux nxService erőforrás
ms.openlocfilehash: ab6544762862c9b2477e92f0d782b13afb96f2c9
ms.sourcegitcommit: 77f62a55cac8c13d69d51eef5fade18f71d66955
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/17/2018
ms.locfileid: "39093568"
---
# <a name="dsc-for-linux-nxservice-resource"></a><span data-ttu-id="7e26e-103">DSC, a Linux nxService erőforrás</span><span class="sxs-lookup"><span data-stu-id="7e26e-103">DSC for Linux nxService Resource</span></span>

<span data-ttu-id="7e26e-104">A **nxService** erőforrás a PowerShell Desired State Configuration (DSC) biztosít egy mechanizmust, amely egy Linux-csomóponton a szolgáltatások kezeléséhez.</span><span class="sxs-lookup"><span data-stu-id="7e26e-104">The **nxService** resource in PowerShell Desired State Configuration (DSC) provides a mechanism to manage services on a Linux node.</span></span>

## <a name="syntax"></a><span data-ttu-id="7e26e-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="7e26e-105">Syntax</span></span>

```
nxService <string> #ResourceName
{
    Name = <string>
    [ Controller = <string> { init | upstart | systemd } ]
    [ Enabled = <bool> ]
    [ State = <string> { Running | Stopped } ]
    [ DependsOn = <string[]> ]
}
```

## <a name="properties"></a><span data-ttu-id="7e26e-106">Tulajdonságok</span><span class="sxs-lookup"><span data-stu-id="7e26e-106">Properties</span></span>
|  <span data-ttu-id="7e26e-107">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="7e26e-107">Property</span></span> |  <span data-ttu-id="7e26e-108">Leírás</span><span class="sxs-lookup"><span data-stu-id="7e26e-108">Description</span></span> |
|---|---|
| <span data-ttu-id="7e26e-109">Név</span><span class="sxs-lookup"><span data-stu-id="7e26e-109">Name</span></span>| <span data-ttu-id="7e26e-110">A szolgáltatás/démon konfigurálása neve.</span><span class="sxs-lookup"><span data-stu-id="7e26e-110">The name of the service/daemon to configure.</span></span>|
| <span data-ttu-id="7e26e-111">Tartományvezérlő</span><span class="sxs-lookup"><span data-stu-id="7e26e-111">Controller</span></span>| <span data-ttu-id="7e26e-112">A szolgáltatás konfigurálásakor használandó szolgáltatásvezérlő típusa.</span><span class="sxs-lookup"><span data-stu-id="7e26e-112">The type of service controller to use when configuring the service.</span></span>|
| <span data-ttu-id="7e26e-113">Engedélyezve</span><span class="sxs-lookup"><span data-stu-id="7e26e-113">Enabled</span></span>| <span data-ttu-id="7e26e-114">Azt jelzi, hogy a szolgáltatás elindul, a rendszerindító.</span><span class="sxs-lookup"><span data-stu-id="7e26e-114">Indicates whether the service starts on boot.</span></span>|
| <span data-ttu-id="7e26e-115">Állapot</span><span class="sxs-lookup"><span data-stu-id="7e26e-115">State</span></span>| <span data-ttu-id="7e26e-116">Azt jelzi, hogy a szolgáltatás fut-e.</span><span class="sxs-lookup"><span data-stu-id="7e26e-116">Indicates whether the service is running.</span></span> <span data-ttu-id="7e26e-117">Ez annak biztosítása érdekében, hogy a szolgáltatás nem fut a "Stopped" tulajdonság értéke.</span><span class="sxs-lookup"><span data-stu-id="7e26e-117">Set this property to "Stopped" to ensure that the service is not running.</span></span> <span data-ttu-id="7e26e-118">Állítsa be, győződjön meg arról, hogy a szolgáltatás nem fut a "fut".</span><span class="sxs-lookup"><span data-stu-id="7e26e-118">Set it to "Running" to ensure that the service is not running.</span></span>|
| <span data-ttu-id="7e26e-119">DependsOn</span><span class="sxs-lookup"><span data-stu-id="7e26e-119">DependsOn</span></span> | <span data-ttu-id="7e26e-120">Azt jelzi, hogy a konfigurációt egy másik erőforrás futtatnia kell, mielőtt az erőforrás konfigurálva van.</span><span class="sxs-lookup"><span data-stu-id="7e26e-120">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="7e26e-121">Például ha a **azonosító** az erőforrás, amely a futtatni kívánt konfigurációs parancsprogram-blokkot első az **ResourceName** és a típusa **ResourceType**, ezzel esetén a tulajdonság `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="7e26e-121">For example, if the **ID** of the resource configuration script block that you want to run first is **ResourceName** and its type is **ResourceType**, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|

## <a name="additional-information"></a><span data-ttu-id="7e26e-122">További információ</span><span class="sxs-lookup"><span data-stu-id="7e26e-122">Additional Information</span></span>

<span data-ttu-id="7e26e-123">A **nxService** erőforrás nem hozza létre a szolgáltatás definíciós vagy parancsfájl a szolgáltatás, ha még nem létezik.</span><span class="sxs-lookup"><span data-stu-id="7e26e-123">The **nxService** resource will not create a service definition or script for the service if it does not exist.</span></span> <span data-ttu-id="7e26e-124">Használhatja a PowerShell Desired State Configuration **nxFile** erőforrásra megléte vagy a szolgáltatásdefiníciós fájl vagy parancsfájl tartalmát kezeléséhez.</span><span class="sxs-lookup"><span data-stu-id="7e26e-124">You can use the PowerShell Desired State Configuration **nxFile** Resource resource to manage the existence or contents of the service definition file or script.</span></span>

## <a name="example"></a><span data-ttu-id="7e26e-125">Példa</span><span class="sxs-lookup"><span data-stu-id="7e26e-125">Example</span></span>

<span data-ttu-id="7e26e-126">Az alábbi példa bemutatja a regisztrált (az Apache HTTP Server), "httpd" szolgáltatás konfigurációját a **SystemD** szolgáltatásvezérlőhöz.</span><span class="sxs-lookup"><span data-stu-id="7e26e-126">The following example shows configuration of the 'httpd' service (for Apache HTTP Server), registered with the **SystemD** service controller.</span></span>

```powershell
Import-DSCResource -Module nx

Node $node {
    #Apache Service
    nxService ApacheService {
        Name = 'httpd'
        State = 'running'
        Enabled = $true
        Controller = 'systemd'
    }
}
```