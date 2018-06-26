---
ms.date: 06/12/2017
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: A DSC folyamatos integrációt és folyamatos üzembe helyezési folyamat létrehozása
ms.openlocfilehash: faeef5022cbd984cab0620b69db19de8b84cca0e
ms.sourcegitcommit: 68093cc12a7a22c53d11ce7d33c18622921a0dd1
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/26/2018
ms.locfileid: "36940344"
---
# <a name="building-a-continuous-integration-and-continuous-deployment-pipeline-with-dsc"></a><span data-ttu-id="347fd-103">A DSC folyamatos integrációt és folyamatos üzembe helyezési folyamat létrehozása</span><span class="sxs-lookup"><span data-stu-id="347fd-103">Building a Continuous Integration and Continuous Deployment pipeline with DSC</span></span>

<span data-ttu-id="347fd-104">Ez a példa bemutatja, hogyan folyamatos integráció/Continuous Deployment (CI/CD) folyamat létrehozása a PowerShell DSC, Pester és a Visual Studio Team Foundation Server (TFS) használatával.</span><span class="sxs-lookup"><span data-stu-id="347fd-104">This example demonstrates how to build a Continuous Integration/Continuous Deployment (CI/CD) pipeline by using PowerShell, DSC, Pester, and Visual Studio Team Foundation Server (TFS).</span></span>

<span data-ttu-id="347fd-105">A feldolgozási sor összeállítása és konfigurálva, után teljes telepítéséhez, konfigurálásához, és DNS-kiszolgáló tesztelése alkalmazhat, és állomásrekordokat társított.</span><span class="sxs-lookup"><span data-stu-id="347fd-105">After the pipeline is built and configured, you can use it to fully deploy, configure and test a DNS server and associated host records.</span></span>
<span data-ttu-id="347fd-106">Ez a folyamat első része egy folyamatot, amely fejlesztői környezetben használni szimulálja.</span><span class="sxs-lookup"><span data-stu-id="347fd-106">This process simulates the first part of a pipeline that would be used in a development environment.</span></span>

<span data-ttu-id="347fd-107">Egy automatizált CI/CD folyamat segít a gyorsabb frissítse a szoftvert, és megbízhatóbb, győződjön meg arról, hogy az összes kód szolgáltatás tesztelése, és hogy a kód aktuális build mindenkor.</span><span class="sxs-lookup"><span data-stu-id="347fd-107">An automated CI/CD pipeline helps you update software faster and more reliably, ensuring that all code is tested, and that a current build of your code is available at all times.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="347fd-108">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="347fd-108">Prerequisites</span></span>

<span data-ttu-id="347fd-109">Ez a példa használatához ismernie kell a következőkkel:</span><span class="sxs-lookup"><span data-stu-id="347fd-109">To use this example, you should be familiar with the following:</span></span>

- <span data-ttu-id="347fd-110">CI-CD fogalmakat.</span><span class="sxs-lookup"><span data-stu-id="347fd-110">CI-CD concepts.</span></span> <span data-ttu-id="347fd-111">Egy jó hivatkozás található a [a kiadási csővezeték modell](http://aka.ms/thereleasepipelinemodelpdf).</span><span class="sxs-lookup"><span data-stu-id="347fd-111">A good reference can be found at [The Release Pipeline Model](http://aka.ms/thereleasepipelinemodelpdf).</span></span>
- <span data-ttu-id="347fd-112">[Git](https://git-scm.com/) forrás-vezérlő</span><span class="sxs-lookup"><span data-stu-id="347fd-112">[Git](https://git-scm.com/) source control</span></span>
- <span data-ttu-id="347fd-113">A [Pester](https://github.com/pester/Pester) keretrendszer tesztelése</span><span class="sxs-lookup"><span data-stu-id="347fd-113">The [Pester](https://github.com/pester/Pester) testing framework</span></span>
- [<span data-ttu-id="347fd-114">A Team Foundation Server</span><span class="sxs-lookup"><span data-stu-id="347fd-114">Team Foundation Server</span></span>](https://www.visualstudio.com/tfs/)

## <a name="what-you-will-need"></a><span data-ttu-id="347fd-115">Mit kell</span><span class="sxs-lookup"><span data-stu-id="347fd-115">What you will need</span></span>

<span data-ttu-id="347fd-116">Építsenek, és ez a példa futtatásához, szüksége lesz a több számítógépek és/vagy a virtuális gépeket tartalmazó környezetben.</span><span class="sxs-lookup"><span data-stu-id="347fd-116">To build and run this example, you will need an environment with several computers and/or virtual machines.</span></span>

### <a name="client"></a><span data-ttu-id="347fd-117">Ügyfél</span><span class="sxs-lookup"><span data-stu-id="347fd-117">Client</span></span>

<span data-ttu-id="347fd-118">Ez az a számítógépen, ahol el kell végeznie összes beállíthatja és futtathatja a példa a munkát.</span><span class="sxs-lookup"><span data-stu-id="347fd-118">This is the computer where you'll do all of the work setting up and running the example.</span></span>

<span data-ttu-id="347fd-119">Az ügyfélszámítógép kell lennie a Windows rendszerű számítógépeken telepítve a következőre:</span><span class="sxs-lookup"><span data-stu-id="347fd-119">The client computer must be a Windows computer with the following installed:</span></span>

- [<span data-ttu-id="347fd-120">Git</span><span class="sxs-lookup"><span data-stu-id="347fd-120">Git</span></span>](https://git-scm.com/)
- <span data-ttu-id="347fd-121">egy helyi git-tárház alapján klónozták https://github.com/PowerShell/Demo_CI</span><span class="sxs-lookup"><span data-stu-id="347fd-121">a local git repo cloned from https://github.com/PowerShell/Demo_CI</span></span>
- <span data-ttu-id="347fd-122">egy szövegszerkesztőben, például a [Visual Studio Code](https://code.visualstudio.com/)</span><span class="sxs-lookup"><span data-stu-id="347fd-122">a text editor, such as [Visual Studio Code](https://code.visualstudio.com/)</span></span>

### <a name="tfssrv1"></a><span data-ttu-id="347fd-123">TFSSrv1</span><span class="sxs-lookup"><span data-stu-id="347fd-123">TFSSrv1</span></span>

<span data-ttu-id="347fd-124">A TFS-kiszolgálóhoz, amelyen határozza meg a build futtató számítógépen és felszabadítása.</span><span class="sxs-lookup"><span data-stu-id="347fd-124">The computer that hosts the TFS server where you will define your build and release.</span></span>
<span data-ttu-id="347fd-125">A számítógépnek rendelkeznie kell [Team Foundation Server 2017](https://www.visualstudio.com/tfs/) telepítve.</span><span class="sxs-lookup"><span data-stu-id="347fd-125">This computer must have [Team Foundation Server 2017](https://www.visualstudio.com/tfs/) installed.</span></span>

### <a name="buildagent"></a><span data-ttu-id="347fd-126">BuildAgent</span><span class="sxs-lookup"><span data-stu-id="347fd-126">BuildAgent</span></span>

<span data-ttu-id="347fd-127">A a Windows rendszerű számítógépre ügynök, amely létrehozza a projekt felépítéséhez.</span><span class="sxs-lookup"><span data-stu-id="347fd-127">The computer that runs the Windows build agent that builds the project.</span></span>
<span data-ttu-id="347fd-128">Ezen a számítógépen telepített és futó ügynök összeállítása Windows kell rendelkeznie.</span><span class="sxs-lookup"><span data-stu-id="347fd-128">This computer must have a Windows build agent installed and running.</span></span>
<span data-ttu-id="347fd-129">Lásd: [egy Windows-ügynök telepítéséhez](https://www.visualstudio.com/en-us/docs/build/actions/agents/v2-windows) vonatkozó útmutatást, telepítéséhez és futtatásához egy Windows-build ügynök.</span><span class="sxs-lookup"><span data-stu-id="347fd-129">See [Deploy an agent on Windows](https://www.visualstudio.com/en-us/docs/build/actions/agents/v2-windows) for instructions on how to install and run a Windows build agent.</span></span>

<span data-ttu-id="347fd-130">Alkalmazást is telepíteni kell a `xDnsServer` és `xNetworking` DSC-modulok ezen a számítógépen.</span><span class="sxs-lookup"><span data-stu-id="347fd-130">You also need to install both the `xDnsServer` and `xNetworking` DSC modules on this computer.</span></span>

### <a name="testagent1"></a><span data-ttu-id="347fd-131">TestAgent1</span><span class="sxs-lookup"><span data-stu-id="347fd-131">TestAgent1</span></span>

<span data-ttu-id="347fd-132">Ez az a számítógép a DSC-konfiguráció ebben a példában a DNS-kiszolgálóként konfigurált.</span><span class="sxs-lookup"><span data-stu-id="347fd-132">This is the computer that is configured as a DNS server by the DSC configuration in this example.</span></span>
<span data-ttu-id="347fd-133">A számítógépen futnia kell [Windows Server 2016](https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2016).</span><span class="sxs-lookup"><span data-stu-id="347fd-133">The computer must be running [Windows Server 2016](https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2016).</span></span>

### <a name="testagent2"></a><span data-ttu-id="347fd-134">TestAgent2</span><span class="sxs-lookup"><span data-stu-id="347fd-134">TestAgent2</span></span>

<span data-ttu-id="347fd-135">Ez az a számítógép, amelyen a webhely a példa.</span><span class="sxs-lookup"><span data-stu-id="347fd-135">This is the computer that hosts the website this example configures.</span></span>
<span data-ttu-id="347fd-136">A számítógépen futnia kell [Windows Server 2016](https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2016).</span><span class="sxs-lookup"><span data-stu-id="347fd-136">The computer must be running [Windows Server 2016](https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2016).</span></span>

## <a name="add-the-code-to-tfs"></a><span data-ttu-id="347fd-137">Adja hozzá a kódot TFS</span><span class="sxs-lookup"><span data-stu-id="347fd-137">Add the code to TFS</span></span>

<span data-ttu-id="347fd-138">Először foglalkozunk a Git-tárház létrehozása a TFS-ben, és importálja a helyi tárház az ügyfélszámítógépen a kódot.</span><span class="sxs-lookup"><span data-stu-id="347fd-138">We'll start out by creating a Git repository in TFS, and importing the code from your local repository on the client computer.</span></span>
<span data-ttu-id="347fd-139">Ha nem rendelkezik már klónozni a Demo_CI tárház az ügyfélszámítógépre tegye most a következő git parancs futtatásával:</span><span class="sxs-lookup"><span data-stu-id="347fd-139">If you have not already cloned the Demo_CI repository to your client computer, do so now by running the following git command:</span></span>

`git clone https://github.com/PowerShell/Demo_CI`

1. <span data-ttu-id="347fd-140">Az ügyfélszámítógépen navigáljon a TFS-kiszolgáló egy webböngészőben.</span><span class="sxs-lookup"><span data-stu-id="347fd-140">On your client computer, navigate to your TFS server in a web browser.</span></span>
1. <span data-ttu-id="347fd-141">A TFS rendszerben [hozzon létre egy új csapatprojektbe](https://www.visualstudio.com/en-us/docs/setup-admin/create-team-project) Demo_CI nevű.</span><span class="sxs-lookup"><span data-stu-id="347fd-141">In TFS, [Create a new team project](https://www.visualstudio.com/en-us/docs/setup-admin/create-team-project) named Demo_CI.</span></span>

   <span data-ttu-id="347fd-142">Győződjön meg arról, hogy **verziókezelést** értéke **Git**.</span><span class="sxs-lookup"><span data-stu-id="347fd-142">Make sure that **Version control** is set to **Git**.</span></span>
1. <span data-ttu-id="347fd-143">Az ügyfélszámítógépen a most létrehozott a TFS-ben a következő paranccsal tárház távoli hozzáadása:</span><span class="sxs-lookup"><span data-stu-id="347fd-143">On your client computer, add a remote to the repository you just created in TFS with the following command:</span></span>

   `git remote add tfs <YourTFSRepoURL>`

   <span data-ttu-id="347fd-144">Ha `<YourTFSRepoURL>` a klón URL-címét az előző lépésben létrehozott TFS-tárházba.</span><span class="sxs-lookup"><span data-stu-id="347fd-144">Where `<YourTFSRepoURL>` is the clone URL to the TFS repository you created in the previous step.</span></span>

   <span data-ttu-id="347fd-145">Ha nem tudja, hol található az URL-cím, lásd: [egy meglévő Git-tárház klónozása](https://www.visualstudio.com/en-us/docs/git/tutorial/clone).</span><span class="sxs-lookup"><span data-stu-id="347fd-145">If you don't know where to find this URL, see [Clone an existing Git repo](https://www.visualstudio.com/en-us/docs/git/tutorial/clone).</span></span>
1. <span data-ttu-id="347fd-146">A kód a helyi tárházból a TFS tárház leküldése a következő paranccsal:</span><span class="sxs-lookup"><span data-stu-id="347fd-146">Push the code from your local repository to your TFS repository with the following command:</span></span>

   `git push tfs --all`
1. <span data-ttu-id="347fd-147">A TFS-tárház tölti fel a Demo_CI kódot.</span><span class="sxs-lookup"><span data-stu-id="347fd-147">The TFS repository will be populated with the Demo_CI code.</span></span>

> [!NOTE]
> <span data-ttu-id="347fd-148">Ebben a példában a kódot használja a `ci-cd-example` a Git-tárház főágába.</span><span class="sxs-lookup"><span data-stu-id="347fd-148">This example uses the code in the `ci-cd-example` branch of the Git repo.</span></span>
> <span data-ttu-id="347fd-149">Ügyeljen arra, hogy az ág az alapértelmezett ágat a TFS-projekt adja meg, és a CI/CD eseményindítók hoz létre.</span><span class="sxs-lookup"><span data-stu-id="347fd-149">Be sure to specify this branch as the default branch in your TFS project, and for the CI/CD triggers you create.</span></span>

## <a name="understanding-the-code"></a><span data-ttu-id="347fd-150">A kód ismertetése</span><span class="sxs-lookup"><span data-stu-id="347fd-150">Understanding the code</span></span>

<span data-ttu-id="347fd-151">A buildelés és üzembe helyezés folyamatok létrehozhatunk, mielőtt vizsgáljuk meg néhány, a kód folyamatainak megértése.</span><span class="sxs-lookup"><span data-stu-id="347fd-151">Before we create the build and deployment pipelines, let's look at some of the code to understand what is going on.</span></span>
<span data-ttu-id="347fd-152">Az ügyfélszámítógépen nyissa meg a kedvenc szövegszerkesztőjével, és keresse meg a Demo_CI Git-tárház gyökérkönyvtárában.</span><span class="sxs-lookup"><span data-stu-id="347fd-152">On your client computer, open your favorite text editor and navigate to the root of your Demo_CI Git repository.</span></span>

### <a name="the-dsc-configuration"></a><span data-ttu-id="347fd-153">A DSC-konfiguráció</span><span class="sxs-lookup"><span data-stu-id="347fd-153">The DSC configuration</span></span>

<span data-ttu-id="347fd-154">Nyissa meg a fájlt `DNSServer.ps1` (a helyi Demo_CI tárház gyökérkönyvtárában `./InfraDNS/Configs/DNSServer.ps1`).</span><span class="sxs-lookup"><span data-stu-id="347fd-154">Open the file `DNSServer.ps1` (from the root of the local Demo_CI repository, `./InfraDNS/Configs/DNSServer.ps1`).</span></span>

<span data-ttu-id="347fd-155">Ez a fájl tartalmazza a DSC-konfiguráció, amely beállítja a DNS-kiszolgáló.</span><span class="sxs-lookup"><span data-stu-id="347fd-155">This file contains the DSC configuration that sets up the DNS server.</span></span> <span data-ttu-id="347fd-156">Itt van egészében:</span><span class="sxs-lookup"><span data-stu-id="347fd-156">Here it is in its entirety:</span></span>

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

<span data-ttu-id="347fd-157">Figyelje meg a `Node` utasítást:</span><span class="sxs-lookup"><span data-stu-id="347fd-157">Notice the `Node` statement:</span></span>

```powershell
Node $AllNodes.Where{$_.Role -eq 'DNSServer'}.NodeName
```

<span data-ttu-id="347fd-158">Ez azoknak a fürtöknek, egyik szerepköre rendelkezőként meghatározott talál `DNSServer` a a [konfigurációs adatok](configData.md), által létrehozott a `DevEnv.ps1` parancsfájl.</span><span class="sxs-lookup"><span data-stu-id="347fd-158">This finds any nodes that were defined as having a role of `DNSServer` in the [configuration data](configData.md), which is created by the `DevEnv.ps1` script.</span></span>

<span data-ttu-id="347fd-159">További információ a `Where` metódus a [about_arrays](/powershell/reference/3.0/Microsoft.PowerShell.Core/About/about_Arrays.md)</span><span class="sxs-lookup"><span data-stu-id="347fd-159">You can read more about the `Where` method in [about_arrays](/powershell/reference/3.0/Microsoft.PowerShell.Core/About/about_Arrays.md)</span></span>

<span data-ttu-id="347fd-160">Konfigurációs adatok segítségével határozza meg a csomópontok fontos CI során, mert a csomópont információk valószínűleg változik a különböző környezetek között, és a konfigurációs adatok használatával lehetővé teszi, könnyen módosíthatja csomópont adatokat a konfigurációs kódjának módosítása nélkül.</span><span class="sxs-lookup"><span data-stu-id="347fd-160">Using configuration data to define nodes is important when doing CI because node information will likely change between environments, and using configuration data allows you to easily make changes to node information without changing the configuration code.</span></span>

<span data-ttu-id="347fd-161">Az első erőforrás blokkban, a konfiguráció meghívja a [WindowsFeature](windowsFeatureResource.md) annak érdekében, hogy a DNS szolgáltatás engedélyezve van-e.</span><span class="sxs-lookup"><span data-stu-id="347fd-161">In the first resource block, the configuration calls the [WindowsFeature](windowsFeatureResource.md) to ensure that the DNS feature is enabled.</span></span>
<span data-ttu-id="347fd-162">A hívás erőforrások a következő erőforrás blokkolja a [xDnsServer](https://github.com/PowerShell/xDnsServer) modul elsődleges zóna és a DNS-rekordok konfigurálása.</span><span class="sxs-lookup"><span data-stu-id="347fd-162">The resource blocks that follow call resources from the [xDnsServer](https://github.com/PowerShell/xDnsServer) module to configure the primary zone and DNS records.</span></span>

<span data-ttu-id="347fd-163">Figyelje meg, hogy a két `xDnsRecord` blokkok csomagolni vannak `foreach` , amely a konfigurációs adatokat a tömbök iterációt hurkok.</span><span class="sxs-lookup"><span data-stu-id="347fd-163">Notice that the two `xDnsRecord` blocks are wrapped in `foreach` loops that iterate through arrays in the configuration data.</span></span>
<span data-ttu-id="347fd-164">Ebben az esetben a konfigurációs adatok hozta létre a `DevEnv.ps1` parancsfájl, amely megnézzük, a Tovább gombra.</span><span class="sxs-lookup"><span data-stu-id="347fd-164">Again, the configuration data is created by the `DevEnv.ps1` script, which we'll look at next.</span></span>

### <a name="configuration-data"></a><span data-ttu-id="347fd-165">Konfigurációs adatok</span><span class="sxs-lookup"><span data-stu-id="347fd-165">Configuration data</span></span>

<span data-ttu-id="347fd-166">A `DevEnv.ps1` fájlt (a helyi Demo_CI tárház gyökérkönyvtárában `./InfraDNS/DevEnv.ps1`) megadja egy kivonattáblát a környezet konfigurációs adatait, és majd hívásakor adja át, hogy hibás a `New-DscConfigurationDataDocument` függvény, amelyet a `DscPipelineTools.psm` (`./Assets/DscPipelineTools/DscPipelineTools.psm1`).</span><span class="sxs-lookup"><span data-stu-id="347fd-166">The `DevEnv.ps1` file (from the root of the local Demo_CI repository, `./InfraDNS/DevEnv.ps1`) specifies the environment-specific configuration data in a hashtable, and then passes that hashtable to a call to the `New-DscConfigurationDataDocument` function, which is defined in `DscPipelineTools.psm` (`./Assets/DscPipelineTools/DscPipelineTools.psm1`).</span></span>

<span data-ttu-id="347fd-167">A `DevEnv.ps1` fájlt:</span><span class="sxs-lookup"><span data-stu-id="347fd-167">The `DevEnv.ps1` file:</span></span>

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

<span data-ttu-id="347fd-168">A `New-DscConfigurationDataDocument` függvény (definiált `\Assets\DscPipelineTools\DscPipelineTools.psm1`) programozott módon a kivonattábla (adatai) és a tömb (nem csomópont adatait) szerint átadott a konfigurációs adatok dokumentum létrehozása a `RawEnvData` és `OtherEnvData` paraméterek.</span><span class="sxs-lookup"><span data-stu-id="347fd-168">The `New-DscConfigurationDataDocument` function (defined in `\Assets\DscPipelineTools\DscPipelineTools.psm1`) programmatically creates a configuration data document from the hashtable (node data) and array (non-node data) that are passed as the `RawEnvData` and `OtherEnvData` parameters.</span></span>

<span data-ttu-id="347fd-169">Ebben az esetben csak a `RawEnvData` paraméterrel.</span><span class="sxs-lookup"><span data-stu-id="347fd-169">In our case, only the `RawEnvData` parameter is used.</span></span>

### <a name="the-psake-build-script"></a><span data-ttu-id="347fd-170">A psake build script</span><span class="sxs-lookup"><span data-stu-id="347fd-170">The psake build script</span></span>

<span data-ttu-id="347fd-171">A [psake](https://github.com/psake/psake) definiált parancsfájl összeállítása `Build.ps1` (Demo_CI tárház gyökérkönyvtárában `./InfraDNS/Build.ps1`) határozza meg a build feladatainak.</span><span class="sxs-lookup"><span data-stu-id="347fd-171">The [psake](https://github.com/psake/psake) build script defined in `Build.ps1` (from the root of the Demo_CI repository, `./InfraDNS/Build.ps1`) defines tasks that are part of the build.</span></span>
<span data-ttu-id="347fd-172">Minden tevékenység attól függ, milyen egyéb feladatokat is meghatározza.</span><span class="sxs-lookup"><span data-stu-id="347fd-172">It also defines which other tasks each task depends on.</span></span>
<span data-ttu-id="347fd-173">Meghívásakor, a psake parancsfájl biztosítja, hogy a megadott feladat (vagy nevű feladat `Default` Ha nincs megadva) fut, és, hogy az összes függősége is futtathatnak (rekurzív, azt, hogy a függőségek függőségek, és így tovább).</span><span class="sxs-lookup"><span data-stu-id="347fd-173">When invoked, the psake script ensures that the specified task (or the task named `Default` if none is specified) runs, and that all dependencies also run (this is recursive, so that dependencies of dependencies run, and so on).</span></span>

<span data-ttu-id="347fd-174">Ebben a példában a `Default` feladat típusúként van definiálva:</span><span class="sxs-lookup"><span data-stu-id="347fd-174">In this example, the `Default` task is defined as:</span></span>

```powershell
Task Default -depends UnitTests
```

<span data-ttu-id="347fd-175">A `Default` feladat nem tartozik megvalósítás magát, de függ a `CompileConfigs` feladat.</span><span class="sxs-lookup"><span data-stu-id="347fd-175">The `Default` task has no implementation itself, but has a dependency on the `CompileConfigs` task.</span></span>
<span data-ttu-id="347fd-176">Az eredményül kapott lánc feladat függőségi biztosítja, hogy futnak-e a build parancsfájlban szereplő összes feladatot.</span><span class="sxs-lookup"><span data-stu-id="347fd-176">The resulting chain of task dependencies ensures that all tasks in the build script are run.</span></span>

<span data-ttu-id="347fd-177">Ebben a példában a psake parancsfájl hívásával meghívott `Invoke-PSake` a a `Initiate.ps1` fájlt (a Demo_CI tárház gyökérkönyvtárában található):</span><span class="sxs-lookup"><span data-stu-id="347fd-177">In this example, the psake script is invoked by a call to `Invoke-PSake` in the `Initiate.ps1` file (located at the root of the Demo_CI repository):</span></span>

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

<span data-ttu-id="347fd-178">Létrehozásakor a build definícióját a fenti példában a TFS-ben, azt fogja adni a psake parancsfájlt, mint a `fileName` paraméter ehhez a parancsprogramhoz.</span><span class="sxs-lookup"><span data-stu-id="347fd-178">When we create the build definition for our example in TFS, we will supply our psake script file as the `fileName` parameter for this script.</span></span>

<span data-ttu-id="347fd-179">A build parancsfájl meghatározza, hogy a következő feladatokat:</span><span class="sxs-lookup"><span data-stu-id="347fd-179">The build script defines the following tasks:</span></span>

#### <a name="generateenvironmentfiles"></a><span data-ttu-id="347fd-180">GenerateEnvironmentFiles</span><span class="sxs-lookup"><span data-stu-id="347fd-180">GenerateEnvironmentFiles</span></span>

<span data-ttu-id="347fd-181">Futtatása `DevEnv.ps1`, amely a konfigurációs adatok fájlt hoz létre.</span><span class="sxs-lookup"><span data-stu-id="347fd-181">Runs `DevEnv.ps1`, which generates the configuration data file.</span></span>

#### <a name="installmodules"></a><span data-ttu-id="347fd-182">InstallModules</span><span class="sxs-lookup"><span data-stu-id="347fd-182">InstallModules</span></span>

<span data-ttu-id="347fd-183">Telepíti a modulok, a konfiguráció szükséges `DNSServer.ps1`.</span><span class="sxs-lookup"><span data-stu-id="347fd-183">Installs the modules required by the configuration `DNSServer.ps1`.</span></span>

#### <a name="scriptanalysis"></a><span data-ttu-id="347fd-184">ScriptAnalysis</span><span class="sxs-lookup"><span data-stu-id="347fd-184">ScriptAnalysis</span></span>

<span data-ttu-id="347fd-185">Hívások a [PSScriptAnalyzer](https://github.com/PowerShell/PSScriptAnalyzer).</span><span class="sxs-lookup"><span data-stu-id="347fd-185">Calls the [PSScriptAnalyzer](https://github.com/PowerShell/PSScriptAnalyzer).</span></span>

#### <a name="unittests"></a><span data-ttu-id="347fd-186">UnitTests</span><span class="sxs-lookup"><span data-stu-id="347fd-186">UnitTests</span></span>

<span data-ttu-id="347fd-187">Fut a [Pester](https://github.com/pester/Pester/wiki) egység teszteket.</span><span class="sxs-lookup"><span data-stu-id="347fd-187">Runs the [Pester](https://github.com/pester/Pester/wiki) unit tests.</span></span>

#### <a name="compileconfigs"></a><span data-ttu-id="347fd-188">CompileConfigs</span><span class="sxs-lookup"><span data-stu-id="347fd-188">CompileConfigs</span></span>

<span data-ttu-id="347fd-189">Lefordítja a konfigurációs (`DNSServer.ps1`) által létrehozott konfigurációs adatok használatával MOF-fájlba, a `GenerateEnvironmentFiles` feladat.</span><span class="sxs-lookup"><span data-stu-id="347fd-189">Compiles the configuration (`DNSServer.ps1`) into a MOF file, using the configuration data generated by the `GenerateEnvironmentFiles` task.</span></span>

#### <a name="clean"></a><span data-ttu-id="347fd-190">Clean</span><span class="sxs-lookup"><span data-stu-id="347fd-190">Clean</span></span>

<span data-ttu-id="347fd-191">A például szolgáló mappákat hoz létre, és a vizsgálati eredmények, a konfigurációs adatok fájlok és a modulok eltávolítja a korábbi futtatásakor.</span><span class="sxs-lookup"><span data-stu-id="347fd-191">Creates the folders used for the example, and removes any test results, configuration data files, and modules from previous runs.</span></span>

### <a name="the-psake-deploy-script"></a><span data-ttu-id="347fd-192">A psake parancsfájl központi telepítése</span><span class="sxs-lookup"><span data-stu-id="347fd-192">The psake deploy script</span></span>

<span data-ttu-id="347fd-193">A [psake](https://github.com/psake/psake) meghatározott telepítési parancsfájl `Deploy.ps1` (Demo_CI tárház gyökérkönyvtárában `./InfraDNS/Deploy.ps1`) telepítése, és futtassa a konfigurációs feladatokat, határozza meg.</span><span class="sxs-lookup"><span data-stu-id="347fd-193">The [psake](https://github.com/psake/psake) deployment script defined in `Deploy.ps1` (from the root of the Demo_CI repository, `./InfraDNS/Deploy.ps1`) defines tasks that deploy and run the configuration.</span></span>

<span data-ttu-id="347fd-194">`Deploy.ps1` Meghatározza, hogy a következő feladatokat:</span><span class="sxs-lookup"><span data-stu-id="347fd-194">`Deploy.ps1` defines the following tasks:</span></span>

#### <a name="deploymodules"></a><span data-ttu-id="347fd-195">DeployModules</span><span class="sxs-lookup"><span data-stu-id="347fd-195">DeployModules</span></span>

<span data-ttu-id="347fd-196">A PowerShell-munkamenetben megkezdése `TestAgent1` és telepíti a konfiguráláshoz szükséges DSC erőforrásokat tartalmazó modult.</span><span class="sxs-lookup"><span data-stu-id="347fd-196">Starts a PowerShell session on `TestAgent1` and installs the modules containing the DSC resources required for the configuration.</span></span>

#### <a name="deployconfigs"></a><span data-ttu-id="347fd-197">DeployConfigs</span><span class="sxs-lookup"><span data-stu-id="347fd-197">DeployConfigs</span></span>

<span data-ttu-id="347fd-198">Hívások a [Start-DscConfiguration](/reference/5.1/PSDesiredStateConfiguration/Start-DscConfiguration.md) parancsmag segítségével futtassa a konfigurációs `TestAgent1`.</span><span class="sxs-lookup"><span data-stu-id="347fd-198">Calls the [Start-DscConfiguration](/reference/5.1/PSDesiredStateConfiguration/Start-DscConfiguration.md) cmdlet to run the configuration on `TestAgent1`.</span></span>

#### <a name="integrationtests"></a><span data-ttu-id="347fd-199">IntegrationTests</span><span class="sxs-lookup"><span data-stu-id="347fd-199">IntegrationTests</span></span>

<span data-ttu-id="347fd-200">Fut a [Pester](https://github.com/pester/Pester/wiki) integrációs teszteket.</span><span class="sxs-lookup"><span data-stu-id="347fd-200">Runs the [Pester](https://github.com/pester/Pester/wiki) integration tests.</span></span>

#### <a name="acceptancetests"></a><span data-ttu-id="347fd-201">AcceptanceTests</span><span class="sxs-lookup"><span data-stu-id="347fd-201">AcceptanceTests</span></span>

<span data-ttu-id="347fd-202">Fut a [Pester](https://github.com/pester/Pester/wiki) elfogadási teszteket.</span><span class="sxs-lookup"><span data-stu-id="347fd-202">Runs the [Pester](https://github.com/pester/Pester/wiki) acceptance tests.</span></span>

#### <a name="clean"></a><span data-ttu-id="347fd-203">Clean</span><span class="sxs-lookup"><span data-stu-id="347fd-203">Clean</span></span>

<span data-ttu-id="347fd-204">Eltávolítja a korábbi fut telepített modul, és biztosítja, hogy létezik-e a teszt eredménye mappa.</span><span class="sxs-lookup"><span data-stu-id="347fd-204">Removes any modules installed in previous runs, and ensures that the test result folder exists.</span></span>

### <a name="test-scripts"></a><span data-ttu-id="347fd-205">Parancsfájlok tesztelése</span><span class="sxs-lookup"><span data-stu-id="347fd-205">Test scripts</span></span>

<span data-ttu-id="347fd-206">Elfogadási, integráció és egység tesztek határozzák meg a parancsfájlok a `Tests` mappa (Demo_CI tárház gyökérkönyvtárában `./InfraDNS/Tests`), a nevű fájlt minden egyes `DNSServer.tests.ps1` megfelelő mappáiban.</span><span class="sxs-lookup"><span data-stu-id="347fd-206">Acceptance, Integration, and Unit tests are defined in scripts in the `Tests` folder (from the root of the Demo_CI repository, `./InfraDNS/Tests`), each in files named `DNSServer.tests.ps1` in their respective folders.</span></span>

<span data-ttu-id="347fd-207">A vizsgálat a parancsfájlok használata [Pester](https://github.com/pester/Pester/wiki) és [PoshSpec](https://github.com/Ticketmaster/poshspec/wiki/Introduction) szintaxist.</span><span class="sxs-lookup"><span data-stu-id="347fd-207">The test scripts use [Pester](https://github.com/pester/Pester/wiki) and [PoshSpec](https://github.com/Ticketmaster/poshspec/wiki/Introduction) syntax.</span></span>

#### <a name="unit-tests"></a><span data-ttu-id="347fd-208">Egység tesztek</span><span class="sxs-lookup"><span data-stu-id="347fd-208">Unit tests</span></span>

<span data-ttu-id="347fd-209">Az egység magát győződjön meg arról, hogy a konfigurációk hajt végre a futtatásakor. várt teszt a DSC-konfigurációk teszteli.</span><span class="sxs-lookup"><span data-stu-id="347fd-209">The unit tests test the DSC configurations themselves to ensure that the configurations will do what is expected when they run.</span></span>
<span data-ttu-id="347fd-210">Az egység tesztelése parancsfájl által használt [Pester](https://github.com/pester/Pester/wiki).</span><span class="sxs-lookup"><span data-stu-id="347fd-210">The unit test script uses [Pester](https://github.com/pester/Pester/wiki).</span></span>

#### <a name="integration-tests"></a><span data-ttu-id="347fd-211">Integráció tesztek</span><span class="sxs-lookup"><span data-stu-id="347fd-211">Integration tests</span></span>

<span data-ttu-id="347fd-212">Az integráció tesztek tesztelje a konfigurációt a rendszer annak érdekében, hogy ha más összetevők integrálva, a rendszer elvártak szerint van konfigurálva.</span><span class="sxs-lookup"><span data-stu-id="347fd-212">The integration tests test the configuration of the system to ensure that when integrated with other components, the system is configured as expected.</span></span> <span data-ttu-id="347fd-213">Ezek a tesztek futtatása célcsomóponton után a DSC lett konfigurálva.</span><span class="sxs-lookup"><span data-stu-id="347fd-213">These tests run on the target node after it has been configured with DSC.</span></span>
<span data-ttu-id="347fd-214">Az integráció teszt parancsfájl keverékével [Pester](https://github.com/pester/Pester/wiki) és [PoshSpec](https://github.com/Ticketmaster/poshspec/wiki/Introduction) szintaxist.</span><span class="sxs-lookup"><span data-stu-id="347fd-214">The integration test script uses a mixture of [Pester](https://github.com/pester/Pester/wiki) and [PoshSpec](https://github.com/Ticketmaster/poshspec/wiki/Introduction) syntax.</span></span>

#### <a name="acceptance-tests"></a><span data-ttu-id="347fd-215">Elfogadási tesztek</span><span class="sxs-lookup"><span data-stu-id="347fd-215">Acceptance tests</span></span>

<span data-ttu-id="347fd-216">Elfogadási vizsgálatok tesztelje a rendszer annak érdekében, hogy úgy viselkedik a várt módon.</span><span class="sxs-lookup"><span data-stu-id="347fd-216">Acceptance tests test the system to ensure that it behaves as expected.</span></span>
<span data-ttu-id="347fd-217">Például ezt megvizsgálja, győződjön meg arról, webes történő lekérdezéskor megfelelő információkat ad vissza.</span><span class="sxs-lookup"><span data-stu-id="347fd-217">For example, it tests to ensure a web page returns the right information when queried.</span></span>
<span data-ttu-id="347fd-218">Ezek a tesztek távolról futtatni a célcsomópont a valós életben előforduló helyzetek teszteléséhez.</span><span class="sxs-lookup"><span data-stu-id="347fd-218">These tests run remotely from the target node in order to test real world scenarios.</span></span>
<span data-ttu-id="347fd-219">Az integráció teszt parancsfájl keverékével [Pester](https://github.com/pester/Pester/wiki) és [PoshSpec](https://github.com/Ticketmaster/poshspec/wiki/Introduction) szintaxist.</span><span class="sxs-lookup"><span data-stu-id="347fd-219">The integration test script uses a mixture of [Pester](https://github.com/pester/Pester/wiki) and [PoshSpec](https://github.com/Ticketmaster/poshspec/wiki/Introduction) syntax.</span></span>

## <a name="define-the-build"></a><span data-ttu-id="347fd-220">A build meghatározása</span><span class="sxs-lookup"><span data-stu-id="347fd-220">Define the build</span></span>

<span data-ttu-id="347fd-221">Most, hogy elvégeztük TFS kód feltölti és tekintett meg működés, is határozza meg a build.</span><span class="sxs-lookup"><span data-stu-id="347fd-221">Now that we've uploaded our code to TFS and looked at what it does, let's define our build.</span></span>

<span data-ttu-id="347fd-222">Itt azt érintünk csak a fogja hozzáadni a buildre build lépéseket.</span><span class="sxs-lookup"><span data-stu-id="347fd-222">Here, we'll cover only the build steps that you'll add to the build.</span></span> <span data-ttu-id="347fd-223">Build definíció létrehozása a TFS-ben, lásd: [létrehozása és a várólista build definíció](https://www.visualstudio.com/en-us/docs/build/define/create).</span><span class="sxs-lookup"><span data-stu-id="347fd-223">For instructions on how to create a build definition in TFS, see [Create and queue a build definition](https://www.visualstudio.com/en-us/docs/build/define/create).</span></span>

<span data-ttu-id="347fd-224">Hozzon létre egy új build definition (válassza ki a **üres** sablon) "InfraDNS" nevű.</span><span class="sxs-lookup"><span data-stu-id="347fd-224">Create a new build definition (select the **Empty** template) named "InfraDNS".</span></span>
<span data-ttu-id="347fd-225">Adja hozzá az alábbi lépések végrehajtásával meg build definíciója:</span><span class="sxs-lookup"><span data-stu-id="347fd-225">Add the following steps to you build definition:</span></span>

- <span data-ttu-id="347fd-226">PowerShell-parancsfájl</span><span class="sxs-lookup"><span data-stu-id="347fd-226">PowerShell Script</span></span>
- <span data-ttu-id="347fd-227">Vizsgálati eredmények közzététele</span><span class="sxs-lookup"><span data-stu-id="347fd-227">Publish Test Results</span></span>
- <span data-ttu-id="347fd-228">Fájlok másolása</span><span class="sxs-lookup"><span data-stu-id="347fd-228">Copy Files</span></span>
- <span data-ttu-id="347fd-229">Összetevő közzététele</span><span class="sxs-lookup"><span data-stu-id="347fd-229">Publish Artifact</span></span>

<span data-ttu-id="347fd-230">Ezek lépések felépítéséhez, az alábbiak szerint minden lépés tulajdonságainak szerkesztése hozzáadása után:</span><span class="sxs-lookup"><span data-stu-id="347fd-230">After adding these build steps, edit the properties of each step as follows:</span></span>

### <a name="powershell-script"></a><span data-ttu-id="347fd-231">PowerShell-parancsfájl</span><span class="sxs-lookup"><span data-stu-id="347fd-231">PowerShell Script</span></span>

1. <span data-ttu-id="347fd-232">Állítsa be a **típus** tulajdonságot `File Path`.</span><span class="sxs-lookup"><span data-stu-id="347fd-232">Set the **Type** property to `File Path`.</span></span>
1. <span data-ttu-id="347fd-233">Állítsa be a **parancsfájl elérési útján** tulajdonságot `initiate.ps1`.</span><span class="sxs-lookup"><span data-stu-id="347fd-233">Set the **Script Path** property to `initiate.ps1`.</span></span>
1. <span data-ttu-id="347fd-234">Adja hozzá `-fileName build` számára a **argumentumok** tulajdonság.</span><span class="sxs-lookup"><span data-stu-id="347fd-234">Add `-fileName build` to the **Arguments** property.</span></span>

<span data-ttu-id="347fd-235">Ez a lépés build a `initiate.ps1` fájlt, amely meghívja a psake build parancsfájlt.</span><span class="sxs-lookup"><span data-stu-id="347fd-235">This build step runs the `initiate.ps1` file, which calls the psake build script.</span></span>

### <a name="publish-test-results"></a><span data-ttu-id="347fd-236">Vizsgálati eredmények közzététele</span><span class="sxs-lookup"><span data-stu-id="347fd-236">Publish Test Results</span></span>

1. <span data-ttu-id="347fd-237">Állítsa be **Eredményformátum tesztelése** számára `NUnit`</span><span class="sxs-lookup"><span data-stu-id="347fd-237">Set **Test Result Format** to `NUnit`</span></span>
1. <span data-ttu-id="347fd-238">Állítsa be **teszteredményei fájlok** számára `InfraDNS/Tests/Results/*.xml`</span><span class="sxs-lookup"><span data-stu-id="347fd-238">Set **Test Results Files** to `InfraDNS/Tests/Results/*.xml`</span></span>
1. <span data-ttu-id="347fd-239">Állítsa be **futtatási cím tesztelése** való `Unit`.</span><span class="sxs-lookup"><span data-stu-id="347fd-239">Set **Test Run Title** to `Unit`.</span></span>
1. <span data-ttu-id="347fd-240">Győződjön meg arról, hogy **beállítások** **engedélyezve** és **mindig fusson** biztosan mindkét kiválasztott.</span><span class="sxs-lookup"><span data-stu-id="347fd-240">Make sure **Control Options** **Enabled** and **Always run** are both selected.</span></span>

<span data-ttu-id="347fd-241">A build lépés a egység tesztek fut a Microsoft megvizsgálta a korábbi Pester parancsfájl, és tárolja az eredményeket a `InfraDNS/Tests/Results/*.xml` mappát.</span><span class="sxs-lookup"><span data-stu-id="347fd-241">This build step runs the unit tests in the Pester script we looked at earlier, and stores the results in the `InfraDNS/Tests/Results/*.xml` folder.</span></span>

### <a name="copy-files"></a><span data-ttu-id="347fd-242">Fájlok másolása</span><span class="sxs-lookup"><span data-stu-id="347fd-242">Copy Files</span></span>

1. <span data-ttu-id="347fd-243">Adja hozzá a következő sorok **tartalma**:</span><span class="sxs-lookup"><span data-stu-id="347fd-243">Add each of the following lines to **Contents**:</span></span>

   ```
   initiate.ps1
   **\deploy.ps1
   **\Acceptance\**
   **\Integration\**
   ```

1. <span data-ttu-id="347fd-244">Állítsa be **TargetFolder** számára `$(Build.ArtifactStagingDirectory)\`</span><span class="sxs-lookup"><span data-stu-id="347fd-244">Set **TargetFolder** to `$(Build.ArtifactStagingDirectory)\`</span></span>

<span data-ttu-id="347fd-245">Ezt a lépést, másolja át a összeállítása és tesztelése a parancsfájlok az átmeneti könyvtárhoz úgy, hogy a tehetők közzé, az összetevők létrehozása a következő lépésben.</span><span class="sxs-lookup"><span data-stu-id="347fd-245">This step copies the build and test scripts to the staging directory so that the can be published as build artifacts by the next step.</span></span>

### <a name="publish-artifact"></a><span data-ttu-id="347fd-246">Összetevő közzététele</span><span class="sxs-lookup"><span data-stu-id="347fd-246">Publish Artifact</span></span>

1. <span data-ttu-id="347fd-247">Állítsa be **közzététele elérési út** számára `$(Build.ArtifactStagingDirectory)\`</span><span class="sxs-lookup"><span data-stu-id="347fd-247">Set **Path to Publish** to `$(Build.ArtifactStagingDirectory)\`</span></span>
1. <span data-ttu-id="347fd-248">Állítsa be **Adatösszetevőt nevét** számára `Deploy`</span><span class="sxs-lookup"><span data-stu-id="347fd-248">Set **Artifact Name** to `Deploy`</span></span>
1. <span data-ttu-id="347fd-249">Állítsa be **összetevő típus** számára `Server`</span><span class="sxs-lookup"><span data-stu-id="347fd-249">Set **Artifact Type** to `Server`</span></span>
1. <span data-ttu-id="347fd-250">Válassza ki `Enabled` a **beállításokat**</span><span class="sxs-lookup"><span data-stu-id="347fd-250">Select `Enabled` in **Control Options**</span></span>

## <a name="enable-continuous-integration"></a><span data-ttu-id="347fd-251">Folyamatos integráció engedélyezése</span><span class="sxs-lookup"><span data-stu-id="347fd-251">Enable continuous integration</span></span>

<span data-ttu-id="347fd-252">Most egy eseményindítót, melynek következtében a projekt felépítéséhez bármikor be lesznek állítva a módosítása a beadása a `ci-cd-example` a git-tárház főágába.</span><span class="sxs-lookup"><span data-stu-id="347fd-252">Now we'll set up a trigger that causes the project to build any time a change is checked in to the `ci-cd-example` branch of the git repository.</span></span>

1. <span data-ttu-id="347fd-253">A TFS rendszerben kattintson a **Build & kiadási** lap</span><span class="sxs-lookup"><span data-stu-id="347fd-253">In TFS, click the **Build & Release** tab</span></span>
1. <span data-ttu-id="347fd-254">Válassza ki a `DNS Infra` definíció létrehozása, és kattintson a **szerkesztése**</span><span class="sxs-lookup"><span data-stu-id="347fd-254">Select the `DNS Infra` build definition, and click **Edit**</span></span>
1. <span data-ttu-id="347fd-255">Kattintson a **eseményindítók** lap</span><span class="sxs-lookup"><span data-stu-id="347fd-255">Click the **Triggers** tab</span></span>
1. <span data-ttu-id="347fd-256">Válassza ki **folyamatos integrációt (CI)**, és válassza ki `refs/heads/ci-cd-example` a fiókiroda legördülő lista</span><span class="sxs-lookup"><span data-stu-id="347fd-256">Select **Continuous integration (CI)**, and select `refs/heads/ci-cd-example` in the branch drop-down list</span></span>
1. <span data-ttu-id="347fd-257">Kattintson a **mentése** , majd **OK**</span><span class="sxs-lookup"><span data-stu-id="347fd-257">Click **Save** and then **OK**</span></span>

<span data-ttu-id="347fd-258">Most már minden változása a TFS git-tárház eseményindítók egy automatizált build.</span><span class="sxs-lookup"><span data-stu-id="347fd-258">Now any change in the TFS git repository triggers an automated build.</span></span>

## <a name="create-the-release-definition"></a><span data-ttu-id="347fd-259">A kiadási definíció létrehozása</span><span class="sxs-lookup"><span data-stu-id="347fd-259">Create the release definition</span></span>

<span data-ttu-id="347fd-260">Hozzon létre egy kiadási definícióját, hogy a projekt központi telepítése a fejlesztési környezet minden kód be.</span><span class="sxs-lookup"><span data-stu-id="347fd-260">Let's create a release definition so that the project is deployed to the development environment with every code check-in.</span></span>

<span data-ttu-id="347fd-261">Ehhez az szükséges, hozzáadása új kiadási társított a `InfraDNS` korábban létrehozott definíció létrehozása.</span><span class="sxs-lookup"><span data-stu-id="347fd-261">To do this, add a new release definition associated with the `InfraDNS` build definition you created previously.</span></span>
<span data-ttu-id="347fd-262">Ügyeljen arra, hogy válasszon **folyamatos üzembe helyezés** , hogy az új kiadási indul bármikor új buildverziót befejeződött.</span><span class="sxs-lookup"><span data-stu-id="347fd-262">Be sure to select **Continuous deployment** so that a new release will be triggered any time a new build is completed.</span></span>
<span data-ttu-id="347fd-263">([Hogyan: kiadás definíciók együttműködve](https://www.visualstudio.com/en-us/docs/build/actions/work-with-release-definitions)), és konfigurálja az alábbiak szerint:</span><span class="sxs-lookup"><span data-stu-id="347fd-263">([How to: Work with release definitions](https://www.visualstudio.com/en-us/docs/build/actions/work-with-release-definitions)) and configure it as follows:</span></span>

<span data-ttu-id="347fd-264">A kiadási definition vegye fel az alábbi lépéseket:</span><span class="sxs-lookup"><span data-stu-id="347fd-264">Add the following steps to the release definition:</span></span>

- <span data-ttu-id="347fd-265">PowerShell-parancsfájl</span><span class="sxs-lookup"><span data-stu-id="347fd-265">PowerShell Script</span></span>
- <span data-ttu-id="347fd-266">Vizsgálati eredmények közzététele</span><span class="sxs-lookup"><span data-stu-id="347fd-266">Publish Test Results</span></span>
- <span data-ttu-id="347fd-267">Vizsgálati eredmények közzététele</span><span class="sxs-lookup"><span data-stu-id="347fd-267">Publish Test Results</span></span>

<span data-ttu-id="347fd-268">A lépések az alábbiak szerint szerkesztése:</span><span class="sxs-lookup"><span data-stu-id="347fd-268">Edit the steps as follows:</span></span>

### <a name="powershell-script"></a><span data-ttu-id="347fd-269">PowerShell-parancsfájl</span><span class="sxs-lookup"><span data-stu-id="347fd-269">PowerShell Script</span></span>

1. <span data-ttu-id="347fd-270">Állítsa be a **parancsfájl elérési útján** mezőről `$(Build.DefinitionName)\Deploy\initiate.ps1"`</span><span class="sxs-lookup"><span data-stu-id="347fd-270">Set the **Script Path** field to `$(Build.DefinitionName)\Deploy\initiate.ps1"`</span></span>
1. <span data-ttu-id="347fd-271">Állítsa be a **argumentumok** mezőről `-fileName Deploy`</span><span class="sxs-lookup"><span data-stu-id="347fd-271">Set the **Arguments** field to `-fileName Deploy`</span></span>

### <a name="first-publish-test-results"></a><span data-ttu-id="347fd-272">Először a vizsgálati eredmények közzététele</span><span class="sxs-lookup"><span data-stu-id="347fd-272">First Publish Test Results</span></span>

1. <span data-ttu-id="347fd-273">Válassza ki `NUnit` a a **teszt Eredményformátum** mező</span><span class="sxs-lookup"><span data-stu-id="347fd-273">Select `NUnit` for the **Test Result Format** field</span></span>
1. <span data-ttu-id="347fd-274">Állítsa be a **vizsgálati eredményeket tartalmazó fájlokat** mezőről `$(Build.DefinitionName)\Deploy\InfraDNS\Tests\Results\Integration*.xml`</span><span class="sxs-lookup"><span data-stu-id="347fd-274">Set the **Test Result Files** field to `$(Build.DefinitionName)\Deploy\InfraDNS\Tests\Results\Integration*.xml`</span></span>
1. <span data-ttu-id="347fd-275">Állítsa be a **futtatási cím tesztelése** számára `Integration`</span><span class="sxs-lookup"><span data-stu-id="347fd-275">Set the **Test Run Title** to `Integration`</span></span>
1. <span data-ttu-id="347fd-276">A **beállítások**, ellenőrizze **mindig futtatása**</span><span class="sxs-lookup"><span data-stu-id="347fd-276">Under **Control Options**, check **Always run**</span></span>

### <a name="second-publish-test-results"></a><span data-ttu-id="347fd-277">Vizsgálati eredmények második közzététele</span><span class="sxs-lookup"><span data-stu-id="347fd-277">Second Publish Test Results</span></span>

1. <span data-ttu-id="347fd-278">Válassza ki `NUnit` a a **teszt Eredményformátum** mező</span><span class="sxs-lookup"><span data-stu-id="347fd-278">Select `NUnit` for the **Test Result Format** field</span></span>
1. <span data-ttu-id="347fd-279">Állítsa be a **vizsgálati eredményeket tartalmazó fájlokat** mezőről `$(Build.DefinitionName)\Deploy\InfraDNS\Tests\Results\Acceptance*.xml`</span><span class="sxs-lookup"><span data-stu-id="347fd-279">Set the **Test Result Files** field to `$(Build.DefinitionName)\Deploy\InfraDNS\Tests\Results\Acceptance*.xml`</span></span>
1. <span data-ttu-id="347fd-280">Állítsa be a **futtatási cím tesztelése** számára `Acceptance`</span><span class="sxs-lookup"><span data-stu-id="347fd-280">Set the **Test Run Title** to `Acceptance`</span></span>
1. <span data-ttu-id="347fd-281">A **beállítások**, ellenőrizze **mindig futtatása**</span><span class="sxs-lookup"><span data-stu-id="347fd-281">Under **Control Options**, check **Always run**</span></span>

## <a name="verify-your-results"></a><span data-ttu-id="347fd-282">Az eredmények ellenőrzése</span><span class="sxs-lookup"><span data-stu-id="347fd-282">Verify your results</span></span>

<span data-ttu-id="347fd-283">Most, bármikor leküldéses módosítások a `ci-cd-example` TFS és az új buildverziót ág indul el.</span><span class="sxs-lookup"><span data-stu-id="347fd-283">Now, any time you push changes in the `ci-cd-example` branch to TFS, a new build will start.</span></span>
<span data-ttu-id="347fd-284">A létrehozás sikeresen befejeződik, ha egy új központi telepítési elindul.</span><span class="sxs-lookup"><span data-stu-id="347fd-284">If the build completes successfully, a new deployment is triggered.</span></span>

<span data-ttu-id="347fd-285">Ellenőrizheti a telepítés eredményét, nyisson meg egy böngészőt, az ügyfélszámítógépen, és navigáljon `www.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="347fd-285">You can check the result of the deployment by opening a browser on the client machine and navigating to `www.contoso.com`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="347fd-286">További lépések</span><span class="sxs-lookup"><span data-stu-id="347fd-286">Next steps</span></span>

<span data-ttu-id="347fd-287">Ebben a példában a DNS-kiszolgáló konfigurálása `TestAgent1` , hogy az URL-cím `www.contoso.com` oldja fel `TestAgent2`, de nem telepítheti valójában a webhely.</span><span class="sxs-lookup"><span data-stu-id="347fd-287">This example configures the DNS server `TestAgent1` so that the URL `www.contoso.com` resolves to `TestAgent2`, but it does not actually deploy a website.</span></span>
<span data-ttu-id="347fd-288">A vázat úgy valósul meg a tárházban alatt a `WebApp` mappát.</span><span class="sxs-lookup"><span data-stu-id="347fd-288">The skeleton for doing so is provided in the repo under the `WebApp` folder.</span></span>
<span data-ttu-id="347fd-289">A kódcsonkok psake parancsfájlok, Pester a és a DSC-konfigurációk létrehozásához megadott segítségével telepítheti a saját webhelyén.</span><span class="sxs-lookup"><span data-stu-id="347fd-289">You can use the stubs provided to create psake scripts, Pester tests, and DSC configurations to deploy your own website.</span></span>