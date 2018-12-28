---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: A DSC folyamatos integrációt és folyamatos üzembe helyezési folyamat felépítésével bajlódnia
ms.openlocfilehash: c305d9bc7e0f8c659129b5a20d0b7e8b34d09ba8
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/14/2018
ms.locfileid: "53404376"
---
# <a name="building-a-continuous-integration-and-continuous-deployment-pipeline-with-dsc"></a><span data-ttu-id="982fb-103">A DSC folyamatos integrációt és folyamatos üzembe helyezési folyamat felépítésével bajlódnia</span><span class="sxs-lookup"><span data-stu-id="982fb-103">Building a Continuous Integration and Continuous Deployment pipeline with DSC</span></span>

<span data-ttu-id="982fb-104">Ez a példa bemutatja, hogyan hozhat létre egy folyamatos integráció/folyamatos üzembe helyezés (CI/CD) folyamatot a PowerShell, DSC, a Pester és a Visual Studio Team Foundation Server (TFS) használatával.</span><span class="sxs-lookup"><span data-stu-id="982fb-104">This example demonstrates how to build a Continuous Integration/Continuous Deployment (CI/CD) pipeline by using PowerShell, DSC, Pester, and Visual Studio Team Foundation Server (TFS).</span></span>

<span data-ttu-id="982fb-105">Miután a folyamat beépített és konfigurálva van, ennek segítségével teljes mértékben központi telepítése, konfigurálása és tesztelése a DNS-kiszolgáló, és állomásrekordokat kapcsolódó.</span><span class="sxs-lookup"><span data-stu-id="982fb-105">After the pipeline is built and configured, you can use it to fully deploy, configure and test a DNS server and associated host records.</span></span>
<span data-ttu-id="982fb-106">Ez a folyamat egy fejlesztési környezetben használni kívánt folyamat első részének szimulálja.</span><span class="sxs-lookup"><span data-stu-id="982fb-106">This process simulates the first part of a pipeline that would be used in a development environment.</span></span>

<span data-ttu-id="982fb-107">Egy automatizált CI/CD-folyamat segítségével gyorsabban szoftverek frissítése és megbízhatóan, biztosítva, hogy az összes kód lett tesztelve, és hogy a kód aktuális build mindenkor.</span><span class="sxs-lookup"><span data-stu-id="982fb-107">An automated CI/CD pipeline helps you update software faster and more reliably, ensuring that all code is tested, and that a current build of your code is available at all times.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="982fb-108">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="982fb-108">Prerequisites</span></span>

<span data-ttu-id="982fb-109">Ebben a példában használatához ismernie kell a következőkkel:</span><span class="sxs-lookup"><span data-stu-id="982fb-109">To use this example, you should be familiar with the following:</span></span>

