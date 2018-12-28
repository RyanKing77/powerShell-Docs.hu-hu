---
ms.date: 12/12/2018
keywords: DSC, powershell, a konfigurációt, a beállítása
title: Konfigurációs azonosítók PowerShell 5.0-s és újabb verziók használata lekérési ügyfél beállítása
ms.openlocfilehash: 8d8cf478f9127e1b7005d1b9e832e84b11612c9c
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/14/2018
ms.locfileid: "53404292"
---
# <a name="set-up-a-pull-client-using-configuration-ids-in-powershell-50-and-later"></a><span data-ttu-id="c00c3-103">Konfigurációs azonosítók PowerShell 5.0-s és újabb verziók használata lekérési ügyfél beállítása</span><span class="sxs-lookup"><span data-stu-id="c00c3-103">Set up a Pull Client using Configuration IDs in PowerShell 5.0 and later</span></span>

> <span data-ttu-id="c00c3-104">Érvényes: Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="c00c3-104">Applies To: Windows PowerShell 5.0</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c00c3-105">A lekéréses kiszolgálón (Windows-szolgáltatás *DSC-szolgáltatás*), a Windows Server támogatott összetevője létezik azonban tervekben sem funkciókat és képességeket kínálnak.</span><span class="sxs-lookup"><span data-stu-id="c00c3-105">The Pull Server (Windows Feature *DSC-Service*) is a supported component of Windows Server however there are no plans to offer new features or capabilities.</span></span> <span data-ttu-id="c00c3-106">Javasoljuk, hogy helyeződnek felügyelt ügyfelek [Azure Automation DSC](/azure/automation/automation-dsc-getting-started) (beleértve a lekéréses kiszolgálón a Windows Server csomagban) vagy a közösségi megoldások felsorolt [Itt](pullserver.md#community-solutions-for-pull-service).</span><span class="sxs-lookup"><span data-stu-id="c00c3-106">It is recommended to begin transitioning managed clients to [Azure Automation DSC](/azure/automation/automation-dsc-getting-started) (includes features beyond Pull Server on Windows Server) or one of the community solutions listed [here](pullserver.md#community-solutions-for-pull-service).</span></span>

<span data-ttu-id="c00c3-107">Lekérési ügyfél beállítása előtt be kell állítania egy lekéréses kiszolgálót.</span><span class="sxs-lookup"><span data-stu-id="c00c3-107">Before setting up a pull client, you should set up a pull server.</span></span> <span data-ttu-id="c00c3-108">Bár nem kötelező ebben a sorrendben, segít a hibák elhárításában, és így gondoskodik róla, hogy a regisztráció sikeres volt-e.</span><span class="sxs-lookup"><span data-stu-id="c00c3-108">Though this order is not required, it helps with troubleshooting, and helps you ensure that the registration was successful.</span></span> <span data-ttu-id="c00c3-109">Állítson be egy lekéréses kiszolgálót, használhatja a következő útmutatókat:</span><span class="sxs-lookup"><span data-stu-id="c00c3-109">To set up a pull server, you can use the following guides:</span></span>

- [<span data-ttu-id="c00c3-110">DSC SMB-lekérési kiszolgáló beállítása</span><span class="sxs-lookup"><span data-stu-id="c00c3-110">Set up a DSC SMB Pull Server</span></span>](pullServerSmb.md)
- [<span data-ttu-id="c00c3-111">A DSC HTTP-lekérési kiszolgáló beállítása</span><span class="sxs-lookup"><span data-stu-id="c00c3-111">Set up a DSC HTTP Pull Server</span></span>](pullServer.md)

