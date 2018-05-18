---
ms.date: 06/12/2017
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: Lekérési ügyfél beállítása konfigurációs nevekkel
ms.openlocfilehash: d71376d84b9d4b0e74fdccab4b9249b2ca4263cb
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/16/2018
---
# <a name="setting-up-a-pull-client-using-configuration-names"></a><span data-ttu-id="af6fe-103">Lekérési ügyfél beállítása konfigurációs nevekkel</span><span class="sxs-lookup"><span data-stu-id="af6fe-103">Setting up a pull client using configuration names</span></span>

> <span data-ttu-id="af6fe-104">Vonatkozik: A Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="af6fe-104">Applies To: Windows PowerShell 5.0</span></span>

> [!IMPORTANT]
> <span data-ttu-id="af6fe-105">A lekéréses kiszolgáló (Windows-szolgáltatás *DSC-szolgáltatás*), Windows Server támogatott összetevője létezik azonban a következők: nem tervezi, hogy új funkciók és képességek kínálnak.</span><span class="sxs-lookup"><span data-stu-id="af6fe-105">The Pull Server (Windows Feature *DSC-Service*) is a supported component of Windows Server however there are no plans to offer new features or capabilities.</span></span> <span data-ttu-id="af6fe-106">Javasoljuk, hogy kezdje a Váltás felügyelt ügyfelek [Azure Automation DSC](/azure/automation/automation-dsc-getting-started) (tartalmazza a Windows Server-kiszolgáló lekéréses is) vagy a közösségi megoldásoknak a valamelyikét felsorolt [Itt](pullserver.md#community-solutions-for-pull-service).</span><span class="sxs-lookup"><span data-stu-id="af6fe-106">It is recommended to begin transitioning managed clients to [Azure Automation DSC](/azure/automation/automation-dsc-getting-started) (includes features beyond Pull Server on Windows Server) or one of the community solutions listed [here](pullserver.md#community-solutions-for-pull-service).</span></span>

<span data-ttu-id="af6fe-107">Minden egyes célcsomóponttal lekéréses módban a rendszergazda és az URL-címet kap, ahol lépjen kapcsolatba a lekérési kiszolgálójával konfigurációt beolvasandó ki.</span><span class="sxs-lookup"><span data-stu-id="af6fe-107">Each target node has to be told to use pull mode and given the URL where it can contact the pull server to get configurations.</span></span>
<span data-ttu-id="af6fe-108">Ehhez az szükséges, hogy a helyi Configuration Manager (LCM) konfigurálnia a szükséges adatokat.</span><span class="sxs-lookup"><span data-stu-id="af6fe-108">To do this, you have to configure the Local Configuration Manager (LCM) with the necessary information.</span></span>
<span data-ttu-id="af6fe-109">A LCM konfigurálásához hoz létre egy speciális konfigurációs attribútummal. az **DSCLocalConfigurationManager** attribútum.</span><span class="sxs-lookup"><span data-stu-id="af6fe-109">To configure the LCM, you create a special type of configuration, decorated with the **DSCLocalConfigurationManager** attribute.</span></span>
<span data-ttu-id="af6fe-110">A LCM konfigurálásával kapcsolatos további információkért lásd: [konfigurálása a helyi Configuration Manager](metaConfig.md).</span><span class="sxs-lookup"><span data-stu-id="af6fe-110">For more information about configuring the LCM, see [Configuring the Local Configuration Manager](metaConfig.md).</span></span>

> <span data-ttu-id="af6fe-111">**Megjegyzés:**: Ez a témakör PowerShell 5.0 vonatkozik.</span><span class="sxs-lookup"><span data-stu-id="af6fe-111">**Note**: This topic applies to PowerShell 5.0.</span></span>
<span data-ttu-id="af6fe-112">A PowerShell 4.0 lekéréses ügyfél beállításával kapcsolatos információkért lásd: [konfigurációs azonosítójával PowerShell 4.0 lekéréses ügyfél beállítása](pullClientConfigID4.md)</span><span class="sxs-lookup"><span data-stu-id="af6fe-112">For information on setting up a pull client in PowerShell 4.0, see [Setting up a pull client using configuration ID in PowerShell 4.0](pullClientConfigID4.md)</span></span>

<span data-ttu-id="af6fe-113">Az alábbi parancsfájl a LCM konfigurálja az lekéréses konfigurációk "CONTOSO-PullSrv" nevű kiszolgálóról:</span><span class="sxs-lookup"><span data-stu-id="af6fe-113">The following script configures the LCM to pull configurations from a server named "CONTOSO-PullSrv":</span></span>

```powershell
[DSCLocalConfigurationManager()]
configuration PullClientConfigNames
{
    Node localhost
    {
        Settings
        {
            RefreshMode = 'Pull'
            RefreshFrequencyMins = 30
            RebootNodeIfNeeded = $true
        }
        ConfigurationRepositoryWeb CONTOSO-PullSrv
        {
            ServerURL = 'https://CONTOSO-PullSrv:8080/PSDSCPullServer.svc'
            RegistrationKey = '140a952b-b9d6-406b-b416-e0f759c9c0e4'
            ConfigurationNames = @('ClientConfig')
        }
    }
}
PullClientConfigNames
```

<span data-ttu-id="af6fe-114">A parancsfájl a **ConfigurationRepositoryWeb** blokk határozza meg a lekérési kiszolgálójával.</span><span class="sxs-lookup"><span data-stu-id="af6fe-114">In the script, the **ConfigurationRepositoryWeb** block defines the pull server.</span></span>
<span data-ttu-id="af6fe-115">A **ServerURL** tulajdonság határozza meg a végpont a lekérési kiszolgálón.</span><span class="sxs-lookup"><span data-stu-id="af6fe-115">The **ServerURL** property specifies the endpoint for the pull server.</span></span>

<span data-ttu-id="af6fe-116">A **RegistrationKey** tulajdonsága egy megosztott kulcsot lekéréses kiszolgáló összes ügyfél-csomópontok és az adott lekéréses kiszolgáló között.</span><span class="sxs-lookup"><span data-stu-id="af6fe-116">The **RegistrationKey** property is a shared key between all client nodes for a pull server and that pull server.</span></span>
<span data-ttu-id="af6fe-117">Ugyanazt az értéket a fájl a lekérési kiszolgálón tárolja.</span><span class="sxs-lookup"><span data-stu-id="af6fe-117">The same value is stored in a file on the pull server.</span></span>

<span data-ttu-id="af6fe-118">A **ConfigurationNames** tulajdonsága olyan tömb, amely meghatározza a konfigurációkat, az ügyfél-csomópontnak szánt nevét.</span><span class="sxs-lookup"><span data-stu-id="af6fe-118">The **ConfigurationNames** property is an array that specifies the names of the configurations intended for the client node.</span></span>
<span data-ttu-id="af6fe-119">A lekérési kiszolgálón a konfigurációs MOF-fájlja nevet kell kapniuk az ügyfél-csomópontnak *ConfigurationNames*.mof, ahol *ConfigurationNames* értéke megegyezik a **ConfigurationNames**  a metakonfigurációját az tulajdonsága.</span><span class="sxs-lookup"><span data-stu-id="af6fe-119">On the pull server, the configuration MOF file for this client node must be named *ConfigurationNames*.mof, where *ConfigurationNames* matches the value of the **ConfigurationNames** property you set in this metaconfiguration.</span></span>

><span data-ttu-id="af6fe-120">**Megjegyzés:** Ha egynél több értéket adja meg a **ConfigurationNames**, meg kell adni **PartialConfiguration** blokkolja a konfigurációt.</span><span class="sxs-lookup"><span data-stu-id="af6fe-120">**Note:** If you specify more than one value in the **ConfigurationNames**, you must also specify **PartialConfiguration** blocks in your configuration.</span></span>
<span data-ttu-id="af6fe-121">Részleges konfigurációkkal kapcsolatos információkért lásd: [PowerShell célállapot-konfiguráció részleges konfigurációk](partialConfigs.md).</span><span class="sxs-lookup"><span data-stu-id="af6fe-121">For information about partial configurations, see [PowerShell Desired State Configuration partial configurations](partialConfigs.md).</span></span>

<span data-ttu-id="af6fe-122">A parancsfájl futtatása után a rendszer létrehoz egy új kimeneti mappát **PullClientConfigNames** , és nincs helyezi metakonfigurációját MOF-fájlt.</span><span class="sxs-lookup"><span data-stu-id="af6fe-122">After this script runs, it creates a new output folder named **PullClientConfigNames** and puts a metaconfiguration MOF file there.</span></span>
<span data-ttu-id="af6fe-123">Ebben az esetben a metakonfigurációját MOF-fájl neve lehet `localhost.meta.mof`.</span><span class="sxs-lookup"><span data-stu-id="af6fe-123">In this case, the metaconfiguration MOF file will be named `localhost.meta.mof`.</span></span>

<span data-ttu-id="af6fe-124">A konfiguráció alkalmazásához, hívja meg a **Set-DscLocalConfigurationManager** parancsmag, az a **elérési** beállítása a metakonfigurációját MOF-fájl helyét.</span><span class="sxs-lookup"><span data-stu-id="af6fe-124">To apply the configuration, call the **Set-DscLocalConfigurationManager** cmdlet, with the **Path** set to the location of the metaconfiguration MOF file.</span></span>

```powershell
Set-DSCLocalConfigurationManager localhost –Path .\PullClientConfigNames –Verbose.
```

> <span data-ttu-id="af6fe-125">**Megjegyzés:**: regisztrációs kulcsokat csak lekéréses webkiszolgálók működik.</span><span class="sxs-lookup"><span data-stu-id="af6fe-125">**Note**: Registration keys work only with web pull servers.</span></span>
<span data-ttu-id="af6fe-126">Továbbra is használnia kell **ConfigurationID** az SMB-lekéréses kiszolgálóval.</span><span class="sxs-lookup"><span data-stu-id="af6fe-126">You must still use **ConfigurationID** with an SMB pull server.</span></span>
<span data-ttu-id="af6fe-127">A lekérési kiszolgálójával használatával konfigurálásával kapcsolatos információkat **ConfigurationID**, lásd: [konfigurációs azonosítójával lekéréses ügyfél beállítása](PullClientConfigNames.md)</span><span class="sxs-lookup"><span data-stu-id="af6fe-127">For information about configuring a pull server by using **ConfigurationID**, see [Setting up a pull client using configuration ID](PullClientConfigNames.md)</span></span>

## <a name="resource-and-report-servers"></a><span data-ttu-id="af6fe-128">Erőforrás-és a jelentés</span><span class="sxs-lookup"><span data-stu-id="af6fe-128">Resource and report servers</span></span>

<span data-ttu-id="af6fe-129">Ha csak adja meg a **ConfigurationRepositoryWeb** vagy **ConfigurationRepositoryShare** (ahogy az előző példában) LCM konfigurációs letiltása, a lekéréses ügyfél erőforrásokat fogja lekérni a megadott kiszolgálón, de nem küld jelentéseket rá.</span><span class="sxs-lookup"><span data-stu-id="af6fe-129">If you specify only a **ConfigurationRepositoryWeb** or **ConfigurationRepositoryShare** block in your LCM configuration (as in the previous example), the pull client will pull resources from the specified server, but it will not send reports to it.</span></span>
<span data-ttu-id="af6fe-130">Konfigurációk, erőforrások és jelentéskészítési olyan egyetlen lekéréses kiszolgálót is használhat, de létre kell hoznia egy **ReportRepositoryWeb** blokk jelentéskészítés beállítása.</span><span class="sxs-lookup"><span data-stu-id="af6fe-130">You can use a single pull server for configurations, resources, and reporting, but you have to create a **ReportRepositoryWeb** block to set up reporting.</span></span>
<span data-ttu-id="af6fe-131">A következő példa bemutatja egy metakonfigurációját állítja be az ügyfél lekéréses konfigurációk és az erőforrások és a jelentés adatainak, lekéréses egyetlen kiszolgálóra történő küldés.</span><span class="sxs-lookup"><span data-stu-id="af6fe-131">The following example shows a metaconfiguration that sets up a client to pull configurations and resources, and send reporting data, to a single pull server.</span></span>

```powershell
[DSCLocalConfigurationManager()]
configuration PullClientConfigNames
{
    Node localhost
    {
        Settings
        {
            RefreshMode = 'Pull'
            RefreshFrequencyMins = 30
            RebootNodeIfNeeded = $true
        }

        ConfigurationRepositoryWeb CONTOSO-PullSrv
        {
            ServerURL = 'https://CONTOSO-PullSrv:8080/PSDSCPullServer.svc'
            RegistrationKey = 'fbc6ef09-ad98-4aad-a062-92b0e0327562'
        }

        ReportServerWeb CONTOSO-PullSrv
        {
            ServerURL = 'https://CONTOSO-PullSrv:8080/PSDSCPullServer.svc'
        }
    }
}
PullClientConfigNames
```

<span data-ttu-id="af6fe-132">Az erőforrások és a jelentéskészítő különböző lekéréses kiszolgálók is megadható.</span><span class="sxs-lookup"><span data-stu-id="af6fe-132">You can also specify different pull servers for resources and reporting.</span></span>
<span data-ttu-id="af6fe-133">Adjon meg egy erőforrás-kiszolgáló, használhatja a **ResourceRepositoryWeb** (a lekéréses webkiszolgálók) vagy egy **ResourceRepositoryShare** blokk (az SMB-lekérési kiszolgálón).</span><span class="sxs-lookup"><span data-stu-id="af6fe-133">To specify a resource server, you use either a **ResourceRepositoryWeb** (for a web pull server) or a **ResourceRepositoryShare** block (for an SMB pull server).</span></span>
<span data-ttu-id="af6fe-134">Adja meg a jelentéskészítő kiszolgálón, akkor használja a **ReportRepositoryWeb** blokkot.</span><span class="sxs-lookup"><span data-stu-id="af6fe-134">To specify a report server, you use a **ReportRepositoryWeb** block.</span></span>
<span data-ttu-id="af6fe-135">A jelentéskészítő kiszolgáló nem lehet egy SMB-kiszolgálón.</span><span class="sxs-lookup"><span data-stu-id="af6fe-135">A report server cannot be an SMB server.</span></span>
<span data-ttu-id="af6fe-136">A következő metakonfigurációját beállítja a konfigurációk a beolvasandó lekéréses ügyfél **CONTOSO-PullSrv** és erőforrását **CONTOSO-ResourceSrv**, és a jelentések küldése  **CONTOSO-ReportSrv**:</span><span class="sxs-lookup"><span data-stu-id="af6fe-136">The following metaconfiguration configures a pull client to get its configurations from **CONTOSO-PullSrv** and its resources from **CONTOSO-ResourceSrv**, and to send status reports to **CONTOSO-ReportSrv**:</span></span>

```powershell
[DSCLocalConfigurationManager()]
configuration PullClientConfigNames
{
    Node localhost
    {
        Settings
        {
            RefreshMode = 'Pull'
            RefreshFrequencyMins = 30
            RebootNodeIfNeeded = $true
        }

        ConfigurationRepositoryWeb CONTOSO-PullSrv
        {
            ServerURL = 'https://CONTOSO-PullSrv:8080/PSDSCPullServer.svc'
            RegistrationKey = 'fbc6ef09-ad98-4aad-a062-92b0e0327562'
        }

        ResourceRepositoryWeb CONTOSO-ResourceSrv
        {
            ServerURL = 'https://CONTOSO-ResourceSrv:8080/PSDSCPullServer.svc'
            RegistrationKey = '30ef9bd8-9acf-4e01-8374-4dc35710fc90'
        }

        ReportServerWeb CONTOSO-ReportSrv
        {
            ServerURL = 'https://CONTOSO-ReportSrv:8080/PSDSCPullServer.svc'
            RegistrationKey = '6b392c6a-818c-4b24-bf38-47124f1e2f14'
        }
    }
}
PullClientConfigNames
```

## <a name="see-also"></a><span data-ttu-id="af6fe-137">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="af6fe-137">See Also</span></span>

* [<span data-ttu-id="af6fe-138">Konfigurációs azonosítójú lekéréses ügyfél beállítása</span><span class="sxs-lookup"><span data-stu-id="af6fe-138">Setting up a pull client with configuration ID</span></span>](PullClientConfigNames.md)
* [<span data-ttu-id="af6fe-139">A DSC lekérési webkiszolgáló beállítása</span><span class="sxs-lookup"><span data-stu-id="af6fe-139">Setting up a DSC web pull server</span></span>](pullServer.md)