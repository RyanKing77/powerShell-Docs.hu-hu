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
# <a name="desired-state-configuration-pull-service"></a>A kívánt állapot konfigurációjának lekérése szolgáltatás

> [!IMPORTANT]
> A lekérési kiszolgáló (Windows *-szolgáltatás DSC-Service*) a Windows Server támogatott összetevője, azonban nincsenek új funkciók vagy képességek kínáló csomagok. Ajánlott megkezdeni a felügyelt ügyfelek átváltását [Azure Automation DSC](/azure/automation/automation-dsc-getting-started) -re (beleértve a Windows Serveren futó lekéréses kiszolgálón túli szolgáltatásokat) vagy az [itt](pullserver.md#community-solutions-for-pull-service)felsorolt közösségi megoldások egyikét.

A helyi Configuration Manager a lekéréses szolgáltatási megoldás központilag kezelhető.
Ezen módszer használatakor a felügyelt csomópont regisztrálva van egy szolgáltatásban, és a konfigurációt az LCD-beállításokban kell kijelölni.
A konfiguráció és az összes olyan DSC-erőforrás, amely a konfiguráció függőségeire van szükség, a rendszer letölti a gépre, és az LCD ChipOnGlas használatával kezeli a konfigurációt.
A rendszer feltölti a felügyelt számítógép állapotára vonatkozó adatokat a jelentéskészítéshez.
Ezt a koncepciót "lekéréses szolgáltatásnak" nevezzük.

A lekéréses szolgáltatás jelenlegi beállításai a következők:

- Azure Automation kívánt állapot-konfigurációs szolgáltatás
- Windows Serveren futó lekéréses szolgáltatás
- A Közösség által karbantartott nyílt forráskódú megoldások
- SMB-megosztás

**A javasolt megoldás**, valamint a legtöbb elérhető funkció, [Azure Automation DSC](/azure/automation/automation-dsc-getting-started).

Az Azure-szolgáltatás a helyszíni csomópontokat a privát adatközpontokban vagy nyilvános felhőkben, például az Azure-ban és az AWS-ben is képes kezelni.
Olyan privát környezetekben, ahol a kiszolgálók nem tudnak közvetlenül csatlakozni az internethez, érdemes lehet csak a közzétett Azure IP-tartományra korlátozni a kimenő forgalmat (lásd: [Azure-adatközpont IP-címtartományok](https://www.microsoft.com/en-us/download/details.aspx?id=41653)).

A Windows Server lekéréses szolgáltatásában jelenleg nem elérhető online szolgáltatás szolgáltatásai a következők:

- Minden adatforgalom titkosítva van az átvitel és a nyugalmi állapotban
- Az ügyféltanúsítványok automatikusan jönnek létre és kezelhetők
- Secrets Store a jelszavak és a [hitelesítő adatok](/azure/automation/automation-credentials)központilag történő kezeléséhez, illetve [változókhoz](/azure/automation/automation-variables) , például kiszolgálónévekhez vagy a kapcsolatok karakterláncához
- Csomópontos LCD- [konfiguráció](../managing-nodes/metaConfig.md#basic-settings) központi kezelése
- Konfigurációk központi kiosztása az ügyfél csomópontjaihoz
- A "Kanári-csoportokra" vonatkozó konfigurációs változások kiadása az éles környezet elérése előtt
- Grafikus jelentéskészítés
  - A részletességi szintű DSC-erőforrás részletességi állapota
  - Részletes hibaüzenetek az ügyfélszámítógépektől a hibaelhárításhoz
- [Integráció az Azure log Analytics](/azure/automation/automation-dsc-diagnostics) a riasztásokhoz, automatizált feladatokhoz, Android/iOS-alkalmazásokhoz jelentéskészítéshez és riasztásokhoz

## <a name="dsc-pull-service-in-windows-server"></a>DSC lekéréses szolgáltatás a Windows Server rendszerben

A lekéréses szolgáltatás beállítható úgy, hogy a Windows Serveren fusson.
Javasoljuk, hogy a Windows Serverben található lekéréses szolgáltatási megoldás csak a konfigurációk/modulok tárolására szolgáló képességeket tartalmazza, amelyekkel letöltheti és rögzítheti a jelentési adatmennyiségeket az adatbázisba.
Nem tartalmazza a szolgáltatás által az Azure-ban kínált számos képességet, ezért nem jó eszköz a szolgáltatás használatának kiértékeléséhez.

A Windows Server rendszerben kínált lekéréses szolgáltatás egy OData felületet használó webszolgáltatás, amely a DSC konfigurációs fájljait elérhetővé teszi a célként megadott csomópontok számára, amikor ezek a csomópontok kérik őket.

A lekéréses kiszolgáló használatára vonatkozó követelmények:

- Egy rendszert futtató kiszolgáló:
  - WMF/PowerShell 4,0 vagy újabb
  - IIS-kiszolgálói szerepkör
  - DSC szolgáltatás
- Ideális esetben a tanúsítvány előállításához szükséges hitelesítő adatok biztonságossá tétele a helyi Configuration Manager (LCD ChipOnGlas) számára a célként megadott csomópontokon

A Windows Server lekéréses szolgáltatásként való konfigurálásának legjobb módja a DSC-konfiguráció használata.
Alább talál egy példát a parancsfájlra.

### <a name="supported-database-systems"></a>Támogatott adatbázis-rendszerek

|WMF 4.0   |WMF 5.0  |WMF 5.1 |WMF 5,1 (Windows Server Insider előzetes verzió 17090)|
|---------|---------|---------|---------|
|MDB     |ESENT (alapértelmezett), MDB |ESENT (alapértelmezett), MDB|ESENT (alapértelmezett), SQL Server, MDB

A [Windows Server Insider előzetes](https://www.microsoft.com/en-us/software-download/windowsinsiderpreviewserver)verziójának 17090-es verziójától kezdve SQL Server a lekéréses szolgáltatás (Windows-szolgáltatás *DSC-Service*) támogatott lehetősége. Ez új lehetőséget biztosít a nagy DSC-környezetek méretezésére, amelyek nem lettek áttelepítve a [DSC-Azure Automation](/azure/automation/automation-dsc-getting-started).

> [!NOTE]
> SQL Server támogatás nem lesz hozzáadva a WMF 5,1 korábbi verzióihoz (vagy korábbi verziókhoz), és csak a 17090-nál nagyobb vagy azzal egyenlő Windows Server-verziókban lesz elérhető.

A lekéréses kiszolgáló a SQL Server használatára való konfigurálásához állítsa `$true` a **SqlProvider** és a **sqlConnectionString** érvényes SQL Server-kapcsolódási karakterláncra. További információ: SqlClient- [kapcsolatok karakterláncai](/dotnet/framework/data/adonet/connection-string-syntax#sqlclient-connection-strings).
A **xDscWebService**-vel való SQL Server konfigurációra például először olvassa el [a xDscWebService](#using-the-xdscwebservice-resource) -erőforrást, majd tekintse át a [Sample_xDscWebServiceRegistration_UseSQLProvider. ps1 programot a githubon](https://github.com/PowerShell/xPSDesiredStateConfiguration/blob/master/Examples/Sample_xDscWebServiceRegistration_UseSQLProvider.ps1).

### <a name="using-the-xdscwebservice-resource"></a>A xDscWebService erőforrás használata

A web pull-kiszolgáló beállításának legegyszerűbb módja a **xPSDesiredStateConfiguration** modulban található **xDscWebService** -erőforrás használata.
A következő lépések azt ismertetik, hogyan használható az erőforrás egy olyan konfigurációban, amely beállítja a webszolgáltatást.

1. A **xPSDesiredStateConfiguration** modul telepítéséhez hívja meg az [install-Module](/powershell/module/PowershellGet/Install-Module) parancsmagot.
   > [!NOTE]
   > A **install-Module** a PowerShell 5,0 részét képező **PowerShellGet** modul része. A PowerShell 3,0-es és 4,0-es **PowerShellGet** -modulját a [PackageManagement PowerShell-modulok előzetes](https://www.microsoft.com/en-us/download/details.aspx?id=49186)verziójában töltheti le.
2. Szerezze be a DSC lekérési kiszolgálójának SSL-tanúsítványát egy megbízható hitelesítésszolgáltatótól, akár a szervezetén belül, akár egy nyilvános szolgáltatóban. A szolgáltatótól kapott tanúsítvány általában PFX formátumú.
3. Telepítse a tanúsítványt azon a csomóponton, amely a DSC lekérési kiszolgáló lesz az alapértelmezett helyen, amelynek `CERT:\LocalMachine\My`a következőnek kell lennie:.
   - Jegyezze fel a tanúsítvány ujjlenyomatát.
4. Válassza ki a regisztrációs kulcsként használni kívánt GUID azonosítót. A PowerShell használatával történő létrehozáshoz írja be a következőt a PS parancssorba, `[guid]::newGuid()` majd `New-Guid`nyomja le az ENTER billentyűt: vagy. Ezt a kulcsot az ügyféloldali csomópontok használják megosztott kulcsként a regisztráció során történő hitelesítéshez. További információt az alábbi regisztrációs kulcs című szakaszban talál.
5. A PowerShell ISE-ben indítsa el (F5) a következő konfigurációs szkriptet (a **xPSDesiredStateConfiguration** modul `Sample_xDscWebServiceRegistration.ps1`példák mappájába). Ez a szkript beállítja a lekérési kiszolgálót.

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

6. Futtassa a konfigurációt, és adja át az SSL-tanúsítvány ujjlenyomatát a **certificateThumbPrint** paraméterként, valamint egy GUID regisztrációs kulcsot a **RegistrationKey** paraméterként:

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

Annak engedélyezéséhez, hogy az ügyféloldali csomópontok regisztráljanak a- `RegistrationKeys.txt` `C:\Program Files\WindowsPowerShell\DscService`kiszolgálóval, hogy a konfigurációs neveket a konfigurációs azonosító helyett tudják használni, a fenti konfiguráció által létrehozott regisztrációs kulcsot a rendszer menti egy nevű fájlba. A regisztrációs kulcs olyan közös titokként működik, amelyet az ügyfél a lekérési kiszolgálóval végzett kezdeti regisztráció során használt. Az ügyfél olyan önaláírt tanúsítványt fog előállítani, amelyet a rendszer a lekéréses kiszolgáló egyedi hitelesítéséhez használ a regisztráció sikeres befejeződése után. A Tanúsítvány ujjlenyomata helyileg tárolódik, és a lekérési kiszolgáló URL-címéhez van társítva.

> [!NOTE]
> A regisztrációs kulcsok nem támogatottak a PowerShell 4,0-ben.

Ahhoz, hogy a csomópontot a lekérési kiszolgálóval való hitelesítésre konfigurálja, a regisztrációs kulcsnak a lekérési kiszolgálóval regisztrálni kívánt metaconfiguration kell lennie. Vegye figyelembe, hogy az alábbi metaconfiguration lévő **RegistrationKey** a célszámítógép sikeres regisztrálását követően törlődik, és az értéknek meg kell egyeznie a lekérési kiszolgálón található `RegistrationKeys.txt` fájlban tárolt értékkel (" 140a952b-b9d6-406b-b416-e0f759c9c0e4 "ebben a példában). Mindig biztonságos módon kezelje a regisztrációs kulcs értékét, mert tudván, hogy bármely célszámítógép regisztrálható a lekérési kiszolgálón.

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
> A **ReportServerWeb** szakasz lehetővé teszi jelentéskészítési adatküldés küldését a lekérési kiszolgálónak.

A metaconfiguration fájl **ConfigurationID** tulajdonságának hiánya implicit módon azt jelenti, hogy a lekérési kiszolgáló támogatja a lekérési kiszolgáló protokolljának v2-es verzióját, így kezdeti regisztrációra van szükség.
Ezzel szemben a **ConfigurationID** jelenléte azt jelenti, hogy a lekéréses kiszolgáló protokolljának v1-es verziója van használatban, és nincs regisztrációs feldolgozás.

> [!NOTE]
> Egy leküldéses forgatókönyvben hiba történt a jelenlegi kiadásban, amely szükségessé teszi a ConfigurationID tulajdonság definiálását a metaconfiguration-fájlban olyan csomópontok esetében, amelyek még nem regisztráltak lekéréses kiszolgálóval. Ez kényszeríti a v1 lekéréses kiszolgáló protokollját, és elkerüli a regisztrációs hibák üzeneteit.

## <a name="placing-configurations-and-resources"></a>Konfigurációk és erőforrások elhelyezése

A lekérési kiszolgáló telepítésének befejezése után a lekérési kiszolgáló konfigurációjában a **ConfigurationPath** és a **ModulePath** tulajdonság által meghatározott mappák a lekéréses csomópontok számára elérhető modulok és konfigurációk helyét fogják elhelyezni.
Ezeknek a fájloknak egy adott formátumban kell lenniük ahhoz, hogy a lekérési kiszolgáló megfelelően feldolgozza őket.

### <a name="dsc-resource-module-package-format"></a>DSC erőforrás modul csomag formátuma

Az egyes erőforrás-modulokat a következő minta `{Module Name}_{Module Version}.zip`szerint kell kibontani és elnevezni.

Például egy xWebAdminstration nevű modul, amely a 3.1.2.0 modul verzióját fogja nevezni `xWebAdministration_3.1.2.0.zip`.
Egy modul minden egyes verziójának egyetlen zip-fájlban kell szerepelnie.
Mivel az egyes zip-fájlokban csak egyetlen verziójú erőforrás található, a WMF 5,0-ben hozzáadott modul formátuma nem támogatott egyetlen címtárban.
Ez azt jelenti, hogy a DSC-erőforrás moduljainak a lekérési kiszolgálón való használatának megkezdése előtt kis módosítást kell végeznie a címtár struktúráján.
A DSC-erőforrást tartalmazó modulok alapértelmezett formátuma a WMF `{Module Folder}\{Module Version}\DscResources\{DSC Resource Folder}\`5,0-ben.
A lekérési kiszolgáló csomagolása előtt távolítsa el a **{Module Version}** mappát, hogy `{Module Folder}\DscResources\{DSC Resource Folder}\`az elérési út legyen.
Ezzel a módosítással zip a mappát a fent leírtak szerint, és helyezze el ezeket a ZIP-fájlokat a **ModulePath** mappába.

A `New-DscChecksum {module zip file}` használatával hozzon létre egy ellenőrzőösszeg-fájlt az újonnan hozzáadott modulhoz.

### <a name="configuration-mof-format"></a>Konfiguráció MOF-formátuma

A konfigurációs MOF-fájlt egy ellenőrzőösszeg-fájllal kell párosítani, hogy a célként megadott csomóponton lévő LCD-eszközök ellenőrizni tudják a konfigurációt.
Ellenőrzőösszeg létrehozásához hívja meg a [New-DscChecksum](/powershell/module/PSDesiredStateConfiguration/New-DscChecksum) parancsmagot.
A parancsmag egy **elérésiút** -paramétert használ, amely meghatározza azt a mappát, ahol a konfigurációs MOF található.
A parancsmag létrehoz egy nevű `ConfigurationMOFName.mof.checksum`ellenőrzőösszeg-fájlt, ahol `ConfigurationMOFName` a a konfigurációs MOF-fájl neve.
Ha a megadott mappában több konfigurációs MOF-fájl található, akkor a mappában található minden egyes konfigurációhoz ellenőrzőösszeg jön létre.
Helyezze a MOF-fájlokat és a hozzájuk tartozó ellenőrzőösszeg-fájlokat a **ConfigurationPath** mappába.

> [!NOTE]
> Ha bármilyen módon módosítja a konfigurációs MOF-fájlt, akkor újra létre kell hoznia az ellenőrzőösszeg-fájlt is.

### <a name="tooling"></a>Eszközök

A lekéréses kiszolgáló telepítésének, ellenőrzésének és felügyeletének megkönnyítéséhez a következő eszközök szerepelnek példaként a xPSDesiredStateConfiguration modul legújabb verziójában:

1. Egy modul, amely segítséget nyújt a lekéréses kiszolgálón való használatra a DSC-erőforrás moduljainak és konfigurációs fájljainak használatához.
   [PublishModulesAndMofsToPullServer.psm1](https://github.com/PowerShell/xPSDesiredStateConfiguration/blob/master/DSCPullServerSetup/PublishModulesAndMofsToPullServer.psm1).
   Példák alább:

    ```powershell
        # Example 1 - Package all versions of given modules installed locally and MOF files are in c:\LocalDepot
         $moduleList = @('xWebAdministration', 'xPhp')
         Publish-DSCModuleAndMof -Source C:\LocalDepot -ModuleNameList $moduleList

         # Example 2 - Package modules and mof documents from c:\LocalDepot
         Publish-DSCModuleAndMof -Source C:\LocalDepot -Force
    ```

1. A lekérési kiszolgálót érvényesítő parancsfájl megfelelően van konfigurálva. [PullServerSetupTests. ps1](https://github.com/PowerShell/xPSDesiredStateConfiguration/blob/master/DSCPullServerSetup/PullServerDeploymentVerificationTest/PullServerSetupTests.ps1).

## <a name="community-solutions-for-pull-service"></a>Közösségi megoldások a lekéréses szolgáltatáshoz

A DSC-Közösség több megoldást hozott létre a lekéréses szolgáltatás protokolljának megvalósításához.
A helyszíni környezetek esetében ezek az ajánlatok lekéréses szolgáltatásokkal kapcsolatos képességeket és lehetőséget biztosítanak a Közösségnek a növekményes fejlesztésekkel való újbóli közreműködés érdekében.

- [Vontatóhajó](https://github.com/powershellorg/tug)
- [DSC-TRÆK](https://github.com/powershellorg/dsc-traek)

## <a name="pull-client-configuration"></a>Ügyfél konfigurációjának lekérése

A következő témakörök részletesen ismertetik a lekéréses ügyfelek beállítását:

- [DSC lekérési ügyfél beállítása konfigurációs azonosító használatával](pullClientConfigID.md)
- [DSC lekérési ügyfél beállítása konfigurációs nevek használatával](pullClientConfigNames.md)
- [Részleges konfigurációk](partialConfigs.md)

## <a name="see-also"></a>Lásd még:

- [A Windows PowerShell kívánt állapotának konfigurálása – áttekintés](../overview/overview.md)
- [Konfigurációk életbe léptetése](enactingConfigurations.md)
- [A DSC jelentéskészítő kiszolgálójának használata](reportServer.md)
- [[MS-DSCPM]: A kívánt állapot konfigurációjának lekérési modellje protokoll](https://msdn.microsoft.com/library/dn393548.aspx)
- [[MS-DSCPM]: A kívánt állapot konfigurációjának lekérése modell protokolljának hibajavításai](https://msdn.microsoft.com/library/mt612824.aspx)
