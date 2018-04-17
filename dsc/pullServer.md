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
# <a name="desired-state-configuration-pull-service"></a>Célállapot-konfiguráló lekéréses szolgáltatása

> Vonatkozik: A Windows PowerShell 5.0

> [!IMPORTANT]
> A lekéréses kiszolgáló (Windows-szolgáltatás *DSC-szolgáltatás*), Windows Server támogatott összetevője létezik azonban a következők: nem tervezi, hogy új funkciók és képességek kínálnak. Javasoljuk, hogy kezdje a Váltás felügyelt ügyfelek [Azure Automation DSC](/azure/automation/automation-dsc-getting-started) (tartalmazza a Windows Server-kiszolgáló lekéréses is) vagy a közösségi megoldásoknak a valamelyikét felsorolt [Itt](pullserver.md#community-solutions-for-pull-service).

Helyi Configuration Manager Service lekéréses megoldás központilag kezelhető.
Ez a módszer használata esetén a csomópont kezelt regisztrálva a szolgáltatásban, és LCM beállítások a konfigurációs hozzárendelni.
A konfiguráció szerint függőségeinek a konfigurációs szükséges összes DSC erőforrásokat a számítógép letölti és LCM felügyelje a konfigurációt használja.
A felügyelt számítógép állapotára vonatkozó adatokat tölt fel az a jelentéskészítés szolgáltatás.
Ez a neve "szolgáltatás lekéréses."

Az aktuális lekéréses szolgáltatás beállításai a következők:

- Azure Automation kívánt állapot konfigurációs szolgáltatás
- Windows Server rendszeren futó lekéréses szolgáltatás
- Közösségi nyílt forráskódú megoldások karbantartása
- SMB-megosztáson

**Az ajánlott megoldás**, és a lehetőség érhető el, a legtöbb szolgáltatásokkal [Azure Automation DSC](/azure/automation/automation-dsc-getting-started).

Az Azure-szolgáltatás csomópontok helyszíni saját adatközpontját, illetve például az Azure és az AWS nyilvános felhőket is kezelheti.
Személyes környezetekben, ahol kiszolgálók nem közvetlenül csatlakozik az internethez, fontolja meg, ezzel a kimenő forgalom csak a közzétett Azure IP-címtartomány (lásd: [Azure Datacenter IP-címtartományok](https://www.microsoft.com/en-us/download/details.aspx?id=41653)).

Az online szolgáltatás, amely még nem állnak rendelkezésre az lekéréses szolgáltatásban, a Windows Server funkciói:
- Összes adata titkosításra kerül az átvitel során, és inaktív
- Ügyfél-tanúsítványok létrehozása és kezelése automatikusan
- Titkos kulcsok tárolására központilag kezelésére szolgáló [jelszavak és a hitelesítő adatok](/azure/automation/automation-credentials), vagy [változók](/azure/automation/automation-variables) például a kiszolgáló nevét vagy a kapcsolati karakterláncok
- Központilag kezelheti a csomópont [LCM konfiguráció](metaConfig.md#basic-settings)
- Központilag konfigurációk kiosztása ügyfél csomópontok
- Kiadás configuration "Kanári csoportok" éles elérése előtt tesztelési módosításai
- Grafikus jelentési
  - A granularitási DSC erőforrás szintjén állapotának részletei
  - Az ügyfél gépek hibaelhárítási részletes hibaüzenetek
- [Integráció az Azure Naplóelemzés](/azure/automation/automation-dsc-diagnostics) riasztások, automatikus feladatokat, jelentések és riasztási Android vagy iOS-alkalmazás

## <a name="dsc-pull-service-in-windows-server"></a>A DSC lekérési szolgáltatás a Windows Server

Akkor lehet egy lekéréses szolgáltatást, hogy a Windows Serveren futó konfigurálására.
Befolyásolható, hogy a lekéréses service megoldás a Windows Serverben megtalálható tartalmaz-e a konfigurációk/modulok letölthető tárolása, és a jelentés adatokat az rögzítése csak képességeit.
Nem tartalmazza az Azure-ban a szolgáltatás által kínált képességeket, és ezért nincs értékeléséhez, hogyan szeretné használni a szolgáltatás egy jó eszköz.

A lekéréses szolgáltatás, a Windows Server egy olyan webes szolgáltatás az IIS-ben elérhetővé DSC konfigurációs fájlokat a célcsomópontokat azokat a csomópontokat, kérje meg őket az OData-illesztőfelület használó.

A lekérési kiszolgálójával használatának követelményei:

- Futtató kiszolgálón:
  - WMF/PowerShell 5.0-s vagy újabb
  - IIS-kiszolgálói szerepkör
  - A DSC szolgáltatás
- Ideális esetben egyes azt jelenti, hogy egy tanúsítványgenerálás során, a biztonságos hitelesítő adatok a helyi Configuration Manager (LCM) számára átadott a célcsomópontokat

A legjobb konfigurálja a Windows Server a gazdaszolgáltatás lekéréses módja a DSC-konfiguráció.
Példa parancsfájl lejjebb tekinthetők meg.

### <a name="supported-database-systems"></a>Támogatott adatbázis-rendszerek

|WMF 4.0   |WMF 5.0  |WMF 5.1 |WMF 5.1 (a Windows Server Insider Preview 17090)|
|---------|---------|---------|---------|
|MDB     |ESENT (alapértelmezett), Postaláda |ESENT (alapértelmezett), Postaláda|(Alapértelmezett), az SQL Server MDB ESENT

Kezdve a 17090 kiadási [Windows Server Insider Preview](https://www.microsoft.com/en-us/software-download/windowsinsiderpreviewserver), SQL Server támogatott beállítás a lekéréses szolgáltatás (Windows-szolgáltatás *DSC-szolgáltatás*).  Ez biztosítja, hogy egy új beállítás nem áttelepített nagy DSC környezetek méretezéshez [Azure Automation DSC](/azure/automation/automation-dsc-getting-started).

> **Megjegyzés:**: SQL Server-támogatása nem lesz felvéve a korábbi verziókra WMF 5.1 (vagy korábbi), és csak a Windows Server-verziók kisebb 17090 elérhető lesz.

A lekérési kiszolgálójával, hogy az SQL Server használata konfigurálásához állítsa **SqlProvider** való `$true` és **SqlConnectionString** egy érvényes SQL Server kapcsolati karakterlánc módosításait.  További információkért lásd: [SqlClient kapcsolati karakterláncok](/dotnet/framework/data/adonet/connection-string-syntax#sqlclient-connection-strings).
Például egy SQL Server-konfiguráció **xDscWebService**, elolvashatja [xDscWebService erőforrást használó](#using-the-xdscwebservice-resource) és tekintse át a [Sample_xDscWebServiceRegistration_ A Githubon UseSQLProvider.ps1](https://github.com/PowerShell/xPSDesiredStateConfiguration/blob/master/Examples/Sample_xDscWebServiceRegistration_UseSQLProvider.ps1).

### <a name="using-the-xdscwebservice-resource"></a>A xDscWebService erőforrás használata

A legegyszerűbben úgy állítsa be a webkiszolgáló lekéréses használatára a **xDscWebService** erőforrás szerepel a **xPSDesiredStateConfiguration** modul.
Az alábbi lépések ismertetik az erőforrás használata, amely beállítja a webszolgáltatás konfigurációban.

1. Hívja a [Install-modul](/powershell/module/PowershellGet/Install-Module) telepítésére szolgáló parancsmagot a **xPSDesiredStateConfiguration** modul. **Megjegyzés:**: **Install-modul** megtalálható a **PowerShellGet** modul, amely PowerShell 5.0 szerepel. Letöltheti a **PowerShellGet** modul a PowerShell 3.0 és 4.0-s verzióját, [PackageManagement PowerShell modulok előzetes](https://www.microsoft.com/en-us/download/details.aspx?id=49186).
1. Az SSL-tanúsítvány lekérése a DSC lekérési kiszolgálójával megbízható hitelesítésszolgáltatótól származó, vagy a szervezet vagy egy nyilvános szolgáltató belül. A szervezet kapott tanúsítvány általában a PFX formátumban van. Telepítse a tanúsítványt a csomóponton a DSC lekérési kiszolgálójával, hogy CERT: \LocalMachine\My alkalmazandó alapértelmezett helyen lesz. Jegyezze fel a tanúsítvány-ujjlenyomatot.
1. Válassza ki a regisztrációs kulcsot használ egy GUID Azonosítót. Hozhat létre egy PowerShell-lel írja be a következő, a PS-parancssorba, és nyomja le az enter: "``` [guid]::newGuid()```"vagy"```New-Guid```". Ez a kulcs által használandó ügyfél-csomópontok egy megosztott kulcsot, hitelesítéséhez a regisztráció során. További információkért tekintse meg a regisztrációs kulcsot következő szakaszban.
1. A PowerShell ISE (F5) a következő konfigurációs parancsfájl futtatásához (például mappájában található a **xPSDesiredStateConfiguration** Sample_xDscWebServiceRegistration.ps1 modul). Ezt a parancsfájlt hoz létre a lekérési kiszolgálójával.

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

#### <a name="registration-key"></a>Regisztrációs kulcs

Teszi lehetővé az ügyfélszámítógépek csomópontok regisztrálni a kiszolgálót, hogy használhatnak konfigurációs nevek helyett egy konfigurációs Azonosítót, egy regisztrációs kulcsot, amely a fenti konfigurációban készült nevű fájlba mentése `RegistrationKeys.txt` a `C:\Program Files\WindowsPowerShell\DscService`. A regisztrációs kulcs funkciókkal, mint a kezdeti regisztráció során az ügyfél és a lekéréses kiszolgáló által használt megosztott titkos kulcs. Az ügyfél létrehoz egy önaláírt tanúsítványt, amellyel egyedi módon a kiszolgálón elvégzett hitelesítéshez lekéréses Ha regisztrálása sikeresen befejeződött. Ez a tanúsítvány ujjlenyomatának helyileg tárolja és társított a lekérési kiszolgálójával URL-CÍMÉT.
> **Megjegyzés:**: PowerShell 4.0-s verzióját nem támogatja a regisztrációs kulccsal.

Ahhoz, hogy egy csomópont a a lekérési kiszolgálón való hitelesítéshez szükséges konfigurálásához a regisztrációs kulcsot kell lennie az összes cél csomóponttal fog a lekérési kiszolgálójával kell regisztrálása metakonfigurációját. Vegye figyelembe, hogy a **RegistrationKey** az alábbi metakonfigurációját tartalomkonvertálást követően törlődik a célként megadott gép sikeresen regisztrálta, és hogy a "140a952b-b9d6-406b-b416-e0f759c9c0e4" értékét meg kell egyeznie az értékeket a A lekérési kiszolgálón RegistrationKeys.txt fájlt. A regisztrációs kulcs értékét biztonságosan, mindig kezelni, mert ismerete, hogy lehetővé teszi, hogy a célszámítógép regisztrálni a lekérési kiszolgálójával.

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

> **Megjegyzés:**: A **ReportServerWeb** szakasz lehetővé teszi a lekérési kiszolgálójával küldendő jelentésadatait.

A hiánya a **ConfigurationID** tulajdonság a metakonfigurációját fájlban implicit módon azt jelenti, hogy a lekéréses kiszolgáló a V2 verziójú kiszolgáló lekéréses protokollt támogat, egy kezdeti regisztrációs szükség.
Ezzel ellentétben a jelenléte egy **ConfigurationID** azt jelenti, hogy a lekéréses protokoll a V1-es verziót használja, és nincs regisztrálása feldolgozási.

>**Megjegyzés:**: a forgatókönyvben a egy LEKÜLDÉSES programhiba van a jelenlegi kiadásban, így meg kell határozni egy ConfigurationID tulajdonság egy lekérési kiszolgálójával soha nem regisztrált csomópontok metakonfigurációját fájlban. Ezzel a V1 lekéréses protokoll kényszerítése és elkerülése érdekében a regisztrációs hibaüzenetek.

## <a name="placing-configurations-and-resources"></a>Konfigurációk és erőforrások

Miután a lekéréses server telepítésének befejezése határozzák meg a mappák a **ConfigurationPath** és **ModulePath** tulajdonságok a lekéréses kiszolgáló konfigurációjában: hol helyezi el a modulok és konfigurációk elérhető a célcsomópontokat való lekérésére fogja tárolni.
Ezeket a fájlokat kell lennie ahhoz, hogy a lekérési kiszolgálójával, hogy helyesen dolgozza fel őket egy meghatározott formátumban.

### <a name="dsc-resource-module-package-format"></a>A DSC erőforrás modul csomag formátuma

Minden erőforrás modul zip és megfelelő a következő mintát kell `{Module Name}_{Module Version}.zip`.
Például 3.1.2.0 modul verziójával xWebAdminstration nevű modul volna neve "xWebAdministration_3.2.1.0.zip".
Egy modul verziói szerepelnie kell egy egyetlen zip-fájlt.
Mivel minden egyes zip-fájlban szereplő erőforrás csak egyetlen verziója van telepítve, a WMF 5.0 támogatja a több verziója egyetlen könyvtárban hozzáadott modul formátum nem támogatott.
Ez azt jelenti, hogy csomagolási erőforrás modulok DSC lekérési kiszolgálójával való használatra mentése előtt szüksége lesz a könyvtárstruktúra kis módosítja.
Az alapértelmezett DSC erőforrást a WMF 5.0 tartalmazó modulok formátuma "{modul mappa}\{verziója} \DscResources\{DSC Erőforrásmappa}\'.
Előtt feliratkozott a lekérési kiszolgálójával csomagolása, távolítsa el a **{verziója}** mappában, így az elérési útja bekerül a(z) {modul mappa} \DscResources\{DSC Erőforrásmappa}\'.
A mappa az módosítását zip-fent leírt módon, és ezek a zip-fájlok a **ModulePath** mappa.

Használjon `New-DscChecksum {module zip file}` az újonnan hozzáadott modul ellenőrzőösszeg-fájl létrehozásához.

### <a name="configuration-mof-format"></a>Konfigurációs MOF formátuma

Konfigurációs MOF-fájlt kell, hogy egy LCM a cél csomópont azt is ellenőrzi a konfigurációt az ellenőrzőösszeg-fájl megfeleltetni.
Hozzon létre egy ellenőrzőösszeg, hívja meg a [New-DscChecksum](/powershell/module/PSDesiredStateConfiguration/New-DscChecksum) parancsmag.
A parancsmag tart egy **elérési** paraméter meghatározza, hogy a mappát, ahol a konfigurációs MOF található.
A parancsmag létrehoz egy ellenőrzőösszeg nevű `ConfigurationMOFName.mof.checksum`, ahol `ConfigurationMOFName` a konfigurációs mof-fájl neve.
Ha egynél több konfigurációs MOF-fájlok a megadott mappában, ellenőrzőösszeg minden konfigurációs a mappában létrejön.
A MOF-fájlok és az azokhoz társított ellenőrzőösszeg fájlokat helyezze a **ConfigurationPath** mappa.

>**Megjegyzés:**: Ha megváltoztatja a konfigurációs MOF-fájl bármely olyan módon, az ellenőrzőösszeg-fájl is kell hozni.

### <a name="tooling"></a>Tooling eszköz

Annak érdekében, hogy a beállítás, érvényesítése és a könnyebb, lekéréses kiszolgáló felügyelete a következő eszközök érhetők el a legújabb verzió xPSDesiredStateConfiguration modul példaként:

1. Ez a modul, amely segít csomagolási DSC erőforrás modulok és konfigurációs fájljait a lekérési kiszolgálón. [PublishModulesAndMofsToPullServer.psm1](https://github.com/PowerShell/xPSDesiredStateConfiguration/blob/master/DSCPullServerSetup/PublishModulesAndMofsToPullServer.psm1). Az alábbi példák:

    ```powershell
        # Example 1 - Package all versions of given modules installed locally and MOF files are in c:\LocalDepot
         $moduleList = @('xWebAdministration', 'xPhp')
         Publish-DSCModuleAndMof -Source C:\LocalDepot -ModuleNameList $moduleList

         # Example 2 - Package modules and mof documents from c:\LocalDepot
         Publish-DSCModuleAndMof -Source C:\LocalDepot -Force
    ```

1. Egy parancsfájl, amely ellenőrzi a lekérési kiszolgálójával megfelelően van konfigurálva. [PullServerSetupTests.ps1](https://github.com/PowerShell/xPSDesiredStateConfiguration/blob/master/DSCPullServerSetup/PullServerDeploymentVerificationTest/PullServerSetupTests.ps1).

## <a name="community-solutions-for-pull-service"></a>Közösségi megoldások lekéréses szolgáltatás

A DSC-Közösség rendelkezik létrehozott több megoldások megvalósításához a lekéréses szolgáltatás protokoll.
A helyszíni környezetben ezek ajánlatot lekéréses szolgáltatás képességei és hozzájárulnak a Közösség növekményes fejlesztések lehetőséget.

- [Vontatóhajó](https://github.com/powershellorg/tug)
- [A DSC-TRÆK](https://github.com/powershellorg/dsc-traek)

## <a name="pull-client-configuration"></a>Leküldéses ügyfél-konfiguráció

A következő témakörök ismertetik részletesen lekéréses ügyfelek beállítása:

- [Egy konfigurációs azonosítójával DSC lekérési ügyfél beállítása](pullClientConfigID.md)
- [Konfigurációs nevek használatával DSC lekérési ügyfél beállítása](pullClientConfigNames.md)
- [Részleges konfigurációk](partialConfigs.md)

## <a name="see-also"></a>Lásd még:

- [A Windows PowerShell célállapot-konfiguráló áttekintése](overview.md)
- [Konfigurációk életbe léptetése](enactingConfigurations.md)
- [A DSC jelentéskészítő kiszolgálójának használata](reportServer.md)