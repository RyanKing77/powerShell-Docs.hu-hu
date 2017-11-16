---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "A DSC lekérési webkiszolgáló beállítása"
ms.openlocfilehash: 03d4d148c87854b146091aa0e8d815b8c35def72
ms.sourcegitcommit: 4102ecc35d473211f50a453f6ae3fbea31cb3428
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/31/2017
---
# <a name="setting-up-a-dsc-web-pull-server"></a><span data-ttu-id="93679-103">A DSC lekérési webkiszolgáló beállítása</span><span class="sxs-lookup"><span data-stu-id="93679-103">Setting up a DSC web pull server</span></span>

> <span data-ttu-id="93679-104">Vonatkozik: A Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="93679-104">Applies To: Windows PowerShell 5.0</span></span>

<span data-ttu-id="93679-105">A DSC lekérési webkiszolgáló egy webszolgáltatás-bővítmény, az IIS-ben elérhetővé DSC konfigurációs fájlokat a célcsomópontokat azokat a csomópontokat, kérje meg őket az OData-illesztőfelület használó.</span><span class="sxs-lookup"><span data-stu-id="93679-105">A DSC web pull server is a web service in IIS that uses an OData interface to make DSC configuration files available to target nodes when those nodes ask for them.</span></span>

<span data-ttu-id="93679-106">A lekérési kiszolgálójával használatának követelményei:</span><span class="sxs-lookup"><span data-stu-id="93679-106">Requirements for using a pull server:</span></span>

* <span data-ttu-id="93679-107">Futtató kiszolgálón:</span><span class="sxs-lookup"><span data-stu-id="93679-107">A server running:</span></span>
  - <span data-ttu-id="93679-108">WMF/PowerShell 5.0-s vagy újabb</span><span class="sxs-lookup"><span data-stu-id="93679-108">WMF/PowerShell 5.0 or greater</span></span>
  - <span data-ttu-id="93679-109">IIS-kiszolgálói szerepkör</span><span class="sxs-lookup"><span data-stu-id="93679-109">IIS server role</span></span>
  - <span data-ttu-id="93679-110">A DSC szolgáltatás</span><span class="sxs-lookup"><span data-stu-id="93679-110">DSC Service</span></span>
* <span data-ttu-id="93679-111">Ideális esetben egyes azt jelenti, hogy egy tanúsítványgenerálás során, a biztonságos hitelesítő adatok a helyi Configuration Manager (LCM) számára átadott a célcsomópontokat</span><span class="sxs-lookup"><span data-stu-id="93679-111">Ideally, some means of generating a certificate, to secure credentials passed to the Local Configuration Manager (LCM) on target nodes</span></span>

<span data-ttu-id="93679-112">Az IIS-kiszolgálói szerepkör és a DSC szolgáltatás a szerepkörök és szolgáltatások hozzáadása varázslót a Kiszolgálókezelőben, vagy a PowerShell használatával adhat hozzá.</span><span class="sxs-lookup"><span data-stu-id="93679-112">You can add the IIS server role and DSC Service with the Add Roles and Features wizard in Server Manager, or by using PowerShell.</span></span> <span data-ttu-id="93679-113">Ebben a témakörben szereplő mintaparancsfájlok kezelnek ezek az Ön is.</span><span class="sxs-lookup"><span data-stu-id="93679-113">The sample scripts included in this topic will handle both of these steps for you as well.</span></span>

## <a name="using-the-xdscwebservice-resource"></a><span data-ttu-id="93679-114">A xDSCWebService erőforrás használata</span><span class="sxs-lookup"><span data-stu-id="93679-114">Using the xDSCWebService resource</span></span>
<span data-ttu-id="93679-115">A legegyszerűbben úgy állítsa be a webkiszolgáló lekéréses az xWebService erőforrás, a xPSDesiredStateConfiguration modulban használatára.</span><span class="sxs-lookup"><span data-stu-id="93679-115">The easiest way to set up a web pull server is to use the xWebService resource, included in the xPSDesiredStateConfiguration module.</span></span> <span data-ttu-id="93679-116">Az alábbi lépések ismertetik az erőforrás használata, amely beállítja a webszolgáltatás konfigurációban.</span><span class="sxs-lookup"><span data-stu-id="93679-116">The following steps explain how to use the resource in a configuration that sets up the web service.</span></span>

