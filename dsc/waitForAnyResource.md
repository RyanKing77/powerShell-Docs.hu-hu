---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: DSC WaitForAny erőforrás
ms.openlocfilehash: 39100f0fc52092c54bbecab55e3ef3dfabb4c70e
ms.sourcegitcommit: e76665315fd928bf85210778f1fea2be15264fea
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/30/2018
ms.locfileid: "50226049"
---
# <a name="dsc-waitforany-resource"></a><span data-ttu-id="816d6-103">DSC WaitForAny erőforrás</span><span class="sxs-lookup"><span data-stu-id="816d6-103">DSC WaitForAny Resource</span></span>

> <span data-ttu-id="816d6-104">A következőkre vonatkozik: Windows PowerShell 5.1-es és újabb verziók</span><span class="sxs-lookup"><span data-stu-id="816d6-104">Applies To: Windows PowerShell 5.1 and later</span></span>

<span data-ttu-id="816d6-105">A **WaitForSome** egy csomópont letiltása a Desired State Configuration (DSC) erőforrás használható egy [DSC-konfiguráció](configurations.md) függőségeinek megadása a konfigurációk a többi csomóponton.</span><span class="sxs-lookup"><span data-stu-id="816d6-105">The **WaitForSome** Desired State Configuration (DSC) resource can be used within a node block in a [DSC configuration](configurations.md) to specify dependencies on configurations on other nodes.</span></span>

<span data-ttu-id="816d6-106">Ez az erőforrás sikeres lesz, abban az esetben, ha az erőforrás által meghatározott a **ResourceName** tulajdonság bármely meghatározott cél-csomópontokon a kívánt állapotban van a **csomópontnév** tulajdonság.</span><span class="sxs-lookup"><span data-stu-id="816d6-106">This resource succeeds if the resource specified by the **ResourceName** property is in the desired state on any target nodes defined in the **NodeName** property.</span></span>


## <a name="syntax"></a><span data-ttu-id="816d6-107">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="816d6-107">Syntax</span></span>

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

## <a name="properties"></a><span data-ttu-id="816d6-108">Tulajdonságok</span><span class="sxs-lookup"><span data-stu-id="816d6-108">Properties</span></span>

|  <span data-ttu-id="816d6-109">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="816d6-109">Property</span></span>  |  <span data-ttu-id="816d6-110">Leírás</span><span class="sxs-lookup"><span data-stu-id="816d6-110">Description</span></span>   |
|---|---|
| <span data-ttu-id="816d6-111">Erőforrásnév</span><span class="sxs-lookup"><span data-stu-id="816d6-111">ResourceName</span></span>| <span data-ttu-id="816d6-112">Az erőforrásnév függenek.</span><span class="sxs-lookup"><span data-stu-id="816d6-112">The resource name to depend on.</span></span> <span data-ttu-id="816d6-113">Ha az erőforrás tartozik egy másik konfigurációs, formázhatja a nevet a következőként "[__ResourceType__]__ResourceName__:: [__ConfigurationName__]:: [ __ConfigurationName__] "</span><span class="sxs-lookup"><span data-stu-id="816d6-113">If this resource belongs to a different configuration, format the name as "[__ResourceType__]__ResourceName__::[__ConfigurationName__]::[__ConfigurationName__]"</span></span>|
| <span data-ttu-id="816d6-114">Csomópontnév</span><span class="sxs-lookup"><span data-stu-id="816d6-114">NodeName</span></span>| <span data-ttu-id="816d6-115">Az erőforrás függenek a célcsomópontokat.</span><span class="sxs-lookup"><span data-stu-id="816d6-115">The target nodes of the resource to depend on.</span></span>|
| <span data-ttu-id="816d6-116">RetryIntervalSec</span><span class="sxs-lookup"><span data-stu-id="816d6-116">RetryIntervalSec</span></span>| <span data-ttu-id="816d6-117">Mielőtt újra próbálkozna másodpercek számát.</span><span class="sxs-lookup"><span data-stu-id="816d6-117">The number of seconds before retrying.</span></span> <span data-ttu-id="816d6-118">Minimális érték 1.</span><span class="sxs-lookup"><span data-stu-id="816d6-118">Minimum is 1.</span></span>|
| <span data-ttu-id="816d6-119">retryCount</span><span class="sxs-lookup"><span data-stu-id="816d6-119">RetryCount</span></span>| <span data-ttu-id="816d6-120">Az újrapróbálkozások maximális száma.</span><span class="sxs-lookup"><span data-stu-id="816d6-120">The maximum number of times to retry.</span></span>|
| <span data-ttu-id="816d6-121">ThrottleLimit</span><span class="sxs-lookup"><span data-stu-id="816d6-121">ThrottleLimit</span></span>| <span data-ttu-id="816d6-122">Egyidejű csatlakozás gépek száma.</span><span class="sxs-lookup"><span data-stu-id="816d6-122">Number of machines to connect simultaneously.</span></span> <span data-ttu-id="816d6-123">Alapértelmezés szerint új cimsession alapértelmezett.</span><span class="sxs-lookup"><span data-stu-id="816d6-123">Default is new-cimsession default.</span></span>|
| <span data-ttu-id="816d6-124">DependsOn</span><span class="sxs-lookup"><span data-stu-id="816d6-124">DependsOn</span></span> | <span data-ttu-id="816d6-125">Azt jelzi, hogy a konfigurációt egy másik erőforrás futtatnia kell, mielőtt az erőforrás konfigurálva van.</span><span class="sxs-lookup"><span data-stu-id="816d6-125">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="816d6-126">Például, ha az erőforrás-konfiguráció azonosítója letiltása, a futtatni kívánt parancsfájl először van __ResourceName__ és a típusa __ResourceType__, ez a tulajdonság használata esetén `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="816d6-126">For example, if the ID of the resource configuration script block that you want to run first is __ResourceName__ and its type is __ResourceType__, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|


## <a name="example"></a><span data-ttu-id="816d6-127">Példa</span><span class="sxs-lookup"><span data-stu-id="816d6-127">Example</span></span>

<span data-ttu-id="816d6-128">Egy példa bemutatja, hogyan használhatja ezt az erőforrást: [csomópontok közötti függőségek megadása](crossNodeDependencies.md)</span><span class="sxs-lookup"><span data-stu-id="816d6-128">For an example of how to use this resource, see [Specifying cross-node dependencies](crossNodeDependencies.md)</span></span>