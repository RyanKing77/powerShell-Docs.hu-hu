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
# <a name="setting-up-a-dsc-web-pull-server"></a>A DSC lekérési webkiszolgáló beállítása

> Vonatkozik: A Windows PowerShell 5.0

A DSC lekérési webkiszolgáló egy webszolgáltatás-bővítmény, az IIS-ben elérhetővé DSC konfigurációs fájlokat a célcsomópontokat azokat a csomópontokat, kérje meg őket az OData-illesztőfelület használó.

A lekérési kiszolgálójával használatának követelményei:

* Futtató kiszolgálón:
  - WMF/PowerShell 5.0-s vagy újabb
  - IIS-kiszolgálói szerepkör
  - A DSC szolgáltatás
* Ideális esetben egyes azt jelenti, hogy egy tanúsítványgenerálás során, a biztonságos hitelesítő adatok a helyi Configuration Manager (LCM) számára átadott a célcsomópontokat

Az IIS-kiszolgálói szerepkör és a DSC szolgáltatás a szerepkörök és szolgáltatások hozzáadása varázslót a Kiszolgálókezelőben, vagy a PowerShell használatával adhat hozzá. Ebben a témakörben szereplő mintaparancsfájlok kezelnek ezek az Ön is.

## <a name="using-the-xdscwebservice-resource"></a>A xDSCWebService erőforrás használata
A legegyszerűbben úgy állítsa be a webkiszolgáló lekéréses az xWebService erőforrás, a xPSDesiredStateConfiguration modulban használatára. Az alábbi lépések ismertetik az erőforrás használata, amely beállítja a webszolgáltatás konfigurációban.

