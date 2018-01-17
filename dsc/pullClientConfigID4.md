---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "A PowerShell 4.0 konfigurációs azonosítójával lekéréses ügyfél beállítása"
ms.openlocfilehash: 2449a4ddfea5c0ee7096ad7478e80166eb095bbe
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 01/17/2018
---
# <a name="setting-up-a-pull-client-using-configuration-id-in-powershell-40"></a><span data-ttu-id="5b6c1-103">A PowerShell 4.0 konfigurációs azonosítójával lekéréses ügyfél beállítása</span><span class="sxs-lookup"><span data-stu-id="5b6c1-103">Setting up a pull client using configuration ID in PowerShell 4.0</span></span>

><span data-ttu-id="5b6c1-104">Vonatkozik: A Windows PowerShell 4.0-s verzióját, a Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="5b6c1-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="5b6c1-105">Minden egyes célcsomóponttal lekéréses módban a rendszergazda és az URL-címet kap, ahol lépjen kapcsolatba a lekérési kiszolgálójával konfigurációt beolvasandó ki.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-105">Each target node has to be told to use pull mode and given the URL where it can contact the pull server to get configurations.</span></span> <span data-ttu-id="5b6c1-106">Ehhez az szükséges, hogy a helyi Configuration Manager (LCM) konfigurálnia a szükséges adatokat.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-106">To do this, you have to configure the Local Configuration Manager (LCM) with the necessary information.</span></span> <span data-ttu-id="5b6c1-107">A LCM konfigurálásához hoz létre egy speciális konfigurációs "metakonfigurációját" néven ismert.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-107">To configure the LCM, you create a special type of configuration known as a "metaconfiguration".</span></span> <span data-ttu-id="5b6c1-108">A LCM konfigurálásával kapcsolatos további információkért lásd: [Windows PowerShell 4.0 kívánt állapot konfigurációs helyi Configuration Manager](metaConfig4.md)</span><span class="sxs-lookup"><span data-stu-id="5b6c1-108">For more information about configuring the LCM, see [Windows PowerShell 4.0 Desired State Configuration Local Configuration Manager](metaConfig4.md)</span></span>

<span data-ttu-id="5b6c1-109">Az alábbi parancsfájl a LCM konfigurálja az lekéréses konfigurációk "PullServer" nevű kiszolgálóról:</span><span class="sxs-lookup"><span data-stu-id="5b6c1-109">The following script configures the LCM to pull configurations from a server named "PullServer":</span></span>

```powershell
Configuration SimpleMetaConfigurationForPull 
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
SimpleMetaConfigurationForPull -Output "."
```

<span data-ttu-id="5b6c1-110">A parancsfájl **DownloadManagerCustomData** cserél az URL-címet a lekérési kiszolgálójával és (ebben a példában), lehetővé teszi egy nem biztonságos kapcsolatot.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-110">In the script, **DownloadManagerCustomData** passes the URL of the pull server and (for this example) allows an unsecured connection.</span></span> 

<span data-ttu-id="5b6c1-111">Ez a parancsfájl futtatása után az új mappát hoz létre kimeneti nevű **SimpleMetaConfigurationForPull** , és nincs helyezi metakonfigurációját MOF-fájlt.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-111">After this script runs, it creates a new output folder called **SimpleMetaConfigurationForPull** and puts a metaconfiguration MOF file there.</span></span>

<span data-ttu-id="5b6c1-112">A konfiguráció segítségével **Set-DscLocalConfigurationManager** a paraméterekkel **számítógépnév** (használja a "localhost") és **elérési** (helyének elérési útvonalát a cél csomópont localhost.meta.mof fájl).</span><span class="sxs-lookup"><span data-stu-id="5b6c1-112">To apply the configuration, use **Set-DscLocalConfigurationManager** with parameters for **ComputerName** (use “localhost”) and **Path** (the path to the location of the target node’s localhost.meta.mof file).</span></span> <span data-ttu-id="5b6c1-113">Például:</span><span class="sxs-lookup"><span data-stu-id="5b6c1-113">For example:</span></span> 
```powershell
Set-DSCLocalConfigurationManager –ComputerName localhost –Path . –Verbose.
```

