---
ms.date: 12/12/2018
keywords: DSC, powershell, a konfigurációt, a beállítása
title: Csomópontok közötti függőségek megadása
ms.openlocfilehash: 62e553d894897ae1908745c2788b7b7b9cbe50ff
ms.sourcegitcommit: 46bebe692689ebedfe65ff2c828fe666b443198d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/10/2019
ms.locfileid: "67734684"
---
# <a name="specifying-cross-node-dependencies"></a><span data-ttu-id="db79b-103">Csomópontok közötti függőségek megadása</span><span class="sxs-lookup"><span data-stu-id="db79b-103">Specifying cross-node dependencies</span></span>

> <span data-ttu-id="db79b-104">Érvényes: Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="db79b-104">Applies To: Windows PowerShell 5.0</span></span>

<span data-ttu-id="db79b-105">DSC biztosít speciális erőforrások **WaitForAll**, **WaitForAny**, és **WaitForSome** , amely használható a konfigurációkban függőségeinek megadása a további beállításai csomópontok.</span><span class="sxs-lookup"><span data-stu-id="db79b-105">DSC provides special resources, **WaitForAll**, **WaitForAny**, and **WaitForSome** that can be used in configurations to specify dependencies on configurations on other nodes.</span></span> <span data-ttu-id="db79b-106">Ezek az erőforrások viselkedését a következőképpen történik:</span><span class="sxs-lookup"><span data-stu-id="db79b-106">The behavior of these resources is as follows:</span></span>

- <span data-ttu-id="db79b-107">**WaitForAll**: Sikeres lesz, ha az adott erőforrás az összes, meghatározott cél csomóponton a kívánt állapotban van a **csomópontnév** tulajdonság.</span><span class="sxs-lookup"><span data-stu-id="db79b-107">**WaitForAll**: Succeeds if the specified resource is in the desired state on all target nodes defined in the **NodeName** property.</span></span>
- <span data-ttu-id="db79b-108">**WaitForAny**: Sikeres lesz, ha a megadott erőforrás legalább az egyik a célcsomópontokat, meghatározott a kívánt állapotban van a **csomópontnév** tulajdonság.</span><span class="sxs-lookup"><span data-stu-id="db79b-108">**WaitForAny**: Succeeds if the specified resource is in the desired state on at least one of the target nodes defined in the **NodeName** property.</span></span>
- <span data-ttu-id="db79b-109">**WaitForSome**: Megadja egy **NodeCount** tulajdonság mellett egy **csomópontnév** tulajdonság.</span><span class="sxs-lookup"><span data-stu-id="db79b-109">**WaitForSome**: Specifies a **NodeCount** property in addition to a **NodeName** property.</span></span> <span data-ttu-id="db79b-110">Az erőforrás sikeres lesz, ha az erőforrás a kívánt állapotban lévő csomópontok minimális száma (által megadott **NodeCount**) által meghatározott a **csomópontnév** tulajdonság.</span><span class="sxs-lookup"><span data-stu-id="db79b-110">The resource succeeds if the resource is in the desired state on a minimum number of nodes (specified by **NodeCount**) defined by the **NodeName** property.</span></span>

## <a name="syntax"></a><span data-ttu-id="db79b-111">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="db79b-111">Syntax</span></span>

<span data-ttu-id="db79b-112">A **WaitForAll** és **WaitForAny** erőforrások megosztása ugyanazt a szintaxist.</span><span class="sxs-lookup"><span data-stu-id="db79b-112">The **WaitForAll** and **WaitForAny** resources share the same syntax.</span></span> <span data-ttu-id="db79b-113">Cserélje le \<ResourceType\> -t az alábbi példában **WaitForAny** vagy **WaitForAll**.</span><span class="sxs-lookup"><span data-stu-id="db79b-113">Replace \<ResourceType\> in the example below with either **WaitForAny** or **WaitForAll**.</span></span>
<span data-ttu-id="db79b-114">Például a **DependsOn** kulcsszó, szüksége lesz a nevet a következőként: "[ResourceType] ResourceName" formátumban.</span><span class="sxs-lookup"><span data-stu-id="db79b-114">Like the **DependsOn** keyword, you will need to format the name as "[ResourceType]ResourceName".</span></span> <span data-ttu-id="db79b-115">Ha az erőforrás tartozik egy külön [konfigurációs](configurations.md), például a **ConfigurationName** a formázott karakterlánc "[ResourceType] ResourceName:: [ConfigurationName]:: [ConfigurationName]".</span><span class="sxs-lookup"><span data-stu-id="db79b-115">If the resource belongs to a separate [Configuration](configurations.md), include the **ConfigurationName** in the formatted string "[ResourceType]ResourceName::[ConfigurationName]::[ConfigurationName]".</span></span> <span data-ttu-id="db79b-116">A **csomópontnév** a számítógép vagy a csomópont, amelyen az aktuális erőforrás várnia kell.</span><span class="sxs-lookup"><span data-stu-id="db79b-116">The **NodeName** is the computer, or Node, on which the current resource should wait.</span></span>

