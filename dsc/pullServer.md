---
ms.date: 04/11/2018
keywords: DSC, powershell, a konfigurációt, a beállítása
title: DSC Pull Service
ms.openlocfilehash: 2ef48b88cc9e14da452e0d19e5a0f43fc8a95ab2
ms.sourcegitcommit: 91786b03704fbd2d185f674df0bc67faddfb6288
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 11/14/2018
ms.locfileid: "51619160"
---
# <a name="desired-state-configuration-pull-service"></a><span data-ttu-id="8871e-103">Desired State Configuration lekéréses szolgáltatás</span><span class="sxs-lookup"><span data-stu-id="8871e-103">Desired State Configuration Pull Service</span></span>

> <span data-ttu-id="8871e-104">A következőkre vonatkozik: Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="8871e-104">Applies To: Windows PowerShell 5.0</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8871e-105">A lekéréses kiszolgálón (Windows-szolgáltatás *DSC-szolgáltatás*), a Windows Server támogatott összetevője létezik azonban tervekben sem funkciókat és képességeket kínálnak.</span><span class="sxs-lookup"><span data-stu-id="8871e-105">The Pull Server (Windows Feature *DSC-Service*) is a supported component of Windows Server however there are no plans to offer new features or capabilities.</span></span> <span data-ttu-id="8871e-106">Javasoljuk, hogy helyeződnek felügyelt ügyfelek [Azure Automation DSC](/azure/automation/automation-dsc-getting-started) (beleértve a lekéréses kiszolgálón a Windows Server csomagban) vagy a közösségi megoldások felsorolt [Itt](pullserver.md#community-solutions-for-pull-service).</span><span class="sxs-lookup"><span data-stu-id="8871e-106">It is recommended to begin transitioning managed clients to [Azure Automation DSC](/azure/automation/automation-dsc-getting-started) (includes features beyond Pull Server on Windows Server) or one of the community solutions listed [here](pullserver.md#community-solutions-for-pull-service).</span></span>

<span data-ttu-id="8871e-107">Helyi Configuration Manager lekéréses Szolgáltatottszoftver-megoldás központilag kezelhetők.</span><span class="sxs-lookup"><span data-stu-id="8871e-107">Local Configuration Manager can be centrally managed by a Pull Service solution.</span></span>
<span data-ttu-id="8871e-108">Ez a megközelítés használatakor a felügyelt csomópont regisztrálva a szolgáltatásban és konfigurálása során a LCM beállításokat rendelt.</span><span class="sxs-lookup"><span data-stu-id="8871e-108">When using this approach, the node that is being managed is registered with a service and assigned a configuration in LCM settings.</span></span>
<span data-ttu-id="8871e-109">A konfiguráció minden DSC-erőforrások függőségeként a konfigurációhoz szükséges a géphez letöltött és LCM használja a konfiguráció kezelésére.</span><span class="sxs-lookup"><span data-stu-id="8871e-109">The configuration and all DSC resources needed as dependencies for the configuration are downloaded to the machine and used by LCM to manage the configuration.</span></span>
<span data-ttu-id="8871e-110">A felügyelt számítógép állapotát a service for reporting töltenek fel.</span><span class="sxs-lookup"><span data-stu-id="8871e-110">Information about the state of the machine being managed is uploaded to the service for reporting.</span></span>
<span data-ttu-id="8871e-111">A fogalom a neve "lekéréses szolgáltatás."</span><span class="sxs-lookup"><span data-stu-id="8871e-111">This concept is referred to as "pull service."</span></span>

<span data-ttu-id="8871e-112">A lekéréses szolgáltatás jelenlegi lehetőségek a következők:</span><span class="sxs-lookup"><span data-stu-id="8871e-112">The current options for pull service include:</span></span>

- <span data-ttu-id="8871e-113">Azure Automation Desired State Configuration service</span><span class="sxs-lookup"><span data-stu-id="8871e-113">Azure Automation Desired State Configuration service</span></span>
- <span data-ttu-id="8871e-114">Windows Server rendszeren futó lekéréses szolgáltatás</span><span class="sxs-lookup"><span data-stu-id="8871e-114">A pull service running on Windows Server</span></span>
- <span data-ttu-id="8871e-115">Közösségi nyílt forráskódú megoldások karbantartása</span><span class="sxs-lookup"><span data-stu-id="8871e-115">Community maintained open-source solutions</span></span>
- <span data-ttu-id="8871e-116">SMB-megosztáson</span><span class="sxs-lookup"><span data-stu-id="8871e-116">An SMB share</span></span>

<span data-ttu-id="8871e-117">**Az ajánlott megoldás a**, és a lehetőség érhető el, a legtöbb funkciót a [Azure Automation DSC](/azure/automation/automation-dsc-getting-started).</span><span class="sxs-lookup"><span data-stu-id="8871e-117">**The recommended solution**, and the option with the most features available, is [Azure Automation DSC](/azure/automation/automation-dsc-getting-started).</span></span>

