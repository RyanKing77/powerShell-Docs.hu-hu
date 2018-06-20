---
ms.date: 06/12/2017
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: Csomópontok közötti függőségek megadása
ms.openlocfilehash: c1802d6baa1f2b3449603e0374a83e213abf598e
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/17/2018
ms.locfileid: "34218620"
---
# <a name="specifying-cross-node-dependencies"></a><span data-ttu-id="14395-103">Csomópontok közötti függőségek megadása</span><span class="sxs-lookup"><span data-stu-id="14395-103">Specifying cross-node dependencies</span></span>

> <span data-ttu-id="14395-104">Vonatkozik: A Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="14395-104">Applies To: Windows PowerShell 5.0</span></span>

<span data-ttu-id="14395-105">A DSC különleges forrásanyagokat biztosít az **WaitForAll**, **WaitForAny**, és **WaitForSome** , amely használható a konfigurációk függőségek határozza meg az egyéb konfigurációk csomópontok.</span><span class="sxs-lookup"><span data-stu-id="14395-105">DSC provides special resources, **WaitForAll**, **WaitForAny**, and **WaitForSome** that can be used in configurations to specify dependencies on configurations on other nodes.</span></span> <span data-ttu-id="14395-106">Ezeket az erőforrásokat viselkedése a következőképpen történik:</span><span class="sxs-lookup"><span data-stu-id="14395-106">The behavior of these resources is as follows:</span></span>

* <span data-ttu-id="14395-107">**WaitForAll**: sikeres lesz, ha a megadott erőforrás definiált összes cél csomóponton megfelelő állapotban a **csomópontnév** tulajdonság.</span><span class="sxs-lookup"><span data-stu-id="14395-107">**WaitForAll**: Succeeds if the specified resource is in the desired state on all target nodes defined in the **NodeName** property.</span></span>
* <span data-ttu-id="14395-108">**WaitForAny**: sikeres lesz, ha a megadott erőforrás a célcsomópontokat definiált legalább egyikének megfelelő állapotban a **csomópontnév** tulajdonság.</span><span class="sxs-lookup"><span data-stu-id="14395-108">**WaitForAny**: Succeeds if the specified resource is in the desired state on at least one of the target nodes defined in the **NodeName** property.</span></span>
* <span data-ttu-id="14395-109">**WaitForSome**: Adja meg a **NodeCount** kívül tulajdonságának egy **csomópontnév** tulajdonság.</span><span class="sxs-lookup"><span data-stu-id="14395-109">**WaitForSome**: Specifies a **NodeCount** property in addition to a **NodeName** property.</span></span> <span data-ttu-id="14395-110">Az erőforrás sikeres lesz, ha az erőforrás a megfelelő állapotban a csomópontok minimális száma (által megadott **NodeCount**) határozzák meg a **csomópontnév** tulajdonság.</span><span class="sxs-lookup"><span data-stu-id="14395-110">The resource succeeds if the resource is in the desired state on a minimum number of nodes (specified by **NodeCount**) defined by the **NodeName** property.</span></span>

## <a name="using-waitforxxxx-resources"></a><span data-ttu-id="14395-111">WaitForXXXX erőforrások használata</span><span class="sxs-lookup"><span data-stu-id="14395-111">Using WaitForXXXX resources</span></span>

<span data-ttu-id="14395-112">Használatához a **WaitForXXXX** erőforrások, létrehozhat egy erőforrás adatblokk, amelyben a DSC-erőforrás és a csomópontokon történő várakozás az erőforrás típusát.</span><span class="sxs-lookup"><span data-stu-id="14395-112">To use the **WaitForXXXX** resources, you create a resource block of that resource type that specifies the DSC resource and node(s) to wait for.</span></span> <span data-ttu-id="14395-113">Ezután a **DependsOn** bármely egyéb erőforrásokat a tulajdonság a konfigurációját, és várja meg a megadott feltételek tárolt metaadatblokkok a **WaitForXXXX** sikeres csomópont.</span><span class="sxs-lookup"><span data-stu-id="14395-113">You then use the **DependsOn** property in any other resource blocks in your configuration to wait for the conditions specified in the **WaitForXXXX** node to succeed.</span></span>

<span data-ttu-id="14395-114">Például a következő konfiguráció célcsomóponton arra vár, hogy a **xADDomain** erőforrás a befejezéséhez a **MyDC** legfeljebb 30-csomópont újrapróbálkozik, 15 másodperces időközönként, mielőtt a célcsomóponttal csatlakozhat a tartományhoz.</span><span class="sxs-lookup"><span data-stu-id="14395-114">For example, in the following configuration, the target node is waiting for the **xADDomain** resource to finish on the **MyDC** node with maximum number of 30 retries, at 15-second intervals, before the target node can join the domain.</span></span>

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

><span data-ttu-id="14395-115">**Megjegyzés:** a WaitForXXX alapértelmezés szerint erőforrások próbálja egyszer, és akkor sikertelen.</span><span class="sxs-lookup"><span data-stu-id="14395-115">**Note:** By default the WaitForXXX resources try one time and then fail.</span></span> <span data-ttu-id="14395-116">Bár nem kötelező, általában célszerű a újrapróbálkozási időköz és számának megadása.</span><span class="sxs-lookup"><span data-stu-id="14395-116">Although it is not required, you will typically want to specify a retry interval and count.</span></span>

## <a name="see-also"></a><span data-ttu-id="14395-117">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="14395-117">See Also</span></span>
* [<span data-ttu-id="14395-118">A DSC-konfigurációk</span><span class="sxs-lookup"><span data-stu-id="14395-118">DSC Configurations</span></span>](configurations.md)
* [<span data-ttu-id="14395-119">A DSC-erőforrások</span><span class="sxs-lookup"><span data-stu-id="14395-119">DSC Resources</span></span>](resources.md)
* [<span data-ttu-id="14395-120">A helyi Configuration Manager konfigurálása</span><span class="sxs-lookup"><span data-stu-id="14395-120">Configuring The Local Configuration Manager</span></span>](metaConfig.md)