---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "A DSC WaitForAll erőforrás"
ms.openlocfilehash: dcc23ad4e6905bc277ad39348350d5425fc90ad7
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2017
---
# <a name="dsc-waitforall-resource"></a><span data-ttu-id="ae1d5-103">A DSC WaitForAll erőforrás</span><span class="sxs-lookup"><span data-stu-id="ae1d5-103">DSC WaitForAll Resource</span></span>

> <span data-ttu-id="ae1d5-104">Vonatkozik: A Windows PowerShell 5.0-s és újabb verziók</span><span class="sxs-lookup"><span data-stu-id="ae1d5-104">Applies To: Windows PowerShell 5.0 and later</span></span>

<span data-ttu-id="ae1d5-105">A **WaitForAll** kívánt állapot konfigurációs szolgáltatása (DSC) erőforrás használhatja egy csomópont blokkja egy [DSC-konfiguráció](configurations.md) függőségek konfigurációk létrehozáskor határozza meg.</span><span class="sxs-lookup"><span data-stu-id="ae1d5-105">The **WaitForAll** Desired State Configuration (DSC) resource can be used within a node block in a [DSC configuration](configurations.md) to specify dependencies on configurations on other nodes.</span></span>

<span data-ttu-id="ae1d5-106">Ehhez az erőforráshoz sikeres lesz, ha az erőforrás által megadott Ha a **ResourceName** tulajdonság definiált összes cél csomóponton megfelelő állapotban van a **csomópontnév** tulajdonság.</span><span class="sxs-lookup"><span data-stu-id="ae1d5-106">This resource succeeds if if the resource specified by the **ResourceName** property is in the desired state on all target nodes defined in the **NodeName** property.</span></span>


## <a name="syntax"></a><span data-ttu-id="ae1d5-107">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="ae1d5-107">Syntax</span></span>

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

## <a name="properties"></a><span data-ttu-id="ae1d5-108">Tulajdonságok</span><span class="sxs-lookup"><span data-stu-id="ae1d5-108">Properties</span></span>

|  <span data-ttu-id="ae1d5-109">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="ae1d5-109">Property</span></span>  |  <span data-ttu-id="ae1d5-110">Leírás</span><span class="sxs-lookup"><span data-stu-id="ae1d5-110">Description</span></span>   | 
|---|---| 
| <span data-ttu-id="ae1d5-111">resourceName</span><span class="sxs-lookup"><span data-stu-id="ae1d5-111">ResourceName</span></span>| <span data-ttu-id="ae1d5-112">Az erőforrásnév függ.</span><span class="sxs-lookup"><span data-stu-id="ae1d5-112">The resource name to depend on.</span></span>| 
| <span data-ttu-id="ae1d5-113">Csomópontnév</span><span class="sxs-lookup"><span data-stu-id="ae1d5-113">NodeName</span></span>| <span data-ttu-id="ae1d5-114">Az erőforrás függ a célcsomópontokat.</span><span class="sxs-lookup"><span data-stu-id="ae1d5-114">The target nodes of the resource to depend on.</span></span>| 
| <span data-ttu-id="ae1d5-115">RetryIntervalSec</span><span class="sxs-lookup"><span data-stu-id="ae1d5-115">RetryIntervalSec</span></span>| <span data-ttu-id="ae1d5-116">Másodpercig az újrapróbálkozás előtt száma.</span><span class="sxs-lookup"><span data-stu-id="ae1d5-116">The number of seconds before retrying.</span></span> <span data-ttu-id="ae1d5-117">Minimális érték 1.</span><span class="sxs-lookup"><span data-stu-id="ae1d5-117">Minimum is 1.</span></span>| 
| <span data-ttu-id="ae1d5-118">a retryCount</span><span class="sxs-lookup"><span data-stu-id="ae1d5-118">RetryCount</span></span>| <span data-ttu-id="ae1d5-119">A próbálkozások maximális számát.</span><span class="sxs-lookup"><span data-stu-id="ae1d5-119">The maximum number of times to retry.</span></span>| 
| <span data-ttu-id="ae1d5-120">ThrottleLimit</span><span class="sxs-lookup"><span data-stu-id="ae1d5-120">ThrottleLimit</span></span>| <span data-ttu-id="ae1d5-121">Az egyidejű csatlakozást a gépek számát.</span><span class="sxs-lookup"><span data-stu-id="ae1d5-121">Number of machines to connect simultaneously.</span></span> <span data-ttu-id="ae1d5-122">Alapértelmezés szerint új-cimsession alapértelmezett.</span><span class="sxs-lookup"><span data-stu-id="ae1d5-122">Default is new-cimsession default.</span></span>| 
| <span data-ttu-id="ae1d5-123">dependsOn</span><span class="sxs-lookup"><span data-stu-id="ae1d5-123">DependsOn</span></span> | <span data-ttu-id="ae1d5-124">Azt jelzi, hogy egy másik erőforrás konfigurációjának kell futtatni, mielőtt ehhez az erőforráshoz van konfigurálva.</span><span class="sxs-lookup"><span data-stu-id="ae1d5-124">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="ae1d5-125">Például, ha az erőforrás-konfiguráció azonosítója blokk futtatni kívánt parancsfájl első az __ResourceName__ és annak típusa __ResourceType__, az e tulajdonság használatával szintaxisa a következő `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="ae1d5-125">For example, if the ID of the resource configuration script block that you want to run first is __ResourceName__ and its type is __ResourceType__, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|


## <a name="example"></a><span data-ttu-id="ae1d5-126">Példa</span><span class="sxs-lookup"><span data-stu-id="ae1d5-126">Example</span></span>

<span data-ttu-id="ae1d5-127">Példa bemutatja, hogyan az erőforrás, lásd: [cross-csomópont függőségeinek megadása](crossNodeDependencies.md)</span><span class="sxs-lookup"><span data-stu-id="ae1d5-127">For an example of how to use this resource, see [Specifying cross-node dependencies](crossNodeDependencies.md)</span></span>

