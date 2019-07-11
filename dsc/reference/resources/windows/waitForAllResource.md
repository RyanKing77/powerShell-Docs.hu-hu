---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: DSC WaitForAll erőforrás
ms.openlocfilehash: c1125b7c5b68b9b520ed052800b6a2abf4e53b85
ms.sourcegitcommit: 46bebe692689ebedfe65ff2c828fe666b443198d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/10/2019
ms.locfileid: "67726880"
---
# <a name="dsc-waitforall-resource"></a><span data-ttu-id="a898b-103">DSC WaitForAll erőforrás</span><span class="sxs-lookup"><span data-stu-id="a898b-103">DSC WaitForAll Resource</span></span>

> <span data-ttu-id="a898b-104">Érvényes: Windows PowerShell 5.0-s és újabb verziók</span><span class="sxs-lookup"><span data-stu-id="a898b-104">Applies To: Windows PowerShell 5.0 and later</span></span>

<span data-ttu-id="a898b-105">A **WaitForAll** egy csomópont letiltása a Desired State Configuration (DSC) erőforrás használható egy [DSC-konfiguráció](../../../configurations/configurations.md) függőségeinek megadása a konfigurációk a többi csomóponton.</span><span class="sxs-lookup"><span data-stu-id="a898b-105">The **WaitForAll** Desired State Configuration (DSC) resource can be used within a node block in a [DSC configuration](../../../configurations/configurations.md) to specify dependencies on configurations on other nodes.</span></span>

<span data-ttu-id="a898b-106">Ez az erőforrás sikeres lesz, abban az esetben, ha az erőforrás által meghatározott a **ResourceName** tulajdonság az összes, meghatározott cél csomóponton a kívánt állapotban van a **csomópontnév** tulajdonság.</span><span class="sxs-lookup"><span data-stu-id="a898b-106">This resource succeeds if the resource specified by the **ResourceName** property is in the desired state on all target nodes defined in the **NodeName** property.</span></span>

> [!NOTE]
> <span data-ttu-id="a898b-107">**WaitForAll** erőforrás használja a Windows távoli felügyeleti ellenőrzéséhez más csomópontok állapotát.</span><span class="sxs-lookup"><span data-stu-id="a898b-107">**WaitForAll** resource uses Windows Remote Management to check the state of other Nodes.</span></span>
> <span data-ttu-id="a898b-108">A Rendszerfelügyeleti webszolgáltatások port és a biztonsági követelményeivel kapcsolatos további információkért lásd: [PowerShell távoli eljáráshívásainak biztonsági megfontolásai](/powershell/scripting/learn/remoting/winrmsecurity?view=powershell-6).</span><span class="sxs-lookup"><span data-stu-id="a898b-108">For more information about port and security requirements for WinRM, see [PowerShell Remoting Security Considerations](/powershell/scripting/learn/remoting/winrmsecurity?view=powershell-6).</span></span>

## <a name="syntax"></a><span data-ttu-id="a898b-109">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="a898b-109">Syntax</span></span>

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

## <a name="properties"></a><span data-ttu-id="a898b-110">Tulajdonságok</span><span class="sxs-lookup"><span data-stu-id="a898b-110">Properties</span></span>

|  <span data-ttu-id="a898b-111">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="a898b-111">Property</span></span>  |  <span data-ttu-id="a898b-112">Leírás</span><span class="sxs-lookup"><span data-stu-id="a898b-112">Description</span></span>   |
|---|---|
| <span data-ttu-id="a898b-113">ResourceName</span><span class="sxs-lookup"><span data-stu-id="a898b-113">ResourceName</span></span>| <span data-ttu-id="a898b-114">Az erőforrásnév függenek.</span><span class="sxs-lookup"><span data-stu-id="a898b-114">The resource name to depend on.</span></span> <span data-ttu-id="a898b-115">Ha az erőforrás tartozik egy másik konfigurációs, formázhatja a nevet a következőként "[__ResourceType__]__ResourceName__:: [__ConfigurationName__]:: [ __ConfigurationName__] "</span><span class="sxs-lookup"><span data-stu-id="a898b-115">If this resource belongs to a different configuration, format the name as "[__ResourceType__]__ResourceName__::[__ConfigurationName__]::[__ConfigurationName__]"</span></span>|
| <span data-ttu-id="a898b-116">Csomópontnév</span><span class="sxs-lookup"><span data-stu-id="a898b-116">NodeName</span></span>| <span data-ttu-id="a898b-117">Az erőforrás függenek a célcsomópontokat.</span><span class="sxs-lookup"><span data-stu-id="a898b-117">The target nodes of the resource to depend on.</span></span>|
| <span data-ttu-id="a898b-118">RetryIntervalSec</span><span class="sxs-lookup"><span data-stu-id="a898b-118">RetryIntervalSec</span></span>| <span data-ttu-id="a898b-119">Mielőtt újra próbálkozna másodpercek számát.</span><span class="sxs-lookup"><span data-stu-id="a898b-119">The number of seconds before retrying.</span></span> <span data-ttu-id="a898b-120">Minimális érték 1.</span><span class="sxs-lookup"><span data-stu-id="a898b-120">Minimum is 1.</span></span>|
| <span data-ttu-id="a898b-121">RetryCount</span><span class="sxs-lookup"><span data-stu-id="a898b-121">RetryCount</span></span>| <span data-ttu-id="a898b-122">Az újrapróbálkozások maximális száma.</span><span class="sxs-lookup"><span data-stu-id="a898b-122">The maximum number of times to retry.</span></span>|
| <span data-ttu-id="a898b-123">ThrottleLimit</span><span class="sxs-lookup"><span data-stu-id="a898b-123">ThrottleLimit</span></span>| <span data-ttu-id="a898b-124">Egyidejű csatlakozás gépek száma.</span><span class="sxs-lookup"><span data-stu-id="a898b-124">Number of machines to connect simultaneously.</span></span> <span data-ttu-id="a898b-125">Alapértelmezés szerint új cimsession alapértelmezett.</span><span class="sxs-lookup"><span data-stu-id="a898b-125">Default is new-cimsession default.</span></span>|
| <span data-ttu-id="a898b-126">DependsOn</span><span class="sxs-lookup"><span data-stu-id="a898b-126">DependsOn</span></span> | <span data-ttu-id="a898b-127">Azt jelzi, hogy a konfigurációt egy másik erőforrás futtatnia kell, mielőtt az erőforrás konfigurálva van.</span><span class="sxs-lookup"><span data-stu-id="a898b-127">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="a898b-128">Például, ha az erőforrás-konfiguráció azonosítója letiltása, a futtatni kívánt parancsfájl először van __ResourceName__ és a típusa __ResourceType__, ez a tulajdonság használata esetén `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="a898b-128">For example, if the ID of the resource configuration script block that you want to run first is __ResourceName__ and its type is __ResourceType__, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|

## <a name="example"></a><span data-ttu-id="a898b-129">Példa</span><span class="sxs-lookup"><span data-stu-id="a898b-129">Example</span></span>

<span data-ttu-id="a898b-130">Egy példa bemutatja, hogyan használhatja ezt az erőforrást: [csomópontok közötti függőségek megadása](../../../configurations/crossNodeDependencies.md)</span><span class="sxs-lookup"><span data-stu-id="a898b-130">For an example of how to use this resource, see [Specifying cross-node dependencies](../../../configurations/crossNodeDependencies.md)</span></span>
