---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: Telepített erőforrás meghatározott verziójának importálása
ms.openlocfilehash: 5ed81e11aa67eb6590d958647f48a33b1b5f1c0e
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62079999"
---
# <a name="import-a-specific-version-of-an-installed-resource"></a><span data-ttu-id="a36cb-103">Telepített erőforrás meghatározott verziójának importálása</span><span class="sxs-lookup"><span data-stu-id="a36cb-103">Import a specific version of an installed resource</span></span>

> <span data-ttu-id="a36cb-104">A következőkre vonatkozik: Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="a36cb-104">Applies To: Windows PowerShell 5.0</span></span>

<span data-ttu-id="a36cb-105">A PowerShell 5.0-DSC-erőforrások különböző verzióit egy számítógép egymás mellett telepíthető.</span><span class="sxs-lookup"><span data-stu-id="a36cb-105">In PowerShell 5.0, separate versions of DSC resources can be installed on a computer side by side.</span></span> <span data-ttu-id="a36cb-106">Egy resource modul erőforrás külön verziói tárolhat mappák nevű verziója.</span><span class="sxs-lookup"><span data-stu-id="a36cb-106">A resource module can store separate versions of a resource in version named folders.</span></span>

## <a name="installing-separate-resource-versions-side-by-side"></a><span data-ttu-id="a36cb-107">Külön erőforrást verziók egymás melletti telepítése</span><span class="sxs-lookup"><span data-stu-id="a36cb-107">Installing separate resource versions side by side</span></span>

<span data-ttu-id="a36cb-108">Használhatja a **MinimumVersion**, **MaximumVersion**, és **RequiredVersion** paramétereit a [Install-Module](/powershell/module/PowershellGet/Install-Module) parancsmag használatával adja meg melyik verzió modulok telepítéséhez.</span><span class="sxs-lookup"><span data-stu-id="a36cb-108">You can use the **MinimumVersion**, **MaximumVersion**, and **RequiredVersion** parameters of the [Install-Module](/powershell/module/PowershellGet/Install-Module) cmdlet to specify which version of a module to install.</span></span> <span data-ttu-id="a36cb-109">Hívó **Install-Module** verziót telepíti a legújabb verzió megadása nélkül.</span><span class="sxs-lookup"><span data-stu-id="a36cb-109">Calling **Install-Module** without specifying a version installs the most recent version.</span></span>

<span data-ttu-id="a36cb-110">Például, nincsenek különböző verzióinak a **xFailOverCluster** modult, amelyek mindegyike tartalmaz egy **xCluster** erőforrás.</span><span class="sxs-lookup"><span data-stu-id="a36cb-110">For example, there are multiple versions of the **xFailOverCluster** module, each of which contains an **xCluster** resource.</span></span> <span data-ttu-id="a36cb-111">Hívó **Install-Module** a verzió megadása nélkül száma a modul legújabb verzióját telepíti.</span><span class="sxs-lookup"><span data-stu-id="a36cb-111">Calling **Install-Module** without specifying the version number installs the most recent version of the module.</span></span>

```powershell
PS> Install-Module xFailOverCluster
PS> Get-DscResource xCluster
```

```output
ImplementedAs   Name                      ModuleName                     Version    Properties
-------------   ----                      ----------                     -------    ----------
PowerShell      xCluster                  xFailOverCluster               1.2.0.0    {DomainAdministratorCredential, ...
```

<span data-ttu-id="a36cb-112">Egy adott verzióját egy modul telepítéséhez, adja meg egy **RequiredVersion** 1.1.0.0-s az.</span><span class="sxs-lookup"><span data-stu-id="a36cb-112">To install a specific version of a module, specify a **RequiredVersion** of 1.1.0.0.</span></span> <span data-ttu-id="a36cb-113">Ez telepíti a megadott verzióját, a telepített verzió párhuzamosan lesz.</span><span class="sxs-lookup"><span data-stu-id="a36cb-113">This installs the specified version side by side with the installed version.</span></span>

```powershell
PS> Install-Module xFailOverCluster -RequiredVersion 1.1
```

<span data-ttu-id="a36cb-114">Most meg kell jelennie mindkét modul verziójának használatakor felsorolt `Get-DSCResource`.</span><span class="sxs-lookup"><span data-stu-id="a36cb-114">Now, you see both version of the module listed when you use `Get-DSCResource`.</span></span>

