---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "PowerShell célállapot-konfiguráció részleges konfigurációk"
ms.openlocfilehash: 4401ea80cffd09f4b92c9fcca16d5dcad7f6a327
ms.sourcegitcommit: 99227f62dcf827354770eb2c3e95c5cf6a3118b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/15/2018
---
# <a name="powershell-desired-state-configuration-partial-configurations"></a><span data-ttu-id="29e0c-103">PowerShell célállapot-konfiguráció részleges konfigurációk</span><span class="sxs-lookup"><span data-stu-id="29e0c-103">PowerShell Desired State Configuration partial configurations</span></span>

><span data-ttu-id="29e0c-104">Vonatkozik: A Windows PowerShell 5.0-s és újabb verziók.</span><span class="sxs-lookup"><span data-stu-id="29e0c-104">Applies To: Windows PowerShell 5.0 and later.</span></span>

<span data-ttu-id="29e0c-105">PowerShell 5.0 használata esetén a kívánt állapot konfigurációs szolgáltatása (DSC) lehetővé teszi, hogy töredékben és a különböző forrásokból származó kézbesítendő konfigurációk.</span><span class="sxs-lookup"><span data-stu-id="29e0c-105">In PowerShell 5.0, Desired State Configuration (DSC) allows configurations to be delivered in fragments and from multiple sources.</span></span> <span data-ttu-id="29e0c-106">A helyi Configuration Manager (LCM) célcsomóponton a töredék mielőtt alkalmazná őket egy egyetlen beállításokkal együtt helyezi.</span><span class="sxs-lookup"><span data-stu-id="29e0c-106">The Local Configuration Manager (LCM) on the target node puts the fragments together before applying them as a single configuration.</span></span> <span data-ttu-id="29e0c-107">Ez a funkció lehetővé teszi, hogy vezérlésének konfigurációs csapatok vagy személyek közötti megosztását.</span><span class="sxs-lookup"><span data-stu-id="29e0c-107">This capability allows sharing control of configuration between teams or individuals.</span></span> <span data-ttu-id="29e0c-108">Például ha két vagy több csoportjai fejlesztők dolgozik, egy szolgáltatás, előfordulhat, hogy minden egyes szeretnék kezelése a saját eszközeiken, a szolgáltatás-konfigurációk létrehozása.</span><span class="sxs-lookup"><span data-stu-id="29e0c-108">For example, if two or more teams of developers are collaborating on a service, they might each want to create configurations to manage their part of the service.</span></span> <span data-ttu-id="29e0c-109">Ezek a konfigurációk mindegyikének sikerült igénylése a különböző lekéréses kiszolgálók, és azok különböző szakaszaiban a fejlesztési lehetett hozzáadni.</span><span class="sxs-lookup"><span data-stu-id="29e0c-109">Each of these configurations could be pulled from different pull servers, and they could be added at different stages of development.</span></span> <span data-ttu-id="29e0c-110">Részleges konfiguráció is engedélyezze a különböző csapatok vagy személyek között különböző jellemzőinek csomópontok konfigurálása anélkül, hogy egyetlen konfigurációs dokumentum szerkesztéséhez koordinálására szabályozására.</span><span class="sxs-lookup"><span data-stu-id="29e0c-110">Partial configurations also allow different individuals or teams to control different aspects of configuring nodes without having to coordinate the editing of a single configuration document.</span></span> <span data-ttu-id="29e0c-111">Például egy csoport előfordulhat, hogy felelős telepítése egy virtuális gép és az operációs rendszer, amíg egy másik csoport központi telepítését egyéb alkalmazások és szolgáltatások a virtuális gépen.</span><span class="sxs-lookup"><span data-stu-id="29e0c-111">For example, one team might be responsible for deploying a VM and operating system, while another team might deploy other applications and services on that VM.</span></span> <span data-ttu-id="29e0c-112">Minden team részleges konfigurációk esetén a saját konfigurációs valamelyiken alatt feleslegesen bonyolítja nélkül hozhat létre.</span><span class="sxs-lookup"><span data-stu-id="29e0c-112">With partial configurations, each team can create its own configuration, without either of them being unnecessarily complicated.</span></span>