<span data-ttu-id="8871e-118">Az Azure-szolgáltatás csomópontjai a helyszíni privát adatközpontok, vagy a nyilvános felhők, például az Azure és az AWS is kezelheti.</span><span class="sxs-lookup"><span data-stu-id="8871e-118">The Azure service can manage nodes on-premises in private datacenters, or in public clouds such as Azure and AWS.</span></span>
<span data-ttu-id="8871e-119">Ahol kiszolgálói nem tudnak közvetlenül kapcsolódni az internetre privát környezetek esetén fontolja meg, csak a közzétett Azure IP-címtartomány irányuló kimenő forgalom korlátozása (lásd: [Azure Datacenter IP-címtartományok](https://www.microsoft.com/en-us/download/details.aspx?id=41653)).</span><span class="sxs-lookup"><span data-stu-id="8871e-119">For private environments where servers cannot directly connect to the Internet, consider limiting outbound traffic to only the published Azure IP range (see [Azure Datacenter IP Ranges](https://www.microsoft.com/en-us/download/details.aspx?id=41653)).</span></span>

<span data-ttu-id="8871e-120">Az online szolgáltatás, amelyek nem a Windows Server, a lekéréses szolgáltatásban jelenleg elérhető funkciók:</span><span class="sxs-lookup"><span data-stu-id="8871e-120">Features of the online service that are not currently available in the pull service on Windows Server include:</span></span>
- <span data-ttu-id="8871e-121">Összes adat titkosítva lesz az úton lévő és inaktív</span><span class="sxs-lookup"><span data-stu-id="8871e-121">All data is encrypted in transit and at rest</span></span>
- <span data-ttu-id="8871e-122">Ügyfél-tanúsítványok létrehozása és felügyelete automatikus</span><span class="sxs-lookup"><span data-stu-id="8871e-122">Client certificates are created and managed automatically</span></span>
- <span data-ttu-id="8871e-123">Titkos kódok tárolása központilag kezelésére szolgáló [jelszavak és a hitelesítő adatok](/azure/automation/automation-credentials), vagy [változók](/azure/automation/automation-variables) például a kiszolgáló nevét vagy a kapcsolati karakterláncok</span><span class="sxs-lookup"><span data-stu-id="8871e-123">Secrets store for centrally managing [passwords/credentials](/azure/automation/automation-credentials), or [variables](/azure/automation/automation-variables) such as server names or connection strings</span></span>
- <span data-ttu-id="8871e-124">Központilag kezelheti a csomópont [LCM konfigurálása](metaConfig.md#basic-settings)</span><span class="sxs-lookup"><span data-stu-id="8871e-124">Centrally manage node [LCM configuration](metaConfig.md#basic-settings)</span></span>
- <span data-ttu-id="8871e-125">Konfigurációk központilag ügyfél-csomópontok hozzárendelése</span><span class="sxs-lookup"><span data-stu-id="8871e-125">Centrally assign configurations to client nodes</span></span>
- <span data-ttu-id="8871e-126">Kiadási konfiguráció módosításait "tesztcsoportos csoportok" tesztelési éles elérése előtt</span><span class="sxs-lookup"><span data-stu-id="8871e-126">Release configuration changes to "canary groups" for testing before reaching production</span></span>
- <span data-ttu-id="8871e-127">Grafikus jelentési</span><span class="sxs-lookup"><span data-stu-id="8871e-127">Graphical reporting</span></span>
  - <span data-ttu-id="8871e-128">A granularitási DSC erőforrás szintjén állapotának részletei</span><span class="sxs-lookup"><span data-stu-id="8871e-128">Status detail at the DSC resource level of granularity</span></span>
  - <span data-ttu-id="8871e-129">Hibaelhárítás az ügyfélgépek a részletes hibaüzenetek</span><span class="sxs-lookup"><span data-stu-id="8871e-129">Verbose error messages from client machines for troubleshooting</span></span>
- <span data-ttu-id="8871e-130">[Integráció az Azure Log Analytics](/azure/automation/automation-dsc-diagnostics) riasztási, automatizált feladatokat, jelentéskészítési és riasztási Android vagy iOS-alkalmazás</span><span class="sxs-lookup"><span data-stu-id="8871e-130">[Integration with Azure Log Analytics](/azure/automation/automation-dsc-diagnostics) for alerting, automated tasks, Android/iOS app for reporting and alerting</span></span>

## <a name="dsc-pull-service-in-windows-server"></a><span data-ttu-id="8871e-131">DSC lekéréses szolgáltatás a Windows Server</span><span class="sxs-lookup"><span data-stu-id="8871e-131">DSC pull service in Windows Server</span></span>

<span data-ttu-id="8871e-132">A Windows Serveren futó lekéréses szolgáltatás konfigurálása lehetőség.</span><span class="sxs-lookup"><span data-stu-id="8871e-132">It is possible to configuring a pull service to run on Windows Server.</span></span>
<span data-ttu-id="8871e-133">Felhasználóitevékenység, hogy az lekéréses szolgáltatás része a Windows Server tartalmaz konfigurációk/modulok letölthető tárolására, és a jelentés adatai az adatbázis csak képességeit.</span><span class="sxs-lookup"><span data-stu-id="8871e-133">Be advised that the pull service solution included in Windows Server includes only capabilities of storing configurations/modules for download and capturing report data in to database.</span></span>
<span data-ttu-id="8871e-134">Nem tartalmazza a képességek a szolgáltatást az Azure által kínált számos, és ezért nem kiértékelését, hogy a szolgáltatás használni kívánt hatékony eszköz.</span><span class="sxs-lookup"><span data-stu-id="8871e-134">It does not include many of the capabilities offered by the service in Azure and so is not a good tool for evaluating how the service would be used.</span></span>

<span data-ttu-id="8871e-135">A lekéréses szolgáltatás, a Windows Server rendszer egy webszolgáltatás, amely egy OData-felületet segítségével DSC konfigurációs fájlok célcsomópontok számára elérhetővé tenni, ha azokat a csomópontokat, kérje meg őket az IIS-ben.</span><span class="sxs-lookup"><span data-stu-id="8871e-135">The pull service offered in Windows Server is a web service in IIS that uses an OData interface to make DSC configuration files available to target nodes when those nodes ask for them.</span></span>

<span data-ttu-id="8871e-136">Egy lekéréses kiszolgálót használatának követelményei:</span><span class="sxs-lookup"><span data-stu-id="8871e-136">Requirements for using a pull server:</span></span>

- <span data-ttu-id="8871e-137">Futtató kiszolgálón:</span><span class="sxs-lookup"><span data-stu-id="8871e-137">A server running:</span></span>
  - <span data-ttu-id="8871e-138">A WMF/PowerShell 5.0-s vagy újabb</span><span class="sxs-lookup"><span data-stu-id="8871e-138">WMF/PowerShell 5.0 or greater</span></span>
  - <span data-ttu-id="8871e-139">IIS-kiszolgálói szerepkör</span><span class="sxs-lookup"><span data-stu-id="8871e-139">IIS server role</span></span>
  - <span data-ttu-id="8871e-140">DSC-szolgáltatás</span><span class="sxs-lookup"><span data-stu-id="8871e-140">DSC Service</span></span>
- <span data-ttu-id="8871e-141">Ideális esetben néhány azt jelenti, hogy egy tanúsítványt létrehozni bloberőforrásokhoz átadott, a helyi Configuration Manager (LCM) Konfigurálása a célcsomópontokat hitelesítő adatok biztonságossá tételéhez</span><span class="sxs-lookup"><span data-stu-id="8871e-141">Ideally, some means of generating a certificate, to secure credentials passed to the Local Configuration Manager (LCM) on target nodes</span></span>

<span data-ttu-id="8871e-142">Windows Server konfigurálása a gazdagépen lekéréses szolgáltatás a legjobb módszer az DSC-konfiguráció használata.</span><span class="sxs-lookup"><span data-stu-id="8871e-142">The best way to configure Windows Server to host pull service is to use a DSC configuration.</span></span>
<span data-ttu-id="8871e-143">Példa parancsfájl lejjebb találja.</span><span class="sxs-lookup"><span data-stu-id="8871e-143">An example script is provided below.</span></span>

### <a name="supported-database-systems"></a><span data-ttu-id="8871e-144">Támogatott adatbázis-rendszerek</span><span class="sxs-lookup"><span data-stu-id="8871e-144">Supported database systems</span></span>

|<span data-ttu-id="8871e-145">WMF 4.0</span><span class="sxs-lookup"><span data-stu-id="8871e-145">WMF 4.0</span></span>   |<span data-ttu-id="8871e-146">WMF 5.0</span><span class="sxs-lookup"><span data-stu-id="8871e-146">WMF 5.0</span></span>  |<span data-ttu-id="8871e-147">WMF 5.1</span><span class="sxs-lookup"><span data-stu-id="8871e-147">WMF 5.1</span></span> |<span data-ttu-id="8871e-148">A WMF 5.1 (Windows Server Insider Preview 17090)</span><span class="sxs-lookup"><span data-stu-id="8871e-148">WMF 5.1 (Windows Server Insider Preview 17090)</span></span>|
|---------|---------|---------|---------|
|<span data-ttu-id="8871e-149">MDB</span><span class="sxs-lookup"><span data-stu-id="8871e-149">MDB</span></span>     |<span data-ttu-id="8871e-150">MDB (alapértelmezett), ESENT</span><span class="sxs-lookup"><span data-stu-id="8871e-150">ESENT (Default), MDB</span></span> |<span data-ttu-id="8871e-151">MDB (alapértelmezett), ESENT</span><span class="sxs-lookup"><span data-stu-id="8871e-151">ESENT (Default), MDB</span></span>|<span data-ttu-id="8871e-152">(Alapértelmezett), SQL Server, MDB ESENT</span><span class="sxs-lookup"><span data-stu-id="8871e-152">ESENT (Default), SQL Server, MDB</span></span>

<span data-ttu-id="8871e-153">Kezdődően az 17090 kiadási [Windows Server Insider Preview](https://www.microsoft.com/en-us/software-download/windowsinsiderpreviewserver), SQL Server támogatott beállítás a lekéréses szolgáltatás a (Windows-szolgáltatás *DSC-szolgáltatás*).</span><span class="sxs-lookup"><span data-stu-id="8871e-153">Starting in release 17090 of [Windows Server Insider Preview](https://www.microsoft.com/en-us/software-download/windowsinsiderpreviewserver), SQL Server is a supported option for the Pull Service (Windows Feature *DSC-Service*).</span></span>  <span data-ttu-id="8871e-154">Ez biztosítja, hogy új lehetőség a skálázás, nagy méretű DSC-környezetekben, amelyek nem áttelepített [Azure Automation DSC](/azure/automation/automation-dsc-getting-started).</span><span class="sxs-lookup"><span data-stu-id="8871e-154">This provides a new option for scaling large DSC environments that have not migrated to [Azure Automation DSC](/azure/automation/automation-dsc-getting-started).</span></span>

> <span data-ttu-id="8871e-155">**Megjegyzés:**: SQL Server-támogatása nem kerül a korábbi verziók a WMF 5.1-es (vagy korábbi), és csak a Windows Server-verziók nagyobb vagy egyenlő 17090 elérhető lesz.</span><span class="sxs-lookup"><span data-stu-id="8871e-155">**Note**: SQL Server support will not be added to previous versions of WMF 5.1 (or earlier) and will only be available on Windows Server versions greater than or equal to 17090.</span></span>

<span data-ttu-id="8871e-156">A lekérési kiszolgálójával, hogy az SQL Server konfigurálásához állítsa **SqlProvider** a `$true` és **SqlConnectionString** a egy érvényes SQL Server kapcsolati karakterláncát.</span><span class="sxs-lookup"><span data-stu-id="8871e-156">To configure the pull server to use SQL Server, set **SqlProvider** to `$true` and **SqlConnectionString** to a valid SQL Server Connection String.</span></span>  <span data-ttu-id="8871e-157">További információkért lásd: [SqlClient kapcsolati karakterláncok](/dotnet/framework/data/adonet/connection-string-syntax#sqlclient-connection-strings).</span><span class="sxs-lookup"><span data-stu-id="8871e-157">For more information, see [SqlClient Connection Strings](/dotnet/framework/data/adonet/connection-string-syntax#sqlclient-connection-strings).</span></span>
<span data-ttu-id="8871e-158">Például egy SQL Server-konfiguráció **xDscWebService**, először olvassa el [xDscWebService erőforrást használó](#using-the-xdscwebservice-resource) , és tekintse át a [Sample_xDscWebServiceRegistration_ A Githubon UseSQLProvider.ps1](https://github.com/PowerShell/xPSDesiredStateConfiguration/blob/master/Examples/Sample_xDscWebServiceRegistration_UseSQLProvider.ps1).</span><span class="sxs-lookup"><span data-stu-id="8871e-158">For an example of SQL Server configuration with **xDscWebService**, first read [Using the xDscWebService resource](#using-the-xdscwebservice-resource) and then review [Sample_xDscWebServiceRegistration_UseSQLProvider.ps1 on GitHub](https://github.com/PowerShell/xPSDesiredStateConfiguration/blob/master/Examples/Sample_xDscWebServiceRegistration_UseSQLProvider.ps1).</span></span>

### <a name="using-the-xdscwebservice-resource"></a><span data-ttu-id="8871e-159">A xDscWebService erőforrás segítségével</span><span class="sxs-lookup"><span data-stu-id="8871e-159">Using the xDscWebService resource</span></span>

<span data-ttu-id="8871e-160">Lekérési kiszolgáló beállítása a legegyszerűbb módja az, hogy használja a **xDscWebService** erőforrás, szerepel a **xPSDesiredStateConfiguration** modul.</span><span class="sxs-lookup"><span data-stu-id="8871e-160">The easiest way to set up a web pull server is to use the **xDscWebService** resource, included in the **xPSDesiredStateConfiguration** module.</span></span>
<span data-ttu-id="8871e-161">A következő lépések azt ismertetik, hogyan használhatja az erőforrást, amely beállítja a web service konfigurációban.</span><span class="sxs-lookup"><span data-stu-id="8871e-161">The following steps explain how to use the resource in a configuration that sets up the web service.</span></span>

1. <span data-ttu-id="8871e-162">Hívja a [Install-Module](/powershell/module/PowershellGet/Install-Module) telepítésére szolgáló parancsmagot a **xPSDesiredStateConfiguration** modul.</span><span class="sxs-lookup"><span data-stu-id="8871e-162">Call the [Install-Module](/powershell/module/PowershellGet/Install-Module) cmdlet to install the **xPSDesiredStateConfiguration** module.</span></span> <span data-ttu-id="8871e-163">**Megjegyzés:**: **Install-Module** szerepel a **PowerShellGet** modult, amely része a PowerShell 5.0-s.</span><span class="sxs-lookup"><span data-stu-id="8871e-163">**Note**: **Install-Module** is included in the **PowerShellGet** module, which is included in PowerShell 5.0.</span></span> <span data-ttu-id="8871e-164">Letöltheti a **PowerShellGet** modul a PowerShell 3.0 és 4.0-s verzióját, [PackageManagement PowerShell modul előzetes](https://www.microsoft.com/en-us/download/details.aspx?id=49186).</span><span class="sxs-lookup"><span data-stu-id="8871e-164">You can download the **PowerShellGet** module for PowerShell 3.0 and 4.0 at [PackageManagement PowerShell Modules Preview](https://www.microsoft.com/en-us/download/details.aspx?id=49186).</span></span>
1. <span data-ttu-id="8871e-165">SSL-tanúsítvány a DSC lekéréses kiszolgálón le egy megbízható hitelesítésszolgáltató, vagy a szervezet vagy egy nyilvános szolgáltató belül.</span><span class="sxs-lookup"><span data-stu-id="8871e-165">Get an SSL certificate for the DSC Pull server from a trusted Certificate Authority, either within your organization or a public authority.</span></span> <span data-ttu-id="8871e-166">A szolgáltató kapott tanúsítvány általában a PFX formátumban van.</span><span class="sxs-lookup"><span data-stu-id="8871e-166">The certificate received from the authority is usually in the PFX format.</span></span> <span data-ttu-id="8871e-167">Telepítse a tanúsítványt, amely a DSC lekéréses kiszolgálón az alapértelmezett helyen, amely lehet a CERT: \LocalMachine\My válnak a csomóponton.</span><span class="sxs-lookup"><span data-stu-id="8871e-167">Install the certificate on the node that will become the DSC Pull server in the default location, which should be CERT:\LocalMachine\My.</span></span> <span data-ttu-id="8871e-168">Jegyezze fel a tanúsítvány-ujjlenyomatot.</span><span class="sxs-lookup"><span data-stu-id="8871e-168">Make a note of the certificate thumbprint.</span></span>
1. <span data-ttu-id="8871e-169">Válassza ki a regisztrációs kulcsát, használható egy GUID Azonosítót.</span><span class="sxs-lookup"><span data-stu-id="8871e-169">Select a GUID to be used as the Registration Key.</span></span> <span data-ttu-id="8871e-170">Hozhat létre egy PowerShell-lel, írja be a következő, a PS-parancssorba, és nyomja le az enter: "``` [guid]::newGuid()```"vagy"```New-Guid```".</span><span class="sxs-lookup"><span data-stu-id="8871e-170">To generate one using PowerShell enter the following at the PS prompt and press enter: '``` [guid]::newGuid()```' or '```New-Guid```'.</span></span> <span data-ttu-id="8871e-171">Ezt a kulcsot a regisztráció során hitelesítsék magukat a megosztott kulcs lesz ügyfél csomópontja.</span><span class="sxs-lookup"><span data-stu-id="8871e-171">This key will be used by client nodes as a shared key to authenticate during registration.</span></span> <span data-ttu-id="8871e-172">További információkért tekintse meg a regisztrációs kulcsot az alábbi szakaszban.</span><span class="sxs-lookup"><span data-stu-id="8871e-172">For more information, see the Registration Key section below.</span></span>
1. <span data-ttu-id="8871e-173">A PowerShell ISE-ben (F5) a következő konfigurációs parancsfájl futtatásához (példák mappájában található a **xPSDesiredStateConfiguration** modul Sample_xDscWebServiceRegistration.ps1 mint).</span><span class="sxs-lookup"><span data-stu-id="8871e-173">In the PowerShell ISE, start (F5) the following configuration script (included in the Examples folder of the  **xPSDesiredStateConfiguration** module as Sample_xDscWebServiceRegistration.ps1).</span></span> <span data-ttu-id="8871e-174">Ez a szkript állítja be a lekéréses kiszolgálón.</span><span class="sxs-lookup"><span data-stu-id="8871e-174">This script sets up the pull server.</span></span>

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

1. <span data-ttu-id="8871e-175">Futtassa a konfigurációt, az SSL-tanúsítvány ujjlenyomata átadása a **certificateThumbPrint** paraméter és a egy GUID regisztrációs kulcsát a **RegistrationKey** paramétert:</span><span class="sxs-lookup"><span data-stu-id="8871e-175">Run the configuration, passing the thumbprint of the SSL certificate as the **certificateThumbPrint** parameter and a GUID registration key as the **RegistrationKey** parameter:</span></span>

    ```powershell
    # To find the Thumbprint for an installed SSL certificate for use with the pull server list all certificates in your local store
    # and then copy the thumbprint for the appropriate certificate by reviewing the certificate subjects
    dir Cert:\LocalMachine\my

    # Then include this thumbprint when running the configuration
    Sample_xDscWebServiceRegistration -certificateThumbprint 'A7000024B753FA6FFF88E966FD6E19301FAE9CCC' -RegistrationKey '140a952b-b9d6-406b-b416-e0f759c9c0e4' -OutputPath c:\Configs\PullServer

    # Run the compiled configuration to make the target node a DSC Pull Server
    Start-DscConfiguration -Path c:\Configs\PullServer -Wait -Verbose
    ```

#### <a name="registration-key"></a><span data-ttu-id="8871e-176">Regisztrációs kulcs</span><span class="sxs-lookup"><span data-stu-id="8871e-176">Registration Key</span></span>

<span data-ttu-id="8871e-177">Ahhoz, hogy az ügyfél-csomópontokat, hogy a konfigurációs nevek helyett egy konfigurációs azonosító használatához regisztrálni a kiszolgálóval, a fenti konfigurációs által létrehozott regisztrációs kulcsát nevű fájlba mentése `RegistrationKeys.txt` a `C:\Program Files\WindowsPowerShell\DscService`.</span><span class="sxs-lookup"><span data-stu-id="8871e-177">To allow client nodes to register with the server so that they can use configuration names instead of a configuration ID, a registration key that was created by the above configuration is saved in a file named `RegistrationKeys.txt` in `C:\Program Files\WindowsPowerShell\DscService`.</span></span> <span data-ttu-id="8871e-178">A regisztrációs kulcs egy közös titkos kulcsot használja a kezdeti regisztráció során az ügyfél és a lekéréses kiszolgálón működik.</span><span class="sxs-lookup"><span data-stu-id="8871e-178">The registration key functions as a shared secret used during the initial registration by the client with the pull server.</span></span> <span data-ttu-id="8871e-179">Az ügyfél, amely után a regisztráció sikeres elvégzése után a lekéréses kiszolgálón egyedi hitelesítésére használt önaláírt tanúsítványt hoz létre.</span><span class="sxs-lookup"><span data-stu-id="8871e-179">The client will generate a self-signed certificate that is used to uniquely authenticate to the pull server once registration is successfully completed.</span></span> <span data-ttu-id="8871e-180">Ez a tanúsítvány ujjlenyomatának helyileg tárolja, és a társított URL-címét a lekéréses kiszolgálón.</span><span class="sxs-lookup"><span data-stu-id="8871e-180">The thumbprint of this certificate is stored locally and associated with the URL of the pull server.</span></span>
> <span data-ttu-id="8871e-181">**Megjegyzés:**: regisztráció kulcsok nem támogatottak a PowerShell 4.0-s verzióját.</span><span class="sxs-lookup"><span data-stu-id="8871e-181">**Note**: Registration keys are not supported in PowerShell 4.0.</span></span>

<span data-ttu-id="8871e-182">Annak érdekében, hogy a pull-kiszolgálóval hitelesíteni csomópontok konfigurálásához, a regisztrációs kulccsal kell lennie az összes cél csomóponttal fog a lekéréses kiszolgálón kell Regisztrálás a metaconfiguration.</span><span class="sxs-lookup"><span data-stu-id="8871e-182">In order to configure a node to authenticate with the pull server, the registration key needs to be in the metaconfiguration for any target node that will be registering with this pull server.</span></span> <span data-ttu-id="8871e-183">Vegye figyelembe, hogy a **RegistrationKey** az alábbi metaconfiguration eltűnik, miután sikeresen regisztrálta a célgépen, és hogy az érték '140a952b-b9d6-406b-b416-e0f759c9c0e4' meg kell egyeznie a tárol a A lekérési kiszolgálón RegistrationKeys.txt fájlt.</span><span class="sxs-lookup"><span data-stu-id="8871e-183">Note that the **RegistrationKey** in the metaconfiguration below is removed after the target machine has successfully registered, and that the value '140a952b-b9d6-406b-b416-e0f759c9c0e4' must match the value stored in the RegistrationKeys.txt file on the pull server.</span></span> <span data-ttu-id="8871e-184">A regisztrációs kulcs értékét biztonságosan, mindig kezeli, mivel azt, hogy lehetővé teszi bármely a célgépen, a lekéréses kiszolgálón regisztrálni.</span><span class="sxs-lookup"><span data-stu-id="8871e-184">Always treat the registration key value securely, because knowing it allows any target machine to register with the pull server.</span></span>

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

> <span data-ttu-id="8871e-185">**Megjegyzés:**: A **ReportServerWeb** szakasz lehetővé teszi, hogy a lekéréses kiszolgálón küldendő adatokról szóló jelentéseket küldeni.</span><span class="sxs-lookup"><span data-stu-id="8871e-185">**Note**: The **ReportServerWeb** section allows reporting data to be sent to the pull server.</span></span>

<span data-ttu-id="8871e-186">Hiánya az **ConfigurationID** tulajdonság a metaconfiguration fájlban implicit módon azt jelenti, hogy a lekéréses kiszolgáló támogat a V2 verziójú lekéréses kiszolgálón protokollt így egy kezdeti regisztrációs megadása kötelező.</span><span class="sxs-lookup"><span data-stu-id="8871e-186">The lack of the **ConfigurationID** property in the metaconfiguration file implicitly means that pull server is supporting the V2 version of the pull server protocol so an initial registration is required.</span></span>
<span data-ttu-id="8871e-187">Ezzel szemben, a jelenléte egy **ConfigurationID** azt jelenti, hogy a lekéréses kiszolgálón protokoll V1 verzióját használja, és nincs a feldolgozás nem regisztrációs.</span><span class="sxs-lookup"><span data-stu-id="8871e-187">Conversely, the presence of a **ConfigurationID** means that the V1 version of the pull server protocol is used and there is no registration processing.</span></span>

><span data-ttu-id="8871e-188">**Megjegyzés:**: a forgatókönyvben a egy LEKÜLDÉSES hibajelentés létezik a jelenlegi kiadásban, amellyel meg kell határozni egy ConfigurationID tulajdonság egy lekéréses kiszolgálót soha nem regisztrált csomópontok metaconfiguration fájlban.</span><span class="sxs-lookup"><span data-stu-id="8871e-188">**Note**: In a PUSH scenario, a bug exists in the current release that makes it necessary to define a ConfigurationID property in the metaconfiguration file for nodes that have never registered with a pull server.</span></span> <span data-ttu-id="8871e-189">Ezzel a V1 lekéréses kiszolgálón protokoll kényszerítése és regisztrációs hibaüzenetek elkerülése érdekében.</span><span class="sxs-lookup"><span data-stu-id="8871e-189">This will force the V1 Pull Server protocol and avoid registration failure messages.</span></span>

## <a name="placing-configurations-and-resources"></a><span data-ttu-id="8871e-190">Konfigurációkat és erőforrásokat elhelyezése</span><span class="sxs-lookup"><span data-stu-id="8871e-190">Placing configurations and resources</span></span>

<span data-ttu-id="8871e-191">Miután a lekéréses server telepítésének befejezése határozzák meg a mappák a **ConfigurationPath** és **ModulePath** a pull-kiszolgálói konfigurációban a tulajdonságok akkor, hogy hol helyezi el a modulok és konfigurációk amely lekéréses cél csomópontok elérhető lesz.</span><span class="sxs-lookup"><span data-stu-id="8871e-191">After the pull server setup completes, the folders defined by the **ConfigurationPath** and **ModulePath** properties in the pull server configuration are where you will place modules and configurations that will be available for target nodes to pull.</span></span>
<span data-ttu-id="8871e-192">Ezeket a fájlokat kell lennie ahhoz, hogy a pull-kiszolgáló megfelelően feldolgozza őket egy meghatározott formátumban.</span><span class="sxs-lookup"><span data-stu-id="8871e-192">These files need to be in a specific format in order for the pull server to correctly process them.</span></span>

### <a name="dsc-resource-module-package-format"></a><span data-ttu-id="8871e-193">DSC erőforrás modul csomag formátuma</span><span class="sxs-lookup"><span data-stu-id="8871e-193">DSC resource module package format</span></span>

<span data-ttu-id="8871e-194">Minden egyes erőforrás modulnak kell zip és a következő mintának megfelelően nevű `{Module Name}_{Module Version}.zip`.</span><span class="sxs-lookup"><span data-stu-id="8871e-194">Each resource module needs to be zipped and named according to the following pattern `{Module Name}_{Module Version}.zip`.</span></span>
<span data-ttu-id="8871e-195">Ha például 3.1.2.0 modul verziójával xWebAdminstration modul neve "xWebAdministration_3.2.1.0.zip".</span><span class="sxs-lookup"><span data-stu-id="8871e-195">For example, a module named xWebAdminstration with a module version of 3.1.2.0 would be named 'xWebAdministration_3.2.1.0.zip'.</span></span>
<span data-ttu-id="8871e-196">Minden egyes modul verzióját tartalmaznia kell egy egyetlen zip-fájlt.</span><span class="sxs-lookup"><span data-stu-id="8871e-196">Each version of a module must be contained in a single zip file.</span></span>
<span data-ttu-id="8871e-197">Mivel minden egyes zip-fájlt az erőforráshoz csak egyetlen verziója, a WMF 5.0-s egyetlen címtárban több modul verzió támogatása hozzáadva a modul formátum nem támogatott.</span><span class="sxs-lookup"><span data-stu-id="8871e-197">Since there is only a single version of a resource in each zip file, the module format added in WMF 5.0 with support for multiple module versions in a single directory is not supported.</span></span>
<span data-ttu-id="8871e-198">Ez azt jelenti, hogy becsomagolást mentése erőforrás modulok DSC lekéréses kiszolgálón való használatra előtt ki kell, hogy módosítsa a könyvtár struktúra.</span><span class="sxs-lookup"><span data-stu-id="8871e-198">This means that before packaging up DSC resource modules for use with pull server you will need to make a small change to the directory structure.</span></span>
<span data-ttu-id="8871e-199">Az alapértelmezett formátum a modulok DSC-erőforrás a WMF 5.0 tartalmazó "{modul mappáját}\{Modulverzió} \DscResources\{DSC Erőforrásmappa}\'.</span><span class="sxs-lookup"><span data-stu-id="8871e-199">The default format of modules containing DSC resource in WMF 5.0 is '{Module Folder}\{Module Version}\DscResources\{DSC Resource Folder}\'.</span></span>
<span data-ttu-id="8871e-200">Terveztük a lekérési kiszolgálón csomagolást, előtt távolítsa el a **{modul version}** mappát az elérési út válik, így a(z) {modul mappáját} \DscResources\{DSC Erőforrásmappa}\'.</span><span class="sxs-lookup"><span data-stu-id="8871e-200">Before packaging up for the pull server, remove the **{Module version}** folder so the path becomes '{Module Folder}\DscResources\{DSC Resource Folder}\'.</span></span>
<span data-ttu-id="8871e-201">A mappa az módosítása zip-fent leírtak szerint, és helyezze ezeket a zip-fájlokat a **ModulePath** mappát.</span><span class="sxs-lookup"><span data-stu-id="8871e-201">With this change, zip the folder as described above and place these zip files in the **ModulePath** folder.</span></span>

<span data-ttu-id="8871e-202">Használat `New-DscChecksum {module zip file}` az újonnan hozzáadott modul ellenőrzőösszeg fájl létrehozásához.</span><span class="sxs-lookup"><span data-stu-id="8871e-202">Use `New-DscChecksum {module zip file}` to create a checksum file for the newly added module.</span></span>

### <a name="configuration-mof-format"></a><span data-ttu-id="8871e-203">Konfigurációs MOF-formátuma</span><span class="sxs-lookup"><span data-stu-id="8871e-203">Configuration MOF format</span></span>

<span data-ttu-id="8871e-204">A konfigurációs MOF-fájlt kell ellenőrzőösszeg fájl párosítani, hogy a cél csomópont egy LCM ellenőrizheti a konfigurációt.</span><span class="sxs-lookup"><span data-stu-id="8871e-204">A configuration MOF file needs to be paired with a checksum file so that an LCM on a target node can validate the configuration.</span></span>
<span data-ttu-id="8871e-205">Ellenőrzőösszeg létrehozásához hívja a [New-DscChecksum](/powershell/module/PSDesiredStateConfiguration/New-DscChecksum) parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="8871e-205">To create a checksum, call the [New-DscChecksum](/powershell/module/PSDesiredStateConfiguration/New-DscChecksum) cmdlet.</span></span>
<span data-ttu-id="8871e-206">A parancsmag lép egy **elérési út** paraméter, amely a mappát, ahol a konfigurációs MOF található.</span><span class="sxs-lookup"><span data-stu-id="8871e-206">The cmdlet takes a **Path** parameter that specifies the folder where the configuration MOF is located.</span></span>
<span data-ttu-id="8871e-207">A parancsmag létrehoz egy ellenőrzőösszeg-fájlt `ConfigurationMOFName.mof.checksum`, ahol `ConfigurationMOFName` a konfigurációs mof-fájl neve.</span><span class="sxs-lookup"><span data-stu-id="8871e-207">The cmdlet creates a checksum file named `ConfigurationMOFName.mof.checksum`, where `ConfigurationMOFName` is the name of the configuration mof file.</span></span>
<span data-ttu-id="8871e-208">Ha egynél több konfigurációs MOF-fájlok a megadott mappában, a mappában az egyes konfigurációkhoz egy ellenőrzőösszeg jön létre.</span><span class="sxs-lookup"><span data-stu-id="8871e-208">If there are more than one configuration MOF files in the specified folder, a checksum is created for each configuration in the folder.</span></span>
<span data-ttu-id="8871e-209">A MOF-fájlok és az azokhoz társított ellenőrzőösszeg fájlokat helyezze a **ConfigurationPath** mappát.</span><span class="sxs-lookup"><span data-stu-id="8871e-209">Place the MOF files and their associated checksum files in the **ConfigurationPath** folder.</span></span>

><span data-ttu-id="8871e-210">**Megjegyzés:**: Ha módosítja a konfigurációs MOF-fájl bármilyen módon, akkor is hozza létre az ellenőrzőösszeg-fájl.</span><span class="sxs-lookup"><span data-stu-id="8871e-210">**Note**: If you change the configuration MOF file in any way, you must also recreate the checksum file.</span></span>

### <a name="tooling"></a><span data-ttu-id="8871e-211">Eszköztámogatás</span><span class="sxs-lookup"><span data-stu-id="8871e-211">Tooling</span></span>

<span data-ttu-id="8871e-212">Annak érdekében, hogy a beállítás alkotják, ellenőrzése és felügyelete egyszerűbb, a lekéréses kiszolgálón a következő eszközöket is a xPSDesiredStateConfiguration modul legújabb verziója található példák:</span><span class="sxs-lookup"><span data-stu-id="8871e-212">In order to make setting up, validating and managing the pull server easier, the following tools are included as examples in the latest version of the xPSDesiredStateConfiguration module:</span></span>

1. <span data-ttu-id="8871e-213">A modul, amely segít a csomagolási DSC erőforrás modulok és konfigurációs fájljait használja a lekérési kiszolgálón.</span><span class="sxs-lookup"><span data-stu-id="8871e-213">A module that will help with packaging DSC resource modules and configuration files for use on the pull server.</span></span> <span data-ttu-id="8871e-214">[PublishModulesAndMofsToPullServer.psm1](https://github.com/PowerShell/xPSDesiredStateConfiguration/blob/master/DSCPullServerSetup/PublishModulesAndMofsToPullServer.psm1).</span><span class="sxs-lookup"><span data-stu-id="8871e-214">[PublishModulesAndMofsToPullServer.psm1](https://github.com/PowerShell/xPSDesiredStateConfiguration/blob/master/DSCPullServerSetup/PublishModulesAndMofsToPullServer.psm1).</span></span> <span data-ttu-id="8871e-215">Az alábbi példákat:</span><span class="sxs-lookup"><span data-stu-id="8871e-215">Examples below:</span></span>

    ```powershell
        # Example 1 - Package all versions of given modules installed locally and MOF files are in c:\LocalDepot
         $moduleList = @('xWebAdministration', 'xPhp')
         Publish-DSCModuleAndMof -Source C:\LocalDepot -ModuleNameList $moduleList

         # Example 2 - Package modules and mof documents from c:\LocalDepot
         Publish-DSCModuleAndMof -Source C:\LocalDepot -Force
    ```

1. <span data-ttu-id="8871e-216">A parancsfájl, amely ellenőrzi a lekérési kiszolgálón megfelelően van konfigurálva.</span><span class="sxs-lookup"><span data-stu-id="8871e-216">A script that validates the pull server is configured correctly.</span></span> <span data-ttu-id="8871e-217">[PullServerSetupTests.ps1](https://github.com/PowerShell/xPSDesiredStateConfiguration/blob/master/DSCPullServerSetup/PullServerDeploymentVerificationTest/PullServerSetupTests.ps1).</span><span class="sxs-lookup"><span data-stu-id="8871e-217">[PullServerSetupTests.ps1](https://github.com/PowerShell/xPSDesiredStateConfiguration/blob/master/DSCPullServerSetup/PullServerDeploymentVerificationTest/PullServerSetupTests.ps1).</span></span>

## <a name="community-solutions-for-pull-service"></a><span data-ttu-id="8871e-218">Közösségi megoldások lekéréses szolgáltatás</span><span class="sxs-lookup"><span data-stu-id="8871e-218">Community Solutions for Pull Service</span></span>

<span data-ttu-id="8871e-219">A DSC-Közösség készített rendelkezik több megoldás megvalósítása a lekéréses szolgáltatás protokollt.</span><span class="sxs-lookup"><span data-stu-id="8871e-219">The DSC community has authored multiple solutions to implement the pull service protocol.</span></span>
<span data-ttu-id="8871e-220">A helyszíni környezetben ezek ajánlat lekéréses szolgáltatásfunkciók és a egy lehetőség, hogy hozzájáruljanak a Közösség növekményes fejlesztései.</span><span class="sxs-lookup"><span data-stu-id="8871e-220">For on-premises environments, these offer pull service capabilities and an opportunity to contribute back to the community with incremental enhancements.</span></span>

- [<span data-ttu-id="8871e-221">Vontatóhajó</span><span class="sxs-lookup"><span data-stu-id="8871e-221">Tug</span></span>](https://github.com/powershellorg/tug)
- [<span data-ttu-id="8871e-222">DSC-TRÆK</span><span class="sxs-lookup"><span data-stu-id="8871e-222">DSC-TRÆK</span></span>](https://github.com/powershellorg/dsc-traek)

## <a name="pull-client-configuration"></a><span data-ttu-id="8871e-223">Lekérési ügyfél-konfiguráció</span><span class="sxs-lookup"><span data-stu-id="8871e-223">Pull client configuration</span></span>

<span data-ttu-id="8871e-224">Az alábbi témakörök ismertetik részletesen pull-ügyfelek beállítását:</span><span class="sxs-lookup"><span data-stu-id="8871e-224">The following topics describe setting up pull clients in detail:</span></span>

- [<span data-ttu-id="8871e-225">Egy konfigurációs azonosítóval DSC lekérési ügyfél beállítása</span><span class="sxs-lookup"><span data-stu-id="8871e-225">Setting up a DSC pull client using a configuration ID</span></span>](pullClientConfigID.md)
- [<span data-ttu-id="8871e-226">Konfigurációs nevekkel DSC lekérési ügyfél beállítása</span><span class="sxs-lookup"><span data-stu-id="8871e-226">Setting up a DSC pull client using configuration names</span></span>](pullClientConfigNames.md)
- [<span data-ttu-id="8871e-227">Részleges konfigurációk</span><span class="sxs-lookup"><span data-stu-id="8871e-227">Partial configurations</span></span>](partialConfigs.md)

## <a name="see-also"></a><span data-ttu-id="8871e-228">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="8871e-228">See also</span></span>

- [<span data-ttu-id="8871e-229">Windows PowerShell Desired State Configuration áttekintése</span><span class="sxs-lookup"><span data-stu-id="8871e-229">Windows PowerShell Desired State Configuration Overview</span></span>](overview.md)
- [<span data-ttu-id="8871e-230">Konfigurációk életbe léptetése</span><span class="sxs-lookup"><span data-stu-id="8871e-230">Enacting configurations</span></span>](enactingConfigurations.md)
- [<span data-ttu-id="8871e-231">A DSC jelentéskészítő kiszolgálójának használata</span><span class="sxs-lookup"><span data-stu-id="8871e-231">Using a DSC report server</span></span>](reportServer.md)
- <span data-ttu-id="8871e-232">[[MS-DSCPM]: a lekéréses modell protokoll Desired State Configuration](https://msdn.microsoft.com/library/dn393548.aspx)</span><span class="sxs-lookup"><span data-stu-id="8871e-232">[[MS-DSCPM]: Desired State Configuration Pull Model Protocol](https://msdn.microsoft.com/library/dn393548.aspx)</span></span>
- <span data-ttu-id="8871e-233">[[MS-DSCPM]: a lekéréses modell protokoll hibajegyzék Desired State Configuration](https://msdn.microsoft.com/library/mt612824.aspx)</span><span class="sxs-lookup"><span data-stu-id="8871e-233">[[MS-DSCPM]: Desired State Configuration Pull Model Protocol Errata](https://msdn.microsoft.com/library/mt612824.aspx)</span></span>
