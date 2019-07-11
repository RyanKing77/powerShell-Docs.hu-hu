---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: DSC WaitForSome Resource
ms.openlocfilehash: 2260f37002171154a6f2c3996b2af1bd9120039d
ms.sourcegitcommit: 46bebe692689ebedfe65ff2c828fe666b443198d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/10/2019
ms.locfileid: "67726768"
---
# <a name="dsc-waitforsome-resource"></a><span data-ttu-id="175a3-103">DSC WaitForSome Resource</span><span class="sxs-lookup"><span data-stu-id="175a3-103">DSC WaitForSome Resource</span></span>

> <span data-ttu-id="175a3-104">Érvényes: Windows PowerShell 5.0-s és újabb verziók</span><span class="sxs-lookup"><span data-stu-id="175a3-104">Applies To: Windows PowerShell 5.0 and later</span></span>

<span data-ttu-id="175a3-105">A **WaitForSome** egy csomópont letiltása a Desired State Configuration (DSC) erőforrás használható egy [DSC-konfiguráció](../../../configurations/configurations.md) függőségeinek megadása a konfigurációk a többi csomóponton.</span><span class="sxs-lookup"><span data-stu-id="175a3-105">The **WaitForSome** Desired State Configuration (DSC) resource can be used within a node block in a [DSC configuration](../../../configurations/configurations.md) to specify dependencies on configurations on other nodes.</span></span>

<span data-ttu-id="175a3-106">Ehhez az erőforráshoz sikeres lesz, abban az esetben, ha az erőforrás által meghatározott a **ResourceName** tulajdonság a kívánt állapotban lévő csomópontok minimális száma (által megadott **NodeCount**) által meghatározott a **csomópontnév**  tulajdonság.</span><span class="sxs-lookup"><span data-stu-id="175a3-106">This resource succeeds if the resource specified by the **ResourceName** property is in the desired state on a minimum number of nodes (specified by **NodeCount**) defined by the **NodeName** property.</span></span>

> [!NOTE]
> <span data-ttu-id="175a3-107">**WaitForSome** erőforrás használja a Windows távoli felügyeleti ellenőrzéséhez más csomópontok állapotát.</span><span class="sxs-lookup"><span data-stu-id="175a3-107">**WaitForSome** resource uses Windows Remote Management to check the state of other Nodes.</span></span>
> <span data-ttu-id="175a3-108">A Rendszerfelügyeleti webszolgáltatások port és a biztonsági követelményeivel kapcsolatos további információkért lásd: [PowerShell távoli eljáráshívásainak biztonsági megfontolásai](/powershell/scripting/learn/remoting/winrmsecurity?view=powershell-6).</span><span class="sxs-lookup"><span data-stu-id="175a3-108">For more information about port and security requirements for WinRM, see [PowerShell Remoting Security Considerations](/powershell/scripting/learn/remoting/winrmsecurity?view=powershell-6).</span></span>

## <a name="syntax"></a><span data-ttu-id="175a3-109">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="175a3-109">Syntax</span></span>

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

## <a name="properties"></a><span data-ttu-id="175a3-110">Tulajdonságok</span><span class="sxs-lookup"><span data-stu-id="175a3-110">Properties</span></span>

