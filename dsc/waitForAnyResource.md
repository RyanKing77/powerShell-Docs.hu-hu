---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "A DSC WaitForAny erőforrás"
ms.openlocfilehash: 795c005c67c196ef9afb08af790fe2a1695392ec
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 01/17/2018
---
# <a name="dsc-waitforany-resource"></a><span data-ttu-id="e8cbb-103">A DSC WaitForAny erőforrás</span><span class="sxs-lookup"><span data-stu-id="e8cbb-103">DSC WaitForAny Resource</span></span>

> <span data-ttu-id="e8cbb-104">Vonatkozik: A Windows PowerShell 5.1-es és újabb verziók</span><span class="sxs-lookup"><span data-stu-id="e8cbb-104">Applies To: Windows PowerShell 5.1 and later</span></span>

<span data-ttu-id="e8cbb-105">A **WaitForSome** kívánt állapot konfigurációs szolgáltatása (DSC) erőforrás használhatja egy csomópont blokkja egy [DSC-konfiguráció](configurations.md) függőségek konfigurációk létrehozáskor határozza meg.</span><span class="sxs-lookup"><span data-stu-id="e8cbb-105">The **WaitForSome** Desired State Configuration (DSC) resource can be used within a node block in a [DSC configuration](configurations.md) to specify dependencies on configurations on other nodes.</span></span>

<span data-ttu-id="e8cbb-106">Ehhez az erőforráshoz sikeres lesz, ha az erőforrás által megadott Ha a **ResourceName** tulajdonság a bármilyen definiált célcsomópontokat megfelelő állapotban van a **csomópontnév** tulajdonság.</span><span class="sxs-lookup"><span data-stu-id="e8cbb-106">This resource succeeds if if the resource specified by the **ResourceName** property is in the desired state on any target nodes defined in the **NodeName** property.</span></span>


## <a name="syntax"></a><span data-ttu-id="e8cbb-107">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="e8cbb-107">Syntax</span></span>

```
WaitForAny [string] #ResourceName
{
    ResourceName = [string]
    NodeName = [string]
    [ RetryIntervalSec = [Uint64] ]
    [ RetryCount = [Uint32] ] 
    [ ThrottleLimit = [Uint32]]
    [ DependsOn = [string[]] ]
}
```

## <a name="properties"></a><span data-ttu-id="e8cbb-108">Tulajdonságok</span><span class="sxs-lookup"><span data-stu-id="e8cbb-108">Properties</span></span>

|  <span data-ttu-id="e8cbb-109">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="e8cbb-109">Property</span></span>  |  <span data-ttu-id="e8cbb-110">Leírás</span><span class="sxs-lookup"><span data-stu-id="e8cbb-110">Description</span></span>   | 
|---|---| 
| <span data-ttu-id="e8cbb-111">resourceName</span><span class="sxs-lookup"><span data-stu-id="e8cbb-111">ResourceName</span></span>| <span data-ttu-id="e8cbb-112">Az erőforrásnév függ.</span><span class="sxs-lookup"><span data-stu-id="e8cbb-112">The resource name to depend on.</span></span>| 
| <span data-ttu-id="e8cbb-113">Csomópontnév</span><span class="sxs-lookup"><span data-stu-id="e8cbb-113">NodeName</span></span>| <span data-ttu-id="e8cbb-114">Az erőforrás függ a célcsomópontokat.</span><span class="sxs-lookup"><span data-stu-id="e8cbb-114">The target nodes of the resource to depend on.</span></span>| 
| <span data-ttu-id="e8cbb-115">RetryIntervalSec</span><span class="sxs-lookup"><span data-stu-id="e8cbb-115">RetryIntervalSec</span></span>| <span data-ttu-id="e8cbb-116">Másodpercig az újrapróbálkozás előtt száma.</span><span class="sxs-lookup"><span data-stu-id="e8cbb-116">The number of seconds before retrying.</span></span> <span data-ttu-id="e8cbb-117">Minimális érték 1.</span><span class="sxs-lookup"><span data-stu-id="e8cbb-117">Minimum is 1.</span></span>| 
| <span data-ttu-id="e8cbb-118">a retryCount</span><span class="sxs-lookup"><span data-stu-id="e8cbb-118">RetryCount</span></span>| <span data-ttu-id="e8cbb-119">A próbálkozások maximális számát.</span><span class="sxs-lookup"><span data-stu-id="e8cbb-119">The maximum number of times to retry.</span></span>| 
| <span data-ttu-id="e8cbb-120">ThrottleLimit</span><span class="sxs-lookup"><span data-stu-id="e8cbb-120">ThrottleLimit</span></span>| <span data-ttu-id="e8cbb-121">Az egyidejű csatlakozást a gépek számát.</span><span class="sxs-lookup"><span data-stu-id="e8cbb-121">Number of machines to connect simultaneously.</span></span> <span data-ttu-id="e8cbb-122">Alapértelmezés szerint új-cimsession alapértelmezett.</span><span class="sxs-lookup"><span data-stu-id="e8cbb-122">Default is new-cimsession default.</span></span>| 
| <span data-ttu-id="e8cbb-123">dependsOn</span><span class="sxs-lookup"><span data-stu-id="e8cbb-123">DependsOn</span></span> | <span data-ttu-id="e8cbb-124">Azt jelzi, hogy egy másik erőforrás konfigurációjának kell futtatni, mielőtt ehhez az erőforráshoz van konfigurálva.</span><span class="sxs-lookup"><span data-stu-id="e8cbb-124">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="e8cbb-125">Például, ha az erőforrás-konfiguráció azonosítója blokk futtatni kívánt parancsfájl első az __ResourceName__ és annak típusa __ResourceType__, az e tulajdonság használatával szintaxisa a következő `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="e8cbb-125">For example, if the ID of the resource configuration script block that you want to run first is __ResourceName__ and its type is __ResourceType__, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|


## <a name="example"></a><span data-ttu-id="e8cbb-126">Példa</span><span class="sxs-lookup"><span data-stu-id="e8cbb-126">Example</span></span>

<span data-ttu-id="e8cbb-127">Példa bemutatja, hogyan az erőforrás, lásd: [cross-csomópont függőségeinek megadása](crossNodeDependencies.md)</span><span class="sxs-lookup"><span data-stu-id="e8cbb-127">For an example of how to use this resource, see [Specifying cross-node dependencies](crossNodeDependencies.md)</span></span>

