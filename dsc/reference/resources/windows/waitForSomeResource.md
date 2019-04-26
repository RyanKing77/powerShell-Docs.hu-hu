---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: DSC WaitForSome Resource
ms.openlocfilehash: 888da1810f0a9233579bad5eef8d5dd556947c61
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62076854"
---
# <a name="dsc-waitforsome-resource"></a><span data-ttu-id="34940-103">DSC WaitForSome Resource</span><span class="sxs-lookup"><span data-stu-id="34940-103">DSC WaitForSome Resource</span></span>

> <span data-ttu-id="34940-104">A következőkre vonatkozik: Windows PowerShell 5.0-s és újabb verziók</span><span class="sxs-lookup"><span data-stu-id="34940-104">Applies To: Windows PowerShell 5.0 and later</span></span>

<span data-ttu-id="34940-105">A **WaitForSome** egy csomópont letiltása a Desired State Configuration (DSC) erőforrás használható egy [DSC-konfiguráció](../../../configurations/configurations.md) függőségeinek megadása a konfigurációk a többi csomóponton.</span><span class="sxs-lookup"><span data-stu-id="34940-105">The **WaitForSome** Desired State Configuration (DSC) resource can be used within a node block in a [DSC configuration](../../../configurations/configurations.md) to specify dependencies on configurations on other nodes.</span></span>

<span data-ttu-id="34940-106">Ehhez az erőforráshoz sikeres lesz, abban az esetben, ha az erőforrás által meghatározott a **ResourceName** tulajdonság a kívánt állapotban lévő csomópontok minimális száma (által megadott **NodeCount**) által meghatározott a **csomópontnév**  tulajdonság.</span><span class="sxs-lookup"><span data-stu-id="34940-106">This resource succeeds if the resource specified by the **ResourceName** property is in the desired state on a minimum number of nodes (specified by **NodeCount**) defined by the **NodeName** property.</span></span>


## <a name="syntax"></a><span data-ttu-id="34940-107">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="34940-107">Syntax</span></span>

```
WaitForSome [String] #ResourceName
{
    NodeCount = [UInt32]
    NodeName = [string[]]
    ResourceName = [string]
    [DependsOn = [string[]]]
    [PsDscRunAsCredential = [PSCredential]]
    [RetryCount = [UInt32]]
    [RetryIntervalSec = [UInt64]]
    [ThrottleLimit = [UInt32]]
}
```

## <a name="properties"></a><span data-ttu-id="34940-108">Tulajdonságok</span><span class="sxs-lookup"><span data-stu-id="34940-108">Properties</span></span>