|  <span data-ttu-id="175a3-111">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="175a3-111">Property</span></span>  |  <span data-ttu-id="175a3-112">Leírás</span><span class="sxs-lookup"><span data-stu-id="175a3-112">Description</span></span>   |
|---|---|
| <span data-ttu-id="175a3-113">NodeCount</span><span class="sxs-lookup"><span data-stu-id="175a3-113">NodeCount</span></span>| <span data-ttu-id="175a3-114">Ehhez az erőforráshoz sikeres a kívánt állapotban kell lennie csomópontok minimális száma.</span><span class="sxs-lookup"><span data-stu-id="175a3-114">The minimum number of nodes that must be in the desired state for this resource to succeed.</span></span>|
| <span data-ttu-id="175a3-115">Csomópontnév</span><span class="sxs-lookup"><span data-stu-id="175a3-115">NodeName</span></span>| <span data-ttu-id="175a3-116">Az erőforrás függenek a célcsomópontokat.</span><span class="sxs-lookup"><span data-stu-id="175a3-116">The target nodes of the resource to depend on.</span></span>|
| <span data-ttu-id="175a3-117">ResourceName</span><span class="sxs-lookup"><span data-stu-id="175a3-117">ResourceName</span></span>| <span data-ttu-id="175a3-118">Az erőforrásnév függenek.</span><span class="sxs-lookup"><span data-stu-id="175a3-118">The resource name to depend on.</span></span> <span data-ttu-id="175a3-119">Ha az erőforrás tartozik egy másik konfigurációs, formázhatja a nevet a következőként "[__ResourceType__]__ResourceName__:: [__ConfigurationName__]:: [ __ConfigurationName__] "</span><span class="sxs-lookup"><span data-stu-id="175a3-119">If this resource belongs to a different configuration, format the name as "[__ResourceType__]__ResourceName__::[__ConfigurationName__]::[__ConfigurationName__]"</span></span>|
| <span data-ttu-id="175a3-120">RetryIntervalSec</span><span class="sxs-lookup"><span data-stu-id="175a3-120">RetryIntervalSec</span></span>| <span data-ttu-id="175a3-121">Mielőtt újra próbálkozna másodpercek számát.</span><span class="sxs-lookup"><span data-stu-id="175a3-121">The number of seconds before retrying.</span></span> <span data-ttu-id="175a3-122">Minimális érték 1.</span><span class="sxs-lookup"><span data-stu-id="175a3-122">Minimum is 1.</span></span>|
| <span data-ttu-id="175a3-123">RetryCount</span><span class="sxs-lookup"><span data-stu-id="175a3-123">RetryCount</span></span>| <span data-ttu-id="175a3-124">Az újrapróbálkozások maximális száma.</span><span class="sxs-lookup"><span data-stu-id="175a3-124">The maximum number of times to retry.</span></span>|
| <span data-ttu-id="175a3-125">ThrottleLimit</span><span class="sxs-lookup"><span data-stu-id="175a3-125">ThrottleLimit</span></span>| <span data-ttu-id="175a3-126">Egyidejű csatlakozás gépek száma.</span><span class="sxs-lookup"><span data-stu-id="175a3-126">Number of machines to connect simultaneously.</span></span> <span data-ttu-id="175a3-127">Alapértelmezés szerint új cimsession alapértelmezett.</span><span class="sxs-lookup"><span data-stu-id="175a3-127">Default is new-cimsession default.</span></span>|
| <span data-ttu-id="175a3-128">DependsOn</span><span class="sxs-lookup"><span data-stu-id="175a3-128">DependsOn</span></span> | <span data-ttu-id="175a3-129">Azt jelzi, hogy a konfigurációt egy másik erőforrás futtatnia kell, mielőtt az erőforrás konfigurálva van.</span><span class="sxs-lookup"><span data-stu-id="175a3-129">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="175a3-130">Például, ha az erőforrás-konfiguráció azonosítója letiltása, a futtatni kívánt parancsfájl először van __ResourceName__ és a típusa __ResourceType__, ez a tulajdonság használata esetén `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="175a3-130">For example, if the ID of the resource configuration script block that you want to run first is __ResourceName__ and its type is __ResourceType__, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|
| <span data-ttu-id="175a3-131">PsDscRunAsCredential</span><span class="sxs-lookup"><span data-stu-id="175a3-131">PsDscRunAsCredential</span></span> | <span data-ttu-id="175a3-132">Lásd: [DSC használata a felhasználói hitelesítő adatok](https://docs.microsoft.com/powershell/dsc/runasuser)</span><span class="sxs-lookup"><span data-stu-id="175a3-132">See [Using DSC with User Credentials](https://docs.microsoft.com/powershell/dsc/runasuser)</span></span> |

## <a name="example"></a><span data-ttu-id="175a3-133">Példa</span><span class="sxs-lookup"><span data-stu-id="175a3-133">Example</span></span>

<span data-ttu-id="175a3-134">Egy példa bemutatja, hogyan használhatja ezt az erőforrást: [csomópontok közötti függőségek megadása](../../../configurations/crossNodeDependencies.md)</span><span class="sxs-lookup"><span data-stu-id="175a3-134">For an example of how to use this resource, see [Specifying cross-node dependencies](../../../configurations/crossNodeDependencies.md)</span></span>
