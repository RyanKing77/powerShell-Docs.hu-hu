---
ms.date: 04/11/2018
ms.topic: conceptual
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: DSC Pull Service
ms.openlocfilehash: 61b4c0e9cfe1d1d7539cd32da35d2fe50da4b0e3
ms.sourcegitcommit: ece1794c94be4880a2af5a2605ed4721593643b6
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/16/2018
---
# <a name="desired-state-configuration-pull-service"></a><span data-ttu-id="45435-103">Célállapot-konfiguráló lekéréses szolgáltatása</span><span class="sxs-lookup"><span data-stu-id="45435-103">Desired State Configuration Pull Service</span></span>

> <span data-ttu-id="45435-104">Vonatkozik: A Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="45435-104">Applies To: Windows PowerShell 5.0</span></span>

> [!IMPORTANT]
> <span data-ttu-id="45435-105">A lekéréses kiszolgáló (Windows-szolgáltatás *DSC-szolgáltatás*), Windows Server támogatott összetevője létezik azonban a következők: nem tervezi, hogy új funkciók és képességek kínálnak.</span><span class="sxs-lookup"><span data-stu-id="45435-105">The Pull Server (Windows Feature *DSC-Service*) is a supported component of Windows Server however there are no plans to offer new features or capabilities.</span></span> <span data-ttu-id="45435-106">Javasoljuk, hogy kezdje a Váltás felügyelt ügyfelek [Azure Automation DSC](/azure/automation/automation-dsc-getting-started) (tartalmazza a Windows Server-kiszolgáló lekéréses is) vagy a közösségi megoldásoknak a valamelyikét felsorolt [Itt](pullserver.md#community-solutions-for-pull-service).</span><span class="sxs-lookup"><span data-stu-id="45435-106">It is recommended to begin transitioning managed clients to [Azure Automation DSC](/azure/automation/automation-dsc-getting-started) (includes features beyond Pull Server on Windows Server) or one of the community solutions listed [here](pullserver.md#community-solutions-for-pull-service).</span></span>

<span data-ttu-id="45435-107">Helyi Configuration Manager Service lekéréses megoldás központilag kezelhető.</span><span class="sxs-lookup"><span data-stu-id="45435-107">Local Configuration Manager can be centrally managed by a Pull Service solution.</span></span>
<span data-ttu-id="45435-108">Ez a módszer használata esetén a csomópont kezelt regisztrálva a szolgáltatásban, és LCM beállítások a konfigurációs hozzárendelni.</span><span class="sxs-lookup"><span data-stu-id="45435-108">When using this approach, the node that is being managed is registered with a service and assigned a configuration in LCM settings.</span></span>
<span data-ttu-id="45435-109">A konfiguráció szerint függőségeinek a konfigurációs szükséges összes DSC erőforrásokat a számítógép letölti és LCM felügyelje a konfigurációt használja.</span><span class="sxs-lookup"><span data-stu-id="45435-109">The configuration and all DSC resources needed as dependencies for the configuration are downloaded to the machine and used by LCM to manage the configuration.</span></span>
<span data-ttu-id="45435-110">A felügyelt számítógép állapotára vonatkozó adatokat tölt fel az a jelentéskészítés szolgáltatás.</span><span class="sxs-lookup"><span data-stu-id="45435-110">Information about the state of the machine being managed is uploaded to the service for reporting.</span></span>
<span data-ttu-id="45435-111">Ez a neve "szolgáltatás lekéréses."</span><span class="sxs-lookup"><span data-stu-id="45435-111">This concept is referred to as "pull service."</span></span>

<span data-ttu-id="45435-112">Az aktuális lekéréses szolgáltatás beállításai a következők:</span><span class="sxs-lookup"><span data-stu-id="45435-112">The current options for pull service include:</span></span>

- <span data-ttu-id="45435-113">Azure Automation kívánt állapot konfigurációs szolgáltatás</span><span class="sxs-lookup"><span data-stu-id="45435-113">Azure Automation Desired State Configuration service</span></span>
- <span data-ttu-id="45435-114">Windows Server rendszeren futó lekéréses szolgáltatás</span><span class="sxs-lookup"><span data-stu-id="45435-114">A pull service running on Windows Server</span></span>
- <span data-ttu-id="45435-115">Közösségi nyílt forráskódú megoldások karbantartása</span><span class="sxs-lookup"><span data-stu-id="45435-115">Community maintained open-source solutions</span></span>
- <span data-ttu-id="45435-116">SMB-megosztáson</span><span class="sxs-lookup"><span data-stu-id="45435-116">An SMB share</span></span>

<span data-ttu-id="45435-117">**Az ajánlott megoldás**, és a lehetőség érhető el, a legtöbb szolgáltatásokkal [Azure Automation DSC](/azure/automation/automation-dsc-getting-started).</span><span class="sxs-lookup"><span data-stu-id="45435-117">**The recommended solution**, and the option with the most features available, is [Azure Automation DSC](/azure/automation/automation-dsc-getting-started).</span></span>

<span data-ttu-id="45435-118">Az Azure-szolgáltatás csomópontok helyszíni saját adatközpontját, illetve például az Azure és az AWS nyilvános felhőket is kezelheti.</span><span class="sxs-lookup"><span data-stu-id="45435-118">The Azure service can manage nodes on-premises in private datacenters, or in public clouds such as Azure and AWS.</span></span>
<span data-ttu-id="45435-119">Személyes környezetekben, ahol kiszolgálók nem közvetlenül csatlakozik az internethez, fontolja meg, ezzel a kimenő forgalom csak a közzétett Azure IP-címtartomány (lásd: [Azure Datacenter IP-címtartományok](https://www.microsoft.com/en-us/download/details.aspx?id=41653)).</span><span class="sxs-lookup"><span data-stu-id="45435-119">For private environments where servers cannot directly connect to the Internet, consider limiting outbound traffic to only the published Azure IP range (see [Azure Datacenter IP Ranges](https://www.microsoft.com/en-us/download/details.aspx?id=41653)).</span></span>

<span data-ttu-id="45435-120">Az online szolgáltatás, amely még nem állnak rendelkezésre az lekéréses szolgáltatásban, a Windows Server funkciói:</span><span class="sxs-lookup"><span data-stu-id="45435-120">Features of the online service that are not currently available in the pull service on Windows Server include:</span></span>
- <span data-ttu-id="45435-121">Összes adata titkosításra kerül az átvitel során, és inaktív</span><span class="sxs-lookup"><span data-stu-id="45435-121">All data is encrypted in transit and at rest</span></span>
- <span data-ttu-id="45435-122">Ügyfél-tanúsítványok létrehozása és kezelése automatikusan</span><span class="sxs-lookup"><span data-stu-id="45435-122">Client certificates are created and managed automatically</span></span>
- <span data-ttu-id="45435-123">Titkos kulcsok tárolására központilag kezelésére szolgáló [jelszavak és a hitelesítő adatok](/azure/automation/automation-credentials), vagy [változók](/azure/automation/automation-variables) például a kiszolgáló nevét vagy a kapcsolati karakterláncok</span><span class="sxs-lookup"><span data-stu-id="45435-123">Secrets store for centrally managing [passwords/credentials](/azure/automation/automation-credentials), or [variables](/azure/automation/automation-variables) such as server names or connection strings</span></span>
- <span data-ttu-id="45435-124">Központilag kezelheti a csomópont [LCM konfiguráció](metaConfig.md#basic-settings)</span><span class="sxs-lookup"><span data-stu-id="45435-124">Centrally manage node [LCM configuration](metaConfig.md#basic-settings)</span></span>
- <span data-ttu-id="45435-125">Központilag konfigurációk kiosztása ügyfél csomópontok</span><span class="sxs-lookup"><span data-stu-id="45435-125">Centrally assign configurations to client nodes</span></span>
- <span data-ttu-id="45435-126">Kiadás configuration "Kanári csoportok" éles elérése előtt tesztelési módosításai</span><span class="sxs-lookup"><span data-stu-id="45435-126">Release configuration changes to "canary groups" for testing before reaching production</span></span>
- <span data-ttu-id="45435-127">Grafikus jelentési</span><span class="sxs-lookup"><span data-stu-id="45435-127">Graphical reporting</span></span>
  - <span data-ttu-id="45435-128">A granularitási DSC erőforrás szintjén állapotának részletei</span><span class="sxs-lookup"><span data-stu-id="45435-128">Status detail at the DSC resource level of granularity</span></span>
  - <span data-ttu-id="45435-129">Az ügyfél gépek hibaelhárítási részletes hibaüzenetek</span><span class="sxs-lookup"><span data-stu-id="45435-129">Verbose error messages from client machines for troubleshooting</span></span>
- <span data-ttu-id="45435-130">[Integráció az Azure Naplóelemzés](/azure/automation/automation-dsc-diagnostics) riasztások, automatikus feladatokat, jelentések és riasztási Android vagy iOS-alkalmazás</span><span class="sxs-lookup"><span data-stu-id="45435-130">[Integration with Azure Log Analytics](/azure/automation/automation-dsc-diagnostics) for alerting, automated tasks, Android/iOS app for reporting and alerting</span></span>

## <a name="dsc-pull-service-in-windows-server"></a><span data-ttu-id="45435-131">A DSC lekérési szolgáltatás a Windows Server</span><span class="sxs-lookup"><span data-stu-id="45435-131">DSC pull service in Windows Server</span></span>

<span data-ttu-id="45435-132">Akkor lehet egy lekéréses szolgáltatást, hogy a Windows Serveren futó konfigurálására.</span><span class="sxs-lookup"><span data-stu-id="45435-132">It is possible to configuring a pull service to run on Windows Server.</span></span>
<span data-ttu-id="45435-133">Befolyásolható, hogy a lekéréses service megoldás a Windows Serverben megtalálható tartalmaz-e a konfigurációk/modulok letölthető tárolása, és a jelentés adatokat az rögzítése csak képességeit.</span><span class="sxs-lookup"><span data-stu-id="45435-133">Be advised that the pull service solution included in Windows Server includes only capabilities of storing configurations/modules for download and capturing report data in to database.</span></span>
<span data-ttu-id="45435-134">Nem tartalmazza az Azure-ban a szolgáltatás által kínált képességeket, és ezért nincs értékeléséhez, hogyan szeretné használni a szolgáltatás egy jó eszköz.</span><span class="sxs-lookup"><span data-stu-id="45435-134">It does not include many of the capabilities offered by the service in Azure and so is not a good tool for evaluating how the service would be used.</span></span>

<span data-ttu-id="45435-135">A lekéréses szolgáltatás, a Windows Server egy olyan webes szolgáltatás az IIS-ben elérhetővé DSC konfigurációs fájlokat a célcsomópontokat azokat a csomópontokat, kérje meg őket az OData-illesztőfelület használó.</span><span class="sxs-lookup"><span data-stu-id="45435-135">The pull service offered in Windows Server is a web service in IIS that uses an OData interface to make DSC configuration files available to target nodes when those nodes ask for them.</span></span>

<span data-ttu-id="45435-136">A lekérési kiszolgálójával használatának követelményei:</span><span class="sxs-lookup"><span data-stu-id="45435-136">Requirements for using a pull server:</span></span>

- <span data-ttu-id="45435-137">Futtató kiszolgálón:</span><span class="sxs-lookup"><span data-stu-id="45435-137">A server running:</span></span>
  - <span data-ttu-id="45435-138">WMF/PowerShell 5.0-s vagy újabb</span><span class="sxs-lookup"><span data-stu-id="45435-138">WMF/PowerShell 5.0 or greater</span></span>
  - <span data-ttu-id="45435-139">IIS-kiszolgálói szerepkör</span><span class="sxs-lookup"><span data-stu-id="45435-139">IIS server role</span></span>
  - <span data-ttu-id="45435-140">A DSC szolgáltatás</span><span class="sxs-lookup"><span data-stu-id="45435-140">DSC Service</span></span>
- <span data-ttu-id="45435-141">Ideális esetben egyes azt jelenti, hogy egy tanúsítványgenerálás során, a biztonságos hitelesítő adatok a helyi Configuration Manager (LCM) számára átadott a célcsomópontokat</span><span class="sxs-lookup"><span data-stu-id="45435-141">Ideally, some means of generating a certificate, to secure credentials passed to the Local Configuration Manager (LCM) on target nodes</span></span>

<span data-ttu-id="45435-142">A legjobb konfigurálja a Windows Server a gazdaszolgáltatás lekéréses módja a DSC-konfiguráció.</span><span class="sxs-lookup"><span data-stu-id="45435-142">The best way to configure Windows Server to host pull service is to use a DSC configuration.</span></span>
<span data-ttu-id="45435-143">Példa parancsfájl lejjebb tekinthetők meg.</span><span class="sxs-lookup"><span data-stu-id="45435-143">An example script is provided below.</span></span>

### <a name="supported-database-systems"></a><span data-ttu-id="45435-144">Támogatott adatbázis-rendszerek</span><span class="sxs-lookup"><span data-stu-id="45435-144">Supported database systems</span></span>

|<span data-ttu-id="45435-145">WMF 4.0</span><span class="sxs-lookup"><span data-stu-id="45435-145">WMF 4.0</span></span>   |<span data-ttu-id="45435-146">WMF 5.0</span><span class="sxs-lookup"><span data-stu-id="45435-146">WMF 5.0</span></span>  |<span data-ttu-id="45435-147">WMF 5.1</span><span class="sxs-lookup"><span data-stu-id="45435-147">WMF 5.1</span></span> |<span data-ttu-id="45435-148">WMF 5.1 (a Windows Server Insider Preview 17090)</span><span class="sxs-lookup"><span data-stu-id="45435-148">WMF 5.1 (Windows Server Insider Preview 17090)</span></span>|
|---------|---------|---------|---------|
|<span data-ttu-id="45435-149">MDB</span><span class="sxs-lookup"><span data-stu-id="45435-149">MDB</span></span>     |<span data-ttu-id="45435-150">ESENT (alapértelmezett), Postaláda</span><span class="sxs-lookup"><span data-stu-id="45435-150">ESENT (Default), MDB</span></span> |<span data-ttu-id="45435-151">ESENT (alapértelmezett), Postaláda</span><span class="sxs-lookup"><span data-stu-id="45435-151">ESENT (Default), MDB</span></span>|<span data-ttu-id="45435-152">(Alapértelmezett), az SQL Server MDB ESENT</span><span class="sxs-lookup"><span data-stu-id="45435-152">ESENT (Default), SQL Server, MDB</span></span>

<span data-ttu-id="45435-153">Kezdve a 17090 kiadási [Windows Server Insider Preview](https://www.microsoft.com/en-us/software-download/windowsinsiderpreviewserver), SQL Server támogatott beállítás a lekéréses szolgáltatás (Windows-szolgáltatás *DSC-szolgáltatás*).</span><span class="sxs-lookup"><span data-stu-id="45435-153">Starting in release 17090 of [Windows Server Insider Preview](https://www.microsoft.com/en-us/software-download/windowsinsiderpreviewserver), SQL Server is a supported option for the Pull Service (Windows Feature *DSC-Service*).</span></span>  <span data-ttu-id="45435-154">Ez biztosítja, hogy egy új beállítás nem áttelepített nagy DSC környezetek méretezéshez [Azure Automation DSC](/azure/automation/automation-dsc-getting-started).</span><span class="sxs-lookup"><span data-stu-id="45435-154">This provides a new option for scaling large DSC environments that have not migrated to [Azure Automation DSC](/azure/automation/automation-dsc-getting-started).</span></span>

> <span data-ttu-id="45435-155">**Megjegyzés:**: SQL Server-támogatása nem lesz felvéve a korábbi verziókra WMF 5.1 (vagy korábbi), és csak a Windows Server-verziók kisebb 17090 elérhető lesz.</span><span class="sxs-lookup"><span data-stu-id="45435-155">**Note**: SQL Server support will not be added to previous versions of WMF 5.1 (or earlier) and will only be available on Windows Server versions greater than or equal to 17090.</span></span>

<span data-ttu-id="45435-156">A lekérési kiszolgálójával, hogy az SQL Server használata konfigurálásához állítsa **SqlProvider** való `$true` és **SqlConnectionString** egy érvényes SQL Server kapcsolati karakterlánc módosításait.</span><span class="sxs-lookup"><span data-stu-id="45435-156">To configure the pull server to use SQL Server, set **SqlProvider** to `$true` and **SqlConnectionString** to a valid SQL Server Connection String.</span></span>  <span data-ttu-id="45435-157">További információkért lásd: [SqlClient kapcsolati karakterláncok](/dotnet/framework/data/adonet/connection-string-syntax#sqlclient-connection-strings).</span><span class="sxs-lookup"><span data-stu-id="45435-157">For more information, see [SqlClient Connection Strings](/dotnet/framework/data/adonet/connection-string-syntax#sqlclient-connection-strings).</span></span>
<span data-ttu-id="45435-158">Például egy SQL Server-konfiguráció **xDscWebService**, elolvashatja [xDscWebService erőforrást használó](#using-the-xdscwebservice-resource) és tekintse át a [Sample_xDscWebServiceRegistration_ A Githubon UseSQLProvider.ps1](https://github.com/PowerShell/xPSDesiredStateConfiguration/blob/master/Examples/Sample_xDscWebServiceRegistration_UseSQLProvider.ps1).</span><span class="sxs-lookup"><span data-stu-id="45435-158">For an example of SQL Server configuration with **xDscWebService**, first read [Using the xDscWebService resource](#using-the-xdscwebservice-resource) and then review [Sample_xDscWebServiceRegistration_UseSQLProvider.ps1 on GitHub](https://github.com/PowerShell/xPSDesiredStateConfiguration/blob/master/Examples/Sample_xDscWebServiceRegistration_UseSQLProvider.ps1).</span></span>

### <a name="using-the-xdscwebservice-resource"></a><span data-ttu-id="45435-159">A xDscWebService erőforrás használata</span><span class="sxs-lookup"><span data-stu-id="45435-159">Using the xDscWebService resource</span></span>

<span data-ttu-id="45435-160">A legegyszerűbben úgy állítsa be a webkiszolgáló lekéréses használatára a **xDscWebService** erőforrás szerepel a **xPSDesiredStateConfiguration** modul.</span><span class="sxs-lookup"><span data-stu-id="45435-160">The easiest way to set up a web pull server is to use the **xDscWebService** resource, included in the **xPSDesiredStateConfiguration** module.</span></span>
<span data-ttu-id="45435-161">Az alábbi lépések ismertetik az erőforrás használata, amely beállítja a webszolgáltatás konfigurációban.</span><span class="sxs-lookup"><span data-stu-id="45435-161">The following steps explain how to use the resource in a configuration that sets up the web service.</span></span>

1. <span data-ttu-id="45435-162">Hívja a [Install-modul](/powershell/module/PowershellGet/Install-Module) telepítésére szolgáló parancsmagot a **xPSDesiredStateConfiguration** modul.</span><span class="sxs-lookup"><span data-stu-id="45435-162">Call the [Install-Module](/powershell/module/PowershellGet/Install-Module) cmdlet to install the **xPSDesiredStateConfiguration** module.</span></span> <span data-ttu-id="45435-163">**Megjegyzés:**: **Install-modul** megtalálható a **PowerShellGet** modul, amely PowerShell 5.0 szerepel.</span><span class="sxs-lookup"><span data-stu-id="45435-163">**Note**: **Install-Module** is included in the **PowerShellGet** module, which is included in PowerShell 5.0.</span></span> <span data-ttu-id="45435-164">Letöltheti a **PowerShellGet** modul a PowerShell 3.0 és 4.0-s verzióját, [PackageManagement PowerShell modulok előzetes](https://www.microsoft.com/en-us/download/details.aspx?id=49186).</span><span class="sxs-lookup"><span data-stu-id="45435-164">You can download the **PowerShellGet** module for PowerShell 3.0 and 4.0 at [PackageManagement PowerShell Modules Preview](https://www.microsoft.com/en-us/download/details.aspx?id=49186).</span></span>
1. <span data-ttu-id="45435-165">Az SSL-tanúsítvány lekérése a DSC lekérési kiszolgálójával megbízható hitelesítésszolgáltatótól származó, vagy a szervezet vagy egy nyilvános szolgáltató belül.</span><span class="sxs-lookup"><span data-stu-id="45435-165">Get an SSL certificate for the DSC Pull server from a trusted Certificate Authority, either within your organization or a public authority.</span></span> <span data-ttu-id="45435-166">A szervezet kapott tanúsítvány általában a PFX formátumban van.</span><span class="sxs-lookup"><span data-stu-id="45435-166">The certificate received from the authority is usually in the PFX format.</span></span> <span data-ttu-id="45435-167">Telepítse a tanúsítványt a csomóponton a DSC lekérési kiszolgálójával, hogy CERT: \LocalMachine\My alkalmazandó alapértelmezett helyen lesz.</span><span class="sxs-lookup"><span data-stu-id="45435-167">Install the certificate on the node that will become the DSC Pull server in the default location, which should be CERT:\LocalMachine\My.</span></span> <span data-ttu-id="45435-168">Jegyezze fel a tanúsítvány-ujjlenyomatot.</span><span class="sxs-lookup"><span data-stu-id="45435-168">Make a note of the certificate thumbprint.</span></span>
1. <span data-ttu-id="45435-169">Válassza ki a regisztrációs kulcsot használ egy GUID Azonosítót.</span><span class="sxs-lookup"><span data-stu-id="45435-169">Select a GUID to be used as the Registration Key.</span></span> <span data-ttu-id="45435-170">Hozhat létre egy PowerShell-lel írja be a következő, a PS-parancssorba, és nyomja le az enter: "``` [guid]::newGuid()```"vagy"```New-Guid```".</span><span class="sxs-lookup"><span data-stu-id="45435-170">To generate one using PowerShell enter the following at the PS prompt and press enter: '``` [guid]::newGuid()```' or '```New-Guid```'.</span></span> <span data-ttu-id="45435-171">Ez a kulcs által használandó ügyfél-csomópontok egy megosztott kulcsot, hitelesítéséhez a regisztráció során.</span><span class="sxs-lookup"><span data-stu-id="45435-171">This key will be used by client nodes as a shared key to authenticate during registration.</span></span> <span data-ttu-id="45435-172">További információkért tekintse meg a regisztrációs kulcsot következő szakaszban.</span><span class="sxs-lookup"><span data-stu-id="45435-172">For more information, see the Registration Key section below.</span></span>
1. <span data-ttu-id="45435-173">A PowerShell ISE (F5) a következő konfigurációs parancsfájl futtatásához (például mappájában található a **xPSDesiredStateConfiguration** Sample_xDscWebServiceRegistration.ps1 modul).</span><span class="sxs-lookup"><span data-stu-id="45435-173">In the PowerShell ISE, start (F5) the following configuration script (included in the Examples folder of the  **xPSDesiredStateConfiguration** module as Sample_xDscWebServiceRegistration.ps1).</span></span> <span data-ttu-id="45435-174">Ezt a parancsfájlt hoz létre a lekérési kiszolgálójával.</span><span class="sxs-lookup"><span data-stu-id="45435-174">This script sets up the pull server.</span></span>

```powershell
configuration Sample_xDscWebServiceRegistration
{
    param
    (
        [string[]]$NodeName = 'localhost',

        [ValidateNotNullOrEmpty()]
        [string] $certificateThumbPrint,

        [Parameter(HelpMessage='This should be a string with enough entropy (randomness) to protect the registration of clients to the pull server.  We will use new GUID by default.')]
        [ValidateNotNullOrEmpty()]
        [string] $RegistrationKey   # A guid that clients use to initiate conversation with pull server
    )

    Import-DSCResource -ModuleName xPSDesiredStateConfiguration

    Node $NodeName
    {
        WindowsFeature DSCServiceFeature
        {
            Ensure = "Present"
            Name   = "DSC-Service"
        }

        xDscWebService PSDSCPullServer
        {
            Ensure                  = "Present"
            EndpointName            = "PSDSCPullServer"
            Port                    = 8080
            PhysicalPath            = "$env:SystemDrive\inetpub\PSDSCPullServer"
            CertificateThumbPrint   = $certificateThumbPrint
            ModulePath              = "$env:PROGRAMFILES\WindowsPowerShell\DscService\Modules"
            ConfigurationPath       = "$env:PROGRAMFILES\WindowsPowerShell\DscService\Configuration"
            State                   = "Started"
            DependsOn               = "[WindowsFeature]DSCServiceFeature"
            RegistrationKeyPath     = "$env:PROGRAMFILES\WindowsPowerShell\DscService"
            AcceptSelfSignedCertificates = $true
            Enable32BitAppOnWin64   = $false
        }

        File RegistrationKeyFile
        {
            Ensure          = 'Present'
            Type            = 'File'
            DestinationPath = "$env:ProgramFiles\WindowsPowerShell\DscService\RegistrationKeys.txt"
            Contents        = $RegistrationKey
        }
    }
}
```

1. <span data-ttu-id="45435-175">Futtassa a konfiguráció sikeres, az SSL-tanúsítvány ujjlenyomatát a **certificateThumbPrint** paraméter vagy a GUID-regisztrációs kulcs a **RegistrationKey** paraméter:</span><span class="sxs-lookup"><span data-stu-id="45435-175">Run the configuration, passing the thumbprint of the SSL certificate as the **certificateThumbPrint** parameter and a GUID registration key as the **RegistrationKey** parameter:</span></span>

```powershell
# To find the Thumbprint for an installed SSL certificate for use with the pull server list all certificates in your local store
# and then copy the thumbprint for the appropriate certificate by reviewing the certificate subjects
dir Cert:\LocalMachine\my

# Then include this thumbprint when running the configuration
Sample_xDSCPullServer -certificateThumbprint 'A7000024B753FA6FFF88E966FD6E19301FAE9CCC' -RegistrationKey '140a952b-b9d6-406b-b416-e0f759c9c0e4' -OutputPath c:\Configs\PullServer

# Run the compiled configuration to make the target node a DSC Pull Server
Start-DscConfiguration -Path c:\Configs\PullServer -Wait -Verbose
```

#### <a name="registration-key"></a><span data-ttu-id="45435-176">Regisztrációs kulcs</span><span class="sxs-lookup"><span data-stu-id="45435-176">Registration Key</span></span>

<span data-ttu-id="45435-177">Teszi lehetővé az ügyfélszámítógépek csomópontok regisztrálni a kiszolgálót, hogy használhatnak konfigurációs nevek helyett egy konfigurációs Azonosítót, egy regisztrációs kulcsot, amely a fenti konfigurációban készült nevű fájlba mentése `RegistrationKeys.txt` a `C:\Program Files\WindowsPowerShell\DscService`.</span><span class="sxs-lookup"><span data-stu-id="45435-177">To allow client nodes to register with the server so that they can use configuration names instead of a configuration ID, a registration key that was created by the above configuration is saved in a file named `RegistrationKeys.txt` in `C:\Program Files\WindowsPowerShell\DscService`.</span></span> <span data-ttu-id="45435-178">A regisztrációs kulcs funkciókkal, mint a kezdeti regisztráció során az ügyfél és a lekéréses kiszolgáló által használt megosztott titkos kulcs.</span><span class="sxs-lookup"><span data-stu-id="45435-178">The registration key functions as a shared secret used during the initial registration by the client with the pull server.</span></span> <span data-ttu-id="45435-179">Az ügyfél létrehoz egy önaláírt tanúsítványt, amellyel egyedi módon a kiszolgálón elvégzett hitelesítéshez lekéréses Ha regisztrálása sikeresen befejeződött.</span><span class="sxs-lookup"><span data-stu-id="45435-179">The client will generate a self-signed certificate that is used to uniquely authenticate to the pull server once registration is successfully completed.</span></span> <span data-ttu-id="45435-180">Ez a tanúsítvány ujjlenyomatának helyileg tárolja és társított a lekérési kiszolgálójával URL-CÍMÉT.</span><span class="sxs-lookup"><span data-stu-id="45435-180">The thumbprint of this certificate is stored locally and associated with the URL of the pull server.</span></span>
> <span data-ttu-id="45435-181">**Megjegyzés:**: PowerShell 4.0-s verzióját nem támogatja a regisztrációs kulccsal.</span><span class="sxs-lookup"><span data-stu-id="45435-181">**Note**: Registration keys are not supported in PowerShell 4.0.</span></span>

<span data-ttu-id="45435-182">Ahhoz, hogy egy csomópont a a lekérési kiszolgálón való hitelesítéshez szükséges konfigurálásához a regisztrációs kulcsot kell lennie az összes cél csomóponttal fog a lekérési kiszolgálójával kell regisztrálása metakonfigurációját.</span><span class="sxs-lookup"><span data-stu-id="45435-182">In order to configure a node to authenticate with the pull server, the registration key needs to be in the metaconfiguration for any target node that will be registering with this pull server.</span></span> <span data-ttu-id="45435-183">Vegye figyelembe, hogy a **RegistrationKey** az alábbi metakonfigurációját tartalomkonvertálást követően törlődik a célként megadott gép sikeresen regisztrálta, és hogy a "140a952b-b9d6-406b-b416-e0f759c9c0e4" értékét meg kell egyeznie az értékeket a A lekérési kiszolgálón RegistrationKeys.txt fájlt.</span><span class="sxs-lookup"><span data-stu-id="45435-183">Note that the **RegistrationKey** in the metaconfiguration below is removed after the target machine has successfully registered, and that the value '140a952b-b9d6-406b-b416-e0f759c9c0e4' must match the value stored in the RegistrationKeys.txt file on the pull server.</span></span> <span data-ttu-id="45435-184">A regisztrációs kulcs értékét biztonságosan, mindig kezelni, mert ismerete, hogy lehetővé teszi, hogy a célszámítógép regisztrálni a lekérési kiszolgálójával.</span><span class="sxs-lookup"><span data-stu-id="45435-184">Always treat the registration key value securely, because knowing it allows any target machine to register with the pull server.</span></span>

```powershell
[DSCLocalConfigurationManager()]
configuration Sample_MetaConfigurationToRegisterWithLessSecurePullServer
{
    param
    (
        [ValidateNotNullOrEmpty()]
        [string] $NodeName = 'localhost',

        [ValidateNotNullOrEmpty()]
        [string] $RegistrationKey, #same as the one used to setup pull server in previous configuration

        [ValidateNotNullOrEmpty()]
        [string] $ServerName = 'localhost' #node name of the pull server, same as $NodeName used in previous configuration
    )

    Node $NodeName
    {
        Settings
        {
            RefreshMode        = 'Pull'
        }

        ConfigurationRepositoryWeb CONTOSO-PullSrv
        {
            ServerURL          = "https://$ServerName`:8080/PSDSCPullServer.svc" # notice it is https
            RegistrationKey    = $RegistrationKey
            ConfigurationNames = @('ClientConfig')
        }

        ReportServerWeb CONTOSO-PullSrv
        {
            ServerURL       = "https://$ServerName`:8080/PSDSCPullServer.svc" # notice it is https
            RegistrationKey = $RegistrationKey
        }
    }
}

Sample_MetaConfigurationToRegisterWithLessSecurePullServer -RegistrationKey $RegistrationKey -OutputPath c:\Configs\TargetNodes
```

> <span data-ttu-id="45435-185">**Megjegyzés:**: A **ReportServerWeb** szakasz lehetővé teszi a lekérési kiszolgálójával küldendő jelentésadatait.</span><span class="sxs-lookup"><span data-stu-id="45435-185">**Note**: The **ReportServerWeb** section allows reporting data to be sent to the pull server.</span></span>

<span data-ttu-id="45435-186">A hiánya a **ConfigurationID** tulajdonság a metakonfigurációját fájlban implicit módon azt jelenti, hogy a lekéréses kiszolgáló a V2 verziójú kiszolgáló lekéréses protokollt támogat, egy kezdeti regisztrációs szükség.</span><span class="sxs-lookup"><span data-stu-id="45435-186">The lack of the **ConfigurationID** property in the metaconfiguration file implicitly means that pull server is supporting the V2 version of the pull server protocol so an initial registration is required.</span></span>
<span data-ttu-id="45435-187">Ezzel ellentétben a jelenléte egy **ConfigurationID** azt jelenti, hogy a lekéréses protokoll a V1-es verziót használja, és nincs regisztrálása feldolgozási.</span><span class="sxs-lookup"><span data-stu-id="45435-187">Conversely, the presence of a **ConfigurationID** means that the V1 version of the pull server protocol is used and there is no registration processing.</span></span>

><span data-ttu-id="45435-188">**Megjegyzés:**: a forgatókönyvben a egy LEKÜLDÉSES programhiba van a jelenlegi kiadásban, így meg kell határozni egy ConfigurationID tulajdonság egy lekérési kiszolgálójával soha nem regisztrált csomópontok metakonfigurációját fájlban.</span><span class="sxs-lookup"><span data-stu-id="45435-188">**Note**: In a PUSH scenario, a bug exists in the current release that makes it necessary to define a ConfigurationID property in the metaconfiguration file for nodes that have never registered with a pull server.</span></span> <span data-ttu-id="45435-189">Ezzel a V1 lekéréses protokoll kényszerítése és elkerülése érdekében a regisztrációs hibaüzenetek.</span><span class="sxs-lookup"><span data-stu-id="45435-189">This will force the V1 Pull Server protocol and avoid registration failure messages.</span></span>

## <a name="placing-configurations-and-resources"></a><span data-ttu-id="45435-190">Konfigurációk és erőforrások</span><span class="sxs-lookup"><span data-stu-id="45435-190">Placing configurations and resources</span></span>

<span data-ttu-id="45435-191">Miután a lekéréses server telepítésének befejezése határozzák meg a mappák a **ConfigurationPath** és **ModulePath** tulajdonságok a lekéréses kiszolgáló konfigurációjában: hol helyezi el a modulok és konfigurációk elérhető a célcsomópontokat való lekérésére fogja tárolni.</span><span class="sxs-lookup"><span data-stu-id="45435-191">After the pull server setup completes, the folders defined by the **ConfigurationPath** and **ModulePath** properties in the pull server configuration are where you will place modules and configurations that will be available for target nodes to pull.</span></span>
<span data-ttu-id="45435-192">Ezeket a fájlokat kell lennie ahhoz, hogy a lekérési kiszolgálójával, hogy helyesen dolgozza fel őket egy meghatározott formátumban.</span><span class="sxs-lookup"><span data-stu-id="45435-192">These files need to be in a specific format in order for the pull server to correctly process them.</span></span>

### <a name="dsc-resource-module-package-format"></a><span data-ttu-id="45435-193">A DSC erőforrás modul csomag formátuma</span><span class="sxs-lookup"><span data-stu-id="45435-193">DSC resource module package format</span></span>

<span data-ttu-id="45435-194">Minden erőforrás modul zip és megfelelő a következő mintát kell `{Module Name}_{Module Version}.zip`.</span><span class="sxs-lookup"><span data-stu-id="45435-194">Each resource module needs to be zipped and named according to the following pattern `{Module Name}_{Module Version}.zip`.</span></span>
<span data-ttu-id="45435-195">Például 3.1.2.0 modul verziójával xWebAdminstration nevű modul volna neve "xWebAdministration_3.2.1.0.zip".</span><span class="sxs-lookup"><span data-stu-id="45435-195">For example, a module named xWebAdminstration with a module version of 3.1.2.0 would be named 'xWebAdministration_3.2.1.0.zip'.</span></span>
<span data-ttu-id="45435-196">Egy modul verziói szerepelnie kell egy egyetlen zip-fájlt.</span><span class="sxs-lookup"><span data-stu-id="45435-196">Each version of a module must be contained in a single zip file.</span></span>
<span data-ttu-id="45435-197">Mivel minden egyes zip-fájlban szereplő erőforrás csak egyetlen verziója van telepítve, a WMF 5.0 támogatja a több verziója egyetlen könyvtárban hozzáadott modul formátum nem támogatott.</span><span class="sxs-lookup"><span data-stu-id="45435-197">Since there is only a single version of a resource in each zip file, the module format added in WMF 5.0 with support for multiple module versions in a single directory is not supported.</span></span>
<span data-ttu-id="45435-198">Ez azt jelenti, hogy csomagolási erőforrás modulok DSC lekérési kiszolgálójával való használatra mentése előtt szüksége lesz a könyvtárstruktúra kis módosítja.</span><span class="sxs-lookup"><span data-stu-id="45435-198">This means that before packaging up DSC resource modules for use with pull server you will need to make a small change to the directory structure.</span></span>
<span data-ttu-id="45435-199">Az alapértelmezett DSC erőforrást a WMF 5.0 tartalmazó modulok formátuma "{modul mappa}\{verziója} \DscResources\{DSC Erőforrásmappa}\'.</span><span class="sxs-lookup"><span data-stu-id="45435-199">The default format of modules containing DSC resource in WMF 5.0 is '{Module Folder}\{Module Version}\DscResources\{DSC Resource Folder}\'.</span></span>
<span data-ttu-id="45435-200">Előtt feliratkozott a lekérési kiszolgálójával csomagolása, távolítsa el a **{verziója}** mappában, így az elérési útja bekerül a(z) {modul mappa} \DscResources\{DSC Erőforrásmappa}\'.</span><span class="sxs-lookup"><span data-stu-id="45435-200">Before packaging up for the pull server, remove the **{Module version}** folder so the path becomes '{Module Folder}\DscResources\{DSC Resource Folder}\'.</span></span>
<span data-ttu-id="45435-201">A mappa az módosítását zip-fent leírt módon, és ezek a zip-fájlok a **ModulePath** mappa.</span><span class="sxs-lookup"><span data-stu-id="45435-201">With this change, zip the folder as described above and place these zip files in the **ModulePath** folder.</span></span>

<span data-ttu-id="45435-202">Használjon `New-DscChecksum {module zip file}` az újonnan hozzáadott modul ellenőrzőösszeg-fájl létrehozásához.</span><span class="sxs-lookup"><span data-stu-id="45435-202">Use `New-DscChecksum {module zip file}` to create a checksum file for the newly added module.</span></span>

### <a name="configuration-mof-format"></a><span data-ttu-id="45435-203">Konfigurációs MOF formátuma</span><span class="sxs-lookup"><span data-stu-id="45435-203">Configuration MOF format</span></span>

<span data-ttu-id="45435-204">Konfigurációs MOF-fájlt kell, hogy egy LCM a cél csomópont azt is ellenőrzi a konfigurációt az ellenőrzőösszeg-fájl megfeleltetni.</span><span class="sxs-lookup"><span data-stu-id="45435-204">A configuration MOF file needs to be paired with a checksum file so that an LCM on a target node can validate the configuration.</span></span>
<span data-ttu-id="45435-205">Hozzon létre egy ellenőrzőösszeg, hívja meg a [New-DscChecksum](/powershell/module/PSDesiredStateConfiguration/New-DscChecksum) parancsmag.</span><span class="sxs-lookup"><span data-stu-id="45435-205">To create a checksum, call the [New-DscChecksum](/powershell/module/PSDesiredStateConfiguration/New-DscChecksum) cmdlet.</span></span>
<span data-ttu-id="45435-206">A parancsmag tart egy **elérési** paraméter meghatározza, hogy a mappát, ahol a konfigurációs MOF található.</span><span class="sxs-lookup"><span data-stu-id="45435-206">The cmdlet takes a **Path** parameter that specifies the folder where the configuration MOF is located.</span></span>
<span data-ttu-id="45435-207">A parancsmag létrehoz egy ellenőrzőösszeg nevű `ConfigurationMOFName.mof.checksum`, ahol `ConfigurationMOFName` a konfigurációs mof-fájl neve.</span><span class="sxs-lookup"><span data-stu-id="45435-207">The cmdlet creates a checksum file named `ConfigurationMOFName.mof.checksum`, where `ConfigurationMOFName` is the name of the configuration mof file.</span></span>
<span data-ttu-id="45435-208">Ha egynél több konfigurációs MOF-fájlok a megadott mappában, ellenőrzőösszeg minden konfigurációs a mappában létrejön.</span><span class="sxs-lookup"><span data-stu-id="45435-208">If there are more than one configuration MOF files in the specified folder, a checksum is created for each configuration in the folder.</span></span>
<span data-ttu-id="45435-209">A MOF-fájlok és az azokhoz társított ellenőrzőösszeg fájlokat helyezze a **ConfigurationPath** mappa.</span><span class="sxs-lookup"><span data-stu-id="45435-209">Place the MOF files and their associated checksum files in the **ConfigurationPath** folder.</span></span>

><span data-ttu-id="45435-210">**Megjegyzés:**: Ha megváltoztatja a konfigurációs MOF-fájl bármely olyan módon, az ellenőrzőösszeg-fájl is kell hozni.</span><span class="sxs-lookup"><span data-stu-id="45435-210">**Note**: If you change the configuration MOF file in any way, you must also recreate the checksum file.</span></span>

### <a name="tooling"></a><span data-ttu-id="45435-211">Tooling eszköz</span><span class="sxs-lookup"><span data-stu-id="45435-211">Tooling</span></span>

<span data-ttu-id="45435-212">Annak érdekében, hogy a beállítás, érvényesítése és a könnyebb, lekéréses kiszolgáló felügyelete a következő eszközök érhetők el a legújabb verzió xPSDesiredStateConfiguration modul példaként:</span><span class="sxs-lookup"><span data-stu-id="45435-212">In order to make setting up, validating and managing the pull server easier, the following tools are included as examples in the latest version of the xPSDesiredStateConfiguration module:</span></span>

1. <span data-ttu-id="45435-213">Ez a modul, amely segít csomagolási DSC erőforrás modulok és konfigurációs fájljait a lekérési kiszolgálón.</span><span class="sxs-lookup"><span data-stu-id="45435-213">A module that will help with packaging DSC resource modules and configuration files for use on the pull server.</span></span> <span data-ttu-id="45435-214">[PublishModulesAndMofsToPullServer.psm1](https://github.com/PowerShell/xPSDesiredStateConfiguration/blob/master/DSCPullServerSetup/PublishModulesAndMofsToPullServer.psm1).</span><span class="sxs-lookup"><span data-stu-id="45435-214">[PublishModulesAndMofsToPullServer.psm1](https://github.com/PowerShell/xPSDesiredStateConfiguration/blob/master/DSCPullServerSetup/PublishModulesAndMofsToPullServer.psm1).</span></span> <span data-ttu-id="45435-215">Az alábbi példák:</span><span class="sxs-lookup"><span data-stu-id="45435-215">Examples below:</span></span>

    ```powershell
        # Example 1 - Package all versions of given modules installed locally and MOF files are in c:\LocalDepot
         $moduleList = @('xWebAdministration', 'xPhp')
         Publish-DSCModuleAndMof -Source C:\LocalDepot -ModuleNameList $moduleList

         # Example 2 - Package modules and mof documents from c:\LocalDepot
         Publish-DSCModuleAndMof -Source C:\LocalDepot -Force
    ```

1. <span data-ttu-id="45435-216">Egy parancsfájl, amely ellenőrzi a lekérési kiszolgálójával megfelelően van konfigurálva.</span><span class="sxs-lookup"><span data-stu-id="45435-216">A script that validates the pull server is configured correctly.</span></span> <span data-ttu-id="45435-217">[PullServerSetupTests.ps1](https://github.com/PowerShell/xPSDesiredStateConfiguration/blob/master/DSCPullServerSetup/PullServerDeploymentVerificationTest/PullServerSetupTests.ps1).</span><span class="sxs-lookup"><span data-stu-id="45435-217">[PullServerSetupTests.ps1](https://github.com/PowerShell/xPSDesiredStateConfiguration/blob/master/DSCPullServerSetup/PullServerDeploymentVerificationTest/PullServerSetupTests.ps1).</span></span>

## <a name="community-solutions-for-pull-service"></a><span data-ttu-id="45435-218">Közösségi megoldások lekéréses szolgáltatás</span><span class="sxs-lookup"><span data-stu-id="45435-218">Community Solutions for Pull Service</span></span>

<span data-ttu-id="45435-219">A DSC-Közösség rendelkezik létrehozott több megoldások megvalósításához a lekéréses szolgáltatás protokoll.</span><span class="sxs-lookup"><span data-stu-id="45435-219">The DSC community has authored multiple solutions to implement the pull service protocol.</span></span>
<span data-ttu-id="45435-220">A helyszíni környezetben ezek ajánlatot lekéréses szolgáltatás képességei és hozzájárulnak a Közösség növekményes fejlesztések lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="45435-220">For on-premises environments, these offer pull service capabilities and an opportunity to contribute back to the community with incremental enhancements.</span></span>

- [<span data-ttu-id="45435-221">Vontatóhajó</span><span class="sxs-lookup"><span data-stu-id="45435-221">Tug</span></span>](https://github.com/powershellorg/tug)
- [<span data-ttu-id="45435-222">A DSC-TRÆK</span><span class="sxs-lookup"><span data-stu-id="45435-222">DSC-TRÆK</span></span>](https://github.com/powershellorg/dsc-traek)

## <a name="pull-client-configuration"></a><span data-ttu-id="45435-223">Leküldéses ügyfél-konfiguráció</span><span class="sxs-lookup"><span data-stu-id="45435-223">Pull client configuration</span></span>

<span data-ttu-id="45435-224">A következő témakörök ismertetik részletesen lekéréses ügyfelek beállítása:</span><span class="sxs-lookup"><span data-stu-id="45435-224">The following topics describe setting up pull clients in detail:</span></span>

- [<span data-ttu-id="45435-225">Egy konfigurációs azonosítójával DSC lekérési ügyfél beállítása</span><span class="sxs-lookup"><span data-stu-id="45435-225">Setting up a DSC pull client using a configuration ID</span></span>](pullClientConfigID.md)
- [<span data-ttu-id="45435-226">Konfigurációs nevek használatával DSC lekérési ügyfél beállítása</span><span class="sxs-lookup"><span data-stu-id="45435-226">Setting up a DSC pull client using configuration names</span></span>](pullClientConfigNames.md)
- [<span data-ttu-id="45435-227">Részleges konfigurációk</span><span class="sxs-lookup"><span data-stu-id="45435-227">Partial configurations</span></span>](partialConfigs.md)

## <a name="see-also"></a><span data-ttu-id="45435-228">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="45435-228">See also</span></span>

- [<span data-ttu-id="45435-229">A Windows PowerShell célállapot-konfiguráló áttekintése</span><span class="sxs-lookup"><span data-stu-id="45435-229">Windows PowerShell Desired State Configuration Overview</span></span>](overview.md)
- [<span data-ttu-id="45435-230">Konfigurációk életbe léptetése</span><span class="sxs-lookup"><span data-stu-id="45435-230">Enacting configurations</span></span>](enactingConfigurations.md)
- [<span data-ttu-id="45435-231">A DSC jelentéskészítő kiszolgálójának használata</span><span class="sxs-lookup"><span data-stu-id="45435-231">Using a DSC report server</span></span>](reportServer.md)