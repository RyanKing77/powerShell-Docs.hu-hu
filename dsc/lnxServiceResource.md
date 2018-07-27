---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: DSC, a Linux nxService erőforrás
ms.openlocfilehash: fe8043995205649378725f2ab0a78e19313739c9
ms.sourcegitcommit: c3f1a83b59484651119630f3089aa51b6e7d4c3c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/26/2018
ms.locfileid: "39267779"
---
# <a name="dsc-for-linux-nxservice-resource"></a><span data-ttu-id="7916d-103">DSC, a Linux nxService erőforrás</span><span class="sxs-lookup"><span data-stu-id="7916d-103">DSC for Linux nxService Resource</span></span>

<span data-ttu-id="7916d-104">A **nxService** erőforrás a PowerShell Desired State Configuration (DSC) biztosít egy mechanizmust, amely egy Linux-csomóponton a szolgáltatások kezeléséhez.</span><span class="sxs-lookup"><span data-stu-id="7916d-104">The **nxService** resource in PowerShell Desired State Configuration (DSC) provides a mechanism to manage services on a Linux node.</span></span>

## <a name="syntax"></a><span data-ttu-id="7916d-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="7916d-105">Syntax</span></span>

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

## <a name="properties"></a><span data-ttu-id="7916d-106">Tulajdonságok</span><span class="sxs-lookup"><span data-stu-id="7916d-106">Properties</span></span>

| <span data-ttu-id="7916d-107">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="7916d-107">Property</span></span> | <span data-ttu-id="7916d-108">Leírás</span><span class="sxs-lookup"><span data-stu-id="7916d-108">Description</span></span> |
|---|---|
| <span data-ttu-id="7916d-109">Név</span><span class="sxs-lookup"><span data-stu-id="7916d-109">Name</span></span>| <span data-ttu-id="7916d-110">A szolgáltatás/démon konfigurálása neve.</span><span class="sxs-lookup"><span data-stu-id="7916d-110">The name of the service/daemon to configure.</span></span>|
| <span data-ttu-id="7916d-111">Tartományvezérlő</span><span class="sxs-lookup"><span data-stu-id="7916d-111">Controller</span></span>| <span data-ttu-id="7916d-112">A szolgáltatás konfigurálásakor használandó szolgáltatásvezérlő típusa.</span><span class="sxs-lookup"><span data-stu-id="7916d-112">The type of service controller to use when configuring the service.</span></span>|
| <span data-ttu-id="7916d-113">Engedélyezve</span><span class="sxs-lookup"><span data-stu-id="7916d-113">Enabled</span></span>| <span data-ttu-id="7916d-114">Azt jelzi, hogy a szolgáltatás elindul, a rendszerindító.</span><span class="sxs-lookup"><span data-stu-id="7916d-114">Indicates whether the service starts on boot.</span></span>|
| <span data-ttu-id="7916d-115">Állapot</span><span class="sxs-lookup"><span data-stu-id="7916d-115">State</span></span>| <span data-ttu-id="7916d-116">Azt jelzi, hogy a szolgáltatás fut-e.</span><span class="sxs-lookup"><span data-stu-id="7916d-116">Indicates whether the service is running.</span></span> <span data-ttu-id="7916d-117">Ez annak biztosítása érdekében, hogy a szolgáltatás nem fut a "Stopped" tulajdonság értéke.</span><span class="sxs-lookup"><span data-stu-id="7916d-117">Set this property to "Stopped" to ensure that the service is not running.</span></span> <span data-ttu-id="7916d-118">Állítsa be, győződjön meg arról, hogy a szolgáltatás nem fut a "fut".</span><span class="sxs-lookup"><span data-stu-id="7916d-118">Set it to "Running" to ensure that the service is not running.</span></span>|
| <span data-ttu-id="7916d-119">DependsOn</span><span class="sxs-lookup"><span data-stu-id="7916d-119">DependsOn</span></span> | <span data-ttu-id="7916d-120">Azt jelzi, hogy a konfigurációt egy másik erőforrás futtatnia kell, mielőtt az erőforrás konfigurálva van.</span><span class="sxs-lookup"><span data-stu-id="7916d-120">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="7916d-121">Például ha a **azonosító** az erőforrás, amely a futtatni kívánt konfigurációs parancsprogram-blokkot első az **ResourceName** és a típusa **ResourceType**, ezzel esetén a tulajdonság `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="7916d-121">For example, if the **ID** of the resource configuration script block that you want to run first is **ResourceName** and its type is **ResourceType**, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|

## <a name="additional-information"></a><span data-ttu-id="7916d-122">További információ</span><span class="sxs-lookup"><span data-stu-id="7916d-122">Additional Information</span></span>

<span data-ttu-id="7916d-123">A **nxService** erőforrás nem hozza létre a szolgáltatás definíciós vagy parancsfájl a szolgáltatás, ha még nem létezik.</span><span class="sxs-lookup"><span data-stu-id="7916d-123">The **nxService** resource will not create a service definition or script for the service if it does not exist.</span></span> <span data-ttu-id="7916d-124">Használhatja a PowerShell Desired State Configuration **nxFile** erőforrásra megléte vagy a szolgáltatásdefiníciós fájl vagy parancsfájl tartalmát kezeléséhez.</span><span class="sxs-lookup"><span data-stu-id="7916d-124">You can use the PowerShell Desired State Configuration **nxFile** Resource resource to manage the existence or contents of the service definition file or script.</span></span>

## <a name="example"></a><span data-ttu-id="7916d-125">Példa</span><span class="sxs-lookup"><span data-stu-id="7916d-125">Example</span></span>

<span data-ttu-id="7916d-126">Az alábbi példa bemutatja a regisztrált (az Apache HTTP Server), "httpd" szolgáltatás konfigurációját a **SystemD** szolgáltatásvezérlőhöz.</span><span class="sxs-lookup"><span data-stu-id="7916d-126">The following example shows configuration of the 'httpd' service (for Apache HTTP Server), registered with the **SystemD** service controller.</span></span>

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