---
ms.date: 06/12/2017
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: A DSC WaitForSome erőforrás
ms.openlocfilehash: 08a5b96bee0b1b4475470e0d857dca79dee2b02e
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/16/2018
---
# <a name="dsc-waitforsome-resource"></a><span data-ttu-id="9841b-103">A DSC WaitForSome erőforrás</span><span class="sxs-lookup"><span data-stu-id="9841b-103">DSC WaitForSome Resource</span></span>

> <span data-ttu-id="9841b-104">Vonatkozik: A Windows PowerShell 5.0-s és újabb verziók</span><span class="sxs-lookup"><span data-stu-id="9841b-104">Applies To: Windows PowerShell 5.0 and later</span></span>

<span data-ttu-id="9841b-105">A **WaitForAny** kívánt állapot konfigurációs szolgáltatása (DSC) erőforrás használhatja egy csomópont blokkja egy [DSC-konfiguráció](configurations.md) függőségek konfigurációk létrehozáskor határozza meg.</span><span class="sxs-lookup"><span data-stu-id="9841b-105">The **WaitForAny** Desired State Configuration (DSC) resource can be used within a node block in a [DSC configuration](configurations.md) to specify dependencies on configurations on other nodes.</span></span>

<span data-ttu-id="9841b-106">Ehhez az erőforráshoz sikeres lesz, ha az erőforrás által megadott a **ResourceName** tulajdonság szerepel a kívánt állapot, a csomópontok minimális száma (által megadott **NodeCount**) határozzák meg a **csomópontnév**  tulajdonság.</span><span class="sxs-lookup"><span data-stu-id="9841b-106">This resource succeeds if the resource specified by the **ResourceName** property is in the desired state on a minimum number of nodes (specified by **NodeCount**) defined by the **NodeName** property.</span></span>


## <a name="syntax"></a><span data-ttu-id="9841b-107">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="9841b-107">Syntax</span></span>

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

## <a name="properties"></a><span data-ttu-id="9841b-108">Tulajdonságok</span><span class="sxs-lookup"><span data-stu-id="9841b-108">Properties</span></span>

|  <span data-ttu-id="9841b-109">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="9841b-109">Property</span></span>  |  <span data-ttu-id="9841b-110">Leírás</span><span class="sxs-lookup"><span data-stu-id="9841b-110">Description</span></span>   |
|---|---|
| <span data-ttu-id="9841b-111">NodeCount</span><span class="sxs-lookup"><span data-stu-id="9841b-111">NodeCount</span></span>| <span data-ttu-id="9841b-112">Ehhez az erőforráshoz sikeres megfelelő állapotban kell lennie csomópontok minimális száma.</span><span class="sxs-lookup"><span data-stu-id="9841b-112">The minimum number of nodes that must be in the desired state for this resource to succeed.</span></span>|
| <span data-ttu-id="9841b-113">Csomópontnév</span><span class="sxs-lookup"><span data-stu-id="9841b-113">NodeName</span></span>| <span data-ttu-id="9841b-114">Az erőforrás függ a célcsomópontokat.</span><span class="sxs-lookup"><span data-stu-id="9841b-114">The target nodes of the resource to depend on.</span></span>|
| <span data-ttu-id="9841b-115">resourceName</span><span class="sxs-lookup"><span data-stu-id="9841b-115">ResourceName</span></span>| <span data-ttu-id="9841b-116">Az erőforrásnév függ.</span><span class="sxs-lookup"><span data-stu-id="9841b-116">The resource name to depend on.</span></span> <span data-ttu-id="9841b-117">Ha egy másik konfigurációs ehhez az erőforráshoz tartozik, a neve, ahogyan formázása "[__ResourceType__]__ResourceName__:: [__ConfigurationName__]:: [ __ConfigurationName__] "</span><span class="sxs-lookup"><span data-stu-id="9841b-117">If this resource belongs to a different configuration, format the name as "[__ResourceType__]__ResourceName__::[__ConfigurationName__]::[__ConfigurationName__]"</span></span>|
| <span data-ttu-id="9841b-118">RetryIntervalSec</span><span class="sxs-lookup"><span data-stu-id="9841b-118">RetryIntervalSec</span></span>| <span data-ttu-id="9841b-119">Másodpercig az újrapróbálkozás előtt száma.</span><span class="sxs-lookup"><span data-stu-id="9841b-119">The number of seconds before retrying.</span></span> <span data-ttu-id="9841b-120">Minimális érték 1.</span><span class="sxs-lookup"><span data-stu-id="9841b-120">Minimum is 1.</span></span>|
| <span data-ttu-id="9841b-121">a retryCount</span><span class="sxs-lookup"><span data-stu-id="9841b-121">RetryCount</span></span>| <span data-ttu-id="9841b-122">A próbálkozások maximális számát.</span><span class="sxs-lookup"><span data-stu-id="9841b-122">The maximum number of times to retry.</span></span>|
| <span data-ttu-id="9841b-123">ThrottleLimit</span><span class="sxs-lookup"><span data-stu-id="9841b-123">ThrottleLimit</span></span>| <span data-ttu-id="9841b-124">Az egyidejű csatlakozást a gépek számát.</span><span class="sxs-lookup"><span data-stu-id="9841b-124">Number of machines to connect simultaneously.</span></span> <span data-ttu-id="9841b-125">Alapértelmezés szerint új-cimsession alapértelmezett.</span><span class="sxs-lookup"><span data-stu-id="9841b-125">Default is new-cimsession default.</span></span>|
| <span data-ttu-id="9841b-126">dependsOn</span><span class="sxs-lookup"><span data-stu-id="9841b-126">DependsOn</span></span> | <span data-ttu-id="9841b-127">Azt jelzi, hogy egy másik erőforrás konfigurációjának kell futtatni, mielőtt ehhez az erőforráshoz van konfigurálva.</span><span class="sxs-lookup"><span data-stu-id="9841b-127">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="9841b-128">Például, ha az erőforrás-konfiguráció azonosítója blokk futtatni kívánt parancsfájl első az __ResourceName__ és annak típusa __ResourceType__, az e tulajdonság használatával szintaxisa a következő `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="9841b-128">For example, if the ID of the resource configuration script block that you want to run first is __ResourceName__ and its type is __ResourceType__, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|
| <span data-ttu-id="9841b-129">PsDscRunAsCredential</span><span class="sxs-lookup"><span data-stu-id="9841b-129">PsDscRunAsCredential</span></span> | <span data-ttu-id="9841b-130">Lásd: [DSC hitelesítő adatokkal rendelkező felhasználó](https://docs.microsoft.com/powershell/dsc/runasuser)</span><span class="sxs-lookup"><span data-stu-id="9841b-130">See [Using DSC with User Credentials](https://docs.microsoft.com/powershell/dsc/runasuser)</span></span> |


## <a name="example"></a><span data-ttu-id="9841b-131">Példa</span><span class="sxs-lookup"><span data-stu-id="9841b-131">Example</span></span>

<span data-ttu-id="9841b-132">Példa bemutatja, hogyan az erőforrás, lásd: [cross-csomópont függőségeinek megadása](crossNodeDependencies.md)</span><span class="sxs-lookup"><span data-stu-id="9841b-132">For an example of how to use this resource, see [Specifying cross-node dependencies](crossNodeDependencies.md)</span></span>