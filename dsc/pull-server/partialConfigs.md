---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: Részleges konfigurációk PowerShell Desired State Configuration
ms.openlocfilehash: b2b17e35597707eb97ecdcea9dda4466deeab0cb
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/14/2018
ms.locfileid: "53404277"
---
# <a name="powershell-desired-state-configuration-partial-configurations"></a><span data-ttu-id="332d4-103">Részleges konfigurációk PowerShell Desired State Configuration</span><span class="sxs-lookup"><span data-stu-id="332d4-103">PowerShell Desired State Configuration partial configurations</span></span>

<span data-ttu-id="332d4-104">_A következőkre vonatkozik: Windows PowerShell 5.0-s és újabb verziók._</span><span class="sxs-lookup"><span data-stu-id="332d4-104">_Applies To: Windows PowerShell 5.0 and later._</span></span>

<span data-ttu-id="332d4-105">A PowerShell 5.0-s Desired State Configuration (DSC) lehetővé teszi a konfigurációkat a töredékeket, és a különböző forrásokból származó üzembe helyezhető.</span><span class="sxs-lookup"><span data-stu-id="332d4-105">In PowerShell 5.0, Desired State Configuration (DSC) allows configurations to be delivered in fragments and from multiple sources.</span></span> <span data-ttu-id="332d4-106">A helyi Configuration Manager (LCM) Konfigurálása a cél-csomóponton a szilánkok mielőtt alkalmazná őket, egyetlen konfigurációval együtt helyezi.</span><span class="sxs-lookup"><span data-stu-id="332d4-106">The Local Configuration Manager (LCM) on the target node puts the fragments together before applying them as a single configuration.</span></span> <span data-ttu-id="332d4-107">Ez a funkció lehetővé teszi, hogy a döntés konfigurációról csapatok vagy személyek közötti megosztását.</span><span class="sxs-lookup"><span data-stu-id="332d4-107">This capability allows sharing control of configuration between teams or individuals.</span></span> <span data-ttu-id="332d4-108">Például ha egy szolgáltatás a fejlesztők két vagy több csapat közreműködő, előfordulhat, hogy minden egyes szeretne létrehozni konfigurációk kezelésére, azok a szolgáltatás részét.</span><span class="sxs-lookup"><span data-stu-id="332d4-108">For example, if two or more teams of developers are collaborating on a service, they might each want to create configurations to manage their part of the service.</span></span> <span data-ttu-id="332d4-109">Ezek a konfigurációk mindegyike sikerült le kell kérnie a különböző lekéréses kiszolgálót, és különböző szakaszaiban a fejlesztési adható.</span><span class="sxs-lookup"><span data-stu-id="332d4-109">Each of these configurations could be pulled from different pull servers, and they could be added at different stages of development.</span></span> <span data-ttu-id="332d4-110">Részleges konfigurációk is lehetővé teszik különböző csapatok vagy személyek különböző aspektusa csomópontok konfigurálása koordinálására, egy egyetlen konfigurációs dokumentum szerkesztése nélkül.</span><span class="sxs-lookup"><span data-stu-id="332d4-110">Partial configurations also allow different individuals or teams to control different aspects of configuring nodes without having to coordinate the editing of a single configuration document.</span></span> <span data-ttu-id="332d4-111">Például egy csapat felelős üzembe helyezése egy virtuális gép és az operációs rendszer, amíg egy másik csapat helyezhetők üzembe, más alkalmazások és szolgáltatások a virtuális gép lehet.</span><span class="sxs-lookup"><span data-stu-id="332d4-111">For example, one team might be responsible for deploying a VM and operating system, while another team might deploy other applications and services on that VM.</span></span> <span data-ttu-id="332d4-112">Részleges konfigurációk minden egyes csapat hozhat létre a saját konfigurációs nélkül lehet őket szükségtelenül bonyolult folyamatban van.</span><span class="sxs-lookup"><span data-stu-id="332d4-112">With partial configurations, each team can create its own configuration, without either of them being unnecessarily complicated.</span></span>

<span data-ttu-id="332d4-113">Részleges konfigurációk leküldéses módban, lekéréses mód vagy a kettő kombinációját is használhatja.</span><span class="sxs-lookup"><span data-stu-id="332d4-113">You can use partial configurations in push mode, pull mode, or a combination of the two.</span></span>

## <a name="partial-configurations-in-push-mode"></a><span data-ttu-id="332d4-114">Részleges konfigurációk leküldési módban</span><span class="sxs-lookup"><span data-stu-id="332d4-114">Partial configurations in push mode</span></span>

