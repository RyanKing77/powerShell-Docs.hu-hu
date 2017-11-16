---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "Konfigurációs nevek használatával lekéréses ügyfél beállítása"
ms.openlocfilehash: 9bfcac87300d30a59b66e60ed24add32e2420e21
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2017
---
# <a name="setting-up-a-pull-client-using-configuration-names"></a><span data-ttu-id="e5c60-103">Konfigurációs nevek használatával lekéréses ügyfél beállítása</span><span class="sxs-lookup"><span data-stu-id="e5c60-103">Setting up a pull client using configuration names</span></span>

> <span data-ttu-id="e5c60-104">Vonatkozik: A Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="e5c60-104">Applies To: Windows PowerShell 5.0</span></span>

<span data-ttu-id="e5c60-105">Minden egyes célcsomóponttal lekéréses módban a rendszergazda és az URL-címet kap, ahol lépjen kapcsolatba a lekérési kiszolgálójával konfigurációt beolvasandó ki.</span><span class="sxs-lookup"><span data-stu-id="e5c60-105">Each target node has to be told to use pull mode and given the URL where it can contact the pull server to get configurations.</span></span>
<span data-ttu-id="e5c60-106">Ehhez az szükséges, hogy a helyi Configuration Manager (LCM) konfigurálnia a szükséges adatokat.</span><span class="sxs-lookup"><span data-stu-id="e5c60-106">To do this, you have to configure the Local Configuration Manager (LCM) with the necessary information.</span></span>
<span data-ttu-id="e5c60-107">A LCM konfigurálásához hoz létre egy speciális konfigurációs attribútummal. az **DSCLocalConfigurationManager** attribútum.</span><span class="sxs-lookup"><span data-stu-id="e5c60-107">To configure the LCM, you create a special type of configuration, decorated with the **DSCLocalConfigurationManager** attribute.</span></span>
<span data-ttu-id="e5c60-108">A LCM konfigurálásával kapcsolatos további információkért lásd: [konfigurálása a helyi Configuration Manager](metaConfig.md).</span><span class="sxs-lookup"><span data-stu-id="e5c60-108">For more information about configuring the LCM, see [Configuring the Local Configuration Manager](metaConfig.md).</span></span>

> <span data-ttu-id="e5c60-109">**Megjegyzés:**: Ez a témakör PowerShell 5.0 vonatkozik.</span><span class="sxs-lookup"><span data-stu-id="e5c60-109">**Note**: This topic applies to PowerShell 5.0.</span></span>
<span data-ttu-id="e5c60-110">A PowerShell 4.0 lekéréses ügyfél beállításával kapcsolatos információkért lásd: [konfigurációs azonosítójával PowerShell 4.0 lekéréses ügyfél beállítása](pullClientConfigID4.md)</span><span class="sxs-lookup"><span data-stu-id="e5c60-110">For information on setting up a pull client in PowerShell 4.0, see [Setting up a pull client using configuration ID in PowerShell 4.0](pullClientConfigID4.md)</span></span>

<span data-ttu-id="e5c60-111">Az alábbi parancsfájl a LCM konfigurálja az lekéréses konfigurációk "CONTOSO-PullSrv" nevű kiszolgálóról:</span><span class="sxs-lookup"><span data-stu-id="e5c60-111">The following script configures the LCM to pull configurations from a server named "CONTOSO-PullSrv":</span></span>

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

<span data-ttu-id="e5c60-112">A parancsfájl a **ConfigurationRepositoryWeb** blokk határozza meg a lekérési kiszolgálójával.</span><span class="sxs-lookup"><span data-stu-id="e5c60-112">In the script, the **ConfigurationRepositoryWeb** block defines the pull server.</span></span>
<span data-ttu-id="e5c60-113">A **ServerURL** tulajdonság határozza meg a végpont a lekérési kiszolgálón.</span><span class="sxs-lookup"><span data-stu-id="e5c60-113">The **ServerURL** property specifies the endpoint for the pull server.</span></span>

<span data-ttu-id="e5c60-114">A **RegistrationKey** tulajdonsága egy megosztott kulcsot lekéréses kiszolgáló összes ügyfél-csomópontok és az adott lekéréses kiszolgáló között.</span><span class="sxs-lookup"><span data-stu-id="e5c60-114">The **RegistrationKey** property is a shared key between all client nodes for a pull server and that pull server.</span></span>
<span data-ttu-id="e5c60-115">Ugyanazt az értéket a fájl a lekérési kiszolgálón tárolja.</span><span class="sxs-lookup"><span data-stu-id="e5c60-115">The same value is stored in a file on the pull server.</span></span>

