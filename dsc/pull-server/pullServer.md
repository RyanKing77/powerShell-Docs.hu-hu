---
ms.date: 03/04/2019
keywords: DSC, PowerShell, konfigurálás, beállítás
title: DSC Pull Service
ms.openlocfilehash: 865eae5813e0c7b656a4158f0b1350e60f1e3291
ms.sourcegitcommit: 5a004064f33acc0145ccd414535763e95f998c89
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/23/2019
ms.locfileid: "69986535"
---
# <a name="desired-state-configuration-pull-service"></a><span data-ttu-id="818d2-103">A kívánt állapot konfigurációjának lekérése szolgáltatás</span><span class="sxs-lookup"><span data-stu-id="818d2-103">Desired State Configuration Pull Service</span></span>

> [!IMPORTANT]
> <span data-ttu-id="818d2-104">A lekérési kiszolgáló (Windows *-szolgáltatás DSC-Service*) a Windows Server támogatott összetevője, azonban nincsenek új funkciók vagy képességek kínáló csomagok.</span><span class="sxs-lookup"><span data-stu-id="818d2-104">The Pull Server (Windows Feature *DSC-Service*) is a supported component of Windows Server however there are no plans to offer new features or capabilities.</span></span> <span data-ttu-id="818d2-105">Ajánlott megkezdeni a felügyelt ügyfelek átváltását [Azure Automation DSC](/azure/automation/automation-dsc-getting-started) -re (beleértve a Windows Serveren futó lekéréses kiszolgálón túli szolgáltatásokat) vagy az [itt](pullserver.md#community-solutions-for-pull-service)felsorolt közösségi megoldások egyikét.</span><span class="sxs-lookup"><span data-stu-id="818d2-105">It is recommended to begin transitioning managed clients to [Azure Automation DSC](/azure/automation/automation-dsc-getting-started) (includes features beyond Pull Server on Windows Server) or one of the community solutions listed [here](pullserver.md#community-solutions-for-pull-service).</span></span>

<span data-ttu-id="818d2-106">A helyi Configuration Manager a lekéréses szolgáltatási megoldás központilag kezelhető.</span><span class="sxs-lookup"><span data-stu-id="818d2-106">Local Configuration Manager can be centrally managed by a Pull Service solution.</span></span>
<span data-ttu-id="818d2-107">Ezen módszer használatakor a felügyelt csomópont regisztrálva van egy szolgáltatásban, és a konfigurációt az LCD-beállításokban kell kijelölni.</span><span class="sxs-lookup"><span data-stu-id="818d2-107">When using this approach, the node that is being managed is registered with a service and assigned a configuration in LCM settings.</span></span>
<span data-ttu-id="818d2-108">A konfiguráció és az összes olyan DSC-erőforrás, amely a konfiguráció függőségeire van szükség, a rendszer letölti a gépre, és az LCD ChipOnGlas használatával kezeli a konfigurációt.</span><span class="sxs-lookup"><span data-stu-id="818d2-108">The configuration and all DSC resources needed as dependencies for the configuration are downloaded to the machine and used by LCM to manage the configuration.</span></span>
<span data-ttu-id="818d2-109">A rendszer feltölti a felügyelt számítógép állapotára vonatkozó adatokat a jelentéskészítéshez.</span><span class="sxs-lookup"><span data-stu-id="818d2-109">Information about the state of the machine being managed is uploaded to the service for reporting.</span></span>
<span data-ttu-id="818d2-110">Ezt a koncepciót "lekéréses szolgáltatásnak" nevezzük.</span><span class="sxs-lookup"><span data-stu-id="818d2-110">This concept is referred to as "pull service."</span></span>

<span data-ttu-id="818d2-111">A lekéréses szolgáltatás jelenlegi beállításai a következők:</span><span class="sxs-lookup"><span data-stu-id="818d2-111">The current options for pull service include:</span></span>

- <span data-ttu-id="818d2-112">Azure Automation kívánt állapot-konfigurációs szolgáltatás</span><span class="sxs-lookup"><span data-stu-id="818d2-112">Azure Automation Desired State Configuration service</span></span>
- <span data-ttu-id="818d2-113">Windows Serveren futó lekéréses szolgáltatás</span><span class="sxs-lookup"><span data-stu-id="818d2-113">A pull service running on Windows Server</span></span>
- <span data-ttu-id="818d2-114">A Közösség által karbantartott nyílt forráskódú megoldások</span><span class="sxs-lookup"><span data-stu-id="818d2-114">Community maintained open-source solutions</span></span>
- <span data-ttu-id="818d2-115">SMB-megosztás</span><span class="sxs-lookup"><span data-stu-id="818d2-115">An SMB share</span></span>

<span data-ttu-id="818d2-116">**A javasolt megoldás**, valamint a legtöbb elérhető funkció, [Azure Automation DSC](/azure/automation/automation-dsc-getting-started).</span><span class="sxs-lookup"><span data-stu-id="818d2-116">**The recommended solution**, and the option with the most features available, is [Azure Automation DSC](/azure/automation/automation-dsc-getting-started).</span></span>

<span data-ttu-id="818d2-117">Az Azure-szolgáltatás a helyszíni csomópontokat a privát adatközpontokban vagy nyilvános felhőkben, például az Azure-ban és az AWS-ben is képes kezelni.</span><span class="sxs-lookup"><span data-stu-id="818d2-117">The Azure service can manage nodes on-premises in private datacenters, or in public clouds such as Azure and AWS.</span></span>
<span data-ttu-id="818d2-118">Olyan privát környezetekben, ahol a kiszolgálók nem tudnak közvetlenül csatlakozni az internethez, érdemes lehet csak a közzétett Azure IP-tartományra korlátozni a kimenő forgalmat (lásd: [Azure-adatközpont IP-címtartományok](https://www.microsoft.com/en-us/download/details.aspx?id=41653)).</span><span class="sxs-lookup"><span data-stu-id="818d2-118">For private environments where servers cannot directly connect to the Internet, consider limiting outbound traffic to only the published Azure IP range (see [Azure Datacenter IP Ranges](https://www.microsoft.com/en-us/download/details.aspx?id=41653)).</span></span>

<span data-ttu-id="818d2-119">A Windows Server lekéréses szolgáltatásában jelenleg nem elérhető online szolgáltatás szolgáltatásai a következők:</span><span class="sxs-lookup"><span data-stu-id="818d2-119">Features of the online service that are not currently available in the pull service on Windows Server include:</span></span>

- <span data-ttu-id="818d2-120">Minden adatforgalom titkosítva van az átvitel és a nyugalmi állapotban</span><span class="sxs-lookup"><span data-stu-id="818d2-120">All data is encrypted in transit and at rest</span></span>
- <span data-ttu-id="818d2-121">Az ügyféltanúsítványok automatikusan jönnek létre és kezelhetők</span><span class="sxs-lookup"><span data-stu-id="818d2-121">Client certificates are created and managed automatically</span></span>
- <span data-ttu-id="818d2-122">Secrets Store a jelszavak és a [hitelesítő adatok](/azure/automation/automation-credentials)központilag történő kezeléséhez, illetve [változókhoz](/azure/automation/automation-variables) , például kiszolgálónévekhez vagy a kapcsolatok karakterláncához</span><span class="sxs-lookup"><span data-stu-id="818d2-122">Secrets store for centrally managing [passwords/credentials](/azure/automation/automation-credentials), or [variables](/azure/automation/automation-variables) such as server names or connection strings</span></span>
- <span data-ttu-id="818d2-123">Csomópontos LCD- [konfiguráció](../managing-nodes/metaConfig.md#basic-settings) központi kezelése</span><span class="sxs-lookup"><span data-stu-id="818d2-123">Centrally manage node [LCM configuration](../managing-nodes/metaConfig.md#basic-settings)</span></span>
- <span data-ttu-id="818d2-124">Konfigurációk központi kiosztása az ügyfél csomópontjaihoz</span><span class="sxs-lookup"><span data-stu-id="818d2-124">Centrally assign configurations to client nodes</span></span>
- <span data-ttu-id="818d2-125">A "Kanári-csoportokra" vonatkozó konfigurációs változások kiadása az éles környezet elérése előtt</span><span class="sxs-lookup"><span data-stu-id="818d2-125">Release configuration changes to "canary groups" for testing before reaching production</span></span>
- <span data-ttu-id="818d2-126">Grafikus jelentéskészítés</span><span class="sxs-lookup"><span data-stu-id="818d2-126">Graphical reporting</span></span>
  - <span data-ttu-id="818d2-127">A részletességi szintű DSC-erőforrás részletességi állapota</span><span class="sxs-lookup"><span data-stu-id="818d2-127">Status detail at the DSC resource level of granularity</span></span>
  - <span data-ttu-id="818d2-128">Részletes hibaüzenetek az ügyfélszámítógépektől a hibaelhárításhoz</span><span class="sxs-lookup"><span data-stu-id="818d2-128">Verbose error messages from client machines for troubleshooting</span></span>
- <span data-ttu-id="818d2-129">[Integráció az Azure log Analytics](/azure/automation/automation-dsc-diagnostics) a riasztásokhoz, automatizált feladatokhoz, Android/iOS-alkalmazásokhoz jelentéskészítéshez és riasztásokhoz</span><span class="sxs-lookup"><span data-stu-id="818d2-129">[Integration with Azure Log Analytics](/azure/automation/automation-dsc-diagnostics) for alerting, automated tasks, Android/iOS app for reporting and alerting</span></span>

## <a name="dsc-pull-service-in-windows-server"></a><span data-ttu-id="818d2-130">DSC lekéréses szolgáltatás a Windows Server rendszerben</span><span class="sxs-lookup"><span data-stu-id="818d2-130">DSC pull service in Windows Server</span></span>

<span data-ttu-id="818d2-131">A lekéréses szolgáltatás beállítható úgy, hogy a Windows Serveren fusson.</span><span class="sxs-lookup"><span data-stu-id="818d2-131">It is possible to configure a pull service to run on Windows Server.</span></span>
<span data-ttu-id="818d2-132">Javasoljuk, hogy a Windows Serverben található lekéréses szolgáltatási megoldás csak a konfigurációk/modulok tárolására szolgáló képességeket tartalmazza, amelyekkel letöltheti és rögzítheti a jelentési adatmennyiségeket az adatbázisba.</span><span class="sxs-lookup"><span data-stu-id="818d2-132">Be advised that the pull service solution included in Windows Server includes only capabilities of storing configurations/modules for download and capturing report data in to database.</span></span>
<span data-ttu-id="818d2-133">Nem tartalmazza a szolgáltatás által az Azure-ban kínált számos képességet, ezért nem jó eszköz a szolgáltatás használatának kiértékeléséhez.</span><span class="sxs-lookup"><span data-stu-id="818d2-133">It does not include many of the capabilities offered by the service in Azure and so is not a good tool for evaluating how the service would be used.</span></span>

<span data-ttu-id="818d2-134">A Windows Server rendszerben kínált lekéréses szolgáltatás egy OData felületet használó webszolgáltatás, amely a DSC konfigurációs fájljait elérhetővé teszi a célként megadott csomópontok számára, amikor ezek a csomópontok kérik őket.</span><span class="sxs-lookup"><span data-stu-id="818d2-134">The pull service offered in Windows Server is a web service in IIS that uses an OData interface to make DSC configuration files available to target nodes when those nodes ask for them.</span></span>

<span data-ttu-id="818d2-135">A lekéréses kiszolgáló használatára vonatkozó követelmények:</span><span class="sxs-lookup"><span data-stu-id="818d2-135">Requirements for using a pull server:</span></span>

- <span data-ttu-id="818d2-136">Egy rendszert futtató kiszolgáló:</span><span class="sxs-lookup"><span data-stu-id="818d2-136">A server running:</span></span>
  - <span data-ttu-id="818d2-137">WMF/PowerShell 4,0 vagy újabb</span><span class="sxs-lookup"><span data-stu-id="818d2-137">WMF/PowerShell 4.0 or greater</span></span>
  - <span data-ttu-id="818d2-138">IIS-kiszolgálói szerepkör</span><span class="sxs-lookup"><span data-stu-id="818d2-138">IIS server role</span></span>
  - <span data-ttu-id="818d2-139">DSC szolgáltatás</span><span class="sxs-lookup"><span data-stu-id="818d2-139">DSC Service</span></span>
- <span data-ttu-id="818d2-140">Ideális esetben a tanúsítvány előállításához szükséges hitelesítő adatok biztonságossá tétele a helyi Configuration Manager (LCD ChipOnGlas) számára a célként megadott csomópontokon</span><span class="sxs-lookup"><span data-stu-id="818d2-140">Ideally, some means of generating a certificate, to secure credentials passed to the Local Configuration Manager (LCM) on target nodes</span></span>

<span data-ttu-id="818d2-141">A Windows Server lekéréses szolgáltatásként való konfigurálásának legjobb módja a DSC-konfiguráció használata.</span><span class="sxs-lookup"><span data-stu-id="818d2-141">The best way to configure Windows Server to host pull service is to use a DSC configuration.</span></span>
<span data-ttu-id="818d2-142">Alább talál egy példát a parancsfájlra.</span><span class="sxs-lookup"><span data-stu-id="818d2-142">An example script is provided below.</span></span>

### <a name="supported-database-systems"></a><span data-ttu-id="818d2-143">Támogatott adatbázis-rendszerek</span><span class="sxs-lookup"><span data-stu-id="818d2-143">Supported database systems</span></span>

|<span data-ttu-id="818d2-144">WMF 4.0</span><span class="sxs-lookup"><span data-stu-id="818d2-144">WMF 4.0</span></span>   |<span data-ttu-id="818d2-145">WMF 5.0</span><span class="sxs-lookup"><span data-stu-id="818d2-145">WMF 5.0</span></span>  |<span data-ttu-id="818d2-146">WMF 5.1</span><span class="sxs-lookup"><span data-stu-id="818d2-146">WMF 5.1</span></span> |<span data-ttu-id="818d2-147">WMF 5,1 (Windows Server Insider előzetes verzió 17090)</span><span class="sxs-lookup"><span data-stu-id="818d2-147">WMF 5.1 (Windows Server Insider Preview 17090)</span></span>|
|---------|---------|---------|---------|
|<span data-ttu-id="818d2-148">MDB</span><span class="sxs-lookup"><span data-stu-id="818d2-148">MDB</span></span>     |<span data-ttu-id="818d2-149">ESENT (alapértelmezett), MDB</span><span class="sxs-lookup"><span data-stu-id="818d2-149">ESENT (Default), MDB</span></span> |<span data-ttu-id="818d2-150">ESENT (alapértelmezett), MDB</span><span class="sxs-lookup"><span data-stu-id="818d2-150">ESENT (Default), MDB</span></span>|<span data-ttu-id="818d2-151">ESENT (alapértelmezett), SQL Server, MDB</span><span class="sxs-lookup"><span data-stu-id="818d2-151">ESENT (Default), SQL Server, MDB</span></span>

<span data-ttu-id="818d2-152">A [Windows Server Insider előzetes](https://www.microsoft.com/en-us/software-download/windowsinsiderpreviewserver)verziójának 17090-es verziójától kezdve SQL Server a lekéréses szolgáltatás (Windows-szolgáltatás *DSC-Service*) támogatott lehetősége.</span><span class="sxs-lookup"><span data-stu-id="818d2-152">Starting in release 17090 of [Windows Server Insider Preview](https://www.microsoft.com/en-us/software-download/windowsinsiderpreviewserver), SQL Server is a supported option for the Pull Service (Windows Feature *DSC-Service*).</span></span> <span data-ttu-id="818d2-153">Ez új lehetőséget biztosít a nagy DSC-környezetek méretezésére, amelyek nem lettek áttelepítve a [DSC-Azure Automation](/azure/automation/automation-dsc-getting-started).</span><span class="sxs-lookup"><span data-stu-id="818d2-153">This provides a new option for scaling large DSC environments that have not migrated to [Azure Automation DSC](/azure/automation/automation-dsc-getting-started).</span></span>

> [!NOTE]
> <span data-ttu-id="818d2-154">SQL Server támogatás nem lesz hozzáadva a WMF 5,1 korábbi verzióihoz (vagy korábbi verziókhoz), és csak a 17090-nál nagyobb vagy azzal egyenlő Windows Server-verziókban lesz elérhető.</span><span class="sxs-lookup"><span data-stu-id="818d2-154">SQL Server support will not be added to previous versions of WMF 5.1 (or earlier) and will only be available on Windows Server versions greater than or equal to 17090.</span></span>

<span data-ttu-id="818d2-155">A lekéréses kiszolgáló a SQL Server használatára való konfigurálásához állítsa `$true` a **SqlProvider** és a **sqlConnectionString** érvényes SQL Server-kapcsolódási karakterláncra.</span><span class="sxs-lookup"><span data-stu-id="818d2-155">To configure the pull server to use SQL Server, set **SqlProvider** to `$true` and **SqlConnectionString** to a valid SQL Server Connection String.</span></span> <span data-ttu-id="818d2-156">További információ: SqlClient- [kapcsolatok karakterláncai](/dotnet/framework/data/adonet/connection-string-syntax#sqlclient-connection-strings).</span><span class="sxs-lookup"><span data-stu-id="818d2-156">For more information, see [SqlClient Connection Strings](/dotnet/framework/data/adonet/connection-string-syntax#sqlclient-connection-strings).</span></span>
<span data-ttu-id="818d2-157">A **xDscWebService**-vel való SQL Server konfigurációra például először olvassa el [a xDscWebService](#using-the-xdscwebservice-resource) -erőforrást, majd tekintse át a [Sample_xDscWebServiceRegistration_UseSQLProvider. ps1 programot a githubon](https://github.com/PowerShell/xPSDesiredStateConfiguration/blob/master/Examples/Sample_xDscWebServiceRegistration_UseSQLProvider.ps1).</span><span class="sxs-lookup"><span data-stu-id="818d2-157">For an example of SQL Server configuration with **xDscWebService**, first read [Using the xDscWebService resource](#using-the-xdscwebservice-resource) and then review [Sample_xDscWebServiceRegistration_UseSQLProvider.ps1 on GitHub](https://github.com/PowerShell/xPSDesiredStateConfiguration/blob/master/Examples/Sample_xDscWebServiceRegistration_UseSQLProvider.ps1).</span></span>

### <a name="using-the-xdscwebservice-resource"></a><span data-ttu-id="818d2-158">A xDscWebService erőforrás használata</span><span class="sxs-lookup"><span data-stu-id="818d2-158">Using the xDscWebService resource</span></span>

<span data-ttu-id="818d2-159">A web pull-kiszolgáló beállításának legegyszerűbb módja a **xPSDesiredStateConfiguration** modulban található **xDscWebService** -erőforrás használata.</span><span class="sxs-lookup"><span data-stu-id="818d2-159">The easiest way to set up a web pull server is to use the **xDscWebService** resource, included in the **xPSDesiredStateConfiguration** module.</span></span>
<span data-ttu-id="818d2-160">A következő lépések azt ismertetik, hogyan használható az erőforrás egy olyan konfigurációban, amely beállítja a webszolgáltatást.</span><span class="sxs-lookup"><span data-stu-id="818d2-160">The following steps explain how to use the resource in a configuration that sets up the web service.</span></span>

1. <span data-ttu-id="818d2-161">A **xPSDesiredStateConfiguration** modul telepítéséhez hívja meg az [install-Module](/powershell/module/PowershellGet/Install-Module) parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="818d2-161">Call the [Install-Module](/powershell/module/PowershellGet/Install-Module) cmdlet to install the **xPSDesiredStateConfiguration** module.</span></span>
   > [!NOTE]
   > <span data-ttu-id="818d2-162">A **install-Module** a PowerShell 5,0 részét képező **PowerShellGet** modul része.</span><span class="sxs-lookup"><span data-stu-id="818d2-162">**Install-Module** is included in the **PowerShellGet** module, which is included in PowerShell 5.0.</span></span> <span data-ttu-id="818d2-163">A PowerShell 3,0-es és 4,0-es **PowerShellGet** -modulját a [PackageManagement PowerShell-modulok előzetes](https://www.microsoft.com/en-us/download/details.aspx?id=49186)verziójában töltheti le.</span><span class="sxs-lookup"><span data-stu-id="818d2-163">You can download the **PowerShellGet** module for PowerShell 3.0 and 4.0 at [PackageManagement PowerShell Modules Preview](https://www.microsoft.com/en-us/download/details.aspx?id=49186).</span></span>
2. <span data-ttu-id="818d2-164">Szerezze be a DSC lekérési kiszolgálójának SSL-tanúsítványát egy megbízható hitelesítésszolgáltatótól, akár a szervezetén belül, akár egy nyilvános szolgáltatóban.</span><span class="sxs-lookup"><span data-stu-id="818d2-164">Get an SSL certificate for the DSC Pull server from a trusted Certificate Authority, either within your organization or a public authority.</span></span> <span data-ttu-id="818d2-165">A szolgáltatótól kapott tanúsítvány általában PFX formátumú.</span><span class="sxs-lookup"><span data-stu-id="818d2-165">The certificate received from the authority is usually in the PFX format.</span></span>
3. <span data-ttu-id="818d2-166">Telepítse a tanúsítványt azon a csomóponton, amely a DSC lekérési kiszolgáló lesz az alapértelmezett helyen, amelynek `CERT:\LocalMachine\My`a következőnek kell lennie:.</span><span class="sxs-lookup"><span data-stu-id="818d2-166">Install the certificate on the node that will become the DSC Pull server in the default location, which should be `CERT:\LocalMachine\My`.</span></span>
   - <span data-ttu-id="818d2-167">Jegyezze fel a tanúsítvány ujjlenyomatát.</span><span class="sxs-lookup"><span data-stu-id="818d2-167">Make a note of the certificate thumbprint.</span></span>
4. <span data-ttu-id="818d2-168">Válassza ki a regisztrációs kulcsként használni kívánt GUID azonosítót.</span><span class="sxs-lookup"><span data-stu-id="818d2-168">Select a GUID to be used as the Registration Key.</span></span> <span data-ttu-id="818d2-169">A PowerShell használatával történő létrehozáshoz írja be a következőt a PS parancssorba, `[guid]::newGuid()` majd `New-Guid`nyomja le az ENTER billentyűt: vagy.</span><span class="sxs-lookup"><span data-stu-id="818d2-169">To generate one using PowerShell enter the following at the PS prompt and press enter: `[guid]::newGuid()` or `New-Guid`.</span></span> <span data-ttu-id="818d2-170">Ezt a kulcsot az ügyféloldali csomópontok használják megosztott kulcsként a regisztráció során történő hitelesítéshez.</span><span class="sxs-lookup"><span data-stu-id="818d2-170">This key will be used by client nodes as a shared key to authenticate during registration.</span></span> <span data-ttu-id="818d2-171">További információt az alábbi regisztrációs kulcs című szakaszban talál.</span><span class="sxs-lookup"><span data-stu-id="818d2-171">For more information, see the Registration Key section below.</span></span>
5. <span data-ttu-id="818d2-172">A PowerShell ISE-ben indítsa el (F5) a következő konfigurációs szkriptet (a **xPSDesiredStateConfiguration** modul `Sample_xDscWebServiceRegistration.ps1`példák mappájába).</span><span class="sxs-lookup"><span data-stu-id="818d2-172">In the PowerShell ISE, start (F5) the following configuration script (included in the Examples folder of the **xPSDesiredStateConfiguration** module as `Sample_xDscWebServiceRegistration.ps1`).</span></span> <span data-ttu-id="818d2-173">Ez a szkript beállítja a lekérési kiszolgálót.</span><span class="sxs-lookup"><span data-stu-id="818d2-173">This script sets up the pull server.</span></span>

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

6. <span data-ttu-id="818d2-174">Futtassa a konfigurációt, és adja át az SSL-tanúsítvány ujjlenyomatát a **certificateThumbPrint** paraméterként, valamint egy GUID regisztrációs kulcsot a **RegistrationKey** paraméterként:</span><span class="sxs-lookup"><span data-stu-id="818d2-174">Run the configuration, passing the thumbprint of the SSL certificate as the **certificateThumbPrint** parameter and a GUID registration key as the **RegistrationKey** parameter:</span></span>

    ```powershell
    # To find the Thumbprint for an installed SSL certificate for use with the pull server list all certificates in your local store
    # and then copy the thumbprint for the appropriate certificate by reviewing the certificate subjects
    dir Cert:\LocalMachine\my

    # Then include this thumbprint when running the configuration
    Sample_xDscWebServiceRegistration -certificateThumbprint 'A7000024B753FA6FFF88E966FD6E19301FAE9CCC' -RegistrationKey '140a952b-b9d6-406b-b416-e0f759c9c0e4' -OutputPath c:\Configs\PullServer

    # Run the compiled configuration to make the target node a DSC Pull Server
    Start-DscConfiguration -Path c:\Configs\PullServer -Wait -Verbose
    ```

#### <a name="registration-key"></a><span data-ttu-id="818d2-175">Regisztrációs kulcs</span><span class="sxs-lookup"><span data-stu-id="818d2-175">Registration Key</span></span>

<span data-ttu-id="818d2-176">Annak engedélyezéséhez, hogy az ügyféloldali csomópontok regisztráljanak a- `RegistrationKeys.txt` `C:\Program Files\WindowsPowerShell\DscService`kiszolgálóval, hogy a konfigurációs neveket a konfigurációs azonosító helyett tudják használni, a fenti konfiguráció által létrehozott regisztrációs kulcsot a rendszer menti egy nevű fájlba.</span><span class="sxs-lookup"><span data-stu-id="818d2-176">To allow client nodes to register with the server so that they can use configuration names instead of a configuration ID, a registration key that was created by the above configuration is saved in a file named `RegistrationKeys.txt` in `C:\Program Files\WindowsPowerShell\DscService`.</span></span> <span data-ttu-id="818d2-177">A regisztrációs kulcs olyan közös titokként működik, amelyet az ügyfél a lekérési kiszolgálóval végzett kezdeti regisztráció során használt.</span><span class="sxs-lookup"><span data-stu-id="818d2-177">The registration key functions as a shared secret used during the initial registration by the client with the pull server.</span></span> <span data-ttu-id="818d2-178">Az ügyfél olyan önaláírt tanúsítványt fog előállítani, amelyet a rendszer a lekéréses kiszolgáló egyedi hitelesítéséhez használ a regisztráció sikeres befejeződése után.</span><span class="sxs-lookup"><span data-stu-id="818d2-178">The client will generate a self-signed certificate that is used to uniquely authenticate to the pull server once registration is successfully completed.</span></span> <span data-ttu-id="818d2-179">A Tanúsítvány ujjlenyomata helyileg tárolódik, és a lekérési kiszolgáló URL-címéhez van társítva.</span><span class="sxs-lookup"><span data-stu-id="818d2-179">The thumbprint of this certificate is stored locally and associated with the URL of the pull server.</span></span>

> [!NOTE]
> <span data-ttu-id="818d2-180">A regisztrációs kulcsok nem támogatottak a PowerShell 4,0-ben.</span><span class="sxs-lookup"><span data-stu-id="818d2-180">Registration keys are not supported in PowerShell 4.0.</span></span>

<span data-ttu-id="818d2-181">Ahhoz, hogy a csomópontot a lekérési kiszolgálóval való hitelesítésre konfigurálja, a regisztrációs kulcsnak a lekérési kiszolgálóval regisztrálni kívánt metaconfiguration kell lennie.</span><span class="sxs-lookup"><span data-stu-id="818d2-181">In order to configure a node to authenticate with the pull server, the registration key needs to be in the metaconfiguration for any target node that will be registering with this pull server.</span></span> <span data-ttu-id="818d2-182">Vegye figyelembe, hogy az alábbi metaconfiguration lévő **RegistrationKey** a célszámítógép sikeres regisztrálását követően törlődik, és az értéknek meg kell egyeznie a lekérési kiszolgálón található `RegistrationKeys.txt` fájlban tárolt értékkel (" 140a952b-b9d6-406b-b416-e0f759c9c0e4 "ebben a példában).</span><span class="sxs-lookup"><span data-stu-id="818d2-182">Note that the **RegistrationKey** in the metaconfiguration below is removed after the target machine has successfully registered, and that the value must match the value stored in the `RegistrationKeys.txt` file on the pull server ('140a952b-b9d6-406b-b416-e0f759c9c0e4' for this example).</span></span> <span data-ttu-id="818d2-183">Mindig biztonságos módon kezelje a regisztrációs kulcs értékét, mert tudván, hogy bármely célszámítógép regisztrálható a lekérési kiszolgálón.</span><span class="sxs-lookup"><span data-stu-id="818d2-183">Always treat the registration key value securely, because knowing it allows any target machine to register with the pull server.</span></span>

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
> <span data-ttu-id="818d2-184">A **ReportServerWeb** szakasz lehetővé teszi jelentéskészítési adatküldés küldését a lekérési kiszolgálónak.</span><span class="sxs-lookup"><span data-stu-id="818d2-184">The **ReportServerWeb** section allows reporting data to be sent to the pull server.</span></span>

<span data-ttu-id="818d2-185">A metaconfiguration fájl **ConfigurationID** tulajdonságának hiánya implicit módon azt jelenti, hogy a lekérési kiszolgáló támogatja a lekérési kiszolgáló protokolljának v2-es verzióját, így kezdeti regisztrációra van szükség.</span><span class="sxs-lookup"><span data-stu-id="818d2-185">The lack of the **ConfigurationID** property in the metaconfiguration file implicitly means that pull server is supporting the V2 version of the pull server protocol so an initial registration is required.</span></span>
<span data-ttu-id="818d2-186">Ezzel szemben a **ConfigurationID** jelenléte azt jelenti, hogy a lekéréses kiszolgáló protokolljának v1-es verziója van használatban, és nincs regisztrációs feldolgozás.</span><span class="sxs-lookup"><span data-stu-id="818d2-186">Conversely, the presence of a **ConfigurationID** means that the V1 version of the pull server protocol is used and there is no registration processing.</span></span>

> [!NOTE]
> <span data-ttu-id="818d2-187">Egy leküldéses forgatókönyvben hiba történt a jelenlegi kiadásban, amely szükségessé teszi a ConfigurationID tulajdonság definiálását a metaconfiguration-fájlban olyan csomópontok esetében, amelyek még nem regisztráltak lekéréses kiszolgálóval.</span><span class="sxs-lookup"><span data-stu-id="818d2-187">In a PUSH scenario, a bug exists in the current release that makes it necessary to define a ConfigurationID property in the metaconfiguration file for nodes that have never registered with a pull server.</span></span> <span data-ttu-id="818d2-188">Ez kényszeríti a v1 lekéréses kiszolgáló protokollját, és elkerüli a regisztrációs hibák üzeneteit.</span><span class="sxs-lookup"><span data-stu-id="818d2-188">This will force the V1 Pull Server protocol and avoid registration failure messages.</span></span>

## <a name="placing-configurations-and-resources"></a><span data-ttu-id="818d2-189">Konfigurációk és erőforrások elhelyezése</span><span class="sxs-lookup"><span data-stu-id="818d2-189">Placing configurations and resources</span></span>

<span data-ttu-id="818d2-190">A lekérési kiszolgáló telepítésének befejezése után a lekérési kiszolgáló konfigurációjában a **ConfigurationPath** és a **ModulePath** tulajdonság által meghatározott mappák a lekéréses csomópontok számára elérhető modulok és konfigurációk helyét fogják elhelyezni.</span><span class="sxs-lookup"><span data-stu-id="818d2-190">After the pull server setup completes, the folders defined by the **ConfigurationPath** and **ModulePath** properties in the pull server configuration are where you will place modules and configurations that will be available for target nodes to pull.</span></span>
<span data-ttu-id="818d2-191">Ezeknek a fájloknak egy adott formátumban kell lenniük ahhoz, hogy a lekérési kiszolgáló megfelelően feldolgozza őket.</span><span class="sxs-lookup"><span data-stu-id="818d2-191">These files need to be in a specific format in order for the pull server to correctly process them.</span></span>

### <a name="dsc-resource-module-package-format"></a><span data-ttu-id="818d2-192">DSC erőforrás modul csomag formátuma</span><span class="sxs-lookup"><span data-stu-id="818d2-192">DSC resource module package format</span></span>

<span data-ttu-id="818d2-193">Az egyes erőforrás-modulokat a következő minta `{Module Name}_{Module Version}.zip`szerint kell kibontani és elnevezni.</span><span class="sxs-lookup"><span data-stu-id="818d2-193">Each resource module needs to be zipped and named according to the following pattern `{Module Name}_{Module Version}.zip`.</span></span>

<span data-ttu-id="818d2-194">Például egy xWebAdminstration nevű modul, amely a 3.1.2.0 modul verzióját fogja nevezni `xWebAdministration_3.1.2.0.zip`.</span><span class="sxs-lookup"><span data-stu-id="818d2-194">For example, a module named xWebAdminstration with a module version of 3.1.2.0 would be named `xWebAdministration_3.1.2.0.zip`.</span></span>
<span data-ttu-id="818d2-195">Egy modul minden egyes verziójának egyetlen zip-fájlban kell szerepelnie.</span><span class="sxs-lookup"><span data-stu-id="818d2-195">Each version of a module must be contained in a single zip file.</span></span>
<span data-ttu-id="818d2-196">Mivel az egyes zip-fájlokban csak egyetlen verziójú erőforrás található, a WMF 5,0-ben hozzáadott modul formátuma nem támogatott egyetlen címtárban.</span><span class="sxs-lookup"><span data-stu-id="818d2-196">Since there is only a single version of a resource in each zip file, the module format added in WMF 5.0 with support for multiple module versions in a single directory is not supported.</span></span>
<span data-ttu-id="818d2-197">Ez azt jelenti, hogy a DSC-erőforrás moduljainak a lekérési kiszolgálón való használatának megkezdése előtt kis módosítást kell végeznie a címtár struktúráján.</span><span class="sxs-lookup"><span data-stu-id="818d2-197">This means that before packaging up DSC resource modules for use with pull server you will need to make a small change to the directory structure.</span></span>
<span data-ttu-id="818d2-198">A DSC-erőforrást tartalmazó modulok alapértelmezett formátuma a WMF `{Module Folder}\{Module Version}\DscResources\{DSC Resource Folder}\`5,0-ben.</span><span class="sxs-lookup"><span data-stu-id="818d2-198">The default format of modules containing DSC resource in WMF 5.0 is `{Module Folder}\{Module Version}\DscResources\{DSC Resource Folder}\`.</span></span>
<span data-ttu-id="818d2-199">A lekérési kiszolgáló csomagolása előtt távolítsa el a **{Module Version}** mappát, hogy `{Module Folder}\DscResources\{DSC Resource Folder}\`az elérési út legyen.</span><span class="sxs-lookup"><span data-stu-id="818d2-199">Before packaging up for the pull server, remove the **{Module version}** folder so the path becomes `{Module Folder}\DscResources\{DSC Resource Folder}\`.</span></span>
<span data-ttu-id="818d2-200">Ezzel a módosítással zip a mappát a fent leírtak szerint, és helyezze el ezeket a ZIP-fájlokat a **ModulePath** mappába.</span><span class="sxs-lookup"><span data-stu-id="818d2-200">With this change, zip the folder as described above and place these zip files in the **ModulePath** folder.</span></span>

<span data-ttu-id="818d2-201">A `New-DscChecksum {module zip file}` használatával hozzon létre egy ellenőrzőösszeg-fájlt az újonnan hozzáadott modulhoz.</span><span class="sxs-lookup"><span data-stu-id="818d2-201">Use `New-DscChecksum {module zip file}` to create a checksum file for the newly added module.</span></span>

### <a name="configuration-mof-format"></a><span data-ttu-id="818d2-202">Konfiguráció MOF-formátuma</span><span class="sxs-lookup"><span data-stu-id="818d2-202">Configuration MOF format</span></span>

<span data-ttu-id="818d2-203">A konfigurációs MOF-fájlt egy ellenőrzőösszeg-fájllal kell párosítani, hogy a célként megadott csomóponton lévő LCD-eszközök ellenőrizni tudják a konfigurációt.</span><span class="sxs-lookup"><span data-stu-id="818d2-203">A configuration MOF file needs to be paired with a checksum file so that an LCM on a target node can validate the configuration.</span></span>
<span data-ttu-id="818d2-204">Ellenőrzőösszeg létrehozásához hívja meg a [New-DscChecksum](/powershell/module/PSDesiredStateConfiguration/New-DscChecksum) parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="818d2-204">To create a checksum, call the [New-DscChecksum](/powershell/module/PSDesiredStateConfiguration/New-DscChecksum) cmdlet.</span></span>
<span data-ttu-id="818d2-205">A parancsmag egy **elérésiút** -paramétert használ, amely meghatározza azt a mappát, ahol a konfigurációs MOF található.</span><span class="sxs-lookup"><span data-stu-id="818d2-205">The cmdlet takes a **Path** parameter that specifies the folder where the configuration MOF is located.</span></span>
<span data-ttu-id="818d2-206">A parancsmag létrehoz egy nevű `ConfigurationMOFName.mof.checksum`ellenőrzőösszeg-fájlt, ahol `ConfigurationMOFName` a a konfigurációs MOF-fájl neve.</span><span class="sxs-lookup"><span data-stu-id="818d2-206">The cmdlet creates a checksum file named `ConfigurationMOFName.mof.checksum`, where `ConfigurationMOFName` is the name of the configuration mof file.</span></span>
<span data-ttu-id="818d2-207">Ha a megadott mappában több konfigurációs MOF-fájl található, akkor a mappában található minden egyes konfigurációhoz ellenőrzőösszeg jön létre.</span><span class="sxs-lookup"><span data-stu-id="818d2-207">If there are more than one configuration MOF files in the specified folder, a checksum is created for each configuration in the folder.</span></span>
<span data-ttu-id="818d2-208">Helyezze a MOF-fájlokat és a hozzájuk tartozó ellenőrzőösszeg-fájlokat a **ConfigurationPath** mappába.</span><span class="sxs-lookup"><span data-stu-id="818d2-208">Place the MOF files and their associated checksum files in the **ConfigurationPath** folder.</span></span>

> [!NOTE]
> <span data-ttu-id="818d2-209">Ha bármilyen módon módosítja a konfigurációs MOF-fájlt, akkor újra létre kell hoznia az ellenőrzőösszeg-fájlt is.</span><span class="sxs-lookup"><span data-stu-id="818d2-209">If you change the configuration MOF file in any way, you must also recreate the checksum file.</span></span>

### <a name="tooling"></a><span data-ttu-id="818d2-210">Eszközök</span><span class="sxs-lookup"><span data-stu-id="818d2-210">Tooling</span></span>

<span data-ttu-id="818d2-211">A lekéréses kiszolgáló telepítésének, ellenőrzésének és felügyeletének megkönnyítéséhez a következő eszközök szerepelnek példaként a xPSDesiredStateConfiguration modul legújabb verziójában:</span><span class="sxs-lookup"><span data-stu-id="818d2-211">In order to make setting up, validating and managing the pull server easier, the following tools are included as examples in the latest version of the xPSDesiredStateConfiguration module:</span></span>

1. <span data-ttu-id="818d2-212">Egy modul, amely segítséget nyújt a lekéréses kiszolgálón való használatra a DSC-erőforrás moduljainak és konfigurációs fájljainak használatához.</span><span class="sxs-lookup"><span data-stu-id="818d2-212">A module that will help with packaging DSC resource modules and configuration files for use on the pull server.</span></span>
   <span data-ttu-id="818d2-213">[PublishModulesAndMofsToPullServer.psm1](https://github.com/PowerShell/xPSDesiredStateConfiguration/blob/master/DSCPullServerSetup/PublishModulesAndMofsToPullServer.psm1).</span><span class="sxs-lookup"><span data-stu-id="818d2-213">[PublishModulesAndMofsToPullServer.psm1](https://github.com/PowerShell/xPSDesiredStateConfiguration/blob/master/DSCPullServerSetup/PublishModulesAndMofsToPullServer.psm1).</span></span>
   <span data-ttu-id="818d2-214">Példák alább:</span><span class="sxs-lookup"><span data-stu-id="818d2-214">Examples below:</span></span>

    ```powershell
        # Example 1 - Package all versions of given modules installed locally and MOF files are in c:\LocalDepot
         $moduleList = @('xWebAdministration', 'xPhp')
         Publish-DSCModuleAndMof -Source C:\LocalDepot -ModuleNameList $moduleList

         # Example 2 - Package modules and mof documents from c:\LocalDepot
         Publish-DSCModuleAndMof -Source C:\LocalDepot -Force
    ```

1. <span data-ttu-id="818d2-215">A lekérési kiszolgálót érvényesítő parancsfájl megfelelően van konfigurálva.</span><span class="sxs-lookup"><span data-stu-id="818d2-215">A script that validates the pull server is configured correctly.</span></span> <span data-ttu-id="818d2-216">[PullServerSetupTests. ps1](https://github.com/PowerShell/xPSDesiredStateConfiguration/blob/master/DSCPullServerSetup/PullServerDeploymentVerificationTest/PullServerSetupTests.ps1).</span><span class="sxs-lookup"><span data-stu-id="818d2-216">[PullServerSetupTests.ps1](https://github.com/PowerShell/xPSDesiredStateConfiguration/blob/master/DSCPullServerSetup/PullServerDeploymentVerificationTest/PullServerSetupTests.ps1).</span></span>

## <a name="community-solutions-for-pull-service"></a><span data-ttu-id="818d2-217">Közösségi megoldások a lekéréses szolgáltatáshoz</span><span class="sxs-lookup"><span data-stu-id="818d2-217">Community Solutions for Pull Service</span></span>

<span data-ttu-id="818d2-218">A DSC-Közösség több megoldást hozott létre a lekéréses szolgáltatás protokolljának megvalósításához.</span><span class="sxs-lookup"><span data-stu-id="818d2-218">The DSC community has authored multiple solutions to implement the pull service protocol.</span></span>
<span data-ttu-id="818d2-219">A helyszíni környezetek esetében ezek az ajánlatok lekéréses szolgáltatásokkal kapcsolatos képességeket és lehetőséget biztosítanak a Közösségnek a növekményes fejlesztésekkel való újbóli közreműködés érdekében.</span><span class="sxs-lookup"><span data-stu-id="818d2-219">For on-premises environments, these offer pull service capabilities and an opportunity to contribute back to the community with incremental enhancements.</span></span>

- [<span data-ttu-id="818d2-220">Vontatóhajó</span><span class="sxs-lookup"><span data-stu-id="818d2-220">Tug</span></span>](https://github.com/powershellorg/tug)
- [<span data-ttu-id="818d2-221">DSC-TRÆK</span><span class="sxs-lookup"><span data-stu-id="818d2-221">DSC-TRÆK</span></span>](https://github.com/powershellorg/dsc-traek)

## <a name="pull-client-configuration"></a><span data-ttu-id="818d2-222">Ügyfél konfigurációjának lekérése</span><span class="sxs-lookup"><span data-stu-id="818d2-222">Pull client configuration</span></span>

<span data-ttu-id="818d2-223">A következő témakörök részletesen ismertetik a lekéréses ügyfelek beállítását:</span><span class="sxs-lookup"><span data-stu-id="818d2-223">The following topics describe setting up pull clients in detail:</span></span>

- [<span data-ttu-id="818d2-224">DSC lekérési ügyfél beállítása konfigurációs azonosító használatával</span><span class="sxs-lookup"><span data-stu-id="818d2-224">Set up a DSC pull client using a configuration ID</span></span>](pullClientConfigID.md)
- [<span data-ttu-id="818d2-225">DSC lekérési ügyfél beállítása konfigurációs nevek használatával</span><span class="sxs-lookup"><span data-stu-id="818d2-225">Set up a DSC pull client using configuration names</span></span>](pullClientConfigNames.md)
- [<span data-ttu-id="818d2-226">Részleges konfigurációk</span><span class="sxs-lookup"><span data-stu-id="818d2-226">Partial configurations</span></span>](partialConfigs.md)

## <a name="see-also"></a><span data-ttu-id="818d2-227">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="818d2-227">See also</span></span>

- [<span data-ttu-id="818d2-228">A Windows PowerShell kívánt állapotának konfigurálása – áttekintés</span><span class="sxs-lookup"><span data-stu-id="818d2-228">Windows PowerShell Desired State Configuration Overview</span></span>](../overview/overview.md)
- [<span data-ttu-id="818d2-229">Konfigurációk életbe léptetése</span><span class="sxs-lookup"><span data-stu-id="818d2-229">Enacting configurations</span></span>](enactingConfigurations.md)
- [<span data-ttu-id="818d2-230">A DSC jelentéskészítő kiszolgálójának használata</span><span class="sxs-lookup"><span data-stu-id="818d2-230">Using a DSC report server</span></span>](reportServer.md)
- <span data-ttu-id="818d2-231">[[MS-DSCPM]: A kívánt állapot konfigurációjának lekérési modellje protokoll](https://msdn.microsoft.com/library/dn393548.aspx)</span><span class="sxs-lookup"><span data-stu-id="818d2-231">[[MS-DSCPM]: Desired State Configuration Pull Model Protocol](https://msdn.microsoft.com/library/dn393548.aspx)</span></span>
- <span data-ttu-id="818d2-232">[[MS-DSCPM]: A kívánt állapot konfigurációjának lekérése modell protokolljának hibajavításai](https://msdn.microsoft.com/library/mt612824.aspx)</span><span class="sxs-lookup"><span data-stu-id="818d2-232">[[MS-DSCPM]: Desired State Configuration Pull Model Protocol Errata](https://msdn.microsoft.com/library/mt612824.aspx)</span></span>
