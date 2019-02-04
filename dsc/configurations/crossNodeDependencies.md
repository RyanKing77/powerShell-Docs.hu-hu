---
ms.date: 12/12/2018
keywords: DSC, powershell, a konfigurációt, a beállítása
title: Csomópontok közötti függőségek megadása
ms.openlocfilehash: 1bdfbd9f8a94809d6bf410eff525e1c877fb6aad
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55687523"
---
# <a name="specifying-cross-node-dependencies"></a><span data-ttu-id="81804-103">Csomópontok közötti függőségek megadása</span><span class="sxs-lookup"><span data-stu-id="81804-103">Specifying cross-node dependencies</span></span>

> <span data-ttu-id="81804-104">Érvényes: Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="81804-104">Applies To: Windows PowerShell 5.0</span></span>

<span data-ttu-id="81804-105">DSC biztosít speciális erőforrások **WaitForAll**, **WaitForAny**, és **WaitForSome** , amely használható a konfigurációkban függőségeinek megadása a további beállításai csomópontok.</span><span class="sxs-lookup"><span data-stu-id="81804-105">DSC provides special resources, **WaitForAll**, **WaitForAny**, and **WaitForSome** that can be used in configurations to specify dependencies on configurations on other nodes.</span></span> <span data-ttu-id="81804-106">Ezek az erőforrások viselkedését a következőképpen történik:</span><span class="sxs-lookup"><span data-stu-id="81804-106">The behavior of these resources is as follows:</span></span>

- <span data-ttu-id="81804-107">**WaitForAll**: Sikeres lesz, ha az adott erőforrás az összes, meghatározott cél csomóponton a kívánt állapotban van a **csomópontnév** tulajdonság.</span><span class="sxs-lookup"><span data-stu-id="81804-107">**WaitForAll**: Succeeds if the specified resource is in the desired state on all target nodes defined in the **NodeName** property.</span></span>
- <span data-ttu-id="81804-108">**WaitForAny**: Sikeres lesz, ha a megadott erőforrás legalább az egyik a célcsomópontokat, meghatározott a kívánt állapotban van a **csomópontnév** tulajdonság.</span><span class="sxs-lookup"><span data-stu-id="81804-108">**WaitForAny**: Succeeds if the specified resource is in the desired state on at least one of the target nodes defined in the **NodeName** property.</span></span>
- <span data-ttu-id="81804-109">**WaitForSome**: Megadja egy **NodeCount** tulajdonság mellett egy **csomópontnév** tulajdonság.</span><span class="sxs-lookup"><span data-stu-id="81804-109">**WaitForSome**: Specifies a **NodeCount** property in addition to a **NodeName** property.</span></span> <span data-ttu-id="81804-110">Az erőforrás sikeres lesz, ha az erőforrás a kívánt állapotban lévő csomópontok minimális száma (által megadott **NodeCount**) által meghatározott a **csomópontnév** tulajdonság.</span><span class="sxs-lookup"><span data-stu-id="81804-110">The resource succeeds if the resource is in the desired state on a minimum number of nodes (specified by **NodeCount**) defined by the **NodeName** property.</span></span>

## <a name="syntax"></a><span data-ttu-id="81804-111">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="81804-111">Syntax</span></span>

<span data-ttu-id="81804-112">A **WaitForAll** és **WaitForAny** erőforrások megosztása ugyanazt a szintaxist.</span><span class="sxs-lookup"><span data-stu-id="81804-112">The **WaitForAll** and **WaitForAny** resources share the same syntax.</span></span> <span data-ttu-id="81804-113">Cserélje le \<ResourceType\> -t az alábbi példában **WaitForAny** vagy **WaitForAll**.</span><span class="sxs-lookup"><span data-stu-id="81804-113">Replace \<ResourceType\> in the example below with either **WaitForAny** or **WaitForAll**.</span></span>
<span data-ttu-id="81804-114">Például a **DependsOn** kulcsszó, szüksége lesz a nevet a következőként: "[ResourceType] ResourceName" formátumban.</span><span class="sxs-lookup"><span data-stu-id="81804-114">Like the **DependsOn** keyword, you will need to format the name as "[ResourceType]ResourceName".</span></span> <span data-ttu-id="81804-115">Ha az erőforrás tartozik egy külön [konfigurációs](configurations.md), például a **ConfigurationName** a formázott karakterlánc "[ResourceType] ResourceName:: [ConfigurationName]:: [ConfigurationName]".</span><span class="sxs-lookup"><span data-stu-id="81804-115">If the resource belongs to a separate [Configuration](configurations.md), include the **ConfigurationName** in the formatted string "[ResourceType]ResourceName::[ConfigurationName]::[ConfigurationName]".</span></span> <span data-ttu-id="81804-116">A **csomópontnév** a számítógép vagy a csomópont, amelyen az aktuális erőforrás várnia kell.</span><span class="sxs-lookup"><span data-stu-id="81804-116">The **NodeName** is the computer, or Node, on which the current resource should wait.</span></span>

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

<span data-ttu-id="81804-117">A **WaitForSome** erőforrás a fenti példában egy hasonló szintaxissal rendelkezik, de hozzáadja a **NodeCount** kulcsot.</span><span class="sxs-lookup"><span data-stu-id="81804-117">The **WaitForSome** resource has a similar syntax to the example above, but adds the **NodeCount** key.</span></span> <span data-ttu-id="81804-118">A **NodeCount** azt jelzi, hogy a várjon az aktuális erőforrás hány csomóponttal.</span><span class="sxs-lookup"><span data-stu-id="81804-118">The **NodeCount** indicates how many Nodes the current resource should wait on.</span></span>

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