1. <span data-ttu-id="93679-117">Hívja a [Install-modul](https://technet.microsoft.com/en-us/library/dn807162.aspx) telepítésére szolgáló parancsmagot a **xPSDesiredStateConfiguration** modul.</span><span class="sxs-lookup"><span data-stu-id="93679-117">Call the [Install-Module](https://technet.microsoft.com/en-us/library/dn807162.aspx) cmdlet to install the **xPSDesiredStateConfiguration** module.</span></span> <span data-ttu-id="93679-118">**Megjegyzés:**: **Install-modul** megtalálható a **PowerShellGet** modul, amely PowerShell 5.0 szerepel.</span><span class="sxs-lookup"><span data-stu-id="93679-118">**Note**: **Install-Module** is included in the **PowerShellGet** module, which is included in PowerShell 5.0.</span></span> <span data-ttu-id="93679-119">Letöltheti a **PowerShellGet** modul a PowerShell 3.0 és 4.0-s verzióját, [PackageManagement PowerShell modulok előzetes](https://www.microsoft.com/en-us/download/details.aspx?id=49186).</span><span class="sxs-lookup"><span data-stu-id="93679-119">You can download the **PowerShellGet** module for PowerShell 3.0 and 4.0 at [PackageManagement PowerShell Modules Preview](https://www.microsoft.com/en-us/download/details.aspx?id=49186).</span></span> 
1. <span data-ttu-id="93679-120">Az SSL-tanúsítvány lekérése a DSC lekérési kiszolgálójával megbízható hitelesítésszolgáltatótól származó, vagy a szervezet vagy egy nyilvános szolgáltató belül.</span><span class="sxs-lookup"><span data-stu-id="93679-120">Get an SSL certificate for the DSC Pull server from a trusted Certificate Authority, either within your organization or a public authority.</span></span> <span data-ttu-id="93679-121">A szervezet kapott tanúsítvány általában a PFX formátumban van.</span><span class="sxs-lookup"><span data-stu-id="93679-121">The certificate received from the authority is usually in the PFX format.</span></span> <span data-ttu-id="93679-122">Telepítse a tanúsítványt a csomóponton a DSC lekérési kiszolgálójával, hogy CERT: \LocalMachine\My alkalmazandó alapértelmezett helyen lesz.</span><span class="sxs-lookup"><span data-stu-id="93679-122">Install the certificate on the node that will become the DSC Pull server in the default location which should be CERT:\LocalMachine\My.</span></span> <span data-ttu-id="93679-123">Jegyezze fel a tanúsítvány-ujjlenyomatot.</span><span class="sxs-lookup"><span data-stu-id="93679-123">Make a note of the certificate thumbprint.</span></span>
1. <span data-ttu-id="93679-124">Válassza ki a regisztrációs kulcsot használ egy GUID Azonosítót.</span><span class="sxs-lookup"><span data-stu-id="93679-124">Select a GUID to be used as the Registration Key.</span></span> <span data-ttu-id="93679-125">Hozhat létre egy PowerShell-lel írja be a következő, a PS-parancssorba, és nyomja le az enter: "``` [guid]::newGuid()```"vagy"```New-Guid```".</span><span class="sxs-lookup"><span data-stu-id="93679-125">To generate one using PowerShell enter the following at the PS prompt and press enter: '``` [guid]::newGuid()```' or '```New-Guid```'.</span></span> <span data-ttu-id="93679-126">Ez a kulcs által használandó ügyfél-csomópontok egy megosztott kulcsot, hitelesítéséhez a regisztráció során.</span><span class="sxs-lookup"><span data-stu-id="93679-126">This key will be used by client nodes as a shared key to authenticate during registration.</span></span> <span data-ttu-id="93679-127">További információ: a regisztrációs kulcsot következő szakaszban.</span><span class="sxs-lookup"><span data-stu-id="93679-127">For more information see the Registration Key section below.</span></span>
1. <span data-ttu-id="93679-128">A PowerShell ISE (F5) a következő konfigurációs parancsfájl futtatásához (például mappájában található a **xPSDesiredStateConfiguration** Sample_xDscWebService.ps1 modul).</span><span class="sxs-lookup"><span data-stu-id="93679-128">In the PowerShell ISE, start (F5) the following configuration script (included in the Example folder of the  **xPSDesiredStateConfiguration** module as Sample_xDscWebService.ps1).</span></span> <span data-ttu-id="93679-129">Ezt a parancsfájlt hoz létre a lekérési kiszolgálójával.</span><span class="sxs-lookup"><span data-stu-id="93679-129">This script sets up the pull server.</span></span>
  
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

1. <span data-ttu-id="93679-130">Futtassa a konfiguráció sikeres, az SSL-tanúsítvány ujjlenyomatát a **certificateThumbPrint** paraméter vagy a GUID-regisztrációs kulcs a **RegistrationKey** paraméter:</span><span class="sxs-lookup"><span data-stu-id="93679-130">Run the configuration, passing the thumbprint of the SSL certificate as the **certificateThumbPrint** parameter and a GUID registration key as the **RegistrationKey** parameter:</span></span>

    ```powershell
    # To find the Thumbprint for an installed SSL certificate for use with the pull server list all certificates in your local store 
    # and then copy the thumbprint for the appropriate certificate by reviewing the certificate subjects
    dir Cert:\LocalMachine\my

    # Then include this thumbprint when running the configuration
    Sample_xDSCPullServer -certificateThumbprint 'A7000024B753FA6FFF88E966FD6E19301FAE9CCC' -RegistrationKey '140a952b-b9d6-406b-b416-e0f759c9c0e4' -OutputPath c:\Configs\PullServer

    # Run the compiled configuration to make the target node a DSC Pull Server
    Start-DscConfiguration -Path c:\Configs\PullServer -Wait -Verbose
    ```

## <a name="registration-key"></a><span data-ttu-id="93679-131">Regisztrációs kulcs</span><span class="sxs-lookup"><span data-stu-id="93679-131">Registration Key</span></span>
<span data-ttu-id="93679-132">Teszi lehetővé az ügyfélszámítógépek csomópontok regisztrálni a kiszolgálót, hogy használhatnak konfigurációs nevek helyett egy konfigurációs Azonosítót, egy regisztrációs kulcsot a fenti konfigurációban által létrehozott nevű fájlba mentése `RegistrationKeys.txt` a `C:\Program Files\WindowsPowerShell\DscService`.</span><span class="sxs-lookup"><span data-stu-id="93679-132">To allow client nodes to register with the server so that they can use configuration names instead of a configuration ID, a registration key which was created by the above configuration is saved in a file named `RegistrationKeys.txt` in `C:\Program Files\WindowsPowerShell\DscService`.</span></span> <span data-ttu-id="93679-133">A regisztrációs kulcs funkciókkal, mint a kezdeti regisztráció során az ügyfél és a lekéréses kiszolgáló által használt megosztott titkos kulcs.</span><span class="sxs-lookup"><span data-stu-id="93679-133">The registration key functions as a shared secret used during the initial registration by the client with the pull server.</span></span> <span data-ttu-id="93679-134">Az ügyfél létrehoz egy önaláírt tanúsítványt, amely egyedi a kiszolgálón elvégzett hitelesítéshez lekéréses Ha regisztrálása sikeresen befejeződött.</span><span class="sxs-lookup"><span data-stu-id="93679-134">The client will generate a self-signed certificate which is used to uniquely authenticate to the pull server once registration is successfully completed.</span></span> <span data-ttu-id="93679-135">Ez a tanúsítvány ujjlenyomatának helyileg tárolja és társított a lekérési kiszolgálójával URL-CÍMÉT.</span><span class="sxs-lookup"><span data-stu-id="93679-135">The thumbprint of this certificate is stored locally and associated with the URL of the pull server.</span></span>
> <span data-ttu-id="93679-136">**Megjegyzés:**: PowerShell 4.0-s verzióját nem támogatja a regisztrációs kulccsal.</span><span class="sxs-lookup"><span data-stu-id="93679-136">**Note**: Registration keys are not supported in PowerShell 4.0.</span></span> 

<span data-ttu-id="93679-137">A lekérési kiszolgálón hitelesíteni a regisztrációját csomópont konfigurálásához kulcsot kell lennie az összes cél csomóponttal fog a lekérési kiszolgálójával kell regisztrálása metakonfigurációját.</span><span class="sxs-lookup"><span data-stu-id="93679-137">In order to configure a node to authenticate with the pull server the registration key needs to be in the metaconfiguration for any target node that will be registering with this pull server.</span></span> <span data-ttu-id="93679-138">Vegye figyelembe, hogy a **RegistrationKey** az alábbi metakonfigurációját tartalomkonvertálást követően törlődik a célként megadott gép sikeresen regisztrálta, és hogy a "140a952b-b9d6-406b-b416-e0f759c9c0e4" értékét meg kell egyeznie az értékeket a A lekérési kiszolgálón RegistrationKeys.txt fájlt.</span><span class="sxs-lookup"><span data-stu-id="93679-138">Note that the **RegistrationKey** in the metaconfiguration below is removed after the target machine has successfully registered, and that the value '140a952b-b9d6-406b-b416-e0f759c9c0e4' must match the value stored in the RegistrationKeys.txt file on the pull server.</span></span> <span data-ttu-id="93679-139">A regisztrációs kulcs értékét biztonságosan, mindig kezelni, mert ismerete, hogy lehetővé teszi, hogy a célszámítógép regisztrálni a lekérési kiszolgálójával.</span><span class="sxs-lookup"><span data-stu-id="93679-139">Always treat the registration key value securely, because knowing it allows any target machine to register with the pull server.</span></span>

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
> <span data-ttu-id="93679-140">**Megjegyzés:**: A **ReportServerWeb** szakasz lehetővé teszi a lekérési kiszolgálójával küldendő jelentésadatait.</span><span class="sxs-lookup"><span data-stu-id="93679-140">**Note**: The **ReportServerWeb** section allows reporting data to be sent to the pull server.</span></span> 

<span data-ttu-id="93679-141">A hiánya a **ConfigurationID** tulajdonság a metakonfigurációját fájlban implicit módon azt jelenti, hogy a lekéréses kiszolgáló a V2 verziójú kiszolgáló lekéréses protokollt támogat, egy kezdeti regisztrációs szükség.</span><span class="sxs-lookup"><span data-stu-id="93679-141">The lack of the **ConfigurationID** property in the metaconfiguration file implicitly means that pull server is supporting the V2 version of the pull server protocol so an initial registration is required.</span></span> <span data-ttu-id="93679-142">Ezzel ellentétben a jelenléte egy **ConfigurationID** azt jelenti, hogy a lekéréses protokoll a V1-es verziót használja, és nincs regisztrálása feldolgozási.</span><span class="sxs-lookup"><span data-stu-id="93679-142">Conversely, the presence of a **ConfigurationID** means that the V1 version of the pull server protocol is used and there is no registration processing.</span></span>

><span data-ttu-id="93679-143">**Megjegyzés:**: a forgatókönyvben a egy LEKÜLDÉSES programhiba szerepel az aktuális tételekor, így meg kell határozni egy ConfigurationID tulajdonság egy lekérési kiszolgálójával soha nem regisztrált csomópontok metakonfigurációját fájlban.</span><span class="sxs-lookup"><span data-stu-id="93679-143">**Note**: In a PUSH scenario, a bug exists in the current relase that makes it necessary to define a ConfigurationID property in the metaconfiguration file for nodes that have never registered with a pull server.</span></span> <span data-ttu-id="93679-144">Ezzel a V1 lekéréses protokoll kényszerítése és elkerülése érdekében a regisztrációs hibaüzenetek.</span><span class="sxs-lookup"><span data-stu-id="93679-144">This will force the V1 Pull Server protocol and avoid registration failure messages.</span></span>

## <a name="placing-configurations-and-resources"></a><span data-ttu-id="93679-145">Konfigurációk és erőforrások</span><span class="sxs-lookup"><span data-stu-id="93679-145">Placing configurations and resources</span></span>

<span data-ttu-id="93679-146">Miután a lekéréses server telepítésének befejezése határozzák meg a mappák a **ConfigurationPath** és **ModulePath** tulajdonságok a lekéréses kiszolgáló konfigurációjában: hol helyezi el a modulok és konfigurációk elérhető a célcsomópontokat való lekérésére fogja tárolni.</span><span class="sxs-lookup"><span data-stu-id="93679-146">After the pull server setup completes, the folders defined by the **ConfigurationPath** and **ModulePath** properties in the pull server configuration are where you will place modules and configurations that will be available for target nodes to pull.</span></span> <span data-ttu-id="93679-147">Ezeket a fájlokat kell lennie ahhoz, hogy a lekérési kiszolgálójával, hogy helyesen dolgozza fel őket egy meghatározott formátumban.</span><span class="sxs-lookup"><span data-stu-id="93679-147">These files need to be in a specific format in order for the pull server to correctly process them.</span></span> 

### <a name="dsc-resource-module-package-format"></a><span data-ttu-id="93679-148">A DSC erőforrás modul csomag formátuma</span><span class="sxs-lookup"><span data-stu-id="93679-148">DSC resource module package format</span></span>

<span data-ttu-id="93679-149">Minden erőforrás modul zip és nevű megfelelően a következő mintát kell `{Module Name}_{Module Version}.zip`.</span><span class="sxs-lookup"><span data-stu-id="93679-149">Each resource module needs to be zipped and named according the following pattern `{Module Name}_{Module Version}.zip`.</span></span> <span data-ttu-id="93679-150">Például 3.1.2.0 modul verziójával xWebAdminstration nevű modul volna neve "xWebAdministration_3.2.1.0.zip".</span><span class="sxs-lookup"><span data-stu-id="93679-150">For example, a module named xWebAdminstration with a module version of 3.1.2.0 would be named 'xWebAdministration_3.2.1.0.zip'.</span></span> <span data-ttu-id="93679-151">Egy modul verziói szerepelnie kell egy egyetlen zip-fájlt.</span><span class="sxs-lookup"><span data-stu-id="93679-151">Each version of a module must be contained in a single zip file.</span></span> <span data-ttu-id="93679-152">Mivel a modul formátum szerepel a WMF 5.0 minden zip-fájlban szereplő erőforrás csak egyetlen verziója támogatása a egyetlen könyvtárban található több verziója nem támogatott.</span><span class="sxs-lookup"><span data-stu-id="93679-152">Since there is only a single version of a resource in each zip file the module format added in WMF 5.0 with support for multiple module versions in a single directory is not supported.</span></span> <span data-ttu-id="93679-153">Ez azt jelenti, hogy csomagolási erőforrás modulok DSC lekérési kiszolgálójával való használatra mentése előtt szüksége lesz a könyvtárstruktúra kis módosítja.</span><span class="sxs-lookup"><span data-stu-id="93679-153">This means that before packaging up DSC resource modules for use with pull server you will need to make a small change to the directory structure.</span></span> <span data-ttu-id="93679-154">Az alapértelmezett DSC erőforrást a WMF 5.0 tartalmazó modulok formátuma "{modul mappa}\{verziója} \DscResources\{DSC Erőforrásmappa}\'.</span><span class="sxs-lookup"><span data-stu-id="93679-154">The default format of modules containing DSC resource in WMF 5.0 is '{Module Folder}\{Module Version}\DscResources\{DSC Resource Folder}\'.</span></span> <span data-ttu-id="93679-155">Előtt feliratkozott a lekérési kiszolgálójával csomagolás egyszerűen távolítsa el a **{verziója}** mappában, így az elérési útja bekerül a(z) {modul mappa} \DscResources\{DSC Erőforrásmappa}\'.</span><span class="sxs-lookup"><span data-stu-id="93679-155">Before packaging up for the pull server simply remove the **{Module version}** folder so the path becomes '{Module Folder}\DscResources\{DSC Resource Folder}\'.</span></span> <span data-ttu-id="93679-156">A mappa az módosítását zip-fent leírt módon, és ezek a zip-fájlok a **ModulePath** mappa.</span><span class="sxs-lookup"><span data-stu-id="93679-156">With this change, zip the folder as described above and place these zip files in the **ModulePath** folder.</span></span>

<span data-ttu-id="93679-157">Használjon `new-dscchecksum {module zip file}` az újonnan hozzáadott modul ellenőrzőösszeg-fájl létrehozásához.</span><span class="sxs-lookup"><span data-stu-id="93679-157">Use `new-dscchecksum {module zip file}` to create a checksum file for the newly-added module.</span></span>

### <a name="configuration-mof-format"></a><span data-ttu-id="93679-158">Konfigurációs MOF formátuma</span><span class="sxs-lookup"><span data-stu-id="93679-158">Configuration MOF format</span></span> 
<span data-ttu-id="93679-159">Konfigurációs MOF-fájlt kell, hogy egy LCM a cél csomópont azt is ellenőrzi a konfigurációt az ellenőrzőösszeg-fájl megfeleltetni.</span><span class="sxs-lookup"><span data-stu-id="93679-159">A configuration MOF file needs to be paired with a checksum file so that an LCM on a target node can validate the configuration.</span></span> <span data-ttu-id="93679-160">Hozzon létre egy ellenőrzőösszeg, hívja meg a [New-DSCCheckSum](https://technet.microsoft.com/en-us/library/dn521622.aspx) parancsmag.</span><span class="sxs-lookup"><span data-stu-id="93679-160">To create a checksum, call the [New-DSCCheckSum](https://technet.microsoft.com/en-us/library/dn521622.aspx) cmdlet.</span></span> <span data-ttu-id="93679-161">A parancsmag tart egy **elérési** paraméter meghatározza, hogy a mappát, ahol a konfigurációs MOF található.</span><span class="sxs-lookup"><span data-stu-id="93679-161">The cmdlet takes a **Path** parameter that specifies the folder where the configuration MOF is located.</span></span> <span data-ttu-id="93679-162">A parancsmag létrehoz egy ellenőrzőösszeg nevű `ConfigurationMOFName.mof.checksum`, ahol `ConfigurationMOFName` a konfigurációs mof-fájl neve.</span><span class="sxs-lookup"><span data-stu-id="93679-162">The cmdlet creates a checksum file named `ConfigurationMOFName.mof.checksum`, where `ConfigurationMOFName` is the name of the configuration mof file.</span></span> <span data-ttu-id="93679-163">Ha egynél több konfigurációs MOF-fájlok a megadott mappában, ellenőrzőösszeg minden konfigurációs a mappában létrejön.</span><span class="sxs-lookup"><span data-stu-id="93679-163">If there are more than one configuration MOF files in the specified folder, a checksum is created for each configuration in the folder.</span></span> <span data-ttu-id="93679-164">A MOF-fájlok és az azokhoz társított ellenőrzőösszeg fájlokat helyezze a a **ConfigurationPath** mappa.</span><span class="sxs-lookup"><span data-stu-id="93679-164">Place the MOF files and their associated checksum files in the the **ConfigurationPath** folder.</span></span>

><span data-ttu-id="93679-165">**Megjegyzés:**: Ha megváltoztatja a konfigurációs MOF-fájl bármely olyan módon, az ellenőrzőösszeg-fájl is kell hozni.</span><span class="sxs-lookup"><span data-stu-id="93679-165">**Note**: If you change the configuration MOF file in any way, you must also recreate the checksum file.</span></span>

## <a name="tooling"></a><span data-ttu-id="93679-166">Tooling eszköz</span><span class="sxs-lookup"><span data-stu-id="93679-166">Tooling</span></span>
<span data-ttu-id="93679-167">Annak érdekében, hogy a beállítás, érvényesítése és a könnyebb, lekéréses kiszolgáló felügyelete a következő eszközök érhetők el a legújabb verzió xPSDesiredStateConfiguration modul példaként:</span><span class="sxs-lookup"><span data-stu-id="93679-167">In order to make setting up, validating and managing the pull server easier, the following tools are included as examples in the latest version of the xPSDesiredStateConfiguration module:</span></span>
1. <span data-ttu-id="93679-168">Ez a modul, amely segít csomagolási DSC erőforrás modulok és konfigurációs fájljait a lekérési kiszolgálón.</span><span class="sxs-lookup"><span data-stu-id="93679-168">A module that will help with packaging DSC resource modules and configuration files for use on the pull server.</span></span> <span data-ttu-id="93679-169">[PublishModulesAndMofsToPullServer.psm1](https://github.com/PowerShell/xPSDesiredStateConfiguration/blob/dev/DSCPullServerSetup/PublishModulesAndMofsToPullServer.psm1).</span><span class="sxs-lookup"><span data-stu-id="93679-169">[PublishModulesAndMofsToPullServer.psm1](https://github.com/PowerShell/xPSDesiredStateConfiguration/blob/dev/DSCPullServerSetup/PublishModulesAndMofsToPullServer.psm1).</span></span> <span data-ttu-id="93679-170">Az alábbi példák:</span><span class="sxs-lookup"><span data-stu-id="93679-170">Examples below:</span></span>

    ```powershell
        # Example 1 - Package all versions of given modules installed locally and MOF files are in c:\LocalDepot
         $moduleList = @("xWebAdministration", "xPhp") 
         Publish-DSCModuleAndMof -Source C:\LocalDepot -ModuleNameList $moduleList 

         # Example 2 - Package modules and mof documents from c:\LocalDepot
         Publish-DSCModuleAndMof -Source C:\LocalDepot -Force
    ```

1. <span data-ttu-id="93679-171">Egy parancsfájl, amely ellenőrzi a lekérési kiszolgálójával megfelelően van konfigurálva.</span><span class="sxs-lookup"><span data-stu-id="93679-171">A script that validates the pull server is configured correctly.</span></span> <span data-ttu-id="93679-172">[PullServerSetupTests.ps1](https://github.com/PowerShell/xPSDesiredStateConfiguration/blob/dev/DSCPullServerSetup/PullServerDeploymentVerificationTest/PullServerSetupTests.ps1).</span><span class="sxs-lookup"><span data-stu-id="93679-172">[PullServerSetupTests.ps1](https://github.com/PowerShell/xPSDesiredStateConfiguration/blob/dev/DSCPullServerSetup/PullServerDeploymentVerificationTest/PullServerSetupTests.ps1).</span></span>


## <a name="pull-client-configuration"></a><span data-ttu-id="93679-173">Leküldéses ügyfél-konfiguráció</span><span class="sxs-lookup"><span data-stu-id="93679-173">Pull client configuration</span></span> 
<span data-ttu-id="93679-174">A következő témakörök ismertetik részletesen lekéréses ügyfelek beállítása:</span><span class="sxs-lookup"><span data-stu-id="93679-174">The following topics describe setting up pull clients in detail:</span></span>

* [<span data-ttu-id="93679-175">Egy konfigurációs azonosítójával DSC lekérési ügyfél beállítása</span><span class="sxs-lookup"><span data-stu-id="93679-175">Setting up a DSC pull client using a configuration ID</span></span>](pullClientConfigID.md)
* [<span data-ttu-id="93679-176">Konfigurációs nevek használatával DSC lekérési ügyfél beállítása</span><span class="sxs-lookup"><span data-stu-id="93679-176">Setting up a DSC pull client using configuration names</span></span>](pullClientConfigNames.md)
* [<span data-ttu-id="93679-177">Részleges konfigurációk</span><span class="sxs-lookup"><span data-stu-id="93679-177">Partial configurations</span></span>](partialConfigs.md)


## <a name="see-also"></a><span data-ttu-id="93679-178">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="93679-178">See also</span></span>
* [<span data-ttu-id="93679-179">A Windows PowerShell célállapot-konfiguráló áttekintése</span><span class="sxs-lookup"><span data-stu-id="93679-179">Windows PowerShell Desired State Configuration Overview</span></span>](overview.md)
* [<span data-ttu-id="93679-180">Életbe konfigurációk</span><span class="sxs-lookup"><span data-stu-id="93679-180">Enacting configurations</span></span>](enactingConfigurations.md)
* [<span data-ttu-id="93679-181">A DSC-jelentés kiszolgálóval</span><span class="sxs-lookup"><span data-stu-id="93679-181">Using a DSC report server</span></span>](reportServer.md)

