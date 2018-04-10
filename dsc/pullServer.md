---
ms.date: 02/02/2018
ms.topic: conceptual
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: DSC Pull Service
ms.openlocfilehash: 1547092d5ea6733296bf89f05dd96f70c0a000ac
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="desired-state-configuration-pull-service"></a><span data-ttu-id="66352-103">Célállapot-konfiguráló lekéréses szolgáltatása</span><span class="sxs-lookup"><span data-stu-id="66352-103">Desired State Configuration Pull Service</span></span>

> <span data-ttu-id="66352-104">Vonatkozik: A Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="66352-104">Applies To: Windows PowerShell 5.0</span></span>

<span data-ttu-id="66352-105">Helyi Configuration Manager Service lekéréses megoldás központilag kezelhető.</span><span class="sxs-lookup"><span data-stu-id="66352-105">Local Configuration Manager can be centrally managed by a Pull Service solution.</span></span>
<span data-ttu-id="66352-106">Ez a módszer használata esetén a csomópont kezelt regisztrálva a szolgáltatásban, és LCM beállítások a konfigurációs hozzárendelni.</span><span class="sxs-lookup"><span data-stu-id="66352-106">When using this approach, the node that is being managed is registered with a service and assigned a configuration in LCM settings.</span></span>
<span data-ttu-id="66352-107">A konfiguráció szerint függőségeinek a konfigurációs szükséges összes DSC erőforrásokat a számítógép letölti és LCM felügyelje a konfigurációt használja.</span><span class="sxs-lookup"><span data-stu-id="66352-107">The configuration and all DSC resources needed as dependencies for the configuration are downloaded to the machine and used by LCM to manage the configuration.</span></span>
<span data-ttu-id="66352-108">A felügyelt számítógép állapotára vonatkozó adatokat tölt fel az a jelentéskészítés szolgáltatás.</span><span class="sxs-lookup"><span data-stu-id="66352-108">Information about the state of the machine being managed is uploaded to the service for reporting.</span></span>
<span data-ttu-id="66352-109">A fogalom "lekéréses szolgáltatás" nevezzük.</span><span class="sxs-lookup"><span data-stu-id="66352-109">This concept is referred to as "pull service".</span></span>

<span data-ttu-id="66352-110">Az aktuális lekéréses szolgáltatás beállításai a következők:</span><span class="sxs-lookup"><span data-stu-id="66352-110">The current options for pull service include:</span></span>

- <span data-ttu-id="66352-111">Azure Automation kívánt állapot konfigurációs szolgáltatás</span><span class="sxs-lookup"><span data-stu-id="66352-111">Azure Automation Desired State Configuration service</span></span>
- <span data-ttu-id="66352-112">Windows Server rendszeren futó lekéréses szolgáltatás</span><span class="sxs-lookup"><span data-stu-id="66352-112">A pull service running on Windows Server</span></span>
- <span data-ttu-id="66352-113">Közösségi Megnyitás megoldások karbantartása</span><span class="sxs-lookup"><span data-stu-id="66352-113">Community maintained open source solutions</span></span>
- <span data-ttu-id="66352-114">SMB-megosztáson</span><span class="sxs-lookup"><span data-stu-id="66352-114">An SMB share</span></span>

