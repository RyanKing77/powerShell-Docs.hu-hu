---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "A DSC WaitForAll erőforrás"
ms.openlocfilehash: 2054d2af7cd7dd839c62e77c1d4b6eee5cff34ab
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 01/17/2018
---
# <a name="dsc-waitforall-resource"></a><span data-ttu-id="80bd9-103">A DSC WaitForAll erőforrás</span><span class="sxs-lookup"><span data-stu-id="80bd9-103">DSC WaitForAll Resource</span></span>

> <span data-ttu-id="80bd9-104">Vonatkozik: A Windows PowerShell 5.0-s és újabb verziók</span><span class="sxs-lookup"><span data-stu-id="80bd9-104">Applies To: Windows PowerShell 5.0 and later</span></span>

<span data-ttu-id="80bd9-105">A **WaitForAll** kívánt állapot konfigurációs szolgáltatása (DSC) erőforrás használhatja egy csomópont blokkja egy [DSC-konfiguráció](configurations.md) függőségek konfigurációk létrehozáskor határozza meg.</span><span class="sxs-lookup"><span data-stu-id="80bd9-105">The **WaitForAll** Desired State Configuration (DSC) resource can be used within a node block in a [DSC configuration](configurations.md) to specify dependencies on configurations on other nodes.</span></span>

<span data-ttu-id="80bd9-106">Ehhez az erőforráshoz sikeres lesz, ha az erőforrás által megadott Ha a **ResourceName** tulajdonság definiált összes cél csomóponton megfelelő állapotban van a **csomópontnév** tulajdonság.</span><span class="sxs-lookup"><span data-stu-id="80bd9-106">This resource succeeds if if the resource specified by the **ResourceName** property is in the desired state on all target nodes defined in the **NodeName** property.</span></span>


## <a name="syntax"></a><span data-ttu-id="80bd9-107">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="80bd9-107">Syntax</span></span>

```
WaitForAll [string] #ResourceName
{
    ResourceName = [string]
    NodeName = [string]
    [ RetryIntervalSec = [Uint64] ]
    [ RetryCount = [Uint32] ] 
    [ ThrottleLimit = [Uint32]]
    [ DependsOn = [string[]] ]
}
```

## <a name="properties"></a><span data-ttu-id="80bd9-108">Tulajdonságok</span><span class="sxs-lookup"><span data-stu-id="80bd9-108">Properties</span></span>

|  <span data-ttu-id="80bd9-109">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="80bd9-109">Property</span></span>  |  <span data-ttu-id="80bd9-110">Leírás</span><span class="sxs-lookup"><span data-stu-id="80bd9-110">Description</span></span>   | 
|---|---| 
| <span data-ttu-id="80bd9-111">resourceName</span><span class="sxs-lookup"><span data-stu-id="80bd9-111">ResourceName</span></span>| <span data-ttu-id="80bd9-112">Az erőforrásnév függ.</span><span class="sxs-lookup"><span data-stu-id="80bd9-112">The resource name to depend on.</span></span>| 
| <span data-ttu-id="80bd9-113">Csomópontnév</span><span class="sxs-lookup"><span data-stu-id="80bd9-113">NodeName</span></span>| <span data-ttu-id="80bd9-114">Az erőforrás függ a célcsomópontokat.</span><span class="sxs-lookup"><span data-stu-id="80bd9-114">The target nodes of the resource to depend on.</span></span>| 
| <span data-ttu-id="80bd9-115">RetryIntervalSec</span><span class="sxs-lookup"><span data-stu-id="80bd9-115">RetryIntervalSec</span></span>| <span data-ttu-id="80bd9-116">Másodpercig az újrapróbálkozás előtt száma.</span><span class="sxs-lookup"><span data-stu-id="80bd9-116">The number of seconds before retrying.</span></span> <span data-ttu-id="80bd9-117">Minimális érték 1.</span><span class="sxs-lookup"><span data-stu-id="80bd9-117">Minimum is 1.</span></span>| 
| <span data-ttu-id="80bd9-118">a retryCount</span><span class="sxs-lookup"><span data-stu-id="80bd9-118">RetryCount</span></span>| <span data-ttu-id="80bd9-119">A próbálkozások maximális számát.</span><span class="sxs-lookup"><span data-stu-id="80bd9-119">The maximum number of times to retry.</span></span>| 
| <span data-ttu-id="80bd9-120">ThrottleLimit</span><span class="sxs-lookup"><span data-stu-id="80bd9-120">ThrottleLimit</span></span>| <span data-ttu-id="80bd9-121">Az egyidejű csatlakozást a gépek számát.</span><span class="sxs-lookup"><span data-stu-id="80bd9-121">Number of machines to connect simultaneously.</span></span> <span data-ttu-id="80bd9-122">Alapértelmezés szerint új-cimsession alapértelmezett.</span><span class="sxs-lookup"><span data-stu-id="80bd9-122">Default is new-cimsession default.</span></span>| 
| <span data-ttu-id="80bd9-123">dependsOn</span><span class="sxs-lookup"><span data-stu-id="80bd9-123">DependsOn</span></span> | <span data-ttu-id="80bd9-124">Azt jelzi, hogy egy másik erőforrás konfigurációjának kell futtatni, mielőtt ehhez az erőforráshoz van konfigurálva.</span><span class="sxs-lookup"><span data-stu-id="80bd9-124">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="80bd9-125">Például, ha az erőforrás-konfiguráció azonosítója blokk futtatni kívánt parancsfájl első az __ResourceName__ és annak típusa __ResourceType__, az e tulajdonság használatával szintaxisa a következő `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="80bd9-125">For example, if the ID of the resource configuration script block that you want to run first is __ResourceName__ and its type is __ResourceType__, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|


## <a name="example"></a><span data-ttu-id="80bd9-126">Példa</span><span class="sxs-lookup"><span data-stu-id="80bd9-126">Example</span></span>

<span data-ttu-id="80bd9-127">Példa bemutatja, hogyan az erőforrás, lásd: [cross-csomópont függőségeinek megadása](crossNodeDependencies.md)</span><span class="sxs-lookup"><span data-stu-id="80bd9-127">For an example of how to use this resource, see [Specifying cross-node dependencies](crossNodeDependencies.md)</span></span>

