---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: Konfigurációs nevekkel PowerShell 5.0-s és újabb verziók lekérési ügyfél beállítása
ms.openlocfilehash: d591e2a757130ccecaf4eaf9f363f607fca82b93
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62079387"
---
# <a name="set-up-a-pull-client-using-configuration-names-in-powershell-50-and-later"></a><span data-ttu-id="95139-103">Konfigurációs nevekkel PowerShell 5.0-s és újabb verziók lekérési ügyfél beállítása</span><span class="sxs-lookup"><span data-stu-id="95139-103">Set up a Pull Client using Configuration Names in PowerShell 5.0 and later</span></span>

> <span data-ttu-id="95139-104">A következőkre vonatkozik: Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="95139-104">Applies To: Windows PowerShell 5.0</span></span>

> [!IMPORTANT]
> <span data-ttu-id="95139-105">A lekéréses kiszolgálón (Windows-szolgáltatás *DSC-szolgáltatás*), a Windows Server támogatott összetevője létezik azonban tervekben sem funkciókat és képességeket kínálnak.</span><span class="sxs-lookup"><span data-stu-id="95139-105">The Pull Server (Windows Feature *DSC-Service*) is a supported component of Windows Server however there are no plans to offer new features or capabilities.</span></span> <span data-ttu-id="95139-106">Javasoljuk, hogy helyeződnek felügyelt ügyfelek [Azure Automation DSC](/azure/automation/automation-dsc-getting-started) (beleértve a lekéréses kiszolgálón a Windows Server csomagban) vagy a közösségi megoldások felsorolt [Itt](pullserver.md#community-solutions-for-pull-service).</span><span class="sxs-lookup"><span data-stu-id="95139-106">It is recommended to begin transitioning managed clients to [Azure Automation DSC](/azure/automation/automation-dsc-getting-started) (includes features beyond Pull Server on Windows Server) or one of the community solutions listed [here](pullserver.md#community-solutions-for-pull-service).</span></span>

<span data-ttu-id="95139-107">Lekérési ügyfél beállítása előtt be kell állítania egy lekéréses kiszolgálót.</span><span class="sxs-lookup"><span data-stu-id="95139-107">Before setting up a pull client, you should set up a pull server.</span></span> <span data-ttu-id="95139-108">Bár nem kötelező ebben a sorrendben, segít a hibák elhárításában, és így gondoskodik róla, hogy a regisztráció sikeres volt-e.</span><span class="sxs-lookup"><span data-stu-id="95139-108">Though this order is not required, it helps with troubleshooting, and helps you ensure that the registration was successful.</span></span> <span data-ttu-id="95139-109">Állítson be egy lekéréses kiszolgálót, használhatja a következő útmutatókat:</span><span class="sxs-lookup"><span data-stu-id="95139-109">To set up a pull server, you can use the following guides:</span></span>

- [<span data-ttu-id="95139-110">DSC SMB-lekérési kiszolgáló beállítása</span><span class="sxs-lookup"><span data-stu-id="95139-110">Set up a DSC SMB Pull Server</span></span>](pullServerSmb.md)
- [<span data-ttu-id="95139-111">A DSC HTTP-lekérési kiszolgáló beállítása</span><span class="sxs-lookup"><span data-stu-id="95139-111">Set up a DSC HTTP Pull Server</span></span>](pullServer.md)

<span data-ttu-id="95139-112">Minden egyes célcsomóponttal konfigurálható töltse le a konfigurációk, az erőforrásokat, és még jelentést annak állapotát.</span><span class="sxs-lookup"><span data-stu-id="95139-112">Each target node can be configured to download configurations, resources, and even report its status.</span></span> <span data-ttu-id="95139-113">Az alábbi szakaszok bemutatják, hogyan lekérési ügyfél beállítása egy SMB-megosztáson, vagy a HTTP-DSC lekéréses kiszolgálón.</span><span class="sxs-lookup"><span data-stu-id="95139-113">The sections below show you how to configure a pull client with an SMB share or HTTP DSC Pull Server.</span></span> <span data-ttu-id="95139-114">Amikor a csomópont LCM frissíti, a konfigurált helyre, töltse le a hozzárendelt konfigurációkat, felveszi Önnel.</span><span class="sxs-lookup"><span data-stu-id="95139-114">When the Node's LCM refreshes, it will reach out to the configured location to download any assigned configurations.</span></span> <span data-ttu-id="95139-115">Ha minden szükséges erőforrás nem létezik a csomóponton, azt automatikusan letöltheti őket a beállított helyről.</span><span class="sxs-lookup"><span data-stu-id="95139-115">If any required resources do not exist on the Node, it will automatically download them from the configured location.</span></span> <span data-ttu-id="95139-116">Ha a csomópont konfigurálva van egy [jelentéskészítő kiszolgáló](reportServer.md), majd a művelet állapotát jelzi.</span><span class="sxs-lookup"><span data-stu-id="95139-116">If the Node is configured with a [Report Server](reportServer.md), it will then report the status of the operation.</span></span>

> [!NOTE]
> <span data-ttu-id="95139-117">Ez a témakör a PowerShell 5.0-s vonatkozik.</span><span class="sxs-lookup"><span data-stu-id="95139-117">This topic applies to PowerShell 5.0.</span></span>
> <span data-ttu-id="95139-118">A PowerShell 4.0-s lekérési ügyfél beállításával kapcsolatos további információkért lásd: [konfigurációs azonosító használatával a PowerShell 4.0-s lekérési ügyfél beállítása](pullClientConfigID4.md)</span><span class="sxs-lookup"><span data-stu-id="95139-118">For information on setting up a pull client in PowerShell 4.0, see [Set up a pull client using configuration ID in PowerShell 4.0](pullClientConfigID4.md)</span></span>

## <a name="configure-the-pull-client-lcm"></a><span data-ttu-id="95139-119">Lekérési ügyfél LCM konfigurálása</span><span class="sxs-lookup"><span data-stu-id="95139-119">Configure the pull client LCM</span></span>

<span data-ttu-id="95139-120">Az alábbi példák bármelyikét végrehajtása hoz létre egy új nevű kimeneti mappát **PullClientConfigName** , és ott helyezi metaconfiguration MOF-fájlt.</span><span class="sxs-lookup"><span data-stu-id="95139-120">Executing any of the examples below creates a new output folder named **PullClientConfigName** and puts a metaconfiguration MOF file there.</span></span> <span data-ttu-id="95139-121">Ebben az esetben a metaconfiguration MOF-fájl neve lesz `localhost.meta.mof`.</span><span class="sxs-lookup"><span data-stu-id="95139-121">In this case, the metaconfiguration MOF file will be named `localhost.meta.mof`.</span></span>

<span data-ttu-id="95139-122">A alkalmazni a konfigurációt, hívja meg a **Set-DscLocalConfigurationManager** parancsmag, az a **elérési út** állítsa be a metaconfiguration MOF-fájl helyét.</span><span class="sxs-lookup"><span data-stu-id="95139-122">To apply the configuration, call the **Set-DscLocalConfigurationManager** cmdlet, with the **Path** set to the location of the metaconfiguration MOF file.</span></span> <span data-ttu-id="95139-123">Például:</span><span class="sxs-lookup"><span data-stu-id="95139-123">For example:</span></span>

```powershell
Set-DSCLocalConfigurationManager –ComputerName localhost –Path .\PullClientConfigName –Verbose.
```

## <a name="configuration-name"></a><span data-ttu-id="95139-124">Konfiguráció neve</span><span class="sxs-lookup"><span data-stu-id="95139-124">Configuration Name</span></span>

<span data-ttu-id="95139-125">Csoportok alábbi példák a **ConfigurationName** egy korábban lefordított konfiguráció nevét a LCM tulajdonságát erre a célra létrehozott.</span><span class="sxs-lookup"><span data-stu-id="95139-125">The examples below sets the **ConfigurationName** property of the LCM to the name of a previously compiled Configuration, created for this purpose.</span></span> <span data-ttu-id="95139-126">A **ConfigurationName** van, használja az LCM Konfigurálása a megfelelő konfiguráció keresése a lekérési kiszolgálón.</span><span class="sxs-lookup"><span data-stu-id="95139-126">The **ConfigurationName** is what the LCM uses to find the appropriate configuration on the pull server.</span></span> <span data-ttu-id="95139-127">A lekérési kiszolgálón a konfigurációs MOF-fájl neve legyen `<ConfigurationName>.mof`, ebben az esetben "ClientConfig.mof".</span><span class="sxs-lookup"><span data-stu-id="95139-127">The configuration MOF file on the pull server must be named `<ConfigurationName>.mof`, in this case, "ClientConfig.mof".</span></span> <span data-ttu-id="95139-128">További információkért lásd: [konfigurációk közzététele egy lekéréses kiszolgálóra (v4 vagy v5)](publishConfigs.md).</span><span class="sxs-lookup"><span data-stu-id="95139-128">For more information, see [Publish Configurations to a Pull Server (v4/v5)](publishConfigs.md).</span></span>

## <a name="set-up-a-pull-client-to-download-configurations"></a><span data-ttu-id="95139-129">Lekérési ügyfél beállítása a konfiguráció letöltése</span><span class="sxs-lookup"><span data-stu-id="95139-129">Set up a Pull Client to download Configurations</span></span>

<span data-ttu-id="95139-130">Minden egyes ügyfélnek meg kell adni a **lekéréses** módban, és a pull-kiszolgáló URL-címét a konfigurációja tárolására.</span><span class="sxs-lookup"><span data-stu-id="95139-130">Each client must be configured in **Pull** mode and given the pull server url where its configuration is stored.</span></span> <span data-ttu-id="95139-131">Ehhez az szükséges, akkor a helyi Configuration Manager (LCM) konfigurálása a szükséges információkat.</span><span class="sxs-lookup"><span data-stu-id="95139-131">To do this, you have to configure the Local Configuration Manager (LCM) with the necessary information.</span></span> <span data-ttu-id="95139-132">Az LCM konfigurálása, a konfiguráció, a kitüntetett különleges hoz létre a **DSCLocalConfigurationManager** attribútum.</span><span class="sxs-lookup"><span data-stu-id="95139-132">To configure the LCM, you create a special type of configuration, decorated with the **DSCLocalConfigurationManager** attribute.</span></span> <span data-ttu-id="95139-133">Az LCM konfigurálása kapcsolatos további információkért lásd: [a Local Configuration Manager](../managing-nodes/metaConfig.md).</span><span class="sxs-lookup"><span data-stu-id="95139-133">For more information about configuring the LCM, see [Configuring the Local Configuration Manager](../managing-nodes/metaConfig.md).</span></span>

<span data-ttu-id="95139-134">A következő szkriptet az LCM lekéréses konfigurációk úgy konfigurálja a kiszolgáló neve "CONTOSO-PullSrv".</span><span class="sxs-lookup"><span data-stu-id="95139-134">The following script configures the LCM to pull configurations from a server named "CONTOSO-PullSrv".</span></span>

- <span data-ttu-id="95139-135">A parancsfájl a **ConfigurationRepositoryWeb** blokk határozza meg a lekéréses kiszolgálón.</span><span class="sxs-lookup"><span data-stu-id="95139-135">In the script, the **ConfigurationRepositoryWeb** block defines the pull server.</span></span> <span data-ttu-id="95139-136">A **ServerURL** tulajdonsága azt adja meg a végpont a lekéréses kiszolgálón.</span><span class="sxs-lookup"><span data-stu-id="95139-136">The **ServerURL** property specifies the endpoint for the pull server.</span></span>

- <span data-ttu-id="95139-137">A **RegistrationKey** tulajdonság egy lekéréses kiszolgálón található összes ügyfél csomópont és a lekéréses kiszolgálón között megosztott kulcs.</span><span class="sxs-lookup"><span data-stu-id="95139-137">The **RegistrationKey** property is a shared key between all client nodes for a pull server and that pull server.</span></span> <span data-ttu-id="95139-138">Ugyanazt az értéket egy fájlt a lekérési kiszolgálón van tárolva.</span><span class="sxs-lookup"><span data-stu-id="95139-138">The same value is stored in a file on the pull server.</span></span>
  > [!NOTE]
  > <span data-ttu-id="95139-139">Regisztrációs kulcs csak a munkahelyi **webes** kiszolgálók lekérése.</span><span class="sxs-lookup"><span data-stu-id="95139-139">Registration keys work only with **web** pull servers.</span></span> <span data-ttu-id="95139-140">Továbbra is kell használnia **ConfigurationID** együtt egy **SMB** lekéréses kiszolgálón.</span><span class="sxs-lookup"><span data-stu-id="95139-140">You must still use **ConfigurationID** with an **SMB** pull server.</span></span>
  > <span data-ttu-id="95139-141">Használatával egy lekéréses kiszolgálót konfigurálásával kapcsolatos információkat **ConfigurationID**, lásd: [konfigurációs azonosítóval lekérési ügyfél beállítása](pullClientConfigId.md)</span><span class="sxs-lookup"><span data-stu-id="95139-141">For information about configuring a pull server by using **ConfigurationID**, see [Setting up a pull client using configuration ID](pullClientConfigId.md)</span></span>

- <span data-ttu-id="95139-142">A **ConfigurationNames** tulajdonság értéke egy tömb, amely megadja azoknak szól, az ügyfél csomópont-konfigurációk a nevét.</span><span class="sxs-lookup"><span data-stu-id="95139-142">The **ConfigurationNames** property is an array that specifies the names of the configurations intended for the client node.</span></span>
  ><span data-ttu-id="95139-143">**Megjegyzés:** Ha egynél több értéket adja meg a **ConfigurationNames**, meg kell adnia **PartialConfiguration** letiltja a konfigurációban.</span><span class="sxs-lookup"><span data-stu-id="95139-143">**Note:** If you specify more than one value in the **ConfigurationNames**, you must also specify **PartialConfiguration** blocks in your configuration.</span></span>
  ><span data-ttu-id="95139-144">Részleges konfigurációk kapcsolatos további információkért lásd: [PowerShell Desired State Configuration részleges konfigurációk](partialConfigs.md).</span><span class="sxs-lookup"><span data-stu-id="95139-144">For information about partial configurations, see [PowerShell Desired State Configuration partial configurations](partialConfigs.md).</span></span>

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

## <a name="set-up-a-pull-client-to-download-resources"></a><span data-ttu-id="95139-145">Lekérési ügyfél beállítása az erőforrások letöltéséhez</span><span class="sxs-lookup"><span data-stu-id="95139-145">Set up a Pull Client to download Resources</span></span>

<span data-ttu-id="95139-146">Ha csak adja meg egy **ConfigurationRepositoryWeb** vagy **ConfigurationRepositoryShare** letiltása az LCM konfigurálása (ahogy az előző példában), a lekérési ügyfél azonos erőforrásokat kéri a ".mof" fájlokat tároló helye.</span><span class="sxs-lookup"><span data-stu-id="95139-146">If you specify only a **ConfigurationRepositoryWeb** or **ConfigurationRepositoryShare** block in your LCM configuration (as in the previous example), the pull client will pull resources from same location where your ".mof" files are stored.</span></span> <span data-ttu-id="95139-147">Emellett megadhatja a különböző helyeken, ahol az ügyfelek erőforrások letöltéséhez.</span><span class="sxs-lookup"><span data-stu-id="95139-147">You can also specify different locations where clients can download resources.</span></span> <span data-ttu-id="95139-148">Adja meg az erőforrás-kiszolgáló, használhatja a **ResourceRepositoryWeb** (a lekérési kiszolgáló) vagy egy **ResourceRepositoryShare** letiltása (a egy SMB-lekérési kiszolgálójának).</span><span class="sxs-lookup"><span data-stu-id="95139-148">To specify a resource server, you use either a **ResourceRepositoryWeb** (for a web pull server) or a **ResourceRepositoryShare** block (for an SMB pull server).</span></span>

<span data-ttu-id="95139-149">Az alábbi példa bemutatja egy metaconfiguration, amely ügyfél beállítja a konfigurációkat egy lekéréses kiszolgálót és erőforrásokat, SMB-megosztáson töltheti le.</span><span class="sxs-lookup"><span data-stu-id="95139-149">The following example shows a metaconfiguration that sets up a client to download configurations from a Pull Server, and resources from an SMB share.</span></span>

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

        ResourceRepositoryShare SMBResources
        {
            SourcePath = '\\SMBPullServer\Resources'
        }
    }
}
PullClientConfigNames
```

## <a name="set-up-a-pull-client-to-report-status"></a><span data-ttu-id="95139-150">Állapot jelentése érdekében a lekérési ügyfél beállítása</span><span class="sxs-lookup"><span data-stu-id="95139-150">Set up a Pull Client to report status</span></span>

<span data-ttu-id="95139-151">Egy lekéréses kiszolgálót használhat a konfigurációk, erőforrások és jelentéskészítés.</span><span class="sxs-lookup"><span data-stu-id="95139-151">You can use a single pull server for configurations, resources, and reporting.</span></span> <span data-ttu-id="95139-152">Jelentéskészítés nincs konfigurálva az ügyfelek alapértelmezés szerint.</span><span class="sxs-lookup"><span data-stu-id="95139-152">Reporting is not configured for clients by default.</span></span> <span data-ttu-id="95139-153">Állapot jelentése érdekében egy ügyfél konfigurálásához létre kell hoznia egy **ReportRepositoryWeb** letiltása.</span><span class="sxs-lookup"><span data-stu-id="95139-153">To configure a client to report status, you have to create a **ReportRepositoryWeb** block.</span></span> <span data-ttu-id="95139-154">Az alábbi példa bemutatja egy metaconfiguration, amely beállítja a pull-konfigurációkat és erőforrásokat, majd küldje el jelentésadatokat, egyetlen lekéréses kiszolgálóra ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="95139-154">The following example shows a metaconfiguration that sets up a client to pull configurations and resources, and send reporting data, to a single pull server.</span></span>

> [!NOTE]
> <span data-ttu-id="95139-155">A jelentéskészítő kiszolgáló nem lehet SMB-megosztáson.</span><span class="sxs-lookup"><span data-stu-id="95139-155">A report server cannot be an SMB share.</span></span>

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
            RegistrationKey = 'fbc6ef09-ad98-4aad-a062-92b0e0327562'
        }
    }
}
PullClientConfigNames
```

## <a name="see-also"></a><span data-ttu-id="95139-156">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="95139-156">See Also</span></span>

* [<span data-ttu-id="95139-157">Konfigurációs Azonosítóval rendelkező lekérési ügyfél beállítása</span><span class="sxs-lookup"><span data-stu-id="95139-157">Setting up a pull client with configuration ID</span></span>](PullClientConfigNames.md)
* [<span data-ttu-id="95139-158">DSC lekérési kiszolgáló beállítása</span><span class="sxs-lookup"><span data-stu-id="95139-158">Setting up a DSC web pull server</span></span>](pullServer.md)
