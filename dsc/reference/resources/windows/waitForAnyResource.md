---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: DSC WaitForAny erőforrás
ms.openlocfilehash: d15acb3fb34d571eca56ed496eaa9a04b2551ff0
ms.sourcegitcommit: 46bebe692689ebedfe65ff2c828fe666b443198d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/10/2019
ms.locfileid: "67726856"
---
# <a name="dsc-waitforany-resource"></a><span data-ttu-id="29991-103">DSC WaitForAny erőforrás</span><span class="sxs-lookup"><span data-stu-id="29991-103">DSC WaitForAny Resource</span></span>

> <span data-ttu-id="29991-104">Érvényes: Windows PowerShell 5.1-es és újabb verziók</span><span class="sxs-lookup"><span data-stu-id="29991-104">Applies To: Windows PowerShell 5.1 and later</span></span>

<span data-ttu-id="29991-105">A **WaitForAny** egy csomópont letiltása a Desired State Configuration (DSC) erőforrás használható egy [DSC-konfiguráció](../../../configurations/configurations.md) függőségeinek megadása a konfigurációk a többi csomóponton.</span><span class="sxs-lookup"><span data-stu-id="29991-105">The **WaitForAny** Desired State Configuration (DSC) resource can be used within a node block in a [DSC configuration](../../../configurations/configurations.md) to specify dependencies on configurations on other nodes.</span></span>

<span data-ttu-id="29991-106">Ez az erőforrás sikeres lesz, abban az esetben, ha az erőforrás által meghatározott a **ResourceName** tulajdonság bármely meghatározott cél-csomópontokon a kívánt állapotban van a **csomópontnév** tulajdonság.</span><span class="sxs-lookup"><span data-stu-id="29991-106">This resource succeeds if the resource specified by the **ResourceName** property is in the desired state on any target nodes defined in the **NodeName** property.</span></span>

> [!NOTE]
> <span data-ttu-id="29991-107">**WaitForAny** erőforrás használja a Windows távoli felügyeleti ellenőrzéséhez más csomópontok állapotát.</span><span class="sxs-lookup"><span data-stu-id="29991-107">**WaitForAny** resource uses Windows Remote Management to check the state of other Nodes.</span></span>
> <span data-ttu-id="29991-108">A Rendszerfelügyeleti webszolgáltatások port és a biztonsági követelményeivel kapcsolatos további információkért lásd: [PowerShell távoli eljáráshívásainak biztonsági megfontolásai](/powershell/scripting/learn/remoting/winrmsecurity?view=powershell-6).</span><span class="sxs-lookup"><span data-stu-id="29991-108">For more information about port and security requirements for WinRM, see [PowerShell Remoting Security Considerations](/powershell/scripting/learn/remoting/winrmsecurity?view=powershell-6).</span></span>

## <a name="syntax"></a><span data-ttu-id="29991-109">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="29991-109">Syntax</span></span>

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

## <a name="properties"></a><span data-ttu-id="29991-110">Tulajdonságok</span><span class="sxs-lookup"><span data-stu-id="29991-110">Properties</span></span>

|  <span data-ttu-id="29991-111">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="29991-111">Property</span></span>  |  <span data-ttu-id="29991-112">Leírás</span><span class="sxs-lookup"><span data-stu-id="29991-112">Description</span></span>   |
|---|---|
| <span data-ttu-id="29991-113">ResourceName</span><span class="sxs-lookup"><span data-stu-id="29991-113">ResourceName</span></span>| <span data-ttu-id="29991-114">Az erőforrásnév függenek.</span><span class="sxs-lookup"><span data-stu-id="29991-114">The resource name to depend on.</span></span> <span data-ttu-id="29991-115">Ha az erőforrás tartozik egy másik konfigurációs, formázhatja a nevet a következőként "[__ResourceType__]__ResourceName__:: [__ConfigurationName__]:: [ __ConfigurationName__] "</span><span class="sxs-lookup"><span data-stu-id="29991-115">If this resource belongs to a different configuration, format the name as "[__ResourceType__]__ResourceName__::[__ConfigurationName__]::[__ConfigurationName__]"</span></span>|
| <span data-ttu-id="29991-116">Csomópontnév</span><span class="sxs-lookup"><span data-stu-id="29991-116">NodeName</span></span>| <span data-ttu-id="29991-117">Az erőforrás függenek a célcsomópontokat.</span><span class="sxs-lookup"><span data-stu-id="29991-117">The target nodes of the resource to depend on.</span></span>|
| <span data-ttu-id="29991-118">RetryIntervalSec</span><span class="sxs-lookup"><span data-stu-id="29991-118">RetryIntervalSec</span></span>| <span data-ttu-id="29991-119">Mielőtt újra próbálkozna másodpercek számát.</span><span class="sxs-lookup"><span data-stu-id="29991-119">The number of seconds before retrying.</span></span> <span data-ttu-id="29991-120">Minimális érték 1.</span><span class="sxs-lookup"><span data-stu-id="29991-120">Minimum is 1.</span></span>|
| <span data-ttu-id="29991-121">RetryCount</span><span class="sxs-lookup"><span data-stu-id="29991-121">RetryCount</span></span>| <span data-ttu-id="29991-122">Az újrapróbálkozások maximális száma.</span><span class="sxs-lookup"><span data-stu-id="29991-122">The maximum number of times to retry.</span></span>|
| <span data-ttu-id="29991-123">ThrottleLimit</span><span class="sxs-lookup"><span data-stu-id="29991-123">ThrottleLimit</span></span>| <span data-ttu-id="29991-124">Egyidejű csatlakozás gépek száma.</span><span class="sxs-lookup"><span data-stu-id="29991-124">Number of machines to connect simultaneously.</span></span> <span data-ttu-id="29991-125">Alapértelmezés szerint új cimsession alapértelmezett.</span><span class="sxs-lookup"><span data-stu-id="29991-125">Default is new-cimsession default.</span></span>|
| <span data-ttu-id="29991-126">DependsOn</span><span class="sxs-lookup"><span data-stu-id="29991-126">DependsOn</span></span> | <span data-ttu-id="29991-127">Azt jelzi, hogy a konfigurációt egy másik erőforrás futtatnia kell, mielőtt az erőforrás konfigurálva van.</span><span class="sxs-lookup"><span data-stu-id="29991-127">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="29991-128">Például, ha az erőforrás-konfiguráció azonosítója letiltása, a futtatni kívánt parancsfájl először van __ResourceName__ és a típusa __ResourceType__, ez a tulajdonság használata esetén `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="29991-128">For example, if the ID of the resource configuration script block that you want to run first is __ResourceName__ and its type is __ResourceType__, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|

## <a name="example"></a><span data-ttu-id="29991-129">Példa</span><span class="sxs-lookup"><span data-stu-id="29991-129">Example</span></span>

<span data-ttu-id="29991-130">Egy példa bemutatja, hogyan használhatja ezt az erőforrást: [csomópontok közötti függőségek megadása](../../../configurations/crossNodeDependencies.md)</span><span class="sxs-lookup"><span data-stu-id="29991-130">For an example of how to use this resource, see [Specifying cross-node dependencies](../../../configurations/crossNodeDependencies.md)</span></span>
