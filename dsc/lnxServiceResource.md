---
ms.date: 06/12/2017
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: A Linux nxService erőforrás DSC
ms.openlocfilehash: 9cab889368469f2c854a387b919aea58a49f2210
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/16/2018
ms.locfileid: "34187718"
---
# <a name="dsc-for-linux-nxservice-resource"></a><span data-ttu-id="38350-103">A Linux nxService erőforrás DSC</span><span class="sxs-lookup"><span data-stu-id="38350-103">DSC for Linux nxService Resource</span></span>

<span data-ttu-id="38350-104">A **nxService** erőforrás a PowerShell kívánt állapot konfigurációs szolgáltatása (DSC) lehetővé teszi a szolgáltatások egy Linux-csomóponton kezelésére.</span><span class="sxs-lookup"><span data-stu-id="38350-104">The **nxService** resource in PowerShell Desired State Configuration (DSC) provides a mechanism to manage services on a Linux node.</span></span>

## <a name="syntax"></a><span data-ttu-id="38350-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="38350-105">Syntax</span></span>

```
nxService <string> #ResourceName
{
    Name = <string>
    [ Controller = <string> { init | upstart | systemd }  ]
    [ Enabled = <bool> ]
    [ State = <string> { Running | Stopped } ]
    [ DependsOn = <string[]> ]

}
```

## <a name="properties"></a><span data-ttu-id="38350-106">Tulajdonságok</span><span class="sxs-lookup"><span data-stu-id="38350-106">Properties</span></span>
|  <span data-ttu-id="38350-107">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="38350-107">Property</span></span> |  <span data-ttu-id="38350-108">Leírás</span><span class="sxs-lookup"><span data-stu-id="38350-108">Description</span></span> |
|---|---|
| <span data-ttu-id="38350-109">Név</span><span class="sxs-lookup"><span data-stu-id="38350-109">Name</span></span>| <span data-ttu-id="38350-110">A szolgáltatás/démon konfigurálása neve.</span><span class="sxs-lookup"><span data-stu-id="38350-110">The name of the service/daemon to configure.</span></span>|
| <span data-ttu-id="38350-111">Tartományvezérlő</span><span class="sxs-lookup"><span data-stu-id="38350-111">Controller</span></span>| <span data-ttu-id="38350-112">A szolgáltatás konfigurálásakor használandó szolgáltatásvezérlővel típusa.</span><span class="sxs-lookup"><span data-stu-id="38350-112">The type of service controller to use when configuring the service.</span></span>|
| <span data-ttu-id="38350-113">Engedélyezve</span><span class="sxs-lookup"><span data-stu-id="38350-113">Enabled</span></span>| <span data-ttu-id="38350-114">Azt jelzi, hogy a szolgáltatás elindul, a rendszerindító.</span><span class="sxs-lookup"><span data-stu-id="38350-114">Indicates whether the service starts on boot.</span></span>|
| <span data-ttu-id="38350-115">Állapot</span><span class="sxs-lookup"><span data-stu-id="38350-115">State</span></span>| <span data-ttu-id="38350-116">Azt jelzi, hogy a szolgáltatás fut-e.</span><span class="sxs-lookup"><span data-stu-id="38350-116">Indicates whether the service is running.</span></span> <span data-ttu-id="38350-117">"Leállítva" Győződjön meg arról, hogy a szolgáltatás nem fut a tulajdonság értékét.</span><span class="sxs-lookup"><span data-stu-id="38350-117">Set this property to "Stopped" to ensure that the service is not running.</span></span> <span data-ttu-id="38350-118">Állítsa az értékét annak érdekében, hogy a szolgáltatás nem fut a "fut".</span><span class="sxs-lookup"><span data-stu-id="38350-118">Set it to "Running" to ensure that the service is not running.</span></span>|
| <span data-ttu-id="38350-119">dependsOn</span><span class="sxs-lookup"><span data-stu-id="38350-119">DependsOn</span></span> | <span data-ttu-id="38350-120">Azt jelzi, hogy egy másik erőforrás konfigurációjának kell futtatni, mielőtt ehhez az erőforráshoz van konfigurálva.</span><span class="sxs-lookup"><span data-stu-id="38350-120">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="38350-121">Például ha a **azonosító** az erőforrás konfigurációs futtatni kívánt először parancsprogramblokkja **ResourceName** és annak típusa **ResourceType**, ez a szintaxis a tulajdonság `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="38350-121">For example, if the **ID** of the resource configuration script block that you want to run first is **ResourceName** and its type is **ResourceType**, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|


## <a name="additional-information"></a><span data-ttu-id="38350-122">További információ</span><span class="sxs-lookup"><span data-stu-id="38350-122">Additional Information</span></span>

<span data-ttu-id="38350-123">A **nxService** erőforrás nem hoz létre egy szolgáltatásdefiníció vagy a szolgáltatás parancsfájl Ha még nem létezik.</span><span class="sxs-lookup"><span data-stu-id="38350-123">The **nxService** resource will not create a service definition or script for the service if it does not exist.</span></span> <span data-ttu-id="38350-124">Használhatja a PowerShell célállapot-konfiguráció **nxFile** erőforrás erőforrás megléte vagy a szolgáltatásdefiníciós fájl vagy parancsfájl tartalmát kezeléséhez.</span><span class="sxs-lookup"><span data-stu-id="38350-124">You can use the PowerShell Desired State Configuration **nxFile** Resource resource to manage the existence or contents of the service definition file or script.</span></span>

## <a name="example"></a><span data-ttu-id="38350-125">Példa</span><span class="sxs-lookup"><span data-stu-id="38350-125">Example</span></span>

<span data-ttu-id="38350-126">A következő példa bemutatja, regisztrált (az Apache HTTP Server), "httpd" szolgáltatás konfigurációját a **SystemD** szolgáltatásvezérlővel.</span><span class="sxs-lookup"><span data-stu-id="38350-126">The following example shows configuration of the “httpd” service (for Apache HTTP Server), registered with the **SystemD** service controller.</span></span>

```
Import-DSCResource -Module nx

Node $node {
#Apache Service
nxService ApacheService
{
Name = "httpd"
State = "running"
Enabled = $true
Controller = "systemd"
}
}
```