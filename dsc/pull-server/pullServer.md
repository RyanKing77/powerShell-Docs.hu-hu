---
ms.date: 03/04/2019
keywords: DSC, powershell, a konfigurációt, a beállítása
title: DSC Pull Service
ms.openlocfilehash: 3cb2ca09111100f39589072a0d8e7010f9188efb
ms.sourcegitcommit: f268dce5b5e72be669be0c6634b8db11369bbae2
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/29/2019
ms.locfileid: "58623942"
---
# <a name="desired-state-configuration-pull-service"></a><span data-ttu-id="16b8a-103">Desired State Configuration lekéréses szolgáltatás</span><span class="sxs-lookup"><span data-stu-id="16b8a-103">Desired State Configuration Pull Service</span></span>

> [!IMPORTANT]
> <span data-ttu-id="16b8a-104">A lekéréses kiszolgálón (Windows-szolgáltatás *DSC-szolgáltatás*), a Windows Server támogatott összetevője létezik azonban tervekben sem funkciókat és képességeket kínálnak.</span><span class="sxs-lookup"><span data-stu-id="16b8a-104">The Pull Server (Windows Feature *DSC-Service*) is a supported component of Windows Server however there are no plans to offer new features or capabilities.</span></span> <span data-ttu-id="16b8a-105">Javasoljuk, hogy helyeződnek felügyelt ügyfelek [Azure Automation DSC](/azure/automation/automation-dsc-getting-started) (beleértve a lekéréses kiszolgálón a Windows Server csomagban) vagy a közösségi megoldások felsorolt [Itt](pullserver.md#community-solutions-for-pull-service).</span><span class="sxs-lookup"><span data-stu-id="16b8a-105">It is recommended to begin transitioning managed clients to [Azure Automation DSC](/azure/automation/automation-dsc-getting-started) (includes features beyond Pull Server on Windows Server) or one of the community solutions listed [here](pullserver.md#community-solutions-for-pull-service).</span></span>

<span data-ttu-id="16b8a-106">Helyi Configuration Manager lekéréses Szolgáltatottszoftver-megoldás központilag kezelhetők.</span><span class="sxs-lookup"><span data-stu-id="16b8a-106">Local Configuration Manager can be centrally managed by a Pull Service solution.</span></span>
<span data-ttu-id="16b8a-107">Ez a megközelítés használatakor a felügyelt csomópont regisztrálva a szolgáltatásban és konfigurálása során a LCM beállításokat rendelt.</span><span class="sxs-lookup"><span data-stu-id="16b8a-107">When using this approach, the node that is being managed is registered with a service and assigned a configuration in LCM settings.</span></span>
<span data-ttu-id="16b8a-108">A konfiguráció minden DSC-erőforrások függőségeként a konfigurációhoz szükséges a géphez letöltött és LCM használja a konfiguráció kezelésére.</span><span class="sxs-lookup"><span data-stu-id="16b8a-108">The configuration and all DSC resources needed as dependencies for the configuration are downloaded to the machine and used by LCM to manage the configuration.</span></span>
<span data-ttu-id="16b8a-109">A felügyelt számítógép állapotát a service for reporting töltenek fel.</span><span class="sxs-lookup"><span data-stu-id="16b8a-109">Information about the state of the machine being managed is uploaded to the service for reporting.</span></span>
<span data-ttu-id="16b8a-110">A fogalom a neve "lekéréses szolgáltatás."</span><span class="sxs-lookup"><span data-stu-id="16b8a-110">This concept is referred to as "pull service."</span></span>

<span data-ttu-id="16b8a-111">A lekéréses szolgáltatás jelenlegi lehetőségek a következők:</span><span class="sxs-lookup"><span data-stu-id="16b8a-111">The current options for pull service include:</span></span>

- <span data-ttu-id="16b8a-112">Azure Automation Desired State Configuration service</span><span class="sxs-lookup"><span data-stu-id="16b8a-112">Azure Automation Desired State Configuration service</span></span>
- <span data-ttu-id="16b8a-113">Windows Server rendszeren futó lekéréses szolgáltatás</span><span class="sxs-lookup"><span data-stu-id="16b8a-113">A pull service running on Windows Server</span></span>
- <span data-ttu-id="16b8a-114">Közösségi nyílt forráskódú megoldások karbantartása</span><span class="sxs-lookup"><span data-stu-id="16b8a-114">Community maintained open-source solutions</span></span>
- <span data-ttu-id="16b8a-115">SMB-megosztáson</span><span class="sxs-lookup"><span data-stu-id="16b8a-115">An SMB share</span></span>

<span data-ttu-id="16b8a-116">**Az ajánlott megoldás a**, és a lehetőség érhető el, a legtöbb funkciót a [Azure Automation DSC](/azure/automation/automation-dsc-getting-started).</span><span class="sxs-lookup"><span data-stu-id="16b8a-116">**The recommended solution**, and the option with the most features available, is [Azure Automation DSC](/azure/automation/automation-dsc-getting-started).</span></span>

<span data-ttu-id="16b8a-117">Az Azure-szolgáltatás csomópontjai a helyszíni privát adatközpontok, vagy a nyilvános felhők, például az Azure és az AWS is kezelheti.</span><span class="sxs-lookup"><span data-stu-id="16b8a-117">The Azure service can manage nodes on-premises in private datacenters, or in public clouds such as Azure and AWS.</span></span>
<span data-ttu-id="16b8a-118">Ahol kiszolgálói nem tudnak közvetlenül kapcsolódni az internetre privát környezetek esetén fontolja meg, csak a közzétett Azure IP-címtartomány irányuló kimenő forgalom korlátozása (lásd: [Azure Datacenter IP-címtartományok](https://www.microsoft.com/en-us/download/details.aspx?id=41653)).</span><span class="sxs-lookup"><span data-stu-id="16b8a-118">For private environments where servers cannot directly connect to the Internet, consider limiting outbound traffic to only the published Azure IP range (see [Azure Datacenter IP Ranges](https://www.microsoft.com/en-us/download/details.aspx?id=41653)).</span></span>

<span data-ttu-id="16b8a-119">Az online szolgáltatás, amelyek nem a Windows Server, a lekéréses szolgáltatásban jelenleg elérhető funkciók:</span><span class="sxs-lookup"><span data-stu-id="16b8a-119">Features of the online service that are not currently available in the pull service on Windows Server include:</span></span>

- <span data-ttu-id="16b8a-120">Összes adat titkosítva lesz az úton lévő és inaktív</span><span class="sxs-lookup"><span data-stu-id="16b8a-120">All data is encrypted in transit and at rest</span></span>
- <span data-ttu-id="16b8a-121">Ügyfél-tanúsítványok létrehozása és felügyelete automatikus</span><span class="sxs-lookup"><span data-stu-id="16b8a-121">Client certificates are created and managed automatically</span></span>
- <span data-ttu-id="16b8a-122">Titkos kódok tárolása központilag kezelésére szolgáló [jelszavak és a hitelesítő adatok](/azure/automation/automation-credentials), vagy [változók](/azure/automation/automation-variables) például a kiszolgáló nevét vagy a kapcsolati karakterláncok</span><span class="sxs-lookup"><span data-stu-id="16b8a-122">Secrets store for centrally managing [passwords/credentials](/azure/automation/automation-credentials), or [variables](/azure/automation/automation-variables) such as server names or connection strings</span></span>
- <span data-ttu-id="16b8a-123">Központilag kezelheti a csomópont [LCM konfigurálása](../managing-nodes/metaConfig.md#basic-settings)</span><span class="sxs-lookup"><span data-stu-id="16b8a-123">Centrally manage node [LCM configuration](../managing-nodes/metaConfig.md#basic-settings)</span></span>
- <span data-ttu-id="16b8a-124">Konfigurációk központilag ügyfél-csomópontok hozzárendelése</span><span class="sxs-lookup"><span data-stu-id="16b8a-124">Centrally assign configurations to client nodes</span></span>
- <span data-ttu-id="16b8a-125">Kiadási konfiguráció módosításait "tesztcsoportos csoportok" tesztelési éles elérése előtt</span><span class="sxs-lookup"><span data-stu-id="16b8a-125">Release configuration changes to "canary groups" for testing before reaching production</span></span>
- <span data-ttu-id="16b8a-126">Grafikus jelentési</span><span class="sxs-lookup"><span data-stu-id="16b8a-126">Graphical reporting</span></span>
  - <span data-ttu-id="16b8a-127">A granularitási DSC erőforrás szintjén állapotának részletei</span><span class="sxs-lookup"><span data-stu-id="16b8a-127">Status detail at the DSC resource level of granularity</span></span>
  - <span data-ttu-id="16b8a-128">Hibaelhárítás az ügyfélgépek a részletes hibaüzenetek</span><span class="sxs-lookup"><span data-stu-id="16b8a-128">Verbose error messages from client machines for troubleshooting</span></span>
- <span data-ttu-id="16b8a-129">[Integráció az Azure Log Analytics](/azure/automation/automation-dsc-diagnostics) riasztási, automatizált feladatokat, jelentéskészítési és riasztási Android vagy iOS-alkalmazás</span><span class="sxs-lookup"><span data-stu-id="16b8a-129">[Integration with Azure Log Analytics](/azure/automation/automation-dsc-diagnostics) for alerting, automated tasks, Android/iOS app for reporting and alerting</span></span>

## <a name="dsc-pull-service-in-windows-server"></a><span data-ttu-id="16b8a-130">DSC lekéréses szolgáltatás a Windows Server</span><span class="sxs-lookup"><span data-stu-id="16b8a-130">DSC pull service in Windows Server</span></span>

<span data-ttu-id="16b8a-131">A Windows Serveren futó lekéréses szolgáltatás konfigurálása lehetőség.</span><span class="sxs-lookup"><span data-stu-id="16b8a-131">It is possible to configure a pull service to run on Windows Server.</span></span>
<span data-ttu-id="16b8a-132">Felhasználóitevékenység, hogy az lekéréses szolgáltatás része a Windows Server tartalmaz konfigurációk/modulok letölthető tárolására, és a jelentés adatai az adatbázis csak képességeit.</span><span class="sxs-lookup"><span data-stu-id="16b8a-132">Be advised that the pull service solution included in Windows Server includes only capabilities of storing configurations/modules for download and capturing report data in to database.</span></span>
<span data-ttu-id="16b8a-133">Nem tartalmazza a képességek a szolgáltatást az Azure által kínált számos, és ezért nem kiértékelését, hogy a szolgáltatás használni kívánt hatékony eszköz.</span><span class="sxs-lookup"><span data-stu-id="16b8a-133">It does not include many of the capabilities offered by the service in Azure and so is not a good tool for evaluating how the service would be used.</span></span>

<span data-ttu-id="16b8a-134">A lekéréses szolgáltatás, a Windows Server rendszer egy webszolgáltatás, amely egy OData-felületet segítségével DSC konfigurációs fájlok célcsomópontok számára elérhetővé tenni, ha azokat a csomópontokat, kérje meg őket az IIS-ben.</span><span class="sxs-lookup"><span data-stu-id="16b8a-134">The pull service offered in Windows Server is a web service in IIS that uses an OData interface to make DSC configuration files available to target nodes when those nodes ask for them.</span></span>

<span data-ttu-id="16b8a-135">Egy lekéréses kiszolgálót használatának követelményei:</span><span class="sxs-lookup"><span data-stu-id="16b8a-135">Requirements for using a pull server:</span></span>

- <span data-ttu-id="16b8a-136">Futtató kiszolgálón:</span><span class="sxs-lookup"><span data-stu-id="16b8a-136">A server running:</span></span>
  - <span data-ttu-id="16b8a-137">A WMF/PowerShell 4.0-s vagy újabb</span><span class="sxs-lookup"><span data-stu-id="16b8a-137">WMF/PowerShell 4.0 or greater</span></span>
  - <span data-ttu-id="16b8a-138">IIS-kiszolgálói szerepkör</span><span class="sxs-lookup"><span data-stu-id="16b8a-138">IIS server role</span></span>
  - <span data-ttu-id="16b8a-139">DSC-szolgáltatás</span><span class="sxs-lookup"><span data-stu-id="16b8a-139">DSC Service</span></span>
- <span data-ttu-id="16b8a-140">Ideális esetben néhány azt jelenti, hogy egy tanúsítványt létrehozni bloberőforrásokhoz átadott, a helyi Configuration Manager (LCM) Konfigurálása a célcsomópontokat hitelesítő adatok biztonságossá tételéhez</span><span class="sxs-lookup"><span data-stu-id="16b8a-140">Ideally, some means of generating a certificate, to secure credentials passed to the Local Configuration Manager (LCM) on target nodes</span></span>

<span data-ttu-id="16b8a-141">Windows Server konfigurálása a gazdagépen lekéréses szolgáltatás a legjobb módszer az DSC-konfiguráció használata.</span><span class="sxs-lookup"><span data-stu-id="16b8a-141">The best way to configure Windows Server to host pull service is to use a DSC configuration.</span></span>
<span data-ttu-id="16b8a-142">Példa parancsfájl lejjebb találja.</span><span class="sxs-lookup"><span data-stu-id="16b8a-142">An example script is provided below.</span></span>

### <a name="supported-database-systems"></a><span data-ttu-id="16b8a-143">Támogatott adatbázis-rendszerek</span><span class="sxs-lookup"><span data-stu-id="16b8a-143">Supported database systems</span></span>

|<span data-ttu-id="16b8a-144">WMF 4.0</span><span class="sxs-lookup"><span data-stu-id="16b8a-144">WMF 4.0</span></span>   |<span data-ttu-id="16b8a-145">WMF 5.0</span><span class="sxs-lookup"><span data-stu-id="16b8a-145">WMF 5.0</span></span>  |<span data-ttu-id="16b8a-146">WMF 5.1</span><span class="sxs-lookup"><span data-stu-id="16b8a-146">WMF 5.1</span></span> |<span data-ttu-id="16b8a-147">A WMF 5.1 (Windows Server Insider Preview 17090)</span><span class="sxs-lookup"><span data-stu-id="16b8a-147">WMF 5.1 (Windows Server Insider Preview 17090)</span></span>|
|---------|---------|---------|---------|
|<span data-ttu-id="16b8a-148">MDB</span><span class="sxs-lookup"><span data-stu-id="16b8a-148">MDB</span></span>     |<span data-ttu-id="16b8a-149">MDB (alapértelmezett), ESENT</span><span class="sxs-lookup"><span data-stu-id="16b8a-149">ESENT (Default), MDB</span></span> |<span data-ttu-id="16b8a-150">MDB (alapértelmezett), ESENT</span><span class="sxs-lookup"><span data-stu-id="16b8a-150">ESENT (Default), MDB</span></span>|<span data-ttu-id="16b8a-151">(Alapértelmezett), SQL Server, MDB ESENT</span><span class="sxs-lookup"><span data-stu-id="16b8a-151">ESENT (Default), SQL Server, MDB</span></span>

<span data-ttu-id="16b8a-152">Kezdődően az 17090 kiadási [Windows Server Insider Preview](https://www.microsoft.com/en-us/software-download/windowsinsiderpreviewserver), SQL Server támogatott beállítás a lekéréses szolgáltatás a (Windows-szolgáltatás *DSC-szolgáltatás*).</span><span class="sxs-lookup"><span data-stu-id="16b8a-152">Starting in release 17090 of [Windows Server Insider Preview](https://www.microsoft.com/en-us/software-download/windowsinsiderpreviewserver), SQL Server is a supported option for the Pull Service (Windows Feature *DSC-Service*).</span></span> <span data-ttu-id="16b8a-153">Ez biztosítja, hogy új lehetőség a skálázás, nagy méretű DSC-környezetekben, amelyek nem áttelepített [Azure Automation DSC](/azure/automation/automation-dsc-getting-started).</span><span class="sxs-lookup"><span data-stu-id="16b8a-153">This provides a new option for scaling large DSC environments that have not migrated to [Azure Automation DSC](/azure/automation/automation-dsc-getting-started).</span></span>

> [!NOTE]
> <span data-ttu-id="16b8a-154">SQL Server-támogatása nem kerül a korábbi verziók a WMF 5.1-es (vagy korábbi), és csak a Windows Server-verziók nagyobb vagy egyenlő 17090 elérhető lesz.</span><span class="sxs-lookup"><span data-stu-id="16b8a-154">SQL Server support will not be added to previous versions of WMF 5.1 (or earlier) and will only be available on Windows Server versions greater than or equal to 17090.</span></span>

<span data-ttu-id="16b8a-155">A lekérési kiszolgálójával, hogy az SQL Server konfigurálásához állítsa **SqlProvider** a `$true` és **SqlConnectionString** a egy érvényes SQL Server kapcsolati karakterláncát.</span><span class="sxs-lookup"><span data-stu-id="16b8a-155">To configure the pull server to use SQL Server, set **SqlProvider** to `$true` and **SqlConnectionString** to a valid SQL Server Connection String.</span></span> <span data-ttu-id="16b8a-156">További információkért lásd: [SqlClient kapcsolati karakterláncok](/dotnet/framework/data/adonet/connection-string-syntax#sqlclient-connection-strings).</span><span class="sxs-lookup"><span data-stu-id="16b8a-156">For more information, see [SqlClient Connection Strings](/dotnet/framework/data/adonet/connection-string-syntax#sqlclient-connection-strings).</span></span>
<span data-ttu-id="16b8a-157">Például egy SQL Server-konfiguráció **xDscWebService**, először olvassa el [xDscWebService erőforrást használó](#using-the-xdscwebservice-resource) , és tekintse át a [Sample_xDscWebServiceRegistration_ A Githubon UseSQLProvider.ps1](https://github.com/PowerShell/xPSDesiredStateConfiguration/blob/master/Examples/Sample_xDscWebServiceRegistration_UseSQLProvider.ps1).</span><span class="sxs-lookup"><span data-stu-id="16b8a-157">For an example of SQL Server configuration with **xDscWebService**, first read [Using the xDscWebService resource](#using-the-xdscwebservice-resource) and then review [Sample_xDscWebServiceRegistration_UseSQLProvider.ps1 on GitHub](https://github.com/PowerShell/xPSDesiredStateConfiguration/blob/master/Examples/Sample_xDscWebServiceRegistration_UseSQLProvider.ps1).</span></span>

### <a name="using-the-xdscwebservice-resource"></a><span data-ttu-id="16b8a-158">A xDscWebService erőforrás segítségével</span><span class="sxs-lookup"><span data-stu-id="16b8a-158">Using the xDscWebService resource</span></span>

<span data-ttu-id="16b8a-159">Lekérési kiszolgáló beállítása a legegyszerűbb módja az, hogy használja a **xDscWebService** erőforrás, szerepel a **xPSDesiredStateConfiguration** modul.</span><span class="sxs-lookup"><span data-stu-id="16b8a-159">The easiest way to set up a web pull server is to use the **xDscWebService** resource, included in the **xPSDesiredStateConfiguration** module.</span></span>
<span data-ttu-id="16b8a-160">A következő lépések azt ismertetik, hogyan használhatja az erőforrást, amely beállítja a web service konfigurációban.</span><span class="sxs-lookup"><span data-stu-id="16b8a-160">The following steps explain how to use the resource in a configuration that sets up the web service.</span></span>

1. <span data-ttu-id="16b8a-161">Hívja a [Install-Module](/powershell/module/PowershellGet/Install-Module) telepítésére szolgáló parancsmagot a **xPSDesiredStateConfiguration** modul.</span><span class="sxs-lookup"><span data-stu-id="16b8a-161">Call the [Install-Module](/powershell/module/PowershellGet/Install-Module) cmdlet to install the **xPSDesiredStateConfiguration** module.</span></span>
   > [!NOTE]
   > <span data-ttu-id="16b8a-162">**Install-Module** szerepel a **PowerShellGet** modult, amely része a PowerShell 5.0-s.</span><span class="sxs-lookup"><span data-stu-id="16b8a-162">**Install-Module** is included in the **PowerShellGet** module, which is included in PowerShell 5.0.</span></span> <span data-ttu-id="16b8a-163">Letöltheti a **PowerShellGet** modul a PowerShell 3.0 és 4.0-s verzióját, [PackageManagement PowerShell modul előzetes](https://www.microsoft.com/en-us/download/details.aspx?id=49186).</span><span class="sxs-lookup"><span data-stu-id="16b8a-163">You can download the **PowerShellGet** module for PowerShell 3.0 and 4.0 at [PackageManagement PowerShell Modules Preview](https://www.microsoft.com/en-us/download/details.aspx?id=49186).</span></span>
2. <span data-ttu-id="16b8a-164">SSL-tanúsítvány a DSC lekéréses kiszolgálón le egy megbízható hitelesítésszolgáltató, vagy a szervezet vagy egy nyilvános szolgáltató belül.</span><span class="sxs-lookup"><span data-stu-id="16b8a-164">Get an SSL certificate for the DSC Pull server from a trusted Certificate Authority, either within your organization or a public authority.</span></span> <span data-ttu-id="16b8a-165">A szolgáltató kapott tanúsítvány általában a PFX formátumban van.</span><span class="sxs-lookup"><span data-stu-id="16b8a-165">The certificate received from the authority is usually in the PFX format.</span></span>
3. <span data-ttu-id="16b8a-166">Telepítse a tanúsítványt a csomóponton a DSC lekéréses kiszolgálón az alapértelmezett helyen, amely elvileg váló `CERT:\LocalMachine\My`.</span><span class="sxs-lookup"><span data-stu-id="16b8a-166">Install the certificate on the node that will become the DSC Pull server in the default location, which should be `CERT:\LocalMachine\My`.</span></span>
   - <span data-ttu-id="16b8a-167">Jegyezze fel a tanúsítvány-ujjlenyomatot.</span><span class="sxs-lookup"><span data-stu-id="16b8a-167">Make a note of the certificate thumbprint.</span></span>
4. <span data-ttu-id="16b8a-168">Válassza ki a regisztrációs kulcsát, használható egy GUID Azonosítót.</span><span class="sxs-lookup"><span data-stu-id="16b8a-168">Select a GUID to be used as the Registration Key.</span></span> <span data-ttu-id="16b8a-169">Hozhat létre egy PowerShell-lel, írja be a következő, a PS-parancssorba, és nyomja le az enter: `[guid]::newGuid()` vagy `New-Guid`.</span><span class="sxs-lookup"><span data-stu-id="16b8a-169">To generate one using PowerShell enter the following at the PS prompt and press enter: `[guid]::newGuid()` or `New-Guid`.</span></span> <span data-ttu-id="16b8a-170">Ezt a kulcsot a regisztráció során hitelesítsék magukat a megosztott kulcs lesz ügyfél csomópontja.</span><span class="sxs-lookup"><span data-stu-id="16b8a-170">This key will be used by client nodes as a shared key to authenticate during registration.</span></span> <span data-ttu-id="16b8a-171">További információkért tekintse meg a regisztrációs kulcsot az alábbi szakaszban.</span><span class="sxs-lookup"><span data-stu-id="16b8a-171">For more information, see the Registration Key section below.</span></span>
5. <span data-ttu-id="16b8a-172">A PowerShell ISE-ben (F5) a következő konfigurációs parancsfájl futtatásához (példák mappájában található a **xPSDesiredStateConfiguration** modul mint `Sample_xDscWebServiceRegistration.ps1`).</span><span class="sxs-lookup"><span data-stu-id="16b8a-172">In the PowerShell ISE, start (F5) the following configuration script (included in the Examples folder of the **xPSDesiredStateConfiguration** module as `Sample_xDscWebServiceRegistration.ps1`).</span></span> <span data-ttu-id="16b8a-173">Ez a szkript állítja be a lekéréses kiszolgálón.</span><span class="sxs-lookup"><span data-stu-id="16b8a-173">This script sets up the pull server.</span></span>

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

        Import-DSCResource -ModuleName PSDesiredStateConfiguration
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
                UseSecurityBestPractices     = $true
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

6. <span data-ttu-id="16b8a-174">Futtassa a konfigurációt, az SSL-tanúsítvány ujjlenyomata átadása a **certificateThumbPrint** paraméter és a egy GUID regisztrációs kulcsát a **RegistrationKey** paramétert:</span><span class="sxs-lookup"><span data-stu-id="16b8a-174">Run the configuration, passing the thumbprint of the SSL certificate as the **certificateThumbPrint** parameter and a GUID registration key as the **RegistrationKey** parameter:</span></span>

    ```powershell
    # To find the Thumbprint for an installed SSL certificate for use with the pull server list all certificates in your local store
    # and then copy the thumbprint for the appropriate certificate by reviewing the certificate subjects
    dir Cert:\LocalMachine\my

    # Then include this thumbprint when running the configuration
    Sample_xDscWebServiceRegistration -certificateThumbprint 'A7000024B753FA6FFF88E966FD6E19301FAE9CCC' -RegistrationKey '140a952b-b9d6-406b-b416-e0f759c9c0e4' -OutputPath c:\Configs\PullServer

    # Run the compiled configuration to make the target node a DSC Pull Server
    Start-DscConfiguration -Path c:\Configs\PullServer -Wait -Verbose
    ```

#### <a name="registration-key"></a><span data-ttu-id="16b8a-175">Regisztrációs kulcs</span><span class="sxs-lookup"><span data-stu-id="16b8a-175">Registration Key</span></span>

<span data-ttu-id="16b8a-176">Ahhoz, hogy az ügyfél-csomópontokat, hogy a konfigurációs nevek helyett egy konfigurációs azonosító használatához regisztrálni a kiszolgálóval, a fenti konfigurációs által létrehozott regisztrációs kulcsát nevű fájlba mentése `RegistrationKeys.txt` a `C:\Program Files\WindowsPowerShell\DscService`.</span><span class="sxs-lookup"><span data-stu-id="16b8a-176">To allow client nodes to register with the server so that they can use configuration names instead of a configuration ID, a registration key that was created by the above configuration is saved in a file named `RegistrationKeys.txt` in `C:\Program Files\WindowsPowerShell\DscService`.</span></span> <span data-ttu-id="16b8a-177">A regisztrációs kulcs egy közös titkos kulcsot használja a kezdeti regisztráció során az ügyfél és a lekéréses kiszolgálón működik.</span><span class="sxs-lookup"><span data-stu-id="16b8a-177">The registration key functions as a shared secret used during the initial registration by the client with the pull server.</span></span> <span data-ttu-id="16b8a-178">Az ügyfél, amely után a regisztráció sikeres elvégzése után a lekéréses kiszolgálón egyedi hitelesítésére használt önaláírt tanúsítványt hoz létre.</span><span class="sxs-lookup"><span data-stu-id="16b8a-178">The client will generate a self-signed certificate that is used to uniquely authenticate to the pull server once registration is successfully completed.</span></span> <span data-ttu-id="16b8a-179">Ez a tanúsítvány ujjlenyomatának helyileg tárolja, és a társított URL-címét a lekéréses kiszolgálón.</span><span class="sxs-lookup"><span data-stu-id="16b8a-179">The thumbprint of this certificate is stored locally and associated with the URL of the pull server.</span></span>

> [!NOTE]
> <span data-ttu-id="16b8a-180">Regisztrációs kulcsok nem támogatottak a PowerShell 4.0-s verzióját.</span><span class="sxs-lookup"><span data-stu-id="16b8a-180">Registration keys are not supported in PowerShell 4.0.</span></span>

<span data-ttu-id="16b8a-181">Annak érdekében, hogy a pull-kiszolgálóval hitelesíteni csomópontok konfigurálásához, a regisztrációs kulccsal kell lennie az összes cél csomóponttal fog a lekéréses kiszolgálón kell Regisztrálás a metaconfiguration.</span><span class="sxs-lookup"><span data-stu-id="16b8a-181">In order to configure a node to authenticate with the pull server, the registration key needs to be in the metaconfiguration for any target node that will be registering with this pull server.</span></span> <span data-ttu-id="16b8a-182">Vegye figyelembe, hogy a **RegistrationKey** az alábbi metaconfiguration eltűnik, miután sikeresen regisztrálta a célgépen, és hogy az érték egyezzen tárol a `RegistrationKeys.txt` fájlt a lekérési kiszolgálón (" 140a952b-b9d6-406b-b416-e0f759c9c0e4 "Ebben a példában).</span><span class="sxs-lookup"><span data-stu-id="16b8a-182">Note that the **RegistrationKey** in the metaconfiguration below is removed after the target machine has successfully registered, and that the value must match the value stored in the `RegistrationKeys.txt` file on the pull server ('140a952b-b9d6-406b-b416-e0f759c9c0e4' for this example).</span></span> <span data-ttu-id="16b8a-183">A regisztrációs kulcs értékét biztonságosan, mindig kezeli, mivel azt, hogy lehetővé teszi bármely a célgépen, a lekéréses kiszolgálón regisztrálni.</span><span class="sxs-lookup"><span data-stu-id="16b8a-183">Always treat the registration key value securely, because knowing it allows any target machine to register with the pull server.</span></span>

```powershell
[DSCLocalConfigurationManager()]
configuration Sample_MetaConfigurationToRegisterWithLessSecurePullServer
{
    param
    (
        [ValidateNotNullOrEmpty()]
        [string] $NodeName = 'localhost',

        [ValidateNotNullOrEmpty()]
        [string] $RegistrationKey, #same as the one used to set up pull server in previous configuration

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

> [!NOTE]
> <span data-ttu-id="16b8a-184">A **ReportServerWeb** szakasz lehetővé teszi, hogy a lekéréses kiszolgálón küldendő adatokról szóló jelentéseket küldeni.</span><span class="sxs-lookup"><span data-stu-id="16b8a-184">The **ReportServerWeb** section allows reporting data to be sent to the pull server.</span></span>

<span data-ttu-id="16b8a-185">Hiánya az **ConfigurationID** tulajdonság a metaconfiguration fájlban implicit módon azt jelenti, hogy a lekéréses kiszolgáló támogat a V2 verziójú lekéréses kiszolgálón protokollt így egy kezdeti regisztrációs megadása kötelező.</span><span class="sxs-lookup"><span data-stu-id="16b8a-185">The lack of the **ConfigurationID** property in the metaconfiguration file implicitly means that pull server is supporting the V2 version of the pull server protocol so an initial registration is required.</span></span>
<span data-ttu-id="16b8a-186">Ezzel szemben, a jelenléte egy **ConfigurationID** azt jelenti, hogy a lekéréses kiszolgálón protokoll V1 verzióját használja, és nincs a feldolgozás nem regisztrációs.</span><span class="sxs-lookup"><span data-stu-id="16b8a-186">Conversely, the presence of a **ConfigurationID** means that the V1 version of the pull server protocol is used and there is no registration processing.</span></span>

> [!NOTE]
> <span data-ttu-id="16b8a-187">A LEKÜLDÉSES forgatókönyvekben jelentse a jelenlegi kiadásban, amellyel meg kell határozni egy ConfigurationID tulajdonság egy lekéréses kiszolgálót soha nem regisztrált csomópontok metaconfiguration fájlban szerepel.</span><span class="sxs-lookup"><span data-stu-id="16b8a-187">In a PUSH scenario, a bug exists in the current release that makes it necessary to define a ConfigurationID property in the metaconfiguration file for nodes that have never registered with a pull server.</span></span> <span data-ttu-id="16b8a-188">Ezzel a V1 lekéréses kiszolgálón protokoll kényszerítése és regisztrációs hibaüzenetek elkerülése érdekében.</span><span class="sxs-lookup"><span data-stu-id="16b8a-188">This will force the V1 Pull Server protocol and avoid registration failure messages.</span></span>

## <a name="placing-configurations-and-resources"></a><span data-ttu-id="16b8a-189">Konfigurációkat és erőforrásokat elhelyezése</span><span class="sxs-lookup"><span data-stu-id="16b8a-189">Placing configurations and resources</span></span>

<span data-ttu-id="16b8a-190">Miután a lekéréses server telepítésének befejezése határozzák meg a mappák a **ConfigurationPath** és **ModulePath** a pull-kiszolgálói konfigurációban a tulajdonságok akkor, hogy hol helyezi el a modulok és konfigurációk amely lekéréses cél csomópontok elérhető lesz.</span><span class="sxs-lookup"><span data-stu-id="16b8a-190">After the pull server setup completes, the folders defined by the **ConfigurationPath** and **ModulePath** properties in the pull server configuration are where you will place modules and configurations that will be available for target nodes to pull.</span></span>
<span data-ttu-id="16b8a-191">Ezeket a fájlokat kell lennie ahhoz, hogy a pull-kiszolgáló megfelelően feldolgozza őket egy meghatározott formátumban.</span><span class="sxs-lookup"><span data-stu-id="16b8a-191">These files need to be in a specific format in order for the pull server to correctly process them.</span></span>

### <a name="dsc-resource-module-package-format"></a><span data-ttu-id="16b8a-192">DSC erőforrás modul csomag formátuma</span><span class="sxs-lookup"><span data-stu-id="16b8a-192">DSC resource module package format</span></span>

<span data-ttu-id="16b8a-193">Minden egyes erőforrás modulnak kell zip és a következő mintának megfelelően nevű `{Module Name}_{Module Version}.zip`.</span><span class="sxs-lookup"><span data-stu-id="16b8a-193">Each resource module needs to be zipped and named according to the following pattern `{Module Name}_{Module Version}.zip`.</span></span>

<span data-ttu-id="16b8a-194">3.1.2.0 modul verziójával xWebAdminstration modul neve például `xWebAdministration_3.2.1.0.zip`.</span><span class="sxs-lookup"><span data-stu-id="16b8a-194">For example, a module named xWebAdminstration with a module version of 3.1.2.0 would be named `xWebAdministration_3.2.1.0.zip`.</span></span>
<span data-ttu-id="16b8a-195">Minden egyes modul verzióját tartalmaznia kell egy egyetlen zip-fájlt.</span><span class="sxs-lookup"><span data-stu-id="16b8a-195">Each version of a module must be contained in a single zip file.</span></span>
<span data-ttu-id="16b8a-196">Mivel minden egyes zip-fájlt az erőforráshoz csak egyetlen verziója, a WMF 5.0-s egyetlen címtárban több modul verzió támogatása hozzáadva a modul formátum nem támogatott.</span><span class="sxs-lookup"><span data-stu-id="16b8a-196">Since there is only a single version of a resource in each zip file, the module format added in WMF 5.0 with support for multiple module versions in a single directory is not supported.</span></span>
<span data-ttu-id="16b8a-197">Ez azt jelenti, hogy becsomagolást mentése erőforrás modulok DSC lekéréses kiszolgálón való használatra előtt ki kell, hogy módosítsa a könyvtár struktúra.</span><span class="sxs-lookup"><span data-stu-id="16b8a-197">This means that before packaging up DSC resource modules for use with pull server you will need to make a small change to the directory structure.</span></span>
<span data-ttu-id="16b8a-198">Az alapértelmezett formátum a modulok DSC-erőforrás a WMF 5.0 tartalmazó `{Module Folder}\{Module Version}\DscResources\{DSC Resource Folder}\`.</span><span class="sxs-lookup"><span data-stu-id="16b8a-198">The default format of modules containing DSC resource in WMF 5.0 is `{Module Folder}\{Module Version}\DscResources\{DSC Resource Folder}\`.</span></span>
<span data-ttu-id="16b8a-199">Terveztük a lekérési kiszolgálón csomagolást, előtt távolítsa el a **{modul version}** mappát az elérési út válik, így `{Module Folder}\DscResources\{DSC Resource Folder}\`.</span><span class="sxs-lookup"><span data-stu-id="16b8a-199">Before packaging up for the pull server, remove the **{Module version}** folder so the path becomes `{Module Folder}\DscResources\{DSC Resource Folder}\`.</span></span>
<span data-ttu-id="16b8a-200">A mappa az módosítása zip-fent leírtak szerint, és helyezze ezeket a zip-fájlokat a **ModulePath** mappát.</span><span class="sxs-lookup"><span data-stu-id="16b8a-200">With this change, zip the folder as described above and place these zip files in the **ModulePath** folder.</span></span>

<span data-ttu-id="16b8a-201">Használat `New-DscChecksum {module zip file}` az újonnan hozzáadott modul ellenőrzőösszeg fájl létrehozásához.</span><span class="sxs-lookup"><span data-stu-id="16b8a-201">Use `New-DscChecksum {module zip file}` to create a checksum file for the newly added module.</span></span>

### <a name="configuration-mof-format"></a><span data-ttu-id="16b8a-202">Konfigurációs MOF-formátuma</span><span class="sxs-lookup"><span data-stu-id="16b8a-202">Configuration MOF format</span></span>

<span data-ttu-id="16b8a-203">A konfigurációs MOF-fájlt kell ellenőrzőösszeg fájl párosítani, hogy a cél csomópont egy LCM ellenőrizheti a konfigurációt.</span><span class="sxs-lookup"><span data-stu-id="16b8a-203">A configuration MOF file needs to be paired with a checksum file so that an LCM on a target node can validate the configuration.</span></span>
<span data-ttu-id="16b8a-204">Ellenőrzőösszeg létrehozásához hívja a [New-DscChecksum](/powershell/module/PSDesiredStateConfiguration/New-DscChecksum) parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="16b8a-204">To create a checksum, call the [New-DscChecksum](/powershell/module/PSDesiredStateConfiguration/New-DscChecksum) cmdlet.</span></span>
<span data-ttu-id="16b8a-205">A parancsmag lép egy **elérési út** paraméter, amely a mappát, ahol a konfigurációs MOF található.</span><span class="sxs-lookup"><span data-stu-id="16b8a-205">The cmdlet takes a **Path** parameter that specifies the folder where the configuration MOF is located.</span></span>
<span data-ttu-id="16b8a-206">A parancsmag létrehoz egy ellenőrzőösszeg-fájlt `ConfigurationMOFName.mof.checksum`, ahol `ConfigurationMOFName` a konfigurációs mof-fájl neve.</span><span class="sxs-lookup"><span data-stu-id="16b8a-206">The cmdlet creates a checksum file named `ConfigurationMOFName.mof.checksum`, where `ConfigurationMOFName` is the name of the configuration mof file.</span></span>
<span data-ttu-id="16b8a-207">Ha egynél több konfigurációs MOF-fájlok a megadott mappában, a mappában az egyes konfigurációkhoz egy ellenőrzőösszeg jön létre.</span><span class="sxs-lookup"><span data-stu-id="16b8a-207">If there are more than one configuration MOF files in the specified folder, a checksum is created for each configuration in the folder.</span></span>
<span data-ttu-id="16b8a-208">A MOF-fájlok és az azokhoz társított ellenőrzőösszeg fájlokat helyezze a **ConfigurationPath** mappát.</span><span class="sxs-lookup"><span data-stu-id="16b8a-208">Place the MOF files and their associated checksum files in the **ConfigurationPath** folder.</span></span>

> [!NOTE]
> <span data-ttu-id="16b8a-209">Ha módosítja a konfigurációs MOF-fájl bármilyen módon, az ellenőrzőösszeg-fájl is létre kell hoznia.</span><span class="sxs-lookup"><span data-stu-id="16b8a-209">If you change the configuration MOF file in any way, you must also recreate the checksum file.</span></span>

### <a name="tooling"></a><span data-ttu-id="16b8a-210">Eszköztámogatás</span><span class="sxs-lookup"><span data-stu-id="16b8a-210">Tooling</span></span>

<span data-ttu-id="16b8a-211">Annak érdekében, hogy a beállítás alkotják, ellenőrzése és felügyelete egyszerűbb, a lekéréses kiszolgálón a következő eszközöket is a xPSDesiredStateConfiguration modul legújabb verziója található példák:</span><span class="sxs-lookup"><span data-stu-id="16b8a-211">In order to make setting up, validating and managing the pull server easier, the following tools are included as examples in the latest version of the xPSDesiredStateConfiguration module:</span></span>

1. <span data-ttu-id="16b8a-212">A modul, amely segít a csomagolási DSC erőforrás modulok és konfigurációs fájljait használja a lekérési kiszolgálón.</span><span class="sxs-lookup"><span data-stu-id="16b8a-212">A module that will help with packaging DSC resource modules and configuration files for use on the pull server.</span></span>
   <span data-ttu-id="16b8a-213">[PublishModulesAndMofsToPullServer.psm1](https://github.com/PowerShell/xPSDesiredStateConfiguration/blob/master/DSCPullServerSetup/PublishModulesAndMofsToPullServer.psm1).</span><span class="sxs-lookup"><span data-stu-id="16b8a-213">[PublishModulesAndMofsToPullServer.psm1](https://github.com/PowerShell/xPSDesiredStateConfiguration/blob/master/DSCPullServerSetup/PublishModulesAndMofsToPullServer.psm1).</span></span>
   <span data-ttu-id="16b8a-214">Az alábbi példákat:</span><span class="sxs-lookup"><span data-stu-id="16b8a-214">Examples below:</span></span>

    ```powershell
        # Example 1 - Package all versions of given modules installed locally and MOF files are in c:\LocalDepot
         $moduleList = @('xWebAdministration', 'xPhp')
         Publish-DSCModuleAndMof -Source C:\LocalDepot -ModuleNameList $moduleList

         # Example 2 - Package modules and mof documents from c:\LocalDepot
         Publish-DSCModuleAndMof -Source C:\LocalDepot -Force
    ```

1. <span data-ttu-id="16b8a-215">A parancsfájl, amely ellenőrzi a lekérési kiszolgálón megfelelően van konfigurálva.</span><span class="sxs-lookup"><span data-stu-id="16b8a-215">A script that validates the pull server is configured correctly.</span></span> <span data-ttu-id="16b8a-216">[PullServerSetupTests.ps1](https://github.com/PowerShell/xPSDesiredStateConfiguration/blob/master/DSCPullServerSetup/PullServerDeploymentVerificationTest/PullServerSetupTests.ps1).</span><span class="sxs-lookup"><span data-stu-id="16b8a-216">[PullServerSetupTests.ps1](https://github.com/PowerShell/xPSDesiredStateConfiguration/blob/master/DSCPullServerSetup/PullServerDeploymentVerificationTest/PullServerSetupTests.ps1).</span></span>

## <a name="community-solutions-for-pull-service"></a><span data-ttu-id="16b8a-217">Közösségi megoldások lekéréses szolgáltatás</span><span class="sxs-lookup"><span data-stu-id="16b8a-217">Community Solutions for Pull Service</span></span>

<span data-ttu-id="16b8a-218">A DSC-Közösség készített rendelkezik több megoldás megvalósítása a lekéréses szolgáltatás protokollt.</span><span class="sxs-lookup"><span data-stu-id="16b8a-218">The DSC community has authored multiple solutions to implement the pull service protocol.</span></span>
<span data-ttu-id="16b8a-219">A helyszíni környezetben ezek ajánlat lekéréses szolgáltatásfunkciók és a egy lehetőség, hogy hozzájáruljanak a Közösség növekményes fejlesztései.</span><span class="sxs-lookup"><span data-stu-id="16b8a-219">For on-premises environments, these offer pull service capabilities and an opportunity to contribute back to the community with incremental enhancements.</span></span>

- [<span data-ttu-id="16b8a-220">Vontatóhajó</span><span class="sxs-lookup"><span data-stu-id="16b8a-220">Tug</span></span>](https://github.com/powershellorg/tug)
- [<span data-ttu-id="16b8a-221">DSC-TRÆK</span><span class="sxs-lookup"><span data-stu-id="16b8a-221">DSC-TRÆK</span></span>](https://github.com/powershellorg/dsc-traek)

## <a name="pull-client-configuration"></a><span data-ttu-id="16b8a-222">Lekérési ügyfél-konfiguráció</span><span class="sxs-lookup"><span data-stu-id="16b8a-222">Pull client configuration</span></span>

<span data-ttu-id="16b8a-223">Az alábbi témakörök ismertetik részletesen pull-ügyfelek beállítását:</span><span class="sxs-lookup"><span data-stu-id="16b8a-223">The following topics describe setting up pull clients in detail:</span></span>

- [<span data-ttu-id="16b8a-224">Egy konfigurációs azonosítóval DSC lekérési ügyfél beállítása</span><span class="sxs-lookup"><span data-stu-id="16b8a-224">Set up a DSC pull client using a configuration ID</span></span>](pullClientConfigID.md)
- [<span data-ttu-id="16b8a-225">Konfigurációs nevekkel DSC lekérési ügyfél beállítása</span><span class="sxs-lookup"><span data-stu-id="16b8a-225">Set up a DSC pull client using configuration names</span></span>](pullClientConfigNames.md)
- [<span data-ttu-id="16b8a-226">Részleges konfigurációk</span><span class="sxs-lookup"><span data-stu-id="16b8a-226">Partial configurations</span></span>](partialConfigs.md)

## <a name="see-also"></a><span data-ttu-id="16b8a-227">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="16b8a-227">See also</span></span>

- [<span data-ttu-id="16b8a-228">Windows PowerShell Desired State Configuration áttekintése</span><span class="sxs-lookup"><span data-stu-id="16b8a-228">Windows PowerShell Desired State Configuration Overview</span></span>](../overview/overview.md)
- [<span data-ttu-id="16b8a-229">Konfigurációk életbe léptetése</span><span class="sxs-lookup"><span data-stu-id="16b8a-229">Enacting configurations</span></span>](enactingConfigurations.md)
- [<span data-ttu-id="16b8a-230">A DSC jelentéskészítő kiszolgálójának használata</span><span class="sxs-lookup"><span data-stu-id="16b8a-230">Using a DSC report server</span></span>](reportServer.md)
- <span data-ttu-id="16b8a-231">[[MS-DSCPM]: A lekéréses modell protokoll Desired State Configuration](https://msdn.microsoft.com/library/dn393548.aspx)</span><span class="sxs-lookup"><span data-stu-id="16b8a-231">[[MS-DSCPM]: Desired State Configuration Pull Model Protocol](https://msdn.microsoft.com/library/dn393548.aspx)</span></span>
- <span data-ttu-id="16b8a-232">[[MS-DSCPM]: A lekéréses modell protokoll hibajegyzék Desired State Configuration](https://msdn.microsoft.com/library/mt612824.aspx)</span><span class="sxs-lookup"><span data-stu-id="16b8a-232">[[MS-DSCPM]: Desired State Configuration Pull Model Protocol Errata](https://msdn.microsoft.com/library/mt612824.aspx)</span></span>