```
<ResourceType> [string] #ResourceName
{
    ResourceName = [string]
    NodeName = [string]
    [ DependsOn = [string[]] ]
    [ PsDscRunAsCredential = [PSCredential]]
    [ RetryCount = [Uint32] ]
    [ RetryIntervalSec = [Uint64] ]
    [ ThrottleLimit = [Uint32]]
}
```

<span data-ttu-id="db79b-117">A **WaitForSome** erőforrás a fenti példában egy hasonló szintaxissal rendelkezik, de hozzáadja a **NodeCount** kulcsot.</span><span class="sxs-lookup"><span data-stu-id="db79b-117">The **WaitForSome** resource has a similar syntax to the example above, but adds the **NodeCount** key.</span></span> <span data-ttu-id="db79b-118">A **NodeCount** azt jelzi, hogy a várjon az aktuális erőforrás hány csomóponttal.</span><span class="sxs-lookup"><span data-stu-id="db79b-118">The **NodeCount** indicates how many Nodes the current resource should wait on.</span></span>

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

<span data-ttu-id="db79b-119">Az összes **WaitForXXXX** az alábbi szintaxissal kulcsok megoszthatja.</span><span class="sxs-lookup"><span data-stu-id="db79b-119">All **WaitForXXXX** share the following syntax keys.</span></span>

|<span data-ttu-id="db79b-120">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="db79b-120">Property</span></span>|  <span data-ttu-id="db79b-121">Leírás</span><span class="sxs-lookup"><span data-stu-id="db79b-121">Description</span></span>   |
|---------|---------------------|
| <span data-ttu-id="db79b-122">RetryIntervalSec</span><span class="sxs-lookup"><span data-stu-id="db79b-122">RetryIntervalSec</span></span>| <span data-ttu-id="db79b-123">Mielőtt újra próbálkozna másodpercek számát.</span><span class="sxs-lookup"><span data-stu-id="db79b-123">The number of seconds before retrying.</span></span> <span data-ttu-id="db79b-124">Minimális érték 1.</span><span class="sxs-lookup"><span data-stu-id="db79b-124">Minimum is 1.</span></span>|
| <span data-ttu-id="db79b-125">RetryCount</span><span class="sxs-lookup"><span data-stu-id="db79b-125">RetryCount</span></span>| <span data-ttu-id="db79b-126">Az újrapróbálkozások maximális száma.</span><span class="sxs-lookup"><span data-stu-id="db79b-126">The maximum number of times to retry.</span></span>|
| <span data-ttu-id="db79b-127">ThrottleLimit</span><span class="sxs-lookup"><span data-stu-id="db79b-127">ThrottleLimit</span></span>| <span data-ttu-id="db79b-128">Egyidejű csatlakozás gépek száma.</span><span class="sxs-lookup"><span data-stu-id="db79b-128">Number of machines to connect simultaneously.</span></span> <span data-ttu-id="db79b-129">Alapértelmezett érték a `New-CimSession` alapértelmezett.</span><span class="sxs-lookup"><span data-stu-id="db79b-129">Default is `New-CimSession` default.</span></span>|
| <span data-ttu-id="db79b-130">DependsOn</span><span class="sxs-lookup"><span data-stu-id="db79b-130">DependsOn</span></span> | <span data-ttu-id="db79b-131">Azt jelzi, hogy a konfigurációt egy másik erőforrás futtatnia kell, mielőtt az erőforrás konfigurálva van.</span><span class="sxs-lookup"><span data-stu-id="db79b-131">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="db79b-132">További információkért lásd: [DependsOn](resource-depends-on.md)</span><span class="sxs-lookup"><span data-stu-id="db79b-132">For more information, see [DependsOn](resource-depends-on.md)</span></span>|
| <span data-ttu-id="db79b-133">PsDscRunAsCredential</span><span class="sxs-lookup"><span data-stu-id="db79b-133">PsDscRunAsCredential</span></span> | <span data-ttu-id="db79b-134">Lásd: [DSC használata a felhasználói hitelesítő adatok](./runAsUser.md)</span><span class="sxs-lookup"><span data-stu-id="db79b-134">See [Using DSC with User Credentials](./runAsUser.md)</span></span> |

## <a name="using-waitforxxxx-resources"></a><span data-ttu-id="db79b-135">WaitForXXXX erőforrások használata</span><span class="sxs-lookup"><span data-stu-id="db79b-135">Using WaitForXXXX resources</span></span>

<span data-ttu-id="db79b-136">Minden egyes **WaitForXXXX** erőforrás megvárja, amíg befejeződik a megadott csomópont a megadott erőforrások.</span><span class="sxs-lookup"><span data-stu-id="db79b-136">Each **WaitForXXXX** resource waits for the specified resources to complete on the specified Node.</span></span>
<span data-ttu-id="db79b-137">Ugyanazt a konfigurációt más erőforrások is majd *függenek* a **WaitForXXXX** erőforrást a **DependsOn** kulcsot.</span><span class="sxs-lookup"><span data-stu-id="db79b-137">Other resources in the same Configuration can then *depend on* the **WaitForXXXX** resource using the **DependsOn** key.</span></span>