<span data-ttu-id="c00c3-112">Minden egyes célcsomóponttal konfigurálható töltse le a konfigurációk, az erőforrásokat, és még jelentést annak állapotát.</span><span class="sxs-lookup"><span data-stu-id="c00c3-112">Each target node can be configured to download configurations, resources, and even report its status.</span></span> <span data-ttu-id="c00c3-113">Az alábbi szakaszok bemutatják, hogyan lekérési ügyfél beállítása egy SMB-megosztáson, vagy a HTTP-DSC lekéréses kiszolgálón.</span><span class="sxs-lookup"><span data-stu-id="c00c3-113">The sections below show you how to configure a pull client with an SMB share or HTTP DSC Pull Server.</span></span> <span data-ttu-id="c00c3-114">Amikor a csomópont LCM frissíti, a konfigurált helyre, töltse le a hozzárendelt konfigurációkat, felveszi Önnel.</span><span class="sxs-lookup"><span data-stu-id="c00c3-114">When the Node's LCM refreshes, it will reach out to the configured location to download any assigned configurations.</span></span> <span data-ttu-id="c00c3-115">Ha minden szükséges erőforrás nem létezik a csomóponton, azt automatikusan letöltheti őket a beállított helyről.</span><span class="sxs-lookup"><span data-stu-id="c00c3-115">If any required resources do not exist on the Node, it will automatically download them from the configured location.</span></span> <span data-ttu-id="c00c3-116">Ha a csomópont konfigurálva van egy [jelentéskészítő kiszolgáló](reportServer.md), majd a művelet állapotát jelzi.</span><span class="sxs-lookup"><span data-stu-id="c00c3-116">If the Node is configured with a [Report Server](reportServer.md), it will then report the status of the operation.</span></span>

> <span data-ttu-id="c00c3-117">**Megjegyzés:**: Ez a témakör a PowerShell 5.0-s vonatkozik.</span><span class="sxs-lookup"><span data-stu-id="c00c3-117">**Note**: This topic applies to PowerShell 5.0.</span></span> <span data-ttu-id="c00c3-118">A PowerShell 4.0-s lekérési ügyfél beállításával kapcsolatos további információkért lásd: [egy lekérési ügyfél beállítása konfigurációs Azonosítóval a PowerShell 4.0-s](pullClientConfigID4.md)</span><span class="sxs-lookup"><span data-stu-id="c00c3-118">For information on setting up a pull client in PowerShell 4.0, see [Setting up a pull client using configuration ID in PowerShell 4.0](pullClientConfigID4.md)</span></span>

## <a name="configure-the-pull-client-lcm"></a><span data-ttu-id="c00c3-119">Lekérési ügyfél LCM konfigurálása</span><span class="sxs-lookup"><span data-stu-id="c00c3-119">Configure the pull client LCM</span></span>

<span data-ttu-id="c00c3-120">Az alábbi példák bármelyikét végrehajtása hoz létre egy új nevű kimeneti mappát **PullClientConfigID** , és ott helyezi metaconfiguration MOF-fájlt.</span><span class="sxs-lookup"><span data-stu-id="c00c3-120">Executing any of the examples below creates a new output folder named **PullClientConfigID** and puts a metaconfiguration MOF file there.</span></span> <span data-ttu-id="c00c3-121">Ebben az esetben a metaconfiguration MOF-fájl neve lesz `localhost.meta.mof`.</span><span class="sxs-lookup"><span data-stu-id="c00c3-121">In this case, the metaconfiguration MOF file will be named `localhost.meta.mof`.</span></span>

<span data-ttu-id="c00c3-122">A alkalmazni a konfigurációt, hívja meg a **Set-DscLocalConfigurationManager** parancsmag, az a **elérési út** állítsa be a metaconfiguration MOF-fájl helyét.</span><span class="sxs-lookup"><span data-stu-id="c00c3-122">To apply the configuration, call the **Set-DscLocalConfigurationManager** cmdlet, with the **Path** set to the location of the metaconfiguration MOF file.</span></span> <span data-ttu-id="c00c3-123">Például:</span><span class="sxs-lookup"><span data-stu-id="c00c3-123">For example:</span></span>

```powershell
Set-DSCLocalConfigurationManager –ComputerName localhost –Path .\PullClientConfigId –Verbose.
```

## <a name="configuration-id"></a><span data-ttu-id="c00c3-124">Konfiguráció azonosítója</span><span class="sxs-lookup"><span data-stu-id="c00c3-124">Configuration ID</span></span>