<span data-ttu-id="29e0c-113">Részleges konfigurációk leküldéses módot, lekéréses mód vagy a kettő kombinációja használható.</span><span class="sxs-lookup"><span data-stu-id="29e0c-113">You can use partial configurations in push mode, pull mode, or a combination of the two.</span></span>

## <a name="partial-configurations-in-push-mode"></a><span data-ttu-id="29e0c-114">Részleges konfigurációk leküldéses módban</span><span class="sxs-lookup"><span data-stu-id="29e0c-114">Partial configurations in push mode</span></span>
<span data-ttu-id="29e0c-115">Részleges konfigurációk leküldéses üzemmódban használja, konfigurálnia a LCM fogadására a részleges konfiguráció célcsomóponton.</span><span class="sxs-lookup"><span data-stu-id="29e0c-115">To use partial configurations in push mode, you configure the LCM on the target node to receive the partial configurations.</span></span> <span data-ttu-id="29e0c-116">Minden egyes részleges konfiguráció a cél lehet leküldeni a Publish-DSCConfiguration parancsmag használatával.</span><span class="sxs-lookup"><span data-stu-id="29e0c-116">Each partial configuration must be pushed to the target by using the Publish-DSCConfiguration cmdlet.</span></span> <span data-ttu-id="29e0c-117">Célcsomóponton majd egyesíti a részleges konfigurációs adatok egyetlen konfigurációja, és hívja a konfigurációs is alkalmazhat a [Start-DscConfiguration](https://technet.microsoft.com/library/dn521623.aspx) parancsmag.</span><span class="sxs-lookup"><span data-stu-id="29e0c-117">The target node then combines the partial configuration into a single configuration, and you can apply the configuration by calling the [Start-DscConfiguration](https://technet.microsoft.com/library/dn521623.aspx) cmdlet.</span></span>

### <a name="configuring-the-lcm-for-push-mode-partial-configurations"></a><span data-ttu-id="29e0c-118">A leküldéses módú részleges konfigurációk LCM konfigurálása</span><span class="sxs-lookup"><span data-stu-id="29e0c-118">Configuring the LCM for push-mode partial configurations</span></span>
<span data-ttu-id="29e0c-119">Leküldéses módban a LCM részleges konfigurációk beállításához hozzon létre egy **DSCLocalConfigurationManager** egy konfigurációs **PartialConfiguration** minden egyes részleges konfiguráció blokkja.</span><span class="sxs-lookup"><span data-stu-id="29e0c-119">To configure the LCM for partial configurations in push mode, you create a **DSCLocalConfigurationManager** configuration with one **PartialConfiguration** block for each partial configuration.</span></span> <span data-ttu-id="29e0c-120">A LCM konfigurálásával kapcsolatos további információkért lásd: [konfigurálása a helyi Configuration Manager Windows](https://technet.microsoft.com/library/mt421188.aspx).</span><span class="sxs-lookup"><span data-stu-id="29e0c-120">For more information about configuring the LCM, see [Windows Configuring the Local Configuration Manager](https://technet.microsoft.com/library/mt421188.aspx).</span></span> <span data-ttu-id="29e0c-121">A következő példa bemutatja, hogy két részleges konfigurációk vár LCM konfigurálása során – egy, az operációs rendszer központi telepítését végző és egy, amely telepíti és konfigurálja a SharePoint.</span><span class="sxs-lookup"><span data-stu-id="29e0c-121">The following example shows an LCM configuration that expects two partial configurations—one that deploys the OS, and one that deploys and configures SharePoint.</span></span>

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

<span data-ttu-id="29e0c-122">A **RefreshMode** az egyes részleges beállítás "Leküldéses".</span><span class="sxs-lookup"><span data-stu-id="29e0c-122">The **RefreshMode** for each partial configuration is set to "Push".</span></span> <span data-ttu-id="29e0c-123">Neve a **PartialConfiguration** blokkok (ebben az esetben az "ServiceAccountConfig" és "SharePointConfig") meg kell egyeznie a pontosan a célcsomóponton vannak leküldve konfigurációkat nevét.</span><span class="sxs-lookup"><span data-stu-id="29e0c-123">The names of the **PartialConfiguration** blocks (in this case, "ServiceAccountConfig" and "SharePointConfig") must match exactly the names of the configurations that are pushed to the target node.</span></span>

><span data-ttu-id="29e0c-124">**Megjegyzés:** a megnevezett egyes **PartialConfiguration** blokk meg kell egyeznie a tényleges nevét, a konfiguráció a konfigurációs parancsfájl, a MOF-fájl neve nem a megadott kell lennie, amely nevét, illetve a célcsomóponttal vagy `localhost`.</span><span class="sxs-lookup"><span data-stu-id="29e0c-124">**Note:** The named of each **PartialConfiguration** block must match the actual name of the configuration as it is specified in the configuration script, not the name of the MOF file, which should be either the name of the target node or `localhost`.</span></span>

### <a name="publishing-and-starting-push-mode-partial-configurations"></a><span data-ttu-id="29e0c-125">Közzététel, és Leküldéses módú részleges konfigurációk indítása</span><span class="sxs-lookup"><span data-stu-id="29e0c-125">Publishing and starting push-mode partial configurations</span></span>

<span data-ttu-id="29e0c-126">Majd meghívja a [Publish-DSCConfiguration](https://msdn.microsoft.com/powershell/reference/5.1/psdesiredstateconfiguration/publish-dscconfiguration) átadja a mappákat, amely minden konfigurációs konfigurációs dokumentumok tartalmazzák a **elérési** paraméterek.</span><span class="sxs-lookup"><span data-stu-id="29e0c-126">You then call [Publish-DSCConfiguration](https://msdn.microsoft.com/powershell/reference/5.1/psdesiredstateconfiguration/publish-dscconfiguration) for each configuration, passing the folders that contain the configuration documents as the **Path** parameters.</span></span> <span data-ttu-id="29e0c-127">`Publish-DSCConfiguration`a konfigurációs MOF-fájlok sorbaállítása a célcsomópontokat helyezi.</span><span class="sxs-lookup"><span data-stu-id="29e0c-127">`Publish-DSCConfiguration`places the configuration MOF files to the target nodes.</span></span> <span data-ttu-id="29e0c-128">Miután közzétette mindkét konfigurációjában, hívása `Start-DSCConfiguration –UseExisting` célcsomóponton.</span><span class="sxs-lookup"><span data-stu-id="29e0c-128">After publishing both configurations, you can call `Start-DSCConfiguration –UseExisting` on the target node.</span></span>

<span data-ttu-id="29e0c-129">Ha például azzal állítottuk össze a következő konfigurációs MOF dokumentumokat a szerzői műveletekhez csomóponton:</span><span class="sxs-lookup"><span data-stu-id="29e0c-129">For example, if you have compiled the following configuration MOF documents on the authoring node:</span></span>

```powershell
PS C:\PartialConfigTest> Get-ChildItem -Recurse


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

<span data-ttu-id="29e0c-130">Szeretné közzétenni, és futtassa a konfiguráció a következőképpen:</span><span class="sxs-lookup"><span data-stu-id="29e0c-130">You would publish and run the configurations as follows:</span></span>

```powershell
PS C:\PartialConfigTest> Publish-DscConfiguration .\ServiceAccountConfig -ComputerName 'TestVM'
PS C:\PartialConfigTest> Publish-DscConfiguration .\SharePointConfig -ComputerName 'TestVM'
PS C:\PartialConfigTest> Start-DscConfiguration -UseExisting -ComputerName 'TestVM'

Id     Name            PSJobTypeName   State         HasMoreData     Location             Command                  
--     ----            -------------   -----         -----------     --------             -------                  
17     Job17           Configuratio... Running       True            TestVM            Start-DscConfiguration...
```

><span data-ttu-id="29e0c-131">**Megjegyzés:** futtató felhasználó az [Publish-DSCConfiguration](https://msdn.microsoft.com/powershell/reference/5.1/psdesiredstateconfiguration/publish-dscconfiguration) parancsmag a célcsomóponton lévő rendszergazdai jogosultsággal kell rendelkeznie.</span><span class="sxs-lookup"><span data-stu-id="29e0c-131">**Note:** The user running the [Publish-DSCConfiguration](https://msdn.microsoft.com/powershell/reference/5.1/psdesiredstateconfiguration/publish-dscconfiguration) cmdlet must have administrator privileges on the target node.</span></span>

## <a name="partial-configurations-in-pull-mode"></a><span data-ttu-id="29e0c-132">Részleges konfigurációk lekéréses módban</span><span class="sxs-lookup"><span data-stu-id="29e0c-132">Partial configurations in pull mode</span></span>

<span data-ttu-id="29e0c-133">Részleges konfigurációk is lekért egy vagy több lekéréses kiszolgáló (lekéréses-kiszolgálókkal kapcsolatos további információkért lásd: [Windows PowerShell kívánt állapot konfigurációs lekéréses kiszolgálók](pullServer.md).</span><span class="sxs-lookup"><span data-stu-id="29e0c-133">Partial configurations can be pulled from one or more pull servers (for more information about pull servers, see [Windows PowerShell Desired State Configuration Pull Servers](pullServer.md).</span></span> <span data-ttu-id="29e0c-134">Ehhez az szükséges, hogy a LCM konfigurálnia a részleges konfigurációk, lekéréses és nevet, és megfelelően keresse meg a konfigurációs dokumentumokat a lekérési kiszolgálón célcsomóponton.</span><span class="sxs-lookup"><span data-stu-id="29e0c-134">To do this, you have to configure the LCM on the target node to pull the partial configurations, and name and locate the configuration documents properly on the pull servers.</span></span>

### <a name="configuring-the-lcm-for-pull-node-configurations"></a><span data-ttu-id="29e0c-135">A csomópont-konfigurációk lekéréses LCM konfigurálása</span><span class="sxs-lookup"><span data-stu-id="29e0c-135">Configuring the LCM for pull node configurations</span></span>

<span data-ttu-id="29e0c-136">A lekérési kiszolgálójáról részleges konfigurációk le tudja LCM konfigurálásához adhat meg a lekérési kiszolgálójával vagy egy **ConfigurationRepositoryWeb** (a HTTP-lekérési kiszolgálón) vagy **ConfigurationRepositoryShare** () az SMB-lekérési kiszolgálón) blokkot.</span><span class="sxs-lookup"><span data-stu-id="29e0c-136">To configure the LCM to pull partial configurations from a pull server, you define the pull server in either a **ConfigurationRepositoryWeb** (for an HTTP pull server) or **ConfigurationRepositoryShare** (for an SMB pull server) block.</span></span> <span data-ttu-id="29e0c-137">Ezután létrehozhat **PartialConfiguration** mutatnak a lekérési kiszolgálójával használatával tekintse meg a **ConfigurationSource** tulajdonság.</span><span class="sxs-lookup"><span data-stu-id="29e0c-137">You then create **PartialConfiguration** blocks that refer to the pull server by using the **ConfigurationSource** property.</span></span> <span data-ttu-id="29e0c-138">Is szeretne létrehozni egy **beállítások** blokk megadásához, hogy a LCM lekéréses módot használ, és adja meg a **ConfigurationNames** vagy **ConfigurationID** , amely a lekérési kiszolgálójával, és cél csomópont használja a felismerésében.</span><span class="sxs-lookup"><span data-stu-id="29e0c-138">You also need to create a **Settings** block to specify that the LCM uses pull mode, and to specify the **ConfigurationNames** or **ConfigurationID** that the pull server and target node use to identify the configurations.</span></span> <span data-ttu-id="29e0c-139">A következő metaadat-konfiguráció a CONTOSO-PullSrv nevű HTTP-lekérési kiszolgálón határozza meg, és használja, amely két részleges konfigurációkat lekérési kiszolgálón.</span><span class="sxs-lookup"><span data-stu-id="29e0c-139">The following meta-configuration defines an HTTP pull server named CONTOSO-PullSrv and two partial configurations that use that pull server.</span></span>

<span data-ttu-id="29e0c-140">A LCM történő konfigurálásáról további információt a **ConfigurationNames**, lásd: [ügyféltelepítéshez lekéréses konfigurációs nevek használatával](pullClientConfigNames.md).</span><span class="sxs-lookup"><span data-stu-id="29e0c-140">For more information about configuring the LCM using **ConfigurationNames**, see [Setting up a pull client using configuration names](pullClientConfigNames.md).</span></span> <span data-ttu-id="29e0c-141">További információk a LCM történő konfigurálásáról **ConfigurationID**, lásd: [ügyféltelepítéshez lekéréses konfigurációs azonosítójával](pullClientConfigID.md).</span><span class="sxs-lookup"><span data-stu-id="29e0c-141">For information about configuring the LCM using **ConfigurationID**, see [Setting up a pull client using configuration ID](pullClientConfigID.md).</span></span>

#### <a name="configuring-the-lcm-for-pull-mode-configurations-using-configuration-names"></a><span data-ttu-id="29e0c-142">Lekéréses mód konfigurációk konfigurációs nevek használatával LCM konfigurálása</span><span class="sxs-lookup"><span data-stu-id="29e0c-142">Configuring the LCM for pull mode configurations using configuration names</span></span>

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

#### <a name="configuring-the-lcm-for-pull-mode-configurations-using-configurationid"></a><span data-ttu-id="29e0c-143">Lekéréses mód konfigurációk használatával ConfigurationID LCM konfigurálása</span><span class="sxs-lookup"><span data-stu-id="29e0c-143">Configuring the LCM for pull mode configurations using ConfigurationID</span></span>

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

<span data-ttu-id="29e0c-144">Képes lekérni a részleges konfigurációk egynél több lekérési kiszolgálójáról – egyes lekéréses kiszolgálók meghatározása, és majd tekintse át a megfelelő lekérési kiszolgálójával, az egyes ugyanúgy kell **PartialConfiguration** blokkot.</span><span class="sxs-lookup"><span data-stu-id="29e0c-144">You can pull partial configurations from more than one pull server—you would just need to define each pull server, and then refer to the appropriate pull server in each **PartialConfiguration** block.</span></span>

<span data-ttu-id="29e0c-145">Miután létrehozta a metaadat-konfiguráció, futtatnia kell, hogy hozzon létre egy konfigurációs dokumentumot (MOF-fájlt), és majd meghívják a [Set-DscLocalConfigurationManager](https://technet.microsoft.com/en-us/library/dn521621(v=wps.630).aspx) a LCM konfigurálásához.</span><span class="sxs-lookup"><span data-stu-id="29e0c-145">After creating the meta-configuration, you must run it to create a configuration document (a MOF file), and then call [Set-DscLocalConfigurationManager](https://technet.microsoft.com/en-us/library/dn521621(v=wps.630).aspx) to configure the LCM.</span></span>

### <a name="naming-and-placing-the-configuration-documents-on-the-pull-server-configurationnames"></a><span data-ttu-id="29e0c-146">Kiosztási és helyezi el a konfigurációs dokumentumok a lekérési kiszolgálón (ConfigurationNames)</span><span class="sxs-lookup"><span data-stu-id="29e0c-146">Naming and placing the configuration documents on the pull server (ConfigurationNames)</span></span>

<span data-ttu-id="29e0c-147">A megadott mappába kell helyezni a részleges konfigurációs dokumentumok a **ConfigurationPath** a a `web.config` a lekérési kiszolgálójával fájlt (általában `C:\Program Files\WindowsPowerShell\DscService\Configuration`).</span><span class="sxs-lookup"><span data-stu-id="29e0c-147">The partial configuration documents must be placed in the folder specified as the **ConfigurationPath** in the `web.config` file for the pull server (typically `C:\Program Files\WindowsPowerShell\DscService\Configuration`).</span></span> 

#### <a name="naming-configuration-documents-on-the-pull-server-in-powershell-51"></a><span data-ttu-id="29e0c-148">A lekérési kiszolgálón PowerShell 5.1 elnevezési konfigurációs dokumentumok</span><span class="sxs-lookup"><span data-stu-id="29e0c-148">Naming configuration documents on the pull server in PowerShell 5.1</span></span>

<span data-ttu-id="29e0c-149">Ha csak egy részleges konfigurációs lekéréses kiszolgálóról vannak húzza, a konfigurációs dokumentum lehet-e bármely nevük.</span><span class="sxs-lookup"><span data-stu-id="29e0c-149">If you are pulling only one partial configuration from an individual pull server, the configuration document can have any name.</span></span> <span data-ttu-id="29e0c-150">A lekérési kiszolgálójáról egynél több részleges konfigurációs rendszer húzza, ha a konfigurációs dokumentum elnevezheti vagy `<ConfigurationName>.mof`, ahol _ConfigurationName_ a részleges konfiguráció neve vagy `<ConfigurationName>.<NodeName>.mof`, ahol  _ConfigurationName_ a részleges konfiguráció neve és _csomópontnév_ célcsomóponton neve.</span><span class="sxs-lookup"><span data-stu-id="29e0c-150">If you are pulling more than one partial configuration from a pull server, the configuration document can be named either `<ConfigurationName>.mof`, where _ConfigurationName_ is the name of the partial configuration, or `<ConfigurationName>.<NodeName>.mof`, where  _ConfigurationName_ is the name of the partial configuration, and _NodeName_ is the name of the target node.</span></span> <span data-ttu-id="29e0c-151">Ez lehetővé teszi a lekéréses beállításokat Azure Automation DSC lekérési kiszolgálójáról.</span><span class="sxs-lookup"><span data-stu-id="29e0c-151">This allows you to pull configurations from Azure Automation DSC pull server.</span></span>


#### <a name="naming-configuration-documents-on-the-pull-server-in-powershell-50"></a><span data-ttu-id="29e0c-152">A lekérési kiszolgálón PowerShell 5.0-s elnevezési konfigurációs dokumentumok</span><span class="sxs-lookup"><span data-stu-id="29e0c-152">Naming configuration documents on the pull server in PowerShell 5.0</span></span>

<span data-ttu-id="29e0c-153">A konfigurációs dokumentumok kell elnevezése a következő: `ConfigurationName.mof`, ahol _ConfigurationName_ a részleges konfiguráció neve.</span><span class="sxs-lookup"><span data-stu-id="29e0c-153">The configuration documents must be named as follows: `ConfigurationName.mof`, where _ConfigurationName_ is the name of the partial configuration.</span></span> <span data-ttu-id="29e0c-154">A fenti példában a konfigurációs dokumentumok nevet kell adni az alábbiak szerint:</span><span class="sxs-lookup"><span data-stu-id="29e0c-154">For our example, the configuration documents should be named as follows:</span></span>

```
ServiceAccountConfig.mof
ServiceAccountConfig.mof.checksum
SharePointConfig.mof
SharePointConfig.mof.checksum
```

### <a name="naming-and-placing-the-configuration-documents-on-the-pull-server-configurationid"></a><span data-ttu-id="29e0c-155">Kiosztási és helyezi el a konfigurációs dokumentumok a lekérési kiszolgálón (ConfigurationID)</span><span class="sxs-lookup"><span data-stu-id="29e0c-155">Naming and placing the configuration documents on the pull server (ConfigurationID)</span></span>

<span data-ttu-id="29e0c-156">A megadott mappába kell helyezni a részleges konfigurációs dokumentumok a **ConfigurationPath** a a `web.config` a lekérési kiszolgálójával fájlt (általában `C:\Program Files\WindowsPowerShell\DscService\Configuration`).</span><span class="sxs-lookup"><span data-stu-id="29e0c-156">The partial configuration documents must be placed in the folder specified as the **ConfigurationPath** in the `web.config` file for the pull server (typically `C:\Program Files\WindowsPowerShell\DscService\Configuration`).</span></span> <span data-ttu-id="29e0c-157">A konfigurációs dokumentumok kell elnevezése a következő: _ConfigurationName_.</span><span class="sxs-lookup"><span data-stu-id="29e0c-157">The configuration documents must be named as follows: _ConfigurationName_.</span></span> <span data-ttu-id="29e0c-158">_ConfigurationID_`.mof`, ahol _ConfigurationName_ a részleges konfiguráció neve és _ConfigurationID_ a konfiguráció azonosítója definiálva van a célszámítógépen LCM csomópont.</span><span class="sxs-lookup"><span data-stu-id="29e0c-158">_ConfigurationID_`.mof`, where _ConfigurationName_ is the name of the partial configuration and _ConfigurationID_ is the configuration ID defined in the LCM on the target node.</span></span> <span data-ttu-id="29e0c-159">A fenti példában a konfigurációs dokumentumok nevet kell adni az alábbiak szerint:</span><span class="sxs-lookup"><span data-stu-id="29e0c-159">For our example, the configuration documents should be named as follows:</span></span>

```
ServiceAccountConfig.1d545e3b-60c3-47a0-bf65-5afc05182fd0.mof
ServiceAccountConfig.1d545e3b-60c3-47a0-bf65-5afc05182fd0.mof.checksum
SharePointConfig.1d545e3b-60c3-47a0-bf65-5afc05182fd0.mof
SharePointConfig.1d545e3b-60c3-47a0-bf65-5afc05182fd0.mof.checksum
```


### <a name="running-partial-configurations-from-a-pull-server"></a><span data-ttu-id="29e0c-160">A lekérési kiszolgálójáról részleges konfigurációk futtatása</span><span class="sxs-lookup"><span data-stu-id="29e0c-160">Running partial configurations from a pull server</span></span>

<span data-ttu-id="29e0c-161">Miután célcsomóponton LCM van konfigurálva, és a konfigurációs dokumentumot létrehozott és a lekérési kiszolgálón megfelelően nevű, a célcsomóponton fogja lekérni a részleges konfigurációk, ötvözze őket, és rendszeres az eredményként létrejövő konfiguráció alkalmazása által meghatározott időközönként a **RefreshFrequencyMins** a LCM tulajdonsága.</span><span class="sxs-lookup"><span data-stu-id="29e0c-161">After the LCM on the target node has been configured, and the configuration documents have been created and properly named on the pull server, the target node will pull the partial configurations, combine them, and apply the resulting configuration at regular intervals as specified by the **RefreshFrequencyMins** property of the LCM.</span></span> <span data-ttu-id="29e0c-162">Szeretne frissítésének kényszerítése, ha hívása a [frissítés-DscConfiguration](https://technet.microsoft.com/en-us/library/mt143541.aspx) parancsmag való lekérésére a konfigurációk, majd `Start-DSCConfiguration –UseExisting` alkalmazás érdekében.</span><span class="sxs-lookup"><span data-stu-id="29e0c-162">If you want to force a refresh, you can call the [Update-DscConfiguration](https://technet.microsoft.com/en-us/library/mt143541.aspx) cmdlet, to pull the configurations, and then `Start-DSCConfiguration –UseExisting` to apply them.</span></span>


## <a name="partial-configurations-in-mixed-push-and-pull-modes"></a><span data-ttu-id="29e0c-163">A vegyes eseménylekérési és eseményküldési módban részleges konfigurációk</span><span class="sxs-lookup"><span data-stu-id="29e0c-163">Partial configurations in mixed push and pull modes</span></span>

<span data-ttu-id="29e0c-164">Is kombinálhatók leküldéses és lekéréses módok részleges konfigurációk.</span><span class="sxs-lookup"><span data-stu-id="29e0c-164">You can also mix push and pull modes for partial configurations.</span></span> <span data-ttu-id="29e0c-165">Ez azt jelenti, hogy egy részleges konfigurációs lekérési kiszolgálójáról, miközben egy másik részleges konfigurációs fejlesztőre beillesztett lehet.</span><span class="sxs-lookup"><span data-stu-id="29e0c-165">That is, you could have one partial configuration that is pulled from a pull server, while another partial configuration is pushed.</span></span> <span data-ttu-id="29e0c-166">Adja meg a frissítési mód minden részleges konfiguráció, a korábbi szakaszokban ismertetett módon.</span><span class="sxs-lookup"><span data-stu-id="29e0c-166">Specify the refresh mode for each partial configuration as described in the previous sections.</span></span> <span data-ttu-id="29e0c-167">Például a következő metaadat-konfiguráció ismerteti az ugyanebben a példában a `ServiceAccountConfig` lekéréses módban részleges konfigurációs és a `SharePointConfig` részleges konfigurációs leküldéses módban.</span><span class="sxs-lookup"><span data-stu-id="29e0c-167">For example, the following meta-configuration describes the same example, with the `ServiceAccountConfig` partial configuration in pull mode and the `SharePointConfig` partial configuration in push mode.</span></span>

### <a name="mixed-push-and-pull-modes-using-configurationnames"></a><span data-ttu-id="29e0c-168">Vegyes eseménylekérési és eseményküldési módban ConfigurationNames használatával</span><span class="sxs-lookup"><span data-stu-id="29e0c-168">Mixed push and pull modes using ConfigurationNames</span></span>

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

### <a name="mixed-push-and-pull-modes-using-configurationid"></a><span data-ttu-id="29e0c-169">Vegyes eseménylekérési és eseményküldési módban ConfigurationID használatával</span><span class="sxs-lookup"><span data-stu-id="29e0c-169">Mixed push and pull modes using ConfigurationID</span></span>

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

<span data-ttu-id="29e0c-170">Vegye figyelembe, hogy a **RefreshMode** "Pull", a beállítások blokk megadott van, de a **RefreshMode** a a `SharePointConfig` részleges beállítás "Push".</span><span class="sxs-lookup"><span data-stu-id="29e0c-170">Note that the **RefreshMode** specified in the Settings block is "Pull", but the **RefreshMode** for the `SharePointConfig` partial configuration is "Push".</span></span>

<span data-ttu-id="29e0c-171">Név, és keresse meg a konfigurációs MOF-fájlok, a megfelelő frissítési módok a fent leírt módon.</span><span class="sxs-lookup"><span data-stu-id="29e0c-171">Name and locate the configuration MOF files as described above for their respective refresh modes.</span></span> <span data-ttu-id="29e0c-172">Hívás **Publish-DSCConfiguration** közzététele a `SharePointConfig` részleges konfigurációs, és vagy várja meg a `ServiceAccountConfig` konfiguráció kell húzni a lekérési kiszolgálójáról, vagy frissítésének kényszerítése meghívásával [ Frissítés-DscConfiguration](https://technet.microsoft.com/en-us/library/mt143541(v=wps.630).aspx).</span><span class="sxs-lookup"><span data-stu-id="29e0c-172">Call **Publish-DSCConfiguration** to publish the `SharePointConfig` partial configuration, and either wait for the `ServiceAccountConfig` configuration to be pulled from the pull server, or force a refresh by calling [Update-DscConfiguration](https://technet.microsoft.com/en-us/library/mt143541(v=wps.630).aspx).</span></span>

## <a name="example-serviceaccountconfig-partial-configuration"></a><span data-ttu-id="29e0c-173">Példa ServiceAccountConfig részleges konfiguráció</span><span class="sxs-lookup"><span data-stu-id="29e0c-173">Example ServiceAccountConfig Partial Configuration</span></span>

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
## <a name="example-sharepointconfig-partial-configuration"></a><span data-ttu-id="29e0c-174">Példa SharePointConfig részleges konfiguráció</span><span class="sxs-lookup"><span data-stu-id="29e0c-174">Example SharePointConfig Partial Configuration</span></span>
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
##<a name="see-also"></a><span data-ttu-id="29e0c-175">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="29e0c-175">See Also</span></span> 

<span data-ttu-id="29e0c-176">**Fogalmak**
[Windows PowerShell célállapot-konfiguráló lekéréses kiszolgálók](pullServer.md)</span><span class="sxs-lookup"><span data-stu-id="29e0c-176">**Concepts**
[Windows PowerShell Desired State Configuration Pull Servers](pullServer.md)</span></span> 

[<span data-ttu-id="29e0c-177">A Windows a helyi Configuration Manager konfigurálása</span><span class="sxs-lookup"><span data-stu-id="29e0c-177">Windows Configuring the Local Configuration Manager</span></span>](https://technet.microsoft.com/library/mt421188.aspx) 

