---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "Konfigurációs azonosítójával lekéréses ügyfél beállítása"
ms.openlocfilehash: bb14bff95c626b65e2d0d0072c39e4c571cea4b0
ms.sourcegitcommit: a5c0795ca6ec9332967bff9c151a8572feb1a53a
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/27/2017
---
# <a name="setting-up-a-pull-client-using-configuration-id"></a><span data-ttu-id="3940e-103">Konfigurációs azonosítójával lekéréses ügyfél beállítása</span><span class="sxs-lookup"><span data-stu-id="3940e-103">Setting up a pull client using configuration ID</span></span>

> <span data-ttu-id="3940e-104">Vonatkozik: A Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="3940e-104">Applies To: Windows PowerShell 5.0</span></span>

<span data-ttu-id="3940e-105">Minden egyes célcsomóponttal lekéréses módban a rendszergazda és az URL-címet kap, ahol lépjen kapcsolatba a lekérési kiszolgálójával konfigurációt beolvasandó ki.</span><span class="sxs-lookup"><span data-stu-id="3940e-105">Each target node has to be told to use pull mode and given the URL where it can contact the pull server to get configurations.</span></span> <span data-ttu-id="3940e-106">Ehhez az szükséges, hogy a helyi Configuration Manager (LCM) konfigurálnia a szükséges adatokat.</span><span class="sxs-lookup"><span data-stu-id="3940e-106">To do this, you have to configure the Local Configuration Manager (LCM) with the necessary information.</span></span> <span data-ttu-id="3940e-107">A LCM konfigurálásához hoz létre egy speciális konfigurációs attribútummal. az **DSCLocalConfigurationManager** attribútum.</span><span class="sxs-lookup"><span data-stu-id="3940e-107">To configure the LCM, you create a special type of configuration, decorated with the **DSCLocalConfigurationManager** attribute.</span></span> <span data-ttu-id="3940e-108">A LCM konfigurálásával kapcsolatos további információkért lásd: [konfigurálása a helyi Configuration Manager](metaConfig.md).</span><span class="sxs-lookup"><span data-stu-id="3940e-108">For more information about configuring the LCM, see [Configuring the Local Configuration Manager](metaConfig.md).</span></span>

> <span data-ttu-id="3940e-109">**Megjegyzés:**: Ez a témakör PowerShell 5.0 vonatkozik.</span><span class="sxs-lookup"><span data-stu-id="3940e-109">**Note**: This topic applies to PowerShell 5.0.</span></span> <span data-ttu-id="3940e-110">A PowerShell 4.0 lekéréses ügyfél beállításával kapcsolatos információkért lásd: [konfigurációs azonosítójával PowerShell 4.0 lekéréses ügyfél beállítása](pullClientConfigID4.md)</span><span class="sxs-lookup"><span data-stu-id="3940e-110">For information on setting up a pull client in PowerShell 4.0, see [Setting up a pull client using configuration ID in PowerShell 4.0](pullClientConfigID4.md)</span></span>

<span data-ttu-id="3940e-111">A következő parancsfájl úgy konfigurálja a LCM lekéréses konfigurációk "CONTOSO-PullSrv" nevű kiszolgálóról.</span><span class="sxs-lookup"><span data-stu-id="3940e-111">The following script configures the LCM to pull configurations from a server named "CONTOSO-PullSrv".</span></span>

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

<span data-ttu-id="3940e-112">A parancsfájl a **ConfigurationRepositoryWeb** blokk határozza meg a lekérési kiszolgálójával.</span><span class="sxs-lookup"><span data-stu-id="3940e-112">In the script, the **ConfigurationRepositoryWeb** block defines the pull server.</span></span> <span data-ttu-id="3940e-113">A **kiszolgáló URL-címe**</span><span class="sxs-lookup"><span data-stu-id="3940e-113">The **ServerURL**</span></span>

<span data-ttu-id="3940e-114">A parancsfájl futtatása után a rendszer létrehoz egy új kimeneti mappát **PullClientConfigID** , és nincs helyezi metakonfigurációját MOF-fájlt.</span><span class="sxs-lookup"><span data-stu-id="3940e-114">After this script runs, it creates a new output folder named **PullClientConfigID** and puts a metaconfiguration MOF file there.</span></span> <span data-ttu-id="3940e-115">Ebben az esetben a metakonfigurációját MOF-fájl neve lehet `localhost.meta.mof`.</span><span class="sxs-lookup"><span data-stu-id="3940e-115">In this case, the metaconfiguration MOF file will be named `localhost.meta.mof`.</span></span>

<span data-ttu-id="3940e-116">A konfiguráció alkalmazásához, hívja meg a **Set-DscLocalConfigurationManager** parancsmag, az a **elérési** beállítása a metakonfigurációját MOF-fájl helyét.</span><span class="sxs-lookup"><span data-stu-id="3940e-116">To apply the configuration, call the **Set-DscLocalConfigurationManager** cmdlet, with the **Path** set to the location of the metaconfiguration MOF file.</span></span> <span data-ttu-id="3940e-117">Például: `Set-DSCLocalConfigurationManager localhost –Path .\PullClientConfigID –Verbose.`</span><span class="sxs-lookup"><span data-stu-id="3940e-117">For example: `Set-DSCLocalConfigurationManager localhost –Path .\PullClientConfigID –Verbose.`</span></span>

## <a name="configuration-id"></a><span data-ttu-id="3940e-118">Konfiguráció azonosítója</span><span class="sxs-lookup"><span data-stu-id="3940e-118">Configuration ID</span></span>

<span data-ttu-id="3940e-119">A parancsfájl beállítása a **ConfigurationID** korábban erre a célra létrehozott egyedi azonosítóvá LCM tulajdonságának (GUID segítségével létrehozható a **New-Guid** parancsmag).</span><span class="sxs-lookup"><span data-stu-id="3940e-119">The script sets the **ConfigurationID** property of LCM to a GUID that had been previously created for this purpose (you can create a GUID by using the **New-Guid** cmdlet).</span></span> <span data-ttu-id="3940e-120">A **ConfigurationID** van a LCM használja a megfelelő konfigurációja a lekérési kiszolgálón található.</span><span class="sxs-lookup"><span data-stu-id="3940e-120">The **ConfigurationID** is what the LCM uses to find the appropriate configuration on the pull server.</span></span> <span data-ttu-id="3940e-121">A konfigurációs MOF-fájlt a lekérési kiszolgálón névvel kell ellátni _ConfigurationID_.mof, ahol _ConfigurationID_ értéke a **ConfigurationID** a TARGET tulajdonság csomópont LCM.</span><span class="sxs-lookup"><span data-stu-id="3940e-121">The configuration MOF file on the pull server must be named _ConfigurationID_.mof, where _ConfigurationID_ is the value of the **ConfigurationID** property of the target node's LCM.</span></span>

## <a name="smb-pull-server"></a><span data-ttu-id="3940e-122">SMB-lekérési kiszolgálón</span><span class="sxs-lookup"><span data-stu-id="3940e-122">SMB pull server</span></span>

<span data-ttu-id="3940e-123">Állíthat be egy ügyfél lekéréses konfigurációi az SMB-kiszolgálón, használja a **ConfigurationRepositoryShare** blokkot.</span><span class="sxs-lookup"><span data-stu-id="3940e-123">To set up a client to pull configurations from an SMB server, use a **ConfigurationRepositoryShare** block.</span></span> <span data-ttu-id="3940e-124">Az egy **ConfigurationRepositoryShare** blokkot, a kiszolgáló elérési útvonalát úgy, hogy adja meg a **SourcePath** tulajdonság.</span><span class="sxs-lookup"><span data-stu-id="3940e-124">In a **ConfigurationRepositoryShare** block, you specify the path to the server by setting the **SourcePath** property.</span></span> <span data-ttu-id="3940e-125">A következő metakonfigurációját konfigurálja a célcsomóponton való lekérésére egy SMB lekérési kiszolgálójáról nevű **SMBPullServer**.</span><span class="sxs-lookup"><span data-stu-id="3940e-125">The following metaconfiguration configures the target node to pull from an SMB pull server named **SMBPullServer**.</span></span>

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

## <a name="resource-and-report-servers"></a><span data-ttu-id="3940e-126">Erőforrás-és a jelentés</span><span class="sxs-lookup"><span data-stu-id="3940e-126">Resource and report servers</span></span>

<span data-ttu-id="3940e-127">Ha csak adja meg a **ConfigurationRepositoryWeb** vagy **ConfigurationRepositoryShare** (ahogy az előző példában) LCM konfigurációs letiltása, a lekéréses ügyfél erőforrásokat fogja lekérni a megadott kiszolgálón, de nem küld jelentéseket rá.</span><span class="sxs-lookup"><span data-stu-id="3940e-127">If you specify only a **ConfigurationRepositoryWeb** or **ConfigurationRepositoryShare** block in your LCM configuration (as in the previous example), the pull client will pull resources from the specified server, but it will not send reports to it.</span></span> <span data-ttu-id="3940e-128">Konfigurációk, erőforrások és jelentéskészítési olyan egyetlen lekéréses kiszolgálót is használhat, de létre kell hoznia egy **ReportRepositoryWeb** blokk jelentéskészítés beállítása.</span><span class="sxs-lookup"><span data-stu-id="3940e-128">You can use a single pull server for configurations, resources, and reporting, but you have to create a **ReportRepositoryWeb** block to set up reporting.</span></span> 

<span data-ttu-id="3940e-129">A következő példa bemutatja egy metakonfigurációját állítja be az ügyfél lekéréses konfigurációk és az erőforrások és a jelentés adatainak, lekéréses egyetlen kiszolgálóra történő küldés.</span><span class="sxs-lookup"><span data-stu-id="3940e-129">The following example shows a metaconfiguration that sets up a client to pull configurations and resources, and send reporting data, to a single pull server.</span></span>

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

<span data-ttu-id="3940e-130">Az erőforrások és a jelentéskészítő különböző lekéréses kiszolgálók is megadható.</span><span class="sxs-lookup"><span data-stu-id="3940e-130">You can also specify different pull servers for resources and reporting.</span></span> <span data-ttu-id="3940e-131">Adjon meg egy erőforrás-kiszolgáló, használhatja a **ResourceRepositoryWeb** (a lekéréses webkiszolgálók) vagy egy **ResourceRepositoryShare** blokk (az SMB-lekérési kiszolgálón).</span><span class="sxs-lookup"><span data-stu-id="3940e-131">To specify a resource server, you use either a **ResourceRepositoryWeb** (for a web pull server) or a **ResourceRepositoryShare** block (for an SMB pull server).</span></span>
<span data-ttu-id="3940e-132">Adja meg a jelentéskészítő kiszolgálón, akkor használja a **ReportRepositoryWeb** blokkot.</span><span class="sxs-lookup"><span data-stu-id="3940e-132">To specify a report server, you use a **ReportRepositoryWeb** block.</span></span> <span data-ttu-id="3940e-133">A jelentéskészítő kiszolgáló nem lehet egy SMB-kiszolgálón.</span><span class="sxs-lookup"><span data-stu-id="3940e-133">A report server cannot be an SMB server.</span></span>
<span data-ttu-id="3940e-134">A következő metakonfigurációját beállítja a konfigurációk a beolvasandó lekéréses ügyfél **CONTOSO-PullSrv** és erőforrását **CONTOSO-ResourceSrv**, és a jelentések küldése  **CONTOSO-ReportSrv**:</span><span class="sxs-lookup"><span data-stu-id="3940e-134">The following metaconfiguration configures a pull client to get its configurations from **CONTOSO-PullSrv** and its resources from **CONTOSO-ResourceSrv**, and to send status reports to **CONTOSO-ReportSrv**:</span></span>

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

## <a name="see-also"></a><span data-ttu-id="3940e-135">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="3940e-135">See Also</span></span>

* [<span data-ttu-id="3940e-136">Konfigurációs nevek lekéréses ügyfél beállítása</span><span class="sxs-lookup"><span data-stu-id="3940e-136">Setting up a pull client with configuration names</span></span>](pullClientConfigNames.md)

