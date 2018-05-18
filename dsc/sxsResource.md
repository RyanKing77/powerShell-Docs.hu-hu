---
ms.date: 06/12/2017
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: Eltérő verziójú erőforrások használata
ms.openlocfilehash: 6400d6506106657ba28fa1f9c83d9f8ee1c93ba3
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/16/2018
---
# <a name="using-resources-with-multiple-versions"></a><span data-ttu-id="3e07b-103">Eltérő verziójú erőforrások használata</span><span class="sxs-lookup"><span data-stu-id="3e07b-103">Using resources with multiple versions</span></span>

> <span data-ttu-id="3e07b-104">Vonatkozik: A Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="3e07b-104">Applies To: Windows PowerShell 5.0</span></span>

<span data-ttu-id="3e07b-105">PowerShell 5.0-s DSC erőforrások több verziója is van, és verziók is telepíthető egy számítógép-mellé.</span><span class="sxs-lookup"><span data-stu-id="3e07b-105">In PowerShell 5.0, DSC resources can have multiple versions, and versions can be installed on a computer side-by-side.</span></span> <span data-ttu-id="3e07b-106">Ez történik, azzal, hogy egy erőforrás-modul több verziója modul azonos mappában találhatók.</span><span class="sxs-lookup"><span data-stu-id="3e07b-106">This is implemented by having multiple versions of a resource module that are contained in the same module folder.</span></span>

## <a name="installing-multiple-resource-versions-side-by-side"></a><span data-ttu-id="3e07b-107">Több erőforrás verziók-párhuzamos telepítése</span><span class="sxs-lookup"><span data-stu-id="3e07b-107">Installing multiple resource versions side-by-side</span></span>