1. Hívja a [Install-modul](https://technet.microsoft.com/en-us/library/dn807162.aspx) telepítésére szolgáló parancsmagot a **xPSDesiredStateConfiguration** modul. **Megjegyzés:**: **Install-modul** megtalálható a **PowerShellGet** modul, amely PowerShell 5.0 szerepel. Letöltheti a **PowerShellGet** modul a PowerShell 3.0 és 4.0-s verzióját, [PackageManagement PowerShell modulok előzetes](https://www.microsoft.com/en-us/download/details.aspx?id=49186). 
1. Az SSL-tanúsítvány lekérése a DSC lekérési kiszolgálójával megbízható hitelesítésszolgáltatótól származó, vagy a szervezet vagy egy nyilvános szolgáltató belül. A szervezet kapott tanúsítvány általában a PFX formátumban van. Telepítse a tanúsítványt a csomóponton a DSC lekérési kiszolgálójával, hogy CERT: \LocalMachine\My alkalmazandó alapértelmezett helyen lesz. Jegyezze fel a tanúsítvány-ujjlenyomatot.
1. Válassza ki a regisztrációs kulcsot használ egy GUID Azonosítót. Hozhat létre egy PowerShell-lel írja be a következő, a PS-parancssorba, és nyomja le az enter: "``` [guid]::newGuid()```"vagy"```New-Guid```". Ez a kulcs által használandó ügyfél-csomópontok egy megosztott kulcsot, hitelesítéséhez a regisztráció során. További információ: a regisztrációs kulcsot következő szakaszban.
1. A PowerShell ISE (F5) a következő konfigurációs parancsfájl futtatásához (például mappájában található a **xPSDesiredStateConfiguration** Sample_xDscWebService.ps1 modul). Ezt a parancsfájlt hoz létre a lekérési kiszolgálójával.
  
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

1. Futtassa a konfiguráció sikeres, az SSL-tanúsítvány ujjlenyomatát a **certificateThumbPrint** paraméter vagy a GUID-regisztrációs kulcs a **RegistrationKey** paraméter:

    ```powershell
    # To find the Thumbprint for an installed SSL certificate for use with the pull server list all certificates in your local store 
    # and then copy the thumbprint for the appropriate certificate by reviewing the certificate subjects
    dir Cert:\LocalMachine\my

    # Then include this thumbprint when running the configuration
    Sample_xDSCPullServer -certificateThumbprint 'A7000024B753FA6FFF88E966FD6E19301FAE9CCC' -RegistrationKey '140a952b-b9d6-406b-b416-e0f759c9c0e4' -OutputPath c:\Configs\PullServer

    # Run the compiled configuration to make the target node a DSC Pull Server
    Start-DscConfiguration -Path c:\Configs\PullServer -Wait -Verbose
    ```

## <a name="registration-key"></a>Regisztrációs kulcs
Teszi lehetővé az ügyfélszámítógépek csomópontok regisztrálni a kiszolgálót, hogy használhatnak konfigurációs nevek helyett egy konfigurációs Azonosítót, egy regisztrációs kulcsot a fenti konfigurációban által létrehozott nevű fájlba mentése `RegistrationKeys.txt` a `C:\Program Files\WindowsPowerShell\DscService`. A regisztrációs kulcs funkciókkal, mint a kezdeti regisztráció során az ügyfél és a lekéréses kiszolgáló által használt megosztott titkos kulcs. Az ügyfél létrehoz egy önaláírt tanúsítványt, amely egyedi a kiszolgálón elvégzett hitelesítéshez lekéréses Ha regisztrálása sikeresen befejeződött. Ez a tanúsítvány ujjlenyomatának helyileg tárolja és társított a lekérési kiszolgálójával URL-CÍMÉT.
> **Megjegyzés:**: PowerShell 4.0-s verzióját nem támogatja a regisztrációs kulccsal. 

A lekérési kiszolgálón hitelesíteni a regisztrációját csomópont konfigurálásához kulcsot kell lennie az összes cél csomóponttal fog a lekérési kiszolgálójával kell regisztrálása metakonfigurációját. Vegye figyelembe, hogy a **RegistrationKey** az alábbi metakonfigurációját tartalomkonvertálást követően törlődik a célként megadott gép sikeresen regisztrálta, és hogy a "140a952b-b9d6-406b-b416-e0f759c9c0e4" értékét meg kell egyeznie az értékeket a A lekérési kiszolgálón RegistrationKeys.txt fájlt. A regisztrációs kulcs értékét biztonságosan, mindig kezelni, mert ismerete, hogy lehetővé teszi, hogy a célszámítógép regisztrálni a lekérési kiszolgálójával.

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
> **Megjegyzés:**: A **ReportServerWeb** szakasz lehetővé teszi a lekérési kiszolgálójával küldendő jelentésadatait. 

A hiánya a **ConfigurationID** tulajdonság a metakonfigurációját fájlban implicit módon azt jelenti, hogy a lekéréses kiszolgáló a V2 verziójú kiszolgáló lekéréses protokollt támogat, egy kezdeti regisztrációs szükség. Ezzel ellentétben a jelenléte egy **ConfigurationID** azt jelenti, hogy a lekéréses protokoll a V1-es verziót használja, és nincs regisztrálása feldolgozási.

>**Megjegyzés:**: a forgatókönyvben a egy LEKÜLDÉSES programhiba szerepel az aktuális tételekor, így meg kell határozni egy ConfigurationID tulajdonság egy lekérési kiszolgálójával soha nem regisztrált csomópontok metakonfigurációját fájlban. Ezzel a V1 lekéréses protokoll kényszerítése és elkerülése érdekében a regisztrációs hibaüzenetek.

## <a name="placing-configurations-and-resources"></a>Konfigurációk és erőforrások

Miután a lekéréses server telepítésének befejezése határozzák meg a mappák a **ConfigurationPath** és **ModulePath** tulajdonságok a lekéréses kiszolgáló konfigurációjában: hol helyezi el a modulok és konfigurációk elérhető a célcsomópontokat való lekérésére fogja tárolni. Ezeket a fájlokat kell lennie ahhoz, hogy a lekérési kiszolgálójával, hogy helyesen dolgozza fel őket egy meghatározott formátumban. 

### <a name="dsc-resource-module-package-format"></a>A DSC erőforrás modul csomag formátuma

Minden erőforrás modul zip és nevű megfelelően a következő mintát kell `{Module Name}_{Module Version}.zip`. Például 3.1.2.0 modul verziójával xWebAdminstration nevű modul volna neve "xWebAdministration_3.2.1.0.zip". Egy modul verziói szerepelnie kell egy egyetlen zip-fájlt. Mivel a modul formátum szerepel a WMF 5.0 minden zip-fájlban szereplő erőforrás csak egyetlen verziója támogatása a egyetlen könyvtárban található több verziója nem támogatott. Ez azt jelenti, hogy csomagolási erőforrás modulok DSC lekérési kiszolgálójával való használatra mentése előtt szüksége lesz a könyvtárstruktúra kis módosítja. Az alapértelmezett DSC erőforrást a WMF 5.0 tartalmazó modulok formátuma "{modul mappa}\{verziója} \DscResources\{DSC Erőforrásmappa}\'. Előtt feliratkozott a lekérési kiszolgálójával csomagolás egyszerűen távolítsa el a **{verziója}** mappában, így az elérési útja bekerül a(z) {modul mappa} \DscResources\{DSC Erőforrásmappa}\'. A mappa az módosítását zip-fent leírt módon, és ezek a zip-fájlok a **ModulePath** mappa.

Használjon `new-dscchecksum {module zip file}` az újonnan hozzáadott modul ellenőrzőösszeg-fájl létrehozásához.

### <a name="configuration-mof-format"></a>Konfigurációs MOF formátuma 
Konfigurációs MOF-fájlt kell, hogy egy LCM a cél csomópont azt is ellenőrzi a konfigurációt az ellenőrzőösszeg-fájl megfeleltetni. Hozzon létre egy ellenőrzőösszeg, hívja meg a [New-DSCCheckSum](https://technet.microsoft.com/en-us/library/dn521622.aspx) parancsmag. A parancsmag tart egy **elérési** paraméter meghatározza, hogy a mappát, ahol a konfigurációs MOF található. A parancsmag létrehoz egy ellenőrzőösszeg nevű `ConfigurationMOFName.mof.checksum`, ahol `ConfigurationMOFName` a konfigurációs mof-fájl neve. Ha egynél több konfigurációs MOF-fájlok a megadott mappában, ellenőrzőösszeg minden konfigurációs a mappában létrejön. A MOF-fájlok és az azokhoz társított ellenőrzőösszeg fájlokat helyezze a a **ConfigurationPath** mappa.

>**Megjegyzés:**: Ha megváltoztatja a konfigurációs MOF-fájl bármely olyan módon, az ellenőrzőösszeg-fájl is kell hozni.

## <a name="tooling"></a>Tooling eszköz
Annak érdekében, hogy a beállítás, érvényesítése és a könnyebb, lekéréses kiszolgáló felügyelete a következő eszközök érhetők el a legújabb verzió xPSDesiredStateConfiguration modul példaként:
1. Ez a modul, amely segít csomagolási DSC erőforrás modulok és konfigurációs fájljait a lekérési kiszolgálón. [PublishModulesAndMofsToPullServer.psm1](https://github.com/PowerShell/xPSDesiredStateConfiguration/blob/dev/DSCPullServerSetup/PublishModulesAndMofsToPullServer.psm1). Az alábbi példák:

    ```powershell
        # Example 1 - Package all versions of given modules installed locally and MOF files are in c:\LocalDepot
         $moduleList = @("xWebAdministration", "xPhp") 
         Publish-DSCModuleAndMof -Source C:\LocalDepot -ModuleNameList $moduleList 

         # Example 2 - Package modules and mof documents from c:\LocalDepot
         Publish-DSCModuleAndMof -Source C:\LocalDepot -Force
    ```

1. Egy parancsfájl, amely ellenőrzi a lekérési kiszolgálójával megfelelően van konfigurálva. [PullServerSetupTests.ps1](https://github.com/PowerShell/xPSDesiredStateConfiguration/blob/dev/DSCPullServerSetup/PullServerDeploymentVerificationTest/PullServerSetupTests.ps1).


## <a name="pull-client-configuration"></a>Leküldéses ügyfél-konfiguráció 
A következő témakörök ismertetik részletesen lekéréses ügyfelek beállítása:

* [Egy konfigurációs azonosítójával DSC lekérési ügyfél beállítása](pullClientConfigID.md)
* [Konfigurációs nevek használatával DSC lekérési ügyfél beállítása](pullClientConfigNames.md)
* [Részleges konfigurációk](partialConfigs.md)


## <a name="see-also"></a>Lásd még:
* [A Windows PowerShell célállapot-konfiguráló áttekintése](overview.md)
* [Életbe konfigurációk](enactingConfigurations.md)
* [A DSC-jelentés kiszolgálóval](reportServer.md)