<span data-ttu-id="81804-119">Az összes **WaitForXXXX** az alábbi szintaxissal kulcsok megoszthatja.</span><span class="sxs-lookup"><span data-stu-id="81804-119">All **WaitForXXXX** share the following syntax keys.</span></span>

<span data-ttu-id="81804-120">|  Vlastnost |}  Leírás || RetryIntervalSec |} Mielőtt újra próbálkozna másodpercek számát.</span><span class="sxs-lookup"><span data-stu-id="81804-120">|  Property  |  Description   | | RetryIntervalSec| The number of seconds before retrying.</span></span> <span data-ttu-id="81804-121">Minimum: 1. |} | RetryCount |} Az újrapróbálkozások maximális számát. |} | ThrottleLimit |} Egyidejű csatlakozás gépek száma.</span><span class="sxs-lookup"><span data-stu-id="81804-121">Minimum is 1.| | RetryCount| The maximum number of times to retry.| | ThrottleLimit| Number of machines to connect simultaneously.</span></span> <span data-ttu-id="81804-122">Alapértelmezett érték a `New-CimSession` alapértelmezett. |} |} DependsOn |} Azt jelzi, hogy a konfigurációt egy másik erőforrás futtatnia kell, mielőtt az erőforrás konfigurálva van.</span><span class="sxs-lookup"><span data-stu-id="81804-122">Default is `New-CimSession` default.| | DependsOn | Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="81804-123">További információkért lásd: [DependsOn](resource-depends-on.md)|| PsDscRunAsCredential |} Lásd: [DSC használata a felhasználói hitelesítő adatok](./runAsUser.md) |</span><span class="sxs-lookup"><span data-stu-id="81804-123">For more information, see [DependsOn](resource-depends-on.md)| | PsDscRunAsCredential | See [Using DSC with User Credentials](./runAsUser.md) |</span></span>


## <a name="using-waitforxxxx-resources"></a><span data-ttu-id="81804-124">WaitForXXXX erőforrások használata</span><span class="sxs-lookup"><span data-stu-id="81804-124">Using WaitForXXXX resources</span></span>

<span data-ttu-id="81804-125">Minden egyes **WaitForXXXX** erőforrás megvárja, amíg befejeződik a megadott csomópont a megadott erőforrások.</span><span class="sxs-lookup"><span data-stu-id="81804-125">Each **WaitForXXXX** resource waits for the specified resources to complete on the specified Node.</span></span> <span data-ttu-id="81804-126">Ugyanazt a konfigurációt más erőforrások is majd *függenek* a **WaitForXXXX** erőforrást a **DependsOn** kulcsot.</span><span class="sxs-lookup"><span data-stu-id="81804-126">Other resources in the same Configuration can then *depend on* the **WaitForXXXX** resource using the **DependsOn** key.</span></span>

<span data-ttu-id="81804-127">Például a következő konfigurációban a célcsomópont várakozik a **xADDomain** erőforrás a befejezéséhez a **MyDC** legfeljebb 30-csomópont újrapróbálkozik, 15 másodperces intervallumon előtt a Célcsomópont csatlakozhat a tartományhoz.</span><span class="sxs-lookup"><span data-stu-id="81804-127">For example, in the following configuration, the target node is waiting for the **xADDomain** resource to finish on the **MyDC** node with maximum number of 30 retries, at 15-second intervals, before the target node can join the domain.</span></span>

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

<span data-ttu-id="81804-128">Konfiguráció fordítása, amikor két ".mof" fájlok jönnek létre.</span><span class="sxs-lookup"><span data-stu-id="81804-128">When you compile the Configuration, two ".mof" files are generated.</span></span> <span data-ttu-id="81804-129">".Mof" fájlok egyaránt vonatkozik a célcsomópontokat, használja a [Start-DSCConfiguration](/powershell/module/psdesiredstateconfiguration/start-dscconfiguration) parancsmag</span><span class="sxs-lookup"><span data-stu-id="81804-129">Apply both ".mof" files to the target Nodes using the [Start-DSCConfiguration](/powershell/module/psdesiredstateconfiguration/start-dscconfiguration) cmdlet</span></span>

><span data-ttu-id="81804-130">**Megjegyzés:** A WaitForXXX alapértelmezés szerint az erőforrások próbálja meg egyszer, és akkor sikertelen.</span><span class="sxs-lookup"><span data-stu-id="81804-130">**Note:** By default the WaitForXXX resources try one time and then fail.</span></span> <span data-ttu-id="81804-131">Bár ez nem szükséges, általában célszerű adjon meg egy **RetryCount** és **RetryIntervalSec**.</span><span class="sxs-lookup"><span data-stu-id="81804-131">Although it is not required, you will typically want to specify a **RetryCount** and **RetryIntervalSec**.</span></span>

## <a name="see-also"></a><span data-ttu-id="81804-132">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="81804-132">See Also</span></span>

- [<span data-ttu-id="81804-133">DSC-konfigurációk</span><span class="sxs-lookup"><span data-stu-id="81804-133">DSC Configurations</span></span>](configurations.md)
- [<span data-ttu-id="81804-134">Erőforrás-függőségek használatára</span><span class="sxs-lookup"><span data-stu-id="81804-134">Use Resource Dependencies</span></span>](resource-depends-on.md)
- [<span data-ttu-id="81804-135">DSC-erőforrások</span><span class="sxs-lookup"><span data-stu-id="81804-135">DSC Resources</span></span>](../resources/resources.md)
- [<span data-ttu-id="81804-136">A helyi Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="81804-136">Configuring The Local Configuration Manager</span></span>](../managing-nodes/metaConfig.md)