<span data-ttu-id="66352-115">**Az ajánlott megoldás**, és a lehetőség érhető el, a legtöbb szolgáltatásokkal [Azure Automation DSC](https://docs.microsoft.com/en-us/azure/automation/automation-dsc-getting-started).</span><span class="sxs-lookup"><span data-stu-id="66352-115">**The recommended solution**, and the option with the most features available, is [Azure Automation DSC](https://docs.microsoft.com/en-us/azure/automation/automation-dsc-getting-started).</span></span>

<span data-ttu-id="66352-116">Az Azure-szolgáltatás csomópontok helyszíni saját adatközpontját, illetve például az Azure és az AWS nyilvános felhőket is kezelheti.</span><span class="sxs-lookup"><span data-stu-id="66352-116">The Azure service can manage nodes on-premises in private datacenters, or in public clouds such as Azure and AWS.</span></span>
<span data-ttu-id="66352-117">Személyes környezetekben, ahol kiszolgálók nem közvetlenül csatlakozik az internethez, fontolja meg, ezzel a kimenő forgalom csak a közzétett Azure IP-címtartomány (lásd: [Azure Datacenter IP-címtartományok](https://www.microsoft.com/en-us/download/details.aspx?id=41653)).</span><span class="sxs-lookup"><span data-stu-id="66352-117">For private environments where servers cannot directly connect to the Internet, consider limiting outbound traffic to only the published Azure IP range (see [Azure Datacenter IP Ranges](https://www.microsoft.com/en-us/download/details.aspx?id=41653)).</span></span>

<span data-ttu-id="66352-118">Az online szolgáltatás, amely még nem állnak rendelkezésre az lekéréses szolgáltatásban, a Windows Server funkciói:</span><span class="sxs-lookup"><span data-stu-id="66352-118">Features of the online service that are not currently available in the pull service on Windows Server include:</span></span>
- <span data-ttu-id="66352-119">Összes adata titkosításra kerül az átvitel során, és inaktív</span><span class="sxs-lookup"><span data-stu-id="66352-119">All data is encrypted in transit and at rest</span></span>
- <span data-ttu-id="66352-120">Ügyfél-tanúsítványok létrehozása és kezelése automatikusan</span><span class="sxs-lookup"><span data-stu-id="66352-120">Client certificates are created and managed automatically</span></span>
- <span data-ttu-id="66352-121">Titkos kulcsok tárolására központilag kezelésére szolgáló [jelszavak és a hitelesítő adatok](https://docs.microsoft.com/en-us/azure/automation/automation-credentials), vagy [változók](https://docs.microsoft.com/en-us/azure/automation/automation-variables) például a kiszolgáló nevét vagy a kapcsolati karakterláncok</span><span class="sxs-lookup"><span data-stu-id="66352-121">Secrets store for centrally managing [passwords/credentials](https://docs.microsoft.com/en-us/azure/automation/automation-credentials), or [variables](https://docs.microsoft.com/en-us/azure/automation/automation-variables) such as server names or connection strings</span></span>
- <span data-ttu-id="66352-122">Központilag kezelheti a csomópont [LCM konfiguráció](metaConfig.md#basic-settings)</span><span class="sxs-lookup"><span data-stu-id="66352-122">Centrally manage node [LCM configuration](metaConfig.md#basic-settings)</span></span>
- <span data-ttu-id="66352-123">Központilag konfigurációk kiosztása ügyfél csomópontok</span><span class="sxs-lookup"><span data-stu-id="66352-123">Centrally assign configurations to client nodes</span></span>
- <span data-ttu-id="66352-124">Kiadás configuration "Kanári csoportok" éles elérése előtt tesztelési módosításai</span><span class="sxs-lookup"><span data-stu-id="66352-124">Release configuration changes to "canary groups" for testing before reaching production</span></span>
- <span data-ttu-id="66352-125">Grafikus jelentési</span><span class="sxs-lookup"><span data-stu-id="66352-125">Graphical reporting</span></span>
  - <span data-ttu-id="66352-126">A granularitási DSC erőforrás szintjén állapotának részletei</span><span class="sxs-lookup"><span data-stu-id="66352-126">Status detail at the DSC resource level of granularity</span></span>
  - <span data-ttu-id="66352-127">Az ügyfél gépek hibaelhárítási részletes hibaüzenetek</span><span class="sxs-lookup"><span data-stu-id="66352-127">Verbose error messages from client machines for troubleshooting</span></span>
- <span data-ttu-id="66352-128">[Integráció az Azure Naplóelemzés](https://docs.microsoft.com/en-us/azure/automation/automation-dsc-diagnostics) riasztások, automatikus feladatokat, jelentések és riasztási Android vagy iOS-alkalmazás</span><span class="sxs-lookup"><span data-stu-id="66352-128">[Integration with Azure Log Analytics](https://docs.microsoft.com/en-us/azure/automation/automation-dsc-diagnostics) for alerting, automated tasks, Android/iOS app for reporting and alerting</span></span>

## <a name="dsc-pull-service-in-windows-server"></a><span data-ttu-id="66352-129">A DSC lekérési szolgáltatás a Windows Server</span><span class="sxs-lookup"><span data-stu-id="66352-129">DSC pull service in Windows Server</span></span>

<span data-ttu-id="66352-130">Akkor lehet egy lekéréses szolgáltatást, hogy a Windows Serveren futó konfigurálására.</span><span class="sxs-lookup"><span data-stu-id="66352-130">It is possible to configuring a pull service to run on Windows Server.</span></span>
<span data-ttu-id="66352-131">Adjon kell azt javasoljuk, hogy a lekéréses service megoldás a Windows Serverben megtalálható tartalmaz-e a konfigurációk/modulok letölthető tárolása, és a jelentés adatokat az rögzítése csak képességeit.</span><span class="sxs-lookup"><span data-stu-id="66352-131">Please be advised that the pull service solution included in Windows Server includes only capabilities of storing configurations/modules for download and capturing report data in to database.</span></span>
<span data-ttu-id="66352-132">Nem tartalmazza az Azure-ban a szolgáltatás által kínált képességeket, és ezért nincs értékeléséhez, hogyan szeretné használni a szolgáltatás egy jó eszköz.</span><span class="sxs-lookup"><span data-stu-id="66352-132">It does not include many of the capabilities offered by the service in Azure and so is not a good tool for evaluating how the service would be used.</span></span>

<span data-ttu-id="66352-133">A lekéréses szolgáltatás, a Windows Server egy olyan webes szolgáltatás az IIS-ben elérhetővé DSC konfigurációs fájlokat a célcsomópontokat azokat a csomópontokat, kérje meg őket az OData-illesztőfelület használó.</span><span class="sxs-lookup"><span data-stu-id="66352-133">The pull service offered in Windows Server is a web service in IIS that uses an OData interface to make DSC configuration files available to target nodes when those nodes ask for them.</span></span>

<span data-ttu-id="66352-134">A lekérési kiszolgálójával használatának követelményei:</span><span class="sxs-lookup"><span data-stu-id="66352-134">Requirements for using a pull server:</span></span>

- <span data-ttu-id="66352-135">Futtató kiszolgálón:</span><span class="sxs-lookup"><span data-stu-id="66352-135">A server running:</span></span>
  - <span data-ttu-id="66352-136">WMF/PowerShell 5.0-s vagy újabb</span><span class="sxs-lookup"><span data-stu-id="66352-136">WMF/PowerShell 5.0 or greater</span></span>
  - <span data-ttu-id="66352-137">IIS-kiszolgálói szerepkör</span><span class="sxs-lookup"><span data-stu-id="66352-137">IIS server role</span></span>
  - <span data-ttu-id="66352-138">DSC Service</span><span class="sxs-lookup"><span data-stu-id="66352-138">DSC Service</span></span>
- <span data-ttu-id="66352-139">Ideális esetben egyes azt jelenti, hogy egy tanúsítványgenerálás során, a biztonságos hitelesítő adatok a helyi Configuration Manager (LCM) számára átadott a célcsomópontokat</span><span class="sxs-lookup"><span data-stu-id="66352-139">Ideally, some means of generating a certificate, to secure credentials passed to the Local Configuration Manager (LCM) on target nodes</span></span>

<span data-ttu-id="66352-140">A legjobb konfigurálja a Windows Server a gazdaszolgáltatás lekéréses módja a DSC-konfiguráció.</span><span class="sxs-lookup"><span data-stu-id="66352-140">The best way to configure Windows Server to host pull service is to use a DSC configuration.</span></span>
<span data-ttu-id="66352-141">Példa parancsfájl lejjebb tekinthetők meg.</span><span class="sxs-lookup"><span data-stu-id="66352-141">An example script is provided below.</span></span>

### <a name="using-the-xdscwebservice-resource"></a><span data-ttu-id="66352-142">A xDSCWebService erőforrás használata</span><span class="sxs-lookup"><span data-stu-id="66352-142">Using the xDSCWebService resource</span></span>

<span data-ttu-id="66352-143">A legegyszerűbben úgy állítsa be a webkiszolgáló lekéréses az xWebService erőforrás, a xPSDesiredStateConfiguration modulban használatára.</span><span class="sxs-lookup"><span data-stu-id="66352-143">The easiest way to set up a web pull server is to use the xWebService resource, included in the xPSDesiredStateConfiguration module.</span></span>
<span data-ttu-id="66352-144">Az alábbi lépések ismertetik az erőforrás használata, amely beállítja a webszolgáltatás konfigurációban.</span><span class="sxs-lookup"><span data-stu-id="66352-144">The following steps explain how to use the resource in a configuration that sets up the web service.</span></span>

1. <span data-ttu-id="66352-145">Hívja a [Install-modul](https://technet.microsoft.com/en-us/library/dn807162.aspx) telepítésére szolgáló parancsmagot a **xPSDesiredStateConfiguration** modul.</span><span class="sxs-lookup"><span data-stu-id="66352-145">Call the [Install-Module](https://technet.microsoft.com/en-us/library/dn807162.aspx) cmdlet to install the **xPSDesiredStateConfiguration** module.</span></span> <span data-ttu-id="66352-146">**Megjegyzés:**: **Install-modul** megtalálható a **PowerShellGet** modul, amely PowerShell 5.0 szerepel.</span><span class="sxs-lookup"><span data-stu-id="66352-146">**Note**: **Install-Module** is included in the **PowerShellGet** module, which is included in PowerShell 5.0.</span></span> <span data-ttu-id="66352-147">Letöltheti a **PowerShellGet** modul a PowerShell 3.0 és 4.0-s verzióját, [PackageManagement PowerShell modulok előzetes](https://www.microsoft.com/en-us/download/details.aspx?id=49186).</span><span class="sxs-lookup"><span data-stu-id="66352-147">You can download the **PowerShellGet** module for PowerShell 3.0 and 4.0 at [PackageManagement PowerShell Modules Preview](https://www.microsoft.com/en-us/download/details.aspx?id=49186).</span></span>
1. <span data-ttu-id="66352-148">Az SSL-tanúsítvány lekérése a DSC lekérési kiszolgálójával megbízható hitelesítésszolgáltatótól származó, vagy a szervezet vagy egy nyilvános szolgáltató belül.</span><span class="sxs-lookup"><span data-stu-id="66352-148">Get an SSL certificate for the DSC Pull server from a trusted Certificate Authority, either within your organization or a public authority.</span></span> <span data-ttu-id="66352-149">A szervezet kapott tanúsítvány általában a PFX formátumban van.</span><span class="sxs-lookup"><span data-stu-id="66352-149">The certificate received from the authority is usually in the PFX format.</span></span> <span data-ttu-id="66352-150">Telepítse a tanúsítványt a csomóponton a DSC lekérési kiszolgálójával, hogy CERT: \LocalMachine\My alkalmazandó alapértelmezett helyen lesz.</span><span class="sxs-lookup"><span data-stu-id="66352-150">Install the certificate on the node that will become the DSC Pull server in the default location which should be CERT:\LocalMachine\My.</span></span> <span data-ttu-id="66352-151">Jegyezze fel a tanúsítvány-ujjlenyomatot.</span><span class="sxs-lookup"><span data-stu-id="66352-151">Make a note of the certificate thumbprint.</span></span>
1. <span data-ttu-id="66352-152">Válassza ki a regisztrációs kulcsot használ egy GUID Azonosítót.</span><span class="sxs-lookup"><span data-stu-id="66352-152">Select a GUID to be used as the Registration Key.</span></span> <span data-ttu-id="66352-153">Hozhat létre egy PowerShell-lel írja be a következő, a PS-parancssorba, és nyomja le az enter: "``` [guid]::newGuid()```"vagy"```New-Guid```".</span><span class="sxs-lookup"><span data-stu-id="66352-153">To generate one using PowerShell enter the following at the PS prompt and press enter: '``` [guid]::newGuid()```' or '```New-Guid```'.</span></span> <span data-ttu-id="66352-154">Ez a kulcs által használandó ügyfél-csomópontok egy megosztott kulcsot, hitelesítéséhez a regisztráció során.</span><span class="sxs-lookup"><span data-stu-id="66352-154">This key will be used by client nodes as a shared key to authenticate during registration.</span></span> <span data-ttu-id="66352-155">További információ: a regisztrációs kulcsot következő szakaszban.</span><span class="sxs-lookup"><span data-stu-id="66352-155">For more information see the Registration Key section below.</span></span>
1. <span data-ttu-id="66352-156">A PowerShell ISE (F5) a következő konfigurációs parancsfájl futtatásához (például mappájában található a **xPSDesiredStateConfiguration** Sample_xDscWebService.ps1 modul).</span><span class="sxs-lookup"><span data-stu-id="66352-156">In the PowerShell ISE, start (F5) the following configuration script (included in the Example folder of the  **xPSDesiredStateConfiguration** module as Sample_xDscWebService.ps1).</span></span> <span data-ttu-id="66352-157">Ezt a parancsfájlt hoz létre a lekérési kiszolgálójával.</span><span class="sxs-lookup"><span data-stu-id="66352-157">This script sets up the pull server.</span></span>

```powershell
    configuration Sample_xDscPullServer
    {
        param
        (
                [string[]]$NodeName = 'localhost',

                [ValidateNotNullOrEmpty()]
                [string] $certificateThumbPrint,

                [Parameter(Mandatory)]
                [ValidateNotNullOrEmpty()]
                [string] $RegistrationKey
         )

         Import-DSCResource -ModuleName xPSDesiredStateConfiguration
         Import-DSCResource –ModuleName PSDesiredStateConfiguration

         Node $NodeName
         {
             WindowsFeature DSCServiceFeature
             {
                 Ensure = 'Present'
                 Name   = 'DSC-Service'
             }

             xDscWebService PSDSCPullServer
             {
                 Ensure                   = 'Present'
                 EndpointName             = 'PSDSCPullServer'
                 Port                     = 8080
                 PhysicalPath             = "$env:SystemDrive\inetpub\PSDSCPullServer"
                 CertificateThumbPrint    = $certificateThumbPrint
                 ModulePath               = "$env:PROGRAMFILES\WindowsPowerShell\DscService\Modules"
                 ConfigurationPath        = "$env:PROGRAMFILES\WindowsPowerShell\DscService\Configuration"
                 State                    = 'Started'
                 DependsOn                = '[WindowsFeature]DSCServiceFeature'
                 UseSecurityBestPractices = $false
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

1. <span data-ttu-id="66352-158">Futtassa a konfiguráció sikeres, az SSL-tanúsítvány ujjlenyomatát a **certificateThumbPrint** paraméter vagy a GUID-regisztrációs kulcs a **RegistrationKey** paraméter:</span><span class="sxs-lookup"><span data-stu-id="66352-158">Run the configuration, passing the thumbprint of the SSL certificate as the **certificateThumbPrint** parameter and a GUID registration key as the **RegistrationKey** parameter:</span></span>

```powershell
    # To find the Thumbprint for an installed SSL certificate for use with the pull server list all certificates in your local store
    # and then copy the thumbprint for the appropriate certificate by reviewing the certificate subjects
    dir Cert:\LocalMachine\my

    # Then include this thumbprint when running the configuration
    Sample_xDSCPullServer -certificateThumbprint 'A7000024B753FA6FFF88E966FD6E19301FAE9CCC' -RegistrationKey '140a952b-b9d6-406b-b416-e0f759c9c0e4' -OutputPath c:\Configs\PullServer

    # Run the compiled configuration to make the target node a DSC Pull Server
    Start-DscConfiguration -Path c:\Configs\PullServer -Wait -Verbose

```

#### <a name="registration-key"></a><span data-ttu-id="66352-159">Regisztrációs kulcs</span><span class="sxs-lookup"><span data-stu-id="66352-159">Registration Key</span></span>

<span data-ttu-id="66352-160">Teszi lehetővé az ügyfélszámítógépek csomópontok regisztrálni a kiszolgálót, hogy használhatnak konfigurációs nevek helyett egy konfigurációs Azonosítót, egy regisztrációs kulcsot a fenti konfigurációban által létrehozott nevű fájlba mentése `RegistrationKeys.txt` a `C:\Program Files\WindowsPowerShell\DscService`.</span><span class="sxs-lookup"><span data-stu-id="66352-160">To allow client nodes to register with the server so that they can use configuration names instead of a configuration ID, a registration key which was created by the above configuration is saved in a file named `RegistrationKeys.txt` in `C:\Program Files\WindowsPowerShell\DscService`.</span></span> <span data-ttu-id="66352-161">A regisztrációs kulcs funkciókkal, mint a kezdeti regisztráció során az ügyfél és a lekéréses kiszolgáló által használt megosztott titkos kulcs.</span><span class="sxs-lookup"><span data-stu-id="66352-161">The registration key functions as a shared secret used during the initial registration by the client with the pull server.</span></span> <span data-ttu-id="66352-162">Az ügyfél létrehoz egy önaláírt tanúsítványt, amely egyedi a kiszolgálón elvégzett hitelesítéshez lekéréses Ha regisztrálása sikeresen befejeződött.</span><span class="sxs-lookup"><span data-stu-id="66352-162">The client will generate a self-signed certificate which is used to uniquely authenticate to the pull server once registration is successfully completed.</span></span> <span data-ttu-id="66352-163">Ez a tanúsítvány ujjlenyomatának helyileg tárolja és társított a lekérési kiszolgálójával URL-CÍMÉT.</span><span class="sxs-lookup"><span data-stu-id="66352-163">The thumbprint of this certificate is stored locally and associated with the URL of the pull server.</span></span>
> <span data-ttu-id="66352-164">**Megjegyzés:**: PowerShell 4.0-s verzióját nem támogatja a regisztrációs kulccsal.</span><span class="sxs-lookup"><span data-stu-id="66352-164">**Note**: Registration keys are not supported in PowerShell 4.0.</span></span>

<span data-ttu-id="66352-165">A lekérési kiszolgálón hitelesíteni a regisztrációját csomópont konfigurálásához kulcsot kell lennie az összes cél csomóponttal fog a lekérési kiszolgálójával kell regisztrálása metakonfigurációját.</span><span class="sxs-lookup"><span data-stu-id="66352-165">In order to configure a node to authenticate with the pull server the registration key needs to be in the metaconfiguration for any target node that will be registering with this pull server.</span></span> <span data-ttu-id="66352-166">Vegye figyelembe, hogy a **RegistrationKey** az alábbi metakonfigurációját tartalomkonvertálást követően törlődik a célként megadott gép sikeresen regisztrálta, és hogy a "140a952b-b9d6-406b-b416-e0f759c9c0e4" értékét meg kell egyeznie az értékeket a A lekérési kiszolgálón RegistrationKeys.txt fájlt.</span><span class="sxs-lookup"><span data-stu-id="66352-166">Note that the **RegistrationKey** in the metaconfiguration below is removed after the target machine has successfully registered, and that the value '140a952b-b9d6-406b-b416-e0f759c9c0e4' must match the value stored in the RegistrationKeys.txt file on the pull server.</span></span> <span data-ttu-id="66352-167">A regisztrációs kulcs értékét biztonságosan, mindig kezelni, mert ismerete, hogy lehetővé teszi, hogy a célszámítógép regisztrálni a lekérési kiszolgálójával.</span><span class="sxs-lookup"><span data-stu-id="66352-167">Always treat the registration key value securely, because knowing it allows any target machine to register with the pull server.</span></span>

```powershell
[DSCLocalConfigurationManager()]
configuration PullClientConfigID
{
    Node localhost
    {
        Settings
        {
            RefreshMode          = 'Pull'
            RefreshFrequencyMins = 30
            RebootNodeIfNeeded   = $true
        }

        ConfigurationRepositoryWeb CONTOSO-PullSrv
        {
            ServerURL          = 'https://CONTOSO-PullSrv:8080/PSDSCPullServer.svc'
            RegistrationKey    = '140a952b-b9d6-406b-b416-e0f759c9c0e4'
            ConfigurationNames = @('ClientConfig')
        }

        ReportServerWeb CONTOSO-PullSrv
        {
            ServerURL       = 'https://CONTOSO-PullSrv:8080/PSDSCPullServer.svc'
            RegistrationKey = '140a952b-b9d6-406b-b416-e0f759c9c0e4'
        }
    }
}

PullClientConfigID -OutputPath c:\Configs\TargetNodes


```

> <span data-ttu-id="66352-168">**Megjegyzés:**: A **ReportServerWeb** szakasz lehetővé teszi a lekérési kiszolgálójával küldendő jelentésadatait.</span><span class="sxs-lookup"><span data-stu-id="66352-168">**Note**: The **ReportServerWeb** section allows reporting data to be sent to the pull server.</span></span>

<span data-ttu-id="66352-169">A hiánya a **ConfigurationID** tulajdonság a metakonfigurációját fájlban implicit módon azt jelenti, hogy a lekéréses kiszolgáló a V2 verziójú kiszolgáló lekéréses protokollt támogat, egy kezdeti regisztrációs szükség.</span><span class="sxs-lookup"><span data-stu-id="66352-169">The lack of the **ConfigurationID** property in the metaconfiguration file implicitly means that pull server is supporting the V2 version of the pull server protocol so an initial registration is required.</span></span>
<span data-ttu-id="66352-170">Ezzel ellentétben a jelenléte egy **ConfigurationID** azt jelenti, hogy a lekéréses protokoll a V1-es verziót használja, és nincs regisztrálása feldolgozási.</span><span class="sxs-lookup"><span data-stu-id="66352-170">Conversely, the presence of a **ConfigurationID** means that the V1 version of the pull server protocol is used and there is no registration processing.</span></span>

><span data-ttu-id="66352-171">**Megjegyzés:**: a forgatókönyvben a egy LEKÜLDÉSES programhiba szerepel az aktuális tételekor, így meg kell határozni egy ConfigurationID tulajdonság egy lekérési kiszolgálójával soha nem regisztrált csomópontok metakonfigurációját fájlban.</span><span class="sxs-lookup"><span data-stu-id="66352-171">**Note**: In a PUSH scenario, a bug exists in the current relase that makes it necessary to define a ConfigurationID property in the metaconfiguration file for nodes that have never registered with a pull server.</span></span> <span data-ttu-id="66352-172">Ezzel a V1 lekéréses protokoll kényszerítése és elkerülése érdekében a regisztrációs hibaüzenetek.</span><span class="sxs-lookup"><span data-stu-id="66352-172">This will force the V1 Pull Server protocol and avoid registration failure messages.</span></span>

## <a name="placing-configurations-and-resources"></a><span data-ttu-id="66352-173">Konfigurációk és erőforrások</span><span class="sxs-lookup"><span data-stu-id="66352-173">Placing configurations and resources</span></span>

<span data-ttu-id="66352-174">Miután a lekéréses server telepítésének befejezése határozzák meg a mappák a **ConfigurationPath** és **ModulePath** tulajdonságok a lekéréses kiszolgáló konfigurációjában: hol helyezi el a modulok és konfigurációk elérhető a célcsomópontokat való lekérésére fogja tárolni.</span><span class="sxs-lookup"><span data-stu-id="66352-174">After the pull server setup completes, the folders defined by the **ConfigurationPath** and **ModulePath** properties in the pull server configuration are where you will place modules and configurations that will be available for target nodes to pull.</span></span>
<span data-ttu-id="66352-175">Ezeket a fájlokat kell lennie ahhoz, hogy a lekérési kiszolgálójával, hogy helyesen dolgozza fel őket egy meghatározott formátumban.</span><span class="sxs-lookup"><span data-stu-id="66352-175">These files need to be in a specific format in order for the pull server to correctly process them.</span></span>

### <a name="dsc-resource-module-package-format"></a><span data-ttu-id="66352-176">A DSC erőforrás modul csomag formátuma</span><span class="sxs-lookup"><span data-stu-id="66352-176">DSC resource module package format</span></span>

<span data-ttu-id="66352-177">Minden erőforrás modul zip és nevű megfelelően a következő mintát kell `{Module Name}_{Module Version}.zip`.</span><span class="sxs-lookup"><span data-stu-id="66352-177">Each resource module needs to be zipped and named according the following pattern `{Module Name}_{Module Version}.zip`.</span></span>
<span data-ttu-id="66352-178">Például 3.1.2.0 modul verziójával xWebAdminstration nevű modul volna neve "xWebAdministration_3.2.1.0.zip".</span><span class="sxs-lookup"><span data-stu-id="66352-178">For example, a module named xWebAdminstration with a module version of 3.1.2.0 would be named 'xWebAdministration_3.2.1.0.zip'.</span></span>
<span data-ttu-id="66352-179">Egy modul verziói szerepelnie kell egy egyetlen zip-fájlt.</span><span class="sxs-lookup"><span data-stu-id="66352-179">Each version of a module must be contained in a single zip file.</span></span>
<span data-ttu-id="66352-180">Mivel a modul formátum szerepel a WMF 5.0 minden zip-fájlban szereplő erőforrás csak egyetlen verziója támogatása a egyetlen könyvtárban található több verziója nem támogatott.</span><span class="sxs-lookup"><span data-stu-id="66352-180">Since there is only a single version of a resource in each zip file the module format added in WMF 5.0 with support for multiple module versions in a single directory is not supported.</span></span>
<span data-ttu-id="66352-181">Ez azt jelenti, hogy csomagolási erőforrás modulok DSC lekérési kiszolgálójával való használatra mentése előtt szüksége lesz a könyvtárstruktúra kis módosítja.</span><span class="sxs-lookup"><span data-stu-id="66352-181">This means that before packaging up DSC resource modules for use with pull server you will need to make a small change to the directory structure.</span></span>
<span data-ttu-id="66352-182">Az alapértelmezett DSC erőforrást a WMF 5.0 tartalmazó modulok formátuma "{modul mappa}\{verziója} \DscResources\{DSC Erőforrásmappa}\'.</span><span class="sxs-lookup"><span data-stu-id="66352-182">The default format of modules containing DSC resource in WMF 5.0 is '{Module Folder}\{Module Version}\DscResources\{DSC Resource Folder}\'.</span></span>
<span data-ttu-id="66352-183">Előtt feliratkozott a lekérési kiszolgálójával csomagolás egyszerűen távolítsa el a **{verziója}** mappában, így az elérési útja bekerül a(z) {modul mappa} \DscResources\{DSC Erőforrásmappa}\'.</span><span class="sxs-lookup"><span data-stu-id="66352-183">Before packaging up for the pull server simply remove the **{Module version}** folder so the path becomes '{Module Folder}\DscResources\{DSC Resource Folder}\'.</span></span>
<span data-ttu-id="66352-184">A mappa az módosítását zip-fent leírt módon, és ezek a zip-fájlok a **ModulePath** mappa.</span><span class="sxs-lookup"><span data-stu-id="66352-184">With this change, zip the folder as described above and place these zip files in the **ModulePath** folder.</span></span>

<span data-ttu-id="66352-185">Használjon `new-dscchecksum {module zip file}` az újonnan hozzáadott modul ellenőrzőösszeg-fájl létrehozásához.</span><span class="sxs-lookup"><span data-stu-id="66352-185">Use `new-dscchecksum {module zip file}` to create a checksum file for the newly-added module.</span></span>

### <a name="configuration-mof-format"></a><span data-ttu-id="66352-186">Konfigurációs MOF formátuma</span><span class="sxs-lookup"><span data-stu-id="66352-186">Configuration MOF format</span></span>

<span data-ttu-id="66352-187">Konfigurációs MOF-fájlt kell, hogy egy LCM a cél csomópont azt is ellenőrzi a konfigurációt az ellenőrzőösszeg-fájl megfeleltetni.</span><span class="sxs-lookup"><span data-stu-id="66352-187">A configuration MOF file needs to be paired with a checksum file so that an LCM on a target node can validate the configuration.</span></span>
<span data-ttu-id="66352-188">Hozzon létre egy ellenőrzőösszeg, hívja meg a [New-DSCCheckSum](https://technet.microsoft.com/en-us/library/dn521622.aspx) parancsmag.</span><span class="sxs-lookup"><span data-stu-id="66352-188">To create a checksum, call the [New-DSCCheckSum](https://technet.microsoft.com/en-us/library/dn521622.aspx) cmdlet.</span></span>
<span data-ttu-id="66352-189">A parancsmag tart egy **elérési** paraméter meghatározza, hogy a mappát, ahol a konfigurációs MOF található.</span><span class="sxs-lookup"><span data-stu-id="66352-189">The cmdlet takes a **Path** parameter that specifies the folder where the configuration MOF is located.</span></span>
<span data-ttu-id="66352-190">A parancsmag létrehoz egy ellenőrzőösszeg nevű `ConfigurationMOFName.mof.checksum`, ahol `ConfigurationMOFName` a konfigurációs mof-fájl neve.</span><span class="sxs-lookup"><span data-stu-id="66352-190">The cmdlet creates a checksum file named `ConfigurationMOFName.mof.checksum`, where `ConfigurationMOFName` is the name of the configuration mof file.</span></span>
<span data-ttu-id="66352-191">Ha egynél több konfigurációs MOF-fájlok a megadott mappában, ellenőrzőösszeg minden konfigurációs a mappában létrejön.</span><span class="sxs-lookup"><span data-stu-id="66352-191">If there are more than one configuration MOF files in the specified folder, a checksum is created for each configuration in the folder.</span></span>
<span data-ttu-id="66352-192">A MOF-fájlok és az azokhoz társított ellenőrzőösszeg fájlokat helyezze a **ConfigurationPath** mappa.</span><span class="sxs-lookup"><span data-stu-id="66352-192">Place the MOF files and their associated checksum files in the **ConfigurationPath** folder.</span></span>

><span data-ttu-id="66352-193">**Megjegyzés:**: Ha megváltoztatja a konfigurációs MOF-fájl bármely olyan módon, az ellenőrzőösszeg-fájl is kell hozni.</span><span class="sxs-lookup"><span data-stu-id="66352-193">**Note**: If you change the configuration MOF file in any way, you must also recreate the checksum file.</span></span>

### <a name="tooling"></a><span data-ttu-id="66352-194">Tooling eszköz</span><span class="sxs-lookup"><span data-stu-id="66352-194">Tooling</span></span>

<span data-ttu-id="66352-195">Annak érdekében, hogy a beállítás, érvényesítése és a könnyebb, lekéréses kiszolgáló felügyelete a következő eszközök érhetők el a legújabb verzió xPSDesiredStateConfiguration modul példaként:</span><span class="sxs-lookup"><span data-stu-id="66352-195">In order to make setting up, validating and managing the pull server easier, the following tools are included as examples in the latest version of the xPSDesiredStateConfiguration module:</span></span>

1. <span data-ttu-id="66352-196">Ez a modul, amely segít csomagolási DSC erőforrás modulok és konfigurációs fájljait a lekérési kiszolgálón.</span><span class="sxs-lookup"><span data-stu-id="66352-196">A module that will help with packaging DSC resource modules and configuration files for use on the pull server.</span></span> <span data-ttu-id="66352-197">[PublishModulesAndMofsToPullServer.psm1](https://github.com/PowerShell/xPSDesiredStateConfiguration/blob/dev/DSCPullServerSetup/PublishModulesAndMofsToPullServer.psm1).</span><span class="sxs-lookup"><span data-stu-id="66352-197">[PublishModulesAndMofsToPullServer.psm1](https://github.com/PowerShell/xPSDesiredStateConfiguration/blob/dev/DSCPullServerSetup/PublishModulesAndMofsToPullServer.psm1).</span></span> <span data-ttu-id="66352-198">Az alábbi példák:</span><span class="sxs-lookup"><span data-stu-id="66352-198">Examples below:</span></span>

    ```powershell
        # Example 1 - Package all versions of given modules installed locally and MOF files are in c:\LocalDepot
         $moduleList = @("xWebAdministration", "xPhp")
         Publish-DSCModuleAndMof -Source C:\LocalDepot -ModuleNameList $moduleList

         # Example 2 - Package modules and mof documents from c:\LocalDepot
         Publish-DSCModuleAndMof -Source C:\LocalDepot -Force
    ```

1. <span data-ttu-id="66352-199">Egy parancsfájl, amely ellenőrzi a lekérési kiszolgálójával megfelelően van konfigurálva.</span><span class="sxs-lookup"><span data-stu-id="66352-199">A script that validates the pull server is configured correctly.</span></span> <span data-ttu-id="66352-200">[PullServerSetupTests.ps1](https://github.com/PowerShell/xPSDesiredStateConfiguration/blob/dev/DSCPullServerSetup/PullServerDeploymentVerificationTest/PullServerSetupTests.ps1).</span><span class="sxs-lookup"><span data-stu-id="66352-200">[PullServerSetupTests.ps1](https://github.com/PowerShell/xPSDesiredStateConfiguration/blob/dev/DSCPullServerSetup/PullServerDeploymentVerificationTest/PullServerSetupTests.ps1).</span></span>

## <a name="community-solutions-for-pull-service"></a><span data-ttu-id="66352-201">Közösségi megoldások lekéréses szolgáltatás</span><span class="sxs-lookup"><span data-stu-id="66352-201">Community Solutions for Pull Service</span></span>

<span data-ttu-id="66352-202">A DSC-Közösség rendelkezik létrehozott több megoldások megvalósításához a lekéréses szolgáltatás protokoll.</span><span class="sxs-lookup"><span data-stu-id="66352-202">The DSC community has authored multiple solutions to implement the pull service protocol.</span></span>
<span data-ttu-id="66352-203">A helyszíni környezetben ezek lekéréses szolgáltatás képességei és közre lehetőséget kínálnak biztonsági a Közösség növekményes fejlesztései.</span><span class="sxs-lookup"><span data-stu-id="66352-203">For on-premises environments these offer pull service capabilities and an opportunity to contribute back to the community with incremental enhancements.</span></span>

- [<span data-ttu-id="66352-204">Tug</span><span class="sxs-lookup"><span data-stu-id="66352-204">Tug</span></span>](https://github.com/powershellorg/tug)
- [<span data-ttu-id="66352-205">DSC-TRÆK</span><span class="sxs-lookup"><span data-stu-id="66352-205">DSC-TRÆK</span></span>](https://github.com/powershellorg/dsc-traek)

## <a name="pull-client-configuration"></a><span data-ttu-id="66352-206">Leküldéses ügyfél-konfiguráció</span><span class="sxs-lookup"><span data-stu-id="66352-206">Pull client configuration</span></span>

<span data-ttu-id="66352-207">A következő témakörök ismertetik részletesen lekéréses ügyfelek beállítása:</span><span class="sxs-lookup"><span data-stu-id="66352-207">The following topics describe setting up pull clients in detail:</span></span>

- [<span data-ttu-id="66352-208">Egy konfigurációs azonosítójával DSC lekérési ügyfél beállítása</span><span class="sxs-lookup"><span data-stu-id="66352-208">Setting up a DSC pull client using a configuration ID</span></span>](pullClientConfigID.md)
- [<span data-ttu-id="66352-209">Konfigurációs nevek használatával DSC lekérési ügyfél beállítása</span><span class="sxs-lookup"><span data-stu-id="66352-209">Setting up a DSC pull client using configuration names</span></span>](pullClientConfigNames.md)
- [<span data-ttu-id="66352-210">Részleges konfigurációk</span><span class="sxs-lookup"><span data-stu-id="66352-210">Partial configurations</span></span>](partialConfigs.md)

## <a name="see-also"></a><span data-ttu-id="66352-211">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="66352-211">See also</span></span>

- [<span data-ttu-id="66352-212">A Windows PowerShell célállapot-konfiguráló áttekintése</span><span class="sxs-lookup"><span data-stu-id="66352-212">Windows PowerShell Desired State Configuration Overview</span></span>](overview.md)
- [<span data-ttu-id="66352-213">Konfigurációk életbe léptetése</span><span class="sxs-lookup"><span data-stu-id="66352-213">Enacting configurations</span></span>](enactingConfigurations.md)
- [<span data-ttu-id="66352-214">A DSC jelentéskészítő kiszolgálójának használata</span><span class="sxs-lookup"><span data-stu-id="66352-214">Using a DSC report server</span></span>](reportServer.md)