<span data-ttu-id="c00c3-125">Csoportok alábbi példák a **ConfigurationID** , az LCM tulajdonságát egy **Guid** , amely korábban létrehozott erre a célra.</span><span class="sxs-lookup"><span data-stu-id="c00c3-125">The examples below sets the **ConfigurationID** property of the LCM to a **Guid** that had been previously created for this purpose.</span></span> <span data-ttu-id="c00c3-126">A **ConfigurationID** van, használja az LCM Konfigurálása a megfelelő konfiguráció keresése a lekérési kiszolgálón.</span><span class="sxs-lookup"><span data-stu-id="c00c3-126">The **ConfigurationID** is what the LCM uses to find the appropriate configuration on the pull server.</span></span> <span data-ttu-id="c00c3-127">A lekérési kiszolgálón a konfigurációs MOF-fájl neve legyen `ConfigurationID.mof`, ahol *ConfigurationID* értéke a **ConfigurationID** a célcsomópont LCM tulajdonságát.</span><span class="sxs-lookup"><span data-stu-id="c00c3-127">The configuration MOF file on the pull server must be named `ConfigurationID.mof`, where *ConfigurationID* is the value of the **ConfigurationID** property of the target node's LCM.</span></span> <span data-ttu-id="c00c3-128">További információ: [konfigurációk közzététele egy lekéréses kiszolgálóra (v4 vagy v5)](publishConfigs.md).</span><span class="sxs-lookup"><span data-stu-id="c00c3-128">For more information see [Publish Configurations to a Pull Server (v4/v5)](publishConfigs.md).</span></span>

<span data-ttu-id="c00c3-129">Létrehozhat egy véletlenszerű **Guid** alább, vagy használja a példánál a [új GUID-azonosítója](/powershell/module/microsoft.powershell.utility/new-guid) parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="c00c3-129">You can create a random **Guid** using the example below, or by using the [New-Guid](/powershell/module/microsoft.powershell.utility/new-guid) cmdlet.</span></span>

```powershell
[System.Guid]::NewGuid()
```

