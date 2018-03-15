---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "A DSC WaitForAll erőforrás"
ms.openlocfilehash: 2b6d9e11acd429eecb30926316d1033331524edc
ms.sourcegitcommit: 99227f62dcf827354770eb2c3e95c5cf6a3118b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/15/2018
---
# <a name="dsc-waitforall-resource"></a><span data-ttu-id="c3c8c-103">A DSC WaitForAll erőforrás</span><span class="sxs-lookup"><span data-stu-id="c3c8c-103">DSC WaitForAll Resource</span></span>

> <span data-ttu-id="c3c8c-104">Vonatkozik: A Windows PowerShell 5.0-s és újabb verziók</span><span class="sxs-lookup"><span data-stu-id="c3c8c-104">Applies To: Windows PowerShell 5.0 and later</span></span>

<span data-ttu-id="c3c8c-105">A **WaitForAll** kívánt állapot konfigurációs szolgáltatása (DSC) erőforrás használhatja egy csomópont blokkja egy [DSC-konfiguráció](configurations.md) függőségek konfigurációk létrehozáskor határozza meg.</span><span class="sxs-lookup"><span data-stu-id="c3c8c-105">The **WaitForAll** Desired State Configuration (DSC) resource can be used within a node block in a [DSC configuration](configurations.md) to specify dependencies on configurations on other nodes.</span></span>

<span data-ttu-id="c3c8c-106">Ehhez az erőforráshoz sikeres lesz, ha az erőforrás által megadott Ha a **ResourceName** tulajdonság definiált összes cél csomóponton megfelelő állapotban van a **csomópontnév** tulajdonság.</span><span class="sxs-lookup"><span data-stu-id="c3c8c-106">This resource succeeds if if the resource specified by the **ResourceName** property is in the desired state on all target nodes defined in the **NodeName** property.</span></span>


## <a name="syntax"></a><span data-ttu-id="c3c8c-107">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="c3c8c-107">Syntax</span></span>

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

## <a name="properties"></a><span data-ttu-id="c3c8c-108">Tulajdonságok</span><span class="sxs-lookup"><span data-stu-id="c3c8c-108">Properties</span></span>

|  <span data-ttu-id="c3c8c-109">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="c3c8c-109">Property</span></span>  |  <span data-ttu-id="c3c8c-110">Leírás</span><span class="sxs-lookup"><span data-stu-id="c3c8c-110">Description</span></span>   | 
|---|---| 
| <span data-ttu-id="c3c8c-111">resourceName</span><span class="sxs-lookup"><span data-stu-id="c3c8c-111">ResourceName</span></span>| <span data-ttu-id="c3c8c-112">Az erőforrásnév függ.</span><span class="sxs-lookup"><span data-stu-id="c3c8c-112">The resource name to depend on.</span></span> <span data-ttu-id="c3c8c-113">Ha egy másik konfigurációs ehhez az erőforráshoz tartozik, a neve, ahogyan formázása "[__ResourceType__]__ResourceName__:: [__ConfigurationName__]:: [ __ConfigurationName__] "</span><span class="sxs-lookup"><span data-stu-id="c3c8c-113">If this resource belongs to a different configuration, format the name as "[__ResourceType__]__ResourceName__::[__ConfigurationName__]::[__ConfigurationName__]"</span></span>| 
| <span data-ttu-id="c3c8c-114">Csomópontnév</span><span class="sxs-lookup"><span data-stu-id="c3c8c-114">NodeName</span></span>| <span data-ttu-id="c3c8c-115">Az erőforrás függ a célcsomópontokat.</span><span class="sxs-lookup"><span data-stu-id="c3c8c-115">The target nodes of the resource to depend on.</span></span>| 
| <span data-ttu-id="c3c8c-116">RetryIntervalSec</span><span class="sxs-lookup"><span data-stu-id="c3c8c-116">RetryIntervalSec</span></span>| <span data-ttu-id="c3c8c-117">Másodpercig az újrapróbálkozás előtt száma.</span><span class="sxs-lookup"><span data-stu-id="c3c8c-117">The number of seconds before retrying.</span></span> <span data-ttu-id="c3c8c-118">Minimális érték 1.</span><span class="sxs-lookup"><span data-stu-id="c3c8c-118">Minimum is 1.</span></span>| 
| <span data-ttu-id="c3c8c-119">a retryCount</span><span class="sxs-lookup"><span data-stu-id="c3c8c-119">RetryCount</span></span>| <span data-ttu-id="c3c8c-120">A próbálkozások maximális számát.</span><span class="sxs-lookup"><span data-stu-id="c3c8c-120">The maximum number of times to retry.</span></span>| 
| <span data-ttu-id="c3c8c-121">ThrottleLimit</span><span class="sxs-lookup"><span data-stu-id="c3c8c-121">ThrottleLimit</span></span>| <span data-ttu-id="c3c8c-122">Az egyidejű csatlakozást a gépek számát.</span><span class="sxs-lookup"><span data-stu-id="c3c8c-122">Number of machines to connect simultaneously.</span></span> <span data-ttu-id="c3c8c-123">Alapértelmezés szerint új-cimsession alapértelmezett.</span><span class="sxs-lookup"><span data-stu-id="c3c8c-123">Default is new-cimsession default.</span></span>| 
| <span data-ttu-id="c3c8c-124">dependsOn</span><span class="sxs-lookup"><span data-stu-id="c3c8c-124">DependsOn</span></span> | <span data-ttu-id="c3c8c-125">Azt jelzi, hogy egy másik erőforrás konfigurációjának kell futtatni, mielőtt ehhez az erőforráshoz van konfigurálva.</span><span class="sxs-lookup"><span data-stu-id="c3c8c-125">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="c3c8c-126">Például, ha az erőforrás-konfiguráció azonosítója blokk futtatni kívánt parancsfájl első az __ResourceName__ és annak típusa __ResourceType__, az e tulajdonság használatával szintaxisa a következő `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="c3c8c-126">For example, if the ID of the resource configuration script block that you want to run first is __ResourceName__ and its type is __ResourceType__, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|


## <a name="example"></a><span data-ttu-id="c3c8c-127">Példa</span><span class="sxs-lookup"><span data-stu-id="c3c8c-127">Example</span></span>

<span data-ttu-id="c3c8c-128">Példa bemutatja, hogyan az erőforrás, lásd: [cross-csomópont függőségeinek megadása](crossNodeDependencies.md)</span><span class="sxs-lookup"><span data-stu-id="c3c8c-128">For an example of how to use this resource, see [Specifying cross-node dependencies](crossNodeDependencies.md)</span></span>

