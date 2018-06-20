---
ms.date: 06/12/2017
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: A DSC WaitForAny erőforrás
ms.openlocfilehash: c9700c908f8601db85f9c922445969a34b59d453
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/16/2018
ms.locfileid: "34186711"
---
# <a name="dsc-waitforany-resource"></a><span data-ttu-id="5f741-103">A DSC WaitForAny erőforrás</span><span class="sxs-lookup"><span data-stu-id="5f741-103">DSC WaitForAny Resource</span></span>

> <span data-ttu-id="5f741-104">Vonatkozik: A Windows PowerShell 5.1-es és újabb verziók</span><span class="sxs-lookup"><span data-stu-id="5f741-104">Applies To: Windows PowerShell 5.1 and later</span></span>

<span data-ttu-id="5f741-105">A **WaitForSome** kívánt állapot konfigurációs szolgáltatása (DSC) erőforrás használhatja egy csomópont blokkja egy [DSC-konfiguráció](configurations.md) függőségek konfigurációk létrehozáskor határozza meg.</span><span class="sxs-lookup"><span data-stu-id="5f741-105">The **WaitForSome** Desired State Configuration (DSC) resource can be used within a node block in a [DSC configuration](configurations.md) to specify dependencies on configurations on other nodes.</span></span>

<span data-ttu-id="5f741-106">Ehhez az erőforráshoz sikeres lesz, ha az erőforrás által megadott Ha a **ResourceName** tulajdonság a bármilyen definiált célcsomópontokat megfelelő állapotban van a **csomópontnév** tulajdonság.</span><span class="sxs-lookup"><span data-stu-id="5f741-106">This resource succeeds if if the resource specified by the **ResourceName** property is in the desired state on any target nodes defined in the **NodeName** property.</span></span>


## <a name="syntax"></a><span data-ttu-id="5f741-107">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="5f741-107">Syntax</span></span>

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

## <a name="properties"></a><span data-ttu-id="5f741-108">Tulajdonságok</span><span class="sxs-lookup"><span data-stu-id="5f741-108">Properties</span></span>

|  <span data-ttu-id="5f741-109">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="5f741-109">Property</span></span>  |  <span data-ttu-id="5f741-110">Leírás</span><span class="sxs-lookup"><span data-stu-id="5f741-110">Description</span></span>   |
|---|---|
| <span data-ttu-id="5f741-111">resourceName</span><span class="sxs-lookup"><span data-stu-id="5f741-111">ResourceName</span></span>| <span data-ttu-id="5f741-112">Az erőforrásnév függ.</span><span class="sxs-lookup"><span data-stu-id="5f741-112">The resource name to depend on.</span></span> <span data-ttu-id="5f741-113">Ha egy másik konfigurációs ehhez az erőforráshoz tartozik, a neve, ahogyan formázása "[__ResourceType__]__ResourceName__:: [__ConfigurationName__]:: [ __ConfigurationName__] "</span><span class="sxs-lookup"><span data-stu-id="5f741-113">If this resource belongs to a different configuration, format the name as "[__ResourceType__]__ResourceName__::[__ConfigurationName__]::[__ConfigurationName__]"</span></span>|
| <span data-ttu-id="5f741-114">Csomópontnév</span><span class="sxs-lookup"><span data-stu-id="5f741-114">NodeName</span></span>| <span data-ttu-id="5f741-115">Az erőforrás függ a célcsomópontokat.</span><span class="sxs-lookup"><span data-stu-id="5f741-115">The target nodes of the resource to depend on.</span></span>|
| <span data-ttu-id="5f741-116">RetryIntervalSec</span><span class="sxs-lookup"><span data-stu-id="5f741-116">RetryIntervalSec</span></span>| <span data-ttu-id="5f741-117">Másodpercig az újrapróbálkozás előtt száma.</span><span class="sxs-lookup"><span data-stu-id="5f741-117">The number of seconds before retrying.</span></span> <span data-ttu-id="5f741-118">Minimális érték 1.</span><span class="sxs-lookup"><span data-stu-id="5f741-118">Minimum is 1.</span></span>|
| <span data-ttu-id="5f741-119">a retryCount</span><span class="sxs-lookup"><span data-stu-id="5f741-119">RetryCount</span></span>| <span data-ttu-id="5f741-120">A próbálkozások maximális számát.</span><span class="sxs-lookup"><span data-stu-id="5f741-120">The maximum number of times to retry.</span></span>|
| <span data-ttu-id="5f741-121">ThrottleLimit</span><span class="sxs-lookup"><span data-stu-id="5f741-121">ThrottleLimit</span></span>| <span data-ttu-id="5f741-122">Az egyidejű csatlakozást a gépek számát.</span><span class="sxs-lookup"><span data-stu-id="5f741-122">Number of machines to connect simultaneously.</span></span> <span data-ttu-id="5f741-123">Alapértelmezés szerint új-cimsession alapértelmezett.</span><span class="sxs-lookup"><span data-stu-id="5f741-123">Default is new-cimsession default.</span></span>|
| <span data-ttu-id="5f741-124">dependsOn</span><span class="sxs-lookup"><span data-stu-id="5f741-124">DependsOn</span></span> | <span data-ttu-id="5f741-125">Azt jelzi, hogy egy másik erőforrás konfigurációjának kell futtatni, mielőtt ehhez az erőforráshoz van konfigurálva.</span><span class="sxs-lookup"><span data-stu-id="5f741-125">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="5f741-126">Például, ha az erőforrás-konfiguráció azonosítója blokk futtatni kívánt parancsfájl első az __ResourceName__ és annak típusa __ResourceType__, az e tulajdonság használatával szintaxisa a következő `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="5f741-126">For example, if the ID of the resource configuration script block that you want to run first is __ResourceName__ and its type is __ResourceType__, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|


## <a name="example"></a><span data-ttu-id="5f741-127">Példa</span><span class="sxs-lookup"><span data-stu-id="5f741-127">Example</span></span>

<span data-ttu-id="5f741-128">Példa bemutatja, hogyan az erőforrás, lásd: [cross-csomópont függőségeinek megadása](crossNodeDependencies.md)</span><span class="sxs-lookup"><span data-stu-id="5f741-128">For an example of how to use this resource, see [Specifying cross-node dependencies](crossNodeDependencies.md)</span></span>