<span data-ttu-id="c00c3-130">Használatával kapcsolatos további részletekért **GUID** a környezetben, lásd: [GUID tervezése](/powershell/dsc/secureserver#guids).</span><span class="sxs-lookup"><span data-stu-id="c00c3-130">For more information about using **Guids** in your environment, see [Plan for Guids](/powershell/dsc/secureserver#guids).</span></span>

## <a name="set-up-a-pull-client-to-download-configurations"></a><span data-ttu-id="c00c3-131">Lekérési ügyfél beállítása a konfiguráció letöltése</span><span class="sxs-lookup"><span data-stu-id="c00c3-131">Set up a Pull Client to download Configurations</span></span>

<span data-ttu-id="c00c3-132">Minden egyes ügyfélnek meg kell adni a **lekéréses** módban, és a pull-kiszolgáló URL-címét a konfigurációja tárolására.</span><span class="sxs-lookup"><span data-stu-id="c00c3-132">Each client must be configured in **Pull** mode and given the pull server url where its configuration is stored.</span></span> <span data-ttu-id="c00c3-133">Ehhez az szükséges, akkor a helyi Configuration Manager (LCM) konfigurálása a szükséges információkat.</span><span class="sxs-lookup"><span data-stu-id="c00c3-133">To do this, you have to configure the Local Configuration Manager (LCM) with the necessary information.</span></span> <span data-ttu-id="c00c3-134">Az LCM konfigurálása, a konfiguráció, a kitüntetett különleges hoz létre a **DSCLocalConfigurationManager** attribútum.</span><span class="sxs-lookup"><span data-stu-id="c00c3-134">To configure the LCM, you create a special type of configuration, decorated with the **DSCLocalConfigurationManager** attribute.</span></span> <span data-ttu-id="c00c3-135">Az LCM konfigurálása kapcsolatos további információkért lásd: [a Local Configuration Manager](../managing-nodes/metaConfig.md).</span><span class="sxs-lookup"><span data-stu-id="c00c3-135">For more information about configuring the LCM, see [Configuring the Local Configuration Manager](../managing-nodes/metaConfig.md).</span></span>

### <a name="http-dsc-pull-server"></a><span data-ttu-id="c00c3-136">HTTP-DSC lekéréses kiszolgálón</span><span class="sxs-lookup"><span data-stu-id="c00c3-136">HTTP DSC Pull Server</span></span>

<span data-ttu-id="c00c3-137">A következő szkriptet az LCM lekéréses konfigurációk úgy konfigurálja a kiszolgáló neve "CONTOSO-PullSrv".</span><span class="sxs-lookup"><span data-stu-id="c00c3-137">The following script configures the LCM to pull configurations from a server named "CONTOSO-PullSrv".</span></span>

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

<span data-ttu-id="c00c3-138">A parancsfájl a **ConfigurationRepositoryWeb** blokk határozza meg a lekéréses kiszolgálón.</span><span class="sxs-lookup"><span data-stu-id="c00c3-138">In the script, the **ConfigurationRepositoryWeb** block defines the pull server.</span></span> <span data-ttu-id="c00c3-139">A **ServerUrl** adja meg az URL-címét a DSC lekéréses</span><span class="sxs-lookup"><span data-stu-id="c00c3-139">The **ServerUrl** specifies the url of the DSC Pull</span></span>

### <a name="smb-share"></a><span data-ttu-id="c00c3-140">SMB-megosztás</span><span class="sxs-lookup"><span data-stu-id="c00c3-140">SMB Share</span></span>

<span data-ttu-id="c00c3-141">A következő szkriptet az LCM konfigurálja lekéréses konfigurációk az SMB-megosztás a `\\SMBPullServer\Pull`.</span><span class="sxs-lookup"><span data-stu-id="c00c3-141">The following script configures the LCM to pull configurations from the SMB Share `\\SMBPullServer\Pull`.</span></span>

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
            SourcePath = '\\SMBPullServer\Pull'
        }
    }
}
PullClientConfigID
```

<span data-ttu-id="c00c3-142">A parancsfájl a **ConfigurationRepositoryShare** letiltása a lekéréses kiszolgálón, amely ebben az esetben csak az SMB-megosztás határozza meg.</span><span class="sxs-lookup"><span data-stu-id="c00c3-142">In the script, the **ConfigurationRepositoryShare** block defines the pull server, which in this case, is just an SMB share.</span></span>

## <a name="set-up-a-pull-client-to-download-resources"></a><span data-ttu-id="c00c3-143">Lekérési ügyfél beállítása az erőforrások letöltéséhez</span><span class="sxs-lookup"><span data-stu-id="c00c3-143">Set up a Pull Client to download Resources</span></span>

<span data-ttu-id="c00c3-144">Ha csak adja meg a **ConfigurationRepositoryWeb** vagy **ConfigurationRepositoryShare** letiltása az LCM konfigurálása (a korábbi példákhoz), a lekéréses ügyfél kéri az azonos erőforrásokat a hely lekéri a konfigurációt.</span><span class="sxs-lookup"><span data-stu-id="c00c3-144">If you specify only the **ConfigurationRepositoryWeb** or **ConfigurationRepositoryShare** block in your LCM configuration (as in the previous examples), the pull client will pull resources from the same location it retrieves its configurations.</span></span> <span data-ttu-id="c00c3-145">Megadhat az erőforrások eltérő helyekről is.</span><span class="sxs-lookup"><span data-stu-id="c00c3-145">You can also specify separate locations for resources.</span></span> <span data-ttu-id="c00c3-146">Önálló kiszolgálóként egy erőforrás helyének megadásához használja a **ResourceRepositoryWeb** letiltása.</span><span class="sxs-lookup"><span data-stu-id="c00c3-146">To specify a resource location as a separate server, use the **ResourceRepositoryWeb** block.</span></span> <span data-ttu-id="c00c3-147">Egy erőforrás helye, SMB-megosztáson megadásához használja a **ResourceRepositoryShare** letiltása.</span><span class="sxs-lookup"><span data-stu-id="c00c3-147">To specify a resource location as an SMB share, use the **ResourceRepositoryShare** block.</span></span>

> [!NOTE]
> <span data-ttu-id="c00c3-148">Kombinálhatja **ConfigurationRepositoryWeb** a **ResourceRepositoryShare** vagy **ConfigurationRepositoryShare** a **ResourceRepositoryWeb** .</span><span class="sxs-lookup"><span data-stu-id="c00c3-148">You can combine **ConfigurationRepositoryWeb** with **ResourceRepositoryShare** or **ConfigurationRepositoryShare** with **ResourceRepositoryWeb**.</span></span> <span data-ttu-id="c00c3-149">Erre vonatkozó példákat nem látható az alábbiakban.</span><span class="sxs-lookup"><span data-stu-id="c00c3-149">Examples of this are not shown below.</span></span>

### <a name="http-dsc-pull-server"></a><span data-ttu-id="c00c3-150">HTTP-DSC lekéréses kiszolgálón</span><span class="sxs-lookup"><span data-stu-id="c00c3-150">HTTP DSC Pull Server</span></span>

<span data-ttu-id="c00c3-151">A következő metaconfiguration konfigurálja beolvasni a konfigurációkat a lekérési ügyfél **CONTOSO-PullSrv** és erőforrását **CONTOSO-ResourceSrv**.</span><span class="sxs-lookup"><span data-stu-id="c00c3-151">The following metaconfiguration configures a pull client to get its configurations from **CONTOSO-PullSrv** and its resources from **CONTOSO-ResourceSrv**.</span></span>

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
    }
}
PullClientConfigID
```