<span data-ttu-id="3e07b-108">Használhatja a **MinimumVersion**, **MaximumVersion**, és **RequiredVersion** paraméterei a [Install-modul](https://technet.microsoft.com/library/dn807162.aspx) parancsmag használatával adja meg a modul telepítése melyik verzióját.</span><span class="sxs-lookup"><span data-stu-id="3e07b-108">You can use the **MinimumVersion**, **MaximumVersion**, and **RequiredVersion** parameters of the [Install-Module](https://technet.microsoft.com/library/dn807162.aspx) cmdlet to specify which version of a module to install.</span></span> <span data-ttu-id="3e07b-109">Hívása **Install-modul** egy verziót telepíti a legújabb verziót megadása nélkül.</span><span class="sxs-lookup"><span data-stu-id="3e07b-109">Calling **Install-Module** without specifying a version installs the most recent version.</span></span>

<span data-ttu-id="3e07b-110">Például több verziója van a **xFailOverCluster** modult tartalmaz, amelyek mindegyike egy **xCluster** kívánt erőforrás.</span><span class="sxs-lookup"><span data-stu-id="3e07b-110">For example, there are multiple versions of the **xFailOverCluster** module, each of which contains an **xCluster** resouce.</span></span> <span data-ttu-id="3e07b-111">A hívás eredménye **Install-modul** nélkül a verzió megadása számot a következőképpen történik:</span><span class="sxs-lookup"><span data-stu-id="3e07b-111">The result of calling **Install-Module** without specifying the version number is as follows:</span></span>

```powershell
C:\Program Files\WindowsPowerShell\Modules\xFailOverCluster> Install-Module xFailOverCluster
C:\Program Files\WindowsPowerShell\Modules\xFailOverCluster> Get-DscResource xCluster

ImplementedAs   Name                      ModuleName                     Version    Properties
-------------   ----                      ----------                     -------    ----------
PowerShell      xCluster                  xFailOverCluster               1.2.0.0    {DomainAdministratorCredential, ...
```

<span data-ttu-id="3e07b-112">Most, ha meghívja a **Install-modul** ebben az esetben adja meg, de egy **RequiredVersion** 1.1.0.0-s, az azt eredményezi, a következő:</span><span class="sxs-lookup"><span data-stu-id="3e07b-112">Now, if you call **Install-Module** again, but specify a **RequiredVersion** of 1.1.0.0, it results in the following:</span></span>

```powershell
C:\Program Files\WindowsPowerShell\Modules\xFailOverCluster> Install-Module xFailOverCluster -RequiredVersion 1.1
C:\Program Files\WindowsPowerShell\Modules\xFailOverCluster> Get-DscResource xCluster

ImplementedAs   Name                      ModuleName                     Version    Properties
-------------   ----                      ----------                     -------    ----------
PowerShell      xCluster                  xFailOverCluster               1.1        {DomainAdministratorCredential, Name, ...
PowerShell      xCluster                  xFailOverCluster               1.2.0.0    {DomainAdministratorCredential, Name, ...
```

## <a name="specifying-a-resource-version-in-a-configuration"></a><span data-ttu-id="3e07b-113">Adja meg egy erőforrás-verziója konfigurációban</span><span class="sxs-lookup"><span data-stu-id="3e07b-113">Specifying a resource version in a configuration</span></span>

<span data-ttu-id="3e07b-114">Ha egy számítógépen több erőforrást, konfiguráció használatakor meg kell adnia az adott erőforrás verziója.</span><span class="sxs-lookup"><span data-stu-id="3e07b-114">If you have multiple resources installed on a computer, you must specify the version of that resource when you use it in a configuration.</span></span> <span data-ttu-id="3e07b-115">Ehhez adja meg a **ModuleVersion** paramétere a **Import-DscResource** kulcsszó.</span><span class="sxs-lookup"><span data-stu-id="3e07b-115">You do this by specifying the **ModuleVersion** parameter of the **Import-DscResource** keyword.</span></span> <span data-ttu-id="3e07b-116">Ha nem adja meg egy erőforrás-modul egy erőforrást, amelyek több verziója telepítve van a verziója, a konfigurációs hibát generál.</span><span class="sxs-lookup"><span data-stu-id="3e07b-116">If you fail to specify the version of a resource module of a resource of which you have more than one version installed, the configuration generates an error.</span></span>

<span data-ttu-id="3e07b-117">A következő konfigurációs adja meg az erőforrás hívására verzióját mutatja be:</span><span class="sxs-lookup"><span data-stu-id="3e07b-117">The following configuration shows how to specify the version of the resource to call:</span></span>

```powershell
configuration VersionTest
{
    Import-DscResource -ModuleName xFailOverCluster -ModuleVersion 1.1

    Node 'localhost'
    {
       xCluster ClusterTest
       {
            Name                          = 'TestCluster'
            StaticIPAddress               = '10.0.0.3'
            DomainAdministratorCredential = Get-Credential
        }
     }
}
```

><span data-ttu-id="3e07b-118">Megjegyzés: Az Import-DscResource ModuleVersion paramétere nem érhető el a PowerShell 4.0.</span><span class="sxs-lookup"><span data-stu-id="3e07b-118">Note: The ModuleVersion parameter of Import-DscResource is not available in PowerShell 4.0.</span></span> <span data-ttu-id="3e07b-119">A PowerShell 4.0-s adjon meg egy modul verziót úgy, hogy egy modul specification objektum importálási-DscResource ModuleName paraméterének.</span><span class="sxs-lookup"><span data-stu-id="3e07b-119">In PowerShell 4.0, you can specify a module version by passing a module specification object to the ModuleName parameter of Import-DscResource.</span></span> <span data-ttu-id="3e07b-120">A modul specification objektum egy kivonattáblát a modulnév és RequiredVersion kulcsot tartalmazó.</span><span class="sxs-lookup"><span data-stu-id="3e07b-120">A module specification object is a hash table that contains ModuleName and RequiredVersion  keys.</span></span> <span data-ttu-id="3e07b-121">Például:</span><span class="sxs-lookup"><span data-stu-id="3e07b-121">For example:</span></span>

```powershell
configuration VersionTest
{
    Import-DscResource -ModuleName (@{ModuleName='xFailOverCluster'; RequiredVersion='1.1'} )

    Node 'localhost'
    {
       xCluster ClusterTest
       {
            Name                          = 'TestCluster'
            StaticIPAddress               = '10.0.0.3'
            DomainAdministratorCredential = Get-Credential
        }
     }
}
```

<span data-ttu-id="3e07b-122">Ez is PowerShell 5.0 fog működni, de javasoljuk, hogy használja a **ModuleVersion** paraméter.</span><span class="sxs-lookup"><span data-stu-id="3e07b-122">This will also work in PowerShell 5.0, but it is recommended that you use the **ModuleVersion** parameter.</span></span>

## <a name="see-also"></a><span data-ttu-id="3e07b-123">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="3e07b-123">See also</span></span>
* [<span data-ttu-id="3e07b-124">A DSC-konfigurációk</span><span class="sxs-lookup"><span data-stu-id="3e07b-124">DSC Configurations</span></span>](configurations.md)
* [<span data-ttu-id="3e07b-125">A DSC-erőforrások</span><span class="sxs-lookup"><span data-stu-id="3e07b-125">DSC Resources</span></span>](resources.md)