```powershell
PS> Get-DscResource xCluster
```

```output
ImplementedAs   Name                      ModuleName                     Version    Properties
-------------   ----                      ----------                     -------    ----------
PowerShell      xCluster                  xFailOverCluster               1.1        {DomainAdministratorCredential, Name, ...
PowerShell      xCluster                  xFailOverCluster               1.2.0.0    {DomainAdministratorCredential, Name, ...
```

## <a name="specifying-a-resource-version-in-a-configuration"></a><span data-ttu-id="a36cb-115">Erőforrás-verzió megadása az konfiguráció</span><span class="sxs-lookup"><span data-stu-id="a36cb-115">Specifying a resource version in a configuration</span></span>

<span data-ttu-id="a36cb-116">Ha rendelkezik a számítógépen telepített külön erőforrást verziók, adjon meg a verziót az erőforrás-konfiguráció használatakor.</span><span class="sxs-lookup"><span data-stu-id="a36cb-116">If you have separate resource versions installed on a computer, you must specify the version of that resource when you use it in a configuration.</span></span> <span data-ttu-id="a36cb-117">Adjon meg ehhez a **ModuleVersion** paraméterében a **Import-DscResource** kulcsszó.</span><span class="sxs-lookup"><span data-stu-id="a36cb-117">You do this by specifying the **ModuleVersion** parameter of the **Import-DscResource** keyword.</span></span> <span data-ttu-id="a36cb-118">Ha nem adja meg, amelyek egynél több verziója telepítve van egy adott erőforrás erőforrás modul verzióját, a konfigurációs hibát jelez.</span><span class="sxs-lookup"><span data-stu-id="a36cb-118">If you fail to specify the version of a resource module of a resource of which you have more than one version installed, the configuration generates an error.</span></span>

<span data-ttu-id="a36cb-119">A következő konfigurációt mutatja be, adja meg a verziót az erőforrás meghívásához:</span><span class="sxs-lookup"><span data-stu-id="a36cb-119">The following configuration shows how to specify the version of the resource to call:</span></span>

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

><span data-ttu-id="a36cb-120">Megjegyzés: Az Import-DscResource-ModuleVersion paramétert a PowerShell 4.0-s nem érhető el.</span><span class="sxs-lookup"><span data-stu-id="a36cb-120">Note: The ModuleVersion parameter of Import-DscResource is not available in PowerShell 4.0.</span></span> <span data-ttu-id="a36cb-121">A PowerShell 4.0-s adjon meg egy modul verziót az Import-DscResource ModuleName paraméterének egy modul specifikáció objektum átadásával.</span><span class="sxs-lookup"><span data-stu-id="a36cb-121">In PowerShell 4.0, you can specify a module version by passing a module specification object to the ModuleName parameter of Import-DscResource.</span></span> <span data-ttu-id="a36cb-122">Egy modul specifikáció objektum ModuleName és RequiredVersion kulcsokat tartalmazó kivonattáblát.</span><span class="sxs-lookup"><span data-stu-id="a36cb-122">A module specification object is a hash table that contains ModuleName and RequiredVersion  keys.</span></span> <span data-ttu-id="a36cb-123">Például:</span><span class="sxs-lookup"><span data-stu-id="a36cb-123">For example:</span></span>

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

<span data-ttu-id="a36cb-124">Ez a PowerShell 5.0 is fog működni, de javasoljuk, hogy használja a **ModuleVersion** paraméter.</span><span class="sxs-lookup"><span data-stu-id="a36cb-124">This will also work in PowerShell 5.0, but it is recommended that you use the **ModuleVersion** parameter.</span></span>

## <a name="see-also"></a><span data-ttu-id="a36cb-125">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="a36cb-125">See also</span></span>

- [<span data-ttu-id="a36cb-126">DSC-konfigurációk</span><span class="sxs-lookup"><span data-stu-id="a36cb-126">DSC Configurations</span></span>](configurations.md)
- [<span data-ttu-id="a36cb-127">DSC-erőforrások</span><span class="sxs-lookup"><span data-stu-id="a36cb-127">DSC Resources</span></span>](../resources/resources.md)