### <a name="smb-share"></a><span data-ttu-id="c00c3-152">SMB-megosztás</span><span class="sxs-lookup"><span data-stu-id="c00c3-152">SMB Share</span></span>

<span data-ttu-id="c00c3-153">Az alábbi példa bemutatja, hogy az SMB-megosztás a pull-konfigurációk úgy állít be egy ügyfél egy metaconfiguration `\\SMBPullServer\Configurations`, és erőforrásokat, az SMB-megosztás `\\SMBPullServer\Resources`.</span><span class="sxs-lookup"><span data-stu-id="c00c3-153">The following example shows a metaconfiguration that sets up a client to pull configurations from the SMB share `\\SMBPullServer\Configurations`, and resources from the SMB share `\\SMBPullServer\Resources`.</span></span>

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
            SourcePath = '\\SMBPullServer\Configurations'
        }

        ResourceRepositoryShare SMBResourceServer
        {
            SourcePath = '\\SMBPullServer\Resources'
        }
    }
}
PullClientConfigID
```

#### <a name="automatically-download-resources-in-push-mode"></a><span data-ttu-id="c00c3-154">Automatikus letöltése a leküldési módban erőforrások</span><span class="sxs-lookup"><span data-stu-id="c00c3-154">Automatically download Resources in Push Mode</span></span>

<span data-ttu-id="c00c3-155">A PowerShell 5.0-es verziótól kezdve a pull-ügyfelek is letölthető modulok SMB-megosztáson, akkor is, ha vannak konfigurálva **leküldéses** mód.</span><span class="sxs-lookup"><span data-stu-id="c00c3-155">Beginning in PowerShell 5.0, your pull clients can download modules from an SMB share, even when they are configured for **Push** mode.</span></span> <span data-ttu-id="c00c3-156">Ez különösen hasznos forgatókönyvekben, ahol nem szeretné beállítani egy lekéréses kiszolgálót.</span><span class="sxs-lookup"><span data-stu-id="c00c3-156">This is especially useful in scenarios where you do not want to set up a Pull Server.</span></span> <span data-ttu-id="c00c3-157">A **ResourceRepositoryShare** blokk megadása nélkül is használható egy **ConfigurationRepositoryShare**.</span><span class="sxs-lookup"><span data-stu-id="c00c3-157">The **ResourceRepositoryShare** block can be used without specifying a **ConfigurationRepositoryShare**.</span></span> <span data-ttu-id="c00c3-158">Az alábbi példa bemutatja egy metaconfiguration, amely beállítja egy ügyfél lekéréses erőforrásokhoz az SMB-megosztáson `\\SMBPullServer\Resources`.</span><span class="sxs-lookup"><span data-stu-id="c00c3-158">The following example shows a metaconfiguration that sets up a client to pull resources from an SMB Share `\\SMBPullServer\Resources`.</span></span> <span data-ttu-id="c00c3-159">Amikor a csomópont nem **PUSHED** konfigurációt, azt automatikusan letölti bármilyen szükséges erőforrásokat a a megadott megosztás.</span><span class="sxs-lookup"><span data-stu-id="c00c3-159">When the Node is **PUSHED** a configuration, it will automatically download any required resources, from the share specified.</span></span>

```powershell
[DSCLocalConfigurationManager()]
configuration PullClientConfigID
{
    Node localhost
    {
        Settings
        {
            RefreshMode = 'Push'
            ConfigurationID = '1d545e3b-60c3-47a0-bf65-5afc05182fd0'
        }

        ResourceRepositoryShare SMBResourceServer
        {
            SourcePath = '\\SMBPullServer\Resources'
        }
    }
}
PullClientConfigID
```

## <a name="set-up-a-pull-client-to-report-status"></a><span data-ttu-id="c00c3-160">Állapot jelentése érdekében a lekérési ügyfél beállítása</span><span class="sxs-lookup"><span data-stu-id="c00c3-160">Set up a Pull Client to report status</span></span>

<span data-ttu-id="c00c3-161">Alapértelmezés szerint csomópontok nem küldenek jelentéseket konfigurált lekéréses kiszolgálón.</span><span class="sxs-lookup"><span data-stu-id="c00c3-161">By default, Nodes will not send reports to a configured Pull Server.</span></span> <span data-ttu-id="c00c3-162">Egy lekéréses kiszolgálót használhat a konfigurációk, az erőforrások és a jelentéskészítés, de létre kell hoznia egy **ReportRepositoryWeb** beállítása a jelentéskészítési letiltása.</span><span class="sxs-lookup"><span data-stu-id="c00c3-162">You can use a single pull server for configurations, resources, and reporting, but you have to create a **ReportRepositoryWeb** block to set up reporting.</span></span>

### <a name="http-dsc-pull-server"></a><span data-ttu-id="c00c3-163">HTTP-DSC lekéréses kiszolgálón</span><span class="sxs-lookup"><span data-stu-id="c00c3-163">HTTP DSC Pull Server</span></span>

<span data-ttu-id="c00c3-164">Az alábbi példa bemutatja egy metaconfiguration, amely beállítja a pull-konfigurációkat és erőforrásokat, majd küldje el jelentésadatokat, egyetlen lekéréses kiszolgálóra ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="c00c3-164">The following example shows a metaconfiguration that sets up a client to pull configurations and resources, and send reporting data, to a single pull server.</span></span>

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

<span data-ttu-id="c00c3-165">A jelentéskészítő kiszolgáló megadásához használja a **ReportRepositoryWeb** letiltása.</span><span class="sxs-lookup"><span data-stu-id="c00c3-165">To specify a report server, you use a **ReportRepositoryWeb** block.</span></span> <span data-ttu-id="c00c3-166">A jelentéskészítő kiszolgáló nem lehet SMB-kiszolgálón.</span><span class="sxs-lookup"><span data-stu-id="c00c3-166">A report server cannot be an SMB server.</span></span>
<span data-ttu-id="c00c3-167">A következő metaconfiguration konfigurálja beolvasni a konfigurációkat a lekérési ügyfél **CONTOSO-PullSrv** és erőforrását **CONTOSO-ResourceSrv**, és a jelentések küldéséhez  **CONTOSO-ReportSrv**:</span><span class="sxs-lookup"><span data-stu-id="c00c3-167">The following metaconfiguration configures a pull client to get its configurations from **CONTOSO-PullSrv** and its resources from **CONTOSO-ResourceSrv**, and to send status reports to **CONTOSO-ReportSrv**:</span></span>

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

### <a name="smb-share"></a><span data-ttu-id="c00c3-168">SMB-megosztás</span><span class="sxs-lookup"><span data-stu-id="c00c3-168">SMB Share</span></span>

<span data-ttu-id="c00c3-169">A jelentéskészítő kiszolgáló nem lehet SMB-megosztáson.</span><span class="sxs-lookup"><span data-stu-id="c00c3-169">A report server cannot be an SMB share.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c00c3-170">Következő lépések</span><span class="sxs-lookup"><span data-stu-id="c00c3-170">Next Steps</span></span>

<span data-ttu-id="c00c3-171">A lekérési ügyfél beállítása után a következő útmutatók használatával hajtsa végre a következő lépéseket:</span><span class="sxs-lookup"><span data-stu-id="c00c3-171">Once the pull client has been configured, you can use the following guides to perform the next steps:</span></span>

- [<span data-ttu-id="c00c3-172">Konfigurációk közzétételére egy lekéréses kiszolgálót (v4 vagy v5)</span><span class="sxs-lookup"><span data-stu-id="c00c3-172">Publish Configurations to a Pull Server (v4/v5)</span></span>](publishConfigs.md)
- [<span data-ttu-id="c00c3-173">Csomag és a egy lekéréses kiszolgálót (v4) erőforrás feltöltése</span><span class="sxs-lookup"><span data-stu-id="c00c3-173">Package and Upload Resources to a Pull Server (v4)</span></span>](package-upload-resources.md)

## <a name="see-also"></a><span data-ttu-id="c00c3-174">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="c00c3-174">See Also</span></span>

* [<span data-ttu-id="c00c3-175">A konfigurációs nevek lekérési ügyfél beállítása</span><span class="sxs-lookup"><span data-stu-id="c00c3-175">Setting up a pull client with configuration names</span></span>](pullClientConfigNames.md)