|  <span data-ttu-id="34940-109">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="34940-109">Property</span></span>  |  <span data-ttu-id="34940-110">Leírás</span><span class="sxs-lookup"><span data-stu-id="34940-110">Description</span></span>   |
|---|---|
| <span data-ttu-id="34940-111">NodeCount</span><span class="sxs-lookup"><span data-stu-id="34940-111">NodeCount</span></span>| <span data-ttu-id="34940-112">Ehhez az erőforráshoz sikeres a kívánt állapotban kell lennie csomópontok minimális száma.</span><span class="sxs-lookup"><span data-stu-id="34940-112">The minimum number of nodes that must be in the desired state for this resource to succeed.</span></span>|
| <span data-ttu-id="34940-113">Csomópontnév</span><span class="sxs-lookup"><span data-stu-id="34940-113">NodeName</span></span>| <span data-ttu-id="34940-114">Az erőforrás függenek a célcsomópontokat.</span><span class="sxs-lookup"><span data-stu-id="34940-114">The target nodes of the resource to depend on.</span></span>|
| <span data-ttu-id="34940-115">ResourceName</span><span class="sxs-lookup"><span data-stu-id="34940-115">ResourceName</span></span>| <span data-ttu-id="34940-116">Az erőforrásnév függenek.</span><span class="sxs-lookup"><span data-stu-id="34940-116">The resource name to depend on.</span></span> <span data-ttu-id="34940-117">Ha az erőforrás tartozik egy másik konfigurációs, formázhatja a nevet a következőként "[__ResourceType__]__ResourceName__:: [__ConfigurationName__]:: [ __ConfigurationName__] "</span><span class="sxs-lookup"><span data-stu-id="34940-117">If this resource belongs to a different configuration, format the name as "[__ResourceType__]__ResourceName__::[__ConfigurationName__]::[__ConfigurationName__]"</span></span>|
| <span data-ttu-id="34940-118">RetryIntervalSec</span><span class="sxs-lookup"><span data-stu-id="34940-118">RetryIntervalSec</span></span>| <span data-ttu-id="34940-119">Mielőtt újra próbálkozna másodpercek számát.</span><span class="sxs-lookup"><span data-stu-id="34940-119">The number of seconds before retrying.</span></span> <span data-ttu-id="34940-120">Minimális érték 1.</span><span class="sxs-lookup"><span data-stu-id="34940-120">Minimum is 1.</span></span>|
| <span data-ttu-id="34940-121">RetryCount</span><span class="sxs-lookup"><span data-stu-id="34940-121">RetryCount</span></span>| <span data-ttu-id="34940-122">Az újrapróbálkozások maximális száma.</span><span class="sxs-lookup"><span data-stu-id="34940-122">The maximum number of times to retry.</span></span>|
| <span data-ttu-id="34940-123">ThrottleLimit</span><span class="sxs-lookup"><span data-stu-id="34940-123">ThrottleLimit</span></span>| <span data-ttu-id="34940-124">Egyidejű csatlakozás gépek száma.</span><span class="sxs-lookup"><span data-stu-id="34940-124">Number of machines to connect simultaneously.</span></span> <span data-ttu-id="34940-125">Alapértelmezés szerint új cimsession alapértelmezett.</span><span class="sxs-lookup"><span data-stu-id="34940-125">Default is new-cimsession default.</span></span>|
| <span data-ttu-id="34940-126">DependsOn</span><span class="sxs-lookup"><span data-stu-id="34940-126">DependsOn</span></span> | <span data-ttu-id="34940-127">Azt jelzi, hogy a konfigurációt egy másik erőforrás futtatnia kell, mielőtt az erőforrás konfigurálva van.</span><span class="sxs-lookup"><span data-stu-id="34940-127">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="34940-128">Például, ha az erőforrás-konfiguráció azonosítója letiltása, a futtatni kívánt parancsfájl először van __ResourceName__ és a típusa __ResourceType__, ez a tulajdonság használata esetén `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="34940-128">For example, if the ID of the resource configuration script block that you want to run first is __ResourceName__ and its type is __ResourceType__, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|
| <span data-ttu-id="34940-129">PsDscRunAsCredential</span><span class="sxs-lookup"><span data-stu-id="34940-129">PsDscRunAsCredential</span></span> | <span data-ttu-id="34940-130">Lásd: [DSC használata a felhasználói hitelesítő adatok](https://docs.microsoft.com/powershell/dsc/runasuser)</span><span class="sxs-lookup"><span data-stu-id="34940-130">See [Using DSC with User Credentials](https://docs.microsoft.com/powershell/dsc/runasuser)</span></span> |

## <a name="example"></a><span data-ttu-id="34940-131">Példa</span><span class="sxs-lookup"><span data-stu-id="34940-131">Example</span></span>

<span data-ttu-id="34940-132">Egy példa bemutatja, hogyan használhatja ezt az erőforrást: [csomópontok közötti függőségek megadása](../../../configurations/crossNodeDependencies.md)</span><span class="sxs-lookup"><span data-stu-id="34940-132">For an example of how to use this resource, see [Specifying cross-node dependencies](../../../configurations/crossNodeDependencies.md)</span></span>