<span data-ttu-id="db79b-138">Például a következő konfigurációban a célcsomópont várakozik a **xADDomain** erőforrás a befejezéséhez a **MyDC** legfeljebb 30-csomópont újrapróbálkozik, 15 másodperces intervallumon előtt a Célcsomópont csatlakozhat a tartományhoz.</span><span class="sxs-lookup"><span data-stu-id="db79b-138">For example, in the following configuration, the target node is waiting for the **xADDomain** resource to finish on the **MyDC** node with maximum number of 30 retries, at 15-second intervals, before the target node can join the domain.</span></span>

<span data-ttu-id="db79b-139">Alapértelmezés szerint a **WaitForXXX** erőforrások próbálja meg egyszer, és akkor sikertelen.</span><span class="sxs-lookup"><span data-stu-id="db79b-139">By default the **WaitForXXX** resources try one time and then fail.</span></span> <span data-ttu-id="db79b-140">Bár ez nem szükséges, általában célszerű adjon meg egy **RetryCount** és **RetryIntervalSec**.</span><span class="sxs-lookup"><span data-stu-id="db79b-140">Although it is not required, you will typically want to specify a **RetryCount** and **RetryIntervalSec**.</span></span>

```powershell
Configuration JoinDomain
{
    Import-DscResource -Module xComputerManagement, xActiveDirectory

    Node myDC
    {
        WindowsFeature InstallAD
        {
            Ensure = 'Present'
            Name = 'AD-Domain-Services'
        }

        xADDomain NewDomain
        {
            DomainName = 'Contoso.com'
            DomainAdministratorCredential = (Get-Credential)
            SafemodeAdministratorPassword = (Get-Credential)
            DatabasePath = "C:\Windows\NTDS"
            LogPath = "C:\Windows\NTDS"
            SysvolPath = "C:\Windows\Sysvol"
        }
    }

    Node myDomainJoinedServer
    {
        WaitForAll DC
        {
            ResourceName      = '[xADDomain]NewDomain'
            NodeName          = 'MyDC'
            RetryIntervalSec  = 15
            RetryCount        = 30
        }

        xComputer JoinDomain
        {
            Name             = 'myPC'
            DomainName       = 'Contoso.com'
            Credential       = (Get-Credential)
            DependsOn        ='[WaitForAll]DC'
        }
    }
}
```

<span data-ttu-id="db79b-141">Konfiguráció fordítása, amikor két ".mof" fájlok jönnek létre.</span><span class="sxs-lookup"><span data-stu-id="db79b-141">When you compile the Configuration, two ".mof" files are generated.</span></span> <span data-ttu-id="db79b-142">".Mof" fájlok egyaránt vonatkozik a célcsomópontokat, használja a [Start-DSCConfiguration](/powershell/module/psdesiredstateconfiguration/start-dscconfiguration) parancsmag</span><span class="sxs-lookup"><span data-stu-id="db79b-142">Apply both ".mof" files to the target Nodes using the [Start-DSCConfiguration](/powershell/module/psdesiredstateconfiguration/start-dscconfiguration) cmdlet</span></span>

> [!NOTE]
> <span data-ttu-id="db79b-143">**WaitForXXX** erőforrások használják a Windows távoli felügyeleti ellenőrzéséhez más csomópontok állapotát.</span><span class="sxs-lookup"><span data-stu-id="db79b-143">**WaitForXXX** resources use Windows Remote Management to check the state of other Nodes.</span></span>
> <span data-ttu-id="db79b-144">A Rendszerfelügyeleti webszolgáltatások port és a biztonsági követelményeivel kapcsolatos további információkért lásd: [PowerShell távoli eljáráshívásainak biztonsági megfontolásai](/powershell/scripting/learn/remoting/winrmsecurity?view=powershell-6).</span><span class="sxs-lookup"><span data-stu-id="db79b-144">For more information about port and security requirements for WinRM, see [PowerShell Remoting Security Considerations](/powershell/scripting/learn/remoting/winrmsecurity?view=powershell-6).</span></span>

## <a name="see-also"></a><span data-ttu-id="db79b-145">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="db79b-145">See Also</span></span>

- [<span data-ttu-id="db79b-146">DSC-konfigurációk</span><span class="sxs-lookup"><span data-stu-id="db79b-146">DSC Configurations</span></span>](configurations.md)
- [<span data-ttu-id="db79b-147">Erőforrás-függőségek használatára</span><span class="sxs-lookup"><span data-stu-id="db79b-147">Use Resource Dependencies</span></span>](resource-depends-on.md)
- [<span data-ttu-id="db79b-148">DSC-erőforrások</span><span class="sxs-lookup"><span data-stu-id="db79b-148">DSC Resources</span></span>](../resources/resources.md)
- [<span data-ttu-id="db79b-149">A helyi Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="db79b-149">Configuring The Local Configuration Manager</span></span>](../managing-nodes/metaConfig.md)
