---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "A DSC WaitForSome erőforrás"
ms.openlocfilehash: cbe16c543f0eeb62dbe1fb439af2f9147f1bc210
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 01/17/2018
---
# <a name="dsc-waitforsome-resource"></a><span data-ttu-id="0ba1a-103">A DSC WaitForSome erőforrás</span><span class="sxs-lookup"><span data-stu-id="0ba1a-103">DSC WaitForSome Resource</span></span>

> <span data-ttu-id="0ba1a-104">Vonatkozik: A Windows PowerShell 5.0-s és újabb verziók</span><span class="sxs-lookup"><span data-stu-id="0ba1a-104">Applies To: Windows PowerShell 5.0 and later</span></span>

<span data-ttu-id="0ba1a-105">A **WaitForAny** kívánt állapot konfigurációs szolgáltatása (DSC) erőforrás használhatja egy csomópont blokkja egy [DSC-konfiguráció](configurations.md) függőségek konfigurációk létrehozáskor határozza meg.</span><span class="sxs-lookup"><span data-stu-id="0ba1a-105">The **WaitForAny** Desired State Configuration (DSC) resource can be used within a node block in a [DSC configuration](configurations.md) to specify dependencies on configurations on other nodes.</span></span>

<span data-ttu-id="0ba1a-106">Ehhez az erőforráshoz sikeres lesz, ha az erőforrás által megadott a **ResourceName** tulajdonság szerepel a kívánt állapot, a csomópontok minimális száma (által megadott **NodeCount**) határozzák meg a **csomópontnév**  tulajdonság.</span><span class="sxs-lookup"><span data-stu-id="0ba1a-106">This resource succeeds if the resource specified by the **ResourceName** property is in the desired state on a minimum number of nodes (specified by **NodeCount**) defined by the **NodeName** property.</span></span> 


## <a name="syntax"></a><span data-ttu-id="0ba1a-107">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="0ba1a-107">Syntax</span></span>

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

## <a name="properties"></a><span data-ttu-id="0ba1a-108">Tulajdonságok</span><span class="sxs-lookup"><span data-stu-id="0ba1a-108">Properties</span></span>

|  <span data-ttu-id="0ba1a-109">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="0ba1a-109">Property</span></span>  |  <span data-ttu-id="0ba1a-110">Leírás</span><span class="sxs-lookup"><span data-stu-id="0ba1a-110">Description</span></span>   | 
|---|---| 
| <span data-ttu-id="0ba1a-111">NodeCount</span><span class="sxs-lookup"><span data-stu-id="0ba1a-111">NodeCount</span></span>| <span data-ttu-id="0ba1a-112">Ehhez az erőforráshoz sikeres megfelelő állapotban kell lennie csomópontok minimális száma.</span><span class="sxs-lookup"><span data-stu-id="0ba1a-112">The minimum number of nodes that must be in the desired state for this resource to succeed.</span></span>|
| <span data-ttu-id="0ba1a-113">Csomópontnév</span><span class="sxs-lookup"><span data-stu-id="0ba1a-113">NodeName</span></span>| <span data-ttu-id="0ba1a-114">Az erőforrás függ a célcsomópontokat.</span><span class="sxs-lookup"><span data-stu-id="0ba1a-114">The target nodes of the resource to depend on.</span></span>| 
| <span data-ttu-id="0ba1a-115">resourceName</span><span class="sxs-lookup"><span data-stu-id="0ba1a-115">ResourceName</span></span>| <span data-ttu-id="0ba1a-116">Az erőforrásnév függ.</span><span class="sxs-lookup"><span data-stu-id="0ba1a-116">The resource name to depend on.</span></span>| 
| <span data-ttu-id="0ba1a-117">RetryIntervalSec</span><span class="sxs-lookup"><span data-stu-id="0ba1a-117">RetryIntervalSec</span></span>| <span data-ttu-id="0ba1a-118">Másodpercig az újrapróbálkozás előtt száma.</span><span class="sxs-lookup"><span data-stu-id="0ba1a-118">The number of seconds before retrying.</span></span> <span data-ttu-id="0ba1a-119">Minimális érték 1.</span><span class="sxs-lookup"><span data-stu-id="0ba1a-119">Minimum is 1.</span></span>| 
| <span data-ttu-id="0ba1a-120">a retryCount</span><span class="sxs-lookup"><span data-stu-id="0ba1a-120">RetryCount</span></span>| <span data-ttu-id="0ba1a-121">A próbálkozások maximális számát.</span><span class="sxs-lookup"><span data-stu-id="0ba1a-121">The maximum number of times to retry.</span></span>| 
| <span data-ttu-id="0ba1a-122">ThrottleLimit</span><span class="sxs-lookup"><span data-stu-id="0ba1a-122">ThrottleLimit</span></span>| <span data-ttu-id="0ba1a-123">Az egyidejű csatlakozást a gépek számát.</span><span class="sxs-lookup"><span data-stu-id="0ba1a-123">Number of machines to connect simultaneously.</span></span> <span data-ttu-id="0ba1a-124">Alapértelmezés szerint új-cimsession alapértelmezett.</span><span class="sxs-lookup"><span data-stu-id="0ba1a-124">Default is new-cimsession default.</span></span>| 
| <span data-ttu-id="0ba1a-125">dependsOn</span><span class="sxs-lookup"><span data-stu-id="0ba1a-125">DependsOn</span></span> | <span data-ttu-id="0ba1a-126">Azt jelzi, hogy egy másik erőforrás konfigurációjának kell futtatni, mielőtt ehhez az erőforráshoz van konfigurálva.</span><span class="sxs-lookup"><span data-stu-id="0ba1a-126">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="0ba1a-127">Például, ha az erőforrás-konfiguráció azonosítója blokk futtatni kívánt parancsfájl első az __ResourceName__ és annak típusa __ResourceType__, az e tulajdonság használatával szintaxisa a következő `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="0ba1a-127">For example, if the ID of the resource configuration script block that you want to run first is __ResourceName__ and its type is __ResourceType__, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|
| <span data-ttu-id="0ba1a-128">PsDscRunAsCredential</span><span class="sxs-lookup"><span data-stu-id="0ba1a-128">PsDscRunAsCredential</span></span> | <span data-ttu-id="0ba1a-129">Lásd: [DSC hitelesítő adatokkal rendelkező felhasználó](https://docs.microsoft.com/en-us/powershell/dsc/runasuser)</span><span class="sxs-lookup"><span data-stu-id="0ba1a-129">See [Using DSC with User Credentials](https://docs.microsoft.com/en-us/powershell/dsc/runasuser)</span></span> |


## <a name="example"></a><span data-ttu-id="0ba1a-130">Példa</span><span class="sxs-lookup"><span data-stu-id="0ba1a-130">Example</span></span>

<span data-ttu-id="0ba1a-131">Példa bemutatja, hogyan az erőforrás, lásd: [cross-csomópont függőségeinek megadása](crossNodeDependencies.md)</span><span class="sxs-lookup"><span data-stu-id="0ba1a-131">For an example of how to use this resource, see [Specifying cross-node dependencies](crossNodeDependencies.md)</span></span>

