---
ms.date: 04/11/2018
keywords: DSC, powershell, a konfigurációt, a beállítása
title: DSC Pull Service
ms.openlocfilehash: 659a8f8b2ce7d34058e789c5de336dc1f1f2abb2
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55687796"
---
# <a name="desired-state-configuration-pull-service"></a>Desired State Configuration lekéréses szolgáltatás

> Érvényes: Windows PowerShell 5.0

> [!IMPORTANT]
> A lekéréses kiszolgálón (Windows-szolgáltatás *DSC-szolgáltatás*), a Windows Server támogatott összetevője létezik azonban tervekben sem funkciókat és képességeket kínálnak. Javasoljuk, hogy helyeződnek felügyelt ügyfelek [Azure Automation DSC](/azure/automation/automation-dsc-getting-started) (beleértve a lekéréses kiszolgálón a Windows Server csomagban) vagy a közösségi megoldások felsorolt [Itt](pullserver.md#community-solutions-for-pull-service).

Helyi Configuration Manager lekéréses Szolgáltatottszoftver-megoldás központilag kezelhetők.
Ez a megközelítés használatakor a felügyelt csomópont regisztrálva a szolgáltatásban és konfigurálása során a LCM beállításokat rendelt.
A konfiguráció minden DSC-erőforrások függőségeként a konfigurációhoz szükséges a géphez letöltött és LCM használja a konfiguráció kezelésére.
A felügyelt számítógép állapotát a service for reporting töltenek fel.
A fogalom a neve "lekéréses szolgáltatás."

A lekéréses szolgáltatás jelenlegi lehetőségek a következők:

- Azure Automation Desired State Configuration service
- Windows Server rendszeren futó lekéréses szolgáltatás
- Közösségi nyílt forráskódú megoldások karbantartása
- SMB-megosztáson

**Az ajánlott megoldás a**, és a lehetőség érhető el, a legtöbb funkciót a [Azure Automation DSC](/azure/automation/automation-dsc-getting-started).

Az Azure-szolgáltatás csomópontjai a helyszíni privát adatközpontok, vagy a nyilvános felhők, például az Azure és az AWS is kezelheti.
Ahol kiszolgálói nem tudnak közvetlenül kapcsolódni az internetre privát környezetek esetén fontolja meg, csak a közzétett Azure IP-címtartomány irányuló kimenő forgalom korlátozása (lásd: [Azure Datacenter IP-címtartományok](https://www.microsoft.com/en-us/download/details.aspx?id=41653)).

Az online szolgáltatás, amelyek nem a Windows Server, a lekéréses szolgáltatásban jelenleg elérhető funkciók:
- Összes adat titkosítva lesz az úton lévő és inaktív
- Ügyfél-tanúsítványok létrehozása és felügyelete automatikus
- Titkos kódok tárolása központilag kezelésére szolgáló [jelszavak és a hitelesítő adatok](/azure/automation/automation-credentials), vagy [változók](/azure/automation/automation-variables) például a kiszolgáló nevét vagy a kapcsolati karakterláncok
- Központilag kezelheti a csomópont [LCM konfigurálása](../managing-nodes/metaConfig.md#basic-settings)
- Konfigurációk központilag ügyfél-csomópontok hozzárendelése
- Kiadási konfiguráció módosításait "tesztcsoportos csoportok" tesztelési éles elérése előtt
- Grafikus jelentési
  - A granularitási DSC erőforrás szintjén állapotának részletei
  - Hibaelhárítás az ügyfélgépek a részletes hibaüzenetek
- [Integráció az Azure Log Analytics](/azure/automation/automation-dsc-diagnostics) riasztási, automatizált feladatokat, jelentéskészítési és riasztási Android vagy iOS-alkalmazás

## <a name="dsc-pull-service-in-windows-server"></a>DSC lekéréses szolgáltatás a Windows Server

A Windows Serveren futó lekéréses szolgáltatás konfigurálása lehetőség.
Felhasználóitevékenység, hogy az lekéréses szolgáltatás része a Windows Server tartalmaz konfigurációk/modulok letölthető tárolására, és a jelentés adatai az adatbázis csak képességeit.
Nem tartalmazza a képességek a szolgáltatást az Azure által kínált számos, és ezért nem kiértékelését, hogy a szolgáltatás használni kívánt hatékony eszköz.

A lekéréses szolgáltatás, a Windows Server rendszer egy webszolgáltatás, amely egy OData-felületet segítségével DSC konfigurációs fájlok célcsomópontok számára elérhetővé tenni, ha azokat a csomópontokat, kérje meg őket az IIS-ben.

Egy lekéréses kiszolgálót használatának követelményei:

- Futtató kiszolgálón:
  - A WMF/PowerShell 5.0-s vagy újabb
  - IIS-kiszolgálói szerepkör
  - DSC-szolgáltatás
- Ideális esetben néhány azt jelenti, hogy egy tanúsítványt létrehozni bloberőforrásokhoz átadott, a helyi Configuration Manager (LCM) Konfigurálása a célcsomópontokat hitelesítő adatok biztonságossá tételéhez

Windows Server konfigurálása a gazdagépen lekéréses szolgáltatás a legjobb módszer az DSC-konfiguráció használata.
Példa parancsfájl lejjebb találja.

### <a name="supported-database-systems"></a>Támogatott adatbázis-rendszerek

|WMF 4.0   |WMF 5.0  |WMF 5.1 |A WMF 5.1 (Windows Server Insider Preview 17090)|
|---------|---------|---------|---------|
|MDB     |MDB (alapértelmezett), ESENT |MDB (alapértelmezett), ESENT|(Alapértelmezett), SQL Server, MDB ESENT

Kezdődően az 17090 kiadási [Windows Server Insider Preview](https://www.microsoft.com/en-us/software-download/windowsinsiderpreviewserver), SQL Server támogatott beállítás a lekéréses szolgáltatás a (Windows-szolgáltatás *DSC-szolgáltatás*).  Ez biztosítja, hogy új lehetőség a skálázás, nagy méretű DSC-környezetekben, amelyek nem áttelepített [Azure Automation DSC](/azure/automation/automation-dsc-getting-started).

> **Megjegyzés:**: SQL Server-támogatása nem kerül a korábbi verziók a WMF 5.1-es (vagy korábbi), és csak a Windows Server-verziók nagyobb vagy egyenlő 17090 elérhető lesz.

A lekérési kiszolgálójával, hogy az SQL Server konfigurálásához állítsa **SqlProvider** a `$true` és **SqlConnectionString** a egy érvényes SQL Server kapcsolati karakterláncát.  További információkért lásd: [SqlClient kapcsolati karakterláncok](/dotnet/framework/data/adonet/connection-string-syntax#sqlclient-connection-strings).
Például egy SQL Server-konfiguráció **xDscWebService**, először olvassa el [xDscWebService erőforrást használó](#using-the-xdscwebservice-resource) , és tekintse át a [Sample_xDscWebServiceRegistration_ A Githubon UseSQLProvider.ps1](https://github.com/PowerShell/xPSDesiredStateConfiguration/blob/master/Examples/Sample_xDscWebServiceRegistration_UseSQLProvider.ps1).

### <a name="using-the-xdscwebservice-resource"></a>A xDscWebService erőforrás segítségével

Lekérési kiszolgáló beállítása a legegyszerűbb módja az, hogy használja a **xDscWebService** erőforrás, szerepel a **xPSDesiredStateConfiguration** modul.
A következő lépések azt ismertetik, hogyan használhatja az erőforrást, amely beállítja a web service konfigurációban.

1. Hívja a [Install-Module](/powershell/module/PowershellGet/Install-Module) telepítésére szolgáló parancsmagot a **xPSDesiredStateConfiguration** modul. **Megjegyzés:**: **Install-Module** szerepel a **PowerShellGet** modult, amely része a PowerShell 5.0-s. Letöltheti a **PowerShellGet** modul a PowerShell 3.0 és 4.0-s verzióját, [PackageManagement PowerShell modul előzetes](https://www.microsoft.com/en-us/download/details.aspx?id=49186).
1. SSL-tanúsítvány a DSC lekéréses kiszolgálón le egy megbízható hitelesítésszolgáltató, vagy a szervezet vagy egy nyilvános szolgáltató belül. A szolgáltató kapott tanúsítvány általában a PFX formátumban van. Telepítse a tanúsítványt, amely a DSC lekéréses kiszolgálón az alapértelmezett helyen, amely lehet a CERT: \LocalMachine\My válnak a csomóponton. Jegyezze fel a tanúsítvány-ujjlenyomatot.
1. Válassza ki a regisztrációs kulcsát, használható egy GUID Azonosítót. Hozhat létre egy PowerShell-lel, írja be a következő, a PS-parancssorba, és nyomja le az enter: "``` [guid]::newGuid()```"vagy"```New-Guid```". Ezt a kulcsot a regisztráció során hitelesítsék magukat a megosztott kulcs lesz ügyfél csomópontja. További információkért tekintse meg a regisztrációs kulcsot az alábbi szakaszban.
1. A PowerShell ISE-ben (F5) a következő konfigurációs parancsfájl futtatásához (példák mappájában található a **xPSDesiredStateConfiguration** modul Sample_xDscWebServiceRegistration.ps1 mint). Ez a szkript állítja be a lekéréses kiszolgálón.

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

1. Futtassa a konfigurációt, az SSL-tanúsítvány ujjlenyomata átadása a **certificateThumbPrint** paraméter és a egy GUID regisztrációs kulcsát a **RegistrationKey** paramétert:

    ```powershell
    # To find the Thumbprint for an installed SSL certificate for use with the pull server list all certificates in your local store
    # and then copy the thumbprint for the appropriate certificate by reviewing the certificate subjects
    dir Cert:\LocalMachine\my

    # Then include this thumbprint when running the configuration
    Sample_xDscWebServiceRegistration -certificateThumbprint 'A7000024B753FA6FFF88E966FD6E19301FAE9CCC' -RegistrationKey '140a952b-b9d6-406b-b416-e0f759c9c0e4' -OutputPath c:\Configs\PullServer

    # Run the compiled configuration to make the target node a DSC Pull Server
    Start-DscConfiguration -Path c:\Configs\PullServer -Wait -Verbose
    ```

#### <a name="registration-key"></a>Regisztrációs kulcs

Ahhoz, hogy az ügyfél-csomópontokat, hogy a konfigurációs nevek helyett egy konfigurációs azonosító használatához regisztrálni a kiszolgálóval, a fenti konfigurációs által létrehozott regisztrációs kulcsát nevű fájlba mentése `RegistrationKeys.txt` a `C:\Program Files\WindowsPowerShell\DscService`. A regisztrációs kulcs egy közös titkos kulcsot használja a kezdeti regisztráció során az ügyfél és a lekéréses kiszolgálón működik. Az ügyfél, amely után a regisztráció sikeres elvégzése után a lekéréses kiszolgálón egyedi hitelesítésére használt önaláírt tanúsítványt hoz létre. Ez a tanúsítvány ujjlenyomatának helyileg tárolja, és a társított URL-címét a lekéréses kiszolgálón.
> **Megjegyzés:**: Regisztrációs kulcsok nem támogatottak a PowerShell 4.0-s verzióját.

Annak érdekében, hogy a pull-kiszolgálóval hitelesíteni csomópontok konfigurálásához, a regisztrációs kulccsal kell lennie az összes cél csomóponttal fog a lekéréses kiszolgálón kell Regisztrálás a metaconfiguration. Vegye figyelembe, hogy a **RegistrationKey** az alábbi metaconfiguration eltűnik, miután sikeresen regisztrálta a célgépen, és hogy az érték '140a952b-b9d6-406b-b416-e0f759c9c0e4' meg kell egyeznie a tárol a A lekérési kiszolgálón RegistrationKeys.txt fájlt. A regisztrációs kulcs értékét biztonságosan, mindig kezeli, mivel azt, hogy lehetővé teszi bármely a célgépen, a lekéréses kiszolgálón regisztrálni.

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

> **Megjegyzés:**: A **ReportServerWeb** szakasz lehetővé teszi, hogy a lekéréses kiszolgálón küldendő adatokról szóló jelentéseket küldeni.

Hiánya az **ConfigurationID** tulajdonság a metaconfiguration fájlban implicit módon azt jelenti, hogy a lekéréses kiszolgáló támogat a V2 verziójú lekéréses kiszolgálón protokollt így egy kezdeti regisztrációs megadása kötelező.
Ezzel szemben, a jelenléte egy **ConfigurationID** azt jelenti, hogy a lekéréses kiszolgálón protokoll V1 verzióját használja, és nincs a feldolgozás nem regisztrációs.

>**Megjegyzés:**: A LEKÜLDÉSES forgatókönyvekben jelentse a jelenlegi kiadásban, amellyel meg kell határozni egy ConfigurationID tulajdonság egy lekéréses kiszolgálót soha nem regisztrált csomópontok metaconfiguration fájlban szerepel. Ezzel a V1 lekéréses kiszolgálón protokoll kényszerítése és regisztrációs hibaüzenetek elkerülése érdekében.

## <a name="placing-configurations-and-resources"></a>Konfigurációkat és erőforrásokat elhelyezése

Miután a lekéréses server telepítésének befejezése határozzák meg a mappák a **ConfigurationPath** és **ModulePath** a pull-kiszolgálói konfigurációban a tulajdonságok akkor, hogy hol helyezi el a modulok és konfigurációk amely lekéréses cél csomópontok elérhető lesz.
Ezeket a fájlokat kell lennie ahhoz, hogy a pull-kiszolgáló megfelelően feldolgozza őket egy meghatározott formátumban.

### <a name="dsc-resource-module-package-format"></a>DSC erőforrás modul csomag formátuma

Minden egyes erőforrás modulnak kell zip és a következő mintának megfelelően nevű `{Module Name}_{Module Version}.zip`.
Ha például 3.1.2.0 modul verziójával xWebAdminstration modul neve "xWebAdministration_3.2.1.0.zip".
Minden egyes modul verzióját tartalmaznia kell egy egyetlen zip-fájlt.
Mivel minden egyes zip-fájlt az erőforráshoz csak egyetlen verziója, a WMF 5.0-s egyetlen címtárban több modul verzió támogatása hozzáadva a modul formátum nem támogatott.
Ez azt jelenti, hogy becsomagolást mentése erőforrás modulok DSC lekéréses kiszolgálón való használatra előtt ki kell, hogy módosítsa a könyvtár struktúra.
Az alapértelmezett formátum a modulok DSC-erőforrás a WMF 5.0 tartalmazó "{modul mappáját}\{Modulverzió} \DscResources\{DSC Erőforrásmappa}\'.
Terveztük a lekérési kiszolgálón csomagolást, előtt távolítsa el a **{modul version}** mappát az elérési út válik, így a(z) {modul mappáját} \DscResources\{DSC Erőforrásmappa}\'.
A mappa az módosítása zip-fent leírtak szerint, és helyezze ezeket a zip-fájlokat a **ModulePath** mappát.

Használat `New-DscChecksum {module zip file}` az újonnan hozzáadott modul ellenőrzőösszeg fájl létrehozásához.

### <a name="configuration-mof-format"></a>Konfigurációs MOF-formátuma

A konfigurációs MOF-fájlt kell ellenőrzőösszeg fájl párosítani, hogy a cél csomópont egy LCM ellenőrizheti a konfigurációt.
Ellenőrzőösszeg létrehozásához hívja a [New-DscChecksum](/powershell/module/PSDesiredStateConfiguration/New-DscChecksum) parancsmagot.
A parancsmag lép egy **elérési út** paraméter, amely a mappát, ahol a konfigurációs MOF található.
A parancsmag létrehoz egy ellenőrzőösszeg-fájlt `ConfigurationMOFName.mof.checksum`, ahol `ConfigurationMOFName` a konfigurációs mof-fájl neve.
Ha egynél több konfigurációs MOF-fájlok a megadott mappában, a mappában az egyes konfigurációkhoz egy ellenőrzőösszeg jön létre.
A MOF-fájlok és az azokhoz társított ellenőrzőösszeg fájlokat helyezze a **ConfigurationPath** mappát.

>**Megjegyzés:**: Ha módosítja a konfigurációs MOF-fájl bármilyen módon, az ellenőrzőösszeg-fájl is létre kell hoznia.

### <a name="tooling"></a>Eszköztámogatás

Annak érdekében, hogy a beállítás alkotják, ellenőrzése és felügyelete egyszerűbb, a lekéréses kiszolgálón a következő eszközöket is a xPSDesiredStateConfiguration modul legújabb verziója található példák:

1. A modul, amely segít a csomagolási DSC erőforrás modulok és konfigurációs fájljait használja a lekérési kiszolgálón. [PublishModulesAndMofsToPullServer.psm1](https://github.com/PowerShell/xPSDesiredStateConfiguration/blob/master/DSCPullServerSetup/PublishModulesAndMofsToPullServer.psm1). Az alábbi példákat:

    ```powershell
        # Example 1 - Package all versions of given modules installed locally and MOF files are in c:\LocalDepot
         $moduleList = @('xWebAdministration', 'xPhp')
         Publish-DSCModuleAndMof -Source C:\LocalDepot -ModuleNameList $moduleList

         # Example 2 - Package modules and mof documents from c:\LocalDepot
         Publish-DSCModuleAndMof -Source C:\LocalDepot -Force
    ```

1. A parancsfájl, amely ellenőrzi a lekérési kiszolgálón megfelelően van konfigurálva. [PullServerSetupTests.ps1](https://github.com/PowerShell/xPSDesiredStateConfiguration/blob/master/DSCPullServerSetup/PullServerDeploymentVerificationTest/PullServerSetupTests.ps1).

## <a name="community-solutions-for-pull-service"></a>Közösségi megoldások lekéréses szolgáltatás

A DSC-Közösség készített rendelkezik több megoldás megvalósítása a lekéréses szolgáltatás protokollt.
A helyszíni környezetben ezek ajánlat lekéréses szolgáltatásfunkciók és a egy lehetőség, hogy hozzájáruljanak a Közösség növekményes fejlesztései.

- [Vontatóhajó](https://github.com/powershellorg/tug)
- [DSC-TRÆK](https://github.com/powershellorg/dsc-traek)

## <a name="pull-client-configuration"></a>Lekérési ügyfél-konfiguráció

Az alábbi témakörök ismertetik részletesen pull-ügyfelek beállítását:

- [Egy konfigurációs azonosítóval DSC lekérési ügyfél beállítása](pullClientConfigID.md)
- [Konfigurációs nevekkel DSC lekérési ügyfél beállítása](pullClientConfigNames.md)
- [Részleges konfigurációk](partialConfigs.md)

## <a name="see-also"></a>Lásd még:

- [Windows PowerShell Desired State Configuration áttekintése](../overview/overview.md)
- [Konfigurációk életbe léptetése](enactingConfigurations.md)
- [A DSC jelentéskészítő kiszolgálójának használata](reportServer.md)
- [[MS-DSCPM]: A lekéréses modell protokoll Desired State Configuration](https://msdn.microsoft.com/library/dn393548.aspx)
- [[MS-DSCPM]: A lekéréses modell protokoll hibajegyzék Desired State Configuration](https://msdn.microsoft.com/library/mt612824.aspx)
