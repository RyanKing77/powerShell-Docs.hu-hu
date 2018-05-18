---
ms.date: 06/12/2017
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: Lekérési ügyfél beállítása konfigurációs azonosítóval
ms.openlocfilehash: b4a45c4d014b3c4fc0140ad492f81474b260065a
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/16/2018
---
# <a name="setting-up-a-pull-client-using-configuration-id"></a><span data-ttu-id="20106-103">Lekérési ügyfél beállítása konfigurációs azonosítóval</span><span class="sxs-lookup"><span data-stu-id="20106-103">Setting up a pull client using configuration ID</span></span>

> <span data-ttu-id="20106-104">Vonatkozik: A Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="20106-104">Applies To: Windows PowerShell 5.0</span></span>

> [!IMPORTANT]
> <span data-ttu-id="20106-105">A lekéréses kiszolgáló (Windows-szolgáltatás *DSC-szolgáltatás*), Windows Server támogatott összetevője létezik azonban a következők: nem tervezi, hogy új funkciók és képességek kínálnak.</span><span class="sxs-lookup"><span data-stu-id="20106-105">The Pull Server (Windows Feature *DSC-Service*) is a supported component of Windows Server however there are no plans to offer new features or capabilities.</span></span> <span data-ttu-id="20106-106">Javasoljuk, hogy kezdje a Váltás felügyelt ügyfelek [Azure Automation DSC](/azure/automation/automation-dsc-getting-started) (tartalmazza a Windows Server-kiszolgáló lekéréses is) vagy a közösségi megoldásoknak a valamelyikét felsorolt [Itt](pullserver.md#community-solutions-for-pull-service).</span><span class="sxs-lookup"><span data-stu-id="20106-106">It is recommended to begin transitioning managed clients to [Azure Automation DSC](/azure/automation/automation-dsc-getting-started) (includes features beyond Pull Server on Windows Server) or one of the community solutions listed [here](pullserver.md#community-solutions-for-pull-service).</span></span>

<span data-ttu-id="20106-107">Minden egyes célcsomóponttal lekéréses módban a rendszergazda és az URL-címet kap, ahol lépjen kapcsolatba a lekérési kiszolgálójával konfigurációt beolvasandó ki.</span><span class="sxs-lookup"><span data-stu-id="20106-107">Each target node has to be told to use pull mode and given the URL where it can contact the pull server to get configurations.</span></span> <span data-ttu-id="20106-108">Ehhez az szükséges, hogy a helyi Configuration Manager (LCM) konfigurálnia a szükséges adatokat.</span><span class="sxs-lookup"><span data-stu-id="20106-108">To do this, you have to configure the Local Configuration Manager (LCM) with the necessary information.</span></span> <span data-ttu-id="20106-109">A LCM konfigurálásához hoz létre egy speciális konfigurációs attribútummal. az **DSCLocalConfigurationManager** attribútum.</span><span class="sxs-lookup"><span data-stu-id="20106-109">To configure the LCM, you create a special type of configuration, decorated with the **DSCLocalConfigurationManager** attribute.</span></span> <span data-ttu-id="20106-110">A LCM konfigurálásával kapcsolatos további információkért lásd: [konfigurálása a helyi Configuration Manager](metaConfig.md).</span><span class="sxs-lookup"><span data-stu-id="20106-110">For more information about configuring the LCM, see [Configuring the Local Configuration Manager](metaConfig.md).</span></span>

> <span data-ttu-id="20106-111">**Megjegyzés:**: Ez a témakör PowerShell 5.0 vonatkozik.</span><span class="sxs-lookup"><span data-stu-id="20106-111">**Note**: This topic applies to PowerShell 5.0.</span></span> <span data-ttu-id="20106-112">A PowerShell 4.0 lekéréses ügyfél beállításával kapcsolatos információkért lásd: [konfigurációs azonosítójával PowerShell 4.0 lekéréses ügyfél beállítása](pullClientConfigID4.md)</span><span class="sxs-lookup"><span data-stu-id="20106-112">For information on setting up a pull client in PowerShell 4.0, see [Setting up a pull client using configuration ID in PowerShell 4.0](pullClientConfigID4.md)</span></span>

<span data-ttu-id="20106-113">A következő parancsfájl úgy konfigurálja a LCM lekéréses konfigurációk "CONTOSO-PullSrv" nevű kiszolgálóról.</span><span class="sxs-lookup"><span data-stu-id="20106-113">The following script configures the LCM to pull configurations from a server named "CONTOSO-PullSrv".</span></span>

```powershell
[DSCLocalConfigurationManager()]
configuration PullClientConfigID
{
    Node localhost
    {
        Settings
        {
            RefreshMode = 'Pull'
            ConfigurationID = '1d545e3b-60c3-47a0-bf65-5afc05182fd0'
            RefreshFrequencyMins = 30
            RebootNodeIfNeeded = $true
        }
        ConfigurationRepositoryWeb CONTOSO-PullSrv
        {
            ServerURL = 'https://CONTOSO-PullSrv:8080/PSDSCPullServer.svc'

        }
    }
}
PullClientConfigID
```

<span data-ttu-id="20106-114">A parancsfájl a **ConfigurationRepositoryWeb** blokk határozza meg a lekérési kiszolgálójával.</span><span class="sxs-lookup"><span data-stu-id="20106-114">In the script, the **ConfigurationRepositoryWeb** block defines the pull server.</span></span> <span data-ttu-id="20106-115">A **kiszolgáló URL-címe**</span><span class="sxs-lookup"><span data-stu-id="20106-115">The **ServerURL**</span></span>

<span data-ttu-id="20106-116">A parancsfájl futtatása után a rendszer létrehoz egy új kimeneti mappát **PullClientConfigID** , és nincs helyezi metakonfigurációját MOF-fájlt.</span><span class="sxs-lookup"><span data-stu-id="20106-116">After this script runs, it creates a new output folder named **PullClientConfigID** and puts a metaconfiguration MOF file there.</span></span> <span data-ttu-id="20106-117">Ebben az esetben a metakonfigurációját MOF-fájl neve lehet `localhost.meta.mof`.</span><span class="sxs-lookup"><span data-stu-id="20106-117">In this case, the metaconfiguration MOF file will be named `localhost.meta.mof`.</span></span>

<span data-ttu-id="20106-118">A konfiguráció alkalmazásához, hívja meg a **Set-DscLocalConfigurationManager** parancsmag, az a **elérési** beállítása a metakonfigurációját MOF-fájl helyét.</span><span class="sxs-lookup"><span data-stu-id="20106-118">To apply the configuration, call the **Set-DscLocalConfigurationManager** cmdlet, with the **Path** set to the location of the metaconfiguration MOF file.</span></span> <span data-ttu-id="20106-119">Például: `Set-DSCLocalConfigurationManager localhost –Path .\PullClientConfigID –Verbose.`</span><span class="sxs-lookup"><span data-stu-id="20106-119">For example: `Set-DSCLocalConfigurationManager localhost –Path .\PullClientConfigID –Verbose.`</span></span>

## <a name="configuration-id"></a><span data-ttu-id="20106-120">Konfiguráció azonosítója</span><span class="sxs-lookup"><span data-stu-id="20106-120">Configuration ID</span></span>

<span data-ttu-id="20106-121">A parancsfájl beállítása a **ConfigurationID** korábban erre a célra létrehozott egyedi azonosítóvá LCM tulajdonságának (GUID segítségével létrehozható a **New-Guid** parancsmag).</span><span class="sxs-lookup"><span data-stu-id="20106-121">The script sets the **ConfigurationID** property of LCM to a GUID that had been previously created for this purpose (you can create a GUID by using the **New-Guid** cmdlet).</span></span> <span data-ttu-id="20106-122">A **ConfigurationID** van a LCM használja a megfelelő konfigurációja a lekérési kiszolgálón található.</span><span class="sxs-lookup"><span data-stu-id="20106-122">The **ConfigurationID** is what the LCM uses to find the appropriate configuration on the pull server.</span></span> <span data-ttu-id="20106-123">A konfigurációs MOF-fájlt a lekérési kiszolgálón névvel kell ellátni _ConfigurationID_.mof, ahol _ConfigurationID_ értéke a **ConfigurationID** a TARGET tulajdonság csomópont LCM.</span><span class="sxs-lookup"><span data-stu-id="20106-123">The configuration MOF file on the pull server must be named _ConfigurationID_.mof, where _ConfigurationID_ is the value of the **ConfigurationID** property of the target node's LCM.</span></span>

## <a name="smb-pull-server"></a><span data-ttu-id="20106-124">SMB-lekérési kiszolgálón</span><span class="sxs-lookup"><span data-stu-id="20106-124">SMB pull server</span></span>

<span data-ttu-id="20106-125">Állíthat be egy ügyfél lekéréses konfigurációi az SMB-kiszolgálón, használja a **ConfigurationRepositoryShare** blokkot.</span><span class="sxs-lookup"><span data-stu-id="20106-125">To set up a client to pull configurations from an SMB server, use a **ConfigurationRepositoryShare** block.</span></span> <span data-ttu-id="20106-126">Az egy **ConfigurationRepositoryShare** blokkot, a kiszolgáló elérési útvonalát úgy, hogy adja meg a **SourcePath** tulajdonság.</span><span class="sxs-lookup"><span data-stu-id="20106-126">In a **ConfigurationRepositoryShare** block, you specify the path to the server by setting the **SourcePath** property.</span></span> <span data-ttu-id="20106-127">A következő metakonfigurációját konfigurálja a célcsomóponton való lekérésére egy SMB lekérési kiszolgálójáról nevű **SMBPullServer**.</span><span class="sxs-lookup"><span data-stu-id="20106-127">The following metaconfiguration configures the target node to pull from an SMB pull server named **SMBPullServer**.</span></span>

```powershell
[DSCLocalConfigurationManager()]
configuration PullClientConfigID
{
    Node localhost
    {
        Settings
        {
            RefreshMode = 'Pull'
            ConfigurationID = '1d545e3b-60c3-47a0-bf65-5afc05182fd0'
            RefreshFrequencyMins = 30
            RebootNodeIfNeeded = $true
        }
        ConfigurationRepositoryShare SMBPullServer
        {
            SourcePath = '\\SMBPullServer\PullSource'

        }
    }
}
PullClientConfigID
```

## <a name="resource-and-report-servers"></a><span data-ttu-id="20106-128">Erőforrás-és a jelentés</span><span class="sxs-lookup"><span data-stu-id="20106-128">Resource and report servers</span></span>

<span data-ttu-id="20106-129">Ha csak adja meg a **ConfigurationRepositoryWeb** vagy **ConfigurationRepositoryShare** (ahogy az előző példában) LCM konfigurációs letiltása, a lekéréses ügyfél erőforrásokat fogja lekérni a megadott kiszolgálón, de nem küld jelentéseket rá.</span><span class="sxs-lookup"><span data-stu-id="20106-129">If you specify only a **ConfigurationRepositoryWeb** or **ConfigurationRepositoryShare** block in your LCM configuration (as in the previous example), the pull client will pull resources from the specified server, but it will not send reports to it.</span></span> <span data-ttu-id="20106-130">Konfigurációk, erőforrások és jelentéskészítési olyan egyetlen lekéréses kiszolgálót is használhat, de létre kell hoznia egy **ReportRepositoryWeb** blokk jelentéskészítés beállítása.</span><span class="sxs-lookup"><span data-stu-id="20106-130">You can use a single pull server for configurations, resources, and reporting, but you have to create a **ReportRepositoryWeb** block to set up reporting.</span></span>

<span data-ttu-id="20106-131">A következő példa bemutatja egy metakonfigurációját állítja be az ügyfél lekéréses konfigurációk és az erőforrások és a jelentés adatainak, lekéréses egyetlen kiszolgálóra történő küldés.</span><span class="sxs-lookup"><span data-stu-id="20106-131">The following example shows a metaconfiguration that sets up a client to pull configurations and resources, and send reporting data, to a single pull server.</span></span>

```powershell
[DSCLocalConfigurationManager()]
configuration PullClientConfigID
{
    Node localhost
    {
        Settings
        {
            RefreshMode = 'Pull'
            ConfigurationID = '1d545e3b-60c3-47a0-bf65-5afc05182fd0'
            RefreshFrequencyMins = 30
            RebootNodeIfNeeded = $true
        }

        ConfigurationRepositoryWeb CONTOSO-PullSrv
        {
            ServerURL = 'https://CONTOSO-PullSrv:8080/PSDSCPullServer.svc'

        }


        ReportServerWeb CONTOSO-PullSrv
        {
            ServerURL = 'https://CONTOSO-PullSrv:8080/PSDSCPullServer.svc'
        }
    }
}
PullClientConfigID
```

<span data-ttu-id="20106-132">Az erőforrások és a jelentéskészítő különböző lekéréses kiszolgálók is megadható.</span><span class="sxs-lookup"><span data-stu-id="20106-132">You can also specify different pull servers for resources and reporting.</span></span> <span data-ttu-id="20106-133">Adjon meg egy erőforrás-kiszolgáló, használhatja a **ResourceRepositoryWeb** (a lekéréses webkiszolgálók) vagy egy **ResourceRepositoryShare** blokk (az SMB-lekérési kiszolgálón).</span><span class="sxs-lookup"><span data-stu-id="20106-133">To specify a resource server, you use either a **ResourceRepositoryWeb** (for a web pull server) or a **ResourceRepositoryShare** block (for an SMB pull server).</span></span>
<span data-ttu-id="20106-134">Adja meg a jelentéskészítő kiszolgálón, akkor használja a **ReportRepositoryWeb** blokkot.</span><span class="sxs-lookup"><span data-stu-id="20106-134">To specify a report server, you use a **ReportRepositoryWeb** block.</span></span> <span data-ttu-id="20106-135">A jelentéskészítő kiszolgáló nem lehet egy SMB-kiszolgálón.</span><span class="sxs-lookup"><span data-stu-id="20106-135">A report server cannot be an SMB server.</span></span>
<span data-ttu-id="20106-136">A következő metakonfigurációját beállítja a konfigurációk a beolvasandó lekéréses ügyfél **CONTOSO-PullSrv** és erőforrását **CONTOSO-ResourceSrv**, és a jelentések küldése  **CONTOSO-ReportSrv**:</span><span class="sxs-lookup"><span data-stu-id="20106-136">The following metaconfiguration configures a pull client to get its configurations from **CONTOSO-PullSrv** and its resources from **CONTOSO-ResourceSrv**, and to send status reports to **CONTOSO-ReportSrv**:</span></span>

```powershell
[DSCLocalConfigurationManager()]
configuration PullClientConfigID
{
    Node localhost
    {
        Settings
        {
            RefreshMode = 'Pull'
            ConfigurationID = '1d545e3b-60c3-47a0-bf65-5afc05182fd0'
            RefreshFrequencyMins = 30
            RebootNodeIfNeeded = $true
        }

        ConfigurationRepositoryWeb CONTOSO-PullSrv
        {
            ServerURL = 'https://CONTOSO-PullSrv:8080/PSDSCPullServer.svc'

        }

        ResourceRepositoryWeb CONTOSO-ResourceSrv
        {
            ServerURL = 'https://CONTOSO-REsourceSrv:8080/PSDSCPullServer.svc'
        }

        ReportServerWeb CONTOSO-ReportSrv
        {
            ServerURL = 'https://CONTOSO-REsourceSrv:8080/PSDSCPullServer.svc'
        }
    }
}
PullClientConfigID
```

## <a name="see-also"></a><span data-ttu-id="20106-137">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="20106-137">See Also</span></span>

* [<span data-ttu-id="20106-138">Konfigurációs nevek lekéréses ügyfél beállítása</span><span class="sxs-lookup"><span data-stu-id="20106-138">Setting up a pull client with configuration names</span></span>](pullClientConfigNames.md)