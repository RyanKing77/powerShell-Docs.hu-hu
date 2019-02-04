---
ms.date: 12/12/2018
keywords: DSC, powershell, a konfigurációt, a beállítása
title: Konfigurációs azonosítók használata a PowerShell 4.0-s lekérési ügyfél beállítása
ms.openlocfilehash: 9adc767e91ff19d373c122a0d493e7b8703d5476
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55685479"
---
# <a name="set-up-a-pull-client-using-configuration-ids-in-powershell-40"></a><span data-ttu-id="317bc-103">Konfigurációs azonosítók használata a PowerShell 4.0-s lekérési ügyfél beállítása</span><span class="sxs-lookup"><span data-stu-id="317bc-103">Set up a Pull Client using Configuration IDs in PowerShell 4.0</span></span>

><span data-ttu-id="317bc-104">Érvényes: Windows PowerShell 4.0-s, a Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="317bc-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

> [!IMPORTANT]
> <span data-ttu-id="317bc-105">A lekéréses kiszolgálón (Windows-szolgáltatás *DSC-szolgáltatás*), a Windows Server támogatott összetevője létezik azonban tervekben sem funkciókat és képességeket kínálnak.</span><span class="sxs-lookup"><span data-stu-id="317bc-105">The Pull Server (Windows Feature *DSC-Service*) is a supported component of Windows Server however there are no plans to offer new features or capabilities.</span></span> <span data-ttu-id="317bc-106">Javasoljuk, hogy helyeződnek felügyelt ügyfelek [Azure Automation DSC](/azure/automation/automation-dsc-getting-started) (beleértve a lekéréses kiszolgálón a Windows Server csomagban) vagy a közösségi megoldások felsorolt [Itt](pullserver.md#community-solutions-for-pull-service).</span><span class="sxs-lookup"><span data-stu-id="317bc-106">It is recommended to begin transitioning managed clients to [Azure Automation DSC](/azure/automation/automation-dsc-getting-started) (includes features beyond Pull Server on Windows Server) or one of the community solutions listed [here](pullserver.md#community-solutions-for-pull-service).</span></span>

<span data-ttu-id="317bc-107">Lekérési ügyfél beállítása előtt be kell állítania egy lekéréses kiszolgálót.</span><span class="sxs-lookup"><span data-stu-id="317bc-107">Before setting up a pull client, you should set up a pull server.</span></span> <span data-ttu-id="317bc-108">Bár nem kötelező ebben a sorrendben, segít a hibák elhárításában, és így gondoskodik róla, hogy a regisztráció sikeres volt-e.</span><span class="sxs-lookup"><span data-stu-id="317bc-108">Though this order is not required, it helps with troubleshooting, and helps you ensure that the registration was successful.</span></span> <span data-ttu-id="317bc-109">Állítson be egy lekéréses kiszolgálót, használhatja a következő útmutatókat:</span><span class="sxs-lookup"><span data-stu-id="317bc-109">To set up a pull server, you can use the following guides:</span></span>

- [<span data-ttu-id="317bc-110">DSC SMB-lekérési kiszolgáló beállítása</span><span class="sxs-lookup"><span data-stu-id="317bc-110">Set up a DSC SMB Pull Server</span></span>](pullServerSmb.md)
- [<span data-ttu-id="317bc-111">A DSC HTTP-lekérési kiszolgáló beállítása</span><span class="sxs-lookup"><span data-stu-id="317bc-111">Set up a DSC HTTP Pull Server</span></span>](pullServer.md)

<span data-ttu-id="317bc-112">Minden egyes célcsomóponttal konfigurálható töltse le a konfigurációk, az erőforrásokat, és még jelentést annak állapotát.</span><span class="sxs-lookup"><span data-stu-id="317bc-112">Each target node can be configured to download configurations, resources, and even report its status.</span></span> <span data-ttu-id="317bc-113">Az alábbi szakaszok bemutatják, hogyan lekérési ügyfél beállítása egy SMB-megosztáson, vagy a HTTP-DSC lekéréses kiszolgálón.</span><span class="sxs-lookup"><span data-stu-id="317bc-113">The sections below show you how to configure a pull client with an SMB share or HTTP DSC Pull Server.</span></span> <span data-ttu-id="317bc-114">Amikor a csomópont LCM frissíti, a konfigurált helyre, töltse le a hozzárendelt konfigurációkat, felveszi Önnel.</span><span class="sxs-lookup"><span data-stu-id="317bc-114">When the Node's LCM refreshes, it will reach out to the configured location to download any assigned configurations.</span></span> <span data-ttu-id="317bc-115">Ha minden szükséges erőforrás nem létezik a csomóponton, azt automatikusan letöltheti őket a beállított helyről.</span><span class="sxs-lookup"><span data-stu-id="317bc-115">If any required resources do not exist on the Node, it will automatically download them from the configured location.</span></span> <span data-ttu-id="317bc-116">Ha a csomópont konfigurálva van egy [jelentéskészítő kiszolgáló](reportServer.md), majd a művelet állapotát jelzi.</span><span class="sxs-lookup"><span data-stu-id="317bc-116">If the Node is configured with a [Report Server](reportServer.md), it will then report the status of the operation.</span></span>

## <a name="configure-the-pull-client-lcm"></a><span data-ttu-id="317bc-117">Lekérési ügyfél LCM konfigurálása</span><span class="sxs-lookup"><span data-stu-id="317bc-117">Configure the pull client LCM</span></span>

<span data-ttu-id="317bc-118">Az alábbi példák bármelyikét végrehajtása hoz létre egy új nevű kimeneti mappát **PullClientConfigID** , és ott helyezi metaconfiguration MOF-fájlt.</span><span class="sxs-lookup"><span data-stu-id="317bc-118">Executing any of the examples below creates a new output folder named **PullClientConfigID** and puts a metaconfiguration MOF file there.</span></span> <span data-ttu-id="317bc-119">Ebben az esetben a metaconfiguration MOF-fájl neve lesz `localhost.meta.mof`.</span><span class="sxs-lookup"><span data-stu-id="317bc-119">In this case, the metaconfiguration MOF file will be named `localhost.meta.mof`.</span></span>

<span data-ttu-id="317bc-120">A alkalmazni a konfigurációt, hívja meg a **Set-DscLocalConfigurationManager** parancsmag, az a **elérési út** állítsa be a metaconfiguration MOF-fájl helyét.</span><span class="sxs-lookup"><span data-stu-id="317bc-120">To apply the configuration, call the **Set-DscLocalConfigurationManager** cmdlet, with the **Path** set to the location of the metaconfiguration MOF file.</span></span> <span data-ttu-id="317bc-121">Például:</span><span class="sxs-lookup"><span data-stu-id="317bc-121">For example:</span></span>

```powershell
Set-DSCLocalConfigurationManager –ComputerName localhost –Path .\PullClientConfigId –Verbose.
```

## <a name="configuration-id"></a><span data-ttu-id="317bc-122">Konfiguráció azonosítója</span><span class="sxs-lookup"><span data-stu-id="317bc-122">Configuration ID</span></span>

<span data-ttu-id="317bc-123">Set alábbi példák a **ConfigurationID** , az LCM tulajdonságát egy **Guid** , amely korábban létrehozott erre a célra.</span><span class="sxs-lookup"><span data-stu-id="317bc-123">The examples below set the **ConfigurationID** property of the LCM to a **Guid** that had been previously created for this purpose.</span></span> <span data-ttu-id="317bc-124">A **ConfigurationID** van, használja az LCM Konfigurálása a megfelelő konfiguráció keresése a lekérési kiszolgálón.</span><span class="sxs-lookup"><span data-stu-id="317bc-124">The **ConfigurationID** is what the LCM uses to find the appropriate configuration on the pull server.</span></span> <span data-ttu-id="317bc-125">A lekérési kiszolgálón a konfigurációs MOF-fájl neve legyen `ConfigurationID.mof`, ahol *ConfigurationID* értéke a **ConfigurationID** a célcsomópont LCM tulajdonságát.</span><span class="sxs-lookup"><span data-stu-id="317bc-125">The configuration MOF file on the pull server must be named `ConfigurationID.mof`, where *ConfigurationID* is the value of the **ConfigurationID** property of the target node's LCM.</span></span> <span data-ttu-id="317bc-126">További információkért lásd: [konfigurációk közzététele egy lekéréses kiszolgálóra (v4 vagy v5)](publishConfigs.md).</span><span class="sxs-lookup"><span data-stu-id="317bc-126">For more information, see [Publish Configurations to a Pull Server (v4/v5)](publishConfigs.md).</span></span>

<span data-ttu-id="317bc-127">Létrehozhat egy véletlenszerű **Guid** az alábbi példa használatával.</span><span class="sxs-lookup"><span data-stu-id="317bc-127">You can create a random **Guid** using the example below.</span></span>

```powershell
[System.Guid]::NewGuid()
```

## <a name="set-up-a-pull-client-to-download-configurations"></a><span data-ttu-id="317bc-128">Lekérési ügyfél beállítása a konfiguráció letöltése</span><span class="sxs-lookup"><span data-stu-id="317bc-128">Set up a Pull Client to download Configurations</span></span>

<span data-ttu-id="317bc-129">Minden egyes ügyfélnek meg kell adni a **lekéréses** módban, és a pull-kiszolgáló URL-címét a konfigurációja tárolására.</span><span class="sxs-lookup"><span data-stu-id="317bc-129">Each client must be configured in **Pull** mode and given the pull server url where its configuration is stored.</span></span> <span data-ttu-id="317bc-130">Ehhez az szükséges, akkor a helyi Configuration Manager (LCM) konfigurálása a szükséges információkat.</span><span class="sxs-lookup"><span data-stu-id="317bc-130">To do this, you have to configure the Local Configuration Manager (LCM) with the necessary information.</span></span> <span data-ttu-id="317bc-131">Az LCM konfigurálása, a létrehozott konfigurációs, különleges típusú egy **LocalConfigurationManager** letiltása.</span><span class="sxs-lookup"><span data-stu-id="317bc-131">To configure the LCM, you create a special type of configuration, with a **LocalConfigurationManager** block.</span></span> <span data-ttu-id="317bc-132">Az LCM konfigurálása kapcsolatos további információkért lásd: [a Local Configuration Manager](../managing-nodes/metaConfig4.md).</span><span class="sxs-lookup"><span data-stu-id="317bc-132">For more information about configuring the LCM, see [Configuring the Local Configuration Manager](../managing-nodes/metaConfig4.md).</span></span>

## <a name="http-dsc-pull-server"></a><span data-ttu-id="317bc-133">HTTP DSC Pull Server</span><span class="sxs-lookup"><span data-stu-id="317bc-133">HTTP DSC Pull Server</span></span>

<span data-ttu-id="317bc-134">Ha a lekéréses kiszolgálón webszolgáltatásként, amely be van állítva, akkor be a **DownloadManagerName** való **WebDownloadManager**.</span><span class="sxs-lookup"><span data-stu-id="317bc-134">If the pull server is set up as a web service, you set the **DownloadManagerName** to **WebDownloadManager**.</span></span> <span data-ttu-id="317bc-135">A **WebDownloadManager** meg kell adnia egy **ServerUrl** , a **DownloadManagerCustomData** kulcsot.</span><span class="sxs-lookup"><span data-stu-id="317bc-135">The **WebDownloadManager** requires that you specify a **ServerUrl** to the **DownloadManagerCustomData** key.</span></span> <span data-ttu-id="317bc-136">Megadhat egy értéket is **AllowUnsecureConnection**, amint az az alábbi példában.</span><span class="sxs-lookup"><span data-stu-id="317bc-136">You can also specify a value for **AllowUnsecureConnection**, as in the example below.</span></span> <span data-ttu-id="317bc-137">A következő szkriptet az LCM konfigurálja a pull-konfigurációk "PullServer" nevű kiszolgálóról.</span><span class="sxs-lookup"><span data-stu-id="317bc-137">The following script configures the LCM to pull configurations from a server named "PullServer".</span></span>

```powershell
Configuration PullClientConfigId
{
    LocalConfigurationManager
    {
        ConfigurationID = "1C707B86-EF8E-4C29-B7C1-34DA2190AE24";
        RefreshMode = "PULL";
        DownloadManagerName = "WebDownloadManager";
        RebootNodeIfNeeded = $true;
        RefreshFrequencyMins = 30;
        ConfigurationModeFrequencyMins = 30;
        ConfigurationMode = "ApplyAndAutoCorrect";
        DownloadManagerCustomData = @{ServerUrl = "http://PullServer:8080/PSDSCPullServer/PSDSCPullServer.svc"; AllowUnsecureConnection = “TRUE”}
    }
}
PullClientConfigId -Output "."
```

## <a name="smb-share"></a><span data-ttu-id="317bc-138">SMB-megosztás</span><span class="sxs-lookup"><span data-stu-id="317bc-138">SMB Share</span></span>

<span data-ttu-id="317bc-139">Ha a lekérési kiszolgálón be van állítva, az SMB-fájlmegosztás, nem pedig egy webszolgáltatás, állít be a **DownloadManagerName** való **DscFileDownloadManager** helyett a **WebDownLoadManager**.</span><span class="sxs-lookup"><span data-stu-id="317bc-139">If the pull server is set up as an SMB file share, rather than a web service, you set the **DownloadManagerName** to **DscFileDownloadManager** rather than the **WebDownLoadManager**.</span></span> <span data-ttu-id="317bc-140">A **DscFileDownloadManager** meg kell adnia egy **SourcePath** tulajdonságot a **DownloadManagerCustomData**.</span><span class="sxs-lookup"><span data-stu-id="317bc-140">The **DscFileDownloadManager** requires that you specify a **SourcePath** property in the **DownloadManagerCustomData**.</span></span> <span data-ttu-id="317bc-141">A következő szkriptet a kiszolgáló neve "CONTOSO-kiszolgáló" a "SmbDscShare" nevű SMB-megosztáson konfigurációk lekérni az LCM konfigurálása.</span><span class="sxs-lookup"><span data-stu-id="317bc-141">The following script configures the LCM to pull configurations from an SMB share named "SmbDscShare" on a server named "CONTOSO-SERVER".</span></span>

```powershell
Configuration PullClientConfigId
{
    LocalConfigurationManager
    {
        ConfigurationID = "1C707B86-EF8E-4C29-B7C1-34DA2190AE24";
        RefreshMode = "PULL";
        DownloadManagerName = "DscFileDownloadManager";
        RebootNodeIfNeeded = $true;
        RefreshFrequencyMins = 30;
        ConfigurationModeFrequencyMins = 30;
        ConfigurationMode = "ApplyAndAutoCorrect";
        DownloadManagerCustomData = @{ServerUrl = "\\CONTOSO-SERVER\SmbDscShare"}
    }
}
PullClientConfigId -Output "."
```

## <a name="next-steps"></a><span data-ttu-id="317bc-142">Következő lépések</span><span class="sxs-lookup"><span data-stu-id="317bc-142">Next Steps</span></span>

<span data-ttu-id="317bc-143">A lekérési ügyfél beállítása után a következő útmutatók használatával hajtsa végre a következő lépéseket:</span><span class="sxs-lookup"><span data-stu-id="317bc-143">Once the pull client has been configured, you can use the following guides to perform the next steps:</span></span>

- [<span data-ttu-id="317bc-144">Konfigurációk közzétételére egy lekéréses kiszolgálót (v4 vagy v5)</span><span class="sxs-lookup"><span data-stu-id="317bc-144">Publish Configurations to a Pull Server (v4/v5)</span></span>](publishConfigs.md)
- [<span data-ttu-id="317bc-145">Csomag és a egy lekéréses kiszolgálót (v4) erőforrás feltöltése</span><span class="sxs-lookup"><span data-stu-id="317bc-145">Package and Upload Resources to a Pull Server (v4)</span></span>](package-upload-resources.md)

## <a name="see-also"></a><span data-ttu-id="317bc-146">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="317bc-146">See Also</span></span>

- [<span data-ttu-id="317bc-147">DSC lekérési kiszolgáló beállítása</span><span class="sxs-lookup"><span data-stu-id="317bc-147">Set up a DSC web pull server</span></span>](pullServer.md)
- [<span data-ttu-id="317bc-148">A DSC SMB-lekérési kiszolgálójának beállítása</span><span class="sxs-lookup"><span data-stu-id="317bc-148">Set up a DSC SMB pull server</span></span>](pullServerSMB.md)