<span data-ttu-id="e5c60-116">A **ConfigurationNames** tulajdonsága olyan tömb, amely meghatározza a konfigurációkat, az ügyfél-csomópontnak szánt nevét.</span><span class="sxs-lookup"><span data-stu-id="e5c60-116">The **ConfigurationNames** property is an array that specifies the names of the configurations intended for the client node.</span></span>
<span data-ttu-id="e5c60-117">A lekérési kiszolgálón a konfigurációs MOF-fájlja nevet kell kapniuk az ügyfél-csomópontnak *ConfigurationNames*.mof, ahol *ConfigurationNames* értéke megegyezik a **ConfigurationNames**  a metakonfigurációját az tulajdonsága.</span><span class="sxs-lookup"><span data-stu-id="e5c60-117">On the pull server, the configuration MOF file for this client node must be named *ConfigurationNames*.mof, where *ConfigurationNames* matches the value of the **ConfigurationNames** property you set in this metaconfiguration.</span></span>

><span data-ttu-id="e5c60-118">**Megjegyzés:** Ha egynél több értéket adja meg a **ConfigurationNames**, meg kell adni **PartialConfiguration** blokkolja a konfigurációt.</span><span class="sxs-lookup"><span data-stu-id="e5c60-118">**Note:** If you specify more than one value in the **ConfigurationNames**, you must also specify **PartialConfiguration** blocks in your configuration.</span></span>
<span data-ttu-id="e5c60-119">Részleges konfigurációkkal kapcsolatos információkért lásd: [PowerShell célállapot-konfiguráció részleges konfigurációk](partialConfigs.md).</span><span class="sxs-lookup"><span data-stu-id="e5c60-119">For information about partial configurations, see [PowerShell Desired State Configuration partial configurations](partialConfigs.md).</span></span>

<span data-ttu-id="e5c60-120">A parancsfájl futtatása után a rendszer létrehoz egy új kimeneti mappát **PullClientConfigNames** , és nincs helyezi metakonfigurációját MOF-fájlt.</span><span class="sxs-lookup"><span data-stu-id="e5c60-120">After this script runs, it creates a new output folder named **PullClientConfigNames** and puts a metaconfiguration MOF file there.</span></span>
<span data-ttu-id="e5c60-121">Ebben az esetben a metakonfigurációját MOF-fájl neve lehet `localhost.meta.mof`.</span><span class="sxs-lookup"><span data-stu-id="e5c60-121">In this case, the metaconfiguration MOF file will be named `localhost.meta.mof`.</span></span>

<span data-ttu-id="e5c60-122">A konfiguráció alkalmazásához, hívja meg a **Set-DscLocalConfigurationManager** parancsmag, az a **elérési** beállítása a metakonfigurációját MOF-fájl helyét.</span><span class="sxs-lookup"><span data-stu-id="e5c60-122">To apply the configuration, call the **Set-DscLocalConfigurationManager** cmdlet, with the **Path** set to the location of the metaconfiguration MOF file.</span></span>

```powershell
Set-DSCLocalConfigurationManager localhost –Path .\PullClientConfigNames –Verbose.
```

> <span data-ttu-id="e5c60-123">**Megjegyzés:**: regisztrációs kulcsokat csak lekéréses webkiszolgálók működik.</span><span class="sxs-lookup"><span data-stu-id="e5c60-123">**Note**: Registration keys work only with web pull servers.</span></span>
<span data-ttu-id="e5c60-124">Továbbra is használnia kell **ConfigurationID** az SMB-lekéréses kiszolgálóval.</span><span class="sxs-lookup"><span data-stu-id="e5c60-124">You must still use **ConfigurationID** with an SMB pull server.</span></span>
<span data-ttu-id="e5c60-125">A lekérési kiszolgálójával használatával konfigurálásával kapcsolatos információkat **ConfigurationID**, lásd: [konfigurációs azonosítójával lekéréses ügyfél beállítása](PullClientConfigNames.md)</span><span class="sxs-lookup"><span data-stu-id="e5c60-125">For information about configuring a pull server by using **ConfigurationID**, see [Setting up a pull client using configuration ID](PullClientConfigNames.md)</span></span>