## <a name="configuration-id"></a><span data-ttu-id="5b6c1-114">Konfiguráció azonosítója</span><span class="sxs-lookup"><span data-stu-id="5b6c1-114">Configuration ID</span></span>
<span data-ttu-id="5b6c1-115">A parancsfájl beállítása a **ConfigurationID** korábban erre a célra létrehozott egyedi azonosítóvá LCM tulajdonságának (GUID segítségével létrehozható a **New-Guid** parancsmag).</span><span class="sxs-lookup"><span data-stu-id="5b6c1-115">The script sets the **ConfigurationID** property of the LCM to a GUID that had been previously created for this purpose (you can create a GUID by using the **New-Guid** cmdlet).</span></span> <span data-ttu-id="5b6c1-116">A **ConfigurationID** van a LCM használja a megfelelő konfigurációja a lekérési kiszolgálón található.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-116">The **ConfigurationID** is what the LCM uses to find the appropriate configuration on the pull server.</span></span> <span data-ttu-id="5b6c1-117">A konfigurációs MOF-fájlt a lekérési kiszolgálón névvel kell ellátni `ConfigurationID.mof`, ahol *ConfigurationID* értéke a **ConfigurationID** a célcsomópont LCM tulajdonsága.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-117">The configuration MOF file on the pull server must be named `ConfigurationID.mof`, where *ConfigurationID* is the value of the **ConfigurationID** property of the target node's LCM.</span></span>

## <a name="pulling-from-an-smb-server"></a><span data-ttu-id="5b6c1-118">Húzza az SMB-kiszolgálón</span><span class="sxs-lookup"><span data-stu-id="5b6c1-118">Pulling from an SMB server</span></span>

<span data-ttu-id="5b6c1-119">Ha a lekérési kiszolgálón be van állítva egy SMB-fájlmegosztás, nem pedig egy webszolgáltatás-bővítmény, megadhatja a **DscFileDownloadManager** helyett a **WebDownLoadManager**.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-119">If the pull server is set up as an SMB file share, rather than a web service, you specify the **DscFileDownloadManager** rather than the **WebDownLoadManager**.</span></span>
<span data-ttu-id="5b6c1-120">A **DscFileDownloadManager** tart egy **SourcePath** tulajdonság helyett **ServerUrl**.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-120">The **DscFileDownloadManager** takes a **SourcePath** property instead of **ServerUrl**.</span></span> <span data-ttu-id="5b6c1-121">A következő parancsfájl való lekérésére konfigurációi az SMB-megosztáson "SmbDscShare" nevű "CONTOSO-kiszolgáló" nevű kiszolgálóra LCM konfigurálja:</span><span class="sxs-lookup"><span data-stu-id="5b6c1-121">The following script configures the LCM to pull configurations from an SMB share named "SmbDscShare" on a server named "CONTOSO-SERVER":</span></span>

```powershell
Configuration SimpleMetaConfigurationForPull 
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
SimpleMetaConfigurationForPull -Output "."
```

## <a name="see-also"></a><span data-ttu-id="5b6c1-122">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="5b6c1-122">See Also</span></span>

- [<span data-ttu-id="5b6c1-123">A DSC lekérési webkiszolgáló beállítása</span><span class="sxs-lookup"><span data-stu-id="5b6c1-123">Setting up a DSC web pull server</span></span>](pullServer.md)
- [<span data-ttu-id="5b6c1-124">A DSC SMB-lekérési kiszolgálójának beállítása</span><span class="sxs-lookup"><span data-stu-id="5b6c1-124">Setting up a DSC SMB pull server</span></span>](pullServerSMB.md)

