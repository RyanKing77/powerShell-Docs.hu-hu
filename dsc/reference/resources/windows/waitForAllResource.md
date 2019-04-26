---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: DSC WaitForAll erőforrás
ms.openlocfilehash: 1e891f1aecbdbe641973669f71f22664ad8ea16c
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62076922"
---
# <a name="dsc-waitforall-resource"></a><span data-ttu-id="d8529-103">DSC WaitForAll erőforrás</span><span class="sxs-lookup"><span data-stu-id="d8529-103">DSC WaitForAll Resource</span></span>

> <span data-ttu-id="d8529-104">A következőkre vonatkozik: Windows PowerShell 5.0-s és újabb verziók</span><span class="sxs-lookup"><span data-stu-id="d8529-104">Applies To: Windows PowerShell 5.0 and later</span></span>

<span data-ttu-id="d8529-105">A **WaitForAll** egy csomópont letiltása a Desired State Configuration (DSC) erőforrás használható egy [DSC-konfiguráció](../../../configurations/configurations.md) függőségeinek megadása a konfigurációk a többi csomóponton.</span><span class="sxs-lookup"><span data-stu-id="d8529-105">The **WaitForAll** Desired State Configuration (DSC) resource can be used within a node block in a [DSC configuration](../../../configurations/configurations.md) to specify dependencies on configurations on other nodes.</span></span>

<span data-ttu-id="d8529-106">Ez az erőforrás sikeres lesz, abban az esetben, ha az erőforrás által meghatározott a **ResourceName** tulajdonság az összes, meghatározott cél csomóponton a kívánt állapotban van a **csomópontnév** tulajdonság.</span><span class="sxs-lookup"><span data-stu-id="d8529-106">This resource succeeds if the resource specified by the **ResourceName** property is in the desired state on all target nodes defined in the **NodeName** property.</span></span>

## <a name="syntax"></a><span data-ttu-id="d8529-107">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="d8529-107">Syntax</span></span>

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

## <a name="properties"></a><span data-ttu-id="d8529-108">Tulajdonságok</span><span class="sxs-lookup"><span data-stu-id="d8529-108">Properties</span></span>

|  <span data-ttu-id="d8529-109">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="d8529-109">Property</span></span>  |  <span data-ttu-id="d8529-110">Leírás</span><span class="sxs-lookup"><span data-stu-id="d8529-110">Description</span></span>   |
|---|---|
| <span data-ttu-id="d8529-111">ResourceName</span><span class="sxs-lookup"><span data-stu-id="d8529-111">ResourceName</span></span>| <span data-ttu-id="d8529-112">Az erőforrásnév függenek.</span><span class="sxs-lookup"><span data-stu-id="d8529-112">The resource name to depend on.</span></span> <span data-ttu-id="d8529-113">Ha az erőforrás tartozik egy másik konfigurációs, formázhatja a nevet a következőként "[__ResourceType__]__ResourceName__:: [__ConfigurationName__]:: [ __ConfigurationName__] "</span><span class="sxs-lookup"><span data-stu-id="d8529-113">If this resource belongs to a different configuration, format the name as "[__ResourceType__]__ResourceName__::[__ConfigurationName__]::[__ConfigurationName__]"</span></span>|
| <span data-ttu-id="d8529-114">Csomópontnév</span><span class="sxs-lookup"><span data-stu-id="d8529-114">NodeName</span></span>| <span data-ttu-id="d8529-115">Az erőforrás függenek a célcsomópontokat.</span><span class="sxs-lookup"><span data-stu-id="d8529-115">The target nodes of the resource to depend on.</span></span>|
| <span data-ttu-id="d8529-116">RetryIntervalSec</span><span class="sxs-lookup"><span data-stu-id="d8529-116">RetryIntervalSec</span></span>| <span data-ttu-id="d8529-117">Mielőtt újra próbálkozna másodpercek számát.</span><span class="sxs-lookup"><span data-stu-id="d8529-117">The number of seconds before retrying.</span></span> <span data-ttu-id="d8529-118">Minimális érték 1.</span><span class="sxs-lookup"><span data-stu-id="d8529-118">Minimum is 1.</span></span>|
| <span data-ttu-id="d8529-119">RetryCount</span><span class="sxs-lookup"><span data-stu-id="d8529-119">RetryCount</span></span>| <span data-ttu-id="d8529-120">Az újrapróbálkozások maximális száma.</span><span class="sxs-lookup"><span data-stu-id="d8529-120">The maximum number of times to retry.</span></span>|
| <span data-ttu-id="d8529-121">ThrottleLimit</span><span class="sxs-lookup"><span data-stu-id="d8529-121">ThrottleLimit</span></span>| <span data-ttu-id="d8529-122">Egyidejű csatlakozás gépek száma.</span><span class="sxs-lookup"><span data-stu-id="d8529-122">Number of machines to connect simultaneously.</span></span> <span data-ttu-id="d8529-123">Alapértelmezés szerint új cimsession alapértelmezett.</span><span class="sxs-lookup"><span data-stu-id="d8529-123">Default is new-cimsession default.</span></span>|
| <span data-ttu-id="d8529-124">DependsOn</span><span class="sxs-lookup"><span data-stu-id="d8529-124">DependsOn</span></span> | <span data-ttu-id="d8529-125">Azt jelzi, hogy a konfigurációt egy másik erőforrás futtatnia kell, mielőtt az erőforrás konfigurálva van.</span><span class="sxs-lookup"><span data-stu-id="d8529-125">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="d8529-126">Például, ha az erőforrás-konfiguráció azonosítója letiltása, a futtatni kívánt parancsfájl először van __ResourceName__ és a típusa __ResourceType__, ez a tulajdonság használata esetén `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="d8529-126">For example, if the ID of the resource configuration script block that you want to run first is __ResourceName__ and its type is __ResourceType__, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|

## <a name="example"></a><span data-ttu-id="d8529-127">Példa</span><span class="sxs-lookup"><span data-stu-id="d8529-127">Example</span></span>

<span data-ttu-id="d8529-128">Egy példa bemutatja, hogyan használhatja ezt az erőforrást: [csomópontok közötti függőségek megadása](../../../configurations/crossNodeDependencies.md)</span><span class="sxs-lookup"><span data-stu-id="d8529-128">For an example of how to use this resource, see [Specifying cross-node dependencies](../../../configurations/crossNodeDependencies.md)</span></span>