<span data-ttu-id="332d4-115">Részleges konfigurációk használata a leküldési módban, konfigurálhatók az LCM Konfigurálása a célcsomópont a részleges konfigurációk fogadásához.</span><span class="sxs-lookup"><span data-stu-id="332d4-115">To use partial configurations in push mode, you configure the LCM on the target node to receive the partial configurations.</span></span> <span data-ttu-id="332d4-116">Minden egyes részleges konfiguráció a cél használatával lehet leküldeni a `Publish-DSCConfiguration` parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="332d4-116">Each partial configuration must be pushed to the target by using the `Publish-DSCConfiguration` cmdlet.</span></span> <span data-ttu-id="332d4-117">A célcsomópont majd egyesíti a részleges egyetlen konfigurációval-konfigurációnak, és alkalmazhatja a konfiguráció meghívásával a [Start-DscConfiguration](/powershell/module/psdesiredstateconfiguration/start-dscconfiguration) parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="332d4-117">The target node then combines the partial configuration into a single configuration, and you can apply the configuration by calling the [Start-DscConfiguration](/powershell/module/psdesiredstateconfiguration/start-dscconfiguration) cmdlet.</span></span>

### <a name="configuring-the-lcm-for-push-mode-partial-configurations"></a><span data-ttu-id="332d4-118">Az LCM konfigurálása a leküldéses módú részleges konfigurációk</span><span class="sxs-lookup"><span data-stu-id="332d4-118">Configuring the LCM for push-mode partial configurations</span></span>

<span data-ttu-id="332d4-119">Részleges konfigurációk esetén az LCM konfigurálása a leküldési módban, hozzon létre egy **DSCLocalConfigurationManager** egy konfigurációs **PartialConfiguration** az egyes részleges konfigurációk letiltása.</span><span class="sxs-lookup"><span data-stu-id="332d4-119">To configure the LCM for partial configurations in push mode, you create a **DSCLocalConfigurationManager** configuration with one **PartialConfiguration** block for each partial configuration.</span></span> <span data-ttu-id="332d4-120">Az LCM konfigurálása kapcsolatos további információkért lásd: [a Local Configuration Manager Windows](/powershell/dsc/metaConfig).</span><span class="sxs-lookup"><span data-stu-id="332d4-120">For more information about configuring the LCM, see [Windows Configuring the Local Configuration Manager](/powershell/dsc/metaConfig).</span></span> <span data-ttu-id="332d4-121">Az alábbi példa bemutatja egy LCM konfigurációt, amely a két részleges konfigurációk vár –, amely telepíti az operációs rendszer, a másikat, amely telepíti és konfigurálja a SharePoint.</span><span class="sxs-lookup"><span data-stu-id="332d4-121">The following example shows an LCM configuration that expects two partial configurations—one that deploys the OS, and one that deploys and configures SharePoint.</span></span>

```powershell
[DSCLocalConfigurationManager()]
configuration PartialConfigDemo
{
    Node localhost
    {

        PartialConfiguration ServiceAccountConfig
        {
            Description = 'Configuration to add the SharePoint service account to the Administrators group.'
            RefreshMode = 'Push'
        }
           PartialConfiguration SharePointConfig
        {
            Description = 'Configuration for the SharePoint server'
            RefreshMode = 'Push'
        }
    }
}

PartialConfigDemo
```

<span data-ttu-id="332d4-122">A **RefreshMode** esetében minden egyes részleges konfiguráció "Leküldéses" értékre van állítva.</span><span class="sxs-lookup"><span data-stu-id="332d4-122">The **RefreshMode** for each partial configuration is set to "Push".</span></span> <span data-ttu-id="332d4-123">Nevei a **PartialConfiguration** blokkok (ebben az esetben az "ServiceAccountConfig" és "SharePointConfig") a konfigurációk, amelyek akkor lesznek leküldve a célcsomópont a nevei pontosan egyeznie kell.</span><span class="sxs-lookup"><span data-stu-id="332d4-123">The names of the **PartialConfiguration** blocks (in this case, "ServiceAccountConfig" and "SharePointConfig") must match exactly the names of the configurations that are pushed to the target node.</span></span>

> [!Note]
> <span data-ttu-id="332d4-124">A megnevezett egyes **PartialConfiguration** blokk meg kell egyeznie a tényleges konfiguráció neve szerint van megadva a konfigurációs parancsfájl, nem a MOF-fájlt, amely lehet a cél csomópont nevét, és neve`localhost`.</span><span class="sxs-lookup"><span data-stu-id="332d4-124">The named of each **PartialConfiguration** block must match the actual name of the configuration as it is specified in the configuration script, not the name of the MOF file, which should be either the name of the target node or `localhost`.</span></span>

### <a name="publishing-and-starting-push-mode-partial-configurations"></a><span data-ttu-id="332d4-125">Közzététel és Leküldéses módú részleges konfigurációk indítása</span><span class="sxs-lookup"><span data-stu-id="332d4-125">Publishing and starting push-mode partial configurations</span></span>