- <span data-ttu-id="982fb-110">CI-CD fogalmakat.</span><span class="sxs-lookup"><span data-stu-id="982fb-110">CI-CD concepts.</span></span> <span data-ttu-id="982fb-111">Útmutatással található [a kiadási adatfolyamat-modell](http://aka.ms/thereleasepipelinemodelpdf).</span><span class="sxs-lookup"><span data-stu-id="982fb-111">A good reference can be found at [The Release Pipeline Model](http://aka.ms/thereleasepipelinemodelpdf).</span></span>
- <span data-ttu-id="982fb-112">[A Git](https://git-scm.com/) verziókövetés</span><span class="sxs-lookup"><span data-stu-id="982fb-112">[Git](https://git-scm.com/) source control</span></span>
- <span data-ttu-id="982fb-113">A [Pester](https://github.com/pester/Pester) tesztelési keretrendszerének</span><span class="sxs-lookup"><span data-stu-id="982fb-113">The [Pester](https://github.com/pester/Pester) testing framework</span></span>
- [<span data-ttu-id="982fb-114">A Team Foundation Server</span><span class="sxs-lookup"><span data-stu-id="982fb-114">Team Foundation Server</span></span>](https://www.visualstudio.com/tfs/)

## <a name="what-you-will-need"></a><span data-ttu-id="982fb-115">Mit kell</span><span class="sxs-lookup"><span data-stu-id="982fb-115">What you will need</span></span>

<span data-ttu-id="982fb-116">Hozza létre, és futtassa az ebben a példában, szüksége lesz számos számítógépek és/vagy virtuális gépek környezet.</span><span class="sxs-lookup"><span data-stu-id="982fb-116">To build and run this example, you will need an environment with several computers and/or virtual machines.</span></span>

### <a name="client"></a><span data-ttu-id="982fb-117">Ügyfél</span><span class="sxs-lookup"><span data-stu-id="982fb-117">Client</span></span>

<span data-ttu-id="982fb-118">Ez az a számítógépen, ahol teheti meg az összes beállíthatja és futtathatja a példa a munkahelyi.</span><span class="sxs-lookup"><span data-stu-id="982fb-118">This is the computer where you'll do all of the work setting up and running the example.</span></span>

<span data-ttu-id="982fb-119">Az ügyfélszámítógépen kell telepíteni az alábbi Windows számítógép:</span><span class="sxs-lookup"><span data-stu-id="982fb-119">The client computer must be a Windows computer with the following installed:</span></span>

- [<span data-ttu-id="982fb-120">a git</span><span class="sxs-lookup"><span data-stu-id="982fb-120">Git</span></span>](https://git-scm.com/)
- <span data-ttu-id="982fb-121">klónozza a helyi git-adattár https://github.com/PowerShell/Demo_CI</span><span class="sxs-lookup"><span data-stu-id="982fb-121">a local git repo cloned from https://github.com/PowerShell/Demo_CI</span></span>
- <span data-ttu-id="982fb-122">egy szövegszerkesztőben, például [Visual Studio Code](https://code.visualstudio.com/)</span><span class="sxs-lookup"><span data-stu-id="982fb-122">a text editor, such as [Visual Studio Code](https://code.visualstudio.com/)</span></span>

### <a name="tfssrv1"></a><span data-ttu-id="982fb-123">TFSSrv1</span><span class="sxs-lookup"><span data-stu-id="982fb-123">TFSSrv1</span></span>

<span data-ttu-id="982fb-124">A számítógép, amelyen a TFS-kiszolgálónak, ahol a build meghatározzuk és kiadása.</span><span class="sxs-lookup"><span data-stu-id="982fb-124">The computer that hosts the TFS server where you will define your build and release.</span></span>
<span data-ttu-id="982fb-125">Ezen a számítógépen telepítve kell [Team Foundation Server 2017](https://www.visualstudio.com/tfs/) telepítve.</span><span class="sxs-lookup"><span data-stu-id="982fb-125">This computer must have [Team Foundation Server 2017](https://www.visualstudio.com/tfs/) installed.</span></span>

### <a name="buildagent"></a><span data-ttu-id="982fb-126">BuildAgent</span><span class="sxs-lookup"><span data-stu-id="982fb-126">BuildAgent</span></span>

<span data-ttu-id="982fb-127">A számítógépen, amelyen a Windows ügynök, amely összeállítja a projekt létrehozása.</span><span class="sxs-lookup"><span data-stu-id="982fb-127">The computer that runs the Windows build agent that builds the project.</span></span>
<span data-ttu-id="982fb-128">Ez a számítógép rendelkeznie kell egy telepített és futó ügynök hozhat létre Windows.</span><span class="sxs-lookup"><span data-stu-id="982fb-128">This computer must have a Windows build agent installed and running.</span></span>
<span data-ttu-id="982fb-129">Lásd: [a Windows-ügynök telepítése](/azure/devops/pipelines/agents/v2-windows) való telepítése és futtatása egy Windows hozhat létre az ügynök számára.</span><span class="sxs-lookup"><span data-stu-id="982fb-129">See [Deploy an agent on Windows](/azure/devops/pipelines/agents/v2-windows) for instructions on how to install and run a Windows build agent.</span></span>

<span data-ttu-id="982fb-130">Alkalmazást is telepíteni kell a `xDnsServer` és `xNetworking` DSC-modulok ezen a számítógépen.</span><span class="sxs-lookup"><span data-stu-id="982fb-130">You also need to install both the `xDnsServer` and `xNetworking` DSC modules on this computer.</span></span>

### <a name="testagent1"></a><span data-ttu-id="982fb-131">TestAgent1</span><span class="sxs-lookup"><span data-stu-id="982fb-131">TestAgent1</span></span>

<span data-ttu-id="982fb-132">Ez az a számítógép, amely szerint ebben a példában a DSC-konfiguráció DNS-kiszolgálóként van konfigurálva.</span><span class="sxs-lookup"><span data-stu-id="982fb-132">This is the computer that is configured as a DNS server by the DSC configuration in this example.</span></span>
<span data-ttu-id="982fb-133">A számítógépen kell futnia [Windows Server 2016](https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2016).</span><span class="sxs-lookup"><span data-stu-id="982fb-133">The computer must be running [Windows Server 2016](https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2016).</span></span>

### <a name="testagent2"></a><span data-ttu-id="982fb-134">TestAgent2</span><span class="sxs-lookup"><span data-stu-id="982fb-134">TestAgent2</span></span>

<span data-ttu-id="982fb-135">Ez az a számítógép, amelyen a webhely, ez a példa konfigurálja.</span><span class="sxs-lookup"><span data-stu-id="982fb-135">This is the computer that hosts the website this example configures.</span></span>
<span data-ttu-id="982fb-136">A számítógépen kell futnia [Windows Server 2016](https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2016).</span><span class="sxs-lookup"><span data-stu-id="982fb-136">The computer must be running [Windows Server 2016](https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2016).</span></span>

## <a name="add-the-code-to-tfs"></a><span data-ttu-id="982fb-137">Adja hozzá a kódot a TFS</span><span class="sxs-lookup"><span data-stu-id="982fb-137">Add the code to TFS</span></span>

<span data-ttu-id="982fb-138">Hozunk egy Git-tárház létrehozása a TFS-ben, és a kód importálja a helyi tárház az ügyfélszámítógépen.</span><span class="sxs-lookup"><span data-stu-id="982fb-138">We'll start out by creating a Git repository in TFS, and importing the code from your local repository on the client computer.</span></span>
<span data-ttu-id="982fb-139">Ha nem rendelkezik már klónozta a Demo_CI tárházat az ügyfélszámítógépre tegye most a következő git-parancs futtatásával:</span><span class="sxs-lookup"><span data-stu-id="982fb-139">If you have not already cloned the Demo_CI repository to your client computer, do so now by running the following git command:</span></span>

`git clone https://github.com/PowerShell/Demo_CI`

1. <span data-ttu-id="982fb-140">Az ügyfélszámítógépen navigáljon a TFS-kiszolgáló egy webböngészőben.</span><span class="sxs-lookup"><span data-stu-id="982fb-140">On your client computer, navigate to your TFS server in a web browser.</span></span>
1. <span data-ttu-id="982fb-141">A TFS rendszerben [hozzon létre egy új csoportprojektet](/azure/devops/organizations/projects/create-project) Demo_CI nevű.</span><span class="sxs-lookup"><span data-stu-id="982fb-141">In TFS, [Create a new team project](/azure/devops/organizations/projects/create-project) named Demo_CI.</span></span>

   <span data-ttu-id="982fb-142">Győződjön meg arról, hogy **verziókövetés** értékre van állítva **Git**.</span><span class="sxs-lookup"><span data-stu-id="982fb-142">Make sure that **Version control** is set to **Git**.</span></span>
1. <span data-ttu-id="982fb-143">Az ügyfélszámítógépen adjon hozzá egy távoli a tárházban létrehozott a TFS-ben a következő paranccsal:</span><span class="sxs-lookup"><span data-stu-id="982fb-143">On your client computer, add a remote to the repository you just created in TFS with the following command:</span></span>

   `git remote add tfs <YourTFSRepoURL>`

   <span data-ttu-id="982fb-144">Ahol `<YourTFSRepoURL>` a TFS-tárházba az előző lépésben létrehozott klón URL-címe.</span><span class="sxs-lookup"><span data-stu-id="982fb-144">Where `<YourTFSRepoURL>` is the clone URL to the TFS repository you created in the previous step.</span></span>

   <span data-ttu-id="982fb-145">Ha nem tudja, hol találja az URL-címet, tekintse meg [egy meglévő Git-adattár klónozása](/azure/devops/repos/git/clone).</span><span class="sxs-lookup"><span data-stu-id="982fb-145">If you don't know where to find this URL, see [Clone an existing Git repo](/azure/devops/repos/git/clone).</span></span>
1. <span data-ttu-id="982fb-146">A kód a helyi adattárból leküldése a TFS-tárunkat, ahol a következő parancsot:</span><span class="sxs-lookup"><span data-stu-id="982fb-146">Push the code from your local repository to your TFS repository with the following command:</span></span>

   `git push tfs --all`
1. <span data-ttu-id="982fb-147">A TFS-tárház tölti fel a Demo_CI kódot.</span><span class="sxs-lookup"><span data-stu-id="982fb-147">The TFS repository will be populated with the Demo_CI code.</span></span>

> [!NOTE]
> <span data-ttu-id="982fb-148">Ez a példa lévő kódot az `ci-cd-example` a Git-adattár ágában.</span><span class="sxs-lookup"><span data-stu-id="982fb-148">This example uses the code in the `ci-cd-example` branch of the Git repo.</span></span>
> <span data-ttu-id="982fb-149">Ügyeljen arra, hogy ez az ág az alapértelmezett ágon, a TFS-projektben adja meg, és a CI/CD-eseményindítók létrehozásához.</span><span class="sxs-lookup"><span data-stu-id="982fb-149">Be sure to specify this branch as the default branch in your TFS project, and for the CI/CD triggers you create.</span></span>

## <a name="understanding-the-code"></a><span data-ttu-id="982fb-150">A kód ismertetése</span><span class="sxs-lookup"><span data-stu-id="982fb-150">Understanding the code</span></span>

<span data-ttu-id="982fb-151">A buildelési és üzembe helyezési folyamatok hozunk létre, mielőtt tekintsük át néhány a kódot, és ismerje meg, mi is történik.</span><span class="sxs-lookup"><span data-stu-id="982fb-151">Before we create the build and deployment pipelines, let's look at some of the code to understand what is going on.</span></span>
<span data-ttu-id="982fb-152">Az ügyfélszámítógépen nyissa meg a kedvenc szövegszerkesztőjével, és keresse meg a Demo_CI Git-tárház gyökérkönyvtárában.</span><span class="sxs-lookup"><span data-stu-id="982fb-152">On your client computer, open your favorite text editor and navigate to the root of your Demo_CI Git repository.</span></span>

### <a name="the-dsc-configuration"></a><span data-ttu-id="982fb-153">A DSC-konfiguráció</span><span class="sxs-lookup"><span data-stu-id="982fb-153">The DSC configuration</span></span>

<span data-ttu-id="982fb-154">Nyissa meg a fájlt `DNSServer.ps1` (a helyi Demo_CI tárház gyökérkönyvtárából `./InfraDNS/Configs/DNSServer.ps1`).</span><span class="sxs-lookup"><span data-stu-id="982fb-154">Open the file `DNSServer.ps1` (from the root of the local Demo_CI repository, `./InfraDNS/Configs/DNSServer.ps1`).</span></span>

<span data-ttu-id="982fb-155">Ez a fájl tartalmazza a DSC-konfiguráció, amely beállítja a DNS-kiszolgálót.</span><span class="sxs-lookup"><span data-stu-id="982fb-155">This file contains the DSC configuration that sets up the DNS server.</span></span> <span data-ttu-id="982fb-156">Itt van ebben az esetben:</span><span class="sxs-lookup"><span data-stu-id="982fb-156">Here it is in its entirety:</span></span>

```powershell
configuration DNSServer
{
    Import-DscResource -module 'xDnsServer','xNetworking', 'PSDesiredStateConfiguration'

    Node $AllNodes.Where{$_.Role -eq 'DNSServer'}.NodeName
    {
        WindowsFeature DNS
        {
            Ensure  = 'Present'
            Name    = 'DNS'
        }

        xDnsServerPrimaryZone $Node.zone
        {
            Ensure    = 'Present'
            Name      = $Node.Zone
            DependsOn = '[WindowsFeature]DNS'
        }

        foreach ($ARec in $Node.ARecords.keys) {
            xDnsRecord $ARec
            {
                Ensure    = 'Present'
                Name      = $ARec
                Zone      = $Node.Zone
                Type      = 'ARecord'
                Target    = $Node.ARecords[$ARec]
                DependsOn = '[WindowsFeature]DNS'
            }
        }

        foreach ($CName in $Node.CNameRecords.keys) {
            xDnsRecord $CName
            {
                Ensure    = 'Present'
                Name      = $CName
                Zone      = $Node.Zone
                Type      = 'CName'
                Target    = $Node.CNameRecords[$CName]
                DependsOn = '[WindowsFeature]DNS'
            }
        }
    }
}
```

<span data-ttu-id="982fb-157">Figyelje meg a `Node` utasítást:</span><span class="sxs-lookup"><span data-stu-id="982fb-157">Notice the `Node` statement:</span></span>

```powershell
Node $AllNodes.Where{$_.Role -eq 'DNSServer'}.NodeName
```

<span data-ttu-id="982fb-158">Ez olyan csomópontokat, hogy az egyik szerepköre, definiált megkeresi `DNSServer` a a [konfigurációs adatok](../configurations/configData.md), által létrehozott a `DevEnv.ps1` parancsfájlt.</span><span class="sxs-lookup"><span data-stu-id="982fb-158">This finds any nodes that were defined as having a role of `DNSServer` in the [configuration data](../configurations/configData.md), which is created by the `DevEnv.ps1` script.</span></span>

<span data-ttu-id="982fb-159">További információ a `Where` metódus az [about_arrays](/powershell/reference/3.0/Microsoft.PowerShell.Core/About/about_Arrays.md)</span><span class="sxs-lookup"><span data-stu-id="982fb-159">You can read more about the `Where` method in [about_arrays](/powershell/reference/3.0/Microsoft.PowerShell.Core/About/about_Arrays.md)</span></span>

<span data-ttu-id="982fb-160">Konfigurációs adatok segítségével határozza meg a csomópontok akkor fontos, ha ezzel a CI, mivel a csomópont-információk valószínűleg változni fognak a környezetek között, és a konfigurációs adatok használata lehetővé teszi, hogy egyszerűen módosításokat csomópontjának adatait a konfigurációs programkód módosítása nélkül.</span><span class="sxs-lookup"><span data-stu-id="982fb-160">Using configuration data to define nodes is important when doing CI because node information will likely change between environments, and using configuration data allows you to easily make changes to node information without changing the configuration code.</span></span>

<span data-ttu-id="982fb-161">Az első resource blokkban, a konfiguráció meghívja a **WindowsFeature** annak érdekében, hogy a DNS szolgáltatás engedélyezve van-e.</span><span class="sxs-lookup"><span data-stu-id="982fb-161">In the first resource block, the configuration calls the **WindowsFeature** to ensure that the DNS feature is enabled.</span></span>
<span data-ttu-id="982fb-162">Az erőforrás blokkokat hívás erőforrásokat, kövesse a [xDnsServer](https://github.com/PowerShell/xDnsServer) modul elsődleges zóna és a DNS-rekordok konfigurálása.</span><span class="sxs-lookup"><span data-stu-id="982fb-162">The resource blocks that follow call resources from the [xDnsServer](https://github.com/PowerShell/xDnsServer) module to configure the primary zone and DNS records.</span></span>

<span data-ttu-id="982fb-163">Figyelje meg, hogy a két `xDnsRecord` blokkok burkolja `foreach` , amely a konfigurációs adatokat a tömbök iterálódnak hurkokat.</span><span class="sxs-lookup"><span data-stu-id="982fb-163">Notice that the two `xDnsRecord` blocks are wrapped in `foreach` loops that iterate through arrays in the configuration data.</span></span>
<span data-ttu-id="982fb-164">A konfigurációs adatok létre újra, a `DevEnv.ps1` szkriptet, amely áttekintjük a Tovább gombra.</span><span class="sxs-lookup"><span data-stu-id="982fb-164">Again, the configuration data is created by the `DevEnv.ps1` script, which we'll look at next.</span></span>

### <a name="configuration-data"></a><span data-ttu-id="982fb-165">Konfigurációs adatok</span><span class="sxs-lookup"><span data-stu-id="982fb-165">Configuration data</span></span>

<span data-ttu-id="982fb-166">A `DevEnv.ps1` fájlt (a helyi Demo_CI tárház gyökérkönyvtárából `./InfraDNS/DevEnv.ps1`) egy kivonattáblát határozza meg az adott környezetre vonatkozó konfigurációs adatokat, és ezután továbbítja a kivonattábla kulcsa hívása a `New-DscConfigurationDataDocument` függvény, amelyet a `DscPipelineTools.psm` (`./Assets/DscPipelineTools/DscPipelineTools.psm1`).</span><span class="sxs-lookup"><span data-stu-id="982fb-166">The `DevEnv.ps1` file (from the root of the local Demo_CI repository, `./InfraDNS/DevEnv.ps1`) specifies the environment-specific configuration data in a hashtable, and then passes that hashtable to a call to the `New-DscConfigurationDataDocument` function, which is defined in `DscPipelineTools.psm` (`./Assets/DscPipelineTools/DscPipelineTools.psm1`).</span></span>

<span data-ttu-id="982fb-167">A `DevEnv.ps1` fájlt:</span><span class="sxs-lookup"><span data-stu-id="982fb-167">The `DevEnv.ps1` file:</span></span>

```powershell
param(
    [parameter(Mandatory=$true)]
    [string]
    $OutputPath
)

Import-Module $PSScriptRoot\..\Assets\DscPipelineTools\DscPipelineTools.psd1 -Force

# Define Unit Test Environment
$DevEnvironment = @{
    Name                        = 'DevEnv';
    Roles = @(
        @{  Role                = 'DNSServer';
            VMName              = 'TestAgent1';
            Zone                = 'Contoso.com';
            ARecords            = @{'TFSSrv1'= '10.0.0.10';'Client'='10.0.0.15';'BuildAgent'='10.0.0.30';'TestAgent1'='10.0.0.40';'TestAgent2'='10.0.0.50'};
            CNameRecords        = @{'DNS' = 'TestAgent1.contoso.com'};
        }
    )
}

Return New-DscConfigurationDataDocument -RawEnvData $DevEnvironment -OutputPath $OutputPath
```

<span data-ttu-id="982fb-168">A `New-DscConfigurationDataDocument` függvény (meghatározott `\Assets\DscPipelineTools\DscPipelineTools.psm1`) programozott módon hoz létre a konfigurációs adatok dokumentum a kivonattábla (csomópont adatait) és a tömb (nem csomópont adatait), amely adhatók be a `RawEnvData` és `OtherEnvData` paramétereket.</span><span class="sxs-lookup"><span data-stu-id="982fb-168">The `New-DscConfigurationDataDocument` function (defined in `\Assets\DscPipelineTools\DscPipelineTools.psm1`) programmatically creates a configuration data document from the hashtable (node data) and array (non-node data) that are passed as the `RawEnvData` and `OtherEnvData` parameters.</span></span>

<span data-ttu-id="982fb-169">Ebben az esetben csak a `RawEnvData` paramétert használja.</span><span class="sxs-lookup"><span data-stu-id="982fb-169">In our case, only the `RawEnvData` parameter is used.</span></span>

### <a name="the-psake-build-script"></a><span data-ttu-id="982fb-170">A psake felépítési szkriptjének</span><span class="sxs-lookup"><span data-stu-id="982fb-170">The psake build script</span></span>

<span data-ttu-id="982fb-171">A [psake](https://github.com/psake/psake) felépítési szkript meghatározott `Build.ps1` (a Demo_CI tárház gyökérkönyvtárából `./InfraDNS/Build.ps1`) a build részét képező tevékenységek meghatározása.</span><span class="sxs-lookup"><span data-stu-id="982fb-171">The [psake](https://github.com/psake/psake) build script defined in `Build.ps1` (from the root of the Demo_CI repository, `./InfraDNS/Build.ps1`) defines tasks that are part of the build.</span></span>
<span data-ttu-id="982fb-172">Minden tevékenység más tevékenységek is meghatározza.</span><span class="sxs-lookup"><span data-stu-id="982fb-172">It also defines which other tasks each task depends on.</span></span>
<span data-ttu-id="982fb-173">Meghívva, ha a psake parancsfájl biztosítja, hogy a megadott feladat (vagy nevű feladatot `Default` Ha nincs megadva) fut, és az összes függőséget is futtathat (Ez azért szükséges, a rekurzív függőségek függőségeinek futtatása, és így tovább).</span><span class="sxs-lookup"><span data-stu-id="982fb-173">When invoked, the psake script ensures that the specified task (or the task named `Default` if none is specified) runs, and that all dependencies also run (this is recursive, so that dependencies of dependencies run, and so on).</span></span>

<span data-ttu-id="982fb-174">Ebben a példában a `Default` feladat típusúként van definiálva:</span><span class="sxs-lookup"><span data-stu-id="982fb-174">In this example, the `Default` task is defined as:</span></span>

```powershell
Task Default -depends UnitTests
```

<span data-ttu-id="982fb-175">A `Default` feladat nem magát végrehajtására van, de maga a `CompileConfigs` feladat.</span><span class="sxs-lookup"><span data-stu-id="982fb-175">The `Default` task has no implementation itself, but has a dependency on the `CompileConfigs` task.</span></span>
<span data-ttu-id="982fb-176">Az eredményül kapott láncában tevékenységfüggőségek biztosítja, hogy a felépítési szkriptjének található összes feladat futtatása.</span><span class="sxs-lookup"><span data-stu-id="982fb-176">The resulting chain of task dependencies ensures that all tasks in the build script are run.</span></span>

<span data-ttu-id="982fb-177">Ebben a példában a psake parancsfájl hívása hív `Invoke-PSake` a a `Initiate.ps1` fájlt (a Demo_CI tárház gyökérkönyvtárában található):</span><span class="sxs-lookup"><span data-stu-id="982fb-177">In this example, the psake script is invoked by a call to `Invoke-PSake` in the `Initiate.ps1` file (located at the root of the Demo_CI repository):</span></span>

```powershell
param(
    [parameter()]
    [ValidateSet('Build','Deploy')]
    [string]
    $fileName
)

#$Error.Clear()

Invoke-PSake $PSScriptRoot\InfraDNS\$fileName.ps1

<#if($Error.count)
{
    Throw "$fileName script failed. Check logs for failure details."
}
#>
```

<span data-ttu-id="982fb-178">Ha a builddefiníció hozunk létre a példa a TFS-ben, azt fogja adni a psake parancsfájlt, a `fileName` Ez a szkript paramétere.</span><span class="sxs-lookup"><span data-stu-id="982fb-178">When we create the build definition for our example in TFS, we will supply our psake script file as the `fileName` parameter for this script.</span></span>

<span data-ttu-id="982fb-179">A felépítési szkriptjének határozza meg a következő feladatokat:</span><span class="sxs-lookup"><span data-stu-id="982fb-179">The build script defines the following tasks:</span></span>

#### <a name="generateenvironmentfiles"></a><span data-ttu-id="982fb-180">GenerateEnvironmentFiles</span><span class="sxs-lookup"><span data-stu-id="982fb-180">GenerateEnvironmentFiles</span></span>

<span data-ttu-id="982fb-181">Futtatások `DevEnv.ps1`, amely állít elő, hogy a konfigurációs adatfájl.</span><span class="sxs-lookup"><span data-stu-id="982fb-181">Runs `DevEnv.ps1`, which generates the configuration data file.</span></span>

#### <a name="installmodules"></a><span data-ttu-id="982fb-182">InstallModules</span><span class="sxs-lookup"><span data-stu-id="982fb-182">InstallModules</span></span>

<span data-ttu-id="982fb-183">Telepíti a modulokat, a konfiguráció szükséges `DNSServer.ps1`.</span><span class="sxs-lookup"><span data-stu-id="982fb-183">Installs the modules required by the configuration `DNSServer.ps1`.</span></span>

#### <a name="scriptanalysis"></a><span data-ttu-id="982fb-184">ScriptAnalysis</span><span class="sxs-lookup"><span data-stu-id="982fb-184">ScriptAnalysis</span></span>

<span data-ttu-id="982fb-185">Hívások a [PSScriptAnalyzer](https://github.com/PowerShell/PSScriptAnalyzer).</span><span class="sxs-lookup"><span data-stu-id="982fb-185">Calls the [PSScriptAnalyzer](https://github.com/PowerShell/PSScriptAnalyzer).</span></span>

#### <a name="unittests"></a><span data-ttu-id="982fb-186">UnitTests</span><span class="sxs-lookup"><span data-stu-id="982fb-186">UnitTests</span></span>

<span data-ttu-id="982fb-187">Futtatás a [Pester](https://github.com/pester/Pester/wiki) egységteszteket.</span><span class="sxs-lookup"><span data-stu-id="982fb-187">Runs the [Pester](https://github.com/pester/Pester/wiki) unit tests.</span></span>

#### <a name="compileconfigs"></a><span data-ttu-id="982fb-188">CompileConfigs</span><span class="sxs-lookup"><span data-stu-id="982fb-188">CompileConfigs</span></span>

<span data-ttu-id="982fb-189">Lefordítja a konfigurációt (`DNSServer.ps1`) által létrehozott konfigurációs adatok használatával MOF-fájlba a `GenerateEnvironmentFiles` feladat.</span><span class="sxs-lookup"><span data-stu-id="982fb-189">Compiles the configuration (`DNSServer.ps1`) into a MOF file, using the configuration data generated by the `GenerateEnvironmentFiles` task.</span></span>

#### <a name="clean"></a><span data-ttu-id="982fb-190">Clean</span><span class="sxs-lookup"><span data-stu-id="982fb-190">Clean</span></span>

<span data-ttu-id="982fb-191">A például szolgáló mappákat hoz létre, és eltávolítja a korábbi közvetítésekből származó terhelésiteszt-eredményei, konfigurációs adatfájllal, és modulok.</span><span class="sxs-lookup"><span data-stu-id="982fb-191">Creates the folders used for the example, and removes any test results, configuration data files, and modules from previous runs.</span></span>

### <a name="the-psake-deploy-script"></a><span data-ttu-id="982fb-192">A psake parancsfájl központi telepítése</span><span class="sxs-lookup"><span data-stu-id="982fb-192">The psake deploy script</span></span>

<span data-ttu-id="982fb-193">A [psake](https://github.com/psake/psake) meghatározott telepítési parancsfájl `Deploy.ps1` (a Demo_CI tárház gyökérkönyvtárából `./InfraDNS/Deploy.ps1`) határozza meg, amely üzembe helyezése és futtatása a konfigurációs feladatok.</span><span class="sxs-lookup"><span data-stu-id="982fb-193">The [psake](https://github.com/psake/psake) deployment script defined in `Deploy.ps1` (from the root of the Demo_CI repository, `./InfraDNS/Deploy.ps1`) defines tasks that deploy and run the configuration.</span></span>

<span data-ttu-id="982fb-194">`Deploy.ps1` határozza meg a következő feladatokat:</span><span class="sxs-lookup"><span data-stu-id="982fb-194">`Deploy.ps1` defines the following tasks:</span></span>

#### <a name="deploymodules"></a><span data-ttu-id="982fb-195">DeployModules</span><span class="sxs-lookup"><span data-stu-id="982fb-195">DeployModules</span></span>

<span data-ttu-id="982fb-196">Elindít egy PowerShell-munkamenetet a `TestAgent1` , és telepíti a modulokat tartalmazó a DSC-erőforrások, a konfigurációhoz szükséges.</span><span class="sxs-lookup"><span data-stu-id="982fb-196">Starts a PowerShell session on `TestAgent1` and installs the modules containing the DSC resources required for the configuration.</span></span>

#### <a name="deployconfigs"></a><span data-ttu-id="982fb-197">DeployConfigs</span><span class="sxs-lookup"><span data-stu-id="982fb-197">DeployConfigs</span></span>

<span data-ttu-id="982fb-198">Hívások a [Start-DscConfiguration](/powershell/module/psdesiredstateconfiguration/start-dscconfiguration) parancsmag futtatása a konfiguráció `TestAgent1`.</span><span class="sxs-lookup"><span data-stu-id="982fb-198">Calls the [Start-DscConfiguration](/powershell/module/psdesiredstateconfiguration/start-dscconfiguration) cmdlet to run the configuration on `TestAgent1`.</span></span>

#### <a name="integrationtests"></a><span data-ttu-id="982fb-199">IntegrationTests</span><span class="sxs-lookup"><span data-stu-id="982fb-199">IntegrationTests</span></span>

<span data-ttu-id="982fb-200">Futtatás a [Pester](https://github.com/pester/Pester/wiki) integráció az egységteszteket.</span><span class="sxs-lookup"><span data-stu-id="982fb-200">Runs the [Pester](https://github.com/pester/Pester/wiki) integration tests.</span></span>

#### <a name="acceptancetests"></a><span data-ttu-id="982fb-201">AcceptanceTests</span><span class="sxs-lookup"><span data-stu-id="982fb-201">AcceptanceTests</span></span>

<span data-ttu-id="982fb-202">Futtatás a [Pester](https://github.com/pester/Pester/wiki) minőségellenőrzési tesztelésben vesznek részt.</span><span class="sxs-lookup"><span data-stu-id="982fb-202">Runs the [Pester](https://github.com/pester/Pester/wiki) acceptance tests.</span></span>

#### <a name="clean"></a><span data-ttu-id="982fb-203">Clean</span><span class="sxs-lookup"><span data-stu-id="982fb-203">Clean</span></span>

<span data-ttu-id="982fb-204">Eltávolítja a modulokat az előző futtatásokat telepítve, és biztosítja, hogy a teszt eredménye mappa létezik-e.</span><span class="sxs-lookup"><span data-stu-id="982fb-204">Removes any modules installed in previous runs, and ensures that the test result folder exists.</span></span>

### <a name="test-scripts"></a><span data-ttu-id="982fb-205">Parancsfájlok tesztelése</span><span class="sxs-lookup"><span data-stu-id="982fb-205">Test scripts</span></span>

<span data-ttu-id="982fb-206">Elfogadó, integráció, és az egységteszteket definiált szkriptekben a `Tests` mappát (a Demo_CI tárház gyökérkönyvtárából `./InfraDNS/Tests`), mindegyik nevű fájlt a `DNSServer.tests.ps1` megfelelő mappáiban.</span><span class="sxs-lookup"><span data-stu-id="982fb-206">Acceptance, Integration, and Unit tests are defined in scripts in the `Tests` folder (from the root of the Demo_CI repository, `./InfraDNS/Tests`), each in files named `DNSServer.tests.ps1` in their respective folders.</span></span>

<span data-ttu-id="982fb-207">A teszt-szkriptek használata [Pester](https://github.com/pester/Pester/wiki) és [PoshSpec](https://github.com/Ticketmaster/poshspec/wiki/Introduction) szintaxist.</span><span class="sxs-lookup"><span data-stu-id="982fb-207">The test scripts use [Pester](https://github.com/pester/Pester/wiki) and [PoshSpec](https://github.com/Ticketmaster/poshspec/wiki/Introduction) syntax.</span></span>

#### <a name="unit-tests"></a><span data-ttu-id="982fb-208">Egységteszteket</span><span class="sxs-lookup"><span data-stu-id="982fb-208">Unit tests</span></span>

<span data-ttu-id="982fb-209">Az egység teszteli magukat, hogy győződjön meg arról, hogy a konfigurációk elvégzi az alkalmazás futtatásakor várt tesztelési a DSC-konfigurációkat.</span><span class="sxs-lookup"><span data-stu-id="982fb-209">The unit tests test the DSC configurations themselves to ensure that the configurations will do what is expected when they run.</span></span>
<span data-ttu-id="982fb-210">A parancsfájlt használja vetünk [Pester](https://github.com/pester/Pester/wiki).</span><span class="sxs-lookup"><span data-stu-id="982fb-210">The unit test script uses [Pester](https://github.com/pester/Pester/wiki).</span></span>

#### <a name="integration-tests"></a><span data-ttu-id="982fb-211">Integráció az egységteszteket</span><span class="sxs-lookup"><span data-stu-id="982fb-211">Integration tests</span></span>

<span data-ttu-id="982fb-212">Az integrációs tesztek a konfiguráció teszteléséhez vagy a rendszer bizonyosodjon meg arról, hogy más összetevők integrálva, amikor a rendszer elvárt módon.</span><span class="sxs-lookup"><span data-stu-id="982fb-212">The integration tests test the configuration of the system to ensure that when integrated with other components, the system is configured as expected.</span></span> <span data-ttu-id="982fb-213">Ezek a tesztek futtatása célcsomóponton után a DSC lett konfigurálva.</span><span class="sxs-lookup"><span data-stu-id="982fb-213">These tests run on the target node after it has been configured with DSC.</span></span>
<span data-ttu-id="982fb-214">Az integrációs teszt szkriptjét használ vegyesen [Pester](https://github.com/pester/Pester/wiki) és [PoshSpec](https://github.com/Ticketmaster/poshspec/wiki/Introduction) szintaxist.</span><span class="sxs-lookup"><span data-stu-id="982fb-214">The integration test script uses a mixture of [Pester](https://github.com/pester/Pester/wiki) and [PoshSpec](https://github.com/Ticketmaster/poshspec/wiki/Introduction) syntax.</span></span>

#### <a name="acceptance-tests"></a><span data-ttu-id="982fb-215">Minőségellenőrzési tesztelésben vesznek részt</span><span class="sxs-lookup"><span data-stu-id="982fb-215">Acceptance tests</span></span>

<span data-ttu-id="982fb-216">Minőségellenőrzési tesztelésben vesznek részt teszteléséhez győződjön meg arról, hogy a várt módon működnek-e, a rendszer.</span><span class="sxs-lookup"><span data-stu-id="982fb-216">Acceptance tests test the system to ensure that it behaves as expected.</span></span>
<span data-ttu-id="982fb-217">Például azt teszteli, annak érdekében, hogy egy weblap történő lekérdezéskor a megfelelő információt ad vissza.</span><span class="sxs-lookup"><span data-stu-id="982fb-217">For example, it tests to ensure a web page returns the right information when queried.</span></span>
<span data-ttu-id="982fb-218">Ezek a tesztek távolról futtatni a célcsomópont a valós életből vett teszteléséhez.</span><span class="sxs-lookup"><span data-stu-id="982fb-218">These tests run remotely from the target node in order to test real world scenarios.</span></span>
<span data-ttu-id="982fb-219">Az integrációs teszt szkriptjét használ vegyesen [Pester](https://github.com/pester/Pester/wiki) és [PoshSpec](https://github.com/Ticketmaster/poshspec/wiki/Introduction) szintaxist.</span><span class="sxs-lookup"><span data-stu-id="982fb-219">The integration test script uses a mixture of [Pester](https://github.com/pester/Pester/wiki) and [PoshSpec](https://github.com/Ticketmaster/poshspec/wiki/Introduction) syntax.</span></span>

## <a name="define-the-build"></a><span data-ttu-id="982fb-220">A build megadása</span><span class="sxs-lookup"><span data-stu-id="982fb-220">Define the build</span></span>

<span data-ttu-id="982fb-221">Most, hogy mi feltöltötte a kódban, TFS és tekintett meg, mire, határozzon meg a build.</span><span class="sxs-lookup"><span data-stu-id="982fb-221">Now that we've uploaded our code to TFS and looked at what it does, let's define our build.</span></span>

<span data-ttu-id="982fb-222">Itt csak a fogja hozzáadni a buildre létrehozási lépések lesz szó.</span><span class="sxs-lookup"><span data-stu-id="982fb-222">Here, we'll cover only the build steps that you'll add to the build.</span></span> <span data-ttu-id="982fb-223">Builddefiníció létrehozása a TFS-ben, lásd: [létrehozása és a várólista builddefiníció](/azure/devops/pipelines/get-started-designer).</span><span class="sxs-lookup"><span data-stu-id="982fb-223">For instructions on how to create a build definition in TFS, see [Create and queue a build definition](/azure/devops/pipelines/get-started-designer).</span></span>

<span data-ttu-id="982fb-224">Hozzon létre egy új builddefiníció (válassza ki a **üres** sablon) "InfraDNS" nevű.</span><span class="sxs-lookup"><span data-stu-id="982fb-224">Create a new build definition (select the **Empty** template) named "InfraDNS".</span></span>
<span data-ttu-id="982fb-225">Adja hozzá az alábbi lépések végrehajtásával, build definíciója:</span><span class="sxs-lookup"><span data-stu-id="982fb-225">Add the following steps to you build definition:</span></span>

- <span data-ttu-id="982fb-226">PowerShell-parancsfájl</span><span class="sxs-lookup"><span data-stu-id="982fb-226">PowerShell Script</span></span>
- <span data-ttu-id="982fb-227">Vizsgálati eredmények közzététele</span><span class="sxs-lookup"><span data-stu-id="982fb-227">Publish Test Results</span></span>
- <span data-ttu-id="982fb-228">Fájlok másolása</span><span class="sxs-lookup"><span data-stu-id="982fb-228">Copy Files</span></span>
- <span data-ttu-id="982fb-229">Összetevők közzététele</span><span class="sxs-lookup"><span data-stu-id="982fb-229">Publish Artifact</span></span>

<span data-ttu-id="982fb-230">Ezek lépések, a következő az egyes lépések tulajdonságainak szerkesztéséhez hozzáadása után:</span><span class="sxs-lookup"><span data-stu-id="982fb-230">After adding these build steps, edit the properties of each step as follows:</span></span>

### <a name="powershell-script"></a><span data-ttu-id="982fb-231">PowerShell-parancsfájl</span><span class="sxs-lookup"><span data-stu-id="982fb-231">PowerShell Script</span></span>

1. <span data-ttu-id="982fb-232">Állítsa be a **típus** tulajdonságot `File Path`.</span><span class="sxs-lookup"><span data-stu-id="982fb-232">Set the **Type** property to `File Path`.</span></span>
1. <span data-ttu-id="982fb-233">Állítsa be a **parancsfájl elérési útján** tulajdonságot `initiate.ps1`.</span><span class="sxs-lookup"><span data-stu-id="982fb-233">Set the **Script Path** property to `initiate.ps1`.</span></span>
1. <span data-ttu-id="982fb-234">Adjon hozzá `-fileName build` , a **argumentumok** tulajdonság.</span><span class="sxs-lookup"><span data-stu-id="982fb-234">Add `-fileName build` to the **Arguments** property.</span></span>

<span data-ttu-id="982fb-235">Ez a létrehozási lépés fut a `initiate.ps1` fájlt, amely meghívja a psake felépítési szkriptet.</span><span class="sxs-lookup"><span data-stu-id="982fb-235">This build step runs the `initiate.ps1` file, which calls the psake build script.</span></span>

### <a name="publish-test-results"></a><span data-ttu-id="982fb-236">Vizsgálati eredmények közzététele</span><span class="sxs-lookup"><span data-stu-id="982fb-236">Publish Test Results</span></span>

1. <span data-ttu-id="982fb-237">Állítsa be **Eredményformátum tesztelése** , `NUnit`</span><span class="sxs-lookup"><span data-stu-id="982fb-237">Set **Test Result Format** to `NUnit`</span></span>
1. <span data-ttu-id="982fb-238">Állítsa be **fájlokat a vizsgálati eredmények** , `InfraDNS/Tests/Results/*.xml`</span><span class="sxs-lookup"><span data-stu-id="982fb-238">Set **Test Results Files** to `InfraDNS/Tests/Results/*.xml`</span></span>
1. <span data-ttu-id="982fb-239">Állítsa be **futtatási cím tesztelése** való `Unit`.</span><span class="sxs-lookup"><span data-stu-id="982fb-239">Set **Test Run Title** to `Unit`.</span></span>
1. <span data-ttu-id="982fb-240">Győződjön meg arról, hogy **verziókövetési lehetőségek állnak rendelkezésre** **engedélyezve** és **mindig fusson** azok mind kiválasztva.</span><span class="sxs-lookup"><span data-stu-id="982fb-240">Make sure **Control Options** **Enabled** and **Always run** are both selected.</span></span>

<span data-ttu-id="982fb-241">A létrehozási lépés fut, a Pester parancsfájl megvizsgáltunk, korábban az egységteszteket, és tárolja az eredményeket a `InfraDNS/Tests/Results/*.xml` mappát.</span><span class="sxs-lookup"><span data-stu-id="982fb-241">This build step runs the unit tests in the Pester script we looked at earlier, and stores the results in the `InfraDNS/Tests/Results/*.xml` folder.</span></span>

### <a name="copy-files"></a><span data-ttu-id="982fb-242">Fájlok másolása</span><span class="sxs-lookup"><span data-stu-id="982fb-242">Copy Files</span></span>

1. <span data-ttu-id="982fb-243">Adja hozzá a következő sorokat **tartalma**:</span><span class="sxs-lookup"><span data-stu-id="982fb-243">Add each of the following lines to **Contents**:</span></span>

   ```
   initiate.ps1
   **\deploy.ps1
   **\Acceptance\**
   **\Integration\**
   ```

1. <span data-ttu-id="982fb-244">Állítsa be **TargetFolder** , `$(Build.ArtifactStagingDirectory)\`</span><span class="sxs-lookup"><span data-stu-id="982fb-244">Set **TargetFolder** to `$(Build.ArtifactStagingDirectory)\`</span></span>

<span data-ttu-id="982fb-245">Ebben a lépésben másolja át a build és a teszt parancsfájlok, az átmeneti könyvtárhoz úgy, hogy a build-összetevőket, által közzétehető a következő lépéssel.</span><span class="sxs-lookup"><span data-stu-id="982fb-245">This step copies the build and test scripts to the staging directory so that the can be published as build artifacts by the next step.</span></span>

### <a name="publish-artifact"></a><span data-ttu-id="982fb-246">Összetevők közzététele</span><span class="sxs-lookup"><span data-stu-id="982fb-246">Publish Artifact</span></span>

1. <span data-ttu-id="982fb-247">Állítsa be **közzététele elérési út** , `$(Build.ArtifactStagingDirectory)\`</span><span class="sxs-lookup"><span data-stu-id="982fb-247">Set **Path to Publish** to `$(Build.ArtifactStagingDirectory)\`</span></span>
1. <span data-ttu-id="982fb-248">Állítsa be **összetevőnév** , `Deploy`</span><span class="sxs-lookup"><span data-stu-id="982fb-248">Set **Artifact Name** to `Deploy`</span></span>
1. <span data-ttu-id="982fb-249">Állítsa be **Összetevőtípussal** , `Server`</span><span class="sxs-lookup"><span data-stu-id="982fb-249">Set **Artifact Type** to `Server`</span></span>
1. <span data-ttu-id="982fb-250">Válassza ki `Enabled` a **beállítások**</span><span class="sxs-lookup"><span data-stu-id="982fb-250">Select `Enabled` in **Control Options**</span></span>

## <a name="enable-continuous-integration"></a><span data-ttu-id="982fb-251">Folyamatos integráció engedélyezése</span><span class="sxs-lookup"><span data-stu-id="982fb-251">Enable continuous integration</span></span>

<span data-ttu-id="982fb-252">Most beállítjuk egy eseményindítót, amely miatt a projekt felépítéséhez bármikor egy módosítást a rendszer ellenőrzi, a `ci-cd-example` a git-adattár ágában.</span><span class="sxs-lookup"><span data-stu-id="982fb-252">Now we'll set up a trigger that causes the project to build any time a change is checked in to the `ci-cd-example` branch of the git repository.</span></span>

1. <span data-ttu-id="982fb-253">A TFS-ben, kattintson a **Build & Release** lap</span><span class="sxs-lookup"><span data-stu-id="982fb-253">In TFS, click the **Build & Release** tab</span></span>
1. <span data-ttu-id="982fb-254">Válassza ki a `DNS Infra` builddefiníció, majd kattintson az **szerkesztése**</span><span class="sxs-lookup"><span data-stu-id="982fb-254">Select the `DNS Infra` build definition, and click **Edit**</span></span>
1. <span data-ttu-id="982fb-255">Kattintson a **eseményindítók** lap</span><span class="sxs-lookup"><span data-stu-id="982fb-255">Click the **Triggers** tab</span></span>
1. <span data-ttu-id="982fb-256">Válassza ki **folyamatos integrációs (CI)**, és válassza ki `refs/heads/ci-cd-example` a fiókiroda legördülő lista</span><span class="sxs-lookup"><span data-stu-id="982fb-256">Select **Continuous integration (CI)**, and select `refs/heads/ci-cd-example` in the branch drop-down list</span></span>
1. <span data-ttu-id="982fb-257">Kattintson a **mentése** , majd **OK**</span><span class="sxs-lookup"><span data-stu-id="982fb-257">Click **Save** and then **OK**</span></span>

<span data-ttu-id="982fb-258">Most már minden változása a TFS git-tárház eseményindítók egy automatizált összeállítási.</span><span class="sxs-lookup"><span data-stu-id="982fb-258">Now any change in the TFS git repository triggers an automated build.</span></span>

## <a name="create-the-release-definition"></a><span data-ttu-id="982fb-259">A kiadási definíció létrehozása</span><span class="sxs-lookup"><span data-stu-id="982fb-259">Create the release definition</span></span>

<span data-ttu-id="982fb-260">Kiadási definíció hozzunk létre úgy, hogy a projekt rendszerbe minden kód bejelentkezés a fejlesztői környezetben.</span><span class="sxs-lookup"><span data-stu-id="982fb-260">Let's create a release definition so that the project is deployed to the development environment with every code check-in.</span></span>

<span data-ttu-id="982fb-261">Ehhez adja hozzá társított új kiadási definíciót a `InfraDNS` hozhat létre a korábban létrehozott builddefiníciót.</span><span class="sxs-lookup"><span data-stu-id="982fb-261">To do this, add a new release definition associated with the `InfraDNS` build definition you created previously.</span></span>
<span data-ttu-id="982fb-262">Ügyeljen arra, hogy válasszon **folyamatos üzembe helyezés** úgy, hogy az új kiadás akkor aktiválódik, amikor elkészül egy új build.</span><span class="sxs-lookup"><span data-stu-id="982fb-262">Be sure to select **Continuous deployment** so that a new release will be triggered any time a new build is completed.</span></span>
<span data-ttu-id="982fb-263">([Hogyan: Kiadási definíciók együttműködve](https://www.visualstudio.com/en-us/docs/build/actions/work-with-release-definitions)) és a következőképpen konfigurálja:</span><span class="sxs-lookup"><span data-stu-id="982fb-263">([How to: Work with release definitions](https://www.visualstudio.com/en-us/docs/build/actions/work-with-release-definitions)) and configure it as follows:</span></span>

<span data-ttu-id="982fb-264">Adja hozzá a kiadási definíció az alábbi lépéseket:</span><span class="sxs-lookup"><span data-stu-id="982fb-264">Add the following steps to the release definition:</span></span>

- <span data-ttu-id="982fb-265">PowerShell-parancsfájl</span><span class="sxs-lookup"><span data-stu-id="982fb-265">PowerShell Script</span></span>
- <span data-ttu-id="982fb-266">Vizsgálati eredmények közzététele</span><span class="sxs-lookup"><span data-stu-id="982fb-266">Publish Test Results</span></span>
- <span data-ttu-id="982fb-267">Vizsgálati eredmények közzététele</span><span class="sxs-lookup"><span data-stu-id="982fb-267">Publish Test Results</span></span>

<span data-ttu-id="982fb-268">Szerkesztése a következő lépéseket:</span><span class="sxs-lookup"><span data-stu-id="982fb-268">Edit the steps as follows:</span></span>

### <a name="powershell-script"></a><span data-ttu-id="982fb-269">PowerShell-parancsfájl</span><span class="sxs-lookup"><span data-stu-id="982fb-269">PowerShell Script</span></span>

1. <span data-ttu-id="982fb-270">Állítsa be a **parancsfájl elérési útján** mezőt `$(Build.DefinitionName)\Deploy\initiate.ps1"`</span><span class="sxs-lookup"><span data-stu-id="982fb-270">Set the **Script Path** field to `$(Build.DefinitionName)\Deploy\initiate.ps1"`</span></span>
1. <span data-ttu-id="982fb-271">Állítsa be a **argumentumok** mezőt `-fileName Deploy`</span><span class="sxs-lookup"><span data-stu-id="982fb-271">Set the **Arguments** field to `-fileName Deploy`</span></span>

### <a name="first-publish-test-results"></a><span data-ttu-id="982fb-272">Először a vizsgálati eredmények közzététele</span><span class="sxs-lookup"><span data-stu-id="982fb-272">First Publish Test Results</span></span>

1. <span data-ttu-id="982fb-273">Válassza ki `NUnit` számára a **teszt Eredményformátum** mező</span><span class="sxs-lookup"><span data-stu-id="982fb-273">Select `NUnit` for the **Test Result Format** field</span></span>
1. <span data-ttu-id="982fb-274">Állítsa be a **eredmény Tesztfájlok** mezőt `$(Build.DefinitionName)\Deploy\InfraDNS\Tests\Results\Integration*.xml`</span><span class="sxs-lookup"><span data-stu-id="982fb-274">Set the **Test Result Files** field to `$(Build.DefinitionName)\Deploy\InfraDNS\Tests\Results\Integration*.xml`</span></span>
1. <span data-ttu-id="982fb-275">Állítsa be a **futtatási cím tesztelése** , `Integration`</span><span class="sxs-lookup"><span data-stu-id="982fb-275">Set the **Test Run Title** to `Integration`</span></span>
1. <span data-ttu-id="982fb-276">A **verziókövetési lehetőségek állnak rendelkezésre**, ellenőrizze **mindig futtatja**</span><span class="sxs-lookup"><span data-stu-id="982fb-276">Under **Control Options**, check **Always run**</span></span>

### <a name="second-publish-test-results"></a><span data-ttu-id="982fb-277">A második a vizsgálati eredmények közzététele</span><span class="sxs-lookup"><span data-stu-id="982fb-277">Second Publish Test Results</span></span>

1. <span data-ttu-id="982fb-278">Válassza ki `NUnit` számára a **teszt Eredményformátum** mező</span><span class="sxs-lookup"><span data-stu-id="982fb-278">Select `NUnit` for the **Test Result Format** field</span></span>
1. <span data-ttu-id="982fb-279">Állítsa be a **eredmény Tesztfájlok** mezőt `$(Build.DefinitionName)\Deploy\InfraDNS\Tests\Results\Acceptance*.xml`</span><span class="sxs-lookup"><span data-stu-id="982fb-279">Set the **Test Result Files** field to `$(Build.DefinitionName)\Deploy\InfraDNS\Tests\Results\Acceptance*.xml`</span></span>
1. <span data-ttu-id="982fb-280">Állítsa be a **futtatási cím tesztelése** , `Acceptance`</span><span class="sxs-lookup"><span data-stu-id="982fb-280">Set the **Test Run Title** to `Acceptance`</span></span>
1. <span data-ttu-id="982fb-281">A **verziókövetési lehetőségek állnak rendelkezésre**, ellenőrizze **mindig futtatja**</span><span class="sxs-lookup"><span data-stu-id="982fb-281">Under **Control Options**, check **Always run**</span></span>

## <a name="verify-your-results"></a><span data-ttu-id="982fb-282">Az eredmények ellenőrzése</span><span class="sxs-lookup"><span data-stu-id="982fb-282">Verify your results</span></span>

<span data-ttu-id="982fb-283">Most bármikor, küldje le változások a `ci-cd-example` ágra a TFS-ben, egy új létrehozást indul el.</span><span class="sxs-lookup"><span data-stu-id="982fb-283">Now, any time you push changes in the `ci-cd-example` branch to TFS, a new build will start.</span></span>
<span data-ttu-id="982fb-284">Ha a létrehozás sikeresen befejeződik, akkor aktiválódik, új központi telepítést.</span><span class="sxs-lookup"><span data-stu-id="982fb-284">If the build completes successfully, a new deployment is triggered.</span></span>

<span data-ttu-id="982fb-285">Az eredmény az üzembe helyezés ellenőrzéséhez nyissa meg egy böngészőt, az ügyfélszámítógépen, és ellenőrizheti, hogy `www.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="982fb-285">You can check the result of the deployment by opening a browser on the client machine and navigating to `www.contoso.com`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="982fb-286">További lépések</span><span class="sxs-lookup"><span data-stu-id="982fb-286">Next steps</span></span>

<span data-ttu-id="982fb-287">Ez a példa konfigurálja a DNS-kiszolgáló `TestAgent1` úgy, hogy az URL-cím `www.contoso.com` mutat `TestAgent2`, de azt nem ténylegesen telepíti egy webhely.</span><span class="sxs-lookup"><span data-stu-id="982fb-287">This example configures the DNS server `TestAgent1` so that the URL `www.contoso.com` resolves to `TestAgent2`, but it does not actually deploy a website.</span></span>
<span data-ttu-id="982fb-288">Ennek a vázat a tárház alatt megtalálható a `WebApp` mappát.</span><span class="sxs-lookup"><span data-stu-id="982fb-288">The skeleton for doing so is provided in the repo under the `WebApp` folder.</span></span>
<span data-ttu-id="982fb-289">A psake parancsfájlok, a Pester tesztek és a DSC-konfigurációk létrehozása a megadott fájl segítségével telepítheti a saját webhelyen.</span><span class="sxs-lookup"><span data-stu-id="982fb-289">You can use the stubs provided to create psake scripts, Pester tests, and DSC configurations to deploy your own website.</span></span>