## <a name="resource-and-report-servers"></a><span data-ttu-id="e5c60-126">Erőforrás-és a jelentés</span><span class="sxs-lookup"><span data-stu-id="e5c60-126">Resource and report servers</span></span>

<span data-ttu-id="e5c60-127">Ha csak adja meg a **ConfigurationRepositoryWeb** vagy **ConfigurationRepositoryShare** (ahogy az előző példában) LCM konfigurációs letiltása, a lekéréses ügyfél erőforrásokat fogja lekérni a megadott kiszolgálón, de nem küld jelentéseket rá.</span><span class="sxs-lookup"><span data-stu-id="e5c60-127">If you specify only a **ConfigurationRepositoryWeb** or **ConfigurationRepositoryShare** block in your LCM configuration (as in the previous example), the pull client will pull resources from the specified server, but it will not send reports to it.</span></span>
<span data-ttu-id="e5c60-128">Konfigurációk, erőforrások és jelentéskészítési olyan egyetlen lekéréses kiszolgálót is használhat, de létre kell hoznia egy **ReportRepositoryWeb** blokk jelentéskészítés beállítása.</span><span class="sxs-lookup"><span data-stu-id="e5c60-128">You can use a single pull server for configurations, resources, and reporting, but you have to create a **ReportRepositoryWeb** block to set up reporting.</span></span>
<span data-ttu-id="e5c60-129">A következő példa bemutatja egy metakonfigurációját állítja be az ügyfél lekéréses konfigurációk és az erőforrások és a jelentés adatainak, lekéréses egyetlen kiszolgálóra történő küldés.</span><span class="sxs-lookup"><span data-stu-id="e5c60-129">The following example shows a metaconfiguration that sets up a client to pull configurations and resources, and send reporting data, to a single pull server.</span></span>

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

<span data-ttu-id="e5c60-130">Az erőforrások és a jelentéskészítő különböző lekéréses kiszolgálók is megadható.</span><span class="sxs-lookup"><span data-stu-id="e5c60-130">You can also specify different pull servers for resources and reporting.</span></span>
<span data-ttu-id="e5c60-131">Adjon meg egy erőforrás-kiszolgáló, használhatja a **ResourceRepositoryWeb** (a lekéréses webkiszolgálók) vagy egy **ResourceRepositoryShare** blokk (az SMB-lekérési kiszolgálón).</span><span class="sxs-lookup"><span data-stu-id="e5c60-131">To specify a resource server, you use either a **ResourceRepositoryWeb** (for a web pull server) or a **ResourceRepositoryShare** block (for an SMB pull server).</span></span>
<span data-ttu-id="e5c60-132">Adja meg a jelentéskészítő kiszolgálón, akkor használja a **ReportRepositoryWeb** blokkot.</span><span class="sxs-lookup"><span data-stu-id="e5c60-132">To specify a report server, you use a **ReportRepositoryWeb** block.</span></span>
<span data-ttu-id="e5c60-133">A jelentéskészítő kiszolgáló nem lehet egy SMB-kiszolgálón.</span><span class="sxs-lookup"><span data-stu-id="e5c60-133">A report server cannot be an SMB server.</span></span>
<span data-ttu-id="e5c60-134">A következő metakonfigurációját beállítja a konfigurációk a beolvasandó lekéréses ügyfél **CONTOSO-PullSrv** és erőforrását **CONTOSO-ResourceSrv**, és a jelentések küldése  **CONTOSO-ReportSrv**:</span><span class="sxs-lookup"><span data-stu-id="e5c60-134">The following metaconfiguration configures a pull client to get its configurations from **CONTOSO-PullSrv** and its resources from **CONTOSO-ResourceSrv**, and to send status reports to **CONTOSO-ReportSrv**:</span></span>

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

## <a name="see-also"></a><span data-ttu-id="e5c60-135">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="e5c60-135">See Also</span></span>

* [<span data-ttu-id="e5c60-136">Konfigurációs azonosítójú lekéréses ügyfél beállítása</span><span class="sxs-lookup"><span data-stu-id="e5c60-136">Setting up a pull client with configuration ID</span></span>](PullClientConfigNames.md)
* [<span data-ttu-id="e5c60-137">A DSC lekérési webkiszolgáló beállítása</span><span class="sxs-lookup"><span data-stu-id="e5c60-137">Setting up a DSC web pull server</span></span>](pullServer.md)