<span data-ttu-id="332d4-126">Majd hívja [Publish-DSCConfiguration](/powershell/module/PSDesiredStateConfiguration/Publish-DscConfiguration) átadja a mappákat, amelyek az egyes konfigurációkhoz konfigurációs dokumentumok tartalmazzák a **elérési út** paramétereket.</span><span class="sxs-lookup"><span data-stu-id="332d4-126">You then call [Publish-DSCConfiguration](/powershell/module/PSDesiredStateConfiguration/Publish-DscConfiguration) for each configuration, passing the folders that contain the configuration documents as the **Path** parameters.</span></span> <span data-ttu-id="332d4-127">`Publish-DSCConfiguration`a konfigurációs MOF-fájlok a célcsomópontokat helyezi.</span><span class="sxs-lookup"><span data-stu-id="332d4-127">`Publish-DSCConfiguration`places the configuration MOF files to the target nodes.</span></span> <span data-ttu-id="332d4-128">Miután közzétette mindkét, meghívhatja `Start-DSCConfiguration –UseExisting` célcsomóponton.</span><span class="sxs-lookup"><span data-stu-id="332d4-128">After publishing both configurations, you can call `Start-DSCConfiguration –UseExisting` on the target node.</span></span>

<span data-ttu-id="332d4-129">Például ha rendelkezik a következő konfigurációs MOF dokumentumok a szerzői műveletekhez részben csomóponton:</span><span class="sxs-lookup"><span data-stu-id="332d4-129">For example, if you have compiled the following configuration MOF documents on the authoring node:</span></span>

```powershell
Get-ChildItem -Recurse
```

```output
    Directory: C:\PartialConfigTest

Mode                LastWriteTime         Length Name
----                -------------         ------ ----
d-----        8/11/2016   1:55 PM                ServiceAccountConfig
d-----       11/17/2016   4:14 PM                SharePointConfig

    Directory: C:\PartialConfigTest\ServiceAccountConfig

Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----        8/11/2016   2:02 PM           2034 TestVM.mof

    Directory: C:\DscTests\SharePointConfig

Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----       11/17/2016   4:14 PM           1930 TestVM.mof
```

<span data-ttu-id="332d4-130">Közzé kívánja, majd futtassa a konfiguráció az alábbiak szerint:</span><span class="sxs-lookup"><span data-stu-id="332d4-130">You would publish and run the configurations as follows:</span></span>

```powershell
Publish-DscConfiguration .\ServiceAccountConfig -ComputerName 'TestVM'
Publish-DscConfiguration .\SharePointConfig -ComputerName 'TestVM'
Start-DscConfiguration -UseExisting -ComputerName 'TestVM'
```

```output
Id     Name            PSJobTypeName   State         HasMoreData     Location             Command
--     ----            -------------   -----         -----------     --------             -------
17     Job17           Configuratio... Running       True            TestVM            Start-DscConfiguration...
```

> [!Note]
> <span data-ttu-id="332d4-131">A futtató felhasználó az [Publish-DSCConfiguration](/powershell/module/PSDesiredStateConfiguration/Publish-DscConfiguration) parancsmagot rendszergazdai jogosultsággal kell rendelkeznie a célként megadott csomóponton.</span><span class="sxs-lookup"><span data-stu-id="332d4-131">The user running the [Publish-DSCConfiguration](/powershell/module/PSDesiredStateConfiguration/Publish-DscConfiguration) cmdlet must have administrator privileges on the target node.</span></span>

## <a name="partial-configurations-in-pull-mode"></a><span data-ttu-id="332d4-132">Részleges konfigurációk lekéréses módban</span><span class="sxs-lookup"><span data-stu-id="332d4-132">Partial configurations in pull mode</span></span>

<span data-ttu-id="332d4-133">Részleges konfigurációk is le kell kérnie, egy vagy több lekéréses kiszolgálót a (pull-kiszolgálókkal kapcsolatos további információkért lásd: [Windows PowerShell Desired State Configuration lekéréses kiszolgálók](pullServer.md).</span><span class="sxs-lookup"><span data-stu-id="332d4-133">Partial configurations can be pulled from one or more pull servers (for more information about pull servers, see [Windows PowerShell Desired State Configuration Pull Servers](pullServer.md).</span></span> <span data-ttu-id="332d4-134">Ehhez az szükséges, akkor az LCM konfigurálása a részleges konfigurációk, lekéréses és nevet, és megfelelően keresse meg a konfiguráció a dokumentumokat a lekéréses kiszolgálójára célcsomóponton.</span><span class="sxs-lookup"><span data-stu-id="332d4-134">To do this, you have to configure the LCM on the target node to pull the partial configurations, and name and locate the configuration documents properly on the pull servers.</span></span>

### <a name="configuring-the-lcm-for-pull-node-configurations"></a><span data-ttu-id="332d4-135">Az LCM konfigurálása a pull-csomópont-konfigurációk</span><span class="sxs-lookup"><span data-stu-id="332d4-135">Configuring the LCM for pull node configurations</span></span>

<span data-ttu-id="332d4-136">Részleges konfigurációk lekéréses kiszolgálóról lekérni az LCM konfigurálása, határozhat meg a lekéréses kiszolgálón vagy egy **ConfigurationRepositoryWeb** (a HTTP-lekéréses kiszolgálón) vagy **ConfigurationRepositoryShare** () az egy SMB-lekérési kiszolgálójának) letiltása.</span><span class="sxs-lookup"><span data-stu-id="332d4-136">To configure the LCM to pull partial configurations from a pull server, you define the pull server in either a **ConfigurationRepositoryWeb** (for an HTTP pull server) or **ConfigurationRepositoryShare** (for an SMB pull server) block.</span></span> <span data-ttu-id="332d4-137">Ezután létre fog hozni **PartialConfiguration** hivatkozni, a lekéréses kiszolgálón használatával blokkolja a **ConfigurationSource** tulajdonság.</span><span class="sxs-lookup"><span data-stu-id="332d4-137">You then create **PartialConfiguration** blocks that refer to the pull server by using the **ConfigurationSource** property.</span></span> <span data-ttu-id="332d4-138">Is szeretne létrehozni egy **beállítások** letiltása, hogy az LCM lekéréses módban használja-e, és adja meg a **ConfigurationNames** vagy **ConfigurationID** , amely a lekéréses kiszolgálón és a cél csomópont használata a felismerésében.</span><span class="sxs-lookup"><span data-stu-id="332d4-138">You also need to create a **Settings** block to specify that the LCM uses pull mode, and to specify the **ConfigurationNames** or **ConfigurationID** that the pull server and target node use to identify the configurations.</span></span> <span data-ttu-id="332d4-139">A következő meta-konfiguráció a CONTOSO-PullSrv nevű HTTP-lekéréses kiszolgálón határozza meg, és két részleges konfigurációk, amelyek használják, amely a lekérési kiszolgálón.</span><span class="sxs-lookup"><span data-stu-id="332d4-139">The following meta-configuration defines an HTTP pull server named CONTOSO-PullSrv and two partial configurations that use that pull server.</span></span>

<span data-ttu-id="332d4-140">Az LCM használatával konfigurálásával kapcsolatos további információkat a **ConfigurationNames**, lásd: [konfigurációs nevek lekérési ügyfél beállítása](pullClientConfigNames.md).</span><span class="sxs-lookup"><span data-stu-id="332d4-140">For more information about configuring the LCM using **ConfigurationNames**, see [Setting up a pull client using configuration names](pullClientConfigNames.md).</span></span> <span data-ttu-id="332d4-141">Az LCM használatával konfigurálásával kapcsolatos információkat **ConfigurationID**, lásd: [konfigurációs azonosítóval lekérési ügyfél beállítása](pullClientConfigID.md).</span><span class="sxs-lookup"><span data-stu-id="332d4-141">For information about configuring the LCM using **ConfigurationID**, see [Setting up a pull client using configuration ID](pullClientConfigID.md).</span></span>

#### <a name="configuring-the-lcm-for-pull-mode-configurations-using-configuration-names"></a><span data-ttu-id="332d4-142">Az LCM konfigurálása a lekérési mód konfigurációk konfigurációs nevekkel</span><span class="sxs-lookup"><span data-stu-id="332d4-142">Configuring the LCM for pull mode configurations using configuration names</span></span>

```powershell
[DscLocalConfigurationManager()]
Configuration PartialConfigDemoConfigNames
{
        Settings
        {
            RefreshFrequencyMins            = 30;
            RefreshMode                     = "PULL";
            ConfigurationMode               ="ApplyAndAutocorrect";
            AllowModuleOverwrite            = $true;
            RebootNodeIfNeeded              = $true;
            ConfigurationModeFrequencyMins  = 60;
        }
        ConfigurationRepositoryWeb CONTOSO-PullSrv
        {
            ServerURL                       = 'https://CONTOSO-PullSrv:8080/PSDSCPullServer.svc'
            RegistrationKey                 = 5b41f4e6-5e6d-45f5-8102-f2227468ef38
            ConfigurationNames              = @("ServiceAccountConfig", "SharePointConfig")
        }

        PartialConfiguration ServiceAccountConfig
        {
            Description                     = "ServiceAccountConfig"
            ConfigurationSource             = @("[ConfigurationRepositoryWeb]CONTOSO-PullSrv")
        }

        PartialConfiguration SharePointConfig
        {
            Description                     = "SharePointConfig"
            ConfigurationSource             = @("[ConfigurationRepositoryWeb]CONTOSO-PullSrv")
            DependsOn                       = '[PartialConfiguration]ServiceAccountConfig'
        }
}
```

#### <a name="configuring-the-lcm-for-pull-mode-configurations-using-configurationid"></a><span data-ttu-id="332d4-143">Az LCM konfigurálása a lekérési mód konfigurációk ConfigurationID használatával</span><span class="sxs-lookup"><span data-stu-id="332d4-143">Configuring the LCM for pull mode configurations using ConfigurationID</span></span>

```powershell
[DSCLocalConfigurationManager()]
configuration PartialConfigDemoConfigID
{
    Node localhost
    {
        Settings
        {
            RefreshMode                     = 'Pull'
            ConfigurationID                 = '1d545e3b-60c3-47a0-bf65-5afc05182fd0'
            RefreshFrequencyMins            = 30
            RebootNodeIfNeeded              = $true
        }
        ConfigurationRepositoryWeb CONTOSO-PullSrv
        {
            ServerURL                       = 'https://CONTOSO-PullSrv:8080/PSDSCPullServer.svc'

        }

           PartialConfiguration ServiceAccountConfig
        {
            Description                     = 'Configuration for the Base OS'
            ConfigurationSource             = '[ConfigurationRepositoryWeb]CONTOSO-PullSrv'
            RefreshMode                     = 'Pull'
        }
           PartialConfiguration SharePointConfig
        {
            Description                     = 'Configuration for the Sharepoint Server'
            ConfigurationSource             = '[ConfigurationRepositoryWeb]CONTOSO-PullSrv'
            DependsOn                       = '[PartialConfiguration]ServiceAccountConfig'
            RefreshMode                     = 'Pull'
        }
    }
}
PartialConfigDemo
```

<span data-ttu-id="332d4-144">Részleges konfigurációk egynél több lekéréses kiszolgálóról kérheti le – ugyanúgy kell minden lekéréses kiszolgálón határozza meg, és ezután tekintse meg a megfelelő lekérési kiszolgálóval **PartialConfiguration** letiltása.</span><span class="sxs-lookup"><span data-stu-id="332d4-144">You can pull partial configurations from more than one pull server—you would just need to define each pull server, and then refer to the appropriate pull server in each **PartialConfiguration** block.</span></span>

<span data-ttu-id="332d4-145">Miután létrehozta a metaadat-konfiguráció, futtatnia kell, hogy hozzon létre egy konfigurációs dokumentumot (MOF-fájlt), és ezután hívja meg [Set-DscLocalConfigurationManager](/powershell/module/PSDesiredStateConfiguration/Set-DscLocalConfigurationManager) az LCM konfigurálása.</span><span class="sxs-lookup"><span data-stu-id="332d4-145">After creating the meta-configuration, you must run it to create a configuration document (a MOF file), and then call [Set-DscLocalConfigurationManager](/powershell/module/PSDesiredStateConfiguration/Set-DscLocalConfigurationManager) to configure the LCM.</span></span>

### <a name="naming-and-placing-the-configuration-documents-on-the-pull-server-configurationnames"></a><span data-ttu-id="332d4-146">Kiosztási és a konfigurációs dokumentum elhelyezése a lekérési kiszolgálón (ConfigurationNames)</span><span class="sxs-lookup"><span data-stu-id="332d4-146">Naming and placing the configuration documents on the pull server (ConfigurationNames)</span></span>

<span data-ttu-id="332d4-147">A részleges konfigurációs dokumentumokat megadott mappába kell helyezni a **ConfigurationPath** a a `web.config` a lekéréses kiszolgálón fájlt (általában `C:\Program
Files\WindowsPowerShell\DscService\Configuration`).</span><span class="sxs-lookup"><span data-stu-id="332d4-147">The partial configuration documents must be placed in the folder specified as the **ConfigurationPath** in the `web.config` file for the pull server (typically `C:\Program
Files\WindowsPowerShell\DscService\Configuration`).</span></span>

#### <a name="naming-configuration-documents-on-the-pull-server-in-powershell-51"></a><span data-ttu-id="332d4-148">A lekérési kiszolgálón a PowerShell 5.1 elnevezési konfigurációs dokumentumok</span><span class="sxs-lookup"><span data-stu-id="332d4-148">Naming configuration documents on the pull server in PowerShell 5.1</span></span>

<span data-ttu-id="332d4-149">Egy különálló lekéréses kiszolgálóról csak egy részleges konfigurációs van lehetőség, ha a konfigurációs dokumentum rendelkezhet egy tetszőleges nevet.</span><span class="sxs-lookup"><span data-stu-id="332d4-149">If you are pulling only one partial configuration from an individual pull server, the configuration document can have any name.</span></span> <span data-ttu-id="332d4-150">Egy lekéréses kiszolgálóról egynél több részleges konfigurációs van lehetőség, ha a konfigurációs dokumentum elnevezheti vagy `<ConfigurationName>.mof`, ahol *ConfigurationName* a részleges konfiguráció neve vagy `<ConfigurationName>.<NodeName>.mof`, ahol *ConfigurationName* a részleges konfiguráció neve és *csomópontnév* a célcsomópont neve.</span><span class="sxs-lookup"><span data-stu-id="332d4-150">If you are pulling more than one partial configuration from a pull server, the configuration document can be named either `<ConfigurationName>.mof`, where *ConfigurationName* is the name of the partial configuration, or `<ConfigurationName>.<NodeName>.mof`, where *ConfigurationName* is the name of the partial configuration, and *NodeName* is the name of the target node.</span></span> <span data-ttu-id="332d4-151">Ez lehetővé teszi a pull-konfigurációk az Azure Automation DSC lekérési kiszolgálóról.</span><span class="sxs-lookup"><span data-stu-id="332d4-151">This allows you to pull configurations from Azure Automation DSC pull server.</span></span>

#### <a name="naming-configuration-documents-on-the-pull-server-in-powershell-50"></a><span data-ttu-id="332d4-152">A lekérési kiszolgálón a PowerShell 5.0 elnevezési konfigurációs dokumentumok</span><span class="sxs-lookup"><span data-stu-id="332d4-152">Naming configuration documents on the pull server in PowerShell 5.0</span></span>

<span data-ttu-id="332d4-153">A konfigurációs dokumentum a következő névvel kell rendelkeznie: `ConfigurationName.mof`, ahol *ConfigurationName* a részleges konfiguráció neve.</span><span class="sxs-lookup"><span data-stu-id="332d4-153">The configuration documents must be named as follows: `ConfigurationName.mof`, where *ConfigurationName* is the name of the partial configuration.</span></span> <span data-ttu-id="332d4-154">A példánkban a konfigurációs dokumentumokat kell elnevezése a következő:</span><span class="sxs-lookup"><span data-stu-id="332d4-154">For our example, the configuration documents should be named as follows:</span></span>

```
ServiceAccountConfig.mof
ServiceAccountConfig.mof.checksum
SharePointConfig.mof
SharePointConfig.mof.checksum
```

### <a name="naming-and-placing-the-configuration-documents-on-the-pull-server-configurationid"></a><span data-ttu-id="332d4-155">Kiosztási és a konfigurációs dokumentum elhelyezése a lekérési kiszolgálón (ConfigurationID)</span><span class="sxs-lookup"><span data-stu-id="332d4-155">Naming and placing the configuration documents on the pull server (ConfigurationID)</span></span>

<span data-ttu-id="332d4-156">A részleges konfigurációs dokumentumokat megadott mappába kell helyezni a **ConfigurationPath** a a `web.config` a lekéréses kiszolgálón fájlt (általában `C:\Program Files\WindowsPowerShell\DscService\Configuration`).</span><span class="sxs-lookup"><span data-stu-id="332d4-156">The partial configuration documents must be placed in the folder specified as the **ConfigurationPath** in the `web.config` file for the pull server (typically `C:\Program Files\WindowsPowerShell\DscService\Configuration`).</span></span> <span data-ttu-id="332d4-157">A konfigurációs dokumentum a következő névvel kell rendelkeznie: `<ConfigurationName>.<ConfigurationID>.mof`, ahol _ConfigurationName_ a részleges konfiguráció neve és _ConfigurationID_ a konfiguráció azonosítója definiálva van a Az LCM célcsomóponton.</span><span class="sxs-lookup"><span data-stu-id="332d4-157">The configuration documents must be named as follows: `<ConfigurationName>.<ConfigurationID>.mof`, where _ConfigurationName_ is the name of the partial configuration and _ConfigurationID_ is the configuration ID defined in the LCM on the target node.</span></span> <span data-ttu-id="332d4-158">A példánkban a konfigurációs dokumentumokat kell elnevezése a következő:</span><span class="sxs-lookup"><span data-stu-id="332d4-158">For our example, the configuration documents should be named as follows:</span></span>

```
ServiceAccountConfig.1d545e3b-60c3-47a0-bf65-5afc05182fd0.mof
ServiceAccountConfig.1d545e3b-60c3-47a0-bf65-5afc05182fd0.mof.checksum
SharePointConfig.1d545e3b-60c3-47a0-bf65-5afc05182fd0.mof
SharePointConfig.1d545e3b-60c3-47a0-bf65-5afc05182fd0.mof.checksum
```

### <a name="running-partial-configurations-from-a-pull-server"></a><span data-ttu-id="332d4-159">Részleges konfigurációk futtatása egy lekéréses kiszolgálóról</span><span class="sxs-lookup"><span data-stu-id="332d4-159">Running partial configurations from a pull server</span></span>

<span data-ttu-id="332d4-160">Miután az LCM Konfigurálása a célként megadott csomóponton lett konfigurálva, és a konfigurációs dokumentumot létrehozott és a lekérési kiszolgálón megfelelően nevű, a célcsomópont a részleges konfigurációk kéri, kombinálhatja őket, és a alkalmazni az így létrejövő konfiguráció rendszeres által megadott időközönként a **RefreshFrequencyMins** az LCM tulajdonságát.</span><span class="sxs-lookup"><span data-stu-id="332d4-160">After the LCM on the target node has been configured, and the configuration documents have been created and properly named on the pull server, the target node will pull the partial configurations, combine them, and apply the resulting configuration at regular intervals as specified by the **RefreshFrequencyMins** property of the LCM.</span></span> <span data-ttu-id="332d4-161">Ha azt szeretné, frissítésének kényszerítése, meghívhatja a [Update-DscConfiguration](/powershell/module/PSDesiredStateConfiguration/Update-DscConfiguration) lekérni a konfigurációkat, a parancsmag, majd `Start-DSCConfiguration –UseExisting` a alkalmazni őket.</span><span class="sxs-lookup"><span data-stu-id="332d4-161">If you want to force a refresh, you can call the [Update-DscConfiguration](/powershell/module/PSDesiredStateConfiguration/Update-DscConfiguration) cmdlet, to pull the configurations, and then `Start-DSCConfiguration –UseExisting` to apply them.</span></span>

## <a name="partial-configurations-in-mixed-push-and-pull-modes"></a><span data-ttu-id="332d4-162">A vegyes eseménylekérési részleges konfigurációk</span><span class="sxs-lookup"><span data-stu-id="332d4-162">Partial configurations in mixed push and pull modes</span></span>

<span data-ttu-id="332d4-163">Is kombinálhatók leküldéses és lekéréses részleges konfigurációk módban.</span><span class="sxs-lookup"><span data-stu-id="332d4-163">You can also mix push and pull modes for partial configurations.</span></span> <span data-ttu-id="332d4-164">Lehet, hogy egy részleges konfigurációval, amely lekéréses kiszolgálóról, miközben egy másik részleges konfigurációs leküldéssel kéri le.</span><span class="sxs-lookup"><span data-stu-id="332d4-164">That is, you could have one partial configuration that is pulled from a pull server, while another partial configuration is pushed.</span></span> <span data-ttu-id="332d4-165">Adja meg az egyes részleges konfigurációs frissítési módot, a korábbi szakaszokban ismertetett módon.</span><span class="sxs-lookup"><span data-stu-id="332d4-165">Specify the refresh mode for each partial configuration as described in the previous sections.</span></span> <span data-ttu-id="332d4-166">Például a következő meta-konfiguráció ismerteti az ugyanebben a példában a `ServiceAccountConfig` részleges konfigurációs lekéréses módban, és a `SharePointConfig` részleges konfigurációs leküldési módban.</span><span class="sxs-lookup"><span data-stu-id="332d4-166">For example, the following meta-configuration describes the same example, with the `ServiceAccountConfig` partial configuration in pull mode and the `SharePointConfig` partial configuration in push mode.</span></span>

### <a name="mixed-push-and-pull-modes-using-configurationnames"></a><span data-ttu-id="332d4-167">Vegyes eseménylekérési ConfigurationNames használatával</span><span class="sxs-lookup"><span data-stu-id="332d4-167">Mixed push and pull modes using ConfigurationNames</span></span>

```powershell
[DscLocalConfigurationManager()]
Configuration PartialConfigDemoConfigNames
{
        Settings
        {
            RefreshFrequencyMins            = 30;
            RefreshMode                     = "PULL";
            ConfigurationMode               = "ApplyAndAutocorrect";
            AllowModuleOverwrite            = $true;
            RebootNodeIfNeeded              = $true;
            ConfigurationModeFrequencyMins  = 60;
        }
        ConfigurationRepositoryWeb CONTOSO-PullSrv
        {
            ServerURL                       = 'https://CONTOSO-PullSrv:8080/PSDSCPullServer.svc'
            RegistrationKey                 = 5b41f4e6-5e6d-45f5-8102-f2227468ef38
            ConfigurationNames              = @("ServiceAccountConfig", "SharePointConfig")
        }

        PartialConfiguration ServiceAccountConfig
        {
            Description                     = "ServiceAccountConfig"
            ConfigurationSource             = @("[ConfigurationRepositoryWeb]CONTOSO-PullSrv")
            RefreshMode                     = 'Pull'
        }

        PartialConfiguration SharePointConfig
        {
            Description                     = "SharePointConfig"
            DependsOn                       = '[PartialConfiguration]ServiceAccountConfig'
            RefreshMode                     = 'Push'
        }

}
```

### <a name="mixed-push-and-pull-modes-using-configurationid"></a><span data-ttu-id="332d4-168">Vegyes eseménylekérési ConfigurationID használatával</span><span class="sxs-lookup"><span data-stu-id="332d4-168">Mixed push and pull modes using ConfigurationID</span></span>

```powershell
[DSCLocalConfigurationManager()]
configuration PartialConfigDemo
{
    Node localhost
    {
        Settings
        {
            RefreshMode             = 'Pull'
            ConfigurationID         = '1d545e3b-60c3-47a0-bf65-5afc05182fd0'
            RefreshFrequencyMins    = 30
            RebootNodeIfNeeded      = $true
        }
        ConfigurationRepositoryWeb CONTOSO-PullSrv
        {
            ServerURL               = 'https://CONTOSO-PullSrv:8080/PSDSCPullServer.svc'

        }

           PartialConfiguration ServiceAccountConfig
        {
            Description             = 'Configuration for the Base OS'
            ConfigurationSource     = '[ConfigurationRepositoryWeb]CONTOSO-PullSrv'
            RefreshMode             = 'Pull'
        }
           PartialConfiguration SharePointConfig
        {
            Description             = 'Configuration for the Sharepoint Server'
            DependsOn               = '[PartialConfiguration]ServiceAccountConfig'
            RefreshMode             = 'Push'
        }
    }
}
PartialConfigDemo
```

<span data-ttu-id="332d4-169">Vegye figyelembe, hogy a **RefreshMode** "Lekérés" található a megadott van, de a **RefreshMode** számára a `SharePointConfig` részleges konfigurációs "Push".</span><span class="sxs-lookup"><span data-stu-id="332d4-169">Note that the **RefreshMode** specified in the Settings block is "Pull", but the **RefreshMode** for the `SharePointConfig` partial configuration is "Push".</span></span>

<span data-ttu-id="332d4-170">Nevezze el, és keresse meg a konfigurációs MOF-fájlok, a megfelelő frissítési módok esetében fentebb leírtakhoz hasonlóan.</span><span class="sxs-lookup"><span data-stu-id="332d4-170">Name and locate the configuration MOF files as described above for their respective refresh modes.</span></span>
<span data-ttu-id="332d4-171">Hívás `Publish-DSCConfiguration` közzététele a `SharePointConfig` részleges konfigurációs, és vagy várjon, amíg a `ServiceAccountConfig` konfiguráció le kell kérnie a a lekéréses kiszolgálón, vagy frissítésének kényszerítése meghívásával [Update-DscConfiguration](/powershell/module/PSDesiredStateConfiguration/Update-DscConfiguration).</span><span class="sxs-lookup"><span data-stu-id="332d4-171">Call `Publish-DSCConfiguration` to publish the `SharePointConfig` partial configuration, and either wait for the `ServiceAccountConfig` configuration to be pulled from the pull server, or force a refresh by calling [Update-DscConfiguration](/powershell/module/PSDesiredStateConfiguration/Update-DscConfiguration).</span></span>

## <a name="example-serviceaccountconfig-partial-configuration"></a><span data-ttu-id="332d4-172">Példa ServiceAccountConfig részleges konfiguráció</span><span class="sxs-lookup"><span data-stu-id="332d4-172">Example ServiceAccountConfig Partial Configuration</span></span>

```powershell
Configuration ServiceAccountConfig
{
    Param (
        [Parameter(Mandatory,
                   HelpMessage="Domain credentials required to add domain\sharepoint_svc to the local Administrators group.")]
        [ValidateNotNullOrEmpty()]
        [pscredential]$Credential
    )

    Import-DscResource -ModuleName PSDesiredStateConfiguration

    Node localhost
    {
        Group LocalAdmins
        {
            GroupName           = 'Administrators'
            MembersToInclude    = 'domain\sharepoint_svc',
                                  'admins@example.domain'
            Ensure              = 'Present'
            Credential          = $Credential
        }

        WindowsFeature Telnet
        {
            Name                = 'Telnet-Server'
            Ensure              = 'Absent'
        }
    }
}
ServiceAccountConfig
```

## <a name="example-sharepointconfig-partial-configuration"></a><span data-ttu-id="332d4-173">Példa SharePointConfig részleges konfiguráció</span><span class="sxs-lookup"><span data-stu-id="332d4-173">Example SharePointConfig Partial Configuration</span></span>

```powershell
Configuration SharePointConfig
{
    Param (
        [Parameter(Mandatory)]
        [ValidateNotNullOrEmpty()]
        [pscredential]$ProductKey
    )

    Import-DscResource -ModuleName xSharePoint

    Node localhost
    {
        xSPInstall SharePointDefault
        {
            Ensure      = 'Present'
            BinaryDir   = '\\FileServer\Installers\Sharepoint\'
            ProductKey  = $ProductKey
        }
    }
}
SharePointConfig
```

## <a name="see-also"></a><span data-ttu-id="332d4-174">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="332d4-174">See Also</span></span>

[<span data-ttu-id="332d4-175">Windows PowerShell Desired State Configuration lekéréses kiszolgálók</span><span class="sxs-lookup"><span data-stu-id="332d4-175">Windows PowerShell Desired State Configuration Pull Servers</span></span>](pullServer.md)

[<span data-ttu-id="332d4-176">A helyi Configuration Manager Windows</span><span class="sxs-lookup"><span data-stu-id="332d4-176">Windows Configuring the Local Configuration Manager</span></span>](../managing-nodes/metaConfig